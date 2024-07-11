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
>Dieser Rückruf wird nicht mehr unterstützt. Verwendung [`filterClickDetails`](clickcollection.md) anstatt.

Die `onBeforeLinkClickSend` Callback ermöglicht die Registrierung einer JavaScript-Funktion, die die Linktracking-Daten ändern kann, die Sie unmittelbar vor dem Senden dieser Daten an Adobe senden. Mit diesem Rückruf können Sie die `xdm` oder `data` -Objekt, einschließlich der Möglichkeit, Elemente hinzuzufügen, zu bearbeiten oder zu entfernen. Sie können das Senden von Daten auch bedingt abbrechen, z. B. mit erkanntem clientseitigem Bot-Traffic. Es wird auf Web SDK 2.15.0 oder höher unterstützt.

Dieser Rückruf wird nur ausgeführt, wenn [`clickCollectionEnabled`](clickcollectionenabled.md) aktiviert ist und [`filterClickDetails`](clickcollection.md) enthält keine registrierte Funktion. Wenn `clickCollectionEnabled` deaktiviert ist oder wenn `filterClickDetails` eine registrierte Funktion enthält, wird dieser Rückruf nicht ausgeführt. Wenn `onBeforeEventSend` und `onBeforeLinkClickSend` beide registrierte Funktionen enthalten, `onBeforeLinkClickSend` wird zuerst ausgeführt.

>[!WARNING]
>
>Dieser Rückruf ermöglicht die Verwendung von benutzerdefiniertem Code. Wenn Code, den Sie in den Rückruf einschließen, eine nicht abgefangene Ausnahme ausgibt, wird die Verarbeitung für das Ereignis angehalten. Daten werden nicht an Adobe gesendet.

## Vor dem Link-Klick Callback mit der Web SDK-Tag-Erweiterung konfigurieren {#tag-extension}

Wählen Sie die **[!UICONTROL Vor Link-Klick-Ereignis angeben Callback-Code senden]** Schaltflächen beim [Konfigurieren der Tag-Erweiterung](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Diese Schaltfläche öffnet ein modales Fenster, in das Sie den gewünschten Code einfügen können.

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** Klicken Sie auf **[!UICONTROL Konfigurieren]** auf [!UICONTROL Adobe Experience Platform Web SDK] Karte.
1. Scrollen Sie nach unten zum [!UICONTROL Datenerfassung] und wählen Sie das Kontrollkästchen aus. **[!UICONTROL Aktivieren der Klickdatenerfassung]**.
1. Wählen Sie die Schaltfläche mit der Bezeichnung **[!UICONTROL Vor Link-Klick-Ereignis angeben Callback-Code senden]**.
1. Diese Schaltfläche öffnet ein modales Fenster mit einem Code-Editor. Fügen Sie den gewünschten Code ein und klicken Sie dann auf **[!UICONTROL Speichern]** , um das modale Fenster zu schließen.
1. Klicks **[!UICONTROL Speichern]** unter den Erweiterungsparametern und veröffentlichen Sie dann Ihre Änderungen.

Im Code-Editor haben Sie Zugriff auf die folgenden Variablen:

* **`content.clickedElement`**: Das angeklickte DOM-Element.
* **`content.xdm`**: Die XDM-Payload für das Ereignis.
* **`content.data`**: Die Payload des Datenobjekts für das Ereignis.
* **`return true`**: Beenden Sie den Callback sofort mit den aktuellen Variablenwerten. Die `onBeforeEventSend` -Rückruf wird ausgeführt, wenn er eine registrierte Funktion enthält.
* **`return false`**: Beenden Sie den Callback sofort und brechen Sie das Senden von Daten an Adobe ab. Die `onBeforeEventSend` -Rückruf wird nicht ausgeführt.

Alle Variablen, die außerhalb von `content` kann verwendet werden, sind aber nicht in der Payload enthalten, die an Adobe gesendet wird.

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

Ähnlich wie [`onBeforeEventSend`](onbeforeeventsend.md), können Sie `return true` die Funktion unverzüglich abzuschließen, oder `return false` um den Versand von Daten an Adobe abzubrechen. Wenn Sie das Senden von Daten abbrechen `onBeforeLinkClickSend` Wenn beide `onBeforeEventSend` und `onBeforeLinkClickSend` enthält registrierte Funktionen, die `onBeforeEventSend` -Funktion nicht ausgeführt.

## Vor dem Link-Klick Callback mit der Web SDK JavaScript-Bibliothek konfigurieren {#library}

Registrieren `onBeforeLinkClickSend` Callback beim Ausführen von `configure` Befehl. Sie können die `content` Variablennamen zu einem beliebigen Wert hinzufügen, indem Sie die Parametervariable innerhalb der Inline-Funktion ändern.

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
