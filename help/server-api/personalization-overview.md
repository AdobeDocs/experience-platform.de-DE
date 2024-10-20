---
title: Personalisierung – Übersicht
description: Erfahren Sie, wie Sie mit der Adobe Experience Platform Edge Network Server API personalisierte Inhalte aus Adobe-Personalisierungslösungen abrufen können.
exl-id: 11be9178-54fe-49d0-b578-69e6a8e6ab90
source-git-commit: ae6c6d21b1eea900d01be3287827296071429d30
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 10%

---

# Personalisierung – Übersicht

Mit dem [!DNL Server API] können Sie personalisierte Inhalte aus Adobe-Personalisierungslösungen abrufen, darunter [Adobe Target](https://business.adobe.com/de/products/target/adobe-target.html), [Adobe Journey Optimizer](https://experienceleague.adobe.com/de/docs/journey-optimizer/using/ajo-home) und [Offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=de).

Darüber hinaus ermöglicht der [!DNL Server API] Personalisierungsfunktionen für die gleiche Seite und die nächste Seite über Adobe Experience Platform-Personalisierungsziele wie [Adobe Target](../destinations/catalog/personalization/adobe-target-connection.md) und die [benutzerdefinierte Personalisierungsverbindung](../destinations/catalog/personalization/custom-personalization.md). Informationen zum Konfigurieren von Experience Platform für die Personalisierung von Seiten mit und nächsten Seiten finden Sie im [dedizierten Handbuch](../destinations/ui/activate-edge-personalization-destinations.md).

Bei Verwendung der Server-API müssen Sie die Antwort der Personalisierungsmaschine in die Logik integrieren, die zum Rendern von Inhalten auf Ihrer Site verwendet wird. Im Gegensatz zum [Web SDK](../web-sdk/home.md) verfügt der [!DNL Server API] nicht über einen Mechanismus zur automatischen Anwendung von Inhalten, die von Adobe-Personalisierungslösungen zurückgegeben werden.

## Terminologie {#terminology}

Bevor Sie mit Adobe-Personalisierungslösungen arbeiten, sollten Sie sich mit den folgenden Konzepten vertraut machen:

* **Angebot**: Ein Angebot ist eine Marketing-Botschaft, der ggf. Regeln zugeordnet sind, die angeben, wer sich zum Anzeigen des Angebots eignet.
* **Entscheidung**: Eine Entscheidung (zuvor als Angebotsaktivität bezeichnet) informiert über die Auswahl eines Angebots.
* **Schema**: Das Schema einer Entscheidung informiert über den zurückgegebenen Angebotstyp.
* **Umfang**: Der Umfang der Entscheidung.
   * In Adobe Target ist dies der [!DNL mbox]. Der [!DNL global mbox] ist der `__view__` Umfang
   * Für [!DNL Offer Decisioning] sind dies die Base64-kodierten Zeichenfolgen von JSON, die die Aktivitäts- und Platzierungs-IDs enthalten, die der offer decisioning-Dienst verwenden soll, um Angebote vorzuschlagen.

## Das Objekt `query` {#query-object}

Für das Abrufen personalisierter Inhalte ist ein explizites Abfrageobjekt für eine Anfrage erforderlich. Das Abfrageobjekt weist das folgende Format auf:

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
| `schemas` | `String[]` | Erforderlich für die Target-Personalisierung. Optional für Offer decisioning. | Liste der in der Entscheidung verwendeten Schemata, um den zurückgegebenen Angebotstyp auszuwählen. |
| `scopes` | `String[]` | Optional | Liste der Entscheidungsbereiche. Maximal 30 pro Anfrage. |

## Das handle -Objekt {#handle}

Der personalisierte Inhalt, der aus Personalisierungslösungen abgerufen wird, wird in einem `personalization:decisions` -Handle dargestellt, das für die Payload das folgende Format aufweist:

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
| `payload.scope` | Zeichenfolge | Der Entscheidungsbereich, der zu den vorgeschlagenen Angeboten führte. |
| `payload.scopeDetails.decisionProvider` | Zeichenfolge | Bei Verwendung von Adobe Target auf `TGT` setzen. |
| `payload.scopeDetails.activity.id` | Zeichenfolge | Die eindeutige Kennung der Angebotsaktivität. |
| `payload.scopeDetails.experience.id` | Zeichenfolge | Die eindeutige ID der Angebotsplatzierung. |
| `items[].id` | Zeichenfolge | Die eindeutige ID der Angebotsplatzierung. |
| `items[].data.id` | Zeichenfolge | Die Kennung des vorgeschlagenen Angebots. |
| `items[].data.schema` | Zeichenfolge | Das Schema des dem vorgeschlagenen Angebot zugeordneten Inhalts. |
| `items[].data.format` | Zeichenfolge | Das Format des mit dem vorgeschlagenen Angebot verknüpften Inhalts. |
| `items[].data.language` | Zeichenfolge | Eine Reihe von Sprachen, die mit dem Inhalt des vorgeschlagenen Angebots verknüpft sind. |
| `items[].data.content` | Zeichenfolge | Inhalt, der mit dem vorgeschlagenen Angebot in Form einer Zeichenfolge verknüpft ist. |
| `items[].data.selector` | Zeichenfolge | HTML-Selektor zur Identifizierung des Ziel-DOM-Elements für ein DOM-Aktionsangebot. |
| `items[].data.prehidingSelector` | Zeichenfolge | HTML-Selektor zur Identifizierung des DOM-Elements, das beim Verarbeiten eines DOM-Aktionangebots ausgeblendet werden soll. |
| `items[].data.deliveryUrl` | Zeichenfolge | Bildinhalt, der mit dem vorgeschlagenen Angebot verknüpft ist, im Format einer URL. |
| `items[].data.characteristics` | Zeichenfolge | Mit dem vorgeschlagenen Angebot verknüpfte Eigenschaften im Format eines JSON-Objekts. |

## Beispiel-API-Aufruf {#sample-call}

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
| `configId` | Zeichenfolge | Ja | Die Datenspeicher-ID. |
| `requestId` | Zeichenfolge | Nein | Geben Sie eine externe Anfrage-Tracking-ID an. Wenn keines angegeben ist, generiert das Edge Network eines für Sie und gibt es im Antworttext/in den Kopfzeilen zurück. |

### Antwort {#response}

Gibt je nach den in der Datastream-Konfiguration aktivierten Edge-Diensten den Status `200 OK` und ein oder mehrere `Handle` -Objekte zurück.

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

Benachrichtigungen sollten ausgelöst werden, wenn ein zuvor abgerufener Inhalt oder eine zuvor abgerufene Ansicht besucht oder für den Endbenutzer gerendert wurde. Damit Benachrichtigungen für den richtigen Bereich ausgelöst werden, achten Sie darauf, den entsprechenden `id` -Wert für jeden Bereich zu verfolgen.

Benachrichtigungen mit dem richtigen &quot;`id`&quot;-Wert für die entsprechenden Bereiche müssen ausgelöst werden, damit die Berichterstellung korrekt dargestellt werden kann.

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
| `dataStreamId` | `String` | Ja | Die ID des vom Datenerfassungs-Endpunkt verwendeten Datastreams. |
| `requestId` | `String` | Nein | Ablaufverfolgungs-ID externer Anfragen. Wenn keines angegeben ist, generiert das Edge Network eines für Sie und gibt es im Antworttext/in den Kopfzeilen zurück. |
| `silent` | `Boolean` | Nein | Optionaler boolean -Parameter, der angibt, ob das Edge Network eine `204 No Content` -Antwort mit einer leeren Payload zurückgeben soll. Kritische Fehler werden mithilfe des entsprechenden HTTP-Status-Codes und der Payload gemeldet. |

### Antwort {#notifications-response}

Eine erfolgreiche Antwort gibt einen der folgenden Status zurück und einen `requestID` , wenn in der Anfrage keiner angegeben wurde.

* `202 Accepted` , wenn die Anfrage erfolgreich verarbeitet wurde;
* `204 No Content` , wenn die Anfrage erfolgreich verarbeitet wurde und der Parameter `silent` auf `true` gesetzt wurde;
* `400 Bad Request` , wenn die Anforderung nicht ordnungsgemäß gebildet wurde (z. B. die obligatorische primäre Identität nicht gefunden wurde).

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```
