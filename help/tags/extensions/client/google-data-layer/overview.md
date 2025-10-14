---
title: Google-Datenschicht-Erweiterung
description: Machen Sie sich mit der Tag-Erweiterung "Google Client Data Layer“ in Adobe Experience Platform vertraut.
exl-id: 7990351d-8669-432b-94a9-4f9db1c2b3fe
source-git-commit: c61afdc2c3df98a0ef815d7cb034ba2907c52908
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 12%

---

# Google-Datenschicht-Erweiterung

Mit der Google-Datenschichterweiterung können Sie eine Google-Datenschicht in Ihrer Tags-Implementierung verwenden. Die Erweiterung kann unabhängig oder gleichzeitig mit Google-Lösungen und mit der Open-Source-Bibliothek [Datenschicht-Helper) von Google verwendet &#x200B;](https://github.com/google/data-layer-helper).

Die Helper-Bibliothek bietet ähnliche ereignisgesteuerte Funktionen wie die Adobe-Client-Datenschicht (ACDL). Die Datenelemente, Regeln und Aktionen der Google-Datenschichterweiterung bieten ähnliche Funktionen wie die [ACDL-Erweiterung](../client-data-layer/overview.md).

## Installation

Um die Erweiterung zu installieren, navigieren Sie in der Datenerfassungs-UI zum Erweiterungskatalog und wählen Sie **[!UICONTROL Google-Datenschicht]** aus.

Nach der Installation erstellt die Erweiterung bei jedem Laden der Adobe Experience Platform Tags-Bibliothek eine Datenschicht oder greift darauf zu.

## Erweiterungsansicht

Die Erweiterungskonfiguration kann verwendet werden, um den Namen der Datenschicht zu definieren, die die Erweiterung verwendet. Wenn beim Laden von Adobe Experience Platform-Tags keine Datenschicht mit dem konfigurierten Namen vorhanden ist, erstellt die Erweiterung eine.

Der standardmäßige Datenschichtname ist der Google-Standardname `dataLayer`.

>[!NOTE]
>
>Es spielt keine Rolle, ob Google- oder Adobe-Code zuerst geladen wird und die Datenschicht erstellt. Beide Systeme verhalten sich gleich: Erstellen Sie die Datenschicht, wenn sie nicht vorhanden ist, oder verwenden Sie die vorhandene Datenschicht.

## Events

>[!NOTE]
>
>Das Wort _Ereignis_ wird überladen, wenn eine ereignisgesteuerte Datenschicht in Adobe Experience Platform Tags verwendet wird. _Ereignisse_ können sein:
> - Adobe Experience Platform Tags-Ereignisse (Bibliothek geladen usw.).
> - JavaScript-Ereignisse.
> - Daten, die mit dem Schlüsselwort _event“ an_ Datenschicht gepusht werden.

Die Erweiterung bietet Ihnen die Möglichkeit, auf Änderungen in der Datenschicht zu warten.

>[!NOTE]
>
>Es ist wichtig, sich mit der Verwendung des _event_-Schlüsselworts vertraut zu machen, wenn Daten an eine Google-Datenschicht gepusht werden, ähnlich wie bei der Adobe-Client-Datenschicht. Das _event_-Schlüsselwort ändert das Verhalten der Google-Datenschicht und damit dieser Erweiterung.\
> Bitte lesen Sie die Google-Dokumentation oder recherchieren Sie, wenn Sie sich in diesem Punkt nicht sicher sind.

### Google-Ereignistypen

Google unterstützt zwei Methoden zum Pushen von Ereignissen: Google Tag Manager mit der `push()` und Google Analytics 4 mit der `gtag()`.

Google Data Layer-Erweiterungsversionen vor 1.2.1 unterstützten nur von `push()` erstellte Ereignisse, wie in den Code-Beispielen auf dieser Seite dargestellt.

Die Versionen 1.2.1 und höher unterstützen Ereignisse, die mit `gtag()` erstellt wurden.  Dies ist optional und kann im Dialogfeld Erweiterungskonfiguration aktiviert werden.

Weitere Informationen zu `push()`- und `gtag()` finden Sie in der [Dokumentation zu Google](https://developers.google.com/analytics/devguides/collection/ga4/reference/events?client_type=gtag).  Weitere Informationen finden Sie in den Konfigurations- und Regeldialogen der Erweiterung.

### Überwachen aller Push-Benachrichtigungen an die Datenschicht

Wenn Sie diese Option auswählen, überwacht Ihr Ereignis-Listener alle Änderungen an der Datenschicht.

### Überwachen von Push-Benachrichtigungen beim Ausschluss von Ereignissen

Wenn Sie diese Option auswählen, überwacht Ihr Ereignis-Listener alle Push-Benachrichtigungen von Daten an die Datenschicht, mit Ausnahme von Ereignissen.

Das folgende Beispiel für Push-Ereignisse wird vom Listener verfolgt:

```js
dataLayer.push({"data":"something"})
```

Die folgenden Beispiel-Push-Ereignisse werden vom Listener nicht verfolgt:

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

### Auf alle Ereignisse überwachen

Wenn Sie diese Option auswählen, überwacht Ihr Ereignis-Listener alle Ereignisse, die an die Datenschicht gepusht werden.

Das folgende Beispiel für Push-Ereignisse wird vom Listener verfolgt:

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

Das folgende Beispiel für ein Push-Ereignis wird vom Listener nicht verfolgt:

```js
dataLayer.push({"data":"something"})
```

### Überwachen eines bestimmten Ereignisses

Wenn Sie ein Ereignis angeben, verfolgt der Ereignis-Listener alle Ereignisse, die mit einer bestimmten Zeichenfolge übereinstimmen.

Wenn Sie beispielsweise `myEvent` bei Verwendung dieser Konfiguration festlegen, verfolgt der Listener nur das folgende Push-Ereignis:

```js
dataLayer.push({"event":"myEvent"})
```

Ein (ECMAScript/JavaScript)-Regex kann verwendet werden, um Ereignisnamen abzugleichen.

Wenn Sie beispielsweise „myEvent\d“ festlegen, werden `myEvent` mit einer Ziffer (\d) verfolgt:

```js
dataLayer.push({"event":"myEvent1"})
dataLayer.push({"event":"myEvent2"})
```

## Aktionen

### Pushen zur Datenschicht {#push-to-data-layer}

Die Erweiterung bietet zwei Aktionen zum Pushen von JSON in die Datenschicht: ein Freitextfeld zum manuellen Erstellen der Push-JSON und ab Version 1.2.0 ein Mehrfeld-Dialogfeld für Schlüsselwerte.

#### Freitext-JSON

Die Freitext-Aktion ermöglicht die direkte Verwendung von Datenelementen in der JSON-Datei. Innerhalb des JSON-Editors sollten Datenelemente mit Prozentnotation referenziert werden. Beispiel: `%dataElementName%`.

```json
{
  "page": {
    "url": "%url%",
    "previous_url": "%previous_url%",
    "concatenated_values": "static string %dataElement%"
  }
}
```

#### Schlüssel-Wert-Mehrfachfeld

Das neuere Dialogfeld für Mehrfeld-Schlüssel ist eine benutzerfreundlichere Oberfläche, mit der eine Push-Benachrichtigung konfiguriert werden kann, ohne dass manuell JSON geschrieben werden muss.

### Google DL Auf berechneten Status zurücksetzen

Die Erweiterung bietet eine Aktion zum Zurücksetzen der Datenschicht . Bei Verwendung in einer Regel, die eine Änderung der Google-Datenschicht verarbeitet, wird die Datenschicht zum Zeitpunkt des Auslösens der Regel auf den berechneten Status der Datenschicht zurückgesetzt. Wenn die Aktion in einer Regel verwendet wird, die keine Änderung der Google-Datenschicht verarbeitet, wird die Datenschicht durch die Aktion geleert.

## Datenelemente

Das bereitgestellte Datenelement kann während der Ausführung einer Regel verwendet werden, die durch eine Google-Datenschichtänderung (Push-Ereignis) ausgelöst wird, oder in einer nicht zugehörigen Regel, wie „Bibliothek geladen“. Im ersteren Fall gibt das Datenelement einen Wert zurück, der aus dem berechneten Status zum Zeitpunkt des Datenschichtwechsels übernommen wurde. In letzterem Fall wird der berechnete Status zum Zeitpunkt der Regelausführung verwendet.

Mit einem Umschalter können Sie auswählen, ob das Datenelement Werte aus dem gesamten berechneten Status oder nur aus Ereignisinformationen zurückgeben soll (wenn es in einer durch eine Datenschichtänderung ausgelösten Regel verwendet wird).

Das Datenelement kann daher Folgendes zurückgeben:

- Leeres Feld: berechneter Status der Datenschicht.
- Feld mit Schlüssel (z. B. page.previous_url im obigen Beispiel): Wert des Schlüssels im Ereignisobjekt oder im berechneten Status.

## Zusätzliche Informationen

Die Datenelement- und Ereignisdialoge der Erweiterung enthalten detaillierte Nutzungsinformationen und Beispiele.

Weitere allgemeine Informationen finden Sie in der [Projekt-README](https://github.com/adobe/reactor-extension-googledatalayer/blob/main/README.md)
