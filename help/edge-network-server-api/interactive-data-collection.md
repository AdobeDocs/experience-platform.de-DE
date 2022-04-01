---
title: Interaktive Datenerfassung
description: Erfahren Sie, wie die Adobe Experience Platform Edge Network Server-API die interaktive Datenerfassung durchführt.
seo-description: Learn how the Adobe Experience Platform Edge Network Server API performs interactive data collection
keywords: Datenerfassung;Datenerfassung;Experience Platform Edge Network;API;interaktive Datenerfassung
source-git-commit: eaeab8fe96a9af399f8288b62b6ca9f31d949cfa
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 7%

---


# Interaktive Datenerfassung

## Übersicht {#overview}

Endpunkte zur interaktiven Datenerfassung erhalten ein einzelnes Ereignis und werden verwendet, wenn der Client erwartet, dass eine Antwort vom Adobe Experience Platform Edge Network-Server zurückgegeben wird. Diese Endpunkte können bei der Datenerfassung auch Inhalte von anderen Experience Edge-Diensten zurückgeben.

Die Serverantwort umfasst eine oder mehrere `Handle` -Objekte, wie unten dargestellt.

## Beispiel für API-Aufruf

### API-Format {#format}

```http
POST /ee/v2/interact
```

### Anfrage {#request}

```shell
curl -X POST "https://server.adobedc.net/v2/interact?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {IMS_ORG_ID}" 
-H "x-api-key: {API_KEY}" 
-H "Content-Type: application/json" 
-d '{
   "event": {
      "xdm": {
         "identityMap": {
            "Email_LC_SHA256": [
               {
                  "id": "0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b",
                  "primary": true
               }
            ]
         },
         "eventType": "web.webpagedetails.pageViews",
         "web": {
            "webPageDetails": {
               "URL": "https://alloystore.dev/",
               "name": "home-demo-Home Page"
            }
         },
         "timestamp": "2021-08-09T14:09:20.859Z"
      },
      "data": {
         "prop1": "custom value"
      }
   }
}'
```

| Parameter | Typ | Erforderlich | Beschreibung |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Ja. | Datastream-ID. |
| `requestId` | `String` | Nein | Geben Sie eine Client-Zufallskennung für die Korrelation interner Server-Anforderungen an. Wenn keines angegeben ist, generiert das Edge-Netzwerk eines und gibt es in der Antwort zurück. |

### Antwort {#response}

Eine erfolgreiche Antwort gibt den HTTP-Status zurück `200 OK`, mit einer oder mehreren `Handle` -Objekte, abhängig von den in der Datastream-Konfiguration aktivierten Echtzeit-Edge-Diensten.

```json
{
   "requestId": "c85402f5-83a1-4fb3-abdd-f4c17bf6dd49",
   "handle": []
}
```
