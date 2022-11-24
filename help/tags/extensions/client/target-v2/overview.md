---
title: Adobe Target v2-Erweiterung – Übersicht
description: Machen Sie sich mit der Tag-Erweiterung „Adobe Target v2“ in Adobe Experience Platform vertraut.
exl-id: 8f491d67-86da-4e27-92bf-909cd6854be1
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '1356'
ht-degree: 93%

---

# Adobe Target v2-Erweiterung – Übersicht

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

Verwenden Sie diese Referenz, um Informationen zu den verfügbaren Optionen beim Erstellen einer Regel mithilfe dieser Erweiterung zu erhalten.

## Konfigurieren der Adobe Target-Erweiterung Version 2

>[!IMPORTANT]
>
>Für die Adobe Target-Erweiterung ist at.js 2.x erforderlich.

Wenn die Adobe Target-Erweiterung noch nicht installiert ist, öffnen Sie die Eigenschaft, wählen Sie dann **[!UICONTROL Mixin > Katalog]**, bewegen Sie den Mauszeiger über die Target-Erweiterung und wählen Sie **[!UICONTROL Installieren]** aus.

Öffnen Sie zum Konfigurieren der Erweiterung die Registerkarte „Erweiterungen“, bewegen Sie den Mauszeiger über die Erweiterung und wählen Sie dann **[!UICONTROL Konfigurieren]** aus.

![](../../../images/targetv2config.png)

### at.js-Einstellungen

All Ihre at.js-Einstellungen mit Ausnahme der Zeitüberschreitung werden automatisch aus Ihrer at.js-Konfiguration in der Target-Benutzeroberfläche abgerufen. Die Erweiterung ruft nur Einstellungen von der Target-Benutzeroberfläche ab, wenn sie zum ersten Mal hinzugefügt wird. Daher sollten alle Einstellungen in der Benutzeroberfläche verwaltet werden, wenn zusätzliche Aktualisierungen erforderlich sind.

Die folgenden Konfigurationsoptionen sind verfügbar:

#### Clientcode

Der Clientcode ist die Konto-ID von Target. Der entsprechende Wert sollte nahezu immer als Standardwert beibehalten werden. Er kann mithilfe von Datenelementen geändert werden.

#### Organisations-ID

Diese ID ordnet die Implementierung Ihrem Adobe Experience Cloud-Konto zu. Der entsprechende Wert sollte nahezu immer als Standardwert beibehalten werden. Er kann mithilfe von Datenelementen geändert werden.

#### Serverdomäne

Die Serverdomain bezieht sich auf die Domain, an die die Target-Anforderungen gesendet werden. Der entsprechende Wert sollte nahezu immer als Standardwert beibehalten werden.

#### DSGVO-Opt-in

Sofern aktiviert, bietet Adobe Target eine Opt-in-Funktion, um Ihre Strategie für das Genehmigungs-Management zu unterstützen. Mit der Opt-in-Funktion können Kunden steuern, wie und wann das Target-Tag ausgelöst wird. Weitere Informationen zur Adobe-Teilnahme finden Sie unter [Datenschutz und Datenschutz-Grundverordnung (DSGVO)](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html?lang=de).

#### Zeitüberschreitung (ms)

Wenn die Antwort von Target nicht innerhalb des definierten Zeitraums empfangen wird, erfolgt eine Zeitüberschreitung für die Anfrage, und der Standardinhalt wird angezeigt. Während der Sitzung des Besuchers wird weiter versucht, Anfragen vorzunehmen. Die Standardeinstellung lautet 3000 ms und kann von der auf der Target-Benutzeroberfläche konfigurierten Zeitüberschreitung abweichen.

Weitere Informationen zur Funktionsweise der Zeitüberschreitungseinstellung finden Sie in der [Hilfe zu Adobe Target](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/deploy-at-js/implementing-target-without-a-tag-manager.html?lang=de).

## Aktionstypen für die Target-Erweiterung

In diesem Abschnitt werden die in der Target-Erweiterung verfügbaren Aktionstypen beschrieben.

Die Target-Erweiterung enthält die folgenden Aktionen im Then-Teil einer Regel:

### Target laden

Fügen Sie diese Aktion Ihrer Tag-Regel hinzu, wenn es sinnvoll ist, Target im Kontext Ihrer Regel zu laden. Dadurch wird die at.js-Bibliothek in die Seite geladen. Bei den meisten Implementierungen sollte Target auf jeder Seite Ihrer Site geladen werden. Adobe empfiehlt, die Aktion „Target laden“ nur zu verwenden, wenn ihr ein Target-Aufruf vorangestellt ist. Andernfalls könnten Fehler auftreten, wie z. B. die Verzögerung des Analytics-Aufrufs.

Es ist keine Konfiguration erforderlich.

### Laden von Target mit On-Device Decisioning

Fügen Sie diese Aktion Ihrer Tag-Regel hinzu, wenn es im Kontext Ihrer Regel sinnvoll ist, Target mit [Entscheidungsfindung auf dem Gerät](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/on-device-decisioning/on-device-decisioning.html?lang=de) zu laden. Dadurch wird die at.js-Bibliothek mit aktiviertem On-Device Decisioning in die Seite geladen. Bei den meisten Implementierungen sollte Target auf jeder Seite Ihrer Site geladen werden. Adobe empfiehlt, die Aktion „Target mit On-Device Decisioning laden“ nur zu verwenden, wenn ihr ein Target-Aufruf vorangestellt ist. Andernfalls könnten Fehler auftreten, wie z. B. die Verzögerung des Analytics-Aufrufs.

Es ist keine Konfiguration erforderlich.

### Hinzufügen von Parametern zu allen Anfragen

Dieser Aktionstyp ermöglicht das Hinzufügen von Parametern zu allen Target-Anfragen. Die Aktion „Target laden“ muss vorher verwendet werden.

1. Geben Sie den Namen und den Wert eines beliebigen Parameters an, den Sie hinzufügen möchten.
1. Klicken Sie auf das Symbol zum Hinzufügen, um weitere Parameter hinzuzufügen.

### Hinzufügen von Parametern zur Seitenladeanfrage

Mit diesem Aktionstyp können Parameter gezielt zu Ihren Seitenladeanfragen hinzugefügt werden. Die Aktion „Target laden“ muss vorher verwendet werden.

1. Geben Sie den Namen und den Wert eines beliebigen Parameters an, den Sie hinzufügen möchten.
1. Klicken Sie auf das Symbol zum Hinzufügen, um weitere Parameter hinzuzufügen.

### Auslösen einer Seitenladeanforderung

Mit diesem Aktionstyp kann Target eine Anfrage auslösen, wenn Ihre Seite geladen wird. Die Aktion „Target laden“ muss vorher verwendet werden.

Geben Sie an, ob Sie die Ausblendung des Textkörpers aktivieren möchten, um Flimmern zu verhindern. Geben Sie außerdem den Stil an, der beim Ausblenden des Textkörperelements verwendet wird. Die folgenden Optionen sind verfügbar:

* **Ausblendung des Textkörpers:** Sie können diese Einstellung aktivieren oder deaktivieren. Der Standardwert lautet „Aktiviert“, was bedeutet, dass der HTML-TEXTKÖRPER ausgeblendet wird.
* **Ausgeblendeter Textkörperstil:** Der Standardwert lautet „body{opacity:0}“. Dieser Wert kann abgeändert werden, beispielsweise zu body{display:none}.

Weitere Informationen finden Sie in der [Onlinehilfe zu Target](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/mbox-implement/advanced-mboxjs-settings.html?lang=de).

### Auslösen einer Ansicht

Die Aktion „Auslösen einer Ansicht“ kann immer aufgerufen werden, wenn eine neue Seite geladen wird oder wenn eine Komponente auf einer Seite erneut gerendert wird. Das Auslösen einer Ansicht sollte für Single Page Applications implementiert werden.

1. Geben Sie den Namen der Ansicht an, die ausgelöst werden muss.
1. Geben Sie an, ob das Auslösen der Ansicht einer Impression für das Reporting zugewiesen werden soll, indem Sie das Seitenkontrollkästchen markieren. Wenn die Ansicht mit einer Komponente korreliert wird, die erneut gerendert wird, und nicht einer Impression für das Reporting zugeschrieben wird, lassen Sie das Seitenkontrollkästchen deaktiviert.

Weitere Informationen zum Auslösen einer Ansicht finden Sie in der [`triggerView()` Hilfedokumentation](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/functions-overview/adobe-target-triggerview-atjs-2.html?lang=de).

## Grundlegende Adobe Target-Implementierung

Nachdem die Target-Erweiterung installiert wurde, erstellen Sie mindestens eine Regel, um sie ordnungsgemäß zu implementieren. Sie müssen zuerst die Target-Bibliothek (at.js) laden, die Parameter angeben, die Sie mit der Seitenladeanfrage verwenden möchten, und die Seitenladeanfrage auslösen.

Eine Target-Regel mit dieser grundlegenden Implementierung sieht folgendermaßen aus:

![](../../../images/targetv2deploy.png)

Nach dem Speichern dieser Regel müssen Sie sie einer Bibliothek hinzufügen und erstellen/bereitstellen, damit Sie das Verhalten testen können.

## Adobe Target-Erweiterung mit einer asynchronen Implementierung

Tags können asynchron bereitgestellt werden. Wenn Sie die Tag-Bibliothek asynchron laden, in der sich Target befindet, wird Target ebenfalls asynchron geladen. Dieses Szenario wird vollständig unterstützt. Es muss jedoch eine weitere Tatsache beachtet werden.

In asynchronen Implementierungen ist es möglich, dass die Seite das Rendern der Standardinhalte fertig stellt, bevor die Target-Bibliothek vollständig geladen wurde und den Tausch des Inhalts durchgeführt hat. Dies kann zum so genannten „Flimmern“ führen. Dabei wird der Standardinhalt kurz angezeigt, bevor er durch den von Target angegebenen personalisierten Inhalt ersetzt wird. Wenn Sie dieses Flimmern verhindern möchten, empfehlen wir, ein spezielles Code-Fragment zu verwenden, das den Seiteninhalt vorab ausblendet, und das Tag-Bundle asynchron zu laden.

Nachfolgend werden einige Aspekte aufgeführt, die Sie bei Verwendung des vorab ausgeblendeten Ausschnitts beachten sollten:

* Das Fragment muss vor dem Laden des Einbettungs-Codes für den Tag-Header hinzugefügt werden.
* Dieser Code kann von Tags nicht verwaltet werden. Daher muss er der Seite direkt hinzugefügt werden.
* Die Seite wird angezeigt, wenn das früheste der folgenden Ereignisse eintritt:
   * Wenn die globale Seitenladeantwort empfangen wurde
   * Wenn für die Seitenladeanfrage eine Zeitüberschreitung eintritt
   * Wenn für den Ausschnitt selbst eine Zeitüberschreitung eintritt
* Die Aktion &quot;Seitenladeanforderung auslösen&quot;sollte auf allen Seiten verwendet werden, die den vorab ausgeblendeten Ausschnitt verwenden, um die Dauer der Vorab-Ausblendung zu minimieren.
* Die Ausblendung des Textkörpers muss auch in der Aktion &quot;Seitenladeanforderung&quot;in der Seitenladeregel aktiviert sein, die Sie für Target verwenden. Andernfalls bleiben alle Seitenladevorgänge für die Timeout-Zeit ausgeblendet.

Der vorab ausgeblendete Codeausschnitt lautet wie folgt und kann minimiert werden. Die konfigurierbaren Optionen befinden sich am Ende:

```js
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
