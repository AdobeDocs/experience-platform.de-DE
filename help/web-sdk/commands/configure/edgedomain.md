---
title: edgeDomain
description: Bestimmen Sie die Stamm-Domain, an die Sie Daten senden möchten.
exl-id: 6beb5116-cd23-42fd-934c-5cf84d1d7153
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 1%

---

# `edgeDomain`

Mit der Eigenschaft `edgeDomain` können Sie die Domain ändern, an die die Web-SDK Daten sendet. Diese Eigenschaft wird häufig von Organisationen verwendet, die [Erstanbieter-Cookies](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=de) verwenden. Daten werden an die unternehmenseigene Domain gesendet. Anschließend werden diese Daten von einem CNAME-Eintrag an Adobe weitergeleitet.

Ihr Unternehmen bestimmt den richtigen Wert für diese Eigenschaft beim Einrichten von [Erstanbieter-Cookies](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=de). Eine Organisation verwendet zu diesem Zweck in der Regel eine dedizierte Subdomain. Wenn Sie beispielsweise den Domain-`example.com` verwenden, können Sie Erstanbieter-Cookies in `data.example.com` einrichten.

## Konfigurieren einer Edge-Domain mit der Tag-Erweiterung „Web SDK&quot;

Legen Sie das Textfeld **[!UICONTROL Edge Domain]** beim Konfigurieren [ Tag-Erweiterung ](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und klicken Sie dann auf **[!UICONTROL Konfigurieren]** auf der Karte [!UICONTROL Adobe Experience Platform Web SDK].
1. Suchen Sie das Textfeld **[!UICONTROL Edge Domain]** und geben Sie dann den gewünschten Wert ein.
1. Klicken Sie **[!UICONTROL Speichern]** und veröffentlichen Sie Ihre Änderungen.

## Konfigurieren einer Edge-Domain mit der Web SDK JavaScript-Bibliothek

Legen Sie die `edgeDomain` beim Ausführen des `configure`-Befehls fest. Wenn Sie diese Eigenschaft beim Konfigurieren der SDK weglassen, wird sie standardmäßig auf `edge.adobedc.net` gesetzt. Legen Sie diesen Wert fest, wenn Sie die Domain überschreiben möchten, an die die Web-SDK-Daten sendet.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  edgeDomain: "data.example.com"
});
```
