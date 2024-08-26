---
title: Vergleich von at.js mit dem Experience Platform Web SDK
description: Erfahren Sie, wie die at.js-Funktionen mit dem Experience Platform Web SDK verglichen werden.
keywords: Target; adobe target; activity.id; experience.id; renderDecisions; DecisionScopes; Vorabausblenden von Snippet; VEC; Form-Based Experience Composer; xdm; Zielgruppen; Entscheidungen; Umfang; Schema; Systemdiagramm; Diagramm
exl-id: b63fe47d-856a-4cae-9057-51917b3e58dd
source-git-commit: 9489b5345c2b13b9d05b26d646aa7f1576840fb8
workflow-type: tm+mt
source-wordcount: '2182'
ht-degree: 4%

---

# Vergleich der at.js-Bibliothek mit dem Web SDK

## Übersicht

Dieser Artikel bietet einen Überblick über die Unterschiede zwischen der `at.js` -Bibliothek und dem Experience Platform Web SDK.

## Installieren der Bibliotheken

### Installieren von at.js

Wir erlauben unseren Kunden, die Bibliothek direkt über die Registerkarte Implementierung von Adobe Experience Cloud herunterzuladen. Die at.js-Bibliothek wird mit Einstellungen wie clientCode, imsOrgId usw. angepasst, die der Kunde verwendet.

### Installieren des Web SDK

Die vordefinierte Version ist in einem CDN verfügbar. Sie können die Bibliothek im CDN direkt auf Ihrer Seite referenzieren oder sie herunterladen und in Ihrer eigenen Infrastruktur hosten. Es ist in minimierten und nicht minimierten Formaten verfügbar. Die nicht minimierte Version ist für Debugging-Zwecke hilfreich.

Weitere Informationen finden Sie unter [Installieren des Web SDK mit der JavaScript-Bibliothek](/help/web-sdk/install/library.md) .

## Bibliotheken konfigurieren

### &quot;at.js&quot;konfigurieren

Am Ende jeder at.js-Datei finden Sie einen Abschnitt, in dem wir ein Einstellungsobjekt instanziieren und übergeben. Es kann angepasst werden. Beim Herunterladen füllen wir diesen Abschnitt mit aktuellen Kundeneinstellungen.

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

[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html)


### Web SDK konfigurieren

Die Konfiguration für das SDK erfolgt mit dem Befehl [`configure`](/help/web-sdk/commands/configure/overview.md) . Der Befehl `configure` ist *always*, der zuerst aufgerufen wird.

## Anfordern und automatischen Rendern von Target-Angeboten für Seitenladevorgänge

### Verwenden von at.js

Wenn Sie at.js 2.x verwenden und die Einstellung &quot;`pageLoadEnabled`&quot;aktivieren, wird ein Aufruf an Target Edge mit &quot;`execute -> pageLoad`&quot;von der Bibliothek Trigger. Wenn alle Einstellungen auf die Standardwerte gesetzt sind, ist keine benutzerdefinierte Codierung erforderlich. Sobald at.js zur Seite hinzugefügt und vom Browser geladen wird, wird ein Target Edge-Aufruf ausgeführt.

### Verwenden des Web SDK

Inhalte, die innerhalb von Adobe Target [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) erstellt wurden, können vom SDK automatisch abgerufen und gerendert werden.

Um Target-Angebote anzufordern und automatisch zu rendern, verwenden Sie den Befehl `sendEvent` und setzen Sie die Option `renderDecisions` auf `true`. Dies zwingt das SDK dazu, personalisierte Inhalte automatisch zu rendern, die für das automatische Rendering geeignet sind.

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

Experience Platform Web SDK sendet automatisch eine Benachrichtigung mit den vom WEB SDK ausgeführten Angeboten. Dies ist ein Beispiel dafür, wie eine Payload einer Benachrichtigungsanfrage aussieht:

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

## Anfordern und NICHT automatisch Rendern von Target-Angeboten für Seitenladevorgänge

### Verwenden von at.js

Es gibt zwei Möglichkeiten, einen Aufruf an Target Edge auszulösen, der Angebote zum Laden der Seite abruft.

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

[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/cmp-atjs-functions.html)

### Verwenden des Web SDK

Führen Sie einen `sendEvent` -Befehl mit einem speziellen Bereich unter `decisionScopes`: `__view__` aus. Dieser Umfang dient als Signal, um alle Seitenladeaktivitäten aus Target abzurufen und alle Ansichten vorab abzurufen. Das Web SDK versucht außerdem, alle ansichtsbasierten VEC-Aktivitäten zu evaluieren. Das Deaktivieren des Vorabrufs von Ansichten wird derzeit im Web SDK nicht unterstützt.

Um auf Personalisierungsinhalte zuzugreifen, können Sie eine Callback-Funktion bereitstellen, die aufgerufen wird, nachdem das SDK eine erfolgreiche Antwort vom Server erhalten hat. Ihr Rückruf wird mit einem Ergebnisobjekt bereitgestellt, das die Eigenschaft propositions enthalten kann, die alle zurückgegebenen Personalisierungsinhalte enthält.

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

Sie können formularbasierte Composer-Aktivitäten mit der Funktion `getOffer` abrufen:

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

[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/cmp-atjs-functions.html)


### Verwenden des Web SDK

Sie können formularbasierte Composer-basierte Aktivitäten abrufen, indem Sie den Befehl `sendEvent` verwenden und die Mbox-Namen unter der Option `decisionScopes` übergeben. Der Befehl `sendEvent` gibt einen Promise zurück, der mit einem Objekt aufgelöst wird, das die angeforderten Aktivitäten/Vorschläge enthält:
So sieht das `propositions` -Array aus:

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

Sie können die Target-Aktivitäten mithilfe der Funktion `applyOffers` anwenden: `adobe.target.applyOffer(options)`

Beispiel:

```javascript
adobe.target.getOffers({...})
  .then(response => adobe.target.applyOffers({ response: response }))
  .then(() => console.log("Success"))
  .catch(error => console.log("Error", error));
```

Weitere Informationen zum Befehl `applyOffers` finden Sie in der [dedizierten Dokumentation](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-applyoffers-atjs-2.html).


### Verwenden des Web SDK

Sie können die Target-Aktivitäten mit dem Befehl `applyPropositions` anwenden.

Beispiel:

```javascript
alloy("applyPropositions", {
    propositions: [...]
});
```

Weitere Informationen zum Befehl `applyPropositions` finden Sie in der [dedizierten Dokumentation](../../personalization/rendering-personalization-content.md#applypropositions).

## Verfolgen von Ereignissen

### Verwenden von at.js

Sie können Ereignisse mit der Funktion `trackEvent` oder mit `sendNotifications` verfolgen.

Diese Funktion löst eine Anforderung zum Reporting von Benutzeraktionen aus, z. B. Klicks und Konversionen. In der Antwort werden keine Aktivitäten bereitgestellt.


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

[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-trackevent.html)

### Verwenden des Web SDK

Sie können Ereignisse und Benutzeraktionen verfolgen, indem Sie den Befehl `sendEvent` aufrufen, die XDM-Feldgruppe mit dem Wert `_experience.decisioning.propositions` ausfüllen und die `eventType` auf einen von 2 Werten festlegen:

* `decisioning.propositionDisplay`: Signalisiert das Rendering der Target-Aktivität.
* `decisioning.propositionInteract`: Signalisiert eine Benutzerinteraktion mit der Aktivität, z. B. einen Mausklick.

Die `_experience.decisioning.propositions` XDM-Feldgruppe ist ein Array von Objekten. Die Eigenschaften der einzelnen Objekte werden aus dem `result.propositions` abgeleitet, der im `sendEvent`-Befehl zurückgegeben wird: `{ id, scope, scopeDetails }`

**Beispiel 1: Verfolgen eines `decisioning.propositionDisplay` -Ereignisses nach dem Rendern einer Aktivität**

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

**Beispiel 2: Verfolgen eines `decisioning.propositionInteract` -Ereignisses, nachdem eine Klickmetrik aufgetreten ist**

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

**Beispiel 3: Tracking eines Ereignisses, das nach Ausführung einer Aktion ausgelöst wurde**

In diesem Beispiel wird ein Ereignis verfolgt, das nach Ausführung einer bestimmten Aktion ausgelöst wurde, z. B. durch Klicken auf eine Schaltfläche.
Sie können zusätzliche benutzerdefinierte Parameter über das Datenobjekt `__adobe.target` hinzufügen.

Sie können auch das XDM-Objekt `commerce` hinzufügen.

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

## Trigger einer Ansichtsänderung in einer Einzelseiten-App

### Verwenden von at.js

Verwenden Sie die Funktion `adobe.target.triggerView` . Diese Funktion kann immer aufgerufen werden, wenn eine neue Seite geladen wird oder wenn eine Komponente auf einer Seite erneut gerendert wird. adobe.target.triggerView() sollte für Einzelseitenanwendungen (SPA) implementiert werden, damit der Visual Experience Composer (VEC) zum Erstellen von A/B-Tests und Erlebnis-Targeting (XT)-Aktivitäten verwendet werden kann. Wenn adobe.target.triggerView() nicht auf der Site implementiert ist, kann VEC nicht für SPA verwendet werden.

**Beispiel**

```javascript
adobe.target.triggerView("homeView")
```

[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-triggerview-atjs-2.html)


### Verwenden des Web SDK

Um eine Änderung der Ansicht einer Einzelseitenanwendung Trigger oder zu signalisieren, legen Sie die Eigenschaft `web.webPageDetails.viewName` unter der Option `xdm` des Befehls `sendEvent` fest. Das Web SDK prüft den Ansichts-Cache. Wenn Angebote für die in `sendEvent` angegebene `viewName` vorhanden sind, werden sie ausgeführt und ein Anzeigebenachrichtigungsereignis gesendet.

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

## Verwenden von Antwort-Token

Personalization-Inhalte, die von Adobe Target zurückgegeben werden, umfassen [Antwort-Token](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html), d. h. Details zu Aktivität, Angebot, Erlebnis, Benutzerprofil, Geo-Informationen und mehr. Diese Details können für Drittanbieter-Tools freigegeben oder zum Debugging verwendet werden. Antwort-Token können in der Benutzeroberfläche von Adobe Target konfiguriert werden.

### Verwenden von at.js

Verwenden Sie benutzerdefinierte at.js-Ereignisse, um auf die Target-Antwort zu warten und die Antwort-Token zu lesen.

**Beispiel**

```javascript
document.addEventListener(adobe.target.event.REQUEST_SUCCEEDED, function(e) { 
  console.log("Request succeeded", e.detail); 
}); 
```

[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)


### Verwenden des Web SDK

>[!IMPORTANT]
>
>Stellen Sie sicher, dass Sie die Platform Web SDK-Version 2.6.0 oder höher verwenden.

Die Antwort-Token werden als Teil der `propositions` zurückgegeben, die im Ergebnis des `sendEvent` -Befehls verfügbar gemacht werden. Jeder Vorschlag enthält ein Array von &quot;`items`&quot;. Jedes Element enthält ein &quot;`meta`&quot;-Objekt, das mit Antwort-Token gefüllt wird, wenn sie in der Target-Administrator-Benutzeroberfläche aktiviert sind. [Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)

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

## Beheben von Flackern

### Verwenden von at.js

Mit at.js können Sie Flackern verhindern, indem Sie `bodyHidingEnabled: true` festlegen, sodass at.js derjenige ist, der sich um die
die personalisierten Container vorab ausblenden, bevor die DOM-Änderungen abgerufen und angewendet werden.
Die Seitenabschnitte, die personalisierte Inhalte enthalten, können durch Überschreiben von at.js `bodyHiddenStyle` vorab ausgeblendet werden.
Standardmäßig blendet `bodyHiddenStyle` die gesamte HTML `body` aus.
Beide Einstellungen können mit `window.targetGlobalSettings` überschrieben werden. `window.targetGlobalSettings` sollte vor dem Laden von at.js platziert werden.

### Verwenden des Web SDK

Mit dem Web SDK kann der Kunde seinen Pre-hiding-Stil im Befehl &quot;configure&quot;einrichten, wie im folgenden Beispiel:

```javascript
alloy("configure", {
  datastreamId: "configurationId",
  orgId: "orgId@AdobeOrg",
  debugEnabled: true,
  prehidingStyle: "body { opacity: 0 !important }"
});
```

Beim asynchronen Laden des Web SDK empfehlen wir, das folgende Snippet in die Seite einzufügen, bevor das Web SDK eingefügt wird:

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

* Clientseitige Protokollierung in Analytics
* Serverseitige Protokollierung in Analytics

#### Clientseitige Protokollierung in Analytics

**Beispiel 1: Verwenden der globalen Target-Einstellung**

Die clientseitige Protokollierung in Analytics kann aktiviert werden, indem in den at.js-Einstellungen `analyticsLogging: client_side` festgelegt oder das `window.targetglobalSettings` -Objekt überschrieben wird.
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

Die Payload kann dann über die Dateneinfüge-API an Analytics weitergeleitet werden.

Beispiel 2: Konfiguration in jeder `getOffers` -Funktion:

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

Die Analytics-Payload (`tnta` Token) sollte mit der [Dateneinfüge-API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md) im Analytics-Treffer enthalten sein.

#### Serverseitige Protokollierung in Analytics

Die serverseitige Protokollierung in Analytics kann durch Festlegen von `analyticsLogging: server_side` in den at.js-Einstellungen oder durch Überschreiben des `window.targetglobalSettings` -Objekts aktiviert werden.
Anschließend werden die Daten wie folgt übertragen:

![Diagramm, das den Workflow für die serverseitige Protokollierung in Analytics anzeigt](assets/a4t-server-side-atjs.png)

[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html)

### Verwenden des Web SDK

Web SDK unterstützt auch:

* Clientseitige Protokollierung in Analytics
* Serverseitige Protokollierung in Analytics

#### Clientseitige Protokollierung in Analytics

Die clientseitige Protokollierung in Analytics ist aktiviert, wenn Adobe Analytics für diese DataStream-Konfiguration deaktiviert ist.

![Diagramm, das den Client-seitigen Protokollierungs-Workflow von Analytics anzeigt](assets/analytics-disabled-datastream-config.png)

Der Kunde hat Zugriff auf das Analytics-Token (`tnta`), das mithilfe der [Dateneinfüge-API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md) für Analytics freigegeben werden muss
in durch Verketten des Befehls `sendEvent` und Iteration durch das resultierende Vorschlagsarray.

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

Im Folgenden finden Sie ein Diagramm, das zeigt, wie Datenflüsse bei der Aktivierung von Analytics Client Side erfolgen:

![Datenflussdiagramm in der clientseitigen Analytics-Protokollierung](assets/analytics-client-side-logging.png)

#### Serverseitige Protokollierung in Analytics

Die serverseitige Protokollierung in Analytics ist aktiviert, wenn Analytics für diese DataStream-Konfiguration aktiviert ist.

![Benutzeroberfläche von Datastreams mit den Analytics-Einstellungen.](assets/analytics-enabled-datastream-config.png)

Wenn die serverseitige Analytics-Protokollierung aktiviert ist, die A4T-Payload, die für Analytics freigegeben werden muss, damit die Analytics-Berichterstellung angezeigt wird
korrekte Impressionen und Konversionen auf der Edge Network-Ebene freigegeben werden, sodass der Kunde keine zusätzliche Verarbeitung durchführen muss.

So fließen Daten in unsere Systeme, wenn die serverseitige Analytics-Protokollierung aktiviert ist:

![Diagramm, das den Datenfluss in der serverseitigen Analytics-Protokollierung anzeigt](assets/analytics-server-side-logging.png)

## Festlegen globaler Target-Einstellungen

### Verwenden von at.js

Sie können Einstellungen in der at.js-Bibliothek mit `window.targetGlobalSettings` überschreiben, anstatt die Einstellungen in der Benutzeroberfläche von Target Standard/Premium oder durch Verwendung von REST-APIs zu konfigurieren.

Die Überschreibung sollte definiert werden, bevor at.js geladen wird, oder in Administration > Implementierung > at.js-Einstellungen bearbeiten > Codeeinstellungen > Bibliothekskopfzeile.

Beispiel:

```javascript
window.targetGlobalSettings = {  
   timeout: 200, // using custom timeout  
   visitorApiTimeout: 500, // using custom API timeout  
   enabled: document.location.href.indexOf('https://www.adobe.com') >= 0 // enabled ONLY on adobe.com  
};
```

[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html)

### Verwenden des Web SDK

Diese Funktion wird im Web SDK nicht unterstützt.

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

### Verwenden des Web SDK

Um ein Target-Profil zu aktualisieren, verwenden Sie den Befehl `sendEvent` und legen Sie die Eigenschaft `data.__adobe.target` fest, wobei den Schlüsselnamen `profile` vorangestellt wird.

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

## Verwendung von Target Recommendations

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

[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-getoffers-atjs-2.html)


### Verwenden des Web SDK

Verwenden Sie zum Senden von Empfehlungsdaten den Befehl `sendEvent` und legen Sie die Eigenschaft `data.__adobe.target` fest, wobei Sie den Schlüsselnamen mit `entity` voranstellen.

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

## Verwendung von Drittanbieter-IDs

### Verwenden von at.js

Bei der Verwendung von at.js gibt es mehrere Möglichkeiten, `mbox3rdPartyId` mit `getOffer` oder `getOffers` zu senden:

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
Wenn Sie es in `targetPageParams` festlegen, wird es in den Anforderungen für `target-global-mbox` gesendet, auch als `pag-lLoad` bezeichnet.
Die Empfehlung muss mit `targetPageParamsAll` eingestellt werden, da sie in jeder Zielanfrage gesendet wird.
Der Vorteil der Verwendung von `targetPageParamsAll` besteht darin, dass Sie die `mbox3rdPartyId` auf der Seite einmalig definieren können. Dadurch wird sichergestellt, dass alle Zielanforderungen den richtigen `mbox3rdPartyId` aufweisen.

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

[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetpageparams.html)

### Verwenden des Web SDK

Das Web SDK unterstützt die Target-Drittanbieter-ID. Es sind jedoch einige weitere Schritte erforderlich. Bevor wir in die Lösung eintauchen, sollten wir ein wenig über `identityMap` sprechen.
Mit Identity Map können Kunden mehrere Identitäten senden. Alle Identitäten sind mit einem Namespace versehen. Jeder Namespace kann eine oder mehrere Identitäten aufweisen. Eine bestimmte Identität kann als primär markiert werden.
Mit diesem Wissen im Hinterkopf können wir sehen, welche Schritte zur Einrichtung des Web SDK zur Verwendung der Target-Drittanbieter-ID erforderlich sind.

1. Richten Sie den Namespace ein, der die Target-Drittanbieter-ID auf der Seite mit der Datastream-Konfiguration enthält:

![Benutzeroberfläche von Datastreams mit dem Namespace-Feld für die Target-Drittanbieter-ID](assets/mbox-3-party-id-setup.png)

1. Senden Sie diesen Identitäts-Namespace in jedem sendEvent-Befehl wie diesem:

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

## Festlegen von Eigenschafts-Token

### Verwenden von at.js

Mit at.js können Sie die Eigenschafts-Token auf zwei Arten einrichten, entweder mit `targetPageParams` oder mit `targetPageParamsAll`. Durch Verwendung von `targetPageParams` wird das Eigenschafts-Token zum `target-global-mbox` -Aufruf hinzugefügt, durch Verwendung von `targetPageParamsAll` wird das Token jedoch zu allen Target-Aufrufen hinzugefügt:

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

### Verwenden des Web SDK

Mit dem Web SDK können Kunden die Eigenschaft bei der Einrichtung der Datastream-Konfiguration auf einer höheren Ebene unter dem Adobe Target-Namespace einrichten:
![Die Benutzeroberfläche &quot;Datastreams&quot;mit den Adobe Target-Einstellungen.](assets/at-property-setup.png)
Das bedeutet, dass jeder Target-Aufruf für diese spezifische Data Stream-Konfiguration dieses Eigenschafts-Token enthält.

## Wie kann ich mboxes vorab abrufen?

### Verwenden von at.js

Diese Funktion ist nur in at.js 2.x verfügbar. at.js 2.x verfügt über eine neue Funktion namens `getOffers`. Mit `getOffers` können Kunden Inhalte für eine oder mehrere Mboxes vorab abrufen. Siehe folgendes Beispiel:

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

HINWEIS: Es wird dringend empfohlen sicherzustellen, dass jede `mbox` im `mboxes` -Array über einen eigenen Index verfügt. Normalerweise hat die erste Mbox `index=0`, die nächste `index=1` usw.

### Verwenden des Web SDK

Diese Funktion wird im Web SDK derzeit nicht unterstützt.

## Debugging der Target-Implementierung

### Verwenden von at.js

at.js stellt die folgenden Debugging-Funktionen bereit:

* Mbox deaktivieren - Deaktivieren Sie Target vom Abrufen und Rendern, um zu überprüfen, ob die Seite ohne Target-Interaktionen fehlerhaft ist.
* Mbox Debug - at.js protokolliert jede Aktion
* Target Trace - mit einem Mbox-Trace-Token, das im Bullseye-Objekt generiert wurde, ist ein Trace-Objekt mit Details, die am Entscheidungsprozess beteiligt waren, unter dem Objekt `window.___target_trace` verfügbar

Hinweis: Alle diese Debugging-Funktionen sind mit erweiterten Funktionen in [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) verfügbar

### Verwenden des Web SDK

Bei Verwendung des Web SDK stehen Ihnen mehrere Debugging-Funktionen zur Verfügung:

* Verwenden von [Assurance](/help/assurance/home.md)
* [Web SDK-Debugging aktiviert](/help/web-sdk/use-cases/debugging.md)
* Verwenden von [Web SDK-Überwachungshooks](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)
* Verwenden Sie [Adobe Experience Platform Debugger](/help/debugger/home.md)
* Target Trace
