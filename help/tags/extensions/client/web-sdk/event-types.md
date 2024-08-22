---
title: Ereignistypen in der Adobe Experience Platform Web SDK-Erweiterung
description: Erfahren Sie, wie Sie Ereignistypen verwenden, die von der Adobe Experience Platform Web SDK-Erweiterung in Adobe Experience Platform Launch bereitgestellt werden.
solution: Experience Platform
exl-id: b3162406-c5ce-42ec-ab01-af8ac8c63560
source-git-commit: 666e8c6fcccf08d0841c5796677890409b22d794
workflow-type: tm+mt
source-wordcount: '1127'
ht-degree: 0%

---

# Ereignistypen

Auf dieser Seite werden die Adobe Experience Platform-Ereignistypen beschrieben, die von der Adobe Experience Platform Web SDK-Tag-Erweiterung bereitgestellt werden. Diese werden für [Erstellungsregeln](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-rules.html?lang=de) verwendet und sollten nicht mit dem Feld `eventType` im Objekt [`xdm`](/help/web-sdk/commands/sendevent/xdm.md) verwechselt werden.

## [!UICONTROL Ereignis-Abschluss senden]

In der Regel enthält Ihre Eigenschaft eine oder mehrere Regeln, die die Aktion [[!UICONTROL Ereignis senden] ](action-types.md#send-event) verwenden, um Ereignisse an das Adobe Experience Platform-Edge Network zu senden. Jedes Mal, wenn ein Ereignis an Edge Network gesendet wird, wird eine Antwort mit nützlichen Daten an den Browser zurückgegeben. Ohne den Ereignistyp [!UICONTROL Ereignisbeendigung senden] hätten Sie keinen Zugriff auf diese zurückgegebenen Daten.

Um auf die zurückgegebenen Daten zuzugreifen, erstellen Sie eine separate Regel und fügen Sie dann ein [!UICONTROL Ereignis zum Abschluss senden] -Ereignis zur Regel hinzu. Diese Regel wird jedes Mal ausgelöst, wenn eine erfolgreiche Antwort vom Server als Ergebnis einer [!UICONTROL Ereignis senden] -Aktion empfangen wird.

Wenn ein Ereignis vom Typ [!UICONTROL Ereignis zum Abschluss senden] eine Regel Trigger, werden vom Server zurückgegebene Daten bereitgestellt, die für die Ausführung bestimmter Aufgaben nützlich sein können. In der Regel fügen Sie eine Aktion vom Typ [!UICONTROL Benutzerdefinierter Code] (aus der Erweiterung [!UICONTROL Core] ) zu derselben Regel hinzu, die das Ereignis [!UICONTROL Abschluss des Sendeereignisses] enthält. In der Aktion [!UICONTROL Benutzerspezifischer Code] hat Ihr benutzerdefinierter Code Zugriff auf eine Variable namens `event`. Diese `event` -Variable enthält die vom Server zurückgegebenen Daten.

Ihre Regel für die Verarbeitung von Daten, die von Edge Network zurückgegeben werden, könnte in etwa so aussehen:

![](assets/send-event-complete.png)

Im Folgenden finden Sie einige Beispiele für die Ausführung bestimmter Aufgaben mithilfe der Aktion [!UICONTROL Benutzerspezifischer Code] in dieser Regel.

### Manuelles Rendern personalisierter Inhalte

In der Aktion &quot;Benutzerspezifischer Code&quot;, die sich in der Regel für die Verarbeitung von Antwortdaten befindet, können Sie auf vom Server zurückgegebene Personalisierungsvorschläge zugreifen. Geben Sie dazu den folgenden benutzerdefinierten Code ein:

```javascript
var propositions = event.propositions;
```

Wenn `event.propositions` vorhanden ist, handelt es sich um ein Array, das Personalisierungspropositionsobjekte enthält. Die im Array enthaltenen Vorschläge werden größtenteils danach bestimmt, wie das Ereignis an den Server gesendet wurde.

Angenommen, Sie haben für dieses erste Szenario das Kontrollkästchen [!UICONTROL Renderentscheidungen] nicht aktiviert und keine [!UICONTROL Entscheidungsbereiche] innerhalb der Aktion [!UICONTROL Ereignis senden] angegeben, die für das Senden des Ereignisses zuständig ist.

![img.png](assets/send-event-render-unchecked-without-scopes.png)

In diesem Beispiel enthält das Array `propositions` nur Vorschläge für das Ereignis, die für die automatische Wiedergabe geeignet sind.

Das Array `propositions` könnte in etwa wie im folgenden Beispiel aussehen:

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

Wenn Sie beim Senden des Ereignisses stattdessen das Kontrollkästchen [!UICONTROL Renderentscheidungen] angekreuzt hätten, hätte das SDK versucht, alle Vorschläge wiederzugeben, die für das automatische Rendering infrage kommen. Daher würde für jedes der Vorschlagsobjekte seine Eigenschaft `renderAttempted` auf `true` gesetzt. In diesem Fall müssen diese Vorschläge nicht manuell gerendert werden.

Bisher haben Sie sich nur mit Personalisierungsinhalten befasst, die für die automatische Wiedergabe geeignet sind (z. B. mit Inhalten, die im Visual Experience Composer von Adobe Target erstellt wurden). Um Personalisierungsinhalte abzurufen, die nicht für die automatische Wiedergabe geeignet sind, fordern Sie den Inhalt an, indem Sie Entscheidungsbereiche mit dem Feld [!UICONTROL Entscheidungsbereiche] in der Aktion [!UICONTROL Ereignis senden] angeben. __ Ein Perimeter ist eine Zeichenfolge, die einen bestimmten Vorschlag identifiziert, den Sie vom Server abrufen möchten.

Die Aktion [!UICONTROL Ereignis senden] würde wie folgt aussehen:

![img.png](assets/send-event-render-unchecked-with-scopes.png)

In diesem Beispiel werden Vorschläge, die dem Umfang `salutation` oder `discount` entsprechen, zurückgegeben und in das Array `propositions` aufgenommen, wenn sie auf dem Server gefunden werden. Beachten Sie, dass Vorschläge, die für das automatische Rendering infrage kommen, weiterhin im Array `propositions` enthalten sind, unabhängig davon, wie Sie die Felder [!UICONTROL Renderentscheidungen] oder [!UICONTROL Entscheidungsbereiche] in der Aktion [!UICONTROL Ereignis senden] konfigurieren. Das Array `propositions` würde in diesem Fall in etwa wie im folgenden Beispiel aussehen:

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

An dieser Stelle können Sie den Vorschlagsinhalt nach Bedarf rendern. In diesem Beispiel handelt es sich bei dem Vorschlag, der dem `discount` -Bereich entspricht, um einen HTML-Vorschlag, der mit dem formularbasierten Experience Composer von Adobe Target erstellt wurde. Angenommen, Sie haben ein Element auf Ihrer Seite mit der Kennung `daily-special` und möchten den Inhalt aus dem Vorschlag `discount` in das Element `daily-special` rendern. Gehen Sie folgendermaßen vor:

1. Extrahieren Sie Vorschläge aus dem Objekt `event` .
1. Durchlaufen Sie jeden Vorschlag und suchen Sie nach dem Vorschlag mit dem Umfang &quot;`discount`&quot;.
1. Wenn Sie einen Vorschlag finden, durchlaufen Sie jedes Element im Vorschlag, suchen Sie nach dem Element, das HTML-Inhalt ist. (Es ist besser zu überprüfen als anzunehmen.)
1. Wenn Sie ein Element mit HTML-Inhalt finden, suchen Sie das Element `daily-special` auf der Seite und ersetzen Sie dessen HTML durch den personalisierten-Inhalt.

Ihr benutzerdefinierter Code innerhalb der Aktion [!UICONTROL Benutzerspezifischer Code] wird möglicherweise wie folgt angezeigt:

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

Personalization-Inhalte, die von Adobe Target zurückgegeben werden, umfassen [Antwort-Token](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html), d. h. Details zu Aktivität, Angebot, Erlebnis, Benutzerprofil, Geo-Informationen und mehr. Diese Details können für Drittanbieter-Tools freigegeben oder zum Debugging verwendet werden. Antwort-Token können in der Benutzeroberfläche von Adobe Target konfiguriert werden.

In der Aktion &quot;Benutzerspezifischer Code&quot;, die sich in der Regel für die Verarbeitung von Antwortdaten befindet, können Sie auf vom Server zurückgegebene Personalisierungsvorschläge zugreifen. Geben Sie dazu den folgenden benutzerdefinierten Code ein:

```javascript
var propositions = event.propositions;
```

Wenn `event.propositions` vorhanden ist, handelt es sich um ein Array, das Personalisierungspropositionsobjekte enthält. Weitere Informationen zum Inhalt von `result.propositions` finden Sie unter [Manuelles Rendern personalisierter Inhalte](#manually-render-personalized-content) .

Angenommen, Sie möchten alle Aktivitätsnamen aus allen Vorschlägen erfassen, die automatisch vom Web SDK gerendert wurden, und sie in ein einzelnes Array übertragen. Sie können dann das einzelne Array an einen Drittanbieter senden. Schreiben Sie in diesem Fall benutzerdefinierten Code in die Aktion [!UICONTROL Benutzerspezifischer Code] in:

1. Extrahieren Sie Vorschläge aus dem Objekt `event` .
1. Durchlaufen Sie jeden Vorschlag.
1. Bestimmen Sie, ob das SDK den Vorschlag wiedergegeben hat.
1. Falls ja, durchlaufen Sie jedes Element des Vorschlags.
1. Rufen Sie den Aktivitätsnamen aus der Eigenschaft `meta` ab, bei der es sich um ein Objekt mit Antwort-Token handelt.
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

## [!UICONTROL Regelsatzelemente abonnieren] {#subscribe-ruleset-items}

Mit dem Ereignistyp **[!UICONTROL Regelsatzelemente abonnieren]** können Sie Adobe Journey Optimizer-Inhaltskarten für eine Oberfläche abonnieren. Jedes Mal, wenn die Regelsätze ausgewertet werden, erhält der für diesen Befehl bereitgestellte Rückruf ein Ergebnisobjekt mit Vorschlägen, die die Inhaltskartendaten enthalten.

![Bild der Experience Platform-Tags-Benutzeroberfläche mit dem Ereignistyp Regelsatzelemente abonnieren.](assets/subscribe-ruleset-items.png)

Dieser Ereignistyp unterstützt die folgenden konfigurierbaren Eigenschaften:

* **[!UICONTROL Schemas]**: Ein Array von Schemas, für die Sie Inhaltskarten abonnieren möchten. Sie können die Schemata manuell oder durch Angabe eines Datenelements eingeben.
* **[!UICONTROL Oberflächen]**: Ein Array von Oberflächen, für die Sie Inhaltskarten abonnieren möchten. Sie können die Oberflächen manuell oder durch Angabe eines Datenelements aufrufen.
