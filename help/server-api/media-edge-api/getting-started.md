---
keywords: Experience Platform; Medien-Edge; beliebte Themen; Datumsbereich
solution: Experience Platform
title: Erste Schritte mit Media Edge-APIs
description: Erste Schritte mit Media Edge-APIs
source-git-commit: b4687fa7f1a2eb8f206ad41eae0af759b0801b83
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 7%

---


# Erste Schritte mit der Media Edge API

Dieses Handbuch enthält Anweisungen für erfolgreiche erste Interaktionen mit dem Media Edge API-Dienst. Dazu gehört das Starten einer Mediensitzung und das anschließende Tracking von Ereignissen, die an eine Adobe Experience Platform (AEP)-Lösung wie Customer Journey Analytics (CJA) gesendet werden. Der Media Edge-API-Dienst wird mit dem Sitzungsstart-Endpunkt initiiert. Nachdem die Sitzung gestartet wurde, können eines oder mehrere der folgenden Ereignisse verfolgt werden:

* play
* ping
* bitrateChange
* bufferStart
* pauseStart
* adBreakStart
* adStart
* adComplete
* adSkip
* adBreakComplete
* chapterStart
* chapterComplete
* chapterSkip
* error
* sessionEnd
* sessionComplete
* statesUpdate

Jedes Ereignis hat seinen eigenen Endpunkt. Alle Media Edge-API-Endpunkte sind POST-Methoden mit JSON-Anfrageinstanzen für Ereignisdaten. Weitere Informationen zu Media Edge API-Endpunkten, Parametern und Beispielen finden Sie in der Datei Media Edge Swagger .

In diesem Handbuch wird gezeigt, wie die folgenden Ereignisse nach dem Start der Sitzung verfolgt werden:

* Pufferstart
* Play
* Sitzungsbeendigung

## Implementieren der API

Abgesehen von geringfügigen Unterschieden im Modell und den Pfaden, die aufgerufen werden, ist die Media Edge-API mit der Media Collection API identisch. Die Implementierungsdetails der Mediensammlung bleiben für die Media Edge-API gültig, wie in der folgenden Dokumentation beschrieben:

* [Einstellen des HTTP-Anfragetyps in Ihrem Player](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-sed-pings.html?lang=en)
* [Senden von Ping-Ereignissen](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-sed-pings.html?lang=en)
* [Timeout-Bedingungen](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-timeout.html?lang=en)
* [Steuern der Ereignisreihenfolge](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-ctrl-order.html?lang=en)

## Authorization

Derzeit erfordern Media Edge-APIs in ihren Anfragen keine Autorisierungskopfzeilen.


## Starten der Sitzung

Um die Mediensitzung auf dem Server zu starten, verwenden Sie den Sitzungsstart-Endpunkt. Eine erfolgreiche Antwort enthält `sessionId`, der ein erforderlicher Parameter für nachfolgende Ereignisanfragen ist.

Bevor Sie die Sitzungsanforderung erstellen, benötigen Sie Folgendes:

* Die `datastreamId` ist ein erforderlicher Parameter für die POST Session Start-Anfrage. So rufen Sie eine `datastreamId`, siehe [Konfigurieren eines Datenspeichers](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=de).

* Ein JSON-Objekt für die Anfrage-Payload, das die erforderlichen Mindestdaten enthält (wie in der Beispielanfrage unten dargestellt).

Sobald Sie über diese Informationen verfügen, geben Sie die `datastreamId` im folgenden Aufruf:

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/sessionStart?configId={datastream ID} \`

### Beispielanfrage

Das folgende Beispiel zeigt eine cURL-Anfrage zum Sitzungsstart:

```
curl -i --request POST '{uri}/ee/va/v1/sessionStart?configId={dataStreamId}' \
--header 'Content-Type: application/json' \
--data-raw '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
          "sessionDetails": {
            "name": "Media Analytics API Sample",
            "playerName": "sample-html5-api-player",
            "contentType": "VOD",
            "length": 60,
            "channel": "sample-channel",
            "appVersion": "va-api-1.0.0"
          },
          "playhead": 0
        }
      }
    }
  ]
}'
```

In der obigen Beispielanfrage wird die `eventType` Wert enthält das Präfix `media` gemäß [Experience-Datenmodell (XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=de) zum Angeben von Domänen.

Außerdem die Zuordnung von Datentypen für `eventType` Im obigen Beispiel sehen Sie Folgendes:

| eventType | Datentypen |
| -------- | ------ |
| mediaSessionStart | [sessionDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/sessiondetails.schema.md) |
| media.chapterStart | [chapterDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/chapterdetails.schema.md) |
| media.adBreakStart | [advertisingPodDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/advertisingpoddetails.schema.md) |
| media.adStart | [advertisingDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/advertisingdetails.schema.md) |
| media.error | [errorDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/errordetails.schema.md) |
| media.statesUpdate | [statesStart](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmstatesstart): Array[playerStateData], [statesEnd](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmstatesend): Array[playerStateData] |
| media.sessionStart, media.chapterStart, media.adStart | [customMetadata](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmcustommetadata) |
| all | [qoeDataDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/qoedatadetails.schema.md) |

### Beispielantwort

Das folgende Beispiel zeigt eine erfolgreiche Antwort für die Sitzungsanforderung:

```
HTTP/2 200
x-request-id: 99603f5c-95cf-49ad-9afb-0ba6c5867fd7
x-rate-limit-remaining: 599
vary: Origin
date: Tue, 07 Mar 2023 14:37:58 GMT
x-konductor: 23.3.2:367bc7dc
x-adobe-edge: IRL1;6
server: jag
content-type: application/json;charset=utf-8
strict-transport-security: max-age=31536000; includeSubDomains
cache-control: no-cache, no-store, max-age=0, no-transform
x-xss-protection: 1; mode=block
x-content-type-options: nosniff

{
    "requestId": "df14bca1-ba0f-4574-ae80-a4e24a960c00",
    "handle": [
        {
            "payload": [
                {
                    "sessionId": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333"
                }
            ],
            "type": "media-analytics:new-session",
            "eventIndex": 0
        },
        {
            "payload": [
                {
                    "key": "kndctr_6D9FE18C5536A5E90A4C98A6_AdobeOrg_cluster",
                    "value": "irl1",
                    "maxAge": 1800
                },
                {
                    "key": "kndctr_6D9FE18C5536A5E90A4C98A6_AdobeOrg_identity",
                    "value": "CiY1MTkxMDM4OTc1MzkwMTY4NTQ1NjAxNDg4OTgzODU5MTAzMDcyMVIPCKKt8KnsMBgBKgRJUkwx8AGirfCp7DA=",
                    "maxAge": 34128000
                }
            ],
            "type": "state:store"
        }
    ]
}
```

In der obigen Beispielantwort wird die `sessionId` wird angezeigt als `af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333`. Sie verwenden diese ID in nachfolgenden Ereignisanfragen als erforderlichen Parameter.

Weitere Informationen zu den Endpunktparametern für den Sitzungsstart und Beispiele finden Sie in der Datei Media Edge Swagger .

Weitere Informationen zu XDM-Mediendatenparametern finden Sie unter [Informationsschema für Mediendetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmplayhead).


## Ereignisanforderung für Pufferstart

Das Ereignis &quot;Pufferstart&quot;signalisiert beim Start der Pufferung im Medienplayer. Die Wiederaufnahme der Pufferung ist kein Ereignis im API-Dienst. wird stattdessen erkannt, wenn nach dem Start der Pufferung ein Wiedergabeereignis gesendet wird. Verwenden Sie Ihre `sessionId` in der Payload eines Aufrufs an den folgenden Endpunkt:

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/bufferStart \`

### Beispielanfrage

Das folgende Beispiel zeigt eine cURL-Anfrage zum Pufferstart:

```
curl -X 'POST' \
  'https://edge.adobedc.net/ee-pre-prd/va/v1/bufferStart' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "events": [
    {
      "xdm": {
        "eventType": "media.bufferStart",
        "mediaCollection": {
          "sessionID": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333",
          "playhead": 25
        },
        "timestamp": "2022-03-04T13:39:00+00:00"
      }
    }
  ]
}'
```

In der obigen Beispielanfrage gilt für `sessionId` wird als der erforderliche Parameter in der Pufferstartanforderung verwendet, der im vorherigen Aufruf zurückgegeben wird.

Weitere Informationen zu den Endpunktparametern für den Pufferstart und Beispiele finden Sie in der Datei Media Edge Swagger .

Die erfolgreiche Antwort gibt den Status 200 an und enthält keinen Inhalt.

## Ereignisanforderung abspielen

Das Abspielereignis wird gesendet, wenn der Medienplayer seinen Status von einem anderen Status wie &quot;Puffern&quot;, &quot;Ausgesetzt&quot;oder &quot;Fehler&quot;zu &quot;Wiedergabe&quot;ändert. Verwenden Sie Ihre `sessionId` in der Payload eines Aufrufs an den folgenden Endpunkt:

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/play \`

### Beispielanfrage

Das folgende Beispiel zeigt eine cURL-Anfrage zum Abspielen:

```
curl -X 'POST' \
  'https://edge.adobedc.net/ee-pre-prd/va/v1/play' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "events": [
    {
      "xdm": {
        "eventType": "media.play",
        "mediaCollection": {
          "sessionID": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333",
          "playhead": 25
        },
        "timestamp": "2022-03-04T13:39:00+00:00"
      }
    }
  ]
}'
```

Die erfolgreiche Antwort gibt den Status 200 an und enthält keinen Inhalt.

Weitere Informationen zu Play-Endpunktparametern und Beispiele finden Sie in der Datei Media Edge Swagger .

## Anfrage zum Sitzungsbeendigungsereignis

Das Ereignis Sitzungsbeendigung wird gesendet, wenn das Ende des Hauptinhalts erreicht ist. Verwenden Sie Ihre `sessionId` in der Payload eines Aufrufs an den folgenden Endpunkt:

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/sessionComplete \`

### Beispielanfrage

Das folgende Beispiel zeigt eine cURL-Anfrage zum Sitzungsabschluss:

```
curl -X 'POST' \
  'https://edge.adobedc.net/ee-pre-prd/va/v1/sessionComplete' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionComplete",
        "mediaCollection": {
          "sessionID": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333",
          "playhead": 25
        },
        "timestamp": "2022-03-04T13:39:00+00:00"
      }
    }
  ]
}'
```

Die erfolgreiche Antwort gibt den Status 200 an und enthält keinen Inhalt.

## Antwort-Codes

Die folgende Tabelle zeigt die möglichen Antwort-Codes, die aus Media Edge-API-Anfragen resultieren:

| Status | Beschreibung |
| ---------- | --------- |
| 200 | Sitzung wurde erfolgreich erstellt |
| 207 | Problem mit einem der Dienste, die mit dem Experience Edge-Netzwerk verbunden sind (weitere Informationen finden Sie im Handbuch zur Problembehebung ) |
| 400-Grad | Ungültige Anfrage |
| 500-Grad | Server-Fehler |

Weitere Informationen zum Umgang mit Fehlern und fehlgeschlagenen Antwort-Codes finden Sie im Handbuch zur Fehlerbehebung bei Media Edge.


