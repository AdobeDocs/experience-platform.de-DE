---
title: Konfigurieren des Adobe Experience Platform Web SDK
description: Verwenden Sie den Befehl "configure", um bei Verwendung des Web SDK die erforderlichen Einstellungen festzulegen.
exl-id: 05ba98ae-c004-4b7b-b55b-38290ca62cfa
source-git-commit: 58cd6300307881c3de7c52e07c401bf2ed908517
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---

# Konfigurieren des Adobe Experience Platform Web SDK

Die Konfiguration für das Web SDK erfolgt mit dem `configure` Befehl. Die Konfiguration des Web SDK ist ein wichtiger und erforderlicher Schritt, der immer dann erfolgen muss, wenn die Bibliothek oder Tag-Erweiterung verwendet wird.

## Web SDK mit der Tag-Erweiterung konfigurieren {#configure-tag-extension}

Gehen Sie wie folgt vor, um das Web SDK über die Tag-Erweiterung zu konfigurieren.

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** Klicken Sie auf **[!UICONTROL Konfigurieren]** auf [!UICONTROL Adobe Experience Platform Web SDK] Karte.
1. Navigieren Sie zu [Konfigurationsseite der Web SDK-Tag-Erweiterung](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) für detaillierte Informationen zu allen Konfigurationsoptionen.

Diese Konfigurationseinstellungen werden immer dann festgelegt, wenn Sie die Erweiterung verwenden, um Daten an Adobe zu senden.

## Web SDK mithilfe der JavaScript-Bibliothek konfigurieren {#configure-js}

Führen Sie die `configure` Befehl. Dieser Befehl ist erforderlich, bevor Sie andere Web SDK-Befehle aufrufen können, z. B. [`sendEvent`](../sendevent/overview.md).

Die [`edgeConfigId`](edgeconfigid.md) und [`orgId`](orgid.md) -Eigenschaften erforderlich sind. Alle anderen Eigenschaften sind je nach den Implementierungsanforderungen Ihres Unternehmens optional.

Detaillierte Informationen zu den einzelnen unterstützten Befehlen finden Sie im Inhaltsverzeichnis dieses Benutzerhandbuchs.

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
