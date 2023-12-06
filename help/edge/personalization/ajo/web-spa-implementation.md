---
title: Implementierung von Einzelseitenanwendungen
description: Erfahren Sie, wie Sie SPA Ansichten in Adobe Journey Optimizer implementieren
exl-id: 1883251b-2d59-46d3-ac74-b8657edd0325
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 77%

---

# Implementieren von Einzelseitenanwendungen (SPAs) {#web-spa-implementation}

Das Adobe Experience Platform Web SDK bietet umfassende Funktionen, mit denen Ihr Unternehmen mithilfe von Client-seitigen Technologien der neuesten Generation Personalisierungen ausführen kann, z. B. Einzelseitenanwendungen (SPA).

Herkömmliche Websites arbeiten auf Basis von „Seite-zu-Seite“-Navigationsmodellen (auch als mehrseitige Anwendungen bekannt), bei denen Website-Designs eng an URLs gekoppelt sind, sodass der Übergang von einer Web-Seite zur anderen ein Laden der Seite erfordert.

Moderne Web-Anwendungen wie z. B. Einzelseitenanwendungen (SPAs) nutzen stattdessen ein Modell, das die Rendering-Funktion der Browser-Oberfläche beschleunigt, wodurch oft keine Neuladungen von Seiten erforderlich sind. Diese Erlebnisse können durch Kundeninteraktionen wie Scrollen, Klicks und Cursor-Bewegungen ausgelöst werden. Da sich die Paradigmen des modernen Webs weiterentwickelt haben, ist die Relevanz herkömmlicher allgemeiner Ereignisse (z. B. das Laden einer Seite) für die Bereitstellung von Personalisierung und Experimenten nicht mehr gegeben.

![Lebenszyklusdiagramm der Seite.](assets/web-spa-vs-traditional-lifecycle.png)

## Vorteile der Verwendung des Web SDK für SPA {#web-spa-benefits}

Im Folgenden finden Sie einige Vorteile der Verwendung des Web SDK für Einzelseitenanwendungen:

* Möglichkeit zur Zwischenspeicherung aller Angebote beim Seitenladen, um mehrere Server-Aufrufe auf einen einzelnen Server-Aufruf zu reduzieren
* Das Benutzererlebnis auf Ihrer Site wird erheblich verbessert, da Angebote sofort über den Cache angezeigt werden, ohne dass durch herkömmliche Server-Aufrufe eine verzögerte Zeit eintritt.
* Durch das einmalige Setup auf Entwicklerseite können Marketing-Fachleute Personalisierungs- und Experimentierungsaktivitäten über den visuellen Web-Editor von Adobe Journey Optimizer auf Ihrer SPA erstellen und ausführen.

## XDM-Ansichten und Einzelseitenanwendungen {#web-spa-xdm}

Der Journey Optimizer-Web-Editor nutzt ein Konzept namens _views_.

Ansichten sind eine logische Gruppe visueller Elemente, aus denen sich ein SPA Erlebnis zusammensetzt. Eine Einzelseitenanwendung kann also als eine Reihe von Ansichten, statt URLs, betrachtet werden, die je nach Benutzerinteraktion aufgerufen werden. Eine Ansicht umfasst in der Regel eine ganze Seite, eine einzelne Seite oder eine Gruppe visueller Elemente innerhalb einer Seite.

Zur weiteren Erläuterung von Ansichten wird im folgenden Beispiel eine hypothetische E-Commerce-Site verwendet.

* Nach dem Navigieren zur Startseite bewirbt ein Hero-Bild saisonale Sammlungen sowie die verschiedenen Produktkataloge, die auf der Site verfügbar sind. In diesem Fall kann der gesamte Startbildschirm als Ansicht definiert werden. Diese Ansicht könnte einfach als „Startseite“ bezeichnet werden.

  ![Beispiel-Website-Bild mit einer Homepage.](assets/web-spa-home.png)

* Mit der Zeit interessieren sich Kundinnen und Kunden mehr und mehr für die Produkte, die das Unternehmen verkauft. Sie klicken auf den Link **Männer**. Ähnlich wie die Startseite kann die gesamte Seite **Männer** als eine Ansicht definiert werden. Diese Ansicht könnte „Männer“ heißen.

  ![Beispiel-Website-Bild, das eine bestimmte Ansicht anzeigt.](assets/web-spa-men.png)

* Da eine Ansicht als ganze Site oder eine Gruppe visueller Elemente auf einer Site definiert werden kann, können die vier auf der Produktseite angezeigten Produkte gruppiert und als Ansicht betrachtet werden. Diese Ansicht könnte „Produkte“ heißen.

  ![Beispiel-Website-Bild, das eine bestimmte Ansicht anzeigt.](assets/web-spa-men-products.png)

* Wenn jemand auf die Schaltfläche **ALLE MÄNNERPRODUKTE** klickt, um sich weitere Produkte auf der Seite anzusehen, ändert sich die Webseite-URL in diesem Fall nicht, aber hier kann eine Ansicht erstellt werden, die nur die zweite Zeile der angezeigten Produkte darstellt. Der Ansichtsname könnte „Produktseite-2“ lauten.

* Die Kundin oder der Kunde möchte einige Produkte von der Seite kaufen und fährt mit dem Checkout-Bildschirm fort. Der Warenkorbbildschirm selbst kann mit einer Ansicht namens „Warenkorb“ verknüpft werden. Alternativ können Sie eine andere Ansicht im Checkout-Bildschirm ansehen, um die unten empfohlenen Produkte zu verarbeiten.

  ![Beispiel-Website-Bild, das eine bestimmte Ansicht anzeigt.](assets/web-spa-cart.png)

Das Konzept der Ansichten kann noch wesentlich stärker ausgeweitet werden. Dies sind nur einige Beispiele für Ansichten, die auf einer Site definiert werden können.

## Implementieren von XDM-Ansichten {#implement-xdm-views}

XDM-Ansichten können in Adobe Journey Optimizer genutzt werden, um Marketingexperten zu ermöglichen, Web-Personalisierungs- und Erlebniskampagnen auf SPA über den Web-Visual-Editor von Journey Optimizer durchzuführen.

Dazu müssen auf Entwicklerseite die folgenden Schritte ausgeführt werden, um ein einmaliges Setup abzuschließen:

1. Installieren [Adobe Experience Platform Web SDK](../../fundamentals/installing-the-sdk.md) und überprüfen Sie die [Voraussetzungen für Webkanäle](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/configure-web-channel/web-prerequisites.html) Seite.

2. Bestimmen Sie alle XDM-Ansichten in Ihrer Einzelseitenanwendung, die Sie personalisieren möchten.

3. Nach dem Definieren der XDM-Ansichten müssen Sie, um Inhalte für diese Ansichten bereitzustellen, in Ihrer Einzelseitenanwendung die Funktion `sendEvent()` mit `renderDecisions` auf `true` und der entsprechenden XDM-Ansicht einstellen. Die XDM-Ansicht muss im `xdm.web.webPageDetails.viewName` übergeben werden. Auf diese Weise können Marketing-Fachleute diese Ansichten im Web-Editor von Journey Optimizer entdecken und Inhaltsänderungen auf sie anwenden:

```
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
>Beim ersten `sendEvent()`-Aufruf werden alle XDM-Ansichten abgerufen und zwischengespeichert, die an die Endbenutzerin bzw. den Endbenutzer gerendert werden sollen. Nachstehende Aufrufe von `sendEvent()` mit XDM-Ansichten, die übermittelt wurden, werden aus dem Cache gelesen und ohne Server-Aufruf gerendert.

## `sendEvent()`-Funktionsbeispiele

In diesem Abschnitt werden zwei Beispiele zum Aufrufen der Funktion `sendEvent()` in React für eine hypothetische E-Commerce-SPA verwendet.

### Beispiel 1: Startseite eines A/B-Tests {#web-spa-sample-1}

Das Marketing-Team möchte A/B-Tests auf der gesamten Startseite durchführen.

![Beispielseite für einseitige Anwendungen.](assets/web-spa-home.png)

So können A/B-Tests auf der gesamten Startseite durchgeführt werden: `sendEvent()` muss aufgerufen werden, während der XDM-`viewName` auf `home` eingestellt ist:

```js
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

### Beispiel 2: Personalisierte Produkte {#web-spa-sample-2}

Das Marketing-Team möchte die zweite Reihe von Produkten personalisieren, indem es die Farbe der Preisbeschriftung in Rot ändert, nachdem jemand auf die Schaltfläche geklickt hat, um alle Männerprodukte anzuzeigen.

![Beispielseite für Einzelseiten-Apps mit personalisierten Produkten.](assets/web-spa-men-products.png)

```js
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

            <
            button type = "button"
            onClick = {
                this.handleLoadMoreClicked
            } > All Men 's Products</button>
        );
    }

    handleLoadMoreClicked() {
        var page = this.state.page + 1; // assuming page number is derived from component's state
        this.setState({
            page: page
        });
        onViewChange('PRODUCTS-PAGE-' + page);
    }
}
```
