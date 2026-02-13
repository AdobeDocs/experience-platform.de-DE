---
title: Vorschläge manuell rendern
description: Rendern Sie den Vorschlagsinhalt mithilfe Ihrer eigenen Benutzeroberflächenlogik (HTML, JSON oder benutzerdefinierte Schemata) und zeichnen Sie dann Anzeigeereignisse auf.
keywords: Personalisierung;Vorschläge;manuelles Rendering;sendEvent;Entscheidungsumfänge;Ereignisse anzeigen;
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Vorschläge manuell rendern

Verwenden Sie dieses Muster, wenn Sie die Anwendung der Vorschlagselemente vollständig steuern müssen. Sie erstellen beispielsweise eine komplexe Benutzeroberfläche aus JSON-Inhalten oder Sie möchten benutzerdefinierte Geschäftsregeln vor dem Rendern anwenden.

## &#x200B;1. Anfragevorschläge

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["salutation", "discount"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  // Render in the next step
});
```

Weitere Informationen finden Sie unter dem [`personalization`](/help/collection/js/commands/sendevent/personalization.md)-Objekt im [`sendEvent`](/help/collection/js/commands/sendevent/overview.md).

## &#x200B;2. Vorschlagselemente rendern (Beispiel)

Beim manuellen Rendern von Vorschlägen können sie viele verschiedene Formen oder Formen annehmen. Im Folgenden finden Sie ein minimales Beispiel, das einen Vorschlag nach Umfang sucht und dann das erste HTML-Inhaltselement anwendet, das er findet.

```js
function findPropositionByScope(propositions, scope) {
  return propositions.find((p) => p.scope === scope);
}

function renderHtmlInto(selector, html) {
  const el = document.querySelector(selector);
  if (!el) return;
  el.innerHTML = html;
}

alloy("sendEvent", {
  personalization: { decisionScopes: ["discount"] },
  xdm: { }
}).then(({ propositions = [] }) => {
  const discount = findPropositionByScope(propositions, "discount");
  if (!discount) return { propositions, rendered: [] };

  const htmlItem = discount.items?.find(
    (i) => i.schema === "https://ns.adobe.com/personalization/html-content-item"
  );

  if (!htmlItem) return { propositions, rendered: [] };

  renderHtmlInto("#daily-special", htmlItem.data.content);
  return { propositions, rendered: [discount] };
});
```

>[!IMPORTANT]
>
>Wenn Sie HTML rendern, stellen Sie sicher, dass es für Ihre Umgebung sicher ist. Behandeln Sie das Rendern von Inhalten als Sicherheitsgrenze (Bereinigung, vertrauenswürdige Quellen und Überlegungen zur CSP).

## &#x200B;3. Zeichnen Sie Anzeigeereignisse für Ihre gerenderten Inhalte auf

Bei manuell gerenderten Vorschlägen werden Anzeigeereignisse über `sendEvent` Aufrufe aufgezeichnet, die auf die gerenderten Vorschläge verweisen.

```js
function toDisplayPayload(propositions) {
  return propositions.map((p) => ({
    id: p.id,
    scope: p.scope,
    scopeDetails: p.scopeDetails
  }));
}

// Example: record display for the propositions you actually rendered.
alloy("sendEvent", {
  xdm: {
    _experience: {
      decisioning: {
        propositions: toDisplayPayload(renderedPropositions),
        propositionEventType: { display: 1 }
      }
    }
  }
});
```

Weitere Informationen [&#x200B; Sie unter &#x200B;](display-events.md) von Anzeigeereignissen .

## &#x200B;4. Rendern

Wenn Änderungen an der Benutzeroberfläche ein erneutes Rendern erfordern, führen Sie Ihre manuelle Rendering-Logik für die Vorschlagsdaten erneut aus, die Sie zwischengespeichert haben (oder rufen Sie sie bei Bedarf erneut ab). Wenn Sie eine Anzeige für Re-Render-Szenarien aufzeichnen müssen, finden Sie weitere Informationen unter [Verwalten von Anzeigeereignissen](display-events.md).
