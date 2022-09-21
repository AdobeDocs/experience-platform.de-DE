---
title: Adobe Target-Erweiterung – Übersicht
description: Erfahren Sie mehr über die Tag-Erweiterung „Adobe Target“ in Adobe Experience Platform.
exl-id: b1c5e25b-42ea-4835-b2d4-913fa2536e77
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 95%

---

# Adobe Target-Erweiterung – Übersicht

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

Verwenden Sie diese Referenz, um Informationen zu den verfügbaren Optionen beim Erstellen einer Regel mithilfe dieser Erweiterung zu erhalten.

## Konfigurieren der Adobe Target-Erweiterung

>[!IMPORTANT]
>
> Für die Adobe Target-Erweiterung ist at.js erforderlich. „mbox.js“ wird nicht unterstützt.

Wenn die Adobe Target-Erweiterung noch nicht installiert ist, öffnen Sie die Eigenschaft, wählen Sie dann **[!UICONTROL Mixin > Katalog]**, bewegen Sie den Mauszeiger über die Target-Erweiterung und wählen Sie **[!UICONTROL Installieren]** aus.

Öffnen Sie zum Konfigurieren der Erweiterung die Registerkarte [!UICONTROL Erweiterungen], bewegen Sie den Mauszeiger über die Erweiterung und wählen Sie dann **[!UICONTROL Konfigurieren]** aus.

![](../../../images/ext-target-config.png)

### at.js-Einstellungen

All Ihre at.js-Einstellungen mit Ausnahme der Zeitüberschreitung werden automatisch aus Ihrer at.js-Konfiguration in der Target-Benutzeroberfläche abgerufen. Die Erweiterung ruft nur Einstellungen von der Target-Benutzeroberfläche ab, wenn sie zum ersten Mal hinzugefügt wird. Daher sollten alle Einstellungen in der Benutzeroberfläche verwaltet werden, wenn zusätzliche Aktualisierungen erforderlich sind.

Die folgenden Konfigurationsoptionen sind verfügbar:

#### Clientcode

Der Clientcode ist die Konto-ID von Target. Der entsprechende Wert sollte nahezu immer als Standardwert beibehalten werden.

Kann mithilfe von Datenelementen geändert werden.

#### Organisations-ID

Diese ID ordnet die Implementierung Ihrem Adobe Experience Cloud-Konto zu. Der entsprechende Wert sollte nahezu immer als Standardwert beibehalten werden.

Kann mithilfe von Datenelementen geändert werden.

#### Globaler Mbox-Name

Zeigt den Namen Ihrer globalen Target-Anfrage an. Standardmäßig lautet dieser Name „target-global-mbox“, es sei denn, Sie haben den Namen auf der Target-Benutzeroberfläche vor dem Hinzufügen der Erweiterung geändert.

Kann mithilfe von Datenelementen geändert werden.

#### Server-Domain

Die Domain, an die Target-Anfragen gesendet werden. Der entsprechende Wert sollte nahezu immer als Standardwert beibehalten werden.

#### Domain-übergreifend

Legt fest, wo Target Cookies in den Browsern einrichtet.

* **Deaktiviert:** Legt die Cookies nur für die Erstanbieter-Domain fest. Dies ist die typische Einstellung.
* **Aktiviert:** Richtet Cookies sowohl auf der Erstanbieter-Domain als auch auf der Target-Drittanbieter-Domain (der „Server-Domain“) ein.

#### Zeitüberschreitung (ms)

Wenn die Antwort von Target nicht innerhalb des definierten Zeitraums empfangen wird, erfolgt eine Zeitüberschreitung für die Anfrage, und der Standardinhalt wird angezeigt. Während der Sitzung des Besuchers wird weiter versucht, Anfragen vorzunehmen. Die Standardeinstellung lautet 3000 ms und kann von der auf der Target-Benutzeroberfläche konfigurierten Zeitüberschreitung abweichen.

Weitere Informationen zur Funktionsweise der Zeitüberschreitungseinstellung finden Sie in der [Hilfe zu Adobe Target](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/deploy-at-js/implementing-target-without-a-tag-manager.html?lang=de).

#### Weitere auf der Target-Benutzeroberfläche verfügbare at.js-Einstellungen

Verschiedene Einstellungen, die auf der Seite [!UICONTROL at.js-Einstellungen bearbeiten] der Target-Benutzeroberfläche verfügbar sind, sind nicht Teil der Target-Erweiterung. Die Vorschläge für die Problemumgehung lauten wie folgt:

* Globale Mbox automatisch erstellen – Diese Einstellung wird durch die Aktion „Globale Mbox auslösen“ in der Target-Erweiterung ersetzt.
* Bibliotheks-Header – Diese Einstellung ist nicht Teil der Target-Erweiterung. Fügen Sie vor der Verwendung der Aktion „Target laden“ Code, der vor at.js geladen werden muss, in eine Aktion vom Typ „Haupterweiterung>Benutzerdefinierter Code“ ein.
* Bibliotheksfußfzeile – Diese Einstellung ist nicht Teil der Target-Erweiterung. Fügen Sie nach Verwendung der Aktion „Target laden“ Code, der nach at.js geladen werden muss, in eine Aktion vom Typ „Haupterweiterung>Benutzerdefinierter Code“ ein.

## Aktionstypen für die Target-Erweiterung

In diesem Abschnitt werden die in der Target-Erweiterung verfügbaren Aktionstypen beschrieben.

Die Target-Erweiterung enthält die folgenden Aktionen im Then-Teil einer Regel:

### Target laden

Fügen Sie diese Aktion Ihrer Tag-Regel hinzu, wenn es sinnvoll ist, Target im Kontext Ihrer Regel zu laden. Dadurch wird die at.js-Bibliothek in die Seite geladen. Bei den meisten Implementierungen sollte Target auf jeder Seite Ihrer Site geladen werden.

Es ist keine Konfiguration erforderlich.

### Hinzufügen von Mbox-Parametern

Fügen Sie allen Mbox-Anfragen Parameter hinzu. Die Aktion „Target laden“ muss vorher verwendet werden.

1. Geben Sie den Namen und den Wert eines beliebigen Parameters an, den Sie hinzufügen möchten.
1. Klicken Sie auf das **Plus-Symbol (+)**, um weitere Parameter hinzuzufügen.

### Hinzufügen globaler Mbox-Parameter

Fügen Sie nur Ihren globalen Mbox-Anfragen Parameter hinzu. Die Aktion „Target laden“ muss vorher verwendet werden.

1. Geben Sie den Namen und den Wert eines beliebigen Parameters an, den Sie hinzufügen möchten.
1. Klicken Sie auf das **Plus-Symbol (+)**, um weitere Parameter hinzuzufügen.

### Globale Mbox auslösen

Lösen Sie die globale Mbox auf Ihrer Seite aus. Die Aktion „Target laden“ muss vorher verwendet werden.

Geben Sie an, ob Sie die Ausblendung des Textkörpers aktivieren möchten, um Flackern zu verhindern. Geben Sie außerdem den Stil an, der beim Ausblenden des Textkörperelements verwendet wird.

Die folgenden Optionen sind verfügbar:

* **Ausblendung des Textkörpers:** Sie können diese Einstellung aktivieren oder deaktivieren. Der Standardwert lautet „Aktiviert“, was bedeutet, dass der HTML-TEXTKÖRPER ausgeblendet wird.
* **Ausgeblendeter Textkörperstil:** Der Standardwert lautet `body{opacity:0}`. Dieser Wert kann abgeändert werden, beispielsweise in `body{display:none}`.

Weitere Informationen finden Sie in der [Onlinehilfe zu Target](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/mbox-implement/advanced-mboxjs-settings.html?lang=de).

## Grundlegende Adobe Target-Implementierung

Nachdem die Target-Erweiterung installiert wurde, müssen Sie mindestens eine Regel erstellen, um sie ordnungsgemäß zu implementieren. Sie müssen zuerst die Target-Bibliothek (at.js) laden, die Parameter angeben, die Sie mit der globalen Mbox verwenden möchten, und die globale Mbox auslösen.

Eine Target-Regel mit dieser grundlegenden Implementierung sieht folgendermaßen aus:

![](../../../images/basic_target_implementation.png)

Nach dem Speichern dieser Regel müssen Sie sie einer Bibliothek hinzufügen und erstellen/bereitstellen, sodass Sie das Verhalten testen können.

## Adobe Target-Erweiterung mit einer asynchronen Implementierung

Tags können asynchron bereitgestellt werden. Wenn Sie die Tag-Bibliothek asynchron laden, in der sich Target befindet, wird Target ebenfalls asynchron geladen. Dieses Szenario wird vollständig unterstützt. Es muss jedoch eine weitere Tatsache beachtet werden.

In asynchronen Implementierungen ist es möglich, dass die Seite das Rendern der Standardinhalte beendet, bevor die Target-Bibliothek vollständig geladen wurde und den Austausch des Inhalts durchgeführt hat. Dies kann zum so genannten „Flimmern“ führen. Dabei wird der Standardinhalt kurz angezeigt, bevor er durch den von Target angegebenen personalisierten Inhalt ersetzt wird. Wenn Sie dieses Flimmern verhindern möchten, empfehlen wir, ein spezielles Code-Fragment zu verwenden, das den Seiteninhalt vorab ausblendet, und das Tag-Bundle asynchron zu laden.

Nachfolgend werden einige Aspekte aufgeführt, die Sie bei Verwendung des vorab ausgeblendeten Ausschnitts beachten sollten:

* Das Fragment muss vor dem Laden des Einbettungs-Codes für den Tag-Header hinzugefügt werden.
* Dieser Code kann von Tags nicht verwaltet werden. Daher muss er der Seite direkt hinzugefügt werden.
* Die Seite wird angezeigt, wenn das früheste der folgenden Ereignisse eintritt:
   * Wenn die globale Mbox-Antwort empfangen wurde
   * Wenn für die globale Mbox-Anfrage eine Zeitüberschreitung eintritt
   * Wenn für den Ausschnitt selbst eine Zeitüberschreitung eintritt
* Die Aktion &quot;Globale Mbox auslösen&quot;sollte auf allen Seiten verwendet werden, die den vorab ausgeblendeten Ausschnitt verwenden, um die Dauer der Vorab-Ausblendung zu minimieren.

Der vorab ausgeblendete Codeausschnitt lautet wie folgt und kann minimiert werden. Die konfigurierbaren Optionen befinden sich am Ende:

```javascript
;(function(win, doc, style, timeout) {
  var STYLE_ID = 'at-body-style';

  function getParent() {
    return doc.getElementsByTagName('head')[0];
  }

  function addStyle(parent, id, def) {
    if (!parent) {
      return;
    }

    var style = doc.createElement('style');
    style.id = id;
    style.innerHTML = def;
    parent.appendChild(style);
  }

  function removeStyle(parent, id) {
    if (!parent) {
      return;
    }

    var style = doc.getElementById(id);

    if (!style) {
      return;
    }

    parent.removeChild(style);
  }

  addStyle(getParent(), STYLE_ID, style);
  setTimeout(function() {
    removeStyle(getParent(), STYLE_ID);
  }, timeout);
}(window, document, "body {opacity: 0 !important}", 3000));
```

Standardmäßig wird durch den Ausschnitt der gesamte HTML-TEXTKÖRPER vorab ausgeblendet. In einigen Fällen sollten nur bestimmte HTML-Elemente vorab ausgeblendet werden und nicht die gesamte Seite. Dazu können Sie den Stilparameter anpassen. Führen Sie eine Ersetzung aus, durch die nur bestimmte Teile der Seite vorab ausgeblendet werden.

Wenn beispielsweise zwei Regionen durch die IDs „container-1“ und „container-2“ identifiziert werden, kann der Stil wie folgt ersetzt werden:

```css
#container-1, #container-2 {opacity: 0 !important}
```

Anstelle der Standardeinstellung:

```css
body {opacity: 0 !important}
```

Standardmäßig tritt für den Ausschnitt bei 3000 ms bzw. 3 Sekunden eine Zeitüberschreitung ein. Dieser Wert kann angepasst werden.
