---
title: Interagieren mit Adobe Analytics
description: Erfahren Sie, wie Sie mit der Edge Network Server-API mit Adobe Analytics interagieren
seo-description: Learn how to use the Edge Network Server API to interact with Adobe Analytics
keywords: Datenerfassung; Auslass; Analyse; Adobe Experience Platform Edge Network API;Analytics
exl-id: b5e7a4d0-9aea-4e70-a7d6-b9aad09aaddf
source-git-commit: 422f859bef8faf292fd7e5fd8b6a8d31967421c1
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 2%

---

# Interagieren mit Adobe Analytics

## Übersicht {#overview}

Die Adobe Analytics-Datenerfassung funktioniert durch die Übersetzung von XDM-Daten in ein Format, das von Adobe Analytics verstanden werden kann. Mehrere XDM-Felder sind [automatisch zugeordnet](../edge/data-collection/adobe-analytics/automatically-mapped-vars.md) in Analytics-Variablen.

Sie können auch [Manuelles Zuordnen von XDM-Werten](../edge/data-collection/adobe-analytics/manually-mapping-variables.md) zu älteren Analytics-Variablen hinzu.

Damit Adobe Analytics Daten von der Server-API empfangen kann, müssen Sie [Datenspeicher konfigurieren](../edge/fundamentals/datastreams.md#adobe-analytics-settings) , um Ereignisse an Adobe Analytics weiterzuleiten, indem Sie die Report Suite-ID auf der Seite mit der Datastream-Konfiguration eingeben.

![Adobe Analytics-Datenspeicherkonfiguration](assets/analytics-datastream.png)

## Interagieren mit Adobe Analytics {#interacting-analytics}

### API-Format {#format}

```http
POST https://server.adobedc.net/v2/interact?dataStreamId={DATASTREAM_ID}
```

### Anfrage {#request}

Das folgende Beispiel enthält mehrere automatisch zugeordnete Werte aus dem `_experience.analytics` Feldergruppe. Sie umfasst auch JSON-basierte Datenschichten. Diese Datenschichten können zwar nicht automatisch zugeordnet werden, es ist jedoch möglich, [Datenvorbereitung für die Datenerfassung](../edge/fundamentals/datastreams.md#data-prep) , um diese Werte einem Schema zuzuordnen, das die oben referenzierten Feldergruppen enthält.

Alle Werte, die Benutzer diesen Feldern zuordnen, werden automatisch den entsprechenden Analytics-Werten zugeordnet, so als wären sie in der API-Anfrage enthalten.

```shell
curl -X POST "https://server.adobedc.net/v2/interact?dataStreamId={DATASTREAM_ID}" \
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {IMS_ORG_ID}" 
-H "x-api-key: {API_KEY}" 
-H "Content-Type: application/json" \
-d '{
   "event": {
      "xdm": {
         "eventType": "web.webpagedetails.pageViews",
         "web": {
            "webPageDetails": {
               "URL": "https://alloystore.dev",
               "name": "Home Page"
            },
            "webReferrer": {
               "URL": ""
            }
         },
         "device": {
            "screenHeight": 1440,
            "screenWidth": 3440,
            "screenOrientation": "landscape"
         },
         "environment": {
            "type": "browser",
            "browserDetails": {
               "viewportWidth": 3440,
               "viewportHeight": 1440
            }
         },
         "placeContext": {
            "localTime": "2022-03-22T22:45:21.193-06:00",
            "localTimezoneOffset": 360
         },
         "timestamp": "2022-03-23T04:45:21.193Z",
         "implementationDetails": {
            "name": "https://ns.adobe.com/experience/alloy/reactor",
            "version": "2.8.0+2.9.0",
            "environment": "browser"
         },
         "_experience": {
            "analytics": {
               "customDimensions": {
                  "eVars": {
                     "eVar14": "eVar14"
                  }
               },
               "event1to100": {
                  "event13": {
                     "value": 1
                  },
                  "event14": {
                     "value": 2
                  }
               }
            }
         }
      }
   },
   "data": {
      "page": {
         "pageInfo": {
            "pageName": "Promotions",
            "siteSection": "Home"
         },
         "promos": {
            "heroPromos": "purse,shoes,sunglasses"
         },
         "customVariables": {
            "testGroup": "orange/black theme"
         },
         "events": {
            "homePage": true
         },
         "products": [
            {
               "productSKU": "abc123",
               "productName": "shirt"
            }
         ]
      }
   }
}'
```

### Antwort {#response}

```json
{
   "requestId": "d2ad6364-5675-4a86-ba41-50e7a4c4a299",
   "handle": []
}
```
