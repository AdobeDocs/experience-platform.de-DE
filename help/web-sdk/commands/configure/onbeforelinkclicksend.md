---
title: onBeforeLinkClickSend
description: Callback, der unmittelbar vor dem Senden der Linktracking-Daten ausgeführt wird.
exl-id: 8c73cb25-2648-4cf7-b160-3d06aecde9b4
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---


# `onBeforeLinkClickSend`

>[!IMPORTANT]
>
>Dieser Callback ist veraltet. Verwenden Sie stattdessen [`filterClickDetails`](clickcollection.md) .

Mit dem `onBeforeLinkClickSend` Callback können Sie eine JavaScript-Funktion registrieren, die Linktracking-Daten ändern kann, die Sie senden, bevor diese Daten an Adobe gesendet werden. Dieser Rückruf ermöglicht es Ihnen, das `xdm`- oder `data`-Objekt zu bearbeiten, einschließlich der Möglichkeit, Elemente hinzuzufügen, zu bearbeiten oder zu entfernen. Sie können das Senden von Daten auch ganz abbrechen, z. B. bei erkanntem Client-seitigem Bot-Traffic. Es wird ab Web SDK 2.15.0 unterstützt.

Dieser Rückruf wird nur ausgeführt, wenn [`clickCollectionEnabled`](clickcollectionenabled.md) aktiviert ist und [`filterClickDetails`](clickcollection.md) keine registrierte Funktion enthält. Wenn `clickCollectionEnabled` deaktiviert ist oder `filterClickDetails` eine registrierte Funktion enthält, wird dieser Callback nicht ausgeführt. Wenn `onBeforeEventSend` und `onBeforeLinkClickSend` beide registrierte Funktionen enthalten, wird `onBeforeLinkClickSend` zuerst ausgeführt.

>[!WARNING]
>
>Dieser Callback ermöglicht die Verwendung von benutzerdefiniertem Code. Wenn ein Code, den Sie in den Callback einbeziehen, eine nicht abgefangene Ausnahme auslöst, wird die Verarbeitung für das Ereignis angehalten. Daten werden nicht an Adobe gesendet.

## Konfigurieren Sie einen Link, bevor Sie auf „Rückruf senden“ klicken, indem Sie die Tag-Erweiterung „Web SDK&quot; verwenden. {#tag-extension}

Wählen Sie beim Konfigurieren **[!UICONTROL Tag-Erweiterung die Schaltfläche]** Vor Link-Klick-Ereignis-Rückruf-Code [Bereitstellen](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) aus. Diese Schaltfläche öffnet ein modales Fenster, in dem Sie den gewünschten Code einfügen können.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei &#x200B;](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und klicken Sie dann auf **[!UICONTROL Konfigurieren]** auf der Karte [!UICONTROL Adobe Experience Platform Web SDK].
1. Scrollen Sie nach unten zum Abschnitt [!UICONTROL Datenerfassung] und aktivieren Sie dann das Kontrollkästchen **[!UICONTROL Aktivieren und auf Datenerfassung klicken]**.
1. Klicken Sie auf die Schaltfläche **[!UICONTROL Bereitstellen eines Links vor dem Klicken auf den Rückruf-Code für das Ereignis senden]**.
1. Diese Schaltfläche öffnet ein modales Fenster mit einem Code-Editor. Fügen Sie den gewünschten Code ein und klicken Sie dann auf **[!UICONTROL Speichern]**, um das modale Fenster zu schließen.
1. Klicken **[!UICONTROL unter]** auf „Speichern“ und veröffentlichen Sie Ihre Änderungen.

Innerhalb des Code-Editors haben Sie Zugriff auf die folgenden Variablen:

* **`content.clickedElement`**: Das angeklickte DOM-Element.
* **`content.xdm`**: Die XDM-Payload für das Ereignis.
* **`content.data`**: Die Payload des Datenobjekts für das Ereignis.
* **`return true`**: Sofort den Callback mit den aktuellen Variablenwerten beenden. Der `onBeforeEventSend`-Rückruf wird ausgeführt, wenn er eine registrierte Funktion enthält.
* **`return false`**: Sofort den Callback beenden und das Senden von Daten an Adobe abbrechen. Der `onBeforeEventSend`-Callback wird nicht ausgeführt.

Alle Variablen, die außerhalb von `content` definiert wurden, können verwendet werden, sind jedoch nicht in der Payload enthalten, die an Adobe gesendet wird.

```js
// Set an already existing value to something else
content.xdm.web.webPageDetails.URL = "https://example.com/current.html";

// Use nullish coalescing assignments to create objects if they don't yet exist, preventing undefined errors. 
// Can be omitted if you are certain that the object is already defined
content.xdm._experience ??= {};
content.xdm._experience.analytics ??= {};
content.xdm._experience.analytics.customDimensions ??= {};
content.xdm._experience.analytics.customDimensions.eVars ??= {};

// Then set the property to the clicked element
content.xdm._experience.analytics.customDimensions.eVars.eVar1 = content.clickedElement;

// Use optional chaining to check if each object is defined, preventing undefined errors
if(content.xdm.web?.webInteraction?.type === "other") content.xdm.web.webInteraction.type = "download";
```

Ähnlich wie bei [`onBeforeEventSend`](onbeforeeventsend.md) können Sie `return true`, die Funktion sofort abzuschließen, oder `return false`, das Senden von Daten an Adobe abzubrechen. Wenn Sie den Versand von Daten in `onBeforeLinkClickSend` abbrechen, wenn sowohl `onBeforeEventSend` als auch `onBeforeLinkClickSend` registrierte Funktionen enthalten, wird die `onBeforeEventSend` nicht ausgeführt.

## Vor dem Klicken auf „Rückruf senden“ unter Verwendung der Web SDK JavaScript-Bibliothek konfigurieren {#library}

Registrieren Sie den `onBeforeLinkClickSend` Callback, wenn Sie den `configure` Befehl ausführen. Sie können den Namen der `content` in einen beliebigen Wert ändern, indem Sie die Parametervariable innerhalb der Inline-Funktion ändern.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeLinkClickSend: function(content) {
    // Add, modify, or delete values
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
    
    // Return true to complete the function immediately
    if (sendImmediate == true) {
      return true;
    }
    
    // Return false to cancel sending data immediately
    if(myBotDetector.isABot()){
      return false;
    }
  }
});
```

Anstelle einer Inline-Funktion können Sie auch eine eigene Funktion registrieren.

```js
function lastChanceLinkLogic(content) {
  content.xdm.application ??= {};
  content.xdm.application.name = "App name";
}

alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeLinkClickSend: lastChanceLinkLogic
});    
```
