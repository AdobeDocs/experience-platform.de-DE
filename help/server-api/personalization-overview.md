---
title: Personalisierung – Übersicht
description: Erfahren Sie, wie Sie mit der Adobe Experience Platform Edge Network Server-API personalisierte Inhalte aus Adobe-Personalisierungslösungen abrufen können.
exl-id: 11be9178-54fe-49d0-b578-69e6a8e6ab90
source-git-commit: ae6c6d21b1eea900d01be3287827296071429d30
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 10%

---

# Personalisierung – Übersicht

Mit dem [!DNL Server API] können Sie personalisierte Inhalte aus Adobe-Personalisierungslösungen abrufen, einschließlich [Adobe Target](https://business.adobe.com/de/products/target/adobe-target.html), [Adobe Journey Optimizer](https://experienceleague.adobe.com/de/docs/journey-optimizer/using/ajo-home) und [Offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=de).

Darüber hinaus ermöglicht die [!DNL Server API] die Personalisierungsfunktionen der gleichen Seite und der nächsten Seite über Adobe Experience Platform-Personalisierungsziele wie [Adobe Target](../destinations/catalog/personalization/adobe-target-connection.md) und die [benutzerdefinierte Personalisierungsverbindung](../destinations/catalog/personalization/custom-personalization.md). Informationen zum Konfigurieren von Experience Platform für die Personalisierung der gleichen und der nächsten Seite finden Sie im [Handbuch zu diesem Thema](../destinations/ui/activate-edge-personalization-destinations.md).

Bei Verwendung der Server-API müssen Sie die von der Personalisierungs-Engine bereitgestellte Antwort mit der Logik integrieren, die zum Rendern von Inhalten auf Ihrer Site verwendet wird. Im Gegensatz [Web SDK](../web-sdk/home.md) verfügt das [!DNL Server API] nicht über einen Mechanismus zum automatischen Anwenden von Inhalten, die von Adobe-Personalisierungslösungen zurückgegeben werden.

## Terminologie {#terminology}

Bevor Sie mit Adobe-Personalisierungslösungen arbeiten, sollten Sie die folgenden Konzepte verstehen:

* **Angebot**: Ein Angebot ist eine Marketing-Botschaft, der ggf. Regeln zugeordnet sind, die angeben, wer sich zum Anzeigen des Angebots eignet.
* **Entscheidung**: Eine Entscheidung (früher als Angebotsaktivität bezeichnet) bestimmt die Auswahl eines Angebots.
* **Schema**: Das Schema einer Entscheidung bestimmt den Typ des zurückgegebenen Angebots.
* **Umfang**: Der Umfang der Entscheidung.
   * In Adobe Target ist dies die [!DNL mbox]. Der [!DNL global mbox] ist der `__view__`
   * Dies sind [!DNL Offer Decisioning] die Base64-kodierten JSON-Zeichenfolgen, die die Aktivitäts- und Platzierungs-IDs enthalten, die der offer decisioning-Service für die Angebotsunterbreitung verwenden soll.

## Das `query` {#query-object}

Zum Abrufen personalisierter Inhalte ist ein explizites Anfrageabfrageobjekt für ein Anfragebeispiel erforderlich. Das Abfrageobjekt hat das folgende Format:

```json
{
  "query": {
    "personalization": {
      "schemas": [
        "https://ns.adobe.com/personalization/html-content-item",
        "https://ns.adobe.com/personalization/json-content-item",
        "https://ns.adobe.com/personalization/redirect-item",
        "https://ns.adobe.com/personalization/dom-action"
      ],
      "decisionScopes": [
        "alloyStore",
        "siteWide",
        "__view__",
        "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ"
      ],
      "surfaces": [
        "web://mywebpage.html/",
        "web://mywebpage.html/#sample-json-content"
      ]
    }
  }
}
```



| Attribut | Typ | Erforderlich/Optional | Beschreibung |
| --- | --- | --- | ---|
| `schemas` | `String[]` | Erforderlich für die Personalisierung von Target. Optional für Offer decisioning. | Liste der in der Entscheidung verwendeten Schemata zur Auswahl des zurückgegebenen Angebotstyps. |
| `scopes` | `String[]` | Optional | Liste der Entscheidungsumfänge Maximal 30 pro Anfrage. |

## Das handle-Objekt {#handle}

Der personalisierte Inhalt, der von Personalisierungslösungen abgerufen wird, wird in einem `personalization:decisions`-Handle dargestellt, das das folgende Format für die Payload hat:

```json
{
   "type":"personalization:decisions",
   "payload":[
      {
         "id":"AT:eyJhY3Rpdml0eUlkIjoiMTMxMDEwIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
         "scope":"__view__",
         "scopeDetails":{
            "decisionProvider":"TGT",
            "activity":{
               "id":"131010"
            },
            "experience":{
               "id":"0"
            },
            "strategies":[
               {
                  "algorithmID":"0",
                  "trafficType":"0"
               }
            ]
         },
         "items":[
            {
               "id":"0",
               "schema":"https://ns.adobe.com/personalization/dom-action",
               "meta":{
                  "offer.name":"Default Content",
                  "experience.id":"0",
                  "activity.name":"Luma target reporting",
                  "activity.id":"131010",
                  "experience.name":"Experience A",
                  "option.id":"2",
                  "offer.id":"0"
               },
               "data":{
                  "type":"setHtml",
                  "format":"application/vnd.adobe.target.dom-action",
                  "content":"Customer Service not chrome",
                  "selector":"HTML > BODY > DIV.page-wrapper:eq(0) > FOOTER.page-footer:eq(0) > DIV.footer:eq(0) > DIV.links:eq(0) > DIV.widget:eq(0) > UL.footer:eq(0) > LI.nav:eq(1) > A:nth-of-type(1)",
                  "prehidingSelector":"HTML > BODY > DIV:nth-of-type(1) > FOOTER:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(2) > DIV:nth-of-type(1) > UL:nth-of-type(1) > LI:nth-of-type(2) > A:nth-of-type(1)"
               }
            }
         ]
      }
   ]
}
```

| Attribut | Typ | Beschreibung |
| --- | --- | --- |
| `payload.id` | Zeichenfolge | Die Entscheidungskennung. |
| `payload.scope` | String | Der Entscheidungsumfang, der zu den vorgeschlagenen Angeboten geführt hat. |
| `payload.scopeDetails.decisionProvider` | String | Bei Verwendung von Adobe Target auf `TGT` gesetzt. |
| `payload.scopeDetails.activity.id` | String | Die eindeutige ID der Angebotsaktivität. |
| `payload.scopeDetails.experience.id` | String | Die eindeutige ID der Angebotsplatzierung. |
| `items[].id` | String | Die eindeutige ID der Angebotsplatzierung. |
| `items[].data.id` | String | Die ID des vorgeschlagenen Angebots. |
| `items[].data.schema` | String | Das Schema des Inhalts, der mit dem vorgeschlagenen Angebot verknüpft ist. |
| `items[].data.format` | String | Das Format des Inhalts, der mit dem vorgeschlagenen Angebot verknüpft ist. |
| `items[].data.language` | String | Eine Reihe von Sprachen, die mit dem Inhalt des vorgeschlagenen Angebots verknüpft sind. |
| `items[].data.content` | String | Dem vorgeschlagenen Angebot im Zeichenfolgenformat entsprechender Inhalt |
| `items[].data.selector` | String | HTML-Selektor zur Identifizierung des DOM-Zielelements für ein DOM-Aktionsangebot. |
| `items[].data.prehidingSelector` | String | HTML-Selektor, der verwendet wird, um das DOM-Element zu identifizieren, das beim Bearbeiten eines DOM-Aktionsangebots ausgeblendet werden soll. |
| `items[].data.deliveryUrl` | String | Bildinhalt im Zusammenhang mit dem vorgeschlagenen Angebot im Format einer URL. |
| `items[].data.characteristics` | String | Merkmale, die mit dem vorgeschlagenen Angebot im Format eines JSON-Objekts verknüpft sind. |

## Beispiel für API-Aufruf {#sample-call}

**API-Format**

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
   "event":{
      "xdm":{
         "identityMap":{
            "Email_LC_SHA256":[
               {
                  "id":"0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b",
                  "primary":true
               }
            ]
         },
         "eventType":"web.webpagedetails.pageViews",
         "web":{
            "webPageDetails":{
               "URL":"https://alloystore.dev/",
               "name":"home-demo-Home Page"
            }
         },
         "timestamp":"2021-08-09T14:09:20.859Z"
      }
   },
   "query":{
      "personalization":{
         "schemas":[
            "https://ns.adobe.com/personalization/html-content-item",
            "https://ns.adobe.com/personalization/json-content-item",
            "https://ns.adobe.com/personalization/redirect-item",
            "https://ns.adobe.com/personalization/dom-action"
         ],
         "decisionScopes":[
            "__view__",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ"
         ]
      }
   }
}'
```

| Parameter | Typ | Erforderlich | Beschreibung |
| --- | --- | --- | --- |
| `configId` | Zeichenfolge | Ja | Die Datenstrom-ID. |
| `requestId` | Zeichenfolge | Nein | Geben Sie eine externe Anforderungsverfolgungs-ID an. Wenn keine angegeben wird, generiert das Edge Network eine für Sie und gibt sie im Antworttext/in den Kopfzeilen zurück. |

### Antwort {#response}

Gibt einen `200 OK` und mindestens ein `Handle` zurück, je nachdem, welche Edge-Services in der Datenstromkonfiguration aktiviert sind.

```json
{
   "requestId":"da20d11d-adac-458c-91ac-15bf4e420a15",
   "handle":[
      {
         "payload":[
            {
               "id":"AT:eyJhY3Rpdml0eUlkIjoiMTMxMDEwIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
               "scope":"__view__",
               "scopeDetails":{
                  "decisionProvider":"TGT",
                  "activity":{
                     "id":"131010"
                  },
                  "experience":{
                     "id":"0"
                  },
                  "strategies":[
                     {
                        "algorithmID":"0",
                        "trafficType":"0"
                     }
                  ]
               },
               "items":[
                  {
                     "id":"0",
                     "schema":"https://ns.adobe.com/personalization/dom-action",
                     "meta":{
                        "offer.name":"Default Content",
                        "experience.id":"0",
                        "activity.name":"Luma target reporting",
                        "activity.id":"131010",
                        "experience.name":"Experience A",
                        "option.id":"2",
                        "offer.id":"0"
                     },
                     "data":{
                        "type":"setHtml",
                        "format":"application/vnd.adobe.target.dom-action",
                        "content":"Customer Service not chrome",
                        "selector":"HTML > BODY > DIV.page-wrapper:eq(0) > FOOTER.page-footer:eq(0) > DIV.footer:eq(0) > DIV.links:eq(0) > DIV.widget:eq(0) > UL.footer:eq(0) > LI.nav:eq(1) > A:nth-of-type(1)",
                        "prehidingSelector":"HTML > BODY > DIV:nth-of-type(1) > FOOTER:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(2) > DIV:nth-of-type(1) > UL:nth-of-type(1) > LI:nth-of-type(2) > A:nth-of-type(1)"
                     }
                  }
               ]
            }
         ],
         "type":"personalization:decisions"
      }
   ]
}
```

## Benachrichtigungen {#notifications}

Benachrichtigungen sollten ausgelöst werden, wenn ein vorab abgerufener Inhalt oder eine vorab abgerufene Ansicht aufgerufen oder für den Endbenutzer gerendert wurde. Damit Benachrichtigungen für den richtigen Umfang ausgelöst werden, sollten Sie für jeden Bereich den entsprechenden `id` nachverfolgen.

Benachrichtigungen mit dem richtigen `id` für die entsprechenden Bereiche müssen ausgelöst werden, damit Berichte korrekt widergespiegelt werden.

**API-Format**

```http
POST /ee/v2/collect
```

### Anfrage {#notifications-request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/collect?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
-H "x-api-key: {API_KEY}"
-H "Content-Type: application/json"
-d '{
   "events":[
      {
         "xdm":{
            "identityMap":{
               "Email_LC_SHA256":[
                  {
                     "id":"0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b",
                     "primary":true
                  }
               ]
            },
            "eventType":"web.webpagedetails.pageViews",
            "web":{
               "webPageDetails":{
                  "URL":"https://alloystore.dev/",
                  "name":"home-demo-Home Page"
               }
            },
            "timestamp":"2021-08-09T14:09:20.859Z",
            "_experience":{
               "decisioning":{
                  "propositions":[
                     {
                        "id":"AT:eyJhY3Rpdml0eUlkIjoiMTMxMDEwIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
                        "scope":"__view__",
                        "items":[
                           {
                              "id":"0"
                           }
                        ]
                     }
                  ]
               }
            }
         }
      }
   ]
}'
```

| Parameter | Typ | Erforderlich | Beschreibung |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Ja | Die ID des vom Datenerfassungs-Endpunkt verwendeten Datenstroms. |
| `requestId` | `String` | Nein | Ablaufverfolgungs-ID der externen Anfrage. Wenn keine angegeben wird, generiert das Edge Network eine für Sie und gibt sie im Antworttext/in den Kopfzeilen zurück. |
| `silent` | `Boolean` | Nein | Optionaler boolescher Parameter, der angibt, ob das Edge Network eine `204 No Content` Antwort mit einer leeren Payload zurückgeben soll. Kritische Fehler werden mit dem entsprechenden HTTP-Status-Code und der entsprechenden Payload gemeldet. |

### Antwort {#notifications-response}

Eine erfolgreiche Antwort gibt einen der folgenden Status sowie eine -`requestID` zurück, wenn in der Anfrage keiner angegeben wurde.

* `202 Accepted`, wann die Anfrage erfolgreich verarbeitet wurde
* `204 No Content`, wann die Anfrage erfolgreich verarbeitet und der `silent` auf `true` gesetzt wurde;
* `400 Bad Request` wenn die Anfrage nicht ordnungsgemäß erstellt wurde (z. B. wurde die obligatorische primäre Identität nicht gefunden).

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```
