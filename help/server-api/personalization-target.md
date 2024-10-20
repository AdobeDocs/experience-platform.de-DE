---
title: Personalisierung über Adobe Target
description: Erfahren Sie, wie Sie mit der Server-API personalisierte Erlebnisse bereitstellen und rendern können, die in Adobe Target erstellt wurden.
exl-id: c9e2f7ef-5022-4dc4-82b4-ecc210f27270
source-git-commit: ddffe9bf30741b457f7de1099b50ac1624fca927
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 3%

---

# Personalisierung über Adobe Target

## Übersicht {#overview}

Die Edge Network Server-API kann mithilfe des [formularbasierten Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=de) personalisierte Erlebnisse bereitstellen und rendern, die in Adobe Target erstellt wurden.

>[!IMPORTANT]
>
>Personalization-Erlebnisse, die über den [Target Visual Experience Composer (VEC)](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) erstellt wurden, werden von der Server-API nicht vollständig unterstützt. Die Server-API kann **von VEC erstellte** -Aktivitäten abrufen, die Server-API kann jedoch keine von VEC erstellten **render** -Aktivitäten rendern. Wenn Sie von VEC erstellte Aktivitäten rendern möchten, implementieren Sie die [Hybrid-Personalisierung](../web-sdk/personalization/hybrid-personalization.md) mit dem Web SDK und der Edge Network Server-API.

## Konfigurieren Ihres Datenspeichers {#configure-your-datastream}

Bevor Sie die Server-API in Verbindung mit Adobe Target verwenden können, müssen Sie die Adobe Target-Personalisierung für Ihre Datastream-Konfiguration aktivieren.

Detaillierte Informationen zum Aktivieren von Adobe Target finden Sie im [Handbuch zum Hinzufügen von Diensten zu einem Datastream](../datastreams/overview.md#adobe-target-settings) .

Beim Konfigurieren Ihres Datastreams können Sie (optional) Werte für [!DNL Property Token], [!DNL Target Environment ID] und [!DNL Target Third Party ID Namespace] angeben.

![UI-Bild, das den Konfigurationsbildschirm des Datastream-Dienstes anzeigt, wobei Adobe Target ausgewählt ist](assets/target-datastream.png)

## Benutzerdefinierte Parameter {#custom-parameters}

Die meisten Felder im Abschnitt [!DNL XDM] jeder Anfrage werden in Punktnotation serialisiert und dann als benutzerdefinierte Parameter oder Parameter an Target gesendet.[!DNL mbox]


### Beispiel {#custom-parameters-example}

Für das folgende XDM-Beispiel:

```json
"xdm":{
   "marketing":{
      "campaignGroup":"winter22",
      "campaignName":"homeOwnerPromo22",
      "trackingCode":"hop22"
   }
}
```

Beim Erstellen von Zielgruppen in Target stehen die folgenden Werte als benutzerdefinierte Parameter zur Verfügung:

* `marketing.campaignGroup`
* `marketing.campaignName`
* `marketing.trackingCode`

## Target-Profilaktualisierungen {#profile-update}

Der [!DNL Server API] ermöglicht Aktualisierungen am Target-Profil. Um ein Target-Profil zu aktualisieren, stellen Sie sicher, dass die Profildaten im Abschnitt `data` der Anfrage im folgenden Format übergeben werden:

```json
"data":  {
    "__adobe.target": {
        "profile.eyeColor": "brown",
        "profile.hairColor": "brown"
    }
}
```

## Abfrage zu Target-Aktivitäten {#querying-target-activities}

### Schemata {#schemas}

Der Abfrageteil der Anfrage bestimmt, welcher Inhalt von Target zurückgegeben wird. Unter dem Objekt `personalization` bestimmt `schemas` den von Target zurückzugebenden Inhaltstyp.

In Situationen, in denen Sie sich nicht sicher sind, welche Art von Angeboten Sie abrufen werden, sollten Sie alle vier Schemas in Ihre Personalisierungsabfrage einschließen:

* **HTML-basierte Angebote:**
https://ns.adobe.com/personalization/html-content-item
* **JSON-basierte Angebote:**
https://ns.adobe.com/personalization/json-content-item
* **Target-Umleitungsangebote**
https://ns.adobe.com/personalization/redirect-item
* **DOM-Verarbeitungsangebote für Target**
https://ns.adobe.com/personalization/dom-action

### Entscheidungsumfänge {#decision-scopes}

Adobe Target [!DNL mbox] -Namen sollten im Array `decisionScopes` enthalten sein, um den entsprechenden Inhalt zurückzugeben.

#### Beispiel {#decision-scopes-example}

Im folgenden Beispiel werden alle vier Angebotstypen zusammen mit einer Target-Aktivität namens `serverapimbox` angefordert.

```json
"query":{
   "personalization":{
      "schemas":[
         "https://ns.adobe.com/personalization/html-content-item",
         "https://ns.adobe.com/personalization/json-content-item",
         "https://ns.adobe.com/personalization/redirect-item",
         "https://ns.adobe.com/personalization/dom-action"
      ],
      "decisionScopes":[
         "serverapimbox"
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

Eine vollständige Anfrage mit einem vollständigen XDM-Objekt und Profilparametern sowie der entsprechenden Target-Abfrage wird unten beschrieben.

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
            },
            "data": {
                "__adobe": {
                    "target": {
                        "profile.eyeColor": "brown",
                        "profile.hairColor": "brown",
                        "profile.shoeColor": "black"
                    }
                }
            }
        }
    },
    "query": {
        "personalization": {
            "schemas": [
                "https://ns.adobe.com/personalization/html-content-item",
                "https://ns.adobe.com/personalization/json-content-item",
                "https://ns.adobe.com/personalization/redirect-item",
                "https://ns.adobe.com/personalization/dom-action"
            ],
            "decisionScopes": [
                "serverapimbox"
            ]
        }
    }
}'
```

### Antwort {#response}

Das Edge Network gibt eine Antwort zurück, die der unten stehenden ähnelt.

```json
{
   "requestId":"10959bbf-f83d-40e1-9521-d9145f19cdc5",
   "handle":[
      {
         "payload":[
            {
               "id":"AT:eyJhY3Rpdml0eUlkIjoiMTQwMjgxIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
               "scope":"serverapimbox",
               "scopeDetails":{
                  "decisionProvider":"TGT",
                  "activity":{
                     "id":"140281"
                  },
                  "experience":{
                     "id":"0"
                  },
                  "strategies":[
                     {
                        "algorithmID":"0",
                        "trafficType":"0"
                     }
                  ],
                  "characteristics":{
                     "eventToken":"xycjBJlZhwVV5MN0kMkmoGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw=="
                  }
               },
               "items":[
                  {
                     "id":"282484",
                     "schema":"https://ns.adobe.com/personalization/json-content-item",
                     "meta":{
                        "offer.name":"/server_apiform/experiences/0/pages/0/zones/0/1648103551041",
                        "experience.id":"0",
                        "activity.name":"Server API Form",
                        "activity.id":"140281",
                        "experience.name":"Experience A",
                        "option.id":"2",
                        "offer.id":"282484"
                     },
                     "data":{
                        "id":"282484",
                        "format":"application/json",
                        "content":{
                           "value":"a/b json experience a",
                           "platform":"server"
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
               "value":"CiYwNTkwNzYzODExMjkyNDQ4NDI0MTAyOTA4MjQwNTI5NzE1MTc2M1IOCL-pwpv9LxgBKgNPUjLwAb-pwpv9Lw==",
               "maxAge":34128000
            }
         ],
         "type":"state:store"
      }
   ]
}
```

Wenn der Besucher auf der Grundlage der an Adobe Target gesendeten Daten für eine Personalisierungsaktivität qualifiziert ist, wird der relevante Aktivitätsinhalt unter dem Objekt `handle` gefunden, wobei der Typ `personalization:decisions` ist.

Andere Inhalte werden manchmal auch unter `handle` zurückgegeben. Andere Inhaltstypen sind für die Target-Personalisierung nicht relevant. Wenn der Besucher für mehrere Aktivitäten qualifiziert ist, ist jede Aktivität ein separates `personalization` -Objekt im Array.

In der folgenden Tabelle werden die Schlüsselelemente dieses Teils der Antwort erläutert.

| Eigenschaft | Beschreibung | Beispiel |
|---|---|---|
| `scope` | Der Target-Mbox-Name, der zu den vorgeschlagenen Angeboten führte. | `"scope": "serverapimbox"` |
| `items[].schema` | Das Schema des dem vorgeschlagenen Angebot zugeordneten Inhalts. Dies hängt vom Aktivitätstyp ab, den Sie bei der Erstellung der Personalisierungsaktivität ausgewählt haben. | `"schema": "https://ns.adobe.com/personalization/json-content-item",` |
| `items[].meta.activity.id` | Die eindeutige Kennung der Angebotsaktivität. Normalerweise eine 6-stellige Zahl. | `"activity.id": "140281"` |
| `items[].meta.activity.name` | Der Name der vom Benutzer angegebenen Angebotsaktivität. Dies wird während des Erstellungsschritts der Aktivität bereitgestellt. | `"activity.name": "Server API Form"` |
| `items[].meta.experience.id` | Die eindeutige ID des Personalisierungserlebnisses. | `"experience.id": "0"` |
| `items[].meta.experience.name` | Der eindeutige Name des Personalisierungserlebnisses. | `"experience.name": "Experience A"` |
| `items[].data.id` | Die Kennung des vorgeschlagenen Angebots. | `"id": "282484"` |
| `items[].data.format` | Das Format des mit dem vorgeschlagenen Angebot verknüpften Inhalts. | `"format: "application/json` |
| `items[].data.content` | Inhalt des vorgeschlagenen Angebots. Dieser wird zur Personalisierung des Inhalts der aufrufenden Anwendung verwendet. | `"content": "<CONTENT CONFIGURED IN TARGET>"` |

## Beispielanwendung für serverseitige Personalisierung {#sample}

Die Beispielanwendung unter [dieser URL](https://github.com/adobe/alloy-samples/tree/main/target/personalization-server-side) zeigt, wie Adobe Experience Platform verwendet wird, um Personalisierungsinhalte von Adobe Target zu erhalten. Die Webseite ändert sich je nach zurückgegebenem Personalisierungsinhalt.

Dieses Beispiel benötigt _nicht_ Client-seitige Bibliotheken wie die [!DNL Web SDK], um Personalisierungsinhalte zu erhalten. Stattdessen werden die Adobe Experience Platform-APIs zum Abrufen von Personalisierungsinhalten verwendet. Anschließend generiert die Implementierung die HTML Server-seitig basierend auf dem zurückgegebenen Personalisierungsinhalt.
