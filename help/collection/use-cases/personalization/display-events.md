---
title: Verwalten von Anzeigeereignissen in der Web-SDK
description: Erläutert Anzeigeereignisse und deren Verwendung in der Web-SDK.
exl-id: 7150ad6e-7693-4f4d-917e-8d08a39a0b41
keywords: Personalisierung;Ereignisse anzeigen;sendEvent;renderDecisions;applyPropositions;Vorschläge;
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# Verwalten von Anzeigeereignissen in der Web-SDK

Anzeigeereignisse teilen Personalisierungs- oder Analytics-Services mit, dass dem Benutzer ein bestimmter Teil des personalisierten Inhalts angezeigt wurde. Das Senden von Anzeigeereignissen verbessert die Genauigkeit des Reportings, indem nachgelagerte Systeme dabei helfen, zwischen *(angeforderten* und tatsächlich *Inhalten* unterscheiden.

## Anzeigeereignisse automatisch senden

Automatische Anzeigeereignisse sind in der Regel die einfachste Option. Sie werden sofort gesendet, nachdem Web SDK das Rendern der zulässigen Inhalte aus der `sendEvent` abgeschlossen hat, was die Berichtsgenauigkeit verbessern kann.

Um Anzeigeereignisse automatisch zu senden, verwenden Sie einen `sendEvent`-Aufruf, der `renderDecisions` auf `true` setzt und `personalization.sendDisplayEvent` auf `true` setzt (oder auslässt, da `true` der Standard ist):

```js
alloy("sendEvent", {
  renderDecisions: true,
  personalization: { }, // sendDisplayEvent defaults to true
  xdm: {
    web: {
      webPageDetails: {
        name: "home"
      }
    }
  }
});
```

>[!NOTE]
>
>Automatische Anzeigeereignisse hängen vom SDK-verwalteten Rendering ab. Wenn Sie Inhalte manuell rendern (auch mithilfe von `applyPropositions`), müssen Sie Anzeigeereignisse explizit mithilfe von `sendEvent` senden.

## Senden von Anzeigeereignissen in nachfolgenden `sendEvent`

Die Einbeziehung von Anzeigeereignissen in einen späteren `sendEvent` ist nützlich, wenn Sie zusätzliche Seitenladedaten anhängen möchten, die bei der Anforderung von Personalisierung nicht verfügbar sind. Er wird häufig bei der Implementierung von [Top- und Bottom-Page-Ereignissen](/help/collection/use-cases/personalization/top-bottom-page-events.md) verwendet. Wenn Sie Anzeigeereignisse auf diese Weise korrekt implementieren, vermeiden Sie Probleme mit [Absprungrate](https://experienceleague.adobe.com/en/docs/analytics/components/metrics/bounce-rate) in Adobe Analytics.

1. Fordern Sie beim ersten `sendEvent`-Aufruf (häufig oben auf der Seite) Inhalte an und rendern Sie sie, unterdrücken Sie jedoch automatische Anzeigeereignisse, indem Sie `renderDecisions` auf `true` und `personalization.sendDisplayEvent` auf `false` setzen:

   ```js
   alloy("sendEvent", {
     renderDecisions: true,
     personalization: { sendDisplayEvent: false },
     xdm: {
       web: {
         webPageDetails: {
            name: "home"
         }
       }
     }
   });
   ```

1. Rufen Sie später (häufig unten auf der Seite) `sendEvent` mit einer XDM-Payload auf, die Anzeigeereignisse für Vorschläge enthält, die seit der vorherigen Anfrage gerendert wurden, indem Sie [`personalization.includeRenderedPropositions`](/help/collection/js/commands/sendevent/personalization.md) auf `true` setzen:

   ```js
   alloy("sendEvent", {
     personalization: { includeRenderedPropositions: true },
     xdm: {
       // Add any additional page load telemetry you want to send here
       web: {
         webPageDetails: {
           name: "home"
         }
       }
     }
   });
   ```

>[!NOTE]
>
>Bei der Verwendung von `includeRenderedPropositions` werden nur automatisch gerenderte Vorschläge einbezogen, die die Anzeige unterdrückt hatten.

## Senden von Anzeigeereignissen für manuell gerenderte Vorschläge

Wenn Sie Inhalte selbst rendern (entweder vollständig manuelles Rendern oder `applyPropositions`), müssen Sie Anzeigeereignisse explizit mit dem Befehl `sendEvent` senden. Rufen Sie `sendEvent` mit einer XDM-Payload auf, die die folgenden Eigenschaften enthält:

* `_experience.decisioning.propositions` mit den `id`, `scope` und `scopeDetails` der gerenderten Vorschläge
* `_experience.decisioning.propositionEventType.display` festgelegt auf `1`

Die folgenden beiden Beispiele verwenden diese Hilfsfunktion zum Erstellen der XDM-Payload für das Anzeigeereignis:

```js
function buildDisplayEventXdm(renderedPropositions) {
  return {
    eventType: "decisioning.propositionDisplay",
    _experience: {
      decisioning: {
        propositions: renderedPropositions.map(({ id, scope, scopeDetails }) => ({
          id,
          scope,
          scopeDetails
        })),
        propositionEventType: { display: 1 }
      }
    }
  };
}
```

Im folgenden Beispiel wird das manuelle Rendering mit Anzeigeereignissen verwendet:

```js
function renderExample(propositions) {
  // Your custom logic here. Return ONLY the propositions that were actually rendered.
  // For example: return [propositions[0]];
  return [];
}

alloy("sendEvent", {
  personalization: { decisionScopes: ["discount"] },
  xdm: { }
}).then(({ propositions = [] }) => {
  const renderedPropositions = renderExample(propositions);
  if (!renderedPropositions.length) { return; }
  return alloy("sendEvent", { xdm: buildDisplayEventXdm(renderedPropositions) });
});
```

Im folgenden Beispiel wird der Befehl `applyPropositions` mit Anzeigeereignissen verwendet. Er verkettet `sendEvent`, `applyPropositions` und dann eine weitere `sendEvent`:

```js
alloy("sendEvent", {
  personalization: { decisionScopes: ["discount", "salutation"] },
  xdm: { }
}).then(({ propositions = [] }) => {
  return alloy("applyPropositions", {
    propositions,
    metadata: {
      salutation: { selector: "#salutation", actionType: "setHtml" },
      discount: { selector: "#daily-special", actionType: "replaceHtml" }
    }
  });
}).then(({ propositions: renderedPropositions = [] }) => {
  if (!renderedPropositions.length) { return; }
  return alloy("sendEvent", { xdm: buildDisplayEventXdm(renderedPropositions) });
});
```

## Häufige zu vermeidende Fehler

* **Anzeigeereignisse senden, bevor das Rendern abgeschlossen ist**: Senden Sie Anzeigeereignisse, nachdem das automatische Rendern abgeschlossen ist, nachdem `applyPropositions` aufgelöst wurde oder nachdem die manuelle Rendering-Logik abgeschlossen ist.
* **Senden von Anzeigeereignissen für Vorschläge, die Sie nicht gerendert haben**: Schließen Sie nur Vorschläge ein, die der Benutzerin bzw. dem Benutzer tatsächlich angezeigt wurden.
* **`scopeDetails`**: Beim Senden von Anzeigeereignissen `scopeDetails` aus dem Vorschlagsobjekt einfügen.
