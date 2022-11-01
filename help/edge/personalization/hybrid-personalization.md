---
title: Hybride Personalisierung mit Web SDK und Edge Network Server API
description: In diesem Artikel wird gezeigt, wie Sie das Web SDK in Verbindung mit der Server-API verwenden können, um Hybrid-Personalisierung in Ihren Web-Eigenschaften bereitzustellen.
keywords: Personalisierung; Hybrid; Server-API; Server-seitig; Hybridimplementierung;
source-git-commit: f280d4cbcde434ccf36df37e95f1902cfd02c96c
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 3%

---


# Hybride Personalisierung mit Web SDK und Edge Network Server API

## Übersicht {#overview}

Die hybride Personalisierung beschreibt den Prozess des serverseitigen Abrufs von Personalisierungsinhalten mithilfe der [Edge Network Server-API](../..//server-api/overview.md)und Client-seitiges Rendern mithilfe des [Web SDK](../home.md).

Sie können Hybrid-Personalisierung mit Personalisierungslösungen wie Adobe Target oder Offer decisioning verwenden, wobei der Unterschied darin besteht, dass die Inhalte der [!UICONTROL Server-API] Nutzlast.

## Voraussetzungen {#prerequisites}

Bevor Sie eine Hybrid-Personalisierung in Ihre Web-Eigenschaften implementieren, müssen Sie sicherstellen, dass Sie die folgenden Bedingungen erfüllen:

* Sie haben entschieden, welche Personalisierungslösung Sie verwenden möchten. Dies wirkt sich auf den Inhalt der [!UICONTROL Server-API] Nutzlast.
* Sie haben Zugriff auf einen Anwendungsserver, mit dem Sie die [!UICONTROL Server-API] -Aufrufe.
* Sie haben Zugriff auf die [Edge Network Server-API](../../server-api/authentication.md).
* Sie haben richtig [konfiguriert und bereitgestellt](../fundamentals/configuring-the-sdk.md) Web SDK auf den Seiten, die Sie personalisieren möchten.

## Flussdiagramm {#flow-diagram}

Im folgenden Flussdiagramm wird die Reihenfolge der Schritte beschrieben, die zur Bereitstellung der hybriden Personalisierung unternommen werden.

![Visuelles Flussdiagramm, das die Reihenfolge der Schritte anzeigt, die zur Bereitstellung der hybriden Personalisierung unternommen wurden.](assets/hybrid-personalization-diagram.png)

1. Alle vorhandenen Cookies, die zuvor vom Browser gespeichert wurden, mit dem Präfix `kndctr_`, sind in der Browser-Anfrage enthalten.
1. Der Client-Webbrowser fordert die Webseite von Ihrem Anwendungsserver an.
1. Wenn der Anwendungsserver die Seitenanforderung erhält, führt er eine `POST` Anfrage an [Interaktiver Datenerfassungs-Endpunkt der Server-API](../../server-api/interactive-data-collection.md) , um Personalisierungsinhalte abzurufen. Die `POST` -Anfrage enthält eine `event` und `query`. Die Cookies aus dem vorherigen Schritt sind, sofern verfügbar, im `meta>state>entries` Array.
1. Die Server-API gibt den Personalisierungsinhalt an Ihren Anwendungsserver zurück.
1. Der Anwendungsserver gibt eine HTML-Antwort an den Clientbrowser zurück, die die [Identitäts- und Cluster-Cookies](#cookies).
1. Auf der Clientseite wird die [!DNL Web SDK] `applyResponse` aufgerufen wird, wobei die Kopfzeilen und der Hauptteil des [!UICONTROL Server-API] Antwort aus dem vorherigen Schritt.
1. Die [!DNL Web SDK] rendert das Laden der Seite [[!DNL Visual Experience Composer (VEC)]](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=en) automatisch anbietet, da die Variable `renderDecisions` Markierung ist auf `true`.
1. Formularbasiert [!DNL JSON] Angebote manuell über die `applyPersonalization` -Methode, um die [!DNL DOM] basierend auf dem Personalisierungsangebot.
1. Bei formularbasierten Aktivitäten müssen Anzeigeereignisse manuell gesendet werden, um anzugeben, wann das Angebot angezeigt wurde. Dies geschieht über die `sendEvent` Befehl.

## Cookies {#cookies}

Cookies werden verwendet, um die Benutzeridentität und Cluster-Informationen beizubehalten.  Bei Verwendung einer Hybridimplementierung übernimmt der Webanwendungsserver das Speichern und Senden dieser Cookies während des Lebenszyklus der Anfrage.

| Cookie | Zweck | Gespeichert von | Gesendet von |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | Enthält Details zur Benutzeridentität. | Anwendungs-Server | Anwendungs-Server |
| `kndctr_AdobeOrg_cluster` | Gibt an, welcher Edge Network-Cluster zur Erfüllung der Anforderungen verwendet werden soll. | Anwendungs-Server | Anwendungs-Server |

## Anfrageplatzierung {#request-placement}

Server-API-Anfragen sind erforderlich, um Vorschläge abzurufen und eine Benachrichtigung zur Anzeige zu senden. Bei Verwendung einer Hybridimplementierung sendet der Anwendungsserver diese Anfragen an die Server-API.

| Anfrage | Made by |
|---|---|
| Interact-Anfrage zum Abrufen von Vorschlägen | Anwendungs-Server |
| Interact-Anfrage zum Senden von Anzeigebenachrichtigungen | Anwendungs-Server |

## Analytics-Auswirkungen {#analytics}

Bei der Implementierung der hybriden Personalisierung müssen Sie besonders darauf achten, dass Seitentreffer in Analytics nicht mehrmals gezählt werden.

Wenn Sie [Datensatz konfigurieren](../datastreams/overview.md) für Analytics werden Ereignisse automatisch weitergeleitet, sodass Seitentreffer erfasst werden.

Das Beispiel aus dieser Implementierung verwendet zwei verschiedene Datenspeicher:

* Ein für Analytics konfigurierter Datenspeicher. Dieser Datastream wird für Web SDK-Interaktionen verwendet.
* Ein zweiter Datastream ohne Analytics-Konfiguration. Dieser Datastream wird für Server-API-Anfragen verwendet.

Auf diese Weise werden bei der serverseitigen Anforderung keine Analytics-Ereignisse registriert, bei den clientseitigen Anforderungen jedoch schon. Dies führt dazu, dass Analytics-Anforderungen genau gezählt werden.


## Serverseitige Anforderung {#server-side-request}

Die folgende Beispielanfrage zeigt eine Server-API-Anfrage, mit der Ihr Anwendungsserver den Personalisierungsinhalt abrufen kann.

>[!IMPORTANT]
>
>In dieser Beispielanfrage wird Adobe Target als Personalisierungslösung verwendet. Ihre Anforderung kann je nach ausgewählter Personalisierungslösung variieren.


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
| `dataStreamId` | `String` | Ja. | Die ID des Datastreams, mit dem Sie die Interaktionen an das Edge-Netzwerk übergeben. Siehe [Übersicht über Datastreams](../datastreams/overview.md) , um zu erfahren, wie Sie einen Datastream konfigurieren. |
| `requestId` | `String` | Nein | Eine zufällige ID zum Korrelieren interner Server-Anforderungen. Wenn keines angegeben ist, generiert das Edge-Netzwerk eines und gibt es in der Antwort zurück. |

### Serverseitige Antwort {#server-response}

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

## Clientseitige Anforderung {#client-request}

Auf der Clientseite wird die [!DNL Web SDK] `applyResponse` aufgerufen wird, wobei die Kopfzeilen und der Hauptteil der serverseitigen Antwort übergeben werden.

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

Formularbasiert [!DNL JSON] Angebote manuell über die `applyPersonalization` -Methode, um die [!DNL DOM] basierend auf dem Personalisierungsangebot. Bei formularbasierten Aktivitäten müssen Anzeigeereignisse manuell gesendet werden, um anzugeben, wann das Angebot angezeigt wurde. Dies geschieht über die `sendEvent` Befehl.

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

Um Ihnen beim Experimentieren und Erfahren mehr über diese Personalisierungstypen zu bieten, stellen wir eine Beispielanwendung bereit, die Sie herunterladen und zum Testen verwenden können. Sie können die Anwendung zusammen mit detaillierten Anweisungen zur Verwendung hier herunterladen. [GitHub-Repository](https://github.com/adobe/alloy-samples).






