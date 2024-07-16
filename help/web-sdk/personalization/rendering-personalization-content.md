---
title: Rendern von personalisierten Inhalten mit dem Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie personalisierte Inhalte mit dem Adobe Experience Platform Web SDK rendern.
keywords: personalization;renderDecisions;sendEvent;DecisionScopes;propositions;
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: 6841a6f777d18845ce36e3503fbdb9698ece84bb
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 1%

---

# Rendern von personalisierten Inhalten

Das Adobe Experience Platform Web SDK unterstützt das Abrufen personalisierter Inhalte aus Adobe-Personalisierungslösungen, einschließlich [Adobe Target](https://business.adobe.com/de/products/target/adobe-target.html), [Offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=de) und [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=de).

Darüber hinaus ermöglicht das Web SDK Personalisierungsfunktionen für die gleiche Seite und die nächste Seite über Adobe Experience Platform-Personalisierungsziele wie [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) und die [benutzerdefinierte Personalisierungsverbindung](../../destinations/catalog/personalization/custom-personalization.md). Informationen zum Konfigurieren von Experience Platform für die Personalisierung von Seiten mit und nächsten Seiten finden Sie im [dedizierten Handbuch](../../destinations/ui/activate-edge-personalization-destinations.md).

Inhalte, die innerhalb von Adobe Target [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) und der [Web-Campaign-Benutzeroberfläche](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) von Adobe Journey Optimizer erstellt wurden, können vom SDK automatisch abgerufen und wiedergegeben werden. Inhalte, die innerhalb von Adobe Target [Form-Based Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=de), Adobe Journey Optimizers [Code-basierter Experience-Kanal](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/code-based-experience/get-started-code-based) oder Offer Decisioning erstellt wurden, können vom SDK nicht automatisch gerendert werden. Stattdessen müssen Sie diesen Inhalt mit dem SDK anfordern und dann den Inhalt manuell selbst rendern.

## Automatisches Rendern von Inhalten {#automatic}

Beim Senden von Ereignissen an den Server können Sie die `renderDecisions`-Option auf `true` festlegen. Dies zwingt das SDK dazu, personalisierte Inhalte automatisch zu rendern, die für das automatische Rendering geeignet sind.

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

Das Rendern personalisierter Inhalte erfolgt asynchron. Daher sollten Sie keine Annahmen darüber treffen, wann ein bestimmtes Inhaltselement das Rendering abgeschlossen hat.

## Manuelles Rendern von Inhalten {#manual}

Um auf Personalisierungsinhalte zuzugreifen, können Sie eine Callback-Funktion bereitstellen, die aufgerufen wird, nachdem das SDK eine erfolgreiche Antwort vom Server erhalten hat. Ihr Rückruf wird mit einem `result` -Objekt bereitgestellt, das eine `propositions` -Eigenschaft enthalten kann, die alle zurückgegebenen Personalisierungsinhalte enthält. Im Folgenden finden Sie ein Beispiel dafür, wie Sie beim Senden eines Ereignisses eine Rückruffunktion bereitstellen.

```javascript
alloy("sendEvent", {
    "xdm": {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

In diesem Beispiel ist `result.propositions`, sofern vorhanden, ein Array, das Personalisierungsvorschläge für das Ereignis enthält. Standardmäßig enthält es nur Vorschläge, die für das automatische Rendering geeignet sind.

Das `propositions` -Array kann in etwa wie im folgenden Beispiel aussehen:

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

Im Beispiel wurde die Option `renderDecisions` nicht auf `true` gesetzt, als der Befehl `sendEvent` ausgeführt wurde. Daher versuchte das SDK nicht, automatisch Inhalte zu rendern. Das SDK hat jedoch weiterhin automatisch die Inhalte abgerufen, die für das automatische Rendering infrage kommen, und Ihnen dies zum manuellen Rendern bereitgestellt, wenn Sie dies möchten. Beachten Sie, dass für jedes Vorschlagsobjekt die Eigenschaft `renderAttempted` auf `false` festgelegt ist.

Wenn Sie stattdessen die Option `renderDecisions` beim Senden des Ereignisses auf `true` gesetzt hätten, hätte das SDK versucht, alle Vorschläge zu rendern, die für das automatische Rendering infrage kommen (wie zuvor beschrieben). Daher würde für jedes der Vorschlagsobjekte seine Eigenschaft `renderAttempted` auf `true` gesetzt. In diesem Fall müssen diese Vorschläge nicht manuell gerendert werden.

Bislang haben wir nur Personalisierungsinhalte besprochen, die für das automatische Rendering infrage kommen (d. h. alle Inhalte, die im Visual Experience Composer von Adobe Target oder in der Web-Campaign-Benutzeroberfläche von Adobe Journey Optimizer erstellt wurden). Um Personalisierungsinhalte abzurufen, die nicht für die automatische Wiedergabe geeignet sind, müssen Sie den Inhalt anfordern, indem Sie beim Senden des Ereignisses die Option `decisionScopes` ausfüllen. __ Ein Perimeter ist eine Zeichenfolge, die einen bestimmten Vorschlag identifiziert, den Sie vom Server abrufen möchten.

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

In diesem Beispiel werden Vorschläge, die dem Umfang `salutation` oder `discount` entsprechen, zurückgegeben und in das Array `result.propositions` aufgenommen, wenn sie auf dem Server gefunden werden. Beachten Sie, dass Vorschläge, die für das automatische Rendering infrage kommen, auch weiterhin im Array `propositions` enthalten sind, unabhängig davon, wie Sie die Optionen `renderDecisions` oder `decisionScopes` konfigurieren. Das Array `propositions` würde in diesem Fall in etwa wie im folgenden Beispiel aussehen:

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

An dieser Stelle können Sie den Vorschlagsinhalt nach Bedarf rendern. In diesem Beispiel handelt es sich bei dem Vorschlag, der dem `discount` -Bereich entspricht, um einen HTML-Vorschlag, der mit dem formularbasierten Experience Composer von Adobe Target erstellt wurde. Gehen Sie wie folgt vor, wenn Sie ein Element auf Ihrer Seite mit der Kennung `daily-special` haben und den Inhalt aus dem Vorschlag `discount` in das Element `daily-special` rendern möchten:

1. Extrahieren Sie Vorschläge aus dem Objekt `result` .
1. Durchlaufen Sie jeden Vorschlag und suchen Sie nach dem Vorschlag mit dem Umfang &quot;`discount`&quot;.
1. Wenn Sie einen Vorschlag finden, durchlaufen Sie jedes Element im Vorschlag, suchen Sie nach dem Element, das HTML-Inhalt ist. (Es ist besser zu überprüfen als anzunehmen.)
1. Wenn Sie ein Element mit HTML-Inhalt finden, suchen Sie das Element `daily-special` auf der Seite und ersetzen Sie dessen HTML durch den personalisierten-Inhalt.
1. Nachdem der Inhalt wiedergegeben wurde, senden Sie ein `display` -Ereignis.

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
    // Rather than assuming there a single item that has HTML
    // content, find the first item whose schema indicates
    // it contains HTML content.
    for (var j = 0; j < discountProposition.items.length; j++) {
      var discountPropositionItem = discountProposition.items[i];
      if (discountPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
        discountHtml = discountPropositionItem.data.content;
        // Render the content
        var dailySpecialElement = document.getElementById("daily-special");
        dailySpecialElement.innerHTML = discountHtml;
        
        // For this example, we assume there is only a signle place to update in the HTML.
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
            ]
          }
        }
      }
    });
  }
});
```


>[!TIP]
>
>Wenn Sie Adobe Target verwenden, entsprechen die Bereiche Mboxes auf dem Server, sie werden jedoch alle gleichzeitig und nicht einzeln angefordert. Die globale Mbox wird immer zurückgegeben.

### Verwalten von Flackern

Das SDK bietet Funktionen zum [Verwalten von Flackern](../personalization/manage-flicker.md) während des Personalisierungsprozesses.

## Vorschläge in Einzelseitenanwendungen rendern, ohne Metriken zu erhöhen {#applypropositions}

Mit dem Befehl `applyPropositions` können Sie ein Array von Vorschlägen aus [!DNL Target] oder Adobe Journey Optimizer in Einzelseitenanwendungen rendern oder ausführen, ohne die Metriken [!DNL Analytics] und [!DNL Target] zu erhöhen. Dies erhöht die Genauigkeit des Reportings.

>[!IMPORTANT]
>
>Wenn Vorschläge für den Bereich `__view__` (oder eine Weboberfläche) beim Laden der Seite gerendert wurden, wird ihre `renderAttempted` -Markierung auf `true` gesetzt. Der Befehl `applyPropositions` rendert die Vorschläge des Bereichs `__view__` (oder der Weboberfläche), die die Markierung `renderAttempted: true` aufweisen, nicht erneut.

### Anwendungsfall 1: Wiedergeben von Vorschlägen zur Ansicht von Einzelseiten-Apps

Der im folgenden Beispiel beschriebene Anwendungsfall rendert die zuvor abgerufenen und gerenderten Vorschläge zur Warenkorbansicht erneut, ohne dass Anzeigebenachrichtigungen gesendet werden.

Im folgenden Beispiel wird der Befehl `sendEvent` bei einer Änderung der Ansicht ausgelöst und speichert das resultierende Objekt in einer Konstante.

Als Nächstes wird bei der Aktualisierung der Ansicht oder einer Komponente der Befehl `applyPropositions` mit den Vorschlägen des vorherigen Befehls `sendEvent` aufgerufen, um die Anzeigevorschläge erneut darzustellen.

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

### Anwendungsfall 2: Wiedergabevorschläge ohne Selektor

Dieser Anwendungsfall gilt für Erlebnisse, die mit dem [!DNL Target Form-based Experience Composer] oder dem [code-basierten Experience-Kanal](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/code-based-experience/get-started-code-based) von Adobe Journey Optimizer erstellt wurden.

Sie müssen den Selektor, die Aktion und den Perimeter im `applyPropositions` -Aufruf angeben.

Unterstützt werden `actionTypes`:

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
                xdm: {
                    eventType: "decisioning.propositionDisplay",
                    _experience: {
                        decisioning: {
                            propositions: [{
                                id: id,
                                scope: scope,
                                scopeDetails: scopeDetails,
                            }, ],
                            propositionEventType: {
                                display: 1
                            },
                        },
                    },
                },
            });
        }
    });
});
```

Wenn Sie für einen Entscheidungsbereich keine Metadaten angeben, werden die zugehörigen Vorschläge nicht gerendert.
