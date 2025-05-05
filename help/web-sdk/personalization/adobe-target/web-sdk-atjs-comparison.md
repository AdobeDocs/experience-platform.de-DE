---
title: Vergleich von at.js mit der Experience Platform Web SDK
description: Vergleich der at.js-Funktionen mit Experience Platform Web SDK
keywords: target;adobe target;activity.id;experience.id;renderDecisions;Entscheidungsumfänge;Snippet vorab ausblenden;VEC;Form-Based Experience Composer;xdm;Zielgruppen;Entscheidungen;Umfang;Schema;Systemdiagramm;Diagramm
exl-id: b63fe47d-856a-4cae-9057-51917b3e58dd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2183'
ht-degree: 4%

---

# Vergleich der at.js-Bibliothek mit dem Web SDK

## Überblick

Dieser Artikel bietet einen Überblick über die Unterschiede zwischen der `at.js`-Bibliothek und der Experience Platform Web SDK.

## Installieren der Bibliotheken

### Installieren von at.js

Unsere Kunden können die Bibliothek direkt von der Registerkarte Implementierung in Adobe Experience Cloud herunterladen. Die at.js-Bibliothek wird mit Einstellungen angepasst, die der Kunde hat: clientCode, imsOrgId usw.

### Installieren von Web SDK

Die vordefinierte Version ist in einem CDN verfügbar. Sie können direkt auf Ihrer Seite auf die Bibliothek im CDN verweisen oder sie herunterladen und in Ihrer eigenen Infrastruktur hosten. Es ist in minimierten und nicht minimierten Formaten verfügbar. Die nicht minimierte Version ist zum Debuggen hilfreich.

Weitere [ finden Sie unter „Installieren von Web SDK mithilfe ](/help/web-sdk/install/library.md) JavaScript-Bibliothek“.

## Konfigurieren der Bibliotheken

### Konfigurieren von at.js

Am Ende jeder at.js-Datei finden Sie einen Abschnitt, in dem wir ein Einstellungsobjekt instanziieren und übergeben. Es ist anpassbar, beim Herunterladen füllen wir diesen Abschnitt mit aktuellen Kundeneinstellungen.

```javascript
window.adobe.target.init(window, document, {
  "clientCode": "demo",
  "imsOrgId": "",
  "serverDomain": "localhost:5000",
  "timeout": 2000,
  "globalMboxName": "target-global-mbox",
  "version": "2.0.0",
  "defaultContentHiddenStyle": "visibility: hidden;",
  "defaultContentVisibleStyle": "visibility: visible;",
  "bodyHiddenStyle": "body {opacity: 0 !important}",
  "bodyHidingEnabled": true,
  "deviceIdLifetime": 63244800000,
  "sessionIdLifetime": 1860000,
  "selectorsPollingTimeout": 5000,
  "visitorApiTimeout": 2000,
  "overrideMboxEdgeServer": false,
  "overrideMboxEdgeServerTimeout": 1860000,
  "optoutEnabled": false,
  "optinEnabled": false,
  "secureOnly": false,
  "supplementalDataIdParamTimeout": 30,
  "authoringScriptUrl": "//cdn.tt.omtrdc.net/cdn/target-vec.js",
  "urlSizeLimit": 2048,
  "endpoint": "/rest/v1/delivery",
  "pageLoadEnabled": true,
  "viewsEnabled": true,
  "analyticsLogging": "server_side",
  "serverState": {},
  "decisioningMethod": "server-side",
  "legacyBrowserSupport":  false
});
```

[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html?lang=de)


### Konfigurieren der Web-SDK

Die Konfiguration für die SDK erfolgt mit dem Befehl [`configure`](/help/web-sdk/commands/configure/overview.md) . Der `configure` Befehl wird *immer* zuerst aufgerufen.

## Anfordern und automatisches Rendern von Seitenladeangeboten für Target

### Verwenden von at.js

Wenn Sie at.js 2.x verwenden und die Einstellung `pageLoadEnabled` aktivieren, führt die -Bibliothek einen Trigger zu Target Edge mit `execute -> pageLoad` durch. Wenn für alle Einstellungen die Standardwerte festgelegt sind, ist keine benutzerdefinierte Codierung erforderlich. Sobald at.js zur Seite hinzugefügt und vom Browser geladen wird, wird ein Target Edge-Aufruf ausgeführt.

### Verwenden von Web SDK

Inhalte, die in Adobe Target [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=de) erstellt wurden, können von SDK automatisch abgerufen und gerendert werden.

Um Target-Angebote anzufordern und automatisch zu rendern, verwenden Sie den Befehl `sendEvent` und setzen die Option `renderDecisions` auf `true`. Dadurch wird SDK gezwungen, automatisch alle personalisierten Inhalte zu rendern, die für das automatische Rendering geeignet sind.

Beispiel:

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

Experience Platform Web SDK sendet automatisch eine Benachrichtigung mit den Angeboten, die von WEB SDK ausgeführt wurden. Dies ist ein Beispiel dafür, wie die Payload einer Benachrichtigungsanfrage aussieht:

```json
{
  "events": [{
      "xdm": {
        "_experience": {
          "decisioning": {
            "propositions": [
              {
                "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
                "scope": "cart",
                "scopeDetails": {
                  "decisionProvider": "TGT",
                  "activity": {
                    "id": "127019"
                  },
                  "experience": {
                    "id": "0"
                  },
                  "strategies": [
                    {
                      "step": "entry",
                      "algorithmID": "0",
                      "trafficType": "0"
                    },
                    {
                      "step": "display",
                      "algorithmID": "0",
                      "trafficType": "0"
                    }
                  ],
                  "characteristics": {
                    "eventToken": "bKMxJ8dCR1XlPfDCx+2vSGqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="
                  }
                }
              }
            ]
          }
        },
        "eventType": "display",
        "web": {
          "webPageDetails": {
            "viewName": "cart",
            "URL": "https://alloyio.com/personalizationSpa/cart"
          },
          "webReferrer": {
            "URL": ""
          }
        },
        "device": {
          "screenHeight": 800,
          "screenWidth": 1280,
          "screenOrientation": "landscape"
        },
        "environment": {
          "type": "browser",
          "browserDetails": {
            "viewportWidth": 1280,
            "viewportHeight": 284
          }
        },
        "placeContext": {
          "localTime": "2021-12-10T15:50:34.467+02:00",
          "localTimezoneOffset": -120
        },
        "timestamp": "2021-12-10T13:50:34.467Z",
        "implementationDetails": {
          "name": "https://ns.adobe.com/experience/alloy",
          "version": "2.6.2",
          "environment": "browser"
        }
      }
    }
  ]
}
```

[Weitere Informationen](../rendering-personalization-content.md)

## Anfordern und NICHT automatisches Rendern von Seitenladeangeboten durch Target

### Verwenden von at.js

Es gibt zwei Möglichkeiten, einen Aufruf an Target Edge auszulösen, mit dem Angebote zum Laden der Seite abgerufen werden.

Beispiel 1:

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox", 
   success: console.log,
   error: console.error
});
```

Beispiel 2:

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {}
    }
  }
})
.then(console.log)
.catch(console.error);
```

[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/cmp-atjs-functions.html?lang=de)

### Verwenden von Web SDK

Führen Sie einen `sendEvent` Befehl mit einem speziellen Bereich unter `decisionScopes` aus: `__view__`. Wir verwenden diesen Umfang als Signal, um alle Seitenladeaktivitäten aus Target abzurufen und alle Ansichten vorab abzurufen. Web SDK versucht auch, alle ansichtsbasierten Aktivitäten des VEC auszuwerten. Das Deaktivieren des Vorabrufs von Ansichten wird derzeit in der Web-SDK nicht unterstützt.

Für den Zugriff auf Personalisierungsinhalte können Sie eine Rückruffunktion bereitstellen, die aufgerufen wird, nachdem die SDK eine erfolgreiche Antwort vom Server erhalten hat. Ihr Callback wird als Ergebnisobjekt bereitgestellt, das die Eigenschaft „Vorschläge“ enthalten kann, die alle zurückgegebenen Personalisierungsinhalte enthält.

Beispiel:

```javascript
alloy("sendEvent", {
    xdm: {...},
    decisionScopes: ["__view__"]
  }).then(function(result) {
    if (result.propositions) {
      result.propositions.forEach(proposition => {
        proposition.items.forEach(item => {
          if (item.schema === HTML_SCHEMA) {
            // manually apply offer
            document.getElementById("form-based-offer-container").innerHTML =
              item.data.content;
            const executedPropositions = [
              {
                id: proposition.id,
                scope: proposition.scope,
                scopeDetails: proposition.scopeDetails
              }
            ];
          // manually send the display notification event, so that Target/Analytics impressions aare increased
            alloy("sendEvent",{
              "xdm": {
                "eventType": "decisioning.propositionDisplay",
                "_experience": {
                  "decisioning": {
                    "propositions": executedPropositions
                  }
                }
              }
            });
          }
        });
      });
    }
  });
```

[Weitere Informationen](../rendering-personalization-content.md#manually-rendering-content)


## Anfordern bestimmter formularbasierter Target-Mboxes


### Verwenden von at.js

Sie können Aktivitäten von Form Based Composer mit der Funktion `getOffer` abrufen:

Beispiel 1:

```javascript
adobe.target.getOffer({
   mbox: "hero-banner", 
   success: console.log,
   error: console.error
});
```

Beispiel 2:

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        mboxes: [
        {
          index: 0,
          name: "hero-banner"
        }]
    }
  }
})
.then(console.log)
.catch(console.error);
```

[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/cmp-atjs-functions.html?lang=de)


### Verwenden von Web SDK

Sie können formularbasierte Composer-basierte Aktivitäten abrufen, indem Sie den Befehl `sendEvent` verwenden und die Mbox-Namen unter der Option `decisionScopes` übergeben. Der Befehl `sendEvent` gibt eine Zusage zurück, die mit einem Objekt aufgelöst wird, das die angeforderten Aktivitäten/Vorschläge enthält:
So sieht das `propositions`-Array aus:

```javascript
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "hero-banner",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "experience": {
        "id": "0"
      },
      "strategies": [
        {
          "algorithmID": "0",
          "trafficType": "0"
        }
      ],
      "characteristics": {
        "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw=="
      }
    },
    "items": [
      {
        "id": "1184844",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434689",
          "experience.id": "0",
          "activity.name": "a4t test form based activity",
          "offer.id": "1184844",
          "profile.tntId": "04608610399599289452943468926942466370-pybgfJ"
        },
        "data": {
          "id": "1184844",
          "format": "text/html",
          "content": "<div> analytics impressions </div>"
        }
      }
    ]
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "hero-banner",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "characteristics": {
        "eventToken": "E0gb6q1+WyFW3FMbbQJmrg=="
      }
    },
    "items": [
      {
        "id": "434689",
        "schema": "https://ns.adobe.com/personalization/measurement",
        "data": {
          "type": "click",
          "format": "application/vnd.adobe.target.metric"
        }
      }
    ]
  }
]
```

Beispiel:

```javascript
alloy("sendEvent", {
  xdm: { ...},
  decisionScopes: ["hero-banner"]
}).then(function (result) {
  var propositions = result.propositions;

  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      for (var j = 0; j < proposition.items; j++) {
        var item = proposition.items[j];
        if (item.schema === HTML_SCHEMA) {
          // apply offer
          document.getElementById("form-based-offer-container").innerHTML =
            item.data.content;
          const executedPropositions = [
            {
              id: proposition.id,
              scope: proposition.scope,
              scopeDetails: proposition.scopeDetails
            }
          ];

          alloy("sendEvent", {
            "xdm": {
              "eventType": "decisioning.propositionDisplay",
              "_experience": {
                "decisioning": {
                  "propositions": executedPropositions
                }
              }
            }
          });
        }
      }
    }
  }
});
```

[Weitere Informationen](../rendering-personalization-content.md#manually-rendering-content)

## Anwenden der Target-Aktivitäten

### Verwenden von at.js

Sie können die Target-Aktivitäten mithilfe der `applyOffers` anwenden: `adobe.target.applyOffer(options)`

Beispiel:

```javascript
adobe.target.getOffers({...})
  .then(response => adobe.target.applyOffers({ response: response }))
  .then(() => console.log("Success"))
  .catch(error => console.log("Error", error));
```

Weitere Informationen über den `applyOffers`-Befehl finden Sie in der [dedizierten Dokumentation](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-applyoffers-atjs-2.html?lang=de).


### Verwenden von Web SDK

Sie können die Target-Aktivitäten mit dem Befehl `applyPropositions` anwenden.

Beispiel:

```javascript
alloy("applyPropositions", {
    propositions: [...]
});
```

Weitere Informationen über den `applyPropositions`-Befehl finden Sie in der [dedizierten Dokumentation](../../personalization/rendering-personalization-content.md#applypropositions).

## Tracking von Ereignissen

### Verwenden von at.js

Sie können Ereignisse mithilfe der `trackEvent`-Funktion oder mithilfe von `sendNotifications` verfolgen.

Diese Funktion löst eine Anfrage aus, um Benutzeraktionen wie Klicks und Konversionen zu melden. In der Antwort werden keine Aktivitäten bereitgestellt.


**Beispiel 1**

```javascript
adobe.target.trackEvent({ 
    "type": "click",
    "mbox": "some-mbox"
});
```

**Beispiel 2**

```javascript
adobe.target.sendNotifications({ 
    request: {
       notifications: [{
          ...,
          mbox: {
            name: "some-mbox"
          },
          type: "click",
          ...
       }]
    }
});
```

[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-trackevent.html?lang=de)

### Verwenden von Web SDK

Sie können Ereignisse und Benutzeraktionen verfolgen, indem Sie den Befehl `sendEvent` aufrufen, die Feldergruppe `_experience.decisioning.propositions` XDM ausfüllen und den `eventType` auf einen von zwei Werten setzen:

* `decisioning.propositionDisplay`: Signalisiert das Rendering der Target-Aktivität.
* `decisioning.propositionInteract`: Signalisiert eine Benutzerinteraktion mit der Aktivität wie ein Mausklick.

Die `_experience.decisioning.propositions` XDM-Feldergruppe ist ein Array von -Objekten. Die Eigenschaften der einzelnen -Objekte werden von dem `result.propositions` abgeleitet, der im `sendEvent`-Befehl zurückgegeben wird: `{ id, scope, scopeDetails }`

**Beispiel 1: Verfolgen eines `decisioning.propositionDisplay` Ereignisses nach dem Rendern einer Aktivität**

```javascript
alloy("sendEvent", {
  xdm: {},
  decisionScopes: ['discount']
}).then(function(result) {
  var propositions = result.propositions;

  var discountProposition;
  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      if (proposition.scope === "discount") {
        discountProposition = proposition;
        break;
      }
    }
  }

  if (discountProposition) {
    // Find the item from proposition that should be rendered.
    // Rather than assuming there a single item that has HTML
    // content, find the first item whose schema indicates
    // it contains HTML content.
    for (var j = 0; j < discountProposition.items.length; j++) {
      var discountPropositionItem = discountProposition.items[i];
      if (discountPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
        var discountHtml = discountPropositionItem.data.content;
        // Render the content
        var dailySpecialElement = document.getElementById("daily-special");
        dailySpecialElement.innerHTML = discountHtml;
        
        // For this example, we assume there is only a single place to update in the HTML.
        break;  
      }
    }
    // Send a "decisioning.propositionDisplay" event signaling that the proposition has been rendered.
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
});
```

**Beispiel 2: Verfolgen eines `decisioning.propositionInteract` Ereignisses nach einem Klick auf eine Metrik**

```javascript
alloy("sendEvent", {
  xdm: { ...},
  decisionScopes: ["hero-banner"]
}).then(function (result) {
  var propositions = result.propositions;

  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      for (var j = 0; j < proposition.items.length; j++) {
        var item = proposition.items[j];

        if (item.schema === "https://ns.adobe.com/personalization/measurement") {
          // add metric to the DOM element
          const button = document.getElementById("form-based-click-metric");

          button.addEventListener("click", event => {
            const executedPropositions = [
              {
                id: proposition.id,
                scope: proposition.scope,
                scopeDetails: proposition.scopeDetails
              }
            ];
            // send the click track event
            alloy("sendEvent", {
              "xdm": {
                "eventType": "decisioning.propositionInteract",
                "_experience": {
                  "decisioning": {
                    "propositions": executedPropositions
                  }
                }
              }
            });
          });
        }
      }
    }
  }
});
```

[Weitere Informationen](../rendering-personalization-content.md#manually-rendering-content)

**Beispiel 3: Verfolgen eines Ereignisses, das nach einer Aktion ausgelöst wurde**

In diesem Beispiel wird ein Ereignis nachverfolgt, das nach Durchführung einer bestimmten Aktion, z. B. Klicken auf eine Schaltfläche, ausgelöst wurde.
Sie können über das `__adobe.target` Datenobjekt beliebige weitere benutzerdefinierte Parameter hinzufügen.

Sie können auch das `commerce` XDM-Objekt hinzufügen.

```js
alloy("sendEvent", {
    "xdm": {
        "_experience": {
            "decisioning": {
                "propositions": [
                    {
                        "scope": "orderConfirm" //example scope name
                    }
                ],
                "propositionEventType": {
                    "display": 1
                }
            }
        },
        "eventType": "decisioning.propositionDisplay"
    },
    "commerce": {
        "order": {
            "purchaseID": "a8g784hjq1mnp3",
            "purchaseOrderNumber": "VAU3123",
            "currencyCode": "USD",
            "priceTotal": 999.98
        }
    },
    "data": {
        "__adobe": {
            "target": {
                "pageType": "Order Confirmation",
                "user.categoryId": "Insurance"
            }
        }
    }
})
```

## Trigger einer Ansichtsänderung in einem Einzelseiten-Programm

### Verwenden von at.js

Verwenden Sie die `adobe.target.triggerView`. Diese Funktion kann aufgerufen werden, wenn eine neue Seite geladen wird oder wenn eine Komponente auf einer Seite erneut gerendert wird. Für Single Page Applications (SPAs) sollte adobe.target.triggerView() implementiert werden, damit der Visual Experience Composer (VEC) zum Erstellen von A/B-Tests und Experience Targeting(XT)-Aktivitäten verwendet werden kann. Wenn adobe.target.triggerView() nicht auf der Website implementiert ist, kann der VEC nicht für SPA verwendet werden.

**Beispiel**

```javascript
adobe.target.triggerView("homeView")
```

[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-triggerview-atjs-2.html?lang=de)


### Verwenden von Web SDK

Um eine Änderung der Ansicht einer Einzelseitenanwendung per Trigger oder Signal vorzunehmen, legen Sie die Eigenschaft `web.webPageDetails.viewName` unter der Option `xdm` des Befehls `sendEvent` fest. Web SDK prüft den Ansichtscache, wenn es Angebote für die in `sendEvent` angegebenen `viewName` gibt. Sie werden ausgeführt und senden ein Anzeigebenachrichtigungsereignis.

**Beispiel**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  xdm:{
    web:{
      webPageDetails:{
        viewName: "homeView"
      }
    }
  }
});
```

[Weitere Informationen](./spa-implementation.md#implementing-xdm-views)

## So nutzen Sie Antwort-Token

Von Adobe Target zurückgegebene Personalization-Inhalte enthalten [Antwort-Token](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=de) mit Details zur Aktivität, zum Angebot, zum Erlebnis, zum Benutzerprofil, zu geografischen Informationen und mehr. Diese Details können für Drittanbieter-Tools freigegeben oder zum Debugging verwendet werden. Antwort-Token können in der Benutzeroberfläche von Adobe Target konfiguriert werden.

### Verwenden von at.js

Verwenden Sie benutzerdefinierte at.js-Ereignisse, um auf die Target-Antwort zu warten und die Antwort-Token zu lesen.

**Beispiel**

```javascript
document.addEventListener(adobe.target.event.REQUEST_SUCCEEDED, function(e) { 
  console.log("Request succeeded", e.detail); 
}); 
```

[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=de)


### Verwenden von Web SDK

>[!IMPORTANT]
>
>Stellen Sie sicher, dass Sie Experience Platform Web SDK Version 2.6.0 oder höher verwenden.

Die Antwort-Token werden als Teil der `propositions` zurückgegeben, die im Ergebnis des `sendEvent`-Befehls verfügbar gemacht werden. Jeder Vorschlag enthält ein Array von `items`, und jedes Element verfügt über ein `meta` Objekt, das mit Antwort-Token gefüllt wird, wenn diese in der Admin-Benutzeroberfläche von Target aktiviert sind. [Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=de)

**Beispiel**

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Format of result.propositions:
      /*
        [
            {
                "id": "",
                "scope": "",
                "items": [
                    {
                        "id": "",
                        "schema": "",
                        "data": {},
                        "meta": { // RESPONSE TOKENS
                            "activity.name": ...,
                            "offer.id": ...,
                            "profile.activeActivities": ...
                        }
                    }
                ],
                "scopeDetails": {}
                "renderAttempted": false
            }
        ]
      */
    }
  });
```

[Weitere Informationen](./accessing-response-tokens.md)

## Verwalten von Flackern

### Verwenden von at.js

Mit at.js können Sie ein Flackern verhindern, indem Sie `bodyHidingEnabled: true` so festlegen, dass at.js diejenige ist, um die Sie sich kümmern würden
Vorab-Ausblenden der personalisierten Container, bevor die DOM-Änderungen abgerufen und angewendet werden.
Die Seitenabschnitte, die personalisierte Inhalte enthalten, können vorab ausgeblendet werden, indem die at.js-`bodyHiddenStyle` überschrieben wird.
Standardmäßig blendet `bodyHiddenStyle` die gesamte HTML-`body` aus.
Beide Einstellungen können mit `window.targetGlobalSettings` überschrieben werden. `window.targetGlobalSettings` sollten vor dem Laden von at.js platziert werden.

### Verwenden von Web SDK

Mit Web SDK kann der Kunde seinen Stil zum Vorab-Ausblenden im configure-Befehl festlegen, wie im folgenden Beispiel dargestellt:

```javascript
alloy("configure", {
  datastreamId: "configurationId",
  orgId: "orgId@AdobeOrg",
  debugEnabled: true,
  prehidingStyle: "body { opacity: 0 !important }"
});
```

Beim asynchronen Laden von Web SDK wird empfohlen, das folgende Snippet auf der Seite einzufügen, bevor Web SDK eingefügt wird:

```html
<script>
  !function(e,a,n,t){
  if (a) return;
  var i=e.head;if(i){
  var o=e.createElement("style");
  o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),
  setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
  (document, document.location.href.indexOf("adobe_authoring_enabled") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

## Handhabung von A4T

### Verwenden von at.js

Es gibt zwei Arten von A4T-Protokollierung, die mit at.js unterstützt werden:

* Client-seitige Protokollierung in Analytics
* Server-seitige Analytics-Protokollierung

#### Client-seitige Protokollierung in Analytics

**Beispiel 1: Verwenden der globalen Zielgruppeneinstellung**

Die Client-seitige Protokollierung in Analytics kann aktiviert werden, indem `analyticsLogging: client_side` in den at.js-Einstellungen festgelegt oder das `window.targetglobalSettings`-Objekt überschrieben wird.
Wenn diese Option eingerichtet ist, sieht das Format der zurückgegebenen Payload wie folgt aus:

```json
{
  "analytics": {
    "payload": {
      "pe": "tnt",
      "tnta": "167169:0:0|0|100,167169:0:0|2|100,167169:0:0|1|100"
    }
  }
}
```

Die Payload kann dann über die Data Insertion-API an Analytics weitergeleitet werden.

Beispiel 2: Konfiguration in jeder `getOffers`:

```javascript
adobe.target.getOffers({
      request: {
        experienceCloud: {
          analytics: {
            logging: "client_side"
          }
        },
        prefetch: {
          mboxes: [{
            index: 0,
            name: "a1-serverside-xt"
          }]
        }
      }
    })
    .then(console.log)
```

So sieht die Antwort-Payload aus:

```json
{
  "prefetch": {
    "mboxes": [{
      "index": 0,
      "name": "a1-serverside-xt",
      "options": [{
        "content": "<img src=\"http://s7d2.scene7.com/is/image/TargetAdobeTargetMobile/L4242-xt-usa?tm=1490025518668&fit=constrain&hei=491&wid=980&fmt=png-alpha\"/>",
        "type": "html",
        "eventToken": "n/K05qdH0MxsiyH4gX05/2qipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
        "responseTokens": {
          "profile.memberlevel": "0",
          "geo.city": "bucharest",
          "activity.id": "167169",
          "experience.name": "USA Experience",
          "geo.country": "romania"
        }
      }],
      "analytics": {
        "payload": {
          "pe": "tnt",
          "tnta": "167169:0:0|0|100,167169:0:0|2|100,167169:0:0|1|100"
        }
      }
    }]
  }
}
```

Die Analytics-Payload (`tnta`-Token) sollte mit der Dateneinfüge-[ in den Analytics-Treffer ](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md) werden.

#### Server-seitige Analytics-Protokollierung

Die Server-seitige Protokollierung von Analytics kann aktiviert werden, indem `analyticsLogging: server_side` in den at.js-Einstellungen festgelegt oder das `window.targetglobalSettings`-Objekt überschrieben wird.
Die Daten fließen dann wie folgt:

![Diagramm mit dem Server-seitigen Analytics-Protokollierungs-Workflow](assets/a4t-server-side-atjs.png)

[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html?lang=de)

### Verwenden von Web SDK

Web SDK unterstützt auch:

* Client-seitige Protokollierung in Analytics
* Server-seitige Analytics-Protokollierung

#### Client-seitige Protokollierung in Analytics

Die Client-seitige Protokollierung in Analytics ist aktiviert, wenn Adobe Analytics für diese DataStream-Konfiguration deaktiviert ist.

![Diagramm mit dem Client-seitigen Analytics-Protokollierungs-Workflow](assets/analytics-disabled-datastream-config.png)

Die Kundin bzw. der Kunde hat Zugriff auf das Analytics-Token (`tnta`), das über die (Data Insertion [) API für Analytics freigegeben werden ](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md)
in durch Verketten des Befehls `sendEvent` und Iteration durch das resultierende Vorschläge-Array.

**Beispiel**

```javascript
alloy("sendEvent", {
    "renderDecisions": true,
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function (results) {
  var analyticsPayloads = new Set();
  for (var i = 0; i < results.propositions.length; i++) {
    var proposition = results.propositions[i];
    var renderAttempted = proposition.renderAttempted;

    if (renderAttempted === true) {
      var analyticsPayload = getAnalyticsPayload(proposition);
      if (analyticsPayload !== undefined) {
        analyticsPayloads.add(analyticsPayload);
      }
    }
  }
  var analyticsPayloadsToken = concatenateAnalyticsPayloads(analyticsPayloads);
  // send the page view Analytics hit with collected Analytics payload using Data Insertion API
});
```

Im Folgenden finden Sie ein Diagramm, das den Datenfluss zeigt, wenn die Client-Seite von Analytics aktiviert ist:

![Datenflussdiagramm in Client-seitiger Analytics-Protokollierung](assets/analytics-client-side-logging.png)

#### Server-seitige Analytics-Protokollierung

Die Server-seitige Protokollierung von Analytics ist aktiviert, wenn Analytics für diese DataStream-Konfiguration aktiviert ist.

![Datenströme -Benutzeroberfläche mit den Analytics-Einstellungen.](assets/analytics-enabled-datastream-config.png)

Wenn die Server-seitige Analytics-Protokollierung aktiviert ist, muss die A4T-Payload für Analytics freigegeben werden, damit die Analytics-Berichte angezeigt werden
Die richtigen Impressionen und Konversionen werden auf Edge Network-Ebene freigegeben, sodass der Kunde keine zusätzliche Verarbeitung durchführen muss.

So fließen Daten in unsere Systeme, wenn die Server-seitige Analytics-Protokollierung aktiviert ist:

![Diagramm mit dem Datenfluss in der Server-seitigen Analytics-Protokollierung](assets/analytics-server-side-logging.png)

## So legen Sie globale Target-Einstellungen fest

### Verwenden von at.js

Sie können Einstellungen in der at.js-Bibliothek mithilfe von `window.targetGlobalSettings` überschreiben, anstatt die Einstellungen in der Benutzeroberfläche von Target Standard/Premium oder durch Verwendung von REST-APIs zu konfigurieren.

Die Überschreibung sollte definiert werden, bevor at.js geladen wird, oder alternativ unter Administration > Implementierung > at.js-Einstellungen bearbeiten > Code-Einstellungen > Bibliothekskopfzeile.

Beispiel:

```javascript
window.targetGlobalSettings = {  
   timeout: 200, // using custom timeout  
   visitorApiTimeout: 500, // using custom API timeout  
   enabled: document.location.href.indexOf('https://www.adobe.com') >= 0 // enabled ONLY on adobe.com  
};
```

[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html?lang=de)

### Verwenden von Web SDK

Diese Funktion wird in Web SDK nicht unterstützt.

## Aktualisieren von Target-Profilattributen

### Verwenden von at.js

**Beispiel 1**

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox",
   params: {
     "profile.name": "test",
     "profile.gender": "female"
   },
   success: console.log,
   error: console.error
});
```

**Beispiel 2**

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {
          profileParameters: {
            name: "test",
            gender: "female"
          }
        }
    }
  }
})
.then(console.log)
.catch(console.error);
```

### Verwenden von Web SDK

Um ein Zielprofil zu aktualisieren, verwenden Sie den Befehl `sendEvent` und legen Sie die Eigenschaft `data.__adobe.target` fest, wobei den Schlüsselnamen `profile` vorangestellt wird.

**Beispiel**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
});
```

## Verwenden von Target Recommendations

### Verwenden von at.js

**Beispiel 1**

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox",
   params: {
     "entity.name": "T-shirt",
     "entity.id": "1234"
   },
   success: console.log,
   error: console.error
});
```

**Beispiel 2**

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {
          parameters: {
            "entity.name": "T-shirt",
            "entity.id": "1234"
          }
        }
    }
  }
})
.then(console.log)
.catch(console.error);
```

[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-getoffers-atjs-2.html?lang=de)


### Verwenden von Web SDK

Um Empfehlungsdaten zu senden, verwenden Sie den `sendEvent`-Befehl und legen Sie die `data.__adobe.target`-Eigenschaft fest, wobei die Schlüsselnamen mit einem Präfix versehen werden`entity`.

**Beispiel**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "entity.name": "T-shirt",
        "entity.id": "1234"
      }
    }
  }
});
```

## Wie verwende ich Drittanbieter-IDs?

### Verwenden von at.js

Bei der Verwendung von at.js gibt es mehrere Möglichkeiten, `mbox3rdPartyId` mithilfe von `getOffer` oder `getOffers` zu senden:

**Beispiel 1**

```javascript
adobe.target.getOffer({
  mbox:"test",
  params:{
    "mbox3rdPartyId": "1234"
  },
  success: console.log,
  error: console.error
});
```

**Beispiel 2**

```javascript
adobe.target.getOffers({
    request: {
      id:{
        thirdPartyId: "1234"
      },
      execute: {
        pageLoad: {}
    }
  }
})
.then(console.log)
.catch(console.error);
```

Oder es gibt eine Möglichkeit, die `mbox3rdPartyId` entweder in `targetPageParams` oder `targetPageParamsAll` einzurichten.
Wenn Sie sie in `targetPageParams` festlegen, wird sie in den Anfragen für `target-global-mbox` gesendet, die auch als `pag-lLoad` bezeichnet werden.
Die Empfehlung muss mit `targetPageParamsAll` festgelegt werden, da sie in jeder Target-Anfrage gesendet wird.
Der Vorteil der Verwendung von `targetPageParamsAll` besteht darin, dass Sie die `mbox3rdPartyId` auf der Seite einmal definieren können, wodurch sichergestellt wird, dass alle Target-Anfragen die richtigen `mbox3rdPartyId` haben.

```javascript
window.targetPageParamsAll = function() {
      return {
        "mbox3rdPartyId": "1234"
      };
    };
```

```javascript
window.targetPageParams = function() {
  return {
    "mbox3rdPartyId": "1234"
  };
};
```

[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetpageparams.html?lang=de)

### Verwenden von Web SDK

Web SDK unterstützt Target-Drittanbieter-IDs. Es sind jedoch einige weitere Schritte erforderlich. Bevor wir uns mit der Lösung befassen, sollten wir ein wenig über `identityMap` sprechen.
Mit Identity Map können Kundinnen und Kunden mehrere Identitäten senden. Alle Identitäten haben einen Namespace. Jeder Namespace kann eine oder mehrere Identitäten aufweisen. Eine bestimmte Identität kann als primär markiert werden.
Mit diesem Wissen im Hinterkopf können wir sehen, welche Schritte zum Einrichten des Web SDK für die Verwendung der Target-Drittanbieter-ID erforderlich sind.

1. Richten Sie den Namespace ein, der die Target-Third-Party-ID auf der Seite zur Datenstromkonfiguration enthalten soll:

![Datenströme -Benutzeroberfläche mit dem Namespace-Feld für die Target-Drittanbieter-ID](assets/mbox-3-party-id-setup.png)

1. Senden Sie diesen Identity-Namespace in jedem sendEvent-Befehl wie folgt:

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "identityMap": {
      "TGT3PID": [
        {
          "id": "1234",
          "primary": true
        }
      ]
    }
  }
});
```

## Wie werden Eigenschafts-Token festgelegt

### Verwenden von at.js

Bei der Verwendung von at.js gibt es zwei Möglichkeiten, die Eigenschafts-Token einzurichten, entweder mit `targetPageParams` oder `targetPageParamsAll`. Durch Verwendung von `targetPageParams` wird das Eigenschafts-Token zum `target-global-mbox`-Aufruf hinzugefügt, durch Verwendung von `targetPageParamsAll` wird das Token jedoch allen Target-Aufrufen hinzugefügt:

**Beispiel 1**

```javascript
   window.targetPageParamsAll = function() {
      return {
        "at_property": "1234"
      };
    };
```

**Beispiel 2**

```javascript
window.targetPageParams = function() {
      return {
        "at_property": "1234"
      };
    };
```

### Verwenden von Web SDK

Mithilfe von Web SDK können Kundinnen und Kunden die Eigenschaft beim Einrichten der Datenstromkonfiguration unter dem Adobe Target-Namespace auf einer höheren Ebene einrichten:
![Datenströme -Benutzeroberfläche mit den Adobe Target-Einstellungen.](assets/at-property-setup.png)
Das bedeutet, dass jeder Target-Aufruf für diese bestimmte Datenstromkonfiguration dieses Eigenschafts-Token enthält.

## Wie kann ich Mboxes vorab abrufen?

### Verwenden von at.js

Diese Funktion ist nur in at.js 2.x verfügbar. at.js 2.x verfügt über eine neue Funktion namens `getOffers`. `getOffers` ermöglichen es Kunden, Inhalte für eine oder mehrere Mboxes vorab abzurufen. Siehe folgendes Beispiel:

```javascript
adobe.target.getOffers({
    request: {
      prefetch: {
        mboxes: [{
          index: 0,
          name: "test-mbox",
          parameters: {
            ...
          },
          profileParameters: {
            ...
          }
        }]
    }
  }
})
.then(console.log)
.catch(console.error);
```

HINWEIS: Es wird dringend empfohlen sicherzustellen, dass jede `mbox` im `mboxes`-Array einen eigenen Index hat. Normalerweise hat die erste Mbox `index=0`, die nächste `index=1` usw.

### Verwenden von Web SDK

Diese Funktion wird derzeit in Web SDK nicht unterstützt.

## So debugge ich meine Target-Implementierung

### Verwenden von at.js

at.js stellt die folgenden Debugging-Funktionen bereit:

* Mbox deaktivieren - Target vom Abrufen und Rendern deaktivieren, um zu überprüfen, ob die Seite ohne Target-Interaktionen beschädigt ist
* Mbox Debug - at.js protokolliert jede Aktion
* Target Trace : Mit einem im Bullseye generierten Mbox-Trace-Token ist ein Trace-Objekt mit Details, die am Entscheidungsprozess beteiligt waren, unter `window.___target_trace` -Objekt verfügbar

Hinweis: Alle diese Debugging-Funktionen sind mit erweiterten Funktionen in [Adobe Experience Platform Debugger verfügbar](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

### Verwenden von Web SDK

Bei Verwendung von Web SDK stehen mehrere Debugging-Funktionen zur Verfügung:

* Verwenden von [Assurance](/help/assurance/home.md)
* [Web SDK Debug aktiviert](/help/web-sdk/use-cases/debugging.md)
* Verwenden [ Überwachungs-Hooks für Web SDK](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)
* Verwenden Sie [Adobe Experience Platform Debugger](/help/debugger/home.md)
* Zielspur
