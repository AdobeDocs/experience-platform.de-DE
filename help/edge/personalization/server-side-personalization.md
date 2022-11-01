---
title: Serverseitige Personalisierung mithilfe der Edge Network Server-API
description: Dieser Artikel zeigt, wie Sie die Edge Network Server-API verwenden können, um eine serverseitige Personalisierung für Ihre Webeigenschaften bereitzustellen.
keywords: Personalisierung; Server-API; Edge-Netzwerk; Server-seitig;
source-git-commit: 3e7084953a5e158059074c857bfce4940a83661b
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 2%

---


# Serverseitige Personalisierung mithilfe der Edge Network Server-API

## Übersicht {#overview}

Die serverseitige Personalisierung umfasst die Verwendung der [Edge Network Server-API](../../server-api/overview.md) , um das Kundenerlebnis in Ihren Web-Eigenschaften zu personalisieren.

In dem in diesem Artikel beschriebenen Beispiel wird der Personalisierungsinhalt mithilfe der Server-API serverseitig abgerufen. Anschließend wird die HTML Server-seitig gerendert, basierend auf dem abgerufenen Personalisierungsinhalt.

Die nachstehende Tabelle zeigt ein Beispiel für personalisierten und nicht personalisierten Inhalt.

| Beispielseite ohne Personalisierung | Beispielseite mit Personalisierung |
|---|---|
| ![Beispiel einer Webseite ohne Personalisierung](assets/plain.png) | ![Beispiel einer Webseite mit Personalisierung](assets/personalized.png) |

## Zu beachten {#considerations}

### Cookies {#cookies}

Cookies werden verwendet, um die Benutzeridentität und Cluster-Informationen beizubehalten.  Bei Verwendung einer serverseitigen Implementierung übernimmt der Anwendungsserver das Speichern und Senden dieser Cookies während des Lebenszyklus der Anfrage.

| Cookie | Zweck | Gespeichert von | Gesendet von |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | Enthält Details zur Benutzeridentität. | Anwendungs-Server | Anwendungs-Server |
| `kndctr_AdobeOrg_cluster` | Gibt an, welcher Edge Network-Cluster zur Erfüllung der Anforderungen verwendet werden soll. | Anwendungs-Server | Anwendungs-Server |

### Anfrageplatzierung {#request-placement}

Personalisierungsanfragen sind erforderlich, um Vorschläge abzurufen und eine Benachrichtigung zur Anzeige zu senden. Bei Verwendung einer serverseitigen Implementierung sendet der Anwendungsserver diese Anfragen an die Edge Network Server-API.

| Anfrage | Made by |
|---|---|
| Interact-Anfrage zum Abrufen von Vorschlägen | Anwendungsserver, der die Edge Network Server-API aufruft. |
| Interact-Anfrage zum Senden von Anzeigebenachrichtigungen | Anwendungsserver, der die Edge Network Server-API aufruft. |

## Beispielanwendung {#sample-app}

Der unten beschriebene Prozess verwendet eine Beispielanwendung, die Sie als Ausgangspunkt zum Experimentieren und Erfahren Sie mehr über diese Art der Personalisierung.

Sie können dieses Beispiel herunterladen und für Ihre eigenen Anforderungen anpassen. Sie können beispielsweise Umgebungsvariablen ändern, sodass die Beispielanwendung Angebote aus Ihrer eigenen Experience Platform abruft.

Öffnen Sie dazu die `.env` -Datei im Stammverzeichnis des Repositorys und ändern Sie die Variablen entsprechend Ihrer Konfiguration. Starten Sie die Beispielanwendung neu und Sie können mit Ihrem eigenen Personalisierungsinhalt experimentieren.

### Ausführen des Musters {#running-sample}

Führen Sie die folgenden Schritte aus, um die Beispielanwendung auszuführen.

1. Klonen [dieses Repository](https://github.com/adobe/alloy-samples) auf Ihren lokalen Computer.
2. Öffnen Sie ein Terminal und navigieren Sie zum `personalization-server-side` Ordner.
3. Ausführen `npm install`.
4. Ausführen `npm start`.
5. Öffnen Sie den Webbrowser und navigieren Sie zu `http://localhost`.

## Prozessübersicht {#process}

In diesem Abschnitt werden die Schritte zum Abrufen des Personalisierungsinhalts beschrieben.

1. [Express](https://expressjs.com/) wird für eine schlanke serverseitige Implementierung verwendet. Dies verarbeitet grundlegende Serveranforderungen und Routing.
2. Der Browser fordert die Webseite an. Alle Cookies, die zuvor vom Browser gespeichert wurden, mit dem Präfix `kndctr_`, sind enthalten.
3. Wenn die Seite vom Anwendungsserver angefordert wird, wird ein Ereignis an die [Endpunkt der interaktiven Datenerfassung](../../../server-api/interactive-data-collection.md) , um Personalisierungsinhalte abzurufen. Die Beispielanwendung verwendet Hilfsmethoden, um das Erstellen und Senden von Anfragen an die API zu vereinfachen (siehe [aepEdgeClient.js](https://github.com/adobe/alloy-samples/blob/main/common/aepEdgeClient.js)). Die `POST` -Anfrage enthält eine `event` und `query`. Die Cookies aus dem vorherigen Schritt sind, sofern verfügbar, im `meta>state>entries` Array.

   ```js
   fetch(
   "https://edge.adobedc.net/ee/v2/interact?dataStreamId=abc&requestId=123",
   {
      headers: {
         accept: "*/*",
         "accept-language": "en-US,en;q=0.9",
         "cache-control": "no-cache",
         "content-type": "text/plain; charset=UTF-8",
         pragma: "no-cache",
         "sec-fetch-dest": "empty",
         "sec-fetch-mode": "cors",
         "sec-fetch-site": "cross-site",
         "sec-gpc": "1",
         "Referrer-Policy": "strict-origin-when-cross-origin",
         Referer: "http://localhost/",
      },
      body: JSON.stringify({
         event: {
         xdm: {
            web: {
               webPageDetails: {
               URL: "http://localhost/",
               },
               webReferrer: {
               URL: "",
               },
            },
            identityMap: {
               FPID: [
               {
                  id: "xyz",
                  authenticatedState: "ambiguous",
                  primary: true,
               },
               ],
            },
            timestamp: "2022-06-23T22:21:00.878Z",
         },
         data: {},
         },
         query: {
         identity: {
            fetch: ["ECID"],
         },
         personalization: {
            schemas: [
               "https://ns.adobe.com/personalization/default-content-item",
               "https://ns.adobe.com/personalization/html-content-item",
               "https://ns.adobe.com/personalization/json-content-item",
               "https://ns.adobe.com/personalization/redirect-item",
               "https://ns.adobe.com/personalization/dom-action",
            ],
            decisionScopes: ["__view__", "sample-json-offer"],
         },
         },
         meta: {
         state: {
            domain: "localhost",
            cookiesEnabled: true,
            entries: [
               {
               "key": "kndctr_XXX_AdobeOrg_identity",
               "value": "abc123"
               },
               {
               "key": "kndctr_XXX_AdobeOrg_cluster",
               "value": "or2"
               }
            ],
         },
         },
      }),
      method: "POST",
   }
   ).then((res) => res.json());
   ```

4. Das Target-Angebot aus der formularbasierten Aktivität wird aus der Antwort gelesen und bei der Erstellung der HTML-Antwort verwendet.
5. Bei formularbasierten Aktivitäten müssen Anzeigeereignisse in der Implementierung manuell gesendet werden, um anzugeben, wann das Angebot angezeigt wurde. In diesem Beispiel wird die Benachrichtigung serverseitig während des Anfragelebenszyklus gesendet.

   ```js
   function sendDisplayEvent(aepEdgeClient, req, propositions, cookieEntries) {
   const address = getAddress(req);
   
   aepEdgeClient.interact(
      {
         event: {
         xdm: {
            web: {
               webPageDetails: { URL: address },
               webReferrer: { URL: "" },
            },
            timestamp: new Date().toISOString(),
            eventType: "decisioning.propositionDisplay",
            _experience: {
               decisioning: {
               propositions: propositions.map((proposition) => {
                  const { id, scope, scopeDetails } = proposition;
   
                  return {
                     id,
                     scope,
                     scopeDetails,
                  };
               }),
               },
            },
         },
         },
         query: { identity: { fetch: ["ECID"] } },
         meta: {
         state: {
            domain: "",
            cookiesEnabled: true,
            entries: [...cookieEntries],
         },
         },
      },
      {
         Referer: address,
      }
   );
   }
   ```

6. [!DNL Visual Experience Composer (VEC)] Angebote werden ignoriert, da sie nur über das Web SDK gerendert werden können.
7. Wenn die HTML-Antwort zurückgegeben wird, werden die Identitäts- und Cluster-Cookies in der Antwort vom Anwendungsserver gesetzt.