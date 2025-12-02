---
title: autoCollectPropositionInteractions
description: Daten beim Klicken auf einen Link automatisch erfassen.
exl-id: c70db76a-3f2f-45a6-86ab-36efcb18d20f
source-git-commit: c2564f1b9ff036a49c9fa4b9e9ffbdbc598a07a8
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---

# `autoCollectPropositionInteractions`

Die `autoCollectPropositionInteractions`-Eigenschaft ist eine optionale Einstellung, die bestimmt, ob die Web-SDK automatisch Vorschlagsinteraktionen erfasst. Der Wert ist eine Zuordnung von Entscheidungsanbietern mit jeweils einem -Wert, der angibt, wie automatische Vorschlagsinteraktionen verarbeitet werden sollen.

Wenn Sie die automatische Interaktionsverfolgung für Vorschläge aktivieren, werden alle Klicks innerhalb eines Vorschlagselements, die im DOM gerendert werden, automatisch vom Web-SDK erfasst. Diese Sammlung enthält alle Erlebnisse, die automatisch vom Web-SDK für das DOM gerendert werden, sowie Erlebnisse, die mithilfe des [`applyPropositions`](../applypropositions.md)-Befehls für das DOM gerendert werden.

Wenn Sie diese Eigenschaft beim Konfigurieren der Web-SDK auslassen, wird sie standardmäßig auf `{"AJO": "always", "TGT": "never"}` gesetzt. Wenn Sie es vorziehen, Vorschlagsinteraktionen nicht automatisch zu verfolgen, setzen Sie den Wert auf `{"AJO": "never", "TGT": "never"}`.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "autoCollectPropositionInteractions": {
    "AJO": "always",
    "TGT": "never"
  }
});
```

Zu den unterstützten Eigenschaften in diesem Objekt gehören:

| Eigenschaft | Beschreibung |
| --- | --- |
| **`AJO`** | Adobe Journey Optimizer. |
| **`TGT`** | Adobe Target. |

Zu den möglichen Werten für jede Eigenschaft gehören:

| Wert | Beschreibung |
| --- | --- |
| **`always`** | Sammeln Sie immer automatisch `interact` Ereignisse für alle Elemente, die mit einem Vorschlag verbunden sind. |
| **`never`** | Nie automatisch `interact` Ereignisse für Elemente erfassen, die mit einem Vorschlag verbunden sind. |
| **`decoratedElementsOnly`** | Sammelt automatisch `interact` Ereignisse für Elemente, die mit einem Vorschlag verknüpft sind, wenn das Element Datenattribute enthält, die eine Beschriftung oder ein Token angeben. |

## Datenattribute {#data-attributes}

Sie können Datenattribute für Elemente verwenden, um einer Interaktion Spezifität hinzuzufügen.

| Name | Datenattribut | Beschreibung |
| --- | --- | --- |
| **[!UICONTROL Label]** | `data-aep-click-label` | Wenn das Datenattribut „Beschriftung“ für ein angeklicktes Element vorhanden ist, wird es in die Interaktionsdetails aufgenommen, die an die Edge Network gesendet werden. Web SDK sucht nach einem Beschriftungsdatenattribut, das mit dem Element beginnt, auf das geklickt wurde und in der DOM-Struktur nach oben navigiert. Die Web-SDK verwendet die erste Kennzeichnung, die sie findet. |
| **[!UICONTROL Token]** | `data-aep-click-token` | Verwenden Sie dieses Token bei der Nutzung von Entscheidungsrichtlinien in [Adobe Journey Optimizer-Code-basierten Kampagnen](https://experienceleague.adobe.com/de/docs/journey-optimizer/using/code-based-experience/get-started-code-based). Mit dem Token können Sie erkennen, auf welches Entscheidungsrichtlinienelement geklickt wurde. Wenn das Token-Datenattribut in einem angeklickten Element vorhanden ist, wird es in die Interaktionsdetails aufgenommen, die an die Edge Network gesendet werden. Web SDK sucht nach einem Token-Datenattribut, das mit dem Element beginnt, auf das geklickt wurde und von der DOM-Baumstruktur nach oben navigiert wird. Die Web-SDK verwendet das erste Token, das sie findet. |
| **[!UICONTROL Interact ID]** | `data-aep-interact-id` | Web SDK fügt diese eindeutige ID beim Rendern von Vorschlägen automatisch zu Container-Elementen hinzu. Web SDK verwendet diese ID, um DOM-Elemente mit Vorschlägen zu korrelieren. Da es sich um eine für die Web-SDK erforderliche ID handelt, sollten Sie sie in keiner Weise ändern. Sie können ihn ignorieren. |

## Beispiel

```html
<div class="row movies" data-aep-interact-id="5">
  <div class="col-md-4 movie" data-aep-click-token="wlpk/z/qyDGoFGF1E47O0w">
    <img src="/img/alpha.jpg" class="poster" />
    <h2>Example Movie Alpha</h2>
    <p class="description"> A lighthearted story about exploration and friendship set on a distant world. Follow a curious rover who discovers that small actions can lead to big changes.</p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Example-Alpha">View details</button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="6ZUrou9BVKIsINIAqxylzw">
    <img src="/img/bravo.jpg" class="poster" />
    <h2>Example Movie Bravo</h2>
    <p class="description">An uplifting tale of a determined chef who overcomes unlikely odds to create culinary masterpieces in a bustling city bistro.</p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Example-Bravo">View details</button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="QuuXntMRGnCP/AsZHf4pnQ">
    <img src="/img/charlie.jpg" class="poster" />
    <h2>Example Movie Charlie</h2>
    <p class="description">A vibrant adventure following a young musician who journeys into a fantastical realm to find the true meaning of family and tradition.</p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Example-Charlie">View details</button>
    </p>
  </div>
</div>
```

### Verwenden von `autoCollectPropositionInteractions` mit dem Befehl `applyPropositions` {#apply-propositions}

Der Befehl [`applyPropositions`](../applypropositions.md) ist eine praktische Methode, Vorschläge für das DOM zu rendern. Im Fall von Code-basierten Kampagnen mit JSON können Sie diesen Befehl jedoch verwenden, um ein vorhandenes DOM-Element (oder das Element, das Ihr Programm-Code auf dem Bildschirm basierend auf den JSON-Werten gerendert hat) mit einem Vorschlag zu korrelieren.

Diese Korrelation aktiviert das automatische Interaktionstracking für dieses Element und weist diesem Element den entsprechenden Vorschlag zu. Legen Sie dazu die `actionType` auf `track` fest.

```javascript
alloy("sendEvent", {
    renderDecisions: true,
}).then((result) => {
    const {
        propositions = []
    } = result;
    const proposition = propositions.find(
        (proposition) => proposition.scope === "web://example.com/#weather-widget"
    );

    if (proposition) {
        renderWeatherWidget(proposition); // custom code that renders the weather widget based on the code-based campaign JSON

        alloy("applyPropositions", {
            propositions: [proposition],
            metadata: {
                "web://example.com/#weather-widget": {
                    selector: "#weather-widget",
                    actionType: "track",
                },
            },
        });
    }
});
```

## Konfigurieren von automatischen Vorschlagsinteraktionen für die Web SDK-Tag-Erweiterung

Die folgenden beiden Dropdown-Menüs bei der Konfiguration der Web-SDK-Tag-Erweiterung entsprechen diesem Objekt:

* [[!UICONTROL Auto click collection for Adobe Journey Optimizer]](/help/tags/extensions/client/web-sdk/configure/personalization.md#auto-click-collection-for-adobe-journey-optimizer)
* [[!UICONTROL Auto click collection for Adobe Target]](/help/tags/extensions/client/web-sdk/configure/personalization.md#auto-click-collection-for-adobe-target)
