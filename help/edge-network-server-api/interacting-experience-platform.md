---
title: Interagieren mit Adobe Experience Platform
description: Erfahren Sie, wie Sie mit der Edge Network Server-API mit Adobe Experience Platform interagieren
seo-description: Learn how to use the Edge Network Server API to interact with Adobe Experience Platform
keywords: Datenerfassung; Auslass; Analyse; Adobe Experience Platform Edge Network API;aep
source-git-commit: 1880f391b3276aa61d0c94c1567f2dd555b66edc
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 1%

---


# Interagieren mit Adobe Experience Platform

## Übersicht {#overview}

Um die Datenerfassung in Experience Platform zu aktivieren, müssen Sie zunächst [Datenspeicher konfigurieren](../edge/fundamentals/datastreams.md) , um Ereignisse an Experience Platform-Datensätze weiterzuleiten.

Nach der Konfiguration sollte die Konfiguration des Datenspeichers Einstellungen für `com_adobe_experience_platform`, wie im folgenden Beispiel gezeigt:


```json
{
  // datastream config header

  "settings": {
    "com_adobe_experience_platform": {
      "sandboxName": "prod",
      "enabled": true,
      "datasets": {
        "event": {
          "xdmSchema": "https://ns.adobe.com/atag/schemas/35a31609b6d3242736751df469ade031",
          "datasetId": "5f67e6ad9501b0194b5aafb6"
        }
      }
    }

    // other settings
  }
}
```
