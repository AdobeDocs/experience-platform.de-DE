---
title: 'Adobe Target und Adobe Experience Platform Web SDK. '
seo-title: Adobe Experience Platform Web SDK und Verwendung von Adobe Target
description: Erfahren Sie, wie Sie personalisierte Inhalte mit Experience Platform Web SDK mit Adobe Target wiedergeben
seo-description: Erfahren Sie, wie Sie personalisierte Inhalte mit Experience Platform Web SDK mit Adobe Target wiedergeben
keywords: zielgruppe;adobe-Zielgruppe;xdm-Ansichten ansichten;Einzelseitenanwendungen;SPA;SPA Lebenszyklus;Clientseitige;AB-Tests;AB;Erlebnis-Targeting;XT;VEC
translation-type: tm+mt
source-git-commit: 3ac00fda2c0a43437fb212dcba7e98c63503b9c4
workflow-type: tm+mt
source-wordcount: '1688'
ht-degree: 12%

---


# Implementieren von Einzelseiten-Apps

Adobe Experience Platform Web SDK bietet umfassende Funktionen, mit denen Ihr Unternehmen Personalisierungen auf clientseitigen Technologien der nächsten Generation, wie z. B. Einzelseitenanwendungen (SPA), durchführen kann.

Herkömmliche Websites arbeiteten auf Basis von Page-to-Page-Navigationsmodellen (auch als Multi-Page-Anwendungen bekannt), bei denen Website-Designs eng an URLs gekoppelt waren und Übergänge von einer Webseite zu einer anderen einen Seitenladevorgang benötigten.

Moderne Webanwendungen, wie Einzelseitenanwendungen, haben stattdessen ein Modell entwickelt, das eine schnelle Nutzung des Browser-UI-Renderings ermöglicht, das häufig unabhängig von Seitenneuladungen ist. Diese Erlebnisse können durch Kundeninteraktionen wie Bildlauf, Klicks und Cursor-Bewegungen ausgelöst werden. Da sich die Paradigmen des modernen Webs weiterentwickelt haben, funktioniert die Relevanz herkömmlicher generischer Ereignis wie das Laden von Seiten, um Personalisierung und Experimentierung bereitzustellen, nicht mehr.

![](assets/spa-vs-traditional-lifecycle.png)

## Vorteile des Platform Web SDK für SPA

Die Verwendung des Adobe Experience Platform Web SDK für Einzelseitenanwendungen bietet folgende Vorteile:

* Möglichkeit zur Zwischenspeicherung aller Angebote beim Seitenladen, um mehrere Server-Aufrufe auf einen einzelnen Server-Aufruf zu reduzieren
* Verbessern Sie die Benutzererfahrung auf Ihrer Site erheblich, da Angebot sofort über den Cache ohne Zeitverzögerung angezeigt werden, die durch herkömmliche Serveraufrufe eingeführt wurde.
* Eine einzelne Codezeile und ein einmaliges Entwicklersetup ermöglichen es Marketingexperten, A/B- und Erlebnis-Targeting (XT)-Aktivitäten über den Visual Experience Composer (VEC) auf Ihrer SPA zu erstellen und auszuführen.

## XDM-Ansichten und Einzelseitenanwendungen

Der Adobe Target VEC for SPA nutzt das Konzept der Ansichten: eine logische Gruppe von visuellen Elementen, die zusammen ein SPA Erlebnis bilden. Eine Einzelseitenanwendung kann daher aufgrund von Benutzerinteraktionen als Übergang durch Ansichten und nicht als URLs betrachtet werden. Eine Ansicht umfasst in der Regel eine ganze Site oder eine Gruppe visueller Elemente innerhalb einer Site.

Zur weiteren Erläuterung der Ansichten verwendet das folgende Beispiel eine hypothetische Online-E-Commerce-Website, die in React implementiert ist, um Beispielslösungen zu untersuchen.

Nach dem Aufrufen der Homepage fördert ein Heldenbild einen Osterverkauf sowie die neuesten Produkte auf der Site. In diesem Fall könnte eine Ansicht für den gesamten Startbildschirm definiert werden. Diese Ansicht könnte man einfach als &quot;Zuhause&quot;bezeichnen.

![](assets/example-views.png)

Wenn sich der Kunde mehr für die Produkte interessiert, die das Unternehmen verkauft, entscheidet er, auf den Link **Produkte** zu klicken. Ähnlich wie die Homepage kann die gesamte Produktseite als Ansicht definiert werden. Diese Ansicht könnte &quot;products-all&quot;heißen.

![](assets/example-products-all.png)

Da eine Ansicht als Ganzes oder als Gruppe von visuellen Elementen auf einer Site definiert werden kann, könnten die vier auf der Produktsite angezeigten Produkte gruppiert und als Ansicht betrachtet werden. Diese Ansicht könnte &quot;products&quot;heißen.

![](assets/example-products.png)

Wenn der Kunde beschließt, auf die Schaltfläche **Mehr laden** zu klicken, um weitere Produkte auf der Site zu untersuchen, ändert sich die Website-URL in diesem Fall nicht, aber hier kann eine Ansicht erstellt werden, die nur die zweite angezeigte Produktzeile darstellt. Der Name der Ansicht könnte &quot;products-page-2&quot;lauten.

![](assets/example-load-more.png)

Der Kunde beschließt, einige Produkte von der Site zu erwerben, und fährt mit dem Kassengang fort. Auf der Kasse-Site erhält der Kunde Optionen zur Auswahl des normalen Versands oder des Express-Versands. Eine Ansicht kann eine beliebige Gruppe visueller Elemente auf einer Site sein. Daher könnte eine Ansicht für die Voreinstellungen des Versands erstellt und als &quot;Versand-Voreinstellungen&quot;bezeichnet werden.

![](assets/example-check-out.png)

Das Konzept der Ansichten kann noch viel weiter ausgebaut werden. Dies sind nur einige Beispiele für Ansichten, die auf einer Site definiert werden können.

## Implementieren von XDM-Ansichten

XDM-Ansichten können in Adobe Target genutzt werden, um Marketern die Möglichkeit zu geben, A/B- und XT-Tests über den Visual Experience Composer SPA durchzuführen. Dies erfordert die folgenden Schritte, um eine einmalige Entwicklereinrichtung abzuschließen:

1. [Adobe Experience Platform Web SDK](../../fundamentals/installing-the-sdk.md) installieren
2. Bestimmen Sie alle XDM-Ansichten in Ihrer Einzelseitenanwendung, die Sie personalisieren möchten.
3. Nachdem Sie die XDM-Ansichten definiert haben, implementieren Sie zur Bereitstellung von AB- oder XT VEC-Aktivitäten die `sendEvent()`-Funktion mit `renderDecisions` auf `true` und der entsprechenden XDM-Ansicht in Ihrer Einzelseitenanwendung. Die XDM-Ansicht muss in `xdm.web.webPageDetails.viewName` übergeben werden. Dieser Schritt ermöglicht es Marketingexperten, den Visual Experience Composer zu nutzen, um A/B- und XT-Tests für diese XDM zu starten.

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
>Beim ersten `sendEvent()`-Aufruf werden alle XDM-Ansichten, die an den Endbenutzer gerendert werden sollen, abgerufen und zwischengespeichert. Nachfolgende `sendEvent()`-Aufrufe mit weitergeleiteten XDM-Ansichten werden aus dem Cache gelesen und ohne Serveraufruf gerendert.

## `sendEvent()` Funktionsbeispiele

In diesem Abschnitt werden drei Beispiele erläutert, wie die Funktion `sendEvent()` in React für eine hypothetische E-Commerce-SPA aufgerufen wird.

### Beispiel 1: A/B-Startseite

Das Marketingteam möchte A/B-Tests für die gesamte Startseite durchführen.

![](assets/use-case-1.png)

Um A/B-Tests auf der gesamten Website auszuführen, muss `sendEvent()` aufgerufen werden, wobei XDM `viewName` auf `home` eingestellt ist:

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

Das Marketing-Team möchte die zweite Produktreihe personalisieren, indem die Farbe der Preisbeschriftung in Rot geändert wird, nachdem ein Benutzer auf **Mehr laden** klickt.

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

### Beispiel 3: Voreinstellungen für A/B-Versand

Das Marketingteam möchte einen A/B-Test durchführen, um zu sehen, ob eine Änderung der Schaltflächenfarbe von blau in rot bei Auswahl von **Express-Versand** die Konvertierung steigern kann (im Gegensatz zur Beibehaltung der Schaltflächenfarbe blau für beide Versand).

![](assets/use-case-3.png)

Um den Inhalt auf der Site je nach ausgewählter Versand-Voreinstellung zu personalisieren, kann für jede Versand-Voreinstellung eine Ansicht erstellt werden. Wenn **Normaler Versand** ausgewählt ist, kann die Ansicht &quot;checkout-normal&quot;heißen. Wenn **Express-Versand** ausgewählt ist, kann die Ansicht &quot;checkout-express&quot;heißen.

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

## Verwenden des Visual Experience Composer für eine SPA

Wenn Sie Ihre XDM-Ansichten definiert und `sendEvent()` mit diesen XDM-Ansichten implementiert haben, kann der VEC diese Ansichten erkennen und Benutzern das Erstellen von Aktionen und Änderungen für A/B- oder XT-Aktivitäten ermöglichen.

>[!NOTE]
>
>Um VEC für Ihre SPA zu verwenden, müssen Sie entweder die VEC Helper Extension [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) oder [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) installieren und aktivieren.

### Bedienfeld „Änderungen“

Im Bereich &quot;Änderungen&quot;werden die Aktionen erfasst, die für eine bestimmte Ansicht erstellt wurden. Alle Aktionen für eine Ansicht werden unter dieser Ansicht gruppiert.

![](assets/modifications-panel.png)

### Aktionen

Durch Klicken auf eine Aktion wird das Element auf der Sites hervorgehoben, in dem diese Aktion angewendet wird. Jede VEC-Aktion, die unter einer Ansicht erstellt wurde, hat folgende Symbole: **Informationen**, **Bearbeiten**, **Klonen**, **Verschieben** und **Löschen**. Diese Symbole werden in der folgenden Tabelle detaillierter erläutert.

![](assets/action-icons.png)

| Symbol | Beschreibung |
|---|---|
| Information | Zeigt die Details der Aktion an. |
| Bearbeiten | Ermöglicht die direkte Bearbeitung der Eigenschaften dieser Aktion. |
| Klonen | Sie können die Aktion auf eine oder mehrere Ansichten klonen, die im Bedienfeld Änderungen vorhanden sind, oder auf eine oder mehrere Ansichten, die Sie im VEC durchsucht haben oder zu denen Sie navigiert sind. Die Aktion muss nicht unbedingt im Bedienfeld „Änderungen“ vorhanden sein.<br/><br/>**Hinweis:** Nachdem ein Klonvorgang durchgeführt wurde, müssen Sie über Durchsuchen zur Ansicht im VEC navigieren, um zu sehen, ob es sich bei der geklonten Aktion um einen gültigen Vorgang handelt. Wenn die Aktion nicht auf die Ansicht angewendet werden kann, wird ein Fehler angezeigt. |
| Verschieben | Hiermit wird die Aktion in ein Seitenladereignis oder eine andere Ansicht verschoben, die im Änderungs-Bedienfeld bereits vorhanden ist.<br/><br/>**Seitenlade-Ereignis:** Alle Aktionen, die dem Ereignis zum Laden der Seite entsprechen, werden beim Laden der ersten Seite Ihrer Webanwendung angewendet. <br/><br/>**Hinweis:** Nachdem ein Verschiebungsvorgang durchgeführt wurde, müssen Sie über &quot;Durchsuchen&quot;zur Ansicht im VEC navigieren, um zu sehen, ob es sich um einen gültigen Vorgang handelt. Wenn die Aktion nicht auf die Ansicht angewendet werden kann, wird ein Fehler angezeigt. |
| Löschen | Löscht die Aktion. |

## Verwenden von VEC für SPA Beispiele

In diesem Abschnitt werden drei Beispiele für die Verwendung des Visual Experience Composer zum Erstellen von Aktionen und Änderungen für A/B- oder XT-Aktivitäten erläutert.

### Beispiel 1: Ansicht &quot;home&quot;aktualisieren

Früher wurde in diesem Dokument eine Ansicht mit dem Namen &quot;home&quot;für die gesamte Homepage definiert. Das Marketingteam möchte nun die &quot;Home&quot;-Ansicht wie folgt aktualisieren:

* Ändern Sie die Schaltflächen **Hinzufügen in &quot;Warenkorb**&quot;und **Gefällt mir**&quot;in einen helleren Anteil Blau. Dies sollte während des Seitenladevorgangs geschehen, da es zu einer Änderung der Komponenten der Kopfzeile kommt.
* Ändern Sie die Beschriftung **Neueste Produkte für 2019** in **Höchste Produkte für 2019** und ändern Sie die Textfarbe in violett.

Um diese Aktualisierungen im VEC vorzunehmen, wählen Sie **Erstellen** und wenden Sie diese Änderungen auf die &quot;Home&quot;-Ansicht an.

![](assets/vec-home.png)

### Beispiel 2: Produktbeschriftungen ändern

Bei der Ansicht &quot;products-page-2&quot;möchte das Marketingteam die Beschriftung **Price** in **Verkaufspreis** ändern und die Beschriftungsfarbe in Rot ändern.

Um diese Aktualisierungen im VEC vorzunehmen, sind die folgenden Schritte erforderlich:

1. Wählen Sie **Durchsuchen** im VEC.
2. Wählen Sie **Produkte** in der oberen Navigation der Site.
3. Wählen Sie **Mehr** einmal laden, um die zweite Produktreihe Ansicht.
4. Wählen Sie **Erstellen** im VEC.
5. Wenden Sie Aktionen an, um die Textbeschriftung in **Verkaufspreis** und die Farbe in Rot zu ändern.

![](assets/vec-products-page-2.png)

### Beispiel 3: Anpassen des Präferenzstils für Versand

Ansichten können granular definiert werden, z. B. ein Status oder eine Option über ein Optionsfeld. Früher in diesem Dokument wurden Ansichten für Versand-Voreinstellungen, &quot;Checkout-normal&quot;und &quot;Checkout-Express&quot;definiert. Das Marketingteam möchte die Schaltflächenfarbe für die Ansicht &quot;Checkout-Express&quot;in Rot ändern.

Um diese Aktualisierungen im VEC vorzunehmen, sind die folgenden Schritte erforderlich:

1. Wählen Sie **Durchsuchen** im VEC.
2. hinzufügen Produkte in den Warenkorb auf der Site.
3. Wählen Sie das Einkaufswagensymbol in der oberen rechten Ecke der Site aus.
4. Wählen Sie **Kaufen Sie Ihre Bestellung** aus.
5. Wählen Sie das Optionsfeld **Express-Versand** unter **Versand-Voreinstellungen**.
6. Wählen Sie **Erstellen** im VEC.
7. Ändern Sie die Schaltflächenfarbe **Pay** in Rot.

>[!NOTE]
>
>Die Ansicht &quot;Checkout-Express&quot;wird erst dann im Bereich &quot;Änderungen&quot;angezeigt, wenn das Optionsfeld **Express-Versand** aktiviert ist. Dies liegt daran, dass die Funktion `sendEvent()` ausgeführt wird, wenn das Optionsfeld **Express-Versand** ausgewählt ist. Daher ist dem VEC die Ansicht &quot;Checkout-Express&quot;erst dann bekannt, wenn das Optionsfeld ausgewählt wurde.

![](assets/vec-delivery-preference.png)
