---
title: Konfigurieren von Adobe Experience Platform Web SDK
description: Verwenden Sie den configure-Befehl, um die erforderlichen Einstellungen festzulegen, wenn Sie die Web-SDK verwenden.
exl-id: 05ba98ae-c004-4b7b-b55b-38290ca62cfa
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---

# Konfigurieren von Adobe Experience Platform Web SDK

Die Konfiguration für die Web-SDK erfolgt mit dem Befehl `configure` . Die Konfiguration der Web-SDK ist ein wichtiger und erforderlicher Schritt, der immer dann erfolgen muss, wenn die Bibliothek oder Tag-Erweiterung verwendet wird.

## Konfigurieren von Web SDK mithilfe der Tag-Erweiterung {#configure-tag-extension}

Gehen Sie wie folgt vor, um Web SDK über die Tag-Erweiterung zu konfigurieren.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei &#x200B;](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und klicken Sie dann auf **[!UICONTROL Konfigurieren]** auf der Karte [!UICONTROL Adobe Experience Platform Web SDK].
1. Gehen Sie zur [Seite Konfiguration von Web SDK Tag-Erweiterungen](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md), um detaillierte Informationen zu allen Konfigurationsoptionen zu erhalten.

Diese Konfigurationseinstellungen werden festgelegt, wenn Sie die Erweiterung zum Senden von Daten an Adobe verwenden.

## Konfigurieren von Web SDK mithilfe der JavaScript-Bibliothek {#configure-js}

Führen Sie den `configure` Befehl aus. Dieser Befehl ist erforderlich, bevor Sie andere Web-SDK-Befehle aufrufen können, z. B. [`sendEvent`](../sendevent/overview.md).

Die [`datastreamId`](datastreamid.md)- und [`orgId`](orgid.md) sind erforderlich. Alle anderen Eigenschaften sind optional, je nach den Implementierungsanforderungen Ihres Unternehmens.

Detaillierte Informationen zu den einzelnen unterstützten Befehlen finden Sie im Inhaltsverzeichnis dieses Benutzerhandbuchs.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: true,
  clickCollection: {
    internalLinkEnabled: true,
    downloadLinkEnabled: true,
    externalLinkEnabled: true,
    eventGroupingEnabled: true,
    sessionStorageEnabled: true
  },
  context: ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"],
  debugEnabled: true,
  defaultConsent: "pending",
  downloadLinkQualifier: "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$",
  edgeBasePath: "ee",
  edgeConfigOverrides: { "datastreamId": "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  edgeDomain: "data.example.com",
  idMigrationEnabled: false,
  onBeforeEventSend: function(content) {
    if(content.xdm.web?.webReferrer) delete content.xdm.web.webReferrer.URL;
  },
  onBeforeLinkClickSend: function(content) {
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
  },
  prehidingStyle: "#container { opacity: 0 !important }",
  targetMigrationEnabled: true,
  thirdPartyCookiesEnabled: false
});
```
