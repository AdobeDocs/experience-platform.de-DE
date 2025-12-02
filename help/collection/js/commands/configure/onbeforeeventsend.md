---
title: onBeforeEventSend
description: Erfahren Sie, wie Sie Web SDK so konfigurieren, dass eine JavaScript-Funktion registriert wird, mit der Sie die Daten ändern können, die Sie unmittelbar vor dem Senden dieser Daten an Adobe senden.
exl-id: 945f4fa1-380c-46aa-a92a-bbcfd6644751
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# `onBeforeEventSend`

Mit dem `onBeforeEventSend` Callback können Sie eine JavaScript-Funktion registrieren, die die Daten ändern kann, die Sie unmittelbar vor dem Senden dieser Daten an Adobe senden. Dieser Rückruf ermöglicht es Ihnen, das `xdm`- oder `data`-Objekt zu bearbeiten, einschließlich der Möglichkeit, Elemente hinzuzufügen, zu bearbeiten oder zu entfernen. Sie können das Senden von Daten auch ganz abbrechen, z. B. bei erkanntem Client-seitigem Bot-Traffic.

>[!WARNING]
>
>Dieser Callback ermöglicht die Verwendung von benutzerdefiniertem Code. Wenn ein Code, den Sie in den Callback einbeziehen, eine nicht abgefangene Ausnahme auslöst, wird die Verarbeitung für das Ereignis angehalten und **Daten werden nicht an Adobe gesendet.**

Registrieren Sie den `onBeforeEventSend` Callback, wenn Sie den `configure` Befehl ausführen. Sie können den Namen der `content` in einen beliebigen Wert ändern, indem Sie die Parametervariable innerhalb der Inline-Funktion ändern.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeEventSend: function(content) {
    // Use nullish coalescing assignments to add a new value
    content.xdm._experience ??= {};
    content.xdm._experience.analytics ??= {};
    content.xdm._experience.analytics.customDimensions ??= {};
    content.xdm._experience.analytics.customDimensions.eVars ??= {};
    content.xdm._experience.analytics.customDimensions.eVars.eVar1 = "Analytics custom value";
    
    // Use optional chaining to change an existing value
    if(content.xdm.web?.webPageDetails) content.xdm.web.webPageDetails.URL = content.xdm.web.webPageDetails.URL.toLowerCase();
    
    // Remove an existing value
    if(content.xdm.web?.webReferrer) delete content.xdm.web.webReferrer.URL;
    
    // Return true to immediately send data
    if (sendImmediate == true) {
      return true;
    }
    
    // Return false to immediately cancel sending data
    if(myBotDetector.isABot()){
      return false;
    }
    
    // Assign the value in the 'cid' query string to the tracking code XDM element
    content.xdm.marketing ??= {};
    content.xdm.marketing.trackingCode = new URLSearchParams(window.location.search).get('cid');
  }
});
```

Anstelle einer Inline-Funktion können Sie auch eine eigene Funktion registrieren.

```js
function lastChanceLogic(content) {
  content.xdm.application ??= {};
  content.xdm.application.name = "App name";
}

alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeEventSend: lastChanceLogic
});    
```

## Konfigurieren eines -Ereignisses vor dem Senden eines Callbacks mithilfe der Tag-Erweiterung „Web SDK&quot;

Diese Einstellungen können in der Tag-Erweiterung „Web SDK&quot; mithilfe der [Konfigurationseinstellungen für die Datenerfassung“ konfiguriert &#x200B;](/help/tags/extensions/client/web-sdk/configure/data-collection.md#on-before-event-send-callback).
