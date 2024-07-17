---
title: autoTrackPropositionInteractionsEnabled
description: Erfahren Sie, wie Sie das Experience Platform Web SDK so konfigurieren, dass es automatisch Linkdaten erfasst.
source-git-commit: ec5fd1c8228388ced96f58476e0174c8a0ff00df
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 1%

---


# `autoTrackPropositionInteractionsEnabled`

Die Eigenschaft `autoTrackPropositionInteractionsEnabled` ist eine optionale Einstellung, die bestimmt, ob das Web SDK automatisch Vorschlagsinteraktionen erfassen soll.

Der Wert ist eine Zuordnung von Entscheidungsträgern, von denen jeder einen Wert enthält, der angibt, wie automatische Vorschlagsinteraktionen verarbeitet werden sollen.

## Unterstützte Werte {#supported-values}

Standardmäßig werden bei automatischen Vorschlagsinteraktionen _immer_ für Adobe Journey Optimizer (`AJO`) und _nie_ für Adobe Target (`TGT`) erfasst.

Der Standardwert `autoTrackPropositionInteractions` ist unten dargestellt.

```json
{
  "AJO": "always",
  "TGT": "never"
}
```

Die unterstützten Konfigurationswerte für die einzelnen Entscheidungsanbieter finden Sie in der folgenden Tabelle.

| Wert | Beschreibung |
| --- | --- |
| `always` | [!DNL Web SDK] erfasst immer automatisch `interact`-Ereignisse für alle Elemente, die mit einem Vorschlag verknüpft sind. |
| `never` | [!DNL Web SDK] erfasst nie automatisch `interact`-Ereignisse für Elemente, die mit einem Vorschlag verknüpft sind. |
| `decoratedElementsOnly` | [!DNL Web SDK] erfasst automatisch `interact` -Ereignisse für Elemente, die mit einem Vorschlag verknüpft sind, jedoch nur, wenn das Element Datenattribute enthält, die eine Bezeichnung oder ein Token angeben. |

## Automatisches Angebotsinteraktions-Tracking {#logic}

Wenn Sie die automatische Verfolgung von Vorschlagsinteraktionen aktivieren, werden alle Klicks innerhalb eines Vorschlagselements, die in das DOM gerendert werden, automatisch von [!DNL Web SDK] erfasst. Dazu gehören alle Erlebnisse, die automatisch von [!DNL Web SDK] an das DOM gerendert werden, und Erlebnisse, die mit dem Befehl [`applyPropositions`](../applypropositions.md) an das DOM gerendert werden.

### Datenattribute {#data-attributes}

Sie können Datenattribute für Elemente verwenden, um einer Interaktion eine Spezifität hinzuzufügen.

| Name | Datenattribut | Beschreibung |
| --- | --- | --- |
| [!DNL Label] | `data-aep-click-label` | Wenn das Datenattribut &quot;Titel&quot;in einem angeklickten Element vorhanden ist, wird es mit den an die [!DNL Edge Network] gesendeten Interaktionsdetails einbezogen. Der [!DNL Web SDK] sucht nach einem Beschriftungsdatenattribut, das mit dem angeklickten Element und dem Aufstieg der DOM-Struktur beginnt. Der [!DNL Web SDK] verwendet die erste Bezeichnung, die er findet. |
| [!DNL Token] | `data-aep-click-token` | Verwenden Sie dieses Token bei der Nutzung von Entscheidungsrichtlinien in [code-basierten Adobe Journey Optimizer-Kampagnen](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/code-based-experience/get-started-code-based). Mit dem Token können Sie ermitteln, auf welches Entscheidungsrichtlinienelement geklickt wurde. Wenn das Token-Datenattribut in einem angeklickten Element vorhanden ist, wird es mit den an das Edge Network gesendeten Interaktionsdetails einbezogen. Der [!DNL Web SDK] sucht nach einem Token-Datenattribut, das mit dem angeklickten Element und dem Aufstieg der DOM-Struktur beginnt. Der [!DNL Web SDK] verwendet das erste Token, das er findet. |
| [!DNL Interact ID] | `data-aep-interact-id` | Der [!DNL Web SDK] fügt diese eindeutige ID beim Rendern von Vorschlägen automatisch zu Containerelementen hinzu. Das Web SDK verwendet diese ID, um [!DNL DOM] -Elemente mit Vorschlägen zu korrelieren. Da dies eine für [!DNL Web SDK] erforderliche ID ist, sollten Sie sie in keiner Weise ändern. Du kannst es ignorieren. |

**Beispiel**

Ein Beispiel für die Verwendung von Datenattributen finden Sie im folgenden Codefragment.

```html
<div class="row movies" data-aep-interact-id="5">
  <div class="col-md-4 movie" data-aep-click-token="wlpk/z/qyDGoFGF1E47O0w">
    <img src="/img/walle.jpg" class="poster" />
    <h2>WALL·E</h2>
    <p class="description"> In a distant, but not so unrealistic, future where mankind has abandoned earth because it has become covered with trash from products sold by the powerful multi-national Buy N Large corporation, WALL-E, a garbage collecting robot has been left to clean up the mess. </p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-WALL·E"> View details >> </button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="6ZUrou9BVKIsINIAqxylzw">
    <img src="/img/ratatouille.jpg" class="poster" />
    <h2>Ratatouille</h2>
    <p class="description"> A rat named Remy dreams of becoming a great French chef despite his family's wishes and the obvious problem of being a rat in a decidedly rodent-phobic profession. When fate places Remy in the sewers of Paris, he finds himself ideally situated beneath a restaurant made famous by his culinary hero, Auguste Gusteau. </p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Ratatouille"> View details >> </button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="QuuXntMRGnCP/AsZHf4pnQ">
    <img src="/img/coco.jpg" class="poster" />
    <h2>Coco</h2>
    <p class="description"> Despite his family's baffling generations-old ban on music, Miguel dreams of becoming an accomplished musician like his idol, Ernesto de la Cruz. Desperate to prove his talent, Miguel finds himself in the stunning and colorful Land of the Dead following a mysterious chain of events. </p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Coco"> View details >> </button>
    </p>
  </div>
</div>
```

### Der Befehl `applyPropositions` {#apply-propositions}

Informationen zur Funktionsweise dieses Befehls finden Sie in der Dokumentation zu [`applyPropositions`](../applypropositions.md) .

Der Befehl `applyPropositions` ist eine praktische Methode, Vorschläge für die [!DNL DOM] zu rendern. Im Fall von code-basierten Kampagnen mit `JSON` können Sie diesen Befehl jedoch verwenden, um ein vorhandenes [!DNL DOM] -Element (oder das Element, das Ihr Anwendungscode basierend auf den `JSON` -Werten wiedergegeben hat) mit einem Vorschlag zu korrelieren.

Diese Korrelation aktiviert das automatische Interaktionstracking für dieses Element und weist diesem Element den entsprechenden Vorschlag zu. Setzen Sie dazu die `actionType` auf `track`.

**Beispiel**

```javascript
alloy("sendEvent", {
    renderDecisions: true,
}).then((result) => {
    const {
        propositions = []
    } = result;
    const proposition = propositions.find(
        (proposition) => proposition.scope === "web://mywebsite.com/#weather-widget"
    );

    if (proposition) {
        renderWeatherWidget(proposition); // custom code that renders the weather widget based on the code-based campaign JSON

        alloy("applyPropositions", {
            propositions: [proposition],
            metadata: {
                "web://mywebsite.com/#weather-widget": {
                    selector: "#weather-widget",
                    actionType: "track",
                },
            },
        });
    }
});
```

## Automatische Vorschläge und Interaktionen zum Klick-Tracking über die Web SDK-Tag-Erweiterung aktivieren {#tag-extension}

1. Melden Sie sich mit Ihren Adobe ID-Anmeldedaten bei [experience.adobe.com](https://experience.adobe.com) an.
2. Navigieren Sie zu **Datenerfassung** > **Tags**.
3. Wählen Sie die gewünschte Tag-Eigenschaft aus.
4. Navigieren Sie zu **Erweiterungen** und wählen Sie auf der Adobe Experience Platform Web SDK-Karte **Konfigurieren** aus.
5. Scrollen Sie nach unten zum Abschnitt **[!UICONTROL Datenerfassung]** und aktivieren Sie dann das Kontrollkästchen **Vorschläge und Linktracking der Interaktionen aktivieren**.
6. Wählen Sie **Speichern** aus und veröffentlichen Sie dann Ihre Änderungen.

## Automatisches Link-Tracking von Vorschlägen und Interaktionen über die Web SDK JavaScript-Bibliothek aktivieren {#library}

Das Tracking von Vorschlägen ist standardmäßig in [!DNL Web SDK] aktiviert. Sie können sie jedoch mit dem Wert `autoTrackPropositionInteractionsEnabled` weiter konfigurieren, wenn Sie den Befehl [`configure`](../configure/overview.md) ausführen.

Wenn Sie diese Eigenschaft beim Konfigurieren des Web SDK weglassen, wird standardmäßig `{"AJO": "always", "TGT": "never"}` verwendet. Wenn Sie es vorziehen, die Interaktionen mit Vorschlägen nicht automatisch zu verfolgen, setzen Sie den Wert auf `{"AJO": "never", "TGT": "never"}`.

```javascript
alloy("configure", {
   "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
   "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
   "autoTrackPropositionInteractionsEnabled": {"AJO": "always", "TGT": "never"}
});
```
