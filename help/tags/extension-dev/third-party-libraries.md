---
title: Implementieren von Bibliotheken von Drittanbietern
description: Erfahren Sie mehr über die verschiedenen Methoden zum Hosten von Drittanbieter-Bibliotheken in Ihren Adobe Experience Platform-Tag-Erweiterungen.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '1330'
ht-degree: 67%

---

# Implementieren von Bibliotheken von Drittanbietern

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../term-updates.md).

Eines der Hauptziele von Tag-Erweiterungen in Adobe Experience Platform besteht darin, Ihnen die einfache Implementierung vorhandener Marketing-Technologien (Bibliotheken) in Ihre Website zu ermöglichen. Durch die Verwendung von Erweiterungen können Sie Bibliotheken implementieren, die von Inhaltsversandnetzwerken (Content Delivery Network, CDN) von Drittanbietern bereitgestellt werden, ohne die HTML-Daten Ihrer Website manuell bearbeiten zu müssen.

Es gibt verschiedene Methoden zum Hosten von Drittanbieter-Bibliotheken in Ihren Erweiterungen. Dieses Dokument bietet einen Überblick über diese verschiedenen Implementierungsmethoden einschließlich der Vor- und Nachteile jeder Methode.

## Voraussetzungen

Dieses Dokument setzt ein Verständnis der Erweiterungen innerhalb von Tags voraus, einschließlich dessen, was sie tun können und wie sie zusammengestellt werden. Weiterführende Informationen dazu finden Sie unter [Erweiterungsentwicklung – Übersicht](./overview.md).

## Ladevorgang für Basis-Code

Außerhalb des Kontexts von Tags ist es wichtig zu verstehen, wie Marketing-Technologien normalerweise auf einer Website geladen werden. Drittanbieter von Bibliotheken stellen einen Code-Ausschnitt (den so genannten Basis-Code) bereit, der in den HTML-Code Ihrer Website eingebettet werden muss, damit die Funktionen der Bibliothek geladen werden können.

Im Allgemeinen führen Basis-Codes für Marketing-Technologien beim Laden auf Ihrer Website einen Prozess ähnlich dem folgenden aus:

1. Richten Sie eine globale Funktion ein, durch die mit der Bibliothek des Anbieters interagiert werden kann.
1. Laden Sie die Bibliothek des Anbieters.
1. Führen Sie zu Konfigurations- und Tracking-Zwecken eine Reihe von in die Warteschlange gestellten Erstaufrufen an die globale Funktion aus.

Wenn die globale Funktion zum ersten Mal eingerichtet ist, können Sie die Funktion noch aufrufen, bevor das Laden der Bibliothek abgeschlossen ist. Alle von Ihnen ausgeführten Aufrufe werden zum Warteschlangenmechanismus des Basis-Codes hinzugefügt und nach dem Laden der Bibliothek in sequenzieller Reihenfolge ausgeführt.

Nach dem Laden der Bibliothek wird die globale Funktion durch eine neue ersetzt, die die Warteschlange umgeht und stattdessen alle zukünftigen Aufrufe der Funktion sofort verarbeitet.

### Beispiel für Basis-Code

Das folgende JavaScript ist ein Beispiel für einen nicht minimierten Basis-Code für das [Pinterest-Konversions-Tag](https://developers.pinterest.com/docs/ad-tools/conversion-tag/?), der später in diesem Dokument referenziert wird, um zu veranschaulichen, wie der Basis-Code für verschiedene Implementierungsstrategien mit Tags angepasst werden kann:

```js
!function(scriptUrl) {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = '3.0';
    var scriptElement = document.createElement('script');
    scriptElement.async = true;
    scriptElement.src = scriptUrl;
    var firstScriptElement = 
      document.getElementsByTagName('script')[0];
    firstScriptElement.parentNode.insertBefore(
      scriptElement, firstScriptElement
    );
  }
}('https://s.pinimg.com/ct/core.js');
pintrk('load', 'YOUR_TAG_ID');
pintrk('page');
```

Zusammenfassend stellt der oben stehende Basis-Code einen [unmittelbar aufgerufenen Funktionsausdruck (Immediately Invoked Function Expression, IIFE)](https://developer.mozilla.org/de-DE/docs/Glossary/IIFE) bereit, der eine globale Funktion zur Interaktion mit der Bibliothek (`window.pintrk`) erstellt. Außerdem wird der Wert von `https://s.pinimg.com/ct/core.js` für den Ort, an dem sich die Bibliothek befindet, einer Variablen `scriptURL` zugewiesen. Wie bereits erläutert, werden alle Funktionen, die vor dem Laden der Bibliothek aufgerufen werden, in eine Warteschlange (`window.pintrk.queue`) verschoben, um eine nach der anderen ausgeführt zu werden, sobald die Bibliothek verfügbar ist.

Der folgende Teil des Basis-Codes ist am relevantesten, wenn es darum geht, zu verstehen, wie die Bibliothek auf Ihrer Website geladen wird:

```js
var scriptElement = document.createElement("script");
scriptElement.async = true;
scriptElement.src = scriptUrl;
var firstScriptElement = 
  document.getElementsByTagName("script")[0];
firstScriptElement.parentNode.insertBefore(
  scriptElement, firstScriptElement
);
```

Der Basis-Code erstellt ein Skriptelement, legt es so fest, dass es asynchron geladen wird, und setzt die URL `src` auf `https://s.pinimg.com/ct/core.js`. Anschließend wird das Skriptelement zu dem Dokument hinzugefügt, indem es vor dem ersten bereits im Dokument enthalten Skriptelement eingefügt wird.

## Implementierungsoptionen für Tags

In den folgenden Abschnitten werden die verschiedenen Möglichkeiten zum Laden von Bibliotheken von Anbietern in Erweiterungen anhand des zuvor gezeigten Pinterest-Basis-Codes veranschaulicht. Bei jedem dieser Beispiele wird ein [Aktionstyp für eine Web-Erweiterung](./web/action-types.md) erstellt, der die Bibliothek auf Ihre Website lädt.

>[!NOTE]
>
>In den folgenden Beispielen werden zwar Aktionstypen für Demonstrationszwecke verwendet, Sie können aber dieselben Prinzipien auf alle Funktionen anwenden, die die Tag-Bibliothek auf Ihre Site laden.


Die folgenden Methoden werden behandelt:

- [Implementieren von Bibliotheken von Drittanbietern](#implementing-third-party-libraries)
   - [Voraussetzungen  ](#prerequisites)
   - [Ladevorgang für Basis-Code](#base-code-loading-process)
      - [Beispiel für Basis-Code](#base-code-example)
   - [Implementierungsoptionen für Tags](#tags-implementation-options)
      - [Laden zur Laufzeit vom Anbieter-Host {#vendor-host}](#load-at-runtime-from-the-vendor-host-vendor-host)
      - [Zur Laufzeit vom Tag-Bibliotheks-Host laden](#load-at-runtime-from-the-tag-library-host)
      - [Bibliothek direkt einbetten](#embed-the-library-directly)
   - [Nächste Schritte](#next-steps)

### Laden zur Laufzeit vom Anbieter-Host {#vendor-host}

Die am häufigsten verwendete Methode zum Hosten von Bibliotheken von Anbietern ist die Verwendung des CDN (Content Delivery Network) des Anbieters. Da der Basis-Code für die meisten Bibliotheken von Anbietern bereits so konfiguriert ist, dass die Bibliothek vom CDN des Anbieters geladen wird, können Sie Ihre Erweiterung so einrichten, dass die Bibliothek vom selben Speicherort geladen wird.

Dieser Ansatz ist in der Regel am einfachsten zu verwalten, da alle Aktualisierungen, die an der Datei im CDN vorgenommen werden, automatisch von der Erweiterung geladen werden.

Bei Verwendung dieser Methode können Sie den gesamten Basis-Code einfach direkt in einen Aktionstyp wie folgt einfügen:

```js
module.exports = function() {
  !function(scriptUrl) {
    if (!window.pintrk) {
      window.pintrk = function() {
        window.pintrk.queue.push(
          Array.prototype.slice.call(arguments)
        );
      };
      window.pintrk.queue = []; 
      window.pintrk.version = "3.0";
      var scriptElement = document.createElement("script");
      scriptElement.async = true;
      scriptElement.src = scriptUrl;
      var firstScriptElement = 
        document.getElementsByTagName("script")[0];
      firstScriptElement.parentNode.insertBefore(
        scriptElement, firstScriptElement
      );
    }
  }("https://s.pinimg.com/ct/core.js");
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

Optional können Sie weitere Schritte unternehmen, um diese Implementierung zu überarbeiten. Da die Variablen `scriptElement` und `firstScriptElement` jetzt auf die exportierte Funktion übertragen werden, können Sie die IIFE entfernen, da diese Variablen nicht das Risiko bergen, global zu werden.

Darüber hinaus stellen Tags mehrere [Kernmodule](./web/core.md) bereit, bei denen es sich um Hilfsprogramme handelt, die von jeder beliebigen Erweiterung verwendet werden können. Das Modul `@adobe/reactor-load-script` lädt ein Skript von einem Remote-Speicherort, indem ein Skriptelement erstellt und zum Dokument hinzugefügt wird. Mithilfe dieses Moduls für den Ladevorgang des Skripts können Sie den Aktions-Code noch weiter umgestalten:

```js
var loadScript = require('@adobe/reactor-load-script');
var scriptUrl = 'https://s.pinimg.com/ct/core.js';
module.exports = function() {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = "3.0";
    loadScript(scriptUrl);   
  }
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

### Zur Laufzeit vom Tag-Bibliotheks-Host laden

Die Verwendung des CDN eines Anbieters für das Hosten von Bibliotheken birgt mehrere Risiken: das CDN kann ausfallen, die Datei kann jederzeit mit einem kritischen Fehler aktualisiert werden oder die Datei kann zu unguten Zwecken kompromittiert werden.

Um diese Bedenken auszuräumen, können Sie die Bibliothek des Anbieters als separate Datei in Ihre Erweiterung aufnehmen. Die Erweiterung kann dann so konfiguriert werden, dass die Datei neben der Haupt-Tag-Bibliothek gehostet wird. Zur Laufzeit lädt die Erweiterung dann die Bibliothek des Anbieters von dem Server, der die Hauptbibliothek für die Website bereitgestellt hat.

>[!IMPORTANT]
>
>In einigen Fällen kann die Bibliothek des Anbieters zusätzlichen Code von Drittanbieter-Servern laden, wie dies bei der Bibliothek des Pinterest-Anbieters der Fall ist. In diesen Fällen kann es sein, dass die Bündelung der Bibliothek des Anbieters mit Ihrer Erweiterung nicht alle Bedenken wegen Risiken vollständig ausräumt.

Um dies zu implementieren, müssen Sie zunächst die Bibliothek des Anbieters auf Ihren Computer herunterladen. Bei Pinterest befindet sich die Bibliothek des Anbieters unter [https://s.pinimg.com/ct/core.js](https://s.pinimg.com/ct/core.js). Nachdem Sie die Datei heruntergeladen haben, müssen Sie sie in Ihrem Erweiterungsprojekt ablegen. Im folgenden Beispiel erhält die Datei den Namen `pinterest.js` und befindet sich in einem Ordner `vendor` im Projektverzeichnis.

Sobald sich die Bibliotheksdatei in Ihrem Projekt befindet, müssen Sie Ihr [Erweiterungsmanifest](./manifest.md) (`extension.json`) aktualisieren, um anzugeben, dass die Bibliothek des Anbieters zusammen mit der Haupt-Tag-Bibliothek bereitgestellt werden soll. Dazu fügen Sie den Pfad zur Bibliotheksdatei in einem `hostedLibFiles`-Array hinzu:

```json
{
  "hostedLibFiles": ["vendor/pinterest.js"]
}
```

Schließlich müssen Sie Ihren Aktions-Code so konfigurieren, dass die Bibliothek des Anbieters von demselben Server geladen wird, auf dem die Hauptbibliothek gehostet wird. Im folgenden Beispiel wird der im [vorherigen Abschnitt](#vendor-host) erstellte Aktions-Code als Ausgangspunkt verwendet. Bei Verwendung des [Turbinenobjekts](./turbine.md) müssen Sie den Dateinamen (ohne Pfad) der Lieferantendatei wie folgt übergeben:

```js
var loadScript = require('@adobe/reactor-load-script');
var scriptUrl = turbine.getHostedLibFileUrl('pinterest.js');
module.exports = function() {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = "3.0";
    loadScript(scriptUrl);   
  }
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

Beachten Sie, dass Sie bei Verwendung dieser Methode Ihre heruntergeladene Datei des Anbieters manuell aktualisieren müssen, sobald die Bibliothek auf seinem CDN aktualisiert wird, und die Änderungen an einer neuen Version Ihrer Erweiterung freigeben müssen.

### Bibliothek direkt einbetten

Sie können das vollständige Laden der Bibliothek des Anbieters umgehen, indem Sie den Bibliotheks-Code direkt in den Aktionscode selbst einbetten, wodurch er effektiv Teil der Haupt-Tag-Bibliothek wird. Diese Methode erhöht zwar die Größe der Hauptbibliothek, vermeidet aber die Notwendigkeit einer zusätzlichen HTTP-Anfrage zum Abrufen einer separaten Datei.

Mithilfe des im [vorherigen Abschnitt](#vendor-host) erstellten Aktions-Codes können Sie die Zeile, in der das Skript geladen wird, durch den Inhalt des Skripts selbst ersetzen:

```js
module.exports = function() {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = "3.0";
    // Paste the full vendor library code here.
  }
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

## Nächste Schritte

Dieses Dokument bietet einen Überblick über die verschiedenen Methoden zum Hosten von Drittanbieter-Bibliotheken in Ihren Tag-Erweiterungen. Während sich die gegebenen Beispiele auf Bibliotheken konzentriert haben, gelten diese Verfahren für jeden Code, den Ihre Erweiterung verwenden kann.

Weitere Informationen zu den Werkzeugen zum Konfigurieren der Erweiterungen, einschließlich Aktionstypen, dem Erweiterungsmanifest, Kernmodulen und dem Turbinenobjekt, finden Sie in der Dokumentation, die in diesem Handbuch verlinkt ist.
