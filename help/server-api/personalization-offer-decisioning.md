---
title: Personalisierung über Offer Decisioning
description: Erfahren Sie, wie Sie mit der Server-API personalisierte Erlebnisse über Offer decisioning bereitstellen und rendern können.
exl-id: 5348cd3e-08db-4778-b413-3339cb56b35a
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 3%

---

# Personalisierung über Offer Decisioning

## Übersicht {#overview}

Die Edge Network Server-API kann personalisierte Erlebnisse bereitstellen, die in [Offer decisioning](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=de) verwaltet werden.

[!DNL Offer Decisioning] unterstützt eine nicht visuelle Benutzeroberfläche zum Erstellen, Aktivieren und Bereitstellen Ihrer Aktivitäten und Personalisierungserlebnisse.

## Voraussetzungen {#prerequisites}

Personalization über [!DNL Offer Decisioning] erfordert Zugriff auf [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=de) , bevor Sie Ihre Integration konfigurieren.

## Konfigurieren Ihres Datenspeichers {#configure-your-datastream}

Bevor Sie die Server-API zusammen mit Offer decisioning verwenden können, müssen Sie die Adobe Experience Platform-Personalisierung in Ihrer Datastraamkonfiguration aktivieren und die Option **[!UICONTROL Offer decisioning]** aktivieren.

Detaillierte Informationen zum Aktivieren von Offer decisioning finden Sie im [Handbuch zum Hinzufügen von Diensten zu einem Datastream](../datastreams/overview.md#adobe-experience-platform-settings).

![UI-Bild, das den Konfigurationsbildschirm des Datastream-Dienstes anzeigt, mit ausgewähltem Offer decisioning](assets/aep-od-datastream.png)

## Zielgruppenerstellung {#audience-creation}

[!DNL Offer Decisioning] verlässt sich bei der Erstellung von Zielgruppen auf den Segmentierungsdienst von Adobe Experience Platform. Die Dokumentation für die [!DNL Segmentation Service] [finden Sie hier](../segmentation/home.md).

## Definieren von Entscheidungsbereichen {#creating-decision-scopes}

Der [!DNL Offer Decision Engine] verwendet Adobe Experience Platform-Daten und [Echtzeit-Kundenprofile](../profile/home.md) zusammen mit dem [!DNL Offer Library], um den richtigen Kunden und Kanälen Angebote zur richtigen Zeit bereitzustellen.

Weitere Informationen zum [!DNL Offer Decisioning Engine] finden Sie in der entsprechenden [Dokumentation](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=de).

Nachdem Sie [Ihren Datastream](#configure-your-datastream) konfiguriert haben, müssen Sie die Entscheidungsbereiche definieren, die in Ihrer Personalisierungskampagne verwendet werden sollen.

[Entscheidungsbereiche](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/create-manage-activities/create-offer-activities.html#add-decision-scopes) sind die Base64-kodierten JSON-Zeichenfolgen, die die Aktivitäts- und Platzierungs-IDs enthalten, die die [!DNL Offer Decisioning Service] beim Vorschlagen von Angeboten verwenden soll.

**Entscheidungsbereich JSON**

```json
{
   "activityId":"xcore:offer-activity:11cfb1fa93381aca",
   "placementId":"xcore:offer-placement:1175009612b0100c"
}
```

**Entscheidungsumfang Base64-kodierter String**

```shell
"eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
```

Nachdem Sie Ihre Angebote und Sammlungen erstellt haben, müssen Sie einen [Entscheidungsbereich](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/create-manage-activities/create-offer-activities.html#add-decision-scopes) definieren.

Kopieren Sie den Base64-kodierten Entscheidungsbereich. Sie verwenden sie im `query` -Objekt der Server-API-Anfrage.

![UI-Bild, das die Offer decisioning-Benutzeroberfläche anzeigt und den Entscheidungsbereich hervorhebt.](assets/decision-scope.png)

```json
"query":{
   "personalization":{
      "decisionScopes":[
         "eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjE0ZWZjYTg5NDE4OTUxODEiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTJkNTQ0YWU1NGU3ZTdkYiJ9"
      ]
   }
}
```

## Beispiel für API-Aufruf {#api-example}

**API-Format**

```http
POST /ee/v2/interact
```

### Anfrage {#request}

Eine vollständige Anfrage mit einem vollständigen XDM-Objekt, Datenobjekt und einer Offer decisioning-Abfrage wird unten beschrieben.

>[!NOTE]
>
>Die Objekte `xdm` und `data` sind optional und sind nur für das Offer decisioning erforderlich, wenn Sie Segmente mit Bedingungen erstellt haben, die Felder in einem dieser Objekte verwenden.

```shell
curl -X POST 'https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org: {ORG_ID}' \
--header 'Authorization: Bearer {TOKEN}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "event": {
        "xdm": {
            "eventType": "web.webpagedetails.pageViews",
            "identityMap": {
                "ECID": [
                    {
                        "id": "05907638112924484241029082405297151763",
                        "authenticatedState": "ambiguous",
                        "primary": true
                    }
                ]
            },
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
                "version": "1.0",
                "environment": "serverapi"
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
            },
            "__adobe.target": {
                "profile.eyeColor": "brown",
                "profile.hairColor": "brown"
            }
        }
    },
    "query": {
        "personalization": {
            "decisionScopes": [
                "eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjE0ZWZjYTg5NDE4OTUxODEiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTJkNTQ0YWU1NGU3ZTdkYiJ9"
            ]
        }
    }
}'
```

### Antwort {#response}

Das Edge Network gibt eine Antwort zurück, die der unten stehenden ähnelt.

```json
{
   "requestId":"b375077d-7e1d-4c18-b7d3-e4da0fb4fbc5",
   "handle":[
      {
         "payload":[
            
         ],
         "type":"personalization:decisions",
         "eventIndex":0
      },
      {
         "payload":[
            {
               "id":"120d5db7-181c-42c5-8653-88b3cd3e1e69",
               "scope":"eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjE0ZWZjYTg5NDE4OTUxODEiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTJkNTQ0YWU1NGU3ZTdkYiJ9",
               "activity":{
                  "id":"xcore:offer-activity:14efca8941895181",
                  "etag":"1"
               },
               "placement":{
                  "id":"xcore:offer-placement:12d544ae54e7e7db",
                  "etag":"1"
               },
               "items":[
                  {
                     "id":"xcore:personalized-offer:14efc848a3577d92",
                     "etag":"2",
                     "schema":"https://ns.adobe.com/experience/offer-management/content-component-json",
                     "data":{
                        "id":"xcore:personalized-offer:14efc848a3577d92",
                        "format":"application/json",
                        "language":[
                           "en-us"
                        ],
                        "content":"{\n\t\"ODEFirstTest\" : \"Personalizaton Content\"\n}",
                        "characteristics":{
                           "reporting":"testRequest"
                        }
                     }
                  }
               ]
            }
         ],
         "type":"personalization:decisions",
         "eventIndex":0
      },
      {
         "payload":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
               "value":"CiYwNTkwNzYzODExMjkyNDQ4NDI0MTAyOTA4MjQwNTI5NzE1MTc2M1IOCLr6xb39LxgBKgNPUjLwAbr6xb39Lw==",
               "maxAge":34128000
            }
         ],
         "type":"state:store"
      }
   ]
}
```

Wenn der Besucher für eine Personalisierungsaktivität qualifiziert ist, die auf an [!DNL Offer Decisioning] gesendeten Daten basiert, wird der relevante Aktivitätsinhalt unter dem Objekt `handle` gefunden, wobei der Typ `personalization:decisions` ist.

Andere Inhalte werden auch unter dem Objekt `handle` zurückgegeben. Andere Inhaltstypen sind für die Personalisierung von [!DNL Offer Decisioning] nicht relevant. Wenn der Besucher für mehrere Aktivitäten qualifiziert ist, sind sie in einem Array enthalten.

In der folgenden Tabelle werden die Schlüsselelemente dieses Teils der Antwort erläutert.

| Eigenschaft | Beschreibung | Beispiel |
|---|---|---|
| `scope` | Der Entscheidungsbereich, der mit den zurückgegebenen Angeboten verknüpft ist. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | Die eindeutige Kennung der Angebotsaktivität. | `"id": "xcore:offer-activity:11cfb1fa93381aca"` |
| `placement.id` | Die eindeutige ID der Angebotsplatzierung. | `"id": "xcore:offer-placement:1175009612b0100c"` |
| `items.id` | Die eindeutige Kennung des vorgeschlagenen Angebots. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | Das Schema des dem vorgeschlagenen Angebot zugeordneten Inhalts. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | Die eindeutige Kennung des vorgeschlagenen Angebots. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | Das Format des mit dem vorgeschlagenen Angebot verknüpften Inhalts. | `"format": "text/html"` |
| `language` | Eine Reihe von Sprachen, die mit dem Inhalt des vorgeschlagenen Angebots verknüpft sind. | `"language": [ "en-US" ]` |
| `content` | Inhalt, der mit dem vorgeschlagenen Angebot in Form einer Zeichenfolge verknüpft ist. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Bildinhalt, der mit dem vorgeschlagenen Angebot verknüpft ist, im Format einer URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | JSON-Objekt, das die dem vorgeschlagenen Angebot zugeordneten Eigenschaften enthält. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |
