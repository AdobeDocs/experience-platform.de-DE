---
title: onBeforeEventSend
description: Erfahren Sie, wie Sie das Web SDK so konfigurieren, dass eine JavaScript-Funktion registriert wird, die die Daten ändern kann, die Sie unmittelbar vor dem Senden dieser Daten an Adobe senden.
exl-id: 945f4fa1-380c-46aa-a92a-bbcfd6644751
source-git-commit: d3be2a9e75514023a7732a1c3460f8695ef02e68
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# `onBeforeEventSend`

Mit dem Rückruf `onBeforeEventSend` können Sie eine JavaScript-Funktion registrieren, die die gesendeten Daten ändern kann, bevor diese Daten an Adobe gesendet werden. Mit diesem Rückruf können Sie das Objekt `xdm` oder `data` bearbeiten, einschließlich der Möglichkeit, Elemente hinzuzufügen, zu bearbeiten oder zu entfernen. Sie können das Senden von Daten auch bedingt abbrechen, z. B. mit erkanntem clientseitigem Bot-Traffic.

>[!WARNING]
>
>Dieser Rückruf ermöglicht die Verwendung von benutzerdefiniertem Code. Wenn Code, den Sie in den Rückruf einschließen, eine nicht abgefangene Ausnahme ausgibt, wird die Verarbeitung für das Ereignis angehalten. Daten werden nicht an Adobe gesendet.

## Vor dem Ereignis-Rückruf konfigurieren mit der Web SDK-Tag-Erweiterung {#tag-extension}

Wählen Sie bei der Konfiguration der Tag-Erweiterung [ die Schaltfläche **[!UICONTROL Vor dem Senden des Rückruffods durch das Ereignis bereitstellen]** aus. ](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) Diese Schaltfläche öffnet ein modales Fenster, in das Sie den gewünschten Code einfügen können.

1. Melden Sie sich mit Ihren Adobe ID-Anmeldedaten bei [experience.adobe.com](https://experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und klicken Sie dann auf der Karte [!UICONTROL Adobe Experience Platform Web SDK] auf **[!UICONTROL Konfigurieren]** .
1. Scrollen Sie nach unten zum Abschnitt [!UICONTROL Datenerfassung] und wählen Sie dann die Schaltfläche **[!UICONTROL Vor dem Senden des Rückrufcodes für das Ereignis bereitstellen]** aus.
1. Diese Schaltfläche öffnet ein modales Fenster mit einem Code-Editor. Fügen Sie den gewünschten Code ein und klicken Sie dann auf **[!UICONTROL Speichern]** , um das modale Fenster zu schließen.
1. Klicken Sie unter den Erweiterungseinstellungen auf **[!UICONTROL Speichern]** und veröffentlichen Sie dann Ihre Änderungen.

Im Code-Editor haben Sie Zugriff auf die folgenden Variablen:

* **`content.xdm`**: Die [XDM](../sendevent/xdm.md)-Payload für das Ereignis.
* **`content.data`**: Die [data](../sendevent/data.md) -Objekt-Payload für das Ereignis.
* **`return true`**: Beenden Sie sofort den Rückruf und senden Sie Daten mit den aktuellen Werten im `content` -Objekt an Adobe.
* **`return false`**: Beenden Sie den Callback sofort und brechen Sie das Senden von Daten an Adobe ab.

Alle Variablen, die außerhalb von `content` definiert sind, können verwendet werden, sind jedoch nicht in der Payload enthalten, die an Adobe gesendet wird.

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
>Vermeiden Sie es, beim ersten Ereignis auf einer Seite `false` zurückzugeben. Die Ausgabe von `false` beim ersten Ereignis kann sich negativ auf die Personalisierung auswirken.

## Vor dem Ereignis-Rückruf konfigurieren mit der Web SDK JavaScript-Bibliothek {#library}

Registrieren Sie den Rückruf `onBeforeEventSend` , wenn Sie den Befehl `configure` ausführen. Sie können den Variablennamen `content` in einen beliebigen Wert ändern, indem Sie die Parametervariable innerhalb der Inline-Funktion ändern.

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

Sie können auch Ihre eigene Funktion anstelle einer Inline-Funktion registrieren.

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
