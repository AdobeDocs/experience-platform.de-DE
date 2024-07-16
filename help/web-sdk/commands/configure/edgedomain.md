---
title: edgeDomain
description: Bestimmen Sie die Stammdomäne, an die Sie Daten senden möchten.
exl-id: 6beb5116-cd23-42fd-934c-5cf84d1d7153
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 1%

---

# `edgeDomain`

Mit der Eigenschaft `edgeDomain` können Sie die Domäne ändern, an die das Web SDK Daten sendet. Diese Eigenschaft wird häufig von Organisationen verwendet, die [Erstanbieter-Cookies](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=de) verwenden. Die Daten werden an die eigene Domäne des Unternehmens gesendet. Anschließend leitet ein CNAME-Eintrag diese Daten an Adobe weiter.

Ihr Unternehmen bestimmt beim Einrichten von [Erstanbieter-Cookies](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=de) den richtigen Wert für diese Eigenschaft. Eine Organisation verwendet zu diesem Zweck in der Regel eine dedizierte Subdomäne. Wenn Sie beispielsweise die Domäne `example.com` verwenden, können Sie Erstanbieter-Cookies für `data.example.com` einrichten.

## Konfigurieren einer Edge-Domäne mithilfe der Web SDK-Tag-Erweiterung

Legen Sie das Textfeld **[!UICONTROL Edge-Domäne]** fest, wenn [die Tag-Erweiterung konfigurieren](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Melden Sie sich mit Ihren Adobe ID-Anmeldedaten bei [experience.adobe.com](https://experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und klicken Sie dann auf der Karte [!UICONTROL Adobe Experience Platform Web SDK] auf **[!UICONTROL Konfigurieren]** .
1. Suchen Sie das Textfeld **[!UICONTROL Edge-Domäne]** und geben Sie dann den gewünschten Wert ein.
1. Klicken Sie auf **[!UICONTROL Speichern]** und veröffentlichen Sie dann Ihre Änderungen.

## Konfigurieren einer Edge-Domäne mithilfe der Web SDK JavaScript-Bibliothek

Legen Sie die Zeichenfolge `edgeDomain` fest, wenn Sie den Befehl `configure` ausführen. Wenn Sie diese Eigenschaft beim Konfigurieren des SDK weglassen, wird standardmäßig `edge.adobedc.net` verwendet. Legen Sie diesen Wert fest, wenn Sie die Domäne überschreiben möchten, an die das Web SDK Daten sendet.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "edgeDomain": "data.example.com"
});
```
