---
title: edgeBasePath
description: Der Basispfad des Endpunkts, der für die Interaktion mit Adobe-Services verwendet wird.
exl-id: 3542575d-ad02-415c-8e47-97c877dfdd9d
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# `edgeBasePath`

Die `edgeBasePath`-Eigenschaft ändert den Zielpfad, wenn Sie mit Adobe-Services interagieren. Die meisten Organisationen müssen diese Eigenschaft nicht festlegen oder ändern.

## Edge-Basispfad mit der Tag-Erweiterung „Web SDK&quot;

Geben Sie den gewünschten Text im Textfeld **[!UICONTROL Edge-Basispfad]** ein, wenn Sie [die Tag-Erweiterung konfigurieren](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und klicken Sie dann auf **[!UICONTROL Konfigurieren]** auf der Karte [!UICONTROL Adobe Experience Platform Web SDK].
1. Scrollen Sie nach unten zum Abschnitt [!UICONTROL Erweiterte Einstellungen] und geben Sie dann den gewünschten Wert in das Textfeld **[!UICONTROL Edge-]** ein.
1. Klicken Sie **[!UICONTROL Speichern]** und veröffentlichen Sie Ihre Änderungen.

## Edge-Basispfad mit der Web SDK JavaScript-Bibliothek

Legen Sie beim Ausführen des `configure`-Befehls das `edgeBasePath` Textfeld fest. Wenn Sie diese Eigenschaft auslassen, wird standardmäßig der Wert `ee` verwendet. Adobe empfiehlt, diese Eigenschaft in den meisten Konfigurationen wegzulassen.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  edgeBasePath: "ee"
});
```
