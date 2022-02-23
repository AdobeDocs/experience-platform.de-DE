---
title: Rendern von personalisierten Inhalten mit dem Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie personalisierte Inhalte mit dem Adobe Experience Platform Web SDK rendern.
keywords: personalization;renderDecisions;sendEvent;DecisionScopes;propositions;
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: 6ba563db7fd31084813426ffbb0c35be9d7fe4bb
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 3%

---

# Rendern von personalisierten Inhalten

Das Adobe Experience Platform Web SDK unterstützt das Abrufen personalisierter Inhalte aus Personalisierungslösungen von Adoben, darunter [Adobe Target](https://business.adobe.com/products/target/adobe-target.html) und [offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=de).

Darüber hinaus ermöglicht das Web SDK Personalisierungsfunktionen für die gleiche Seite und die nächste Seite über Adobe Experience Platform-Personalisierungsziele, z. B. [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) und [Benutzerdefinierte Personalisierungsverbindung](../../destinations/catalog/personalization/custom-personalization.md). Informationen zum Konfigurieren der Experience Platform für die Personalisierung der gleichen Seite und der nächsten Seite finden Sie unter [dediziertes Handbuch](../../destinations/ui/configure-personalization-destinations.md).

In Adobe Target erstellte Inhalte [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) kann automatisch vom SDK abgerufen und gerendert werden. In Adobe Target erstellte Inhalte [Form-Based Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) oder Offer decisioning kann nicht automatisch vom SDK gerendert werden. Stattdessen müssen Sie diesen Inhalt mit dem SDK anfordern und dann den Inhalt manuell selbst rendern.

## Automatisches Rendern von Inhalten

Beim Senden von Ereignissen an den Server können Sie die `renderDecisions` -Option `true`. Dies zwingt das SDK dazu, personalisierte Inhalte automatisch zu rendern, die für das automatische Rendering geeignet sind.

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

## Manuelles Rendern von Inhalten

Um auf Personalisierungsinhalte zuzugreifen, können Sie eine Callback-Funktion bereitstellen, die aufgerufen wird, nachdem das SDK eine erfolgreiche Antwort vom Server erhalten hat. Ihr Rückruf wird mit einem `result` -Objekt, das eine `propositions` -Eigenschaft, die alle zurückgegebenen Personalisierungsinhalte enthält. Im Folgenden finden Sie ein Beispiel dafür, wie Sie beim Senden eines Ereignisses eine Rückruffunktion bereitstellen.

```javascript
alloy("sendEvent", {
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

In diesem Beispiel `result.propositions`, sofern vorhanden, ist ein Array mit Personalisierungsvorschlägen für das Ereignis. Standardmäßig enthält es nur Vorschläge, die für das automatische Rendering geeignet sind.

Die `propositions` -Array ähnelt möglicherweise diesem Beispiel:

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

Im Beispiel wird die `renderDecisions` -Option wurde nicht auf `true` wenn die `sendEvent` ausgeführt wurde, sodass das SDK nicht versucht hat, automatisch Inhalte zu rendern. Das SDK hat jedoch weiterhin automatisch die Inhalte abgerufen, die für das automatische Rendering infrage kommen, und Ihnen dies zum manuellen Rendern bereitgestellt, wenn Sie dies möchten. Beachten Sie, dass jedes Vorschlagsobjekt seinen `renderAttempted` Eigenschaft auf `false`.

Wenn Sie stattdessen die Variable `renderDecisions` -Option `true` Beim Senden des Ereignisses hätte das SDK versucht, alle Vorschläge zu rendern, die für das automatische Rendering infrage kommen (wie zuvor beschrieben). Daher würde jedes der Vorschlagsobjekte seine `renderAttempted` Eigenschaft auf `true`. In diesem Fall müssen diese Vorschläge nicht manuell gerendert werden.

Bislang haben wir nur Personalisierungsinhalte besprochen, die für die automatische Wiedergabe geeignet sind (d. h. alle Inhalte, die im Visual Experience Composer von Adobe Target erstellt wurden). Abrufen von Personalisierungsinhalten _not_ für das automatische Rendering geeignet ist, müssen Sie den Inhalt anfordern, indem Sie die `decisionScopes` -Option beim Senden des Ereignisses. Ein Perimeter ist eine Zeichenfolge, die einen bestimmten Vorschlag identifiziert, den Sie vom Server abrufen möchten.

Siehe folgendes Beispiel:

```javascript
alloy("sendEvent", {
    xdm: {},
    decisionScopes: ['salutation', 'discount']
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

In diesem Beispiel, wenn Vorschläge auf dem Server gefunden werden, die dem `salutation` oder `discount` , werden sie zurückgegeben und in die `result.propositions` Array. Beachten Sie, dass Vorschläge, die für das automatische Rendering infrage kommen, weiterhin im Abschnitt `propositions` Array, unabhängig von der Konfiguration `renderDecisions` oder `decisionScopes` Optionen. Die `propositions` -Array würde in diesem Fall in etwa wie folgt aussehen:

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

An dieser Stelle können Sie den Vorschlagsinhalt nach Bedarf rendern. In diesem Beispiel entspricht der Vorschlag dem `discount` scope ist ein HTML-Vorschlag, der mit dem formularbasierten Experience Composer von Adobe Target erstellt wurde. Angenommen, Sie haben ein Element auf Ihrer Seite mit der ID `daily-special` und den Inhalt aus der `discount` Vorschlag in die `daily-special` -Element Folgendes ausführen:

1. Entnehmen Sie Vorschläge aus dem `result` -Objekt.
1. Durchlaufen Sie jeden Vorschlag und suchen Sie nach dem Vorschlag mit einem Umfang von `discount`.
1. Wenn Sie einen Vorschlag finden, durchlaufen Sie jedes Element im Vorschlag, suchen Sie nach dem Element, das HTML-Inhalt ist. (Es ist besser zu überprüfen als anzunehmen.)
1. Wenn Sie einen Artikel finden, der HTML-Inhalt enthält, suchen Sie nach der `daily-special` -Element auf der Seite und ersetzen Sie die zugehörige HTML durch den personalisierten Inhalt.
1. Nachdem der Inhalt wiedergegeben wurde, senden Sie eine `display` -Ereignis.

Ihr Code würde wie folgt aussehen:

```javascript
alloy("sendEvent", {
  xdm: {},
  decisionScopes: ['salutation', 'discount']
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
      xdm: {
        eventType: "decisioning.propositionDisplay",
        _experience: {
          decisioning: {
            propositions: [
              {
                id: discountProposition.id,
                scope: discountProposition.scope,
                scopeDetails: discountProposition.scopeDetails
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

Das SDK bietet Funktionen für [Flackern verwalten](../personalization/manage-flicker.md) während des Personalisierungsprozesses.
