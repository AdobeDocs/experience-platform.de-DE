---
title: edgeBasePath
description: Der Basispfad des Endpunkts, der für die Interaktion mit Adobe-Diensten verwendet wird.
exl-id: 3542575d-ad02-415c-8e47-97c877dfdd9d
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# `edgeBasePath`

Die Eigenschaft `edgeBasePath` ändert den Zielpfad bei der Interaktion mit Adobe-Diensten. Die meisten Unternehmen müssen diese Eigenschaft nicht festlegen oder ändern.

## Edge-Basispfad mit der Web SDK-Tag-Erweiterung

Geben Sie den gewünschten Text im Textfeld **[!UICONTROL Edge-Basispfad]** ein, wenn [die Tag-Erweiterung konfigurieren](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Melden Sie sich mit Ihren Adobe ID-Anmeldedaten bei [experience.adobe.com](https://experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und klicken Sie dann auf der Karte [!UICONTROL Adobe Experience Platform Web SDK] auf **[!UICONTROL Konfigurieren]** .
1. Scrollen Sie nach unten zum Abschnitt [!UICONTROL Erweiterte Einstellungen] und geben Sie dann den gewünschten Wert in das Textfeld **[!UICONTROL Edge-Basispfad]** ein.
1. Klicken Sie auf **[!UICONTROL Speichern]** und veröffentlichen Sie dann Ihre Änderungen.

## Edge-Basispfad mit der Web SDK JavaScript-Bibliothek

Legen Sie das Textfeld `edgeBasePath` fest, wenn Sie den Befehl `configure` ausführen. Wenn Sie diese Eigenschaft weglassen, wird standardmäßig der Wert `ee` verwendet. Adobe empfiehlt, diese Eigenschaft in den meisten Konfigurationen wegzulassen.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "edgeBasePath": "ee"
});
```
