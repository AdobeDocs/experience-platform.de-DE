---
title: onBeforeEventSend
description: Erfahren Sie, wie Sie Web SDK so konfigurieren, dass eine JavaScript-Funktion registriert wird, mit der Sie die Daten ändern können, die Sie unmittelbar vor dem Senden dieser Daten an Adobe senden.
exl-id: 945f4fa1-380c-46aa-a92a-bbcfd6644751
source-git-commit: d3be2a9e75514023a7732a1c3460f8695ef02e68
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# `onBeforeEventSend`

Mit dem `onBeforeEventSend` Callback können Sie eine JavaScript-Funktion registrieren, die die Daten ändern kann, die Sie gerade vor dem Senden dieser Daten an Adobe senden. Dieser Rückruf ermöglicht es Ihnen, das `xdm`- oder `data`-Objekt zu bearbeiten, einschließlich der Möglichkeit, Elemente hinzuzufügen, zu bearbeiten oder zu entfernen. Sie können das Senden von Daten auch ganz abbrechen, z. B. bei erkanntem Client-seitigem Bot-Traffic.

>[!WARNING]
>
>Dieser Callback ermöglicht die Verwendung von benutzerdefiniertem Code. Wenn ein Code, den Sie in den Callback einbeziehen, eine nicht abgefangene Ausnahme auslöst, wird die Verarbeitung für das Ereignis angehalten. Daten werden nicht an Adobe gesendet.

## Konfigurieren eines -Ereignisses vor dem Senden eines Callbacks mithilfe der Tag-Erweiterung „Web SDK&quot; {#tag-extension}

Klicken Sie beim **[!UICONTROL Konfigurieren der Tag-Erweiterung]** auf die Schaltfläche [Bereitstellen eines Ereignisses vor dem Senden des Callback-Codes](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Diese Schaltfläche öffnet ein modales Fenster, in dem Sie den gewünschten Code einfügen können.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei &#x200B;](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und klicken Sie dann auf **[!UICONTROL Konfigurieren]** auf der Karte [!UICONTROL Adobe Experience Platform Web SDK].
1. Scrollen Sie nach unten zum Abschnitt [!UICONTROL Datenerfassung] und klicken Sie dann auf die Schaltfläche **[!UICONTROL Bereitstellung eines Ereignisses vor dem Senden des Callback-Codes]**.
1. Diese Schaltfläche öffnet ein modales Fenster mit einem Code-Editor. Fügen Sie den gewünschten Code ein und klicken Sie dann auf **[!UICONTROL Speichern]**, um das modale Fenster zu schließen.
1. Klicken **[!UICONTROL unter]** auf „Speichern“ und veröffentlichen Sie Ihre Änderungen.

Innerhalb des Code-Editors haben Sie Zugriff auf die folgenden Variablen:

* **`content.xdm`**: Die [XDM](../sendevent/xdm.md)-Payload für das Ereignis.
* **`content.data`**: Die [Daten](../sendevent/data.md) Objekt-Payload für das Ereignis.
* **`return true`**: Sofort den Callback beenden und Daten mit den aktuellen Werten im `content` Objekt an Adobe senden.
* **`return false`**: Sofort den Callback beenden und das Senden von Daten an Adobe abbrechen.

Alle Variablen, die außerhalb von `content` definiert wurden, können verwendet werden, sind jedoch nicht in der Payload enthalten, die an Adobe gesendet wird.

```js
// Use nullish coalescing assignments to add objects if they don't yet exist
content.xdm.commerce ??= {};
content.xdm.commerce.order ??= {};

// Then add the purchase ID
content.xdm.commerce.order.purchaseID = "12345";

// Use optional chaining to prevent undefined errors when setting tracking code to lower case
if(content.xdm.marketing?.trackingCode) content.xdm.marketing.trackingCode = content.xdm.marketing.trackingCode.toLowerCase();

// Delete operating system version
if(content.xdm.environment) delete content.xdm.environment.operatingSystemVersion;

// Immediately end onBeforeEventSend logic and send the data to Adobe for this event type
if (content.xdm.eventType === "web.webInteraction.linkClicks") {
  return true;
}

// Cancel sending data if it is a known bot
if (myBotDetector.isABot()) {
  return false;
}
```

>[!TIP]
>Vermeiden Sie die Rückgabe von `false` beim ersten Ereignis auf einer Seite. Eine Rückkehr der `false` beim ersten Ereignis kann sich negativ auf die Personalisierung auswirken.

## Konfigurieren eines -Ereignisses vor dem Senden eines Callbacks mithilfe der Web SDK JavaScript-Bibliothek {#library}

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
