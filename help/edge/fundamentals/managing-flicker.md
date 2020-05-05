---
source-git-commit: db4bfec04a1116ce2b6a0be7ca0e8cb2f9639ad6
translation-type: tm+mt

---
# Beheben von Flackern

Beim Versuch, Personalisierungsinhalte zu rendern, muss das SDK sicherstellen, dass kein Flackern auftritt. Beim Flackern, auch FOOC (Flash of Original Content) genannt, wird ein Originalinhalt kurz angezeigt, bevor die Alternative während des Tests/der Personalisierung angezeigt wird. Das SDK versucht, CSS-Stile auf Elemente der Seite anzuwenden, um sicherzustellen, dass diese Elemente ausgeblendet werden, bis der Personalisierungsinhalt erfolgreich gerendert wird.

Die Funktion zum Beheben von Flackern umfasst einige Phasen:

1. Vorabausblenden
1. Vorverarbeitung
1. Rendern

## Vorabausblenden

Während der Vorabausblendungsphase verwendet das SDK die `prehidingStyle`-Konfigurationsoption, um ein HTML-Tag zu erstellen und es an die DOM anzuhängen, um sicherzustellen, dass große Teile der Seite ausgeblendet werden. Wenn Sie sich nicht sicher sind, welche Teile der Seite personalisiert werden, sollten Sie `prehidingStyle` auf `body { opacity: 0 !important }` einstellen. Dadurch wird sichergestellt, dass die gesamte Seite ausgeblendet wird. Dies führt jedoch zu einer schlechteren Seitenwiedergabeleistung, die von Tools wie Lighthouse, Webseitentests usw. gemeldet wird. Um die beste Leistung beim Seiten-Rendering zu erzielen, wird empfohlen, `prehidingStyle` auf eine Liste von Container-Elementen einzustellen, die die Seitenabschnitte enthalten, die personalisiert werden.

Assuming you have an HTML page like the one below and you know that only `bar` and `bazz` container elements will be ever personalized:

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

Dann sollte `prehidingStyle` auf einen Wert wie `#bar, #bazz { opacity: 0 !important }` eingestellt werden.

## Vorverarbeitung

Die Phase der Vorverarbeitung beginnt, sobald das SDK den personalisierten Inhalt vom Server erhalten hat. Während dieser Phase wird die Antwort vorverarbeitet, um sicherzustellen, dass Elemente, die personalisierte Inhalte enthalten müssen, ausgeblendet werden. Nachdem diese Elemente ausgeblendet wurden, wird das HTML-Tag, das anhand der `prehidingStyle`-Konfigurationsoption erstellt wurde, entfernt und der HTML-Textkörper oder die verborgenen Container-Elemente werden angezeigt.

## Rendern

Nachdem der gesamte Personalisierungsinhalt erfolgreich wiedergegeben wurde oder nachdem ein Fehler auftrat, werden alle zuvor ausgeblendeten Elemente angezeigt, um sicherzustellen, dass keine ausgeblendeten Elemente auf der Seite vorhanden sind, die vom SDK ausgeblendet wurden.

## Beheben von Flackern beim asynchronen Laden des SDK

Es wird empfohlen, das SDK immer asynchron zu laden, um die beste Leistung beim Seiten-Rendering zu erhalten. Dies hat jedoch einige Auswirkungen auf das Rendering personalisierter Inhalte. Wenn das SDK asynchron geladen wird, muss das Vorabausblendungs-Snippet verwendet werden. Das Vorabausblendungs-Snippet muss vor dem SDK auf der HTML-Seite hinzugefügt werden. Hier ein Beispiel-Snippet, das den gesamten Textkörper ausblendet:

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

Um sicherzustellen, dass der HTML-Textkörper oder die Container-Elemente über einen längeren Zeitraum nicht ausgeblendet werden, verwendet das Vorabausblendungs-Snippet einen Timer, der das Snippet standardmäßig nach `3000` Millisekunden entfernt. Die `3000` Millisekunden sind die maximale Wartezeit. Wenn die Antwort vom Server früher empfangen und verarbeitet wurde, wird das HTML-Tag, das das Ausblenden verhindert, so bald wie möglich entfernt.
