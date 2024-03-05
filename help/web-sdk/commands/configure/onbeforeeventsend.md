---
title: onBeforeEventSend
description: Callback, der kurz vor dem Senden von Daten ausgeführt wird.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 0%

---

# `onBeforeEventSend`

Die `onBeforeEventSend` callback ermöglicht die Registrierung einer JavaScript-Funktion, die die Daten, die Sie senden, unmittelbar vor dem Senden dieser Daten an Adobe ändern kann. Mit diesem Rückruf können Sie die `xdm` oder `data` -Objekt, einschließlich der Möglichkeit, Elemente hinzuzufügen, zu bearbeiten oder zu entfernen. Sie können das Senden von Daten auch bedingt abbrechen, z. B. mit erkanntem clientseitigem Bot-Traffic.

>[!WARNING]
>
>Dieser Rückruf ermöglicht die Verwendung von benutzerdefiniertem Code. Wenn Code, den Sie in den Rückruf einschließen, eine nicht abgefangene Ausnahme ausgibt, wird die Verarbeitung für das Ereignis angehalten. Daten werden nicht an Adobe gesendet.

## Vor dem Senden des Rückrufs mit der Web SDK-Tag-Erweiterung

Wählen Sie die **[!UICONTROL Bereitstellung vor dem Senden des Rückruffods durch das Ereignis]** Schaltflächen beim [Konfigurieren der Tag-Erweiterung](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Diese Schaltfläche öffnet ein modales Fenster, in das Sie den gewünschten Code einfügen können.

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** Klicken Sie auf **[!UICONTROL Konfigurieren]** auf [!UICONTROL Adobe Experience Platform Web SDK] Karte.
1. Scrollen Sie nach unten zum [!UICONTROL Datenerfassung] und wählen Sie dann die Schaltfläche **[!UICONTROL Bereitstellung vor dem Senden des Rückruffods durch das Ereignis]**.
1. Diese Schaltfläche öffnet ein modales Fenster mit einem Code-Editor. Fügen Sie den gewünschten Code ein und klicken Sie dann auf **[!UICONTROL Speichern]** , um das modale Fenster zu schließen.
1. Klicks **[!UICONTROL Speichern]** unter den Erweiterungsparametern und veröffentlichen Sie dann Ihre Änderungen.

Im Code-Editor können Sie Elemente innerhalb der `content` -Objekt. Dieses Objekt enthält die Payload, die an Adobe gesendet wird. Sie müssen die `content` -Objekt oder einen beliebigen Code innerhalb einer Funktion einschließen. Alle Variablen, die außerhalb von `content` kann verwendet werden, sind aber nicht in der Payload enthalten, die an Adobe gesendet wird.

>[!TIP]
>
>Die Objekte `content.xdm` und `content.data` in diesem Kontext immer definiert sind, sodass Sie nicht überprüfen müssen, ob sie vorhanden sind. Einige Variablen in diesen Objekten hängen von Ihrer Implementierung und Datenschicht ab. Adobe empfiehlt, in diesen Objekten nach nicht definierten Werten zu suchen, um JavaScript-Fehler zu vermeiden.

Beispiel:

* Hinzufügen des XDM-Elements `xdm.commerce.order.purchaseID`
* Alle Zeichen in erzwingen `xdm.marketing.trackingCode` Kleinbuchstaben
* `xdm.environment.operatingSystemVersion` löschen
* Wenn es sich bei einem Ereignistyp um einen Link-Klick handelt, senden Sie sofort Daten, unabhängig vom Code darunter
* Senden von Daten an Adobe abbrechen, wenn ein Bot erkannt wird

Der entsprechende Code innerhalb des modalen Fensters lautet wie folgt:

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

>[!NOTE]
>
>Rückgabe vermeiden `false` beim ersten Ereignis auf einer Seite. Returning `false` beim ersten Ereignis die Personalisierung negativ beeinflussen.

## Vor dem Senden des Rückrufs mit der Web SDK-JavaScript-Bibliothek durch das Ereignis

Registrieren `onBeforeEventSend` Callback beim Ausführen von `configure` Befehl. Sie können die `content` Variablennamen zu einem beliebigen Wert hinzufügen, indem Sie die Parametervariable innerhalb der Inline-Funktion ändern.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": function(content) {
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
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": lastChanceLogic
});    
```
