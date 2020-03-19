---
title: Rendern von personalisiertem Inhalt
seo-title: Adobe Experience Platform Web SDK Rendering personalisierter Inhalte
description: Erfahren Sie, wie Sie personalisierte Inhalte mit dem Experience Platform Web SDK wiedergeben
seo-description: Erfahren Sie, wie Sie personalisierte Inhalte mit dem Experience Platform Web SDK wiedergeben
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Rendern personalisierter Inhalte

>[!IMPORTANT]
>
>Das Adobe Experience Platform Web SDK befindet sich derzeit in der Betaphase und steht nicht allen Benutzern zur Verfügung. Dokumentation und Funktionalität können sich ändern.

Das SDK rendert automatisch personalisierte Inhalte, wenn Sie ein Ereignis an den Server senden und `viewStart` als `true` Option auf dem Ereignis festlegen.

```javascript
alloy("event", {
  "viewStart": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

Die Wiedergabe personalisierter Inhalte erfolgt asynchron, sodass keine Annahme vorliegt, wenn ein bestimmtes Inhaltselement Teil der Seite ist.

## Verwalten des Flackerns

Beim Versuch, Personalisierungsinhalte zu rendern, muss das SDK sicherstellen, dass kein Flimmern auftritt. Beim Flackern, auch FOOC (Flash of Original Content) genannt, wird ein Originalinhalt kurz angezeigt, bevor die Alternative während des Tests oder der Personalisierung angezeigt wird. Das SDK versucht, CSS-Stile auf Elemente der Seite anzuwenden, um sicherzustellen, dass diese Elemente ausgeblendet werden, bis der Personalisierungsinhalt erfolgreich wiedergegeben wird.

Die Flimmerverwaltungsfunktion umfasst einige Phasen:

1. Ausblenden
1. Vorverarbeitung
1. Rendering

### Ausblenden

Während der Ausblendephase verwendet das SDK die `prehidingStyle` Konfigurationsoption, um ein HTML-Tag zu erstellen und es an das DOM anzuhängen, um sicherzustellen, dass große Teile der Seite ausgeblendet werden. Wenn Sie sich nicht sicher sind, welche Teile der Seite personalisiert werden, sollten Sie `prehidingStyle` auf `body { opacity: 0 !important }`. Dadurch wird sichergestellt, dass die gesamte Seite ausgeblendet wird. Dies führt jedoch zu einer schlechteren Seitenwiedergabeleistung, die von Tools wie Lighthouse, Webseitentests usw. gemeldet wird. Um die beste Seitenwiedergabeleistung zu erzielen, wird empfohlen, eine Liste von Seitenelementen `prehidingStyle` zu erstellen, die die Seitenabschnitte enthalten, die personalisiert werden.

Wenn Sie eine HTML-Seite wie die unten stehende haben und Sie wissen, dass nur `bar` und `bazz` Container-Elemente jemals personalisiert werden:

```html
<html>
  <head>
  </head>
  <body>
    <div id="foo">
      Foo foo foo
    </div>

    <div id="bar">
      Bar bar bar
    </div>

    <div id="bazz">
      Bazz bazz bazz
    </div>
  </body>
</html>
```

Dann `prehidingStyle` sollte die Einstellung auf etwas wie `#bar, #bazz { opacity: 0 !important }`.

### Vorverarbeitung

Die Phase der Vorverarbeitung beginnt, sobald das SDK die personalisierten Inhalte vom Server erhalten hat. Während dieser Phase wird die Antwort vorverarbeitet, um sicherzustellen, dass Elemente, die personalisierte Inhalte enthalten müssen, ausgeblendet werden. Nachdem diese Elemente ausgeblendet wurden, wird das HTML-Tag, das anhand der `prehidingStyle` Konfigurationsoption erstellt wurde, entfernt und der HTML-Textkörper oder die verborgenen Container-Elemente werden angezeigt.

### Rendering

Nachdem der gesamte Personalisierungsinhalt erfolgreich wiedergegeben wurde oder ein Fehler auftrat, werden alle zuvor ausgeblendeten Elemente angezeigt, um sicherzustellen, dass keine ausgeblendeten Elemente auf der Seite vorhanden sind, die vom SDK ausgeblendet wurden.

## Verwalten des Flackerns beim asynchronen Laden des SDK

Es wird empfohlen, das SDK immer asynchron zu laden, um die beste Seitenwiedergabeleistung zu erhalten. Dies hat jedoch einige Auswirkungen auf die Wiedergabe personalisierter Inhalte. Wenn das SDK asynchron geladen wird, muss das Prähiding-Snippet verwendet werden. Das Ausblendungsfragment muss vor dem SDK auf der HTML-Seite hinzugefügt werden. Hier ein Beispielfragment, das den gesamten Körper verbirgt:

```html
<script>
  !function(e,a,n,t){
    if (a) return;
    var i=e.head;if(i){
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),
    setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

Um sicherzustellen, dass der HTML-Textkörper oder die Container-Elemente über einen längeren Zeitraum nicht ausgeblendet werden, verwendet das Ausblendungsfragment einen Timer, der das Codefragment standardmäßig nach `3000` Millisekunden entfernt. Die `3000` Millisekunden sind die maximale Wartezeit. Wenn die Antwort vom Server früher empfangen und verarbeitet wurde, wird das HTML-Tag, das das Ausblenden verhindert, so bald wie möglich entfernt.
