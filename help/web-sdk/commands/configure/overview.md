---
title: Konfigurieren des Adobe Experience Platform Web SDK
description: Verwenden Sie den Befehl "configure", um bei Verwendung des Web SDK die erforderlichen Einstellungen festzulegen.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Konfigurieren des Adobe Experience Platform Web SDK

Die Konfiguration für das Web SDK erfolgt mit dem `configure` Befehl. Die Konfiguration des Web SDK ist ein wichtiger und erforderlicher Schritt, der immer dann erfolgen muss, wenn die Bibliothek oder Tag-Erweiterung verwendet wird.

## Konfigurationseinstellungen mit der Web SDK-Tag-Erweiterung

Navigieren Sie zum [Tag-Erweiterungskonfigurationsseite](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** Klicken Sie auf **[!UICONTROL Konfigurieren]** auf [!UICONTROL Adobe Experience Platform Web SDK] Karte.

Diese Konfigurationseinstellungen werden immer dann festgelegt, wenn Sie die Erweiterung verwenden, um Daten an Adobe zu senden.

## Konfigurationseinstellungen mit der JavaScript-Bibliothek des Web SDK

Führen Sie die `configure` Befehl. Dieser Befehl ist erforderlich, bevor Sie andere Web SDK-Befehle aufrufen können, z. B. [`sendEvent`](../sendevent/overview.md). Die Eigenschaften [`edgeConfigId`](edgeconfigid.md) und [`orgId`](orgid.md) sind erforderlich. Alle anderen Eigenschaften sind je nach den Implementierungsanforderungen Ihres Unternehmens optional.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "clickCollectionEnabled": false,
  "context": ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"],
  "debugEnabled": true,
  "defaultConsent": "pending",
  "downloadLinkQualifier": "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$",
  "edgeBasePath": "ee",
  "edgeConfigOverrides": { "datastreamId": "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  "edgeDomain": "data.example.com",
  "idMigrationEnabled": false,
  "onBeforeEventSend": function(content) {
    if(content.xdm.web?.webReferrer) delete content.xdm.web.webReferrer.URL;
  },
  "onBeforeLinkClickSend": function(content) {
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
  },
  "prehidingStyle": "#container { opacity: 0 !important }",
  "targetMigrationEnabled": true,
  "thirdPartyCookiesEnabled": false
});
```
