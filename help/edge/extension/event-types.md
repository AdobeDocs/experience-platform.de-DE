---
title: Ereignistypen in der Adobe Experience Platform Web SDK-Erweiterung
description: Erfahren Sie, wie Sie Ereignistypen verwenden, die von der Adobe Experience Platform Web SDK-Erweiterung in Adobe Experience Platform Launch bereitgestellt werden.
solution: Experience Platform
feature: Web SDK
exl-id: b3162406-c5ce-42ec-ab01-af8ac8c63560
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 1%

---

# Ereignistypen

Auf dieser Seite werden die Adobe Experience Platform-Ereignistypen beschrieben, die von der Adobe Experience Platform Web SDK-Tag-Erweiterung bereitgestellt werden. Diese werden für [Build-Regeln](https://experienceleague.adobe.com/docs/launch-learn/tutorials/fundamentals/building-rules-in-launch.html) verwendet und sollten nicht mit dem [`eventType`-Feld in XDM](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=de) verwechselt werden.

## [!UICONTROL Abschluss des Ereignisses senden]

In der Regel enthält Ihre Eigenschaft eine oder mehrere Regeln, die die Aktion [[!UICONTROL Ereignis senden] verwenden,](action-types.md#send-event), um Ereignisse an Adobe Experience Platform Edge Network zu senden. Jedes Mal, wenn ein Ereignis an Edge Network gesendet wird, wird eine Antwort mit nützlichen Daten an den Browser zurückgegeben. Ohne den Ereignistyp [!UICONTROL Ereignis-Abschluss senden] hätten Sie keinen Zugriff auf diese zurückgegebenen Daten.

Um auf die zurückgegebenen Daten zuzugreifen, erstellen Sie eine separate Regel und fügen Sie dann ein [!UICONTROL Ereignis &quot;Ereignisbeendigung senden]&quot;zur Regel hinzu. Diese Regel wird jedes Mal ausgelöst, wenn eine erfolgreiche Antwort vom Server als Ergebnis einer [!UICONTROL Ereignis senden] -Aktion empfangen wird.

Wenn ein [!UICONTROL Ereignis &quot;Ereignisbeendigung senden]&quot;eine Regel Trigger, werden vom Server zurückgegebene Daten bereitgestellt, die für die Ausführung bestimmter Aufgaben nützlich sein können. In der Regel fügen Sie eine Aktion [!UICONTROL Benutzerspezifischer Code] (aus der [!UICONTROL Core]-Erweiterung) zu derselben Regel hinzu, die das Ereignis [!UICONTROL Ereignis-Abschluss senden] enthält. In der Aktion [!UICONTROL Benutzerspezifischer Code] hat Ihr benutzerdefinierter Code Zugriff auf eine Variable namens `event`. Diese Variable `event` enthält die vom Server zurückgegebenen Daten.

Ihre Regel für die Verarbeitung von Daten, die vom Edge Network zurückgegeben werden, könnte in etwa so aussehen:

![](./assets/send-event-complete.png)

Im Folgenden finden Sie einige Beispiele für die Ausführung bestimmter Aufgaben mithilfe der Aktion [!UICONTROL Benutzerspezifischer Code] in dieser Regel.

### Manuelles Rendern personalisierter Inhalte

In der Aktion &quot;Benutzerspezifischer Code&quot;, die sich in der Regel für die Verarbeitung von Antwortdaten befindet, können Sie auf vom Server zurückgegebene Personalisierungsvorschläge zugreifen. Geben Sie dazu den folgenden benutzerdefinierten Code ein:

```javascript
var propositions = event.propositions;
```

Wenn `event.propositions` vorhanden ist, handelt es sich um ein Array, das Personalisierungspropositionsobjekte enthält. Die im Array enthaltenen Vorschläge werden größtenteils danach bestimmt, wie das Ereignis an den Server gesendet wurde.

Angenommen, Sie haben für dieses erste Szenario das Kontrollkästchen [!UICONTROL Renderentscheidungen] nicht aktiviert und keine [!UICONTROL Entscheidungsbereiche] innerhalb der [!UICONTROL Ereignis senden]-Aktion angegeben, die für das Senden des Ereignisses verantwortlich ist.

![img.png](assets/send-event-render-unchecked-without-scopes.png)

In diesem Beispiel enthält das Array `propositions` nur Vorschläge für das Ereignis, die für die automatische Wiedergabe geeignet sind.

Das `propositions`-Array könnte in etwa wie im folgenden Beispiel aussehen:

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

Beim Senden des Ereignisses wurde das Kontrollkästchen [!UICONTROL Renderentscheidungen] nicht aktiviert, sodass das SDK nicht versucht hat, automatisch Inhalte zu rendern. Das SDK hat jedoch weiterhin automatisch die Inhalte abgerufen, die für das automatische Rendering infrage kommen, und Ihnen zur manuellen Wiedergabe bereitgestellt, sofern dies gewünscht ist. Beachten Sie, dass für jedes Vorschlagsobjekt die Eigenschaft `renderAttempted` auf `false` festgelegt ist.

Hätten Sie beim Senden des Ereignisses stattdessen das Kontrollkästchen [!UICONTROL Renderentscheidungen] aktiviert, hätte das SDK versucht, alle Vorschläge wiederzugeben, die für das automatische Rendering infrage kommen. Daher wird für jedes der Vorschlagsobjekte die Eigenschaft `renderAttempted` auf `true` gesetzt. In diesem Fall müssen diese Vorschläge nicht manuell gerendert werden.

Bisher haben Sie sich nur mit Personalisierungsinhalten befasst, die für die automatische Wiedergabe geeignet sind (z. B. mit Inhalten, die im Visual Experience Composer von Adobe Target erstellt wurden). Um Personalisierungsinhalte abzurufen, die für das automatische Rendering nicht _infrage kommen, fordern Sie den Inhalt an, indem Sie mithilfe des Felds [!UICONTROL Entscheidungsbereiche] in der Aktion [!UICONTROL Ereignis senden] Entscheidungsbereiche angeben._ Ein Perimeter ist eine Zeichenfolge, die einen bestimmten Vorschlag identifiziert, den Sie vom Server abrufen möchten.

Die Aktion [!UICONTROL Ereignis senden] würde wie folgt aussehen:

![img.png](assets/send-event-render-unchecked-with-scopes.png)

In diesem Beispiel werden Vorschläge, die dem Perimeter `salutation` oder `discount` entsprechen, zurückgegeben und in das Array `propositions` aufgenommen. Beachten Sie, dass Vorschläge, die für das automatische Rendering infrage kommen, weiterhin im Array `propositions` enthalten sind, unabhängig davon, wie Sie die Felder [!UICONTROL Renderentscheidungen] oder [!UICONTROL Entscheidungsbereiche] in der Aktion [!UICONTROL Ereignis senden] konfigurieren. Das `propositions` -Array würde in diesem Fall in etwa wie im folgenden Beispiel aussehen:

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

An dieser Stelle können Sie den Vorschlagsinhalt nach Bedarf rendern. In diesem Beispiel handelt es sich bei dem Vorschlag, der mit dem Perimeter `discount` übereinstimmt, um einen HTML-Vorschlag, der mit dem formularbasierten Experience Composer von Adobe Target erstellt wurde. Angenommen, Sie haben ein Element auf Ihrer Seite mit der Kennung `daily-special` und möchten den Inhalt aus dem Vorschlag `discount` in das Element `daily-special` rendern. Gehen Sie folgendermaßen vor:

1. Entpacken Sie Vorschläge aus dem `event` -Objekt.
1. Durchlaufen Sie jeden Vorschlag und suchen Sie nach dem Vorschlag mit einem Umfang von `discount`.
1. Wenn Sie einen Vorschlag finden, durchlaufen Sie jedes Element im Vorschlag und suchen Sie nach dem Element, das HTML-Inhalt ist. (Es ist besser zu überprüfen als anzunehmen.)
1. Wenn Sie ein Element mit HTML-Inhalt finden, suchen Sie das Element `daily-special` auf der Seite und ersetzen Sie dessen HTML durch den personalisierten Inhalt.

Ihr benutzerspezifischer Code innerhalb der Aktion [!UICONTROL Benutzerspezifischer Code] kann wie folgt aussehen:

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

Zu den von Adobe Target zurückgegebenen Personalisierungsinhalten gehören [Antwort-Token](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html), die Details zu Aktivität, Angebot, Erlebnis, Benutzerprofil, Geo-Informationen und mehr enthalten. Diese Details können für Drittanbieter-Tools freigegeben oder zum Debugging verwendet werden. Antwort-Token können in der Benutzeroberfläche von Adobe Target konfiguriert werden.

In der Aktion &quot;Benutzerspezifischer Code&quot;, die sich in der Regel für die Verarbeitung von Antwortdaten befindet, können Sie auf vom Server zurückgegebene Personalisierungsvorschläge zugreifen. Geben Sie dazu den folgenden benutzerdefinierten Code ein:

```javascript
var propositions = event.propositions;
```

Wenn `event.propositions` vorhanden ist, handelt es sich um ein Array, das Personalisierungspropositionsobjekte enthält. Weitere Informationen zum Inhalt von `result.propositions` finden Sie unter [Manuelles Rendern personalisierter Inhalte](#manually-render-personalized-content) .

Angenommen, Sie möchten alle Aktivitätsnamen aus allen Vorschlägen erfassen, die automatisch vom Web SDK gerendert wurden, und sie in ein einzelnes Array übertragen. Sie können dann das einzelne Array an einen Drittanbieter senden. Schreiben Sie in diesem Fall benutzerdefinierten Code in die Aktion [!UICONTROL Benutzerspezifischer Code] in:

1. Entpacken Sie Vorschläge aus dem `event` -Objekt.
1. Durchlaufen Sie jeden Vorschlag.
1. Bestimmen Sie, ob das SDK den Vorschlag wiedergegeben hat.
1. Falls ja, durchlaufen Sie jedes Element des Vorschlags.
1. Rufen Sie den Aktivitätsnamen aus der `meta` -Eigenschaft ab, bei der es sich um ein Objekt mit Antwort-Token handelt.
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
