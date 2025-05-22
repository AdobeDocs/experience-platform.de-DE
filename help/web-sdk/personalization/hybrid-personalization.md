---
title: Hybride Personalisierung mit Web SDK und Edge Network API
description: In diesem Artikel wird gezeigt, wie Sie die Web-SDK zusammen mit der Edge Network-API verwenden können, um hybride Personalisierung in Ihren Web-Eigenschaften bereitzustellen.
keywords: Personalisierung;hybride;Server-API;Server-seitig;Hybridimplementierung;
exl-id: 506991e8-701c-49b8-9d9d-265415779876
source-git-commit: 7b91f4f486db67d4673877477a6be8287693533a
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 41%

---

# Hybride Personalisierung mit Web SDK und Edge Network API

## Überblick {#overview}

Die hybride Personalisierung beschreibt den Prozess des Server-seitigen Abrufens von Personalisierungsinhalten mithilfe der [Edge Network-API](https://developer.adobe.com/data-collection-apis/docs/api/) und des Client-seitigen Renderns mithilfe der [Web-SDK](../home.md).

Sie können hybride Personalisierung mit Personalisierungslösungen wie Adobe Target, Adobe Journey Optimizer oder Offer Decisioning verwenden, wobei der Unterschied in den Payload-Inhalten der [!UICONTROL Edge Network-API] besteht.

## Voraussetzungen {#prerequisites}

Bevor Sie hybride Personalisierung in Ihre Web-Eigenschaften implementieren, müssen Sie sicherstellen, dass Sie die folgenden Bedingungen erfüllen:

* Sie haben entschieden, welche Personalisierungslösung Sie verwenden möchten. Dies wirkt sich auf die Payload-Inhalte der [!UICONTROL Edge Network-API] aus.
* Sie haben Zugriff auf einen Anwendungsserver, mit dem Sie die Aufrufe der [!UICONTROL Edge Network-API] durchführen können.
* Sie haben Zugriff auf die [Edge Network-API](https://developer.adobe.com/data-collection-apis/docs/api/).
* Sie haben [ Web SDK korrekt ](/help/web-sdk/commands/configure/overview.md)konfiguriert) und auf den Seiten bereitgestellt, die Sie personalisieren möchten.

## Flussdiagramm {#flow-diagram}

Im folgenden Flussdiagramm wird die Reihenfolge der Schritte beschrieben, die zur Bereitstellung der hybriden Personalisierung unternommen werden.

![Visuelles Flussdiagramm, das die Reihenfolge der Schritte anzeigt, die zur Bereitstellung der hybriden Personalisierung unternommen werden.](assets/hybrid-personalization-diagram.png)

1. Alle vorhandenen Cookies, die zuvor vom Browser gespeichert wurden, sind, mit dem Präfix `kndctr_` versehen, in der Browser-Anfrage enthalten.
1. Der Client-Webbrowser fordert die Webseite von Ihrem Anwendungs-Server an.
1. Wenn der Anwendungs-Server die Seitenanforderung erhält, führt er eine `POST` Anfrage an den interaktiven Datenerfassungsendpunkt der [Edge Network-API durch](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/) um Personalisierungsinhalte abzurufen. Die `POST`-Anfrage enthält ein `event` und eine `query`. Die Cookies aus dem vorherigen Schritt sind, sofern verfügbar, im Array `meta>state>entries` enthalten.
1. Die Edge Network-API gibt den Personalisierungsinhalt an Ihren Anwendungsserver zurück.
1. Der Anwendungs-Server gibt eine HTML-Antwort an den Client-Browser zurück, die die [Identitäts- und Cluster-Cookies](#cookies) enthält.
1. Auf der Client-Seite wird der Befehl [!DNL Web SDK] `applyResponse` aufgerufen, wobei die Kopfzeilen und der Hauptteil der Antwort der [!UICONTROL Edge Network]API aus dem vorherigen Schritt übergeben werden.
1. Die [!DNL Web SDK] rendert Target-[[!DNL Visual Experience Composer (VEC)]](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) und Journey Optimizer-Webkanal-Elemente automatisch, da das `renderDecisions`-Flag auf `true` gesetzt ist.
1. Zielformularbasierte [!DNL HTML]/[!DNL JSON]-Angebote und Journey Optimizer-Code-basierte Erlebnisse werden manuell über die `applyProposition` angewendet, um die [!DNL DOM] basierend auf dem Personalisierungsinhalt im Vorschlag zu aktualisieren.
1. Bei formularbasierten [!DNL HTML]/[!DNL JSON]-Angeboten in Target und Journey Optimizer müssen Anzeigeereignisse manuell gesendet werden, um anzugeben, wann der zurückgegebene Inhalt angezeigt wurde. Dies geschieht über den Befehl `sendEvent`.

## Cookies {#cookies}

Cookies werden verwendet, um die Benutzeridentität und Cluster-Informationen beizubehalten.  Bei Verwendung einer Hybridimplementierung übernimmt der Web-Anwendungs-Server das Speichern und Senden dieser Cookies während des Lebenszyklus der Anfrage.

| Cookie | Zweck | Gespeichert von | Gesendet von |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | Enthält Details zur Benutzeridentität. | Anwendungs-Server | Anwendungs-Server |
| `kndctr_AdobeOrg_cluster` | Gibt an, welcher Edge Network-Cluster zur Erfüllung der Anforderungen verwendet werden soll. | Anwendungs-Server | Anwendungs-Server |

## Platzierung anfordern {#request-placement}

Edge Network-API-Anfragen sind erforderlich, um Vorschläge zu erhalten und eine Anzeigebenachrichtigung zu senden. Bei Verwendung einer Hybridimplementierung sendet der Anwendungs-Server diese Anfragen an die Edge Network-API.

| Anfrage | Gemacht von |
|---|---|
| Interaktionsanfrage zum Abrufen von Vorschlägen | Anwendungs-Server |
| Interaktionsanfrage zum Senden von Anzeigebenachrichtigungen | Anwendungs-Server |


## Einrichten des regionalen Hosts für Edge Network {#regional-host}

Um den regionalen Edge Network-Host einzurichten, lesen Sie zunächst den Standorthinweis aus dem `kndctr_<orgId>_AdobeOrg_cluster`-Cookie, das die folgenden Werte haben kann:

* `va6`
* `or2`
* `irl1`
* `ind1`
* `sgp3`
* `jpn3`
* `aus3`

Beispiel: `kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_cluster: va6`

Der regionale Edge Network-Host verwendet das folgende Format:`<location_hint>.server.adobedc.net` und kann die folgenden Werte haben:

* `va6.server.adobedc.net`
* `or2.server.adobedc.net`
* `irl1.server.adobedc.net`
* `ind1.server.adobedc.net`
* `sgp3.server.adobedc.net`
* `jpn3.server.adobedc.net`
* `aus3.server.adobedc.net`

Durch die Verwendung dieser spezifischen Hosts werden die Anfragen an denselben Edge Network-Speicherort weitergeleitet, den der Benutzer zuvor besucht hat, und das System kann das beste Erlebnis bieten, da die Benutzerdaten dort vorhanden sind.

Wenn kein Standorthinweis (d. h. kein Cookie) vorhanden ist, verwenden Sie den Standard-Host: `server.adobedc.net`.

>[!TIP]
>
>Als Best Practice sollten Sie eine Liste der zulässigen Speicherorte verwenden. Dadurch wird verhindert, dass der Standorthinweis beeinflusst wird, da er über Client-seitige Cookies bereitgestellt wird.

## Analytics-Auswirkungen {#analytics}

Bei der Implementierung der hybriden Personalisierung müssen Sie besonders darauf achten, dass Seitentreffer in Analytics nicht mehrmals gezählt werden.

Wenn Sie für Analytics [einen Datenstrom konfigurieren](../../datastreams/overview.md), werden Ereignisse automatisch weitergeleitet, sodass Seitentreffer erfasst werden.

Das Beispiel aus dieser Implementierung verwendet zwei verschiedene Datenströme:

* Ein für Analytics konfigurierter Datenstrom. Dieser Datenstrom wird für Web SDK-Interaktionen verwendet.
* Ein zweiter Datenstrom ohne eine Analytics-Konfiguration. Dieser Datenstrom wird für Edge Network-API-Anfragen verwendet. Sie müssen diesen Datenstrom mit derselben Zielkonfiguration konfigurieren wie den Datenstrom, den Sie für Analytics konfiguriert haben.

Auf diese Weise werden bei der Server-seitigen Anforderung keine Analytics-Ereignisse registriert, bei den Client-seitigen Anforderungen jedoch schon. Dies führt dazu, dass Analytics-Anforderungen genau gezählt werden.

## Erstellen der Server-seitigen Anfrage {#server-side-request}

Die folgende Beispielanfrage zeigt eine Edge Network-API-Anfrage, mit der Ihr Anwendungsserver den Personalisierungsinhalt abrufen kann.

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
         "entries": [{
           "key": "kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
           "value":"CiY0NzE0NzkwMTUyMzYzMzI4NDAxMjc3NDcwNzA2NTcxMjI3OTI1NVIRCJ_S-uCRMRABGAEqBElSTDHwAZ_S-uCRMQ=="
         }, {
           "key": "kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent",
           "value": "general=in"
         }, {
            "key": "kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_cluster",
            "value": "va6"
         }]
      }
   }
}'
```

| Parameter | Typ | Erforderlich | Beschreibung |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Ja. | Die ID des Datenstroms, mit dem Sie die Interaktionen an das Edge-Netzwerk weitergeben. Siehe [Datenströme – Übersicht](../../datastreams/overview.md), um zu erfahren, wie Sie einen Datenstrom konfigurieren. |
| `requestId` | `String` | Nein | Eine zufällige ID zum Korrelieren interner Server-Anfragen. Wenn keine angegeben ist, generiert das Edge-Netzwerk eine und gibt sie in der Antwort zurück. |

### Proxy-Kopfzeilen {#proxy-headers}

Die folgenden Kopfzeilen sind erforderlich, um die Anfrage korrekt zu verarbeiten.

* `Referer`
* `X-Forwarded-For`
* `X-Forwarded-Proto`
* `X-Forwarded-Host`

Stellen Sie sicher, dass diese korrekt eingestellt sind, sodass sie auf die tatsächlichen Client-Informationen verweisen. Beispielsweise sollte der `X-Forwarded-For`-Header die Client-IP enthalten, damit eine ordnungsgemäße Geolokalisierung stattfindet.

### User-Agent-Header {#user-agent-headers}

Verwenden Sie die folgenden User-Agent-Header, um die Anfrage korrekt zu verarbeiten.

**Standard**

* `User-Agent`

**Niedrige Entropie (obligatorisch):**

* `Sec-CH-UA`
* `Sec-CH-UA-Mobile`
* `Sec-CH-UA-Platform`

**Hohe Entropie (optional):**

* `Sec-CH-UA-Platform-Version`
* `Sec-CH-UA-Arch`
* `Sec-CH-UA-Model`
* `Sec-CH-UA-Bitness`
* `Sec-CH-UA-WoW64`

Die Anfrage muss gesendet werden, wie in der [Edge Network-API-Spezifikation](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/) dargestellt. Siehe die [Personalisierungsdokumentation](https://developer.adobe.com/data-collection-apis/docs/getting-started/personalization/) falls Ihr Anwendungsfall dies erfordert.

### Server-seitige Antwort {#server-response}

Die Edge Network-Antwort enthält `state:store` Anweisungen, die in `Set-Cookie`-Kopfzeilen umgewandelt werden sollten. Sie werden im Browser gespeichert und können von der Web SDK-Implementierung verwendet werden.

Die Cookies sollten in der Domain auf oberster Ebene gesetzt werden, damit sie zusammen mit Anfragen an die -Serverimplementierung sowie an den Client gesendet werden. (Oder zumindest eine von beiden Implementierungen verwendete gemeinsame Subdomain)

Beispiel:

* Server-seitige Aufrufe verwenden `api.example.com`
* Client-seitige Aufrufe verwenden `adobe.example.com`

Cookies sollten auf `.example.com` gesetzt werden, damit sie in beiden Fällen freigegeben werden.

Die Server-seitige Antwort ist in Fragmente namens `Handles` organisiert, die je nach Datenstromkonfiguration generiert werden. Beispielsweise geben Echtzeit-Personalisierungs-Engines `personalization:decisions`-Handles zurück, während die Echtzeit-Aktivierungs-Engine `activation:pull`-Handles erzeugt.

Die folgende Beispielantwort zeigt, wie die Edge Network-API-Antwort aussehen könnte.

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
        "xdm": {
            "eventType": "decisioning.propositionDisplay",
            "_experience": {
                "decisioning": {
                    "propositions": [{
                        "id": id,
                        "scope": scope,
                        "scopeDetails": scopeDetails
                    }],
                    "propositionEventType": {
                        "display": 1
                    }
                }
            }
        }
    });
}
```

## Beispielanwendung {#sample-app}

Um Ihnen beim Experimentieren zu helfen und damit Sie mehr über diese Personalisierungsart erfahren können, stellen wir eine Beispielanwendung bereit, die Sie herunterladen und zum Testen verwenden können. Sie können die Anwendung zusammen mit detaillierten Anweisungen zu ihrer Verwendung von diesem [GitHub-Repository](https://github.com/adobe/alloy-samples) herunterladen.
