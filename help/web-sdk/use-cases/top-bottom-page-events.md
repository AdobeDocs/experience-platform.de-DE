---
title: Konfigurieren von Ereignissen am Anfang und Ende der Seite im Web SDK
description: In diesem Artikel wird erläutert, wie Sie die Seitenereignisse oben und unten im Web SDK verwenden.
exl-id: 43c6d53a-6bf9-45f8-b001-d148adaff829
source-git-commit: 4d0895c6ad38523f5527c9630931c3c0b8ef83c0
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 2%

---


# Konfigurieren von Ereignissen am Anfang und Ende der Seite im Web SDK

Wenn Sie Ihren Kunden personalisierte Erlebnisse bereitstellen möchten, ist die Ladezeit einer Webseite von entscheidender Bedeutung.

Um die Ladezeiten zu optimieren und die Personalisierung so schnell wie möglich bereitzustellen, unterstützt das Web SDK die Konfiguration der oberen und unteren Seitenereignisse.

Oben und unten von Seitenereignissen beschreiben die Methode zum asynchronen Laden verschiedener Elemente auf der Seite, wobei die Seitenladezeit auf ein Minimum beschränkt bleibt.

Diese Konfiguration minimiert die Wartezeit, die ein Benutzer hat, bis der personalisierte Inhalt geladen ist.

Hinsichtlich der Genauigkeit von Metriken kann Adobe Analytics den Anfang von Seitenereignissen ignorieren, was zu einer präziseren Metrikaufzeichnung führt, da nur ein Seitentreffer aufgezeichnet wird (am Ende des Seitenereignisses).

## Anwendungsfälle {#use-cases}

Ein Sportbekleidungshändler möchte seinen Käufern personalisierte Erlebnisse bieten und dabei gleichzeitig die Benutzerspannungen beim Besuch seiner Website minimieren, während er gleichzeitig in der Lage ist, genaue Besuchermetriken zu erfassen.

Durch die Verwendung der Ereignisse oben und unten auf der Seite im Web SDK kann das Marketing-Team den Personalisierungsversand optimal konfigurieren:

* Das Web SDK sendet eine Personalisierungsanfrage, die geladen wird, sobald die Seite geladen wird. Dies ist der Anfang des Seitenereignisses.
* Wenn das Laden der Seite abgeschlossen ist, wird ein Seitenansichtsereignis aufgezeichnet. Dies geschieht später im Seitenladeprozess. Dies ist das Ende des Seitenereignisses.

## Beispiel für Seitenereignis oben {#top-of-page}

Im folgenden Codebeispiel wird ein Anfang der Seitenereigniskonfiguration veranschaulicht, die eine Personalisierung anfordert, aber für automatisch gerenderte Vorschläge keine [Anzeigeereignisse senden](../personalization/display-events.md#send-sendEvent-calls) sendet. Die [Anzeigeereignisse](../personalization/display-events.md#send-sendEvent-calls) werden als Teil des Seitenende-Ereignisses gesendet.

>[!BEGINTABS]

>[!TAB Anfang des Seitenereignisses]

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
| `type` | Erforderlich | Setzen Sie diesen Parameter auf `decisioning.propositionFetch`. Dieser Ereignistyp weist Adobe Analytics an, dieses Ereignis abzulegen. Bei Verwendung von Customer Journey Analytics können Sie auch einen Filter einrichten, um diese Ereignisse abzulegen. |
| `renderDecisions` | Erforderlich | Setzen Sie diesen Parameter auf `true`. Dieser Parameter weist das Web SDK an, vom Edge Network zurückgegebene Entscheidungen zu rendern. |
| `personalization.sendDisplayEvent` | Erforderlich | Setzen Sie diesen Parameter auf `false`. Dadurch wird das Senden von Ereignissen verhindert. |

>[!ENDTABS]

## Beispiele für Seitenereignisse am Ende {#bottom-of-page}

>[!BEGINTABS]

>[!TAB Automatisch gerenderte Vorschläge]

Das folgende Codebeispiel veranschaulicht den unteren Rand der Seitenereigniskonfiguration, der Anzeigeereignisse für Vorschläge sendet, die automatisch auf der Seite gerendert wurden, für die jedoch Anzeigeereignisse am Anfang des Ereignisses [Seite](#top-of-page) unterdrückt wurden.

>[!NOTE]
>
>In diesem Szenario müssen Sie das Ende des Seitenereignisses _nach_ am Anfang des ersten Seitenereignisses aufrufen. Das Ende des Seitenereignisses muss jedoch nicht warten, bis der Anfang der ersten Seite abgeschlossen ist.

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
| `personalization.includeRenderedPropositions` | Erforderlich | Setzen Sie diesen Parameter auf `true`. Dies ermöglicht das Senden von Anzeigeereignissen, die oben im Seitenereignis unterdrückt wurden. |
| `xdm` | Optional | Verwenden Sie diesen Abschnitt, um alle Daten einzuschließen, die Sie für das Ende des Seitenereignisses benötigen. |

>[!TAB Manuell gerenderte Vorschläge]

Das folgende Codebeispiel veranschaulicht den unteren Rand der Seitenereigniskonfiguration, der Anzeigeereignisse für Vorschläge sendet, die manuell auf der Seite gerendert wurden (d. h. für benutzerdefinierte Entscheidungsbereiche oder Oberflächen).

>[!NOTE]
>
>In diesem Szenario muss das Ende des Seitenereignisses warten, bis der Anfang des Seitenereignisses abgeschlossen ist, um die Vorschläge zu rendern und das Ende des Seitenereignisses aufzuzeichnen.

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
| `xdm._experience.decisioning.propositions` | Erforderlich | In diesem Abschnitt werden die manuell gerenderten Vorschläge definiert. Sie müssen die Vorschläge `ID`, `scope` und `scopeDetails` einbeziehen. Weitere Informationen zum Aufzeichnen von Anzeigeereignissen für manuell gerenderte Inhalte finden Sie in der Dokumentation zum manuellen Rendern der Personalisierung [ . ](../personalization/rendering-personalization-content.md#manually) Manuell gerenderte Personalisierungsinhalte müssen am Ende des Seitenaufrufs enthalten sein. |
| `xdm._experience.decisioning.propositionEventType` | Erforderlich | Setzen Sie diesen Parameter auf `display: 1`. |
| `xdm` | Optional | Verwenden Sie diesen Abschnitt, um alle Daten einzuschließen, die Sie für das Ende des Seitenereignisses benötigen. |

>[!ENDTABS]


## Einzelseitenanwendung mit Treffern auf der oberen und unteren Seite {#spa-example}


>[!BEGINTABS]

>[!TAB Erste Seitenansicht]

Im folgenden Beispiel wird der erforderliche Parameter `xdm.web.webPageDetails.viewName` hinzugefügt. Dies macht es zu einer einseitigen Anwendung. Die `viewName` in diesem Beispiel ist die Ansicht, die beim Laden der Seite geladen wird.

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

In diesem Beispiel ist es nicht erforderlich, die Seitentrennung oben/unten vorzunehmen, da die Personalisierung für die Seite bereits abgerufen wurde.

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

Wenn Sie den unteren Seitenaufruf weiterhin verzögern müssen, können Sie für den oberen Seitenaufruf den Wert &quot;`applyPropositions`&quot;verwenden. Da keine Personalisierung abgerufen werden muss und keine Analytics-Daten aufgezeichnet werden müssen, ist es nicht erforderlich, eine Anfrage an das Edge Network zu richten.

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

Das Beispiel unter [dieser Adresse](https://github.com/adobe/alloy-samples/tree/main/target/top-and-bottom) zeigt, wie Experience Platform und Web SDK verwendet werden, um eine Personalisierung am oberen Seitenrand anzufordern und Analytics-Metriken am unteren Seitenrand zu senden. Sie können das Beispiel herunterladen und lokal ausführen, um zu verstehen, wie oben und unten von Seitenereignissen funktionieren.
