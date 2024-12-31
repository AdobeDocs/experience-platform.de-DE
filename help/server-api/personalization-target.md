---
title: Personalisierung über Adobe Target
description: Erfahren Sie, wie Sie mit der Server-API in Adobe Target erstellte personalisierte Erlebnisse bereitstellen und rendern können.
exl-id: c9e2f7ef-5022-4dc4-82b4-ecc210f27270
source-git-commit: ddffe9bf30741b457f7de1099b50ac1624fca927
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 3%

---

# Personalisierung über Adobe Target

## Übersicht {#overview}

Die Edge Network-Server-API kann mithilfe des [Form-Based Experience Composer) in Adobe Target erstellte personalisierte Erlebnisse bereitstellen und ](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=de).

>[!IMPORTANT]
>
>Personalization-Erlebnisse, die mit [Target Visual Experience Composer (VEC) erstellt ](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html), werden von der Server-API nicht vollständig unterstützt. Die Server-API kann **von VEC erstellte Aktivitäten** abrufen), die Server-API kann jedoch **von VEC erstellte Aktivitäten nicht** rendern). Wenn Sie die von VEC erstellten Aktivitäten rendern möchten, implementieren Sie die [hybride Personalisierung](../web-sdk/personalization/hybrid-personalization.md) mithilfe der Web-SDK und der Edge Network-Server-API.

## Konfigurieren des Datenstroms {#configure-your-datastream}

Bevor Sie die Server-API in Verbindung mit Adobe Target verwenden können, müssen Sie die Adobe Target-Personalisierung in Ihrer Datenstromkonfiguration aktivieren.

Ausführliche Informationen [ Aktivieren von Adobe Target finden Sie im ](../datastreams/overview.md#adobe-target-settings) zum Hinzufügen von Services zu einem Datenstrom .

Beim Konfigurieren Ihres Datenstroms können Sie (optional) Werte für [!DNL Property Token], [!DNL Target Environment ID] und [!DNL Target Third Party ID Namespace] angeben.

![UI-Bild, das den Konfigurationsbildschirm des Datenstrom-Service mit ausgewählter Adobe Target anzeigt](assets/target-datastream.png)

## Benutzerdefinierte Parameter {#custom-parameters}

Die meisten Felder im [!DNL XDM] Teil jeder Anfrage werden in Punktnotation serialisiert und dann als benutzerdefinierte oder [!DNL mbox] Parameter an Target gesendet.


### Beispiel {#custom-parameters-example}

Unter Berücksichtigung des folgenden XDM-Beispiels:

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

## Aktualisierungen des Zielprofils {#profile-update}

Der [!DNL Server API] ermöglicht Aktualisierungen am Zielprofil. Um ein Zielprofil zu aktualisieren, stellen Sie sicher, dass die Profildaten im `data` Teil der Anfrage im folgenden Format übergeben werden:

```json
"data":  {
    "__adobe.target": {
        "profile.eyeColor": "brown",
        "profile.hairColor": "brown"
    }
}
```

## Abfrage von Target-Aktivitäten {#querying-target-activities}

### Schemata {#schemas}

Der Abfrageteil der Anfrage bestimmt, welche Inhalte von Target zurückgegeben werden. Unter dem `personalization`-Objekt bestimmt `schemas` den Typ des von Target zurückzugebenden Inhalts.

In Situationen, in denen Sie sich nicht sicher sind, welche Art von Angeboten Sie abrufen werden, sollten Sie alle vier Schemata in Ihre Personalisierungsabfrage an das Edge Network einbeziehen:

* **HTML-basierte Angebote:**
https://ns.adobe.com/personalization/html-content-item
* **JSON-basierte Angebote:**
https://ns.adobe.com/personalization/json-content-item
* **Target-Umleitungsangebote**
https://ns.adobe.com/personalization/redirect-item
* **Target-Angebote zur DOM-Manipulation**
https://ns.adobe.com/personalization/dom-action

### Entscheidungsumfänge {#decision-scopes}

Adobe Target-[!DNL mbox] sollten im `decisionScopes`-Array enthalten sein, um den entsprechenden Inhalt zurückzugeben.

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

## Beispiel für einen API-Aufruf {#api-example}

**API-Format**

```http
POST /ee/v2/interact
```

### Anfrage {#request}

Nachfolgend finden Sie eine vollständige Anfrage mit einem vollständigen XDM-Objekt, Profilparametern und der entsprechenden Target-Abfrage.

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

Das Edge Network gibt eine -Antwort ähnlich der folgenden zurück.

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

Wenn der Besucher basierend auf den an Adobe Target gesendeten Daten für eine Personalisierungsaktivität qualifiziert ist, wird der entsprechende Aktivitätsinhalt unter dem `handle` gefunden, wobei der Typ `personalization:decisions` ist.

Manchmal werden auch andere Inhalte unter `handle` zurückgegeben. Andere Inhaltstypen sind für die Target-Personalisierung nicht relevant. Wenn der Besucher für mehrere Aktivitäten qualifiziert ist, ist jede Aktivität ein separates `personalization` im Array.

In der folgenden Tabelle werden die Schlüsselelemente dieses Teils der Antwort erläutert.

| Eigenschaft | Beschreibung | Beispiel |
|---|---|---|
| `scope` | Der Name der Ziel-Mbox, der zu den vorgeschlagenen Angeboten geführt hat. | `"scope": "serverapimbox"` |
| `items[].schema` | Das Schema des Inhalts, der mit dem vorgeschlagenen Angebot verknüpft ist. Dieser Wert hängt vom Aktivitätstyp ab, den Sie beim Erstellen der Personalisierungsaktivität ausgewählt haben. | `"schema": "https://ns.adobe.com/personalization/json-content-item",` |
| `items[].meta.activity.id` | Die eindeutige ID der Angebotsaktivität. In der Regel eine 6-stellige Zahl. | `"activity.id": "140281"` |
| `items[].meta.activity.name` | Der Name der benutzerdefinierten Angebotsaktivität. Dies wird während des Schritts zur Erstellung der Aktivität bereitgestellt. | `"activity.name": "Server API Form"` |
| `items[].meta.experience.id` | Die eindeutige ID des Personalisierungserlebnisses. | `"experience.id": "0"` |
| `items[].meta.experience.name` | Der eindeutige Name des Personalisierungserlebnisses. | `"experience.name": "Experience A"` |
| `items[].data.id` | Die ID des vorgeschlagenen Angebots. | `"id": "282484"` |
| `items[].data.format` | Das Format des Inhalts, der mit dem vorgeschlagenen Angebot verknüpft ist. | `"format: "application/json` |
| `items[].data.content` | Mit dem vorgeschlagenen Angebot verknüpfter Inhalt Dies wird für die Personalisierung des Inhalts der aufrufenden Anwendung verwendet. | `"content": "<CONTENT CONFIGURED IN TARGET>"` |

## Beispielanwendung für die Server-seitige Personalisierung {#sample}

Die Beispielanwendung unter [diese URL](https://github.com/adobe/alloy-samples/tree/main/target/personalization-server-side) veranschaulicht die Verwendung von Adobe Experience Platform zum Abrufen von Personalisierungsinhalten aus Adobe Target. Die Web-Seite ändert sich je nach dem zurückgegebenen Personalisierungsinhalt.

Dieses Beispiel _sich_ Client-seitigen Bibliotheken wie dem [!DNL Web SDK], um Personalisierungsinhalte zu erhalten. Stattdessen werden die Adobe Experience Platform-APIs zum Abrufen von Personalisierungsinhalten verwendet. Anschließend generiert die Implementierung die HTML Server-seitig basierend auf dem zurückgegebenen Personalisierungsinhalt.
