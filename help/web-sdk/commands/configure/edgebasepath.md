---
title: edgeBasePath
description: Der Basispfad des Endpunkts, der für die Interaktion mit Adobe-Diensten verwendet wird.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# `edgeBasePath`

Die `edgeBasePath` -Eigenschaft ändert den Zielpfad bei der Interaktion mit Adobe-Diensten. Die meisten Unternehmen müssen diese Eigenschaft nicht festlegen oder ändern.

## Edge-Basispfad mit der Web SDK-Tag-Erweiterung

Geben Sie den gewünschten Text im **[!UICONTROL Edge-Basispfad]** Textfeld bei [Konfigurieren der Tag-Erweiterung](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** Klicken Sie auf **[!UICONTROL Konfigurieren]** auf [!UICONTROL Adobe Experience Platform Web SDK] Karte.
1. Scrollen Sie nach unten zum [!UICONTROL Erweiterte Einstellungen] und geben Sie dann den gewünschten Wert im **[!UICONTROL Edge-Basispfad]** Textfeld.
1. Klicks **[!UICONTROL Speichern]** und veröffentlichen Sie dann Ihre Änderungen.

## Edge-Basispfad mit der Web SDK-JavaScript-Bibliothek

Legen Sie die `edgeBasePath` Textfeld beim Ausführen von `configure` Befehl. Wenn Sie diese Eigenschaft weglassen, wird standardmäßig der Wert von `ee`. Adobe empfiehlt, diese Eigenschaft in den meisten Konfigurationen wegzulassen.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "edgeBasePath": "ee"
});
```
