---
title: onBeforeLinkClickSend
description: Callback, der kurz vor dem Senden von Linktracking-Daten ausgeführt wird.
exl-id: 8c73cb25-2648-4cf7-b160-3d06aecde9b4
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---


# `onBeforeLinkClickSend`

>[!IMPORTANT]
>
>Dieser Rückruf wird nicht mehr unterstützt. Verwenden Sie stattdessen [`filterClickDetails`](clickcollection.md) .

Mit dem Rückruf `onBeforeLinkClickSend` können Sie eine JavaScript-Funktion registrieren, die die von Ihnen gesendeten Linktracking-Daten ändern kann, bevor diese Daten an Adobe gesendet werden. Mit diesem Rückruf können Sie das Objekt `xdm` oder `data` bearbeiten, einschließlich der Möglichkeit, Elemente hinzuzufügen, zu bearbeiten oder zu entfernen. Sie können das Senden von Daten auch bedingt abbrechen, z. B. mit erkanntem clientseitigem Bot-Traffic. Es wird auf Web SDK 2.15.0 oder höher unterstützt.

Dieser Rückruf wird nur ausgeführt, wenn [`clickCollectionEnabled`](clickcollectionenabled.md) aktiviert ist und [`filterClickDetails`](clickcollection.md) keine registrierte Funktion enthält. Wenn `clickCollectionEnabled` deaktiviert ist oder `filterClickDetails` eine registrierte Funktion enthält, wird dieser Rückruf nicht ausgeführt. Wenn `onBeforeEventSend` und `onBeforeLinkClickSend` beide registrierte Funktionen enthalten, wird zuerst `onBeforeLinkClickSend` ausgeführt.

>[!WARNING]
>
>Dieser Rückruf ermöglicht die Verwendung von benutzerdefiniertem Code. Wenn Code, den Sie in den Rückruf einschließen, eine nicht abgefangene Ausnahme ausgibt, wird die Verarbeitung für das Ereignis angehalten. Daten werden nicht an Adobe gesendet.

## Vor dem Link-Klick Callback mit der Web SDK-Tag-Erweiterung konfigurieren {#tag-extension}

Wählen Sie bei der Konfiguration der Tag-Erweiterung [ die Schaltfläche **[!UICONTROL Vor dem Link-Klick-Ereignis bereitstellen - Callback-Code senden]** aus. ](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) Diese Schaltfläche öffnet ein modales Fenster, in das Sie den gewünschten Code einfügen können.

1. Melden Sie sich mit Ihren Adobe ID-Anmeldedaten bei [experience.adobe.com](https://experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und klicken Sie dann auf der Karte [!UICONTROL Adobe Experience Platform Web SDK] auf **[!UICONTROL Konfigurieren]** .
1. Scrollen Sie nach unten zum Abschnitt [!UICONTROL Datenerfassung] und aktivieren Sie dann das Kontrollkästchen **[!UICONTROL Klick-Datenerfassung aktivieren]** .
1. Wählen Sie die Schaltfläche mit der Bezeichnung **[!UICONTROL Vor dem Link-Klick-Ereignis-Rückrufcode senden]** angeben.
1. Diese Schaltfläche öffnet ein modales Fenster mit einem Code-Editor. Fügen Sie den gewünschten Code ein und klicken Sie dann auf **[!UICONTROL Speichern]** , um das modale Fenster zu schließen.
1. Klicken Sie unter den Erweiterungseinstellungen auf **[!UICONTROL Speichern]** und veröffentlichen Sie dann Ihre Änderungen.

Im Code-Editor haben Sie Zugriff auf die folgenden Variablen:

* **`content.clickedElement`**: Das DOM-Element, auf das geklickt wurde.
* **`content.xdm`**: Die XDM-Payload für das Ereignis.
* **`content.data`**: Die Payload des Datenobjekts für das Ereignis.
* **`return true`**: Beenden Sie den Rückruf sofort mit den aktuellen Variablenwerten. Der Rückruf `onBeforeEventSend` wird ausgeführt, wenn er eine registrierte Funktion enthält.
* **`return false`**: Beenden Sie den Callback sofort und brechen Sie das Senden von Daten an Adobe ab. Der Rückruf `onBeforeEventSend` wird nicht ausgeführt.

Alle Variablen, die außerhalb von `content` definiert sind, können verwendet werden, sind jedoch nicht in der Payload enthalten, die an Adobe gesendet wird.

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

Ähnlich wie bei [`onBeforeEventSend`](onbeforeeventsend.md) können Sie `return true` die Funktion sofort abschließen oder `return false` den Versand von Daten an Adobe abbrechen. Wenn Sie das Senden von Daten in `onBeforeLinkClickSend` abbrechen, wenn sowohl `onBeforeEventSend` als auch `onBeforeLinkClickSend` registrierte Funktionen enthalten, wird die Funktion `onBeforeEventSend` nicht ausgeführt.

## Vor dem Link-Klick Callback mit der Web SDK JavaScript-Bibliothek konfigurieren {#library}

Registrieren Sie den Rückruf `onBeforeLinkClickSend` , wenn Sie den Befehl `configure` ausführen. Sie können den Variablennamen `content` in einen beliebigen Wert ändern, indem Sie die Parametervariable innerhalb der Inline-Funktion ändern.

```js
alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
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

Sie können auch Ihre eigene Funktion anstelle einer Inline-Funktion registrieren.

```js
function lastChanceLinkLogic(content) {
  content.xdm.application ??= {};
  content.xdm.application.name = "App name";
}

alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeLinkClickSend: lastChanceLinkLogic
});    
```
