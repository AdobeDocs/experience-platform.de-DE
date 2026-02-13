---
title: Rendern von HTML-Angeboten ohne Selektoren
description: Rendern Sie HTML-Vorschlagselemente, die keine Selektoren enthalten, indem Sie Metadaten für applyPropositions bereitstellen und dann Anzeigeereignisse aufzeichnen.
keywords: Personalisierung;applyPropositions;Metadaten;actionType;Entscheidungsumfänge;Ereignisse anzeigen;
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# Rendern von HTML-Angeboten ohne Selektoren

Verwenden Sie dieses Muster, wenn Ihre Vorschläge HTML-Inhalte enthalten, Sie jedoch angeben müssen, wo Sie es anwenden möchten (Selektor) und wie es angewendet werden soll (Aktionstyp). Dies können Sie tun, indem Sie [`applyPropositions`](/help/collection/js/commands/applypropositions.md) mit einem vom Umfang `metadata` -Objekt aufrufen. Unterstützte `actionType` sind `setHtml`, `replaceHtml` und `appendHtml`.

## &#x200B;1. Verwalten von Flackern (optional)

Wenn Sie Inhalte beim Rendern ausblenden, sind Sie dafür verantwortlich, sie nach Abschluss des Renderings anzuzeigen. Weitere Informationen finden [&#x200B; unter &#x200B;](manage-flicker.md) verwalten.

## &#x200B;2. Anfordern von Vorschlägen für die Bereiche, die Sie rendern möchten

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["discount", "salutation"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  // Render in the next step
});
```

Weitere Informationen finden Sie unter [`personalization.decisionScopes`](/help/collection/js/commands/sendevent/personalization.md) .

## &#x200B;3. Rendern von Angeboten mit `applyPropositions` Metadaten

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["discount", "salutation"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  return alloy("applyPropositions", {
    propositions,
    metadata: {
      salutation: {
        selector: "#salutation",
        actionType: "setHtml"
      },
      discount: {
        selector: "#daily-special",
        actionType: "replaceHtml"
      }
    }
  }).then(({ propositions: renderedPropositions = [] }) => {
    return { renderedPropositions };
  });
});
```

## &#x200B;4. Anzeigen von Ereignissen für gerenderte Vorschläge aufzeichnen

Anzeigeereignisse werden beim Aufruf von `applyPropositions` nicht automatisch gesendet. Verwenden Sie nach Abschluss des Renderings einen `sendEvent`-Aufruf, der auf die gerenderten Vorschläge verweist:

```js
function toDisplayPayload(propositions) {
  return propositions.map((p) => ({
    id: p.id,
    scope: p.scope,
    scopeDetails: p.scopeDetails
  }));
}

alloy("sendEvent", {
  personalization: {
    decisionScopes: ["discount", "salutation"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  return alloy("applyPropositions", {
    propositions,
    metadata: {
      salutation: { selector: "#salutation", actionType: "setHtml" },
      discount: { selector: "#daily-special", actionType: "replaceHtml" }
    }
  }).then(({ propositions: renderedPropositions = [] }) => {
    return alloy("sendEvent", {
      xdm: {
        _experience: {
          decisioning: {
            propositions: toDisplayPayload(renderedPropositions),
            propositionEventType: { display: 1 }
          }
        }
      }
    });
  });
});
```

Weitere Informationen [&#x200B; Sie unter &#x200B;](display-events.md) von Anzeigeereignissen .

>[!TIP]
>
>Wenn Sie [Ereignisse der oberen und unteren Seite](top-bottom-page-events.md) verwenden, wird dieser Aufruf zur Datensatzanzeige häufig im Aufruf der unteren `sendEvent` implementiert.

## &#x200B;5. Rendern

Wenn Ihre Implementierung später erneut gerendert werden muss (z. B. in Single Page Applications), rufen Sie `applyPropositions` mit denselben Vorschlägen und Metadaten erneut auf:

```js
alloy("applyPropositions", {
  propositions,
  metadata: {
    discount: { selector: "#daily-special", actionType: "replaceHtml" }
  }
});
```

Wenn Sie ein Anzeigeereignis für dieses erneute Rendern aufzeichnen müssen, finden Sie weitere Informationen unter [Verwalten von Anzeigeereignissen](display-events.md).
