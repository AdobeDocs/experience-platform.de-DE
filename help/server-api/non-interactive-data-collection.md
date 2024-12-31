---
title: Nicht interaktive Datenerfassung
description: Erfahren Sie, wie die Adobe Experience Platform Edge Network Server-API eine nicht interaktive Datenerfassung durchführt.
exl-id: 1a704e8f-8900-4f56-a843-9550007088fe
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 5%

---


# Nicht interaktive Datenerfassung

## Übersicht {#overview}

Nicht interaktive Endpunkte für die Ereignisdatenerfassung werden verwendet, um mehrere Ereignisse an Experience Platform-Datensätze oder andere Outlets zu senden.

Das Senden von Ereignissen im Batch-Modus wird empfohlen, wenn Endbenutzerereignisse für einen kurzen Zeitraum lokal in die Warteschlange gestellt werden (z. B. wenn keine Netzwerkverbindung besteht).

Batch-Ereignisse sollten nicht unbedingt zum selben Endbenutzer gehören, d. h. Ereignisse können unterschiedliche Identitäten in ihrem `identityMap` enthalten.

## Beispiel für einen nicht interaktiven API-Aufruf {#example}

### API-Format {#api-format}

```http
POST /ee/v2/collect
```

### Anfrage {#request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/collect?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
-H "x-api-key: {API_KEY}" 
-H "Content-Type: application/json" 
-d '{
   "events": [
      {
         "xdm": {
            "identityMap": {
               "FPID": [
                  {
                     "id": "79bf8e83-f708-414b-b1ed-5789ff33bf0b",
                     "primary": "true"
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
      },
      {
         "xdm": {
            "identityMap": {
               "FPID": [
                  {
                     "id": "871e8460-a329-4e96-a5b6-ff359fb0afb9",
                     "primary": "true"
                  }
               ]
            },
            "eventType": "web.webinteraction.linkClicks",
            "web": {
               "webInteraction": {
                  "linkClicks": {
                     "value": 1
                  }
               },
               "name": "My Custom Link",
               "URL": "https://myurl.com"
            },
            "timestamp": "2021-08-09T14:09:20.859Z"
         }
      }
   ]
}'
```

| Parameter | Typ | Erforderlich | Beschreibung |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Ja | Die ID des vom Datenerfassungs-Endpunkt verwendeten Datenstroms. |
| `requestId` | `String` | Nein | Geben Sie eine externe Anforderungsverfolgungs-ID an. Wenn keine angegeben wird, generiert das Edge Network eine für Sie und gibt sie im Antworttext/in den Kopfzeilen zurück. |
| `silent` | `Boolean` | Nein | Optionaler boolescher Parameter, der angibt, ob das Edge Network eine `204 No Content` Antwort mit leerer Payload zurückgeben soll oder nicht. Kritische Fehler werden mit dem entsprechenden HTTP-Status-Code und der entsprechenden Payload gemeldet. |

### Antwort {#response}

Eine erfolgreiche Antwort gibt einen der folgenden Status sowie eine -`requestID` zurück, wenn in der Anfrage keiner angegeben wurde.

* `202 Accepted`, wann die Anfrage erfolgreich verarbeitet wurde
* `204 No Content`, wann die Anfrage erfolgreich verarbeitet und der `silent` auf `true` gesetzt wurde;
* `400 Bad Request` wenn die Anfrage nicht ordnungsgemäß erstellt wurde (z. B. wurde die obligatorische primäre Identität nicht gefunden).

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```
