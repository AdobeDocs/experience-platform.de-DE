---
title: Rendern von personalisierten Inhalten mit der Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie mit der Adobe Experience Platform Web SDK personalisierte Inhalte rendern können.
keywords: Personalisierung;renderDecisions;sendEvent;decisionScopes;Vorschläge;
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 2%

---

# Rendern von personalisierten Inhalten

Adobe Experience Platform Web SDK unterstützt das Abrufen personalisierter Inhalte aus Adobe-Personalisierungslösungen, einschließlich [Adobe Target](https://business.adobe.com/de/products/target/adobe-target.html), [Offer Decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=de) und [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=de).

Darüber hinaus ermöglicht der Web-SDK die Personalisierung derselben Seite und der nächsten Seite über Adobe Experience Platform-Personalisierungsziele wie [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) und die [benutzerdefinierte Personalisierungsverbindung](../../destinations/catalog/personalization/custom-personalization.md). Informationen zum Konfigurieren von Experience Platform für die Personalisierung der gleichen und der nächsten Seite finden Sie im [Handbuch zu diesem Thema](../../destinations/ui/activate-edge-personalization-destinations.md).

Inhalte, die in Adobe Target [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=de) und der [Web Campaign-Benutzeroberfläche von Adobe Journey Optimizer erstellt ](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html?lang=de), können von SDK automatisch abgerufen und gerendert werden. Inhalte, die in Adobe Target [Form-Based Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=de), Adobe Journey Optimizers [Code-Based Experience Channel](https://experienceleague.adobe.com/de/docs/journey-optimizer/using/code-based-experience/get-started-code-based) oder Offer Decisioning erstellt wurden, können nicht automatisch von SDK gerendert werden. Stattdessen müssen Sie diesen Inhalt mit der SDK anfordern und dann den Inhalt manuell selbst rendern.

## Inhalt automatisch rendern {#automatic}

Beim Senden von Ereignissen an den Server können Sie die Option `renderDecisions` auf `true` setzen. Dadurch wird SDK gezwungen, automatisch alle personalisierten Inhalte zu rendern, die für das automatische Rendering geeignet sind.

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

Das Rendern personalisierter Inhalte ist asynchron, sodass Sie nicht davon ausgehen sollten, wann ein bestimmtes Inhaltselement das Rendering abgeschlossen hat.

## Manuelles Rendern von Inhalt {#manual}

Für den Zugriff auf Personalisierungsinhalte können Sie eine Rückruffunktion bereitstellen, die aufgerufen wird, nachdem die SDK eine erfolgreiche Antwort vom Server erhalten hat. Ihr Callback wird als `result`-Objekt bereitgestellt, das eine `propositions`-Eigenschaft enthalten kann, die alle zurückgegebenen Personalisierungsinhalte enthält. Nachfolgend finden Sie ein Beispiel dafür, wie Sie beim Senden eines Ereignisses eine Rückruffunktion bereitstellen würden.

```javascript
alloy("sendEvent", {
    "xdm": {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

In diesem Beispiel ist `result.propositions`, falls vorhanden, ein Array mit Personalisierungsvorschlägen im Zusammenhang mit dem Ereignis. Standardmäßig enthält sie nur Vorschläge, die für das automatische Rendering geeignet sind.

Das `propositions`-Array kann in etwa wie im folgenden Beispiel aussehen:

```json
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "__view__",
    "items": [
      {
        "id": "11223344",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">An HTML proposition.</h2>",
          "selector": "#hero",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      ...
    },
    "renderAttempted": false
  },
  {
    "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
    "scope": "__view__",
    "items": [
      {
        "id": "11223345",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">Another HTML proposition.</h2>",
          "selector": "#sidebar",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      ...
    },
    "renderAttempted": false
  }
]
```

In diesem Beispiel wurde die `renderDecisions`-Option bei Ausführung des `true`-Befehls nicht auf `sendEvent` gesetzt, weshalb die SDK nicht versuchte, automatisch Inhalte zu rendern. Die SDK hat jedoch weiterhin automatisch die Inhalte abgerufen, die für die automatische Wiedergabe infrage kommen, und hat Ihnen diese zur manuellen Wiedergabe bereitgestellt, wenn Sie dies tun möchten. Beachten Sie, dass die `renderAttempted` jedes Vorschlagsobjekts auf `false` gesetzt ist.

Wenn Sie stattdessen beim Senden des Ereignisses die Option `renderDecisions` auf `true` gesetzt hätten, hätte die SDK versucht, alle Vorschläge zu rendern, die für das automatische Rendern infrage kommen (wie zuvor beschrieben). Infolgedessen würde die `renderAttempted`-Eigenschaft jedes Vorschlagsobjekts auf `true` gesetzt. In diesem Fall müssten diese Vorschläge nicht manuell gerendert werden.

Bisher haben wir nur Personalisierungsinhalte behandelt, die für das automatische Rendering geeignet sind (d. h. alle Inhalte, die in Adobe Target Visual Experience Composer oder der Web Campaign-Benutzeroberfläche von Adobe Journey Optimizer erstellt wurden). Um Personalisierungsinhalte abzurufen _die nicht automatisch gerendert_ können, müssen Sie den Inhalt anfordern, indem Sie die Option `decisionScopes` beim Senden des Ereignisses ausfüllen. Ein Bereich ist eine Zeichenfolge, die einen bestimmten Vorschlag identifiziert, den Sie vom Server abrufen möchten.

Siehe folgendes Beispiel:

```javascript
alloy("sendEvent", {
    "xdm": {},
    "decisionScopes": ['salutation', 'discount']
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

Wenn in diesem Beispiel Vorschläge auf dem Server gefunden werden, die mit dem `salutation`- oder `discount` übereinstimmen, werden sie zurückgegeben und in das `result.propositions`-Array aufgenommen. Beachten Sie, dass Vorschläge, die sich für das automatische Rendering qualifizieren, weiterhin im `propositions`-Array enthalten sind, unabhängig davon, wie Sie `renderDecisions`- oder `decisionScopes` konfigurieren. Das `propositions`-Array würde in diesem Fall in etwa wie im folgenden Beispiel aussehen:

```json
[
  {
    "id": "AT:cZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ2",
    "scope": "salutation",
    "items": [
      {
        "schema": "https://ns.adobe.com/personalization/json-content-item",
        "data": {
          "id": "4433221",
          "content": {
            "salutation": "Welcome, esteemed visitor!"
          }
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:cZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ2",
      "activity": {
        "id": "384456"
      }
    },  
    "renderAttempted": false
  },
  {
    "id": "AT:FZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ0",
    "scope": "discount",
    "items": [
      {
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "data": {
          "id": "4433222",
          "content": "<div>50% off your order!</div>",
          "format": "text/html"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:FZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ0",
      "activity": {
        "id": "384457"
      }
    },
    "renderAttempted": false
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "__view__",
    "items": [
      {
        "id": "11223344",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">An HTML proposition.</h2>",
          "selector": "#hero",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
      "activity": {
        "id": "384459"
      }
    },
    "renderAttempted": false
  },
  {
    "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
    "scope": "__view__",
    "items": [
      {
        "id": "11223345",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">Another HTML proposition.</h2>",
          "selector": "#sidebar",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
      "activity": {
        "id": "384459"
      }
    },
    "renderAttempted": false
  }
]
```

An dieser Stelle können Sie den Vorschlagsinhalt nach Belieben rendern. In diesem Beispiel ist der Vorschlag, der mit dem `discount` übereinstimmt, ein HTML-Vorschlag, der mit dem formularbasierten Experience Composer von Adobe Target erstellt wurde. Wenn Sie ein Element mit der ID `daily-special` auf Ihrer Seite haben und den Inhalt aus dem `discount` in das `daily-special` rendern möchten, gehen Sie wie folgt vor:

1. Extrahieren von Vorschlägen aus dem `result`.
1. Durchsuchen Sie jeden Vorschlag auf der Suche nach dem Vorschlag mit einem Umfang von `discount`.
1. Wenn Sie einen Vorschlag finden, durchsuchen Sie jedes Element im Vorschlag und suchen Sie nach dem Element, das HTML-Inhalt ist. (Es ist besser zu überprüfen, als anzunehmen.)
1. Wenn Sie ein Element finden, das HTML-Inhalte enthält, suchen Sie auf der Seite nach dem `daily-special`-Element und ersetzen Sie dessen HTML durch den personalisierten Inhalt.
1. Nachdem der Inhalt gerendert wurde, senden Sie ein `display`.

Ihr Code würde wie folgt aussehen:

```javascript
alloy("sendEvent", {
  "xdm": {},
  "decisionScopes": ['salutation', 'discount']
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

  var discountHtml;
  if (discountProposition) {
    // Find the item from proposition that should be rendered.
    // Rather than assuming there is a single item that has HTML
    // content, find the first item whose schema indicates
    // it contains HTML content.
    for (var j = 0; j < discountProposition.items.length; j++) {
      var discountPropositionItem = discountProposition.items[i];
      if (discountPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
        discountHtml = discountPropositionItem.data.content;
        // Render the content
        var dailySpecialElement = document.getElementById("daily-special");
        dailySpecialElement.innerHTML = discountHtml;
        
        // For this example, we assume there is only a single place to update in the HTML.
        break;  
      }
    }
    // Send a "display" event 
    alloy("sendEvent", {
      "xdm": {
        "eventType": "decisioning.propositionDisplay",
        "_experience": {
          "decisioning": {
            "propositions": [
              {
                "id": discountProposition.id,
                "scope": discountProposition.scope,
                "scopeDetails": discountProposition.scopeDetails
              }
            ],
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


>[!TIP]
>
>Wenn Sie Adobe Target verwenden, entsprechen die Bereiche den Mboxes auf dem Server, mit der Ausnahme, dass sie alle gleichzeitig und nicht einzeln angefordert werden. Die globale Mbox wird immer zurückgegeben.

### Verwalten von Flackern

Die SDK bietet Funktionen [Verwalten von Flackern](../personalization/manage-flicker.md) während des Personalisierungsprozesses.

## Vorschläge rendern in Single-Page Applications ohne Inkrementierung von Metriken {#applypropositions}

Mit dem Befehl `applyPropositions` können Sie ein Vorschläge-Array aus [!DNL Target] oder Adobe Journey Optimizer in Einzelseitenanwendungen rendern oder ausführen, ohne die [!DNL Analytics]- und [!DNL Target] zu inkrementieren. Dies erhöht die Genauigkeit des Reportings.

>[!IMPORTANT]
>
>Wenn Vorschläge für den `__view__` (oder eine Web-Oberfläche) beim Laden der Seite gerendert wurden, wird ihr `renderAttempted`-Flag auf `true` gesetzt. Der Befehl `applyPropositions` rendert die Vorschläge für den `__view__` (oder die Web-Oberfläche), die das `renderAttempted: true`-Flag aufweisen, nicht erneut.

### Anwendungsfall 1: Rendern von Ansichtsvorschlägen für Einzelseiten-Apps

Der im folgenden Beispiel beschriebene Anwendungsfall rendert die zuvor abgerufenen und gerenderten Warenkorbansichtsvorschläge erneut, ohne Anzeigebenachrichtigungen zu senden.

Im folgenden Beispiel wird der Befehl `sendEvent` bei einer Änderung der Ansicht ausgelöst und das resultierende Objekt in einer Konstante gespeichert.

Wenn die Ansicht oder eine Komponente aktualisiert wird, wird als Nächstes der Befehl `applyPropositions` mit den Vorschlägen aus dem vorherigen `sendEvent` aufgerufen, um die Ansichtsvorschläge erneut zu rendern.

```js
var cartPropositions = alloy("sendEvent", {
    "renderDecisions": true,
    "xdm": {
        "web": {
            "webPageDetails": {
                "viewName": "cart"
            }
        }
    }
}).then(function(result) {
    var propositions = result.propositions;

    // Collect response tokens, etc.
    return propositions;
});

// Call applyPropositions to re-render the view propositions from the previous sendEvent command.
alloy("applyPropositions", {
    "propositions": cartPropositions
});
```

### Anwendungsfall 2: Vorschläge rendern, die keinen Selektor haben

Dieser Anwendungsfall gilt für Erlebnisse, die mit dem [!DNL Target Form-based Experience Composer] oder dem ([-basierten Erlebniskanal) von Adobe Journey Optimizer ](https://experienceleague.adobe.com/de/docs/journey-optimizer/using/code-based-experience/get-started-code-based).

Sie müssen den Selektor, die Aktion und den Umfang im `applyPropositions`-Aufruf angeben.

Folgende `actionTypes` werden unterstützt:

* `setHtml`
* `replaceHtml`
* `appendHtml`

```js
// Retrieve propositions for salutation and discount scopes
alloy("sendEvent", {
    "decisionScopes": ["salutation", "discount"]
}).then(function(result) {
    var retrievedPropositions = result.propositions;
    // Render propositions on the page by providing additional metadata

    return alloy("applyPropositions", {
        "propositions": retrievedPropositions,
        "metadata": {
            "salutation": {
                "selector": "#first-form-based-offer",
                "actionType": "setHtml"
            },
            "discount": {
                "selector": "#second-form-based-offer",
                "actionType": "replaceHtml"
            }
        }
    }).then(function(applyPropositionsResult) {
        var renderedPropositions = applyPropositionsResult.propositions;

        // Send the display notifications via sendEvent command
        function sendDisplayEvent(proposition) {
            const {
                id,
                scope,
                scopeDetails = {}
            } = proposition;

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
});
```

Wenn Sie keine Metadaten für einen Entscheidungsumfang angeben, werden die zugehörigen Vorschläge nicht gerendert.
