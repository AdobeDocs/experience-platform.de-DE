---
title: Interaktive Datenerfassung
description: Erfahren Sie, wie die Adobe Experience Platform Edge Network Server-API die interaktive Datenerfassung durchführt.
exl-id: 1b06e755-b6a9-42dd-96c1-98ad67e7d222
source-git-commit: f8434746c4a023ec895d23a59e04fca4baecfc36
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 15%

---

# Interaktive Datenerfassung

## Übersicht {#overview}

Interaktive Datenerfassungs-Endpunkte erhalten ein einzelnes Edge Network und werden verwendet, wenn der Client erwartet, dass eine Antwort vom Adobe Experience Platform-Ereignisserver zurückgegeben wird. Diese Endpunkte können bei der Datenerfassung auch Inhalte von anderen Edge Network-Services zurückgeben.

>[!IMPORTANT]
>
>Der `/interact`-Endpunkt wurde hauptsächlich für die Verwendung durch die Experience Platform-SDKs entwickelt. Dieser Endpunkt unterliegt additiven Änderungen und sein Verhalten kann sich ohne Vorankündigung ändern. Beispielsweise könnten der Antwort-Payload in Zukunft neue Elemente hinzugefügt werden.

Die Antwort des Servers enthält ein oder mehrere `Handle`, wie unten dargestellt.

## Beispiel für einen API-Aufruf

### API-Format {#format}

```http
POST /ee/v2/interact
```

### Anfrage {#request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
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
| `dataStreamId` | `String` | Ja. | Datenstrom-ID. |
| `requestId` | `String` | Nein | Geben Sie eine zufällige Client-ID zum Korrelieren interner Server-Anfragen an. Wenn keine angegeben ist, generiert das Edge-Netzwerk eine und gibt sie in der Antwort zurück. |

### Antwort {#response}

Bei einer erfolgreichen Antwort wird der HTTP-Status `200 OK` mit einem oder mehreren `Handle` zurückgegeben, je nachdem, welche Echtzeit-Edge-Services in der Datenstromkonfiguration aktiviert sind.

```json
{
   "requestId": "c85402f5-83a1-4fb3-abdd-f4c17bf6dd49",
   "handle": []
}
```
