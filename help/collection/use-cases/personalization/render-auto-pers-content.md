---
title: DOM-Aktionsvorschläge automatisch rendern
description: Verwenden Sie Web SDK, um geeignete DOM-Aktionsvorschläge automatisch zu rendern und gängige SPA-Render-Szenarien zu verarbeiten.
keywords: Personalisierung;renderDecisions;dom-action;sendEvent;applyPropositions;Einzelseitenanwendung;
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# DOM-Aktionsvorschläge automatisch rendern

Verwenden Sie dieses Muster, wenn Ihre Personalisierungsantwort Vorschlagselemente mit dem Schema enthält:

**`https://ns.adobe.com/personalization/dom-action`**

Diese Elemente enthalten in der Regel einen Selektor und einen Aktionstyp (z. B. `setHtml`), den die Web-SDK automatisch anwenden kann, wenn `renderDecisions` aktiviert ist.

## &#x200B;1. Verwalten von Flackern (optional)

Wenn Sie ein Flackern verhindern müssen, während personalisierte Inhalte angewendet werden, verwenden Sie den empfohlenen Flimmerverwaltungsansatz für Ihre Implementierung. Verfügbare Optionen [ Sie unter ](manage-flicker.md)Verwalten von Flackern“.

## &#x200B;2. Anfordern und Rendern von Entscheidungen, die für das automatische Rendern notiert sind

Legen Sie `renderDecisions` beim Aufrufen des `true`-Befehls auf `sendEvent` fest. Die `renderDecisions`-Eigenschaft ist standardmäßig auf „false“ festgelegt, wenn sie weggelassen wird.

```js
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    web: {
      webPageDetails: {
        name: "home"
      }
    }
  }
});
```

Optional können Sie, wenn Sie bestimmte Platzierungen anfordern müssen, Folgendes `personalization.decisionScopes`:

```js
alloy("sendEvent", {
  renderDecisions: true,
  personalization: {
    decisionScopes: ["hero-banner", "recommendations"]
  },
  xdm: { }
});
```

Weitere Informationen finden Sie unter dem [`personalization`](/help/collection/js/commands/sendevent/personalization.md)-Objekt im [`sendEvent`](/help/collection/js/commands/sendevent/overview.md).

## &#x200B;3. Ereignisse anzeigen

Wenn Sie `renderDecisions` auf `true` setzen und `personalization.sendDisplayEvent` entweder auf `true` setzen oder auslassen, sendet die Web-SDK Anzeigeereignisse sofort nach dem Rendern der Personalisierung.

```js
alloy("sendEvent", {
  renderDecisions: true,
  personalization: {
    // sendDisplayEvent defaults to true when omitted
  },
  xdm: { }
});
```

Unter [Anzeigeereignisse verwalten](display-events.md) finden Sie alternative Optionen, die den Anforderungen Ihrer Implementierung entsprechen, z. B. bei Verwendung von [Ereignissen der oberen und unteren Seite](top-bottom-page-events.md).

## &#x200B;4. Änderungen und Rendering der SPA-Ansicht

Geben Sie bei Single Page Applications eine `viewName` zu Ereignissen an, die die Ansicht ändern.

```js
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    web: {
      webPageDetails: {
        viewName: "cart"
      }
    }
  }
});
```

Wenn Ihre SPA die Benutzeroberfläche für dieselbe Ansicht ohne neuen Entscheidungsabruf erneut rendert, können Sie die zuvor zurückgegebenen Vorschläge erneut anwenden:

```js
let lastPropositions = [];

alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    web: { webPageDetails: { viewName: "cart" } }
  }
}).then(({ propositions = [] }) => {
  lastPropositions = propositions;
});

// Later, after a UI re-render:
alloy("applyPropositions", {
  propositions: lastPropositions
});
```

Weitere Informationen finden Sie unter [`applyPropositions`](/help/collection/js/commands/applypropositions.md) .

>[!NOTE]
>
>Der Befehl `applyPropositions` sendet nicht automatisch Anzeigeereignisse. Wenn Sie „Anzeige“ für Re-Render-Szenarien aufzeichnen müssen, finden Sie weitere Informationen unter [Verwalten von Anzeigeereignissen](display-events.md).
