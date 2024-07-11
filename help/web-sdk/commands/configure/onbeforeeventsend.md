---
title: onBeforeEventSend
description: Erfahren Sie, wie Sie das Web SDK so konfigurieren, dass eine JavaScript-Funktion registriert wird, die die Daten ändern kann, die Sie unmittelbar vor dem Senden dieser Daten an Adobe senden.
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---


# `onBeforeEventSend`

Die `onBeforeEventSend` callback ermöglicht die Registrierung einer JavaScript-Funktion, die die Daten, die Sie senden, verändern kann, bevor diese Daten an Adobe gesendet werden. Mit diesem Rückruf können Sie die `xdm` oder `data` -Objekt, einschließlich der Möglichkeit, Elemente hinzuzufügen, zu bearbeiten oder zu entfernen. Sie können das Senden von Daten auch bedingt abbrechen, z. B. mit erkanntem clientseitigem Bot-Traffic.

>[!WARNING]
>
>Dieser Rückruf ermöglicht die Verwendung von benutzerdefiniertem Code. Wenn Code, den Sie in den Rückruf einschließen, eine nicht abgefangene Ausnahme ausgibt, wird die Verarbeitung für das Ereignis angehalten. Daten werden nicht an Adobe gesendet.

## Vor dem Ereignis-Rückruf konfigurieren mit der Web SDK-Tag-Erweiterung {#tag-extension}

Wählen Sie die **[!UICONTROL Bereitstellung vor dem Senden des Rückruffods durch das Ereignis]** Schaltflächen beim [Konfigurieren der Tag-Erweiterung](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Diese Schaltfläche öffnet ein modales Fenster, in das Sie den gewünschten Code einfügen können.

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** Klicken Sie auf **[!UICONTROL Konfigurieren]** auf [!UICONTROL Adobe Experience Platform Web SDK] Karte.
1. Scrollen Sie nach unten zum [!UICONTROL Datenerfassung] und wählen Sie dann die Schaltfläche **[!UICONTROL Bereitstellung vor dem Senden des Rückruffods durch das Ereignis]**.
1. Diese Schaltfläche öffnet ein modales Fenster mit einem Code-Editor. Fügen Sie den gewünschten Code ein und klicken Sie dann auf **[!UICONTROL Speichern]** , um das modale Fenster zu schließen.
1. Klicks **[!UICONTROL Speichern]** unter den Erweiterungsparametern und veröffentlichen Sie dann Ihre Änderungen.

Im Code-Editor haben Sie Zugriff auf die folgenden Variablen:

* **`content.xdm`**: Die [XDM](../sendevent/xdm.md) Nutzlast für das Ereignis.
* **`content.data`**: Die [data](../sendevent/data.md) Objekt-Payload für das Ereignis.
* **`return true`**: Beenden Sie sofort den Rückruf und senden Sie Daten an Adobe mit den aktuellen Werten im `content` -Objekt.
* **`return false`**: Beenden Sie den Callback sofort und brechen Sie das Senden von Daten an Adobe ab.

Alle Variablen, die außerhalb von `content` kann verwendet werden, sind aber nicht in der Payload enthalten, die an Adobe gesendet wird.

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
>Rückgabe vermeiden `false` beim ersten Ereignis auf einer Seite. Returning `false` beim ersten Ereignis die Personalisierung negativ beeinflussen.

## Vor dem Ereignis-Rückruf konfigurieren mit der Web SDK JavaScript-Bibliothek {#library}

Registrieren `onBeforeEventSend` Callback beim Ausführen von `configure` Befehl. Sie können die `content` Variablennamen zu einem beliebigen Wert hinzufügen, indem Sie die Parametervariable innerhalb der Inline-Funktion ändern.

```js
alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
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
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeEventSend: lastChanceLogic
});    
```
