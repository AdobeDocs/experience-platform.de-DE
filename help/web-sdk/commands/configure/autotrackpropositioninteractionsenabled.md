---
title: autoTrackPropositionInteractionsEnabled
description: Erfahren Sie, wie Sie Experience Platform Web SDK so konfigurieren, dass Linkdaten automatisch erfasst werden.
exl-id: c70db76a-3f2f-45a6-86ab-36efcb18d20f
source-git-commit: 11f3ccf494878dd8ee16bfc87a5cc901cc945b3e
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 1%

---

# `autoTrackPropositionInteractionsEnabled`

Die `autoTrackPropositionInteractionsEnabled`-Eigenschaft ist eine optionale Einstellung, die bestimmt, ob die Web-SDK automatisch Vorschlagsinteraktionen erfassen soll.

Der Wert ist eine Zuordnung von Entscheidungsanbietern mit jeweils einem -Wert, der angibt, wie automatische Vorschlagsinteraktionen verarbeitet werden sollen.

## Unterstützte Werte {#supported-values}

Standardmäßig werden automatische Vorschlagsinteraktionen (_)_ Adobe Journey Optimizer (`AJO`) und _nie)_ Adobe Target (`TGT`) erfasst.

Der Standardwert von `autoTrackPropositionInteractions` wird unten angezeigt.

```json
{
  "AJO": "always",
  "TGT": "never"
}
```

In der folgenden Tabelle finden Sie die unterstützten Konfigurationswerte für jeden Entscheidungsanbieter.

| Wert | Beschreibung |
| --- | --- |
| `always` | [!DNL Web SDK] erfasst immer automatisch `interact` Ereignisse für alle Elemente, die mit einem Vorschlag verbunden sind. |
| `never` | [!DNL Web SDK] werden nie automatisch `interact` Ereignisse für Elemente erfassen, die mit einem Vorschlag verbunden sind. |
| `decoratedElementsOnly` | [!DNL Web SDK] erfasst automatisch `interact` Ereignisse für Elemente, die mit einem Vorschlag verknüpft sind, jedoch nur, wenn das Element Datenattribute enthält, die eine Beschriftung oder ein Token angeben. |

## Automatisches Tracking der Vorschlagsinteraktionen {#logic}

Wenn Sie die automatische Interaktionsverfolgung für Vorschläge aktivieren, werden alle Klicks innerhalb eines Vorschlagselements, die im DOM gerendert werden, automatisch vom [!DNL Web SDK] erfasst. Dazu gehören alle Erlebnisse, die automatisch vom [!DNL Web SDK] im DOM gerendert werden, und Erlebnisse, die mit dem Befehl [`applyPropositions`](../applypropositions.md) im DOM gerendert werden.

### Datenattribute {#data-attributes}

Sie können Datenattribute für Elemente verwenden, um einer Interaktion Spezifität hinzuzufügen.

| Name | Datenattribut | Beschreibung |
| --- | --- | --- |
| [!DNL Label] | `data-aep-click-label` | Wenn das Datenattribut „Beschriftung“ für ein angeklicktes Element vorhanden ist, wird es in die Interaktionsdetails aufgenommen, die an das [!DNL Edge Network] gesendet werden. Die [!DNL Web SDK] sucht nach einem Beschriftungsdatenattribut, das mit dem Element beginnt, auf das geklickt wurde und in der DOM-Struktur nach oben navigiert. Die [!DNL Web SDK] verwendet die erste Kennzeichnung, die sie findet. |
| [!DNL Token] | `data-aep-click-token` | Verwenden Sie dieses Token bei der Nutzung von Entscheidungsrichtlinien in [Adobe Journey Optimizer-Code-basierten Kampagnen](https://experienceleague.adobe.com/de/docs/journey-optimizer/using/code-based-experience/get-started-code-based). Mit dem Token können Sie erkennen, auf welches Entscheidungsrichtlinienelement geklickt wurde. Wenn das Token-Datenattribut in einem angeklickten Element vorhanden ist, wird es in die Interaktionsdetails aufgenommen, die an das Edge Network gesendet werden. Die [!DNL Web SDK] sucht nach einem Token-Datenattribut, das mit dem Element beginnt, auf das geklickt wurde und zur DOM-Struktur hinaufgeht. Der [!DNL Web SDK] verwendet das erste Token, das er findet. |
| [!DNL Interact ID] | `data-aep-interact-id` | Der [!DNL Web SDK] fügt beim Rendern von Vorschlägen automatisch diese eindeutige ID zu Container-Elementen hinzu. Web SDK verwendet diese ID, um [!DNL DOM] Elemente mit Vorschlägen zu korrelieren. Da es sich um eine vom [!DNL Web SDK] benötigte ID handelt, sollten Sie sie in keiner Weise ändern. Sie können ihn ignorieren. |

**Beispiel**

Ein Beispiel für die Verwendung von Datenattributen finden Sie im folgenden Code-Snippet .

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

### Der `applyPropositions` Befehl {#apply-propositions}

Weitere Informationen zur Funktionsweise dieses Befehls finden Sie in der [`applyPropositions`](../applypropositions.md)-Dokumentation .

Der Befehl `applyPropositions` ist eine praktische Methode, Vorschläge für die [!DNL DOM] zu rendern. Im Fall von Code-basierten Kampagnen mit `JSON` können Sie diesen Befehl jedoch verwenden, um ein vorhandenes [!DNL DOM]-Element (oder das Element, das Ihr Programm-Code auf dem Bildschirm basierend auf den `JSON`-Werten gerendert hat) mit einem Vorschlag zu korrelieren.

Diese Korrelation aktiviert das automatische Interaktionstracking für dieses Element und weist diesem Element den entsprechenden Vorschlag zu. Legen Sie dazu die `actionType` auf `track` fest.

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

## Automatische Vorschläge und Interaktionen für das Klick-Tracking über die Tag-Erweiterung von Web SDK aktivieren {#tag-extension}

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
2. Navigieren Sie **Datenerfassung** > **Tags**.
3. Wählen Sie die gewünschte Tag-Eigenschaft aus.
4. Navigieren Sie zu **Erweiterungen** und wählen Sie dann **Konfigurieren** auf der Karte Adobe Experience Platform Web SDK aus.
5. Scrollen Sie nach unten zum Abschnitt **[!UICONTROL Datenerfassung]** und aktivieren Sie dann das Kontrollkästchen **Vorschläge und Interaktions-Linktracking aktivieren**.
6. Wählen **Speichern** und veröffentlichen Sie Ihre Änderungen.

## Aktivieren des Trackings von automatischen Vorschlägen und Interaktionen von Links über die Web SDK JavaScript-Bibliothek {#library}

Die Vorschlagsverfolgung ist in [!DNL Web SDK] standardmäßig aktiviert. Sie können ihn jedoch mithilfe des `autoTrackPropositionInteractionsEnabled`-Werts beim Ausführen des [`configure`](../configure/overview.md)-Befehls weiter konfigurieren.

Wenn Sie diese Eigenschaft beim Konfigurieren der Web-SDK auslassen, wird sie standardmäßig auf `{"AJO": "always", "TGT": "never"}` gesetzt. Wenn Sie es vorziehen, Vorschlagsinteraktionen nicht automatisch zu verfolgen, setzen Sie den Wert auf `{"AJO": "never", "TGT": "never"}`.

```javascript
alloy("configure", {
   "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
   "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
   "autoTrackPropositionInteractionsEnabled": {"AJO": "always", "TGT": "never"}
});
```
