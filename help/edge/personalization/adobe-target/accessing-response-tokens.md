---
title: Zugriff auf Antwort-Token mit dem Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie mit dem Adobe Experience Platform Web SDK auf Antwort-Token zugreifen können.
keywords: Personalisierung;Target;adobe target;renderDecisions;sendEvent;DecisionScopes;result.Decisions,response tokens;
exl-id: fc9d552a-29ba-4693-9ee2-599c7bc76cdf
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 2%

---

# Zugriff auf Antwort-Token

Von Adobe Target zurückgegebene Personalisierungsinhalte umfassen [Antwort-Token](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html), die Details zur Aktivität, zum Angebot, zum Erlebnis, zum Benutzerprofil, zu geografischen Informationen und mehr enthalten. Diese Details können für Drittanbieter-Tools freigegeben oder zum Debugging verwendet werden. Antwort-Token können in der Benutzeroberfläche von Adobe Target konfiguriert werden.

Stellen Sie beim Senden eines Ereignisses eine Rückruffunktion bereit, um auf beliebige Personalisierungsinhalte zuzugreifen. Dieser Rückruf wird aufgerufen, nachdem das SDK eine erfolgreiche Antwort vom Server erhält. Ihr Rückruf wird mit einem `result` -Objekt, das eine `propositions` -Eigenschaft, die alle zurückgegebenen Personalisierungsinhalte enthält. Nachfolgend finden Sie ein Beispiel für die Bereitstellung einer Callback-Funktion.

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions
    }
  });
```

In diesem Beispiel `result.propositions`, sofern vorhanden, ist ein Array mit Personalisierungsvorschlägen für das Ereignis. Siehe [Rendern von Personalisierungsinhalten](../rendering-personalization-content.md) für weitere Informationen über den Inhalt von `result.propositions`.

Angenommen, Sie möchten alle Aktivitätsnamen aus allen Vorschlägen erfassen, die automatisch vom Web SDK gerendert wurden, und sie in ein einzelnes Array übertragen. Sie können dann das einzelne Array an einen Drittanbieter senden. In diesem Fall:

1. Entnehmen Sie Vorschläge aus dem `result` -Objekt.
1. Durchlaufen Sie jeden Vorschlag.
1. Bestimmen Sie, ob das SDK den Vorschlag wiedergegeben hat.
1. Falls ja, durchlaufen Sie jedes Element des Vorschlags.
1. Rufen Sie den Aktivitätsnamen aus dem `meta` -Eigenschaft, ein Objekt, das Antwort-Token enthält.
1. Ziehen Sie den Namen der Aktivität in ein Array.
1. Senden Sie die Aktivitätsnamen an einen Drittanbieter.

Ihr Code würde wie folgt aussehen:

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
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
  });
```
