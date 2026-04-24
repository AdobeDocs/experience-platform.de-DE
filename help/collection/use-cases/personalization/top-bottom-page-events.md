---
title: Konfigurieren der Seitenansichten oben und unten in Web SDK
description: In diesem Artikel wird erläutert, wie in Web SDK Seitenereignisse am Anfang und Ende verwendet werden.
exl-id: 43c6d53a-6bf9-45f8-b001-d148adaff829
source-git-commit: 8058ee470717b95d30269a8072b12385c920c85f
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 1%

---


# Konfigurieren der Seitenansichten oben und unten in Web SDK

Bei der Bereitstellung personalisierter Erlebnisse ist die Ladezeit einer Web-Seite von entscheidender Bedeutung. Um die Zeit zu minimieren, die Benutzende auf personalisierte Inhalte warten, unterstützt Web SDK die Konfiguration von Top- und Bottom-of-Page-Ereignissen.

Die Ereignisse oben und unten auf der Seite beschreiben eine Methode zum asynchronen Laden verschiedener Elemente auf der Seite, wobei die Ladezeit der Seite auf ein Minimum beschränkt bleibt:

* Das Ereignis „Seitenanfang“ fordert die Personalisierung an, sobald die Seite geladen wird.
* Das Ereignis „Unten auf der Seite“ zeichnet eine Seitenansicht auf, wenn das Laden der Seite abgeschlossen ist.

Adobe Analytics ignoriert die Top-of-Page-Ereignisse, was zu einer genaueren Metrikaufzeichnung führt, da nur ein Seitentreffer aufgezeichnet wird (das untere Seitenereignis).

Sie können die oberen und unteren Ränder von Seitenereignissen auf zwei Arten konfigurieren: indem Sie die Web-SDK-JavaScript-Bibliothek (`alloy()`) direkt aufrufen, oder indem Sie die Web-SDK-Tag-Erweiterung in der Adobe Experience Platform Tags-Benutzeroberfläche verwenden. Die [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md)-Aktion der Tag-Erweiterung enthält eine Option &quot;[!UICONTROL Use guided events]&quot;, mit der Feldwerte für die Szenarien &quot;[!UICONTROL Request personalization]&quot; (Seitenanfang) und &quot;[!UICONTROL Collect analytics]&quot; (Seitenende) vorkonfiguriert werden. Jedes der folgenden Beispiele zeigt beide Implementierungen.

## Ereignis „Anfang der Seite“ {#top-of-page}

Im folgenden Beispiel wird ein Ereignis „Seitenanfang“ konfiguriert, das die Personalisierung anfordert, aber [Anzeigeereignisse](display-events.md) für automatisch gerenderte Vorschläge unterdrückt. Diese Anzeigeereignisse werden stattdessen mit dem Ereignis „Seitenende“ gesendet.

>[!BEGINTABS]

>[!TAB JavaScript-Bibliothek]

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
| --- | --- | --- |
| `type` | Erforderlich | Legen Sie diesen Parameter auf `decisioning.propositionFetch` fest. Dieser spezielle Ereignistyp weist Adobe Analytics an, dieses Ereignis zu ignorieren. Bei Verwendung von Customer Journey Analytics können Sie auch einen Filter einrichten, um diese Ereignisse zu löschen. Weitere Informationen finden Sie unter [Ereignistypen für Edge Network ](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/hit-types) Adobe Analytics. |
| `renderDecisions` | Erforderlich | Legen Sie diesen Parameter auf `true` fest. Dieser Parameter weist Web SDK an, von Edge Network zurückgegebene Entscheidungen zu rendern. |
| `personalization.sendDisplayEvent` | Erforderlich | Legen Sie diesen Parameter auf `false` fest. Dieser Parameter verhindert das Senden von Anzeigeereignissen. |

>[!TAB Web SDK-Tag-Erweiterung]

Konfigurieren Sie eine [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) Aktion in der Regel, die oben auf der Seite ausgelöst wird. Aktivieren Sie **[!UICONTROL Use guided events]** und wählen Sie dann **[!UICONTROL Request personalization]** aus. Diese Option sperrt &quot;[!UICONTROL Type]&quot; auf &quot;[!UICONTROL Decisioning Proposition Fetch]&quot;, &quot;[!UICONTROL Render visual personalization decisions]&quot; auf „aktiviert“ und &quot;[!UICONTROL Automatically send a display event]&quot; auf „deaktiviert“.

Wenn Sie diese Felder stattdessen manuell festlegen möchten, lassen Sie **[!UICONTROL Use guided events]** deaktiviert und konfigurieren Sie jedes Feld selbst.

>[!ENDTABS]

## Ereignisbeispiele unten auf der Seite {#bottom-of-page}

### Automatisch gerenderte Vorschläge {#bottom-auto-rendered}

Im folgenden Beispiel wird ein Ereignis „Seitenende“ konfiguriert, das Anzeigeereignisse für Vorschläge sendet, die automatisch auf der Seite gerendert, aber im Ereignis &quot;[ der Seite“ ](#top-of-page) wurden.

>[!BEGINTABS]

>[!TAB JavaScript-Bibliothek]

```js
alloy("sendEvent", {
  personalization: {
    includeRenderedPropositions: true
  },
  xdm: { ... }
});
```

| Parameter | Erforderlich/Optional | Beschreibung |
| --- | --- | --- |
| `personalization.includeRenderedPropositions` | Erforderlich | Legen Sie diesen Parameter auf `true` fest. Dieser Parameter ermöglicht das Senden von Anzeigeereignissen, die oben auf der Seite unterdrückt wurden. |
| `xdm` | Optional | Verwenden Sie dieses Objekt, um alle Daten einzuschließen, die Sie für das Ereignis „Seitenende“ benötigen. |

>[!TAB Web SDK-Tag-Erweiterung]

Konfigurieren Sie eine [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) Aktion in der Regel, die am unteren Rand der Seite ausgelöst wird. Aktivieren Sie **[!UICONTROL Use guided events]** und wählen Sie dann **[!UICONTROL Collect analytics]** aus. Diese Option sperrt &quot;[!UICONTROL Include rendered propositions]&quot; auf „Aktiviert“.

Wenn Sie dieses Feld stattdessen manuell festlegen möchten, lassen Sie **[!UICONTROL Use guided events]** deaktiviert und aktivieren Sie **[!UICONTROL Include rendered propositions]** direkt. Füllen Sie optional das **[!UICONTROL XDM]** mit einem Datenelement [XDM-Objekt](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object), das Ihre Seitendaten enthält.

>[!ENDTABS]

### Manuell gerenderte Vorschläge {#bottom-manually-rendered}

Im folgenden Beispiel wird ein Ereignis „Seitenende“ konfiguriert, das Anzeigeereignisse für Vorschläge sendet, die auf der Seite manuell gerendert wurden (d. h. für benutzerdefinierte Entscheidungsumfänge oder Oberflächen).

>[!NOTE]
>
>In diesem Szenario muss das Ereignis „Seitenende“ warten, bis das Ereignis „Seitenanfang“ abgeschlossen ist, damit die Vorschläge gerendert und aufgezeichnet werden können.

>[!BEGINTABS]

>[!TAB JavaScript-Bibliothek]

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
| --- | --- | --- |
| `xdm._experience.decisioning.propositions` | Erforderlich | In diesem Abschnitt werden die manuell gerenderten Vorschläge definiert. Sie müssen die `id`, `scope` und `scopeDetails` der Vorschläge einbeziehen. Weitere Informationen [ Sie unter ](display-events.md) von Anzeigeereignissen . Manuell gerenderte Personalisierungsinhalte müssen im Ereignis „Seitenende“ enthalten sein. |
| `xdm._experience.decisioning.propositionEventType` | Erforderlich | Legen Sie diesen Parameter auf `display: 1` fest. |
| `xdm` | Optional | Verwenden Sie dieses Objekt, um alle Daten einzuschließen, die Sie für das Ereignis „Seitenende“ benötigen. |

>[!TAB Web SDK-Tag-Erweiterung]

Die Option &quot;[!UICONTROL Use guided events]&quot; deckt dieses Szenario nicht ab. Konfigurieren Sie die Aktion daher manuell:

1. Erstellen Sie ein [XDM](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object)-Datenelement (oder [Variable](/help/tags/extensions/client/web-sdk/data-element-types.md#variable)), das `_experience.decisioning.propositions` mit den `id`, `scope` und `scopeDetails` jedes gerenderten Vorschlags füllt und `_experience.decisioning.propositionEventType.display` auf `1` setzt. Weitere Informationen [ Sie unter ](display-events.md) von Anzeigeereignissen .
1. Lassen Sie in der [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) für die Regel „Seitenende“ **[!UICONTROL Use guided events]** deaktiviert und verweisen Sie auf das Datenelement im Feld &quot;**[!UICONTROL XDM]**&quot;.

>[!ENDTABS]

## Einzelseitenanwendung mit Ereignissen der oberen und unteren Seite {#spa-example}

In einem Einzelseitenprogramm müssen Sie bei jeder Ansichtsänderung den Ansichtsnamen angeben, damit Web SDK die richtige Personalisierung am Seitenanfang rendert und die richtige Ansicht am Seitenende aufzeichnet.

### Erste Seitenansicht {#spa-first-view}

In diesem Beispiel ist `home` die Ansicht, die beim ersten Laden der Seite geladen wurde.

>[!BEGINTABS]

>[!TAB JavaScript-Bibliothek]

Der Top-Aufruf fordert eine Personalisierung für die `home`-Ansicht an, ohne einen Analytics-Treffer aufzuzeichnen oder Anzeigeereignisse auszulösen. Der Aufruf unten zeichnet die Seitenansicht auf und löst die unterdrückten Anzeigeereignisse aus. Nehmen Sie in beide Aufrufe denselben `viewName` auf, damit die Ansicht konsistent aufgezeichnet wird.

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

>[!TAB Web SDK-Tag-Erweiterung]

1. Erstellen Sie ein [XDM-Objekt](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object)-Datenelement, das den Namen der Ansicht `web.webPageDetails.viewName` (z. B. `home`).
1. Konfigurieren einer Aktion des Typs Seitenanfang [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) : Aktivieren Sie **[!UICONTROL Use guided events]**, wählen Sie **[!UICONTROL Request personalization]** aus und verweisen Sie auf das Datenelement im Feld **[!UICONTROL XDM]** .
1. Konfigurieren einer **[!UICONTROL Send event]**-Aktion für das Ende der Seite: Aktivieren Sie **[!UICONTROL Use guided events]**, wählen Sie **[!UICONTROL Collect analytics]** aus und verweisen Sie im **[!UICONTROL XDM]** auf dasselbe Datenelement, sodass die `viewName` in beiden Ereignissen übereinstimmt.

>[!ENDTABS]

### Zweite Seitenansicht — Option 1 {#spa-second-view-option-1}

In diesem Beispiel ist ein einzelnes Ereignis ausreichend, da die Personalisierung für die Seite bereits abgerufen wurde.

>[!BEGINTABS]

>[!TAB JavaScript-Bibliothek]

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

>[!TAB Web SDK-Tag-Erweiterung]

1. Erstellen Sie ein [XDM-Objekt](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object)-Datenelement, das den Namen der neuen Ansicht `web.webPageDetails.viewName` (z. B. `cart`).
1. Konfigurieren Sie bei der Änderung der Ansicht eine einzelne [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md): Lassen Sie **[!UICONTROL Use guided events]** deaktiviert, aktivieren Sie **[!UICONTROL Render visual personalization decisions]** und verweisen Sie auf das Datenelement im **[!UICONTROL XDM]**.

>[!ENDTABS]

### Zweite Seitenansicht — Option 2 {#spa-second-view-option-2}

Verwenden Sie diesen Ansatz, wenn Sie das Ereignis „Ende der Seite“ verzögern müssen (z. B. wenn die Analysedaten der Seite zum Zeitpunkt der Änderung der Ansicht nicht bereit sind). Die Änderung der Ansicht wird in zwei Schritten vorgenommen:

1. Rendern Sie oben auf der Seite die bereits abgerufenen Vorschläge, ohne einen Edge Network-Aufruf durchzuführen.
1. Sobald die Analysedaten bereit sind, senden Sie das Ereignis „Seitenende“.

Nehmen Sie in beide Aufrufe denselben `viewName` auf, damit die Ansicht konsistent aufgezeichnet wird.

>[!BEGINTABS]

>[!TAB JavaScript-Bibliothek]

Rufen Sie [`applyPropositions`](/help/collection/js/commands/applypropositions.md) oben auf der Seite auf, um die zwischengespeicherten Vorschläge für die neue Ansicht zu rendern. Rufen Sie dann `sendEvent` am unteren Rand der Seite mit `includeRenderedPropositions: true` auf, damit die unterdrückten Anzeigeereignisse ausgelöst werden.

```js
// Top of page, render the decisions already fetched for the "cart" view.
alloy("applyPropositions", {
    viewName: "cart"
});

// Bottom of page, send display events for the items that were rendered.
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

>[!TAB Web SDK-Tag-Erweiterung]

1. Erstellen Sie ein [XDM-Objekt](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object)-Datenelement, das den Namen der neuen Ansicht `web.webPageDetails.viewName` (z. B. `cart`).
1. Konfigurieren Sie für das Ereignis „Anfang der Seite“ eine [[!UICONTROL Apply propositions]](/help/tags/extensions/client/web-sdk/actions/apply-propositions.md) Aktion und legen Sie für das Feld &quot;**[!UICONTROL View name]**&quot; den Namen der Ansicht fest (z. B. `cart`). Diese Aktion rendert die bereits abgerufenen Vorschläge, ohne den Edge Network zu kontaktieren.
1. Konfigurieren Sie für das Ereignis „Ende der Seite“ eine [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) Aktion: Aktivieren Sie **[!UICONTROL Use guided events]**, wählen Sie **[!UICONTROL Collect analytics]** aus und verweisen Sie auf das Datenelement im **[!UICONTROL XDM]**.

>[!ENDTABS]

## GitHub-Beispiel {#github-sample}

Das [obere und untere Beispiel im Legierungsbeispiele-Repository](https://github.com/adobe/alloy-samples/tree/main/target/top-and-bottom) zeigt, wie Sie oben auf der Seite eine Personalisierung anfordern und unten Analysemetriken senden können. Laden Sie das Beispiel herunter und führen Sie es lokal aus, um zu sehen, wie die Ereignisse oben und unten auf der Seite funktionieren. Im Beispiel wird die JavaScript-Bibliothek direkt verwendet. Dasselbe Muster gilt, wenn Sie äquivalente Regeln in der Web-SDK-Tag-Erweiterung konfigurieren.
