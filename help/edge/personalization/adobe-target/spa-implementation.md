---
title: Implementierung von Einzelseiten-Apps für das Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie mit Adobe Target eine SPA-Implementierung des Adobe Experience Platform Web SDK erstellen.
keywords: Target; Adobe Target; xdm-Ansichten; Ansichten; Einzelseitenanwendungen; SPA; SPA Lebenszyklus; clientseitig; AB-Tests; AB; Erlebnis-Targeting; XT; VEC
exl-id: cc48c375-36b9-433e-b45f-60e6c6ea4883
source-git-commit: 0085306a2f5172eb19590cc12bc9645278bd2b42
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 12%

---

# Implementierung von Einzelseitenanwendungen

Adobe Experience Platform Web SDK bietet umfassende Funktionen, mit denen Ihr Unternehmen mithilfe von Client-seitigen Technologien der neuesten Generation, wie Single Page Applications (SPA), Personalisierungen ausführen kann.

Herkömmliche Websites arbeiteten auf Basis von Page-to-Page-Navigationsmodellen (auch als Multi-Page-Anwendungen bekannt), bei denen Website-Designs eng an URLs gekoppelt waren und Übergänge von einer Webseite zu einer anderen einen Seitenladevorgang benötigten.

Moderne Webanwendungen wie Einzelseiten-Apps haben stattdessen ein Modell übernommen, das die schnelle Nutzung des Browser-UI-Renderings ermöglicht, das häufig unabhängig von Seitenneuladungen ist. Diese Erlebnisse können durch Kundeninteraktionen wie Bildläufe, Klicks und Cursorbewegungen ausgelöst werden. Da sich die Paradigmen des modernen Webs weiterentwickelt haben, funktioniert die Relevanz herkömmlicher generischer Ereignisse wie Seitenladevorgänge für die Bereitstellung von Personalisierung und Experimenten nicht mehr.

![](assets/spa-vs-traditional-lifecycle.png)

## Vorteile des Platform Web SDK für SPA

Hier einige Vorteile der Verwendung des Adobe Experience Platform Web SDK für Einzelseitenanwendungen:

* Möglichkeit zur Zwischenspeicherung aller Angebote beim Seitenladen, um mehrere Server-Aufrufe auf einen einzelnen Server-Aufruf zu reduzieren
* Das Benutzererlebnis auf Ihrer Site wird erheblich verbessert, da Angebote sofort über den Cache angezeigt werden, ohne dass durch herkömmliche Server-Aufrufe eine verzögerungsfreie Zeit entsteht.
* Eine einzelne Codezeile und eine einmalige Einrichtung für Entwickler ermöglichen es Marketing-Experten, A/B- und Erlebnis-Targeting (XT)-Aktivitäten über den Visual Experience Composer (VEC) auf Ihrer SPA zu erstellen und auszuführen.

## XDM-Ansichten und Einzelseitenanwendungen

Der Adobe Target VEC für SPA nutzt das Konzept Ansichten: eine logische Gruppe visueller Elemente, aus denen ein SPA Erlebnis besteht. Eine Einzelseitenanwendung kann daher als Übergang durch Ansichten anstelle von URLs betrachtet werden, basierend auf Benutzerinteraktionen. Eine Ansicht umfasst in der Regel eine ganze Site oder eine Gruppe visueller Elemente innerhalb einer Site.

Um genauer zu erklären, was Ansichten sind, verwendet das folgende Beispiel eine hypothetische E-Commerce-Site, die in React implementiert wurde, um Beispielansichten zu untersuchen.

Nachdem Sie zur Homepage navigiert sind, fördert ein Hero-Bild einen Osterverkauf sowie die neuesten Produkte, die auf der Site verfügbar sind. In diesem Fall kann eine Ansicht für den gesamten Startbildschirm definiert werden. Diese Ansicht könnte einfach &quot;home&quot;genannt werden.

![](assets/example-views.png)

Wenn sich der Kunde mehr für die Produkte interessiert, die das Unternehmen verkauft, entscheidet er, auf die **Produkte** Link. Ähnlich wie die Homepage kann die gesamte Produktseite als Ansicht definiert werden. Diese Ansicht könnte &quot;products-all&quot;heißen.

![](assets/example-products-all.png)

Da eine Ansicht als ganze Site oder eine Gruppe visueller Elemente auf einer Site definiert werden kann, können die vier auf der Produktseite angezeigten Produkte gruppiert und als Ansicht betrachtet werden. Diese Ansicht könnte &quot;Produkte&quot;heißen.

![](assets/example-products.png)

Wenn der Kunde entscheidet, auf die **Mehr laden** -Schaltfläche, um weitere Produkte auf der Site zu erkunden, ändert sich die Website-URL in diesem Fall nicht, aber hier kann eine Ansicht erstellt werden, die nur die zweite Zeile der angezeigten Produkte darstellt. Der Name der Ansicht könnte &quot;products-page-2&quot;lauten.

![](assets/example-load-more.png)

Der Kunde beschließt, einige Produkte von der Site zu kaufen, und fährt mit dem Checkout-Bildschirm fort. Auf der Checkout-Site erhält der Kunde die Möglichkeit, einen normalen Versand oder einen Expressversand auszuwählen. Eine Ansicht kann aus einer beliebigen Gruppe visueller Elemente auf einer Site bestehen. Daher kann eine Ansicht für Versandvoreinstellungen erstellt und als &quot;Versandvoreinstellungen&quot;bezeichnet werden.

![](assets/example-check-out.png)

Das Konzept der Ansichten kann noch viel weiter erweitert werden. Dies sind nur einige Beispiele für Ansichten, die auf einer Site definiert werden können.

## Implementieren von XDM-Ansichten

XDM-Ansichten können in Adobe Target genutzt werden, um Marketern zu ermöglichen, A/B- und XT-Tests über SPA über den Visual Experience Composer durchzuführen. Dazu müssen Sie die folgenden Schritte ausführen, um eine einmalige Entwicklereinrichtung abzuschließen:

1. Installieren [Adobe Experience Platform Web SDK](../../fundamentals/installing-the-sdk.md)
2. Bestimmen Sie alle XDM-Ansichten in Ihrer Einzelseitenanwendung, die Sie personalisieren möchten.
3. Nachdem Sie die XDM-Ansichten definiert haben, implementieren Sie zur Bereitstellung von AB- oder XT VEC-Aktivitäten die `sendEvent()` Funktion mit `renderDecisions` auf `true` und der entsprechenden XDM-Ansicht in Ihrer Einzelseiten-App. Die XDM-Ansicht muss übergeben werden `xdm.web.webPageDetails.viewName`. Dieser Schritt ermöglicht es Marketing-Experten, den Visual Experience Composer zu nutzen, um A/B- und XT-Tests für diese XDM zu starten.

   ```javascript
   alloy("sendEvent", { 
     "renderDecisions": true, 
     "xdm": { 
       "web": { 
         "webPageDetails": { 
         "viewName":"home" 
         }
       } 
     } 
   });
   ```

>[!NOTE]
>
>Zum ersten `sendEvent()` aufrufen, werden alle XDM-Ansichten abgerufen und zwischengespeichert, die für den Endbenutzer gerendert werden sollen. Nachstehend `sendEvent()` -Aufrufe mit übergebenen XDM-Ansichten werden aus dem Cache gelesen und ohne Serveraufruf gerendert.

## `sendEvent()` Funktionsbeispiele

In diesem Abschnitt werden drei Beispiele zum Aufrufen der `sendEvent()` -Funktion in React für eine hypothetische E-Commerce-SPA.

### Beispiel 1: Startseite von A/B-Tests

Das Marketing-Team möchte A/B-Tests auf der gesamten Startseite durchführen.

![](assets/use-case-1.png)

So führen Sie A/B-Tests auf der gesamten Homepage durch: `sendEvent()` muss mit dem XDM aufgerufen werden `viewName` auf `home`:

```jsx
function onViewChange() { 
  
  var viewName = window.location.hash; // or use window.location.pathName if router works on path and not hash 

  viewName = viewName || 'home'; // view name cannot be empty 

  // Sanitize viewName to get rid of any trailing symbols derived from URL 

  if (viewName.startsWith('#') || viewName.startsWith('/')) { 
    viewName = viewName.substr(1); 
  }
   
  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName":"home" 
        } 
      } 
    }
  }); 
} 

// react router v4 

const history = syncHistoryWithStore(createBrowserHistory(), store); 

history.listen(onViewChange); 

// react router v3 

<Router history={hashHistory} onUpdate={onViewChange} > 
```

### Beispiel 2: Personalisierte Produkte

Das Marketing-Team möchte die zweite Produktzeile personalisieren, indem die Farbe der Preisbeschriftung nach dem Klicken eines Benutzers in Rot geändert wird. **Mehr laden**.

![](assets/use-case-2.png)

```jsx
function onViewChange(viewName) { 

  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName": viewName
        }
      } 
    } 
  }); 
} 

class Products extends Component { 
  
  render() { 
    return ( 
      <button type="button" onClick={this.handleLoadMoreClicked}>Load more</button> 
    ); 
  } 

  handleLoadMoreClicked() { 
    var page = this.state.page + 1; // assuming page number is derived from component’s state 
    this.setState({page: page}); 
    onViewChange('PRODUCTS-PAGE-' + page); 
  } 

} 
```

### Beispiel 3: Versandvoreinstellungen für A/B-Tests

Das Marketing-Team möchte einen A/B-Test durchführen, um zu sehen, ob die Farbe der Schaltfläche von blau in rot geändert wird, wenn **Expresszustellung** aktiviert ist, kann die Konversionen steigern (im Gegensatz zur blauen Button-Farbe für beide Versandoptionen).

![](assets/use-case-3.png)

Um den Inhalt auf der Site je nach ausgewählter Versandpräferenz zu personalisieren, kann für jede Versandpräferenz eine Ansicht erstellt werden. Wann **Normaler Versand** ausgewählt ist, kann die Ansicht &quot;Checkout-normal&quot;genannt werden. Wenn **Expresszustellung** ausgewählt ist, kann die Ansicht &quot;Checkout-Express&quot;genannt werden.

```jsx
function onViewChange(viewName) { 
  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName": viewName 
        }
      }
    }
  }); 
} 

class Checkout extends Component { 

  render() { 
    return ( 
      <div onChange={this.onDeliveryPreferenceChanged}> 
        <label> 
          <input type="radio" id="normal" name="deliveryPreference" value={"Normal Delivery"} defaultChecked={true}/> 
          <span> Normal Delivery (7-10 business days)</span> 
        </label> 
        <label> 
          <input type="radio" id="express" name="deliveryPreference" value={"Express Delivery"}/> 
          <span> Express Delivery* (2-3 business days)</span> 
        </label> 
      </div> 
    ); 
  } 

  onDeliveryPreferenceChanged(evt) { 
    var selectedPreferenceValue = evt.target.value; 
    onViewChange(selectedPreferenceValue); 
  } 

} 
```

## Verwenden von Visual Experience Composer für eine SPA

Wenn Sie mit der Definition Ihrer XDM-Ansichten fertig sind und implementiert haben `sendEvent()` Wenn diese XDM-Ansichten übergeben werden, kann der VEC diese Ansichten erkennen und es Benutzern ermöglichen, Aktionen und Änderungen für A/B- oder XT-Aktivitäten zu erstellen.

>[!NOTE]
>
>Um VEC für Ihre SPA zu verwenden, müssen Sie entweder die [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) oder [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper-Erweiterung.

### Bedienfeld „Änderungen“

Im Bedienfeld Änderungen werden die für eine bestimmte Ansicht erstellten Aktionen erfasst. Alle Aktionen für eine Ansicht sind unter dieser Ansicht gruppiert.

![](assets/modifications-panel.png)

### Aktionen

Durch Klicken auf eine Aktion wird das Element auf der Sites hervorgehoben, in dem diese Aktion angewendet wird. Jede VEC-Aktion, die unter einer Ansicht erstellt wird, verfügt über die folgenden Symbole: **Informationen**, **Bearbeiten**, **Klonen**, **Verschieben** und **Löschen**. Diese Symbole werden in der folgenden Tabelle ausführlicher erläutert.

![](assets/action-icons.png)

| Symbol | Beschreibung |
|---|---|
| Information | Zeigt die Details der Aktion an. |
| Bearbeiten | Ermöglicht die direkte Bearbeitung der Eigenschaften dieser Aktion. |
| Klonen | Sie können die Aktion auf eine oder mehrere Ansichten klonen, die im Bedienfeld Änderungen vorhanden sind, oder auf eine oder mehrere Ansichten, die Sie im VEC durchsucht haben oder zu denen Sie navigiert sind. Die Aktion muss nicht unbedingt im Bedienfeld „Änderungen“ vorhanden sein.<br/><br/>**Hinweis:** Nachdem ein Klonvorgang durchgeführt wurde, müssen Sie über &quot;Durchsuchen&quot;zur Ansicht im VEC navigieren, um zu sehen, ob die geklonte Aktion ein gültiger Vorgang war. Wenn die Aktion nicht auf die Ansicht angewendet werden kann, wird ein Fehler angezeigt. |
| Verschieben | Hiermit wird die Aktion in ein Seitenladereignis oder eine andere Ansicht verschoben, die im Änderungs-Bedienfeld bereits vorhanden ist.<br/><br/>**Seitenladeereignis:** Alle Aktionen, die dem Seitenladeereignis entsprechen, werden beim ersten Laden der Seite Ihrer Webanwendung angewendet. <br/><br/>**Hinweis:** Nachdem ein Verschiebevorgang ausgeführt wurde, müssen Sie über &quot;Durchsuchen&quot;zur Ansicht im VEC navigieren, um zu sehen, ob das Verschieben ein gültiger Vorgang war. Wenn die Aktion nicht auf die Ansicht angewendet werden kann, wird ein Fehler angezeigt. |
| Löschen | Löscht die Aktion. |

## VEC für SPA Beispiele verwenden

In diesem Abschnitt werden drei Beispiele für die Verwendung von Visual Experience Composer zum Erstellen von Aktionen und Änderungen für A/B- oder XT-Aktivitäten beschrieben.

### Beispiel 1: Aktualisieren der Startansicht

Zuvor wurde in diesem Dokument eine Ansicht mit dem Namen &quot;home&quot;für die gesamte Homepage definiert. Das Marketing-Team möchte nun die Startansicht wie folgt aktualisieren:

* Ändern Sie die **Zum Warenkorb hinzufügen** und **liken** -Schaltflächen zu einem leichteren Anteil von Blau. Dies sollte während des Seitenladevorgangs geschehen, da die Komponenten der Kopfzeile geändert werden müssen.
* Ändern Sie die **Neueste Produkte für 2019** Beschriftung zu **Schärfste Produkte für 2019** und ändern Sie die Textfarbe in violett.

Um diese Aktualisierungen im VEC vorzunehmen, wählen Sie **Erstellen** und wenden Sie diese Änderungen auf die Startansicht an.

![](assets/vec-home.png)

### Beispiel 2: Produktbeschriftungen ändern

Für die Ansicht &quot;products-page-2&quot;möchte das Marketing-Team die **Preis** Beschriftung zu **Verkaufspreis** und ändern Sie die Beschriftungsfarbe in Rot.

Um diese Aktualisierungen im VEC vorzunehmen, sind die folgenden Schritte erforderlich:

1. Auswählen **Durchsuchen** im VEC.
2. Auswählen **Produkte** in der oberen Navigation der Site.
3. Auswählen **Mehr laden** einmal , um die zweite Produktzeile anzuzeigen.
4. Auswählen **Erstellen** im VEC.
5. Aktionen anwenden, um die Textbeschriftung auf **Verkaufspreis** und die Farbe in Rot.

![](assets/vec-products-page-2.png)

### Beispiel 3: Präferenzstil eines Versands personalisieren

Ansichten können auf granularer Ebene definiert werden, z. B. ein Status oder eine Option über ein Optionsfeld. Zuvor in diesem Dokument wurden Ansichten für Versandvoreinstellungen, &quot;Checkout-normal&quot;und &quot;Checkout-Express&quot;definiert. Das Marketing-Team möchte die Schaltflächenfarbe für die &quot;Checkout-Express&quot;-Ansicht in Rot ändern.

Um diese Aktualisierungen im VEC vorzunehmen, sind die folgenden Schritte erforderlich:

1. Auswählen **Durchsuchen** im VEC.
2. Fügen Sie Produkte zum Warenkorb auf der Site hinzu.
3. Wählen Sie oben rechts auf der Site das Warenkorbsymbol aus.
4. Auswählen **Bestellung auschecken**.
5. Wählen Sie die **Expresszustellung** Optionsfeld unter **Versandvoreinstellungen**.
6. Auswählen **Erstellen** im VEC.
7. Ändern Sie die **Bezahlen** Schaltflächenfarbe in Rot.

>[!NOTE]
>
>Die Ansicht &quot;Checkout-Express&quot;wird im Bedienfeld Änderungen erst dann angezeigt, wenn die **Expresszustellung** Optionsfeld ausgewählt ist. Dies liegt daran, dass die Variable `sendEvent()` -Funktion ausgeführt wird, wenn die **Expresszustellung** Optionsfeld ausgewählt ist, daher ist dem VEC die Ansicht &quot;Checkout-Express&quot;erst bekannt, wenn das Optionsfeld ausgewählt ist.

![](assets/vec-delivery-preference.png)
