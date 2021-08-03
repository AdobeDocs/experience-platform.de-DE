---
title: Rendern von personalisierten Inhalten mit dem Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie personalisierte Inhalte mit dem Adobe Experience Platform Web SDK rendern.
keywords: personalization;renderDecisions;sendEvent;DecisionScopes;propositions;
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: 5ae7488e715ff97d2b667c40505b79433eb74f49
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 3%

---

# Rendern von personalisierten Inhalten

Das Adobe Experience Platform Web SDK unterstützt das Abrufen personalisierter Inhalte aus Personalisierungslösungen bei Adobe, einschließlich [Adobe Target](https://business.adobe.com/products/target/adobe-target.html) und [Offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=de). Inhalte, die innerhalb von Adobe Target [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) erstellt wurden, können vom SDK automatisch abgerufen und gerendert werden. Inhalte, die innerhalb von Adobe Target [Form-Based Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) oder Offer decisioning erstellt wurden, können nicht automatisch vom SDK gerendert werden. Stattdessen müssen Sie diesen Inhalt mit dem SDK anfordern und dann den Inhalt manuell selbst rendern.

## Automatisches Rendern von Inhalten

Beim Senden von Ereignissen an den Server können Sie die `renderDecisions`-Option auf `true` setzen. Dies zwingt das SDK dazu, personalisierte Inhalte automatisch zu rendern, die für das automatische Rendering geeignet sind.

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

Um auf Personalisierungsinhalte zuzugreifen, können Sie eine Callback-Funktion bereitstellen, die aufgerufen wird, nachdem das SDK eine erfolgreiche Antwort vom Server erhalten hat. Ihr Rückruf wird mit einem `result` -Objekt bereitgestellt, das eine `propositions` -Eigenschaft enthalten kann, die alle zurückgegebenen Personalisierungsinhalte enthält. Im Folgenden finden Sie ein Beispiel dafür, wie Sie beim Senden eines Ereignisses eine Rückruffunktion bereitstellen.

```javascript
alloy("sendEvent", {
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions
    }
  });
```

In diesem Beispiel ist `result.propositions`, sofern vorhanden, ein Array, das Personalisierungsvorschläge für das Ereignis enthält. Standardmäßig enthält es nur Vorschläge, die für das automatische Rendering geeignet sind.

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
    "renderAttempted": false
  }
]
```

Im Beispiel wurde die Option `renderDecisions` bei Ausführung des Befehls `sendEvent` nicht auf `true` gesetzt, sodass das SDK nicht versucht hat, automatisch Inhalte zu rendern. Das SDK hat jedoch weiterhin automatisch die Inhalte abgerufen, die für das automatische Rendering infrage kommen, und Ihnen dies zum manuellen Rendern bereitgestellt, wenn Sie dies möchten. Beachten Sie, dass für jedes Vorschlagsobjekt die Eigenschaft `renderAttempted` auf `false` festgelegt ist.

Wenn Sie stattdessen die Option `renderDecisions` beim Senden des Ereignisses auf `true` gesetzt hätten, hätte das SDK versucht, alle Vorschläge wiederzugeben, die für das automatische Rendering infrage kommen (wie zuvor beschrieben). Daher wird für jedes der Vorschlagsobjekte die Eigenschaft `renderAttempted` auf `true` gesetzt. In diesem Fall müssen diese Vorschläge nicht manuell gerendert werden.

Bislang haben wir nur Personalisierungsinhalte besprochen, die für die automatische Wiedergabe geeignet sind (d. h. alle Inhalte, die im Visual Experience Composer von Adobe Target erstellt wurden). Um Personalisierungsinhalte abzurufen, die für das automatische Rendering nicht _infrage kommen, müssen Sie den Inhalt anfordern, indem Sie beim Senden des Ereignisses die Option `decisionScopes` ausfüllen._ Ein Perimeter ist eine Zeichenfolge, die einen bestimmten Vorschlag identifiziert, den Sie vom Server abrufen möchten.

Siehe folgendes Beispiel:

```javascript
alloy("sendEvent", {
    xdm: {},
    decisionScopes: ['salutation', 'discount']
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions
    }
  });
```

In diesem Beispiel werden Vorschläge, die dem Perimeter `salutation` oder `discount` entsprechen, zurückgegeben und in das Array `result.propositions` aufgenommen. Beachten Sie, dass Vorschläge, die für das automatische Rendering infrage kommen, weiterhin im Array `propositions` enthalten sind, unabhängig davon, wie Sie die Optionen `renderDecisions` oder `decisionScopes` konfigurieren. Das `propositions` -Array würde in diesem Fall in etwa wie im folgenden Beispiel aussehen:

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
    "renderAttempted": false
  }
]
```

An dieser Stelle können Sie den Vorschlagsinhalt nach Bedarf rendern. In diesem Beispiel handelt es sich bei dem Vorschlag, der mit dem Perimeter `discount` übereinstimmt, um einen HTML-Vorschlag, der mit dem formularbasierten Experience Composer von Adobe Target erstellt wurde. Gehen Sie wie folgt vor, wenn Sie ein Element auf Ihrer Seite mit der Kennung `daily-special` haben und den Inhalt aus dem `discount`-Vorschlag in das Element `daily-special` rendern möchten:

1. Entpacken Sie Vorschläge aus dem `result` -Objekt.
1. Durchlaufen Sie jeden Vorschlag und suchen Sie nach dem Vorschlag mit einem Umfang von `discount`.
1. Wenn Sie einen Vorschlag finden, durchlaufen Sie jedes Element im Vorschlag und suchen Sie nach dem Element, das HTML-Inhalt ist. (Es ist besser zu überprüfen als anzunehmen.)
1. Wenn Sie ein Element mit HTML-Inhalt finden, suchen Sie das Element `daily-special` auf der Seite und ersetzen Sie dessen HTML durch den personalisierten Inhalt.

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
        break;
      }
    }
  }

  if (discountHtml) {
    // Discount HTML exists. Time to render it.
    var dailySpecialElement = document.getElementById("daily-special");
    dailySpecialElement.innerHTML = discountHtml;
  }
});
```


>[!TIP]
>
>Wenn Sie Adobe Target verwenden, entsprechen die Bereiche Mboxes auf dem Server, sie werden jedoch alle gleichzeitig und nicht einzeln angefordert. Die globale Mbox wird immer zurückgegeben.

### Verwalten von Flackern

Das SDK bietet Funktionen zum [Verwalten von Flackern](../personalization/manage-flicker.md) während des Personalisierungsprozesses.
