---
title: edgeDomain
description: Bestimmen Sie die Stammdomäne, an die Sie Daten senden möchten.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 1%

---

# `edgeDomain`

Die `edgeDomain` -Eigenschaft können Sie die Domäne ändern, an die das Web SDK Daten sendet. Diese Eigenschaft wird häufig von Organisationen verwendet, die [Erstanbieter-Cookies](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=de). Die Daten werden an die eigene Domäne des Unternehmens gesendet. Anschließend leitet ein CNAME-Eintrag diese Daten an Adobe weiter.

Ihr Unternehmen bestimmt beim Einrichten des [Erstanbieter-Cookies](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=de). Eine Organisation verwendet zu diesem Zweck in der Regel eine dedizierte Subdomäne. Wenn Sie beispielsweise die Domäne `example.com`, können Sie Erstanbieter-Cookies in `data.example.com`.

## Konfigurieren einer Edge-Domäne mithilfe der Web SDK-Tag-Erweiterung

Legen Sie die **[!UICONTROL Edge-Domäne]** Textfeld bei [Konfigurieren der Tag-Erweiterung](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** Klicken Sie auf **[!UICONTROL Konfigurieren]** auf [!UICONTROL Adobe Experience Platform Web SDK] Karte.
1. Suchen Sie das Textfeld **[!UICONTROL Edge-Domäne]** und geben Sie den gewünschten Wert ein.
1. Klicks **[!UICONTROL Speichern]** und veröffentlichen Sie dann Ihre Änderungen.

## Konfigurieren einer Edge-Domäne mithilfe der JavaScript-Bibliothek des Web SDK

Legen Sie die `edgeDomain` Zeichenfolge beim Ausführen der `configure` Befehl. Wenn Sie diese Eigenschaft beim Konfigurieren des SDK weglassen, wird standardmäßig `edge.adobedc.net`. Legen Sie diesen Wert fest, wenn Sie die Domäne überschreiben möchten, an die das Web SDK Daten sendet.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "edgeDomain": "data.example.com"
});
```
