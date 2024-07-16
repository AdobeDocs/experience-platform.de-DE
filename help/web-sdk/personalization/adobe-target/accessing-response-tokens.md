---
title: Zugriff auf Antwort-Token mit dem Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie mit dem Adobe Experience Platform Web SDK auf Antwort-Token zugreifen können.
keywords: Personalisierung;Target;adobe target;renderDecisions;sendEvent;DecisionScopes;result.Decisions,response tokens;
exl-id: fc9d552a-29ba-4693-9ee2-599c7bc76cdf
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 1%

---

# Zugriff auf Antwort-Token

Personalization-Inhalte, die von Adobe Target zurückgegeben werden, umfassen [Antwort-Token](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html), d. h. Details zu Aktivität, Angebot, Erlebnis, Benutzerprofil, Geo-Informationen und mehr. Diese Details können für Drittanbieter-Tools freigegeben oder zum Debugging verwendet werden. Antwort-Token können in der Benutzeroberfläche von Adobe Target konfiguriert werden.

Stellen Sie beim Senden eines Ereignisses eine Rückruffunktion bereit, um auf einen beliebigen Personalisierungsinhalt zuzugreifen. Dieser Rückruf wird aufgerufen, nachdem das SDK eine erfolgreiche Antwort vom Server erhält. Ihr Rückruf wird mit einem `result` -Objekt bereitgestellt, das eine `propositions` -Eigenschaft enthalten kann, die alle zurückgegebenen Personalisierungsinhalte enthält. Nachfolgend finden Sie ein Beispiel für die Bereitstellung einer Callback-Funktion.

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

In diesem Beispiel ist `result.propositions`, sofern vorhanden, ein Array, das Personalisierungsvorschläge für das Ereignis enthält. Weitere Informationen zum Inhalt von `result.propositions` finden Sie unter [Rendering personalization content](../rendering-personalization-content.md) .

Angenommen, Sie möchten alle Aktivitätsnamen aus allen Vorschlägen erfassen, die automatisch vom Web SDK gerendert wurden, und sie in ein einzelnes Array übertragen. Sie können dann das einzelne Array an einen Drittanbieter senden. In diesem Fall:

1. Extrahieren Sie Vorschläge aus dem Objekt `result` .
1. Durchlaufen Sie jeden Vorschlag.
1. Bestimmen Sie, ob das SDK den Vorschlag wiedergegeben hat.
1. Falls ja, durchlaufen Sie jedes Element des Vorschlags.
1. Rufen Sie den Aktivitätsnamen aus der Eigenschaft `meta` ab, bei der es sich um ein Objekt mit Antwort-Token handelt.
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
