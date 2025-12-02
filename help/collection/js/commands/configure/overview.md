---
title: Konfigurieren von Adobe Experience Platform Web SDK
description: Verwenden Sie den configure-Befehl, um die erforderlichen Einstellungen festzulegen, wenn Sie die Web-SDK verwenden.
exl-id: 05ba98ae-c004-4b7b-b55b-38290ca62cfa
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# Konfigurieren von Adobe Experience Platform Web SDK

Die Konfiguration für die Web-SDK erfolgt mit dem Befehl **`configure`** . Dieser Befehl ist bei jedem Laden der Seite erforderlich, bevor Sie andere Web-SDK-Befehle aufrufen, z. B. [`sendEvent`](../sendevent/overview.md).

**Die [`datastreamId`](datastreamid.md)- und [`orgId`](orgid.md) sind erforderlich.** Alle anderen Eigenschaften sind optional, je nach den Implementierungsanforderungen Ihres Unternehmens. Das folgende Beispiel zeigt ein Konfigurationsobjekt mit den meisten verfügbaren Eigenschaften:

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
    filterClickDetails: function(content) {
      content.linkUrl = "https://example.com/current.html";
    },
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
  prehidingStyle: "#container { opacity: 0 !important }",
  targetMigrationEnabled: true,
  thirdPartyCookiesEnabled: false
});
```
