---
solution: Experience Platform
title: Erste Schritte mit Media Edge-APIs
description: Erste Schritte mit Media Edge-APIs
exl-id: 76022dea-408b-4d8e-abd4-1a6de81beceb
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 100%

---

# Erste Schritte mit Media Edge-APIs

Dieses Handbuch enthält Anweisungen, mit denen Sie erste Interaktionen mit dem Media Edge-API-Service erfolgreich durchführen können. Dazu gehört das Starten einer Mediensitzung und das anschließende Tracking von Ereignissen, die an eine Adobe Experience Platform-Lösung wie Customer Journey Analytics (CJA) gesendet werden. Der Media Edge-API-Service wird mit dem Sitzungsstart-Endpunkt initiiert. Nachdem die Sitzung gestartet wurde, ist es möglich, eines oder mehrere der folgenden Ereignisse nachzuverfolgen:

* `play`
* `ping`
* `bitrateChange`
* `bufferStart`
* `pauseStart`
* `adBreakStart`
* `adStart`
* `adComplete`
* `adSkip`
* `adBreakComplete`
* `chapterStart`
* `chapterComplete`
* `chapterSkip`
* `error`
* `sessionEnd`
* `sessionComplete`
* `statesUpdate`

Jedes Ereignis besitzt einen eigenen Endpunkt. Bei allen Media Edge-API-Endpunkten handelt es sich um POST-Methoden mit JSON-Anfragetext für Ereignisdaten. Weitere Informationen zu Media Edge-API-Endpunkten, -Parametern und -Beispielen finden Sie in der [Media Edge-Swagger-Datei](swagger.md).

In diesem Handbuch wird gezeigt, wie die folgenden Ereignisse nach dem Sitzungsstart nachverfolgt werden:

* [Pufferstart](#buffer-start-event-request)
* [Play](#play-event-request)
* [Sitzungsende](#session-complete-event-request)

## Implementieren der API {#implement-api}

Abgesehen von geringfügigen Unterschieden im Modell und den Pfaden, die aufgerufen werden, wird die Media Edge-API so wie die [Mediensammlungs-API](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-overview.html?lang=de) implementiert. Die Implementierungsdetails der Mediensammlung gelten auch für die Media Edge-API, wie in der folgenden Dokumentation beschrieben:

* [Einstellen des HTTP-Anfragetyps in Ihrem Player](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-sed-pings.html?lang=de)
* [Senden von Ping-Ereignissen](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-sed-pings.html?lang=de)
* [Timeout-Bedingungen](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-timeout.html?lang=de)
* [Steuern der Ereignisreihenfolge](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-ctrl-order.html?lang=de)

## Autorisierung {#authorization}

Aktuell sind in Anfragen von Media Edge-APIs keine Autorisierungs-Header erforderlich.


## Starten der Sitzung {#start-session}

Um die Mediensitzung auf dem Server zu starten, verwenden Sie den Sitzungsstart-Endpunkt. Eine erfolgreiche Antwort enthält den Parameter `sessionId`, der für nachfolgende Ereignisanfragen erforderlich ist.

Um eine Sitzungsanfrage zu erstellen, benötigen Sie zunächst Folgendes:

* `datastreamId`, ein erforderlicher Parameter für die POST-Sitzungsstart-Anfrage. Informationen zum Abrufen von `datastreamId` finden Sie unter [Konfigurieren eines Datenstroms](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=de).

* Ein JSON-Objekt für die Anfrage-Payload, das die erforderlichen Mindestdaten enthält (wie in der Beispielanfrage unten dargestellt).

Sobald Sie über diese Informationen verfügen, geben Sie `datastreamId` im folgenden Aufruf an:

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/sessionStart?configId={datastream ID} \`

### Beispielanfrage

Das folgende Beispiel zeigt eine cURL-Sitzungsstart-Anfrage:

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

In der obigen Beispielanfrage enthält der Wert `eventType` das Präfix `media.` gemäß [Experience-Datenmodell (XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=de), um Domains anzugeben.

Außerdem sind die Datentypen für `eventType` im obigen Beispiel wie folgt zugeordnet:

| eventType | Datentypen |
| -------- | ------ |
| media.SessionStart | [sessionDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/sessiondetails.schema.md) |
| media.chapterStart | [chapterDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/chapterdetails.schema.md) |
| media.adBreakStart | [advertisingPodDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/advertisingpoddetails.schema.md) |
| media.adStart | [advertisingDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/advertisingdetails.schema.md) |
| media.error | [errorDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/errordetails.schema.md) |
| media.statesUpdate | [statesStart](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmstatesstart): Array[playerStateData], [statesEnd](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmstatesend): Array[playerStateData] |
| media.sessionStart, media.chapterStart, media.adStart | [customMetadata](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmcustommetadata) |
| all | [qoeDataDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/qoedatadetails.schema.md) |

### Beispielantwort

Das folgende Beispiel zeigt eine erfolgreiche Antwort für die Sitzungsstart-Anfrage:

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

In der obigen Beispielantwort wird `sessionId` als `af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333` angezeigt. In nachfolgenden Ereignisanfragen wird diese ID als erforderlichen Parameter verwendet.

Weitere Informationen zu Sitzungsstart-Endpunktparametern und -Beispielen finden Sie in der [Medien Edge-Swagger](swagger.md)-Datei.

Weitere Informationen zu XDM-Mediendatenparametern finden Sie unter [Informationsschema für Mediendetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmplayhead).


## Pufferstart-Ereignisanfrage {#buffer-start}

Das Pufferstart-Ereignis signalisiert, wenn die Pufferung im Medien-Player beginnt. Die Wiederaufnahme der Pufferung ist kein Ereignis im API-Service. Vielmehr wird dieser Vorgang abgeleitet, wenn nach dem Pufferstart ein Wiedergabeereignis gesendet wird. Verwenden Sie `sessionId` in der Payload eines Aufrufs an den folgenden Endpunkt, um eine Pufferstart-Ereignisanfrage zu stellen:

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/bufferStart \`

### Beispielanfrage

Das folgende Beispiel zeigt eine cURL-Pufferstart-Anfrage:

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

In der obigen Beispielanfrage wird der gleiche Parameter `sessionId`, der im vorherigen Aufruf zurückgegeben wird, als erforderlicher Parameter in der Pufferstart-Anfrage verwendet.

Eine erfolgreiche Antwort zeigt den Status 200 an und weist keinen Inhalt auf.

Weitere Informationen zu den Pufferstart-Endpunktparametern und -Beispielen finden Sie in der [Media Edge-Swagger](swagger.md)-Datei.


## Wiedergabe-Ereignisanfrage {#play-event}

Das Wiedergabe-Ereignis wird gesendet, wenn der Medien-Player seinen Status von einem anderen Status wie „Puffern“, „Angehalten“ oder „Fehler“ zu „Wiedergabe“ ändert. Verwenden Sie `sessionId` in der Payload eines Aufrufs an den folgenden Endpunkt, um eine Wiedergabe-Ereignisanfrage zu stellen:

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/play \`

### Beispielanfrage

Das folgende Beispiel zeigt eine cURL-Wiedergabeanfrage:

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

Eine erfolgreiche Antwort zeigt den Status 200 an und weist keinen Inhalt auf.

Weitere Informationen zu Wiedergabe-Endpunktparametern und -Beispielen finden Sie in der [Medien-Edge-Swagger](swagger.md)-Datei.

## Sitzungsende-Ereignisanfrage {#session-complete}

Das Sitzungsende-Ereignis wird beim Erreichen des Hauptinhalts gesendet. Verwenden Sie `sessionId` in der Payload eines Aufrufs an den folgenden Endpunkt, um eine Sitzungsende-Ereignisanfrage zu stellen:

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/sessionComplete \`

### Beispielanfrage

Das folgende Beispiel zeigt eine cURL-Sitzungsende-Anfrage:

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

Eine erfolgreiche Antwort zeigt den Status 200 an und weist keinen Inhalt auf.

Weitere Informationen zu Sitzungabschluss-Endpunktparametern und -Beispielen finden Sie in der [Medien-Edge-Swagger](swagger.md)-Datei.

## Antwort-Codes

Die folgende Tabelle zeigt die möglichen Antwort-Codes, die sich aus Media Edge-API-Anfragen ergeben:

| Status | Beschreibung |
| ---------- | --------- |
| 200 | Sitzung erfolgreich erstellt |
| 207 | Problem mit einem der Services, die eine Verbindung zu Edge Network herstellen (weitere Informationen im [Handbuch zur Fehlerbehebung](troubleshooting.md)) |
| 400er-Reihe | Ungültige Anfrage |
| 500er-Reihe | Server-Fehler |

## Weitere Informationen zu dieser Funktion

* [Media Edge-Handbuch zur Fehlerbehebung](troubleshooting.md)
* [Media Edge-APIs – Übersicht](overview.md)
