---
title: Ereignistypen in der Adobe Experience Platform Web SDK-Erweiterung
description: Erfahren Sie, wie Sie Ereignistypen verwenden, die von der Adobe Experience Platform Web SDK-Erweiterung in Adobe Experience Platform Launch bereitgestellt werden.
solution: Experience Platform
exl-id: b3162406-c5ce-42ec-ab01-af8ac8c63560
source-git-commit: 5218e6cf82b74efbbbcf30495395a4fe2ad9fe14
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 1%

---

# Ereignistypen

Auf dieser Seite werden die Adobe Experience Platform-Ereignistypen beschrieben, die von der Adobe Experience Platform Web SDK-Tag-Erweiterung bereitgestellt werden. Diese werden verwendet, um [Build-Regeln](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-rules.html) und sollten nicht mit der [`eventType` -Feld in XDM](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=de).

## [!UICONTROL Abschluss des Ereignisses senden]

Normalerweise verfügt Ihre Eigenschaft über eine oder mehrere Regeln, die die [[!UICONTROL Ereignis senden] action](action-types.md#send-event) , um Ereignisse an Adobe Experience Platform Edge Network zu senden. Jedes Mal, wenn ein Ereignis an Edge Network gesendet wird, wird eine Antwort mit nützlichen Daten an den Browser zurückgegeben. Ohne [!UICONTROL Abschluss des Ereignisses senden] Ereignistyp verwenden, hätten Sie keinen Zugriff auf diese zurückgegebenen Daten.

Um auf die zurückgegebenen Daten zuzugreifen, erstellen Sie eine separate Regel und fügen Sie dann eine [!UICONTROL Abschluss des Ereignisses senden] -Ereignis der Regel hinzufügen. Diese Regel wird jedes Mal ausgelöst, wenn eine erfolgreiche Antwort vom Server als Ergebnis einer [!UICONTROL Ereignis senden] Aktion.

Wenn eine [!UICONTROL Abschluss des Ereignisses senden] -Ereignis eine Regel Trigger, werden vom Server zurückgegebene Daten bereitgestellt, die für die Ausführung bestimmter Aufgaben nützlich sein können. In der Regel fügen Sie eine [!UICONTROL Benutzerspezifischer Code] Aktion (aus der [!UICONTROL Core] -Erweiterung) auf dieselbe Regel, die die [!UICONTROL Abschluss des Ereignisses senden] -Ereignis. Im [!UICONTROL Benutzerspezifischer Code] Aktion verwenden, hat Ihr benutzerdefinierter Code Zugriff auf eine Variable mit dem Namen `event`. Diese `event` enthält die vom Server zurückgegebenen Daten.

Ihre Regel für die Verarbeitung von Daten, die vom Edge Network zurückgegeben werden, könnte in etwa so aussehen:

![](./assets/send-event-complete.png)

Im Folgenden finden Sie einige Beispiele für die Ausführung bestimmter Aufgaben mithilfe der Variablen [!UICONTROL Benutzerspezifischer Code] -Aktion in dieser Regel.

### Manuelles Rendern personalisierter Inhalte

In der Aktion &quot;Benutzerspezifischer Code&quot;, die sich in der Regel für die Verarbeitung von Antwortdaten befindet, können Sie auf vom Server zurückgegebene Personalisierungsvorschläge zugreifen. Geben Sie dazu den folgenden benutzerdefinierten Code ein:

```javascript
var propositions = event.propositions;
```

Wenn `event.propositions` vorhanden ist, ist es ein Array, das Personalisierungspropositionsobjekte enthält. Die im Array enthaltenen Vorschläge werden größtenteils danach bestimmt, wie das Ereignis an den Server gesendet wurde.

Für dieses erste Szenario nehmen Sie an, dass Sie die Variable [!UICONTROL Renderentscheidungen] und haben keine [!UICONTROL Entscheidungsbereiche] innerhalb der [!UICONTROL Ereignis senden] Aktion, die für das Senden des Ereignisses verantwortlich ist.

![img.png](assets/send-event-render-unchecked-without-scopes.png)

In diesem Beispiel wird die `propositions` -Array enthält nur Vorschläge für das Ereignis, die für das automatische Rendering geeignet sind.

Die `propositions` -Array ähnelt möglicherweise diesem Beispiel:

```json
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "__view__",
    "items": [
      {
        "id": "11223344",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">An HTML proposition.</h2>",
          "selector": "#hero",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  },
  {
    "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
    "scope": "__view__",
    "items": [
      {
        "id": "11223345",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">Another HTML proposition.</h2>",
          "selector": "#sidebar",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  }
]
```

Beim Senden des Ereignisses wird die Variable [!UICONTROL Renderentscheidungen] nicht aktiviert wurde, sodass das SDK nicht versucht hat, automatisch Inhalte zu rendern. Das SDK hat jedoch weiterhin automatisch die Inhalte abgerufen, die für das automatische Rendering infrage kommen, und Ihnen zur manuellen Wiedergabe bereitgestellt, sofern dies gewünscht ist. Beachten Sie, dass jedes Vorschlagsobjekt seinen `renderAttempted` Eigenschaft auf `false`.

Wenn Sie stattdessen die Option [!UICONTROL Renderentscheidungen] aktivieren, wenn das Ereignis gesendet wird, hätte das SDK versucht, alle Vorschläge wiederzugeben, die für die automatische Wiedergabe infrage kommen. Daher würde jedes der Vorschlagsobjekte seine `renderAttempted` Eigenschaft auf `true`. In diesem Fall müssen diese Vorschläge nicht manuell gerendert werden.

Bisher haben Sie sich nur mit Personalisierungsinhalten befasst, die für die automatische Wiedergabe geeignet sind (z. B. mit Inhalten, die im Visual Experience Composer von Adobe Target erstellt wurden). Abrufen von Personalisierungsinhalten _not_ für das automatische Rendering infrage kommen, fordern Sie den Inhalt an, indem Sie Entscheidungsbereiche mit der [!UICONTROL Entscheidungsbereiche] im Feld [!UICONTROL Ereignis senden] Aktion. Ein Perimeter ist eine Zeichenfolge, die einen bestimmten Vorschlag identifiziert, den Sie vom Server abrufen möchten.

Die [!UICONTROL Ereignis senden] -Aktion würde wie folgt aussehen:

![img.png](assets/send-event-render-unchecked-with-scopes.png)

In diesem Beispiel, wenn Vorschläge auf dem Server gefunden werden, die dem `salutation` oder `discount` , werden sie zurückgegeben und in die `propositions` Array. Beachten Sie, dass Vorschläge, die für das automatische Rendering infrage kommen, weiterhin im Abschnitt `propositions` Array, unabhängig davon, wie Sie die [!UICONTROL Renderentscheidungen] oder [!UICONTROL Entscheidungsbereiche] -Felder in [!UICONTROL Ereignis senden] Aktion. Die `propositions` -Array würde in diesem Fall in etwa wie folgt aussehen:

```json
[
  {
    "id": "AT:cZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ2",
    "scope": "salutation",
    "items": [
      {
        "schema": "https://ns.adobe.com/personalization/json-content-item",
        "data": {
          "id": "4433221",
          "content": {
            "salutation": "Welcome, esteemed visitor!"
          }
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  },
  {
    "id": "AT:FZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ0",
    "scope": "discount",
    "items": [
      {
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "data": {
          "id": "4433222",
          "content": "<div>50% off your order!</div>",
          "format": "text/html"
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "__view__",
    "items": [
      {
        "id": "11223344",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">An HTML proposition.</h2>",
          "selector": "#hero",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  },
  {
    "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
    "scope": "__view__",
    "items": [
      {
        "id": "11223345",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">Another HTML proposition.</h2>",
          "selector": "#sidebar",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "renderAttempted": false
  }
]
```

An dieser Stelle können Sie den Vorschlagsinhalt nach Bedarf rendern. In diesem Beispiel entspricht der Vorschlag dem `discount` scope ist ein HTML-Vorschlag, der mit dem formularbasierten Experience Composer von Adobe Target erstellt wurde. Angenommen, Sie haben ein Element auf Ihrer Seite mit der ID von `daily-special` und den Inhalt aus der `discount` Vorschlag in die `daily-special` -Element. Gehen Sie folgendermaßen vor:

1. Entnehmen Sie Vorschläge aus dem `event` -Objekt.
1. Durchlaufen Sie jeden Vorschlag und suchen Sie nach dem Vorschlag mit einem Umfang von `discount`.
1. Wenn Sie einen Vorschlag finden, durchlaufen Sie jedes Element im Vorschlag, suchen Sie nach dem Element, das HTML-Inhalt ist. (Es ist besser zu überprüfen als anzunehmen.)
1. Wenn Sie einen Artikel finden, der HTML-Inhalt enthält, suchen Sie nach der `daily-special` -Element auf der Seite und ersetzen Sie die zugehörige HTML durch den personalisierten Inhalt.

Ihr benutzerspezifischer Code innerhalb der [!UICONTROL Benutzerspezifischer Code] -Aktion könnte wie folgt aussehen:

```javascript
var propositions = event.propositions;

var discountProposition;
if (propositions) {
  // Find the discount proposition, if it exists.
  for (var i = 0; i < propositions.length; i++) {
    var proposition = propositions[i]; 
    if (proposition.scope === "discount") {
      discountProposition = proposition;
      break;
    }
  }
}

var discountHtml;
if (discountProposition) {
  // Find the item from proposition that should be rendered.
  // Rather than assuming there a single item that has HTML
  // content, find the first item whose schema indicates
  // it contains HTML content.
  for (var j = 0; j < discountProposition.items.length; j++) {
    var discountPropositionItem = discountProposition.items[i]; 
    if (discountPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
      discountHtml = discountPropositionItem.data.content;
      break;
    }
  }
}

if (discountHtml) {
  // Discount HTML exists. Time to render it.
  var dailySpecialElement = document.getElementById("daily-special");
  dailySpecialElement.innerHTML = discountHtml;
}
```

### Zugriff auf Adobe Target-Antwort-Token

Von Adobe Target zurückgegebene Personalisierungsinhalte umfassen [Antwort-Token](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html), die Details zur Aktivität, zum Angebot, zum Erlebnis, zum Benutzerprofil, zu geografischen Informationen und mehr enthalten. Diese Details können für Drittanbieter-Tools freigegeben oder zum Debugging verwendet werden. Antwort-Token können in der Benutzeroberfläche von Adobe Target konfiguriert werden.

In der Aktion &quot;Benutzerspezifischer Code&quot;, die sich in der Regel für die Verarbeitung von Antwortdaten befindet, können Sie auf vom Server zurückgegebene Personalisierungsvorschläge zugreifen. Geben Sie dazu den folgenden benutzerdefinierten Code ein:

```javascript
var propositions = event.propositions;
```

Wenn `event.propositions` vorhanden ist, ist es ein Array, das Personalisierungspropositionsobjekte enthält. Siehe [Manuelles Rendern personalisierter Inhalte](#manually-render-personalized-content) für weitere Informationen über den Inhalt von `result.propositions`.

Angenommen, Sie möchten alle Aktivitätsnamen aus allen Vorschlägen erfassen, die automatisch vom Web SDK gerendert wurden, und sie in ein einzelnes Array übertragen. Sie können dann das einzelne Array an einen Drittanbieter senden. In diesem Fall schreiben Sie benutzerdefinierten Code in die [!UICONTROL Benutzerspezifischer Code] Aktion für:

1. Entnehmen Sie Vorschläge aus dem `event` -Objekt.
1. Durchlaufen Sie jeden Vorschlag.
1. Bestimmen Sie, ob das SDK den Vorschlag wiedergegeben hat.
1. Falls ja, durchlaufen Sie jedes Element des Vorschlags.
1. Rufen Sie den Aktivitätsnamen aus dem `meta` -Eigenschaft, ein Objekt, das Antwort-Token enthält.
1. Ziehen Sie den Namen der Aktivität in ein Array.
1. Senden Sie die Aktivitätsnamen an einen Drittanbieter.

```javascript
var propositions = event.propositions;
if (propositions) {
  var activityNames = [];
  propositions.forEach(function(proposition) {
    if (proposition.renderAttempted) {
      proposition.items.forEach(function(item) {
        if (item.meta) {
          // item.meta contains the response tokens.
          var activityName = item.meta["activity.name"];
          // Ignore duplicates
          if (activityNames.indexOf(activityName) === -1) {
            activityNames.push(activityName);  
          }
        }
      });
    }
  });
  // Now that activity names are in an array,
  // you can send them to a third party or use
  // them in some other way.
}
```
