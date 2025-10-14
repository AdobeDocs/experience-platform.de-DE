---
title: Konfigurieren der Seitenansichten oben und unten in Web SDK
description: In diesem Artikel wird erläutert, wie in Web SDK Seitenereignisse am Anfang und Ende verwendet werden.
exl-id: 43c6d53a-6bf9-45f8-b001-d148adaff829
source-git-commit: 4d0895c6ad38523f5527c9630931c3c0b8ef83c0
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 2%

---


# Konfigurieren der Seitenansichten oben und unten in Web SDK

Wenn Sie Ihren Kunden personalisierte Erlebnisse bieten möchten, ist die Ladezeit einer Web-Seite von entscheidender Bedeutung.

Um die Ladezeiten zu optimieren und Personalisierung so schnell wie möglich bereitzustellen, unterstützt Web SDK die Konfiguration von Top- und Bottom-of-Page-Ereignissen.

Die Ereignisse oben und unten auf der Seite beschreiben eine Methode zum asynchronen Laden verschiedener Elemente auf der Seite, wobei die Ladezeit der Seite auf ein Minimum beschränkt bleibt.

Diese Konfiguration minimiert die Zeit, die ein Benutzer warten muss, bis der personalisierte Inhalt geladen wird.

Was die Genauigkeit von Metriken angeht, kann Adobe Analytics die Ereignisse am Seitenanfang ignorieren, was zu einer präziseren Metrikaufzeichnung führt, da nur ein Seitentreffer aufgezeichnet wird (das Ereignis am Seitenende).

## Anwendungsfälle {#use-cases}

Ein Einzelhändler für Sportbekleidung möchte seinen Kundinnen und Kunden personalisierte Erlebnisse bieten und gleichzeitig die Reibung der Benutzenden beim Besuch seiner Website minimieren, während er in der Lage ist, Besuchermetriken genau zu erfassen.

Durch die Verwendung von Top- und Bottom-of-Page-Ereignissen in Web SDK kann das Marketing-Team den Personalisierungsversand optimal konfigurieren:

* Web SDK sendet eine Personalisierungsanfrage, die geladen wird, sobald die Seite geladen wird. Dies ist ein Ereignis am Anfang der Seite.
* Nach dem Laden der Seite wird ein Seitenansichtsereignis aufgezeichnet. Dies geschieht später beim Laden der Seite. Dies ist ein Ereignis am Ende der Seite.

## Beispiel für ein Top-of-Page-Ereignis {#top-of-page}

Das folgende Codebeispiel veranschaulicht eine Ereigniskonfiguration „Seitenanfang“, bei der für automatisch gerenderte Vorschläge eine Personalisierung angefordert, aber [Anzeigeereignisse](../personalization/display-events.md#send-sendEvent-calls) gesendet wird. Die [Anzeigeereignisse](../personalization/display-events.md#send-sendEvent-calls) werden als Teil des Ereignisses „Seitenende“ gesendet.

>[!BEGINTABS]

>[!TAB Ereignis am Seitenanfang]

```js
alloy("sendEvent", {
  type: "decisioning.propositionFetch",
  renderDecisions: true,
  personalization: {
    sendDisplayEvent: false
  }
});
```

| Parameter | Erforderlich/Optional | Beschreibung |
|---|---|---|
| `type` | Erforderlich | Legen Sie diesen Parameter auf `decisioning.propositionFetch` fest. Dieser spezielle Ereignistyp weist Adobe Analytics an, dieses Ereignis zu ignorieren. Wenn Sie Customer Journey Analytics verwenden, können Sie auch einen Filter einrichten, um diese Ereignisse zu löschen. |
| `renderDecisions` | Erforderlich | Legen Sie diesen Parameter auf `true` fest. Dieser Parameter weist Web SDK an, vom Edge Network zurückgegebene Entscheidungen zu rendern. |
| `personalization.sendDisplayEvent` | Erforderlich | Legen Sie diesen Parameter auf `false` fest. Dies verhindert, dass Anzeigeereignisse gesendet werden. |

>[!ENDTABS]

## Ereignisbeispiele unten auf der Seite {#bottom-of-page}

>[!BEGINTABS]

>[!TAB Automatisch gerenderte Vorschläge]

Das folgende Codebeispiel veranschaulicht eine Ereigniskonfiguration für das untere Ende der Seite, die Anzeigeereignisse für Vorschläge sendet, die automatisch auf der Seite gerendert wurden, für die jedoch Anzeigeereignisse im Ereignis [Seitenanfang](#top-of-page) unterdrückt wurden.

>[!NOTE]
>
>In diesem Szenario müssen Sie das Ereignis „Ende der Seite“ _nach_ oben auf der ersten Seite aufrufen. Das Ereignis „Seitenende“ muss jedoch nicht warten, bis der Seitenanfang abgeschlossen ist.

```js
alloy("sendEvent", {
  personalization: {
    includeRenderedPropositions: true
  },
  xdm: { ... }
});
```

| Parameter | Erforderlich/Optional | Beschreibung |
|---|---|---|
| `personalization.includeRenderedPropositions` | Erforderlich | Legen Sie diesen Parameter auf `true` fest. Dies ermöglicht das Senden von Anzeigeereignissen, die oben auf der Seite unterdrückt wurden. |
| `xdm` | Optional | Verwenden Sie diesen Abschnitt, um alle Daten einzuschließen, die Sie für das Ereignis „Seitenende“ benötigen. |

>[!TAB Manuell gerenderte Vorschläge]

Das folgende Codebeispiel veranschaulicht eine Ereigniskonfiguration für das Ende der Seite, die Anzeigeereignisse für Vorschläge sendet, die auf der Seite manuell gerendert wurden (d. h. für benutzerdefinierte Entscheidungsumfänge oder Oberflächen).

>[!NOTE]
>
>In diesem Szenario muss das Ereignis „Seitenende“ warten, bis das Ereignis „Seitenanfang“ abgeschlossen ist, um die Vorschläge zu rendern und das Ereignis „Seitenende“ aufzuzeichnen.

```js
alloy("sendEvent", {
  xdm: { 
    ... // Optional bottom of page event data
    _experience: {
      decisioning: {
        propositions: propositions.map(function(p) {
          return {
            id: p.id,
            scope: p.scope,
            scopeDetails: p.scopeDetails
          };
        }),
        propositionEventType: {
          display: 1
        }
      }
    }
  }
});
```



| Parameter | Erforderlich/Optional | Beschreibung |
|---|---|---|
| `xdm._experience.decisioning.propositions` | Erforderlich | In diesem Abschnitt werden die manuell gerenderten Vorschläge definiert. Sie müssen die `ID`, `scope` und `scopeDetails` der Vorschläge einbeziehen. Weitere Informationen zum Aufzeichnen von Anzeigeereignissen für manuell [&#x200B; Inhalte finden Sie in &#x200B;](../personalization/rendering-personalization-content.md#manually) Dokumentation zum manuellen Rendern der Personalisierung . Manuell gerenderte Personalisierungsinhalte müssen am unteren Rand des Seitenaufrufs eingefügt werden. |
| `xdm._experience.decisioning.propositionEventType` | Erforderlich | Legen Sie diesen Parameter auf `display: 1` fest. |
| `xdm` | Optional | Verwenden Sie diesen Abschnitt, um alle Daten einzuschließen, die Sie für das Ereignis „Seitenende“ benötigen. |

>[!ENDTABS]


## Einzelseitenanwendung mit Seitenaufrufen am oberen und unteren Rand {#spa-example}


>[!BEGINTABS]

>[!TAB Erste Seitenansicht]

Im folgenden Beispiel wird der erforderliche `xdm.web.webPageDetails.viewName`-Parameter hinzugefügt. Dadurch wird sie zu einer Single Page Application. Der `viewName` in diesem Beispiel ist die Ansicht, die beim Laden der Seite geladen wird.

```js
// Top of page, render decisions for the "home" view.
alloy("sendEvent", {
    type: "decisioning.propositionFetch",
    renderDecisions: true,
    personalization: {
        sendDisplayEvent: false
    },
    xdm: {
        web: {
            webPageDetails: {
                viewName: "home"
            }
        }
    }
});

// Bottom of page, send display events for the items that were rendered.
// Note: You need to include the viewName in both top and bottom of page so that the
// correct view is rendered at the top of the page, and the correct view is recorded
// at the bottom of the page.

alloy("sendEvent", {
    personalization: {
        includeRenderedPropositions: true
    },
    xdm: {
        ...,
        web: {
            webPageDetails: {
                viewName: "home"
            }
        }
    }
});
```

>[!TAB Zweite Seitenansicht (Option 1)]

In diesem Beispiel ist es nicht erforderlich, eine Oben/Unten-Aufteilung der Seite durchzuführen, da die Personalisierung für die Seite bereits abgerufen wurde.

```js
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    ...,
    web: {
      webPageDetails: {
        viewName: "cart"
      }
    }
  }
});
```


>[!TAB Zweite Seitenansicht (Option 2)]

Wenn Sie den Seitenende-Treffer immer noch verzögern müssen, können Sie `applyPropositions` für den Seitenanfang verwenden. Da keine Personalisierung abgerufen werden muss und keine Analytics-Daten aufgezeichnet werden müssen, ist keine Anfrage an das Edge Network erforderlich.

```js
// top of page, render the decisions already fetched for the "cart" view.
alloy("applyPropositions", {
    viewName: "cart"
});

// bottom of page, send display events for the items that were rendered.
// Note: You need to include the viewName in both top and bottom of page so that the
// correct view is rendered at the top of the page, and the correct view is recorded
// at the bottom of the page.
alloy("sendEvent", {
    personalization: {
        includeRenderedPropositions: true
    },
    xdm: {
        ...,
        web: {
            webPageDetails: {
                viewName: "cart"
            }
        }
    }
});
```

>[!ENDTABS]

## GitHub-Beispiel {#github-sample}

Das Beispiel unter [diese Adresse](https://github.com/adobe/alloy-samples/tree/main/target/top-and-bottom) zeigt, wie Sie mit Experience Platform und Web SDK eine Personalisierung anfordern können, indem Sie oben auf der Seite klicken und unten Analysemetriken senden. Sie können das Beispiel herunterladen und lokal ausführen, um zu verstehen, wie die Ereignisse oben und unten auf der Seite funktionieren.
