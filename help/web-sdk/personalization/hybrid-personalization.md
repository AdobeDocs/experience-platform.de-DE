---
title: Hybride Personalisierung mit Web SDK und Edge Network Server API
description: In diesem Artikel wird gezeigt, wie Sie das Web SDK in Verbindung mit der Server-API verwenden können, um hybride Personalisierung in Ihren Web-Eigenschaften bereitzustellen.
keywords: Personalisierung;hybride;Server-API;Server-seitig;Hybridimplementierung;
exl-id: 506991e8-701c-49b8-9d9d-265415779876
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 94%

---

# Hybride Personalisierung mit Web SDK und Edge Network Server API

## Übersicht {#overview}

Die hybride Personalisierung beschreibt den Prozess des Server-seitigen Abrufens von Personalisierungsinhalten mithilfe der [Edge Network Server-API](../../server-api/overview.md) und des Client-seitigen Renderns mithilfe des [Web SDK](../home.md).

Sie können hybride Personalisierung mit Personalisierungslösungen wie Adobe Target oder Offer Decisioning verwenden, wobei der Unterschied in den Payload-Inhalten der [!UICONTROL Server-API] besteht.

## Voraussetzungen {#prerequisites}

Bevor Sie hybride Personalisierung in Ihre Web-Eigenschaften implementieren, müssen Sie sicherstellen, dass Sie die folgenden Bedingungen erfüllen:

* Sie haben entschieden, welche Personalisierungslösung Sie verwenden möchten. Dies wirkt sich auf die Payload-Inhalte der [!UICONTROL Server-API] aus.
* Sie haben Zugriff auf einen Anwendungs-Server, mit dem Sie die Aufrufe der [!UICONTROL Server-API] vornehmen können.
* Sie haben Zugriff auf die [Edge Network Server API](../../server-api/authentication.md).
* Sie haben richtig [konfiguriert](/help/web-sdk/commands/configure/overview.md) und das Web SDK auf den Seiten bereitgestellt, die Sie personalisieren möchten.

## Flussdiagramm {#flow-diagram}

Im folgenden Flussdiagramm wird die Reihenfolge der Schritte beschrieben, die zur Bereitstellung der hybriden Personalisierung unternommen werden.

![Visuelles Flussdiagramm, das die Reihenfolge der Schritte anzeigt, die zur Bereitstellung der hybriden Personalisierung unternommen werden.](assets/hybrid-personalization-diagram.png)

1. Alle vorhandenen Cookies, die zuvor vom Browser gespeichert wurden, sind, mit dem Präfix `kndctr_` versehen, in der Browser-Anfrage enthalten.
1. Der Client-Webbrowser fordert die Webseite von Ihrem Anwendungs-Server an.
1. Wenn der Anwendungs-Server die Seitenanforderung erhält, führt er eine `POST`-Anfrage an den [interaktiven Datenerfassungs-Endpunkt der Server-API](../../server-api/interactive-data-collection.md) durch, um Personalisierungsinhalte abzurufen. Die `POST`-Anfrage enthält ein `event` und eine `query`. Die Cookies aus dem vorherigen Schritt sind, sofern verfügbar, im Array `meta>state>entries` enthalten.
1. Die Server-API gibt die Personalisierungsinhalte an Ihren Anwendungs-Server zurück.
1. Der Anwendungs-Server gibt eine HTML-Antwort an den Client-Browser zurück, die die [Identitäts- und Cluster-Cookies](#cookies) enthält.
1. Auf der Client-Seite wird der Befehl [!DNL Web SDK] `applyResponse` aufgerufen, wobei die Kopfzeilen und der Hauptteil der Antwort der [!UICONTROL Server-API] aus dem vorherigen Schritt übergeben werden.
1. Das [!DNL Web SDK] rendert das Laden der Angebotsseiten von [[!DNL Visual Experience Composer (VEC)]](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) automatisch, da das `renderDecisions`-Flag auf `true` gesetzt ist.
1. Formularbasierte [!DNL JSON]-Angebote werden manuell über die Methode `applyPersonalization` angewendet, um die [!DNL DOM] basierend auf dem Personalisierungsangebot zu aktualisieren.
1. Bei formularbasierten Aktivitäten müssen Anzeigeereignisse manuell gesendet werden, um anzugeben, wann das Angebot angezeigt wurde. Dies geschieht über den Befehl `sendEvent`.

## Cookies {#cookies}

Cookies werden verwendet, um die Benutzeridentität und Cluster-Informationen beizubehalten.  Bei Verwendung einer Hybridimplementierung übernimmt der Web-Anwendungs-Server das Speichern und Senden dieser Cookies während des Lebenszyklus der Anfrage.

| Cookie | Zweck | Gespeichert von | Gesendet von |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | Enthält Details zur Benutzeridentität. | Anwendungs-Server | Anwendungs-Server |
| `kndctr_AdobeOrg_cluster` | Gibt an, welcher Edge Network-Cluster zur Erfüllung der Anforderungen verwendet werden soll. | Anwendungs-Server | Anwendungs-Server |

## Platzierung anfordern {#request-placement}

Server-API-Anfragen sind erforderlich, um Vorschläge zu erhalten und eine Anzeigebenachrichtigung zu senden. Bei Verwendung einer Hybridimplementierung sendet der Anwendungs-Server diese Anfragen an die Server-API.

| Anfrage | Gemacht von |
|---|---|
| Interaktionsanfrage zum Abrufen von Vorschlägen | Anwendungs-Server |
| Interaktionsanfrage zum Senden von Anzeigebenachrichtigungen | Anwendungs-Server |

## Analytics-Auswirkungen {#analytics}

Bei der Implementierung der hybriden Personalisierung müssen Sie besonders darauf achten, dass Seitentreffer in Analytics nicht mehrmals gezählt werden.

Wenn Sie für Analytics [einen Datenstrom konfigurieren](../../datastreams/overview.md), werden Ereignisse automatisch weitergeleitet, sodass Seitentreffer erfasst werden.

Das Beispiel aus dieser Implementierung verwendet zwei verschiedene Datenströme:

* Ein für Analytics konfigurierter Datenstrom. Dieser Datenstrom wird für Web SDK-Interaktionen verwendet.
* Ein zweiter Datenstrom ohne eine Analytics-Konfiguration. Dieser Datastream wird für Server-API-Anfragen verwendet. Sie müssen diesen Datastream mit derselben Zielkonfiguration wie den für Analytics konfigurierten Datastream konfigurieren.

Auf diese Weise werden bei der Server-seitigen Anforderung keine Analytics-Ereignisse registriert, bei den Client-seitigen Anforderungen jedoch schon. Dies führt dazu, dass Analytics-Anforderungen genau gezählt werden.


## Server-seitige Anfrage {#server-side-request}

Die folgende Beispielanfrage zeigt eine Server-API-Anfrage, mit der Ihr Anwendungs-Server die Personalisierungsinhalte abrufen kann.

>[!IMPORTANT]
>
>In dieser Beispielanfrage wird Adobe Target als Personalisierungslösung verwendet. Ihre Anfrage kann je nach ausgewählter Personalisierungslösung variieren.


**API-Format**

```http
POST /ee/v2/interact
```

### Anfrage {#request}

```shell
curl -X POST "https://edge.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}" 
-H "Content-Type: text/plain" 
-d '{
   "event":{
      "xdm":{
         "web":{
            "webPageDetails":{
               "URL":"http://localhost/"
            },
            "webReferrer":{
               "URL":""
            }
         },
         "identityMap":{
            "FPID":[
               {
                  "id":"xyz",
                  "authenticatedState":"ambiguous",
                  "primary":true
               }
            ]
         },
         "timestamp":"2022-06-23T22:21:00.878Z"
      },
      "data":{
         
      }
   },
   "query":{
      "identity":{
         "fetch":[
            "ECID"
         ]
      },
      "personalization":{
         "schemas":[
            "https://ns.adobe.com/personalization/default-content-item",
            "https://ns.adobe.com/personalization/html-content-item",
            "https://ns.adobe.com/personalization/json-content-item",
            "https://ns.adobe.com/personalization/redirect-item",
            "https://ns.adobe.com/personalization/dom-action"
         ],
         "decisionScopes":[
            "__view__",
            "sample-json-offer"
         ]
      }
   },
   "meta":{
      "state":{
         "domain":"localhost",
         "cookiesEnabled":true,
         "entries":[
            {
               "key":"kndctr_XXX_AdobeOrg_identity",
               "value":"abc123"
            },
            {
               "key":"kndctr_XXX_AdobeOrg_cluster",
               "value":"or2"
            }
         ]
      }
   }
}'
```

| Parameter | Typ | Erforderlich | Beschreibung |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Ja. | Die ID des Datenstroms, mit dem Sie die Interaktionen an das Edge-Netzwerk weitergeben. Siehe [Datenströme – Übersicht](../../datastreams/overview.md), um zu erfahren, wie Sie einen Datenstrom konfigurieren. |
| `requestId` | `String` | Nein | Eine zufällige ID zum Korrelieren interner Server-Anfragen. Wenn keine angegeben ist, generiert das Edge-Netzwerk eine und gibt sie in der Antwort zurück. |

### Server-seitige Antwort {#server-response}

Die folgende Beispielantwort zeigt, wie die Antwort der Server-API aussehen könnte.


```json
{
   "requestId":"5c539bd0-33bf-43b6-a054-2924ac58038b",
   "handle":[
      {
         "payload":[
            {
               "id":"XXX",
               "namespace":{
                  "code":"ECID"
               }
            }
         ],
         "type":"identity:result"
      },
      {
         "payload":[
            {
               "..."
            },
            {
               "..."
            }
         ],
         "type":"personalization:decisions",
         "eventIndex":0
      }
   ]
}
```

## Client-seitige Anfrage {#client-request}

Auf der Client-Seite wird der Befehl [!DNL Web SDK] `applyResponse` aufgerufen, wobei die Kopfzeilen und der Hauptteil der Server-seitigen Antwort übergeben werden.

```js
   alloy("applyResponse", {
      "renderDecisions": true,
      "responseHeaders": {
         "cache-control": "no-cache, no-store, max-age=0, no-transform, private",
         "connection": "close",
         "content-encoding": "deflate",
         "content-type": "application/json;charset=utf-8",
         "date": "Mon, 11 Jul 2022 19:42:01 GMT",
         "server": "jag",
         "strict-transport-security": "max-age=31536000; includeSubDomains",
         "transfer-encoding": "chunked",
         "vary": "Origin",
         "x-adobe-edge": "OR2;9",
         "x-content-type-options": "nosniff",
         "x-konductor": "22.6.78-BLACKOUTSERVERDOMAINS:7fa23f82",
         "x-rate-limit-remaining": "599",
         "x-request-id": "5c539bd0-33bf-43b6-a054-2924ac58038b",
         "x-xss-protection": "1; mode=block"
      },
      "responseBody": {
         "requestId": "5c539bd0-33bf-43b6-a054-2924ac58038b",
         "handle": [
         {
            "payload": [
               {
               "id": "XXX",
               "namespace": {
                  "code": "ECID"
               }
               }
            ],
            "type": "identity:result"
         },
         {
            "payload": [
               {...}, 
               {...}
            ],
            "type": "personalization:decisions",
            "eventIndex": 0
         }
         ]
      }
   }
   ).then(applyPersonalization("sample-json-offer"));
```

Formularbasierte [!DNL JSON]-Angebote werden manuell über die Methode `applyPersonalization` angewendet, um die [!DNL DOM] basierend auf dem Personalisierungsangebot zu aktualisieren. Bei formularbasierten Aktivitäten müssen Anzeigeereignisse manuell gesendet werden, um anzugeben, wann das Angebot angezeigt wurde. Dies geschieht über den Befehl `sendEvent`.

```js
function sendDisplayEvent(decision) {
    const { id, scope, scopeDetails = {} } = decision;

    alloy("sendEvent", {
        xdm: {
            eventType: "decisioning.propositionDisplay",
            _experience: {
                decisioning: {
                    propositions: [
                        {
                            id: id,
                            scope: scope,
                            scopeDetails: scopeDetails,
                        },
                    ],
                },
            },
        },
    });
}
```

## Beispielanwendung {#sample-app}

Um Ihnen beim Experimentieren zu helfen und damit Sie mehr über diese Personalisierungsart erfahren können, stellen wir eine Beispielanwendung bereit, die Sie herunterladen und zum Testen verwenden können. Sie können die Anwendung zusammen mit detaillierten Anweisungen zu ihrer Verwendung von diesem [GitHub-Repository](https://github.com/adobe/alloy-samples) herunterladen.
