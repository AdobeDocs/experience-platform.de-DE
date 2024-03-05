---
title: Verwalten von Flackern für personalisierte Erlebnisse mit dem Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie mit dem Adobe Experience Platform Web SDK Flackern bei Benutzererlebnissen verhindern können.
keywords: target;flackern;prehidingStyle;asynchron;asynchron;
exl-id: f4b59109-df7c-471b-9bd6-7082e00c293b
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 53%

---

# Verwalten von Flackern

Beim Versuch, Personalisierungsinhalte zu rendern, muss das SDK sicherstellen, dass kein Flackern auftritt. Beim Flackern, auch FOOC (Flash des Originalinhalts) genannt, wird kurz ein Originalinhalt angezeigt, bevor die Alternative während des Tests/der Personalisierung erscheint. Das SDK versucht, CSS-Stile auf Elemente der Seite anzuwenden, um sicherzustellen, dass diese Elemente ausgeblendet werden, bis der Personalisierungsinhalt erfolgreich gerendert wird.

Wie Sie Flackern verwalten, hängt davon ab, ob Sie das Web SDK synchron oder asynchron bereitstellen. Überprüfen Sie die `<head>` Tag, an dem Sie `alloy.js` oder dem Tag-Lader. Das Vorhandensein der `async` -Attribut im `<script>` -Tag bestimmt, ob das Web-SDK asynchron geladen wird.

```html
<!-- This tag loads synchronously -->
<script src="https://assets.adobedtm.com/[...]/launch-example.min.js"></script>

<!-- This tag loads asynchronously -->
<script src="https://assets.adobedtm.com/[...]/launch-example.min.js" async></script>

<!-- This library loads synchronously -->
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js"></script>

<!-- This library loads asynchronously -->
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js" async></script>
```

## Flackern bei synchronen Bereitstellungen verwalten

Die synchrone Flackerverwaltung ist in drei Phasen unterteilt:

1. Vorabausblenden
1. Vorverarbeitung
1. Rendern

Während **Pre-hiding-Phase** verwendet das SDK die Variable [`prehidingStyle`](../commands/configure/prehidingstyle.md) Konfigurationseigenschaft, um ein HTML-Tag zu erstellen und es an das DOM anzuhängen, um sicherzustellen, dass die gewünschten Seitenabschnitte ausgeblendet sind. Wenn Sie sich nicht sicher sind, welche Teile der Seite personalisiert werden, sollten Sie `prehidingStyle` auf `body { opacity: 0 !important }` einstellen. Dadurch wird sichergestellt, dass die gesamte Seite ausgeblendet wird. Dies hat jedoch den Nachteil, dass die Leistung beim Seiten-Rendering schlechter wird, was von Tools wie Lighthouse, Webseitentests usw. gemeldet wird. Um die beste Performance beim Seiten-Rendering zu erzielen, wird empfohlen, `prehidingStyle` auf eine Liste von Container-Elementen einzustellen, die die Seitenabschnitte enthalten, die personalisiert werden.

Angenommen, Sie haben eine HTML-Seite wie die unten stehende, und Sie wissen nur, dass `bar` und `bazz` Container-Elemente werden immer personalisiert:

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

Sobald das SDK personalisierte Inhalte vom Server erhalten hat, wird die **Vorverarbeitungsphase** beginnt. Während dieser Phase wird die Antwort vorverarbeitet, um sicherzustellen, dass Elemente, die personalisierte Inhalte enthalten müssen, ausgeblendet werden. Nachdem diese Elemente ausgeblendet wurden, wird das HTML-Tag, das anhand der `prehidingStyle`-Konfigurationsoption erstellt wurde, entfernt und der HTML-Textkörper oder die verborgenen Container-Elemente werden angezeigt.

Nachdem der gesamte Personalisierungsinhalt erfolgreich wiedergegeben wurde oder wenn ein Fehler aufgetreten ist, wird die **Renderphase** beginnt. Alle zuvor ausgeblendeten Elemente werden angezeigt, um sicherzustellen, dass keine ausgeblendeten Elemente auf der Seite vorhanden sind, die vom SDK ausgeblendet wurden.

## Flackern bei asynchronen Implementierungen verwalten

Es wird empfohlen, das SDK immer asynchron zu laden, um die beste Performance beim Seiten-Rendering zu erhalten. Dies hat jedoch einige Auswirkungen auf das Rendering personalisierter Inhalte. Wenn das SDK asynchron geladen wird, muss das Vorabausblendungs-Snippet verwendet werden. Das Vorabausblendungs-Snippet muss vor dem SDK auf der HTML-Seite hinzugefügt werden. Hier ein Beispiel-Snippet, das den gesamten Textkörper ausblendet:

```html
<script>
  !function(e,a,n,t){
    if (a) return;
    var i=e.head;if(i){
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),
    setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("adobe_authoring_enabled") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

Um sicherzustellen, dass der HTML-Textkörper oder die Container-Elemente über einen längeren Zeitraum nicht ausgeblendet werden, verwendet das Vorabausblendungs-Snippet einen Timer, der das Snippet standardmäßig nach `3000` Millisekunden entfernt. Die `3000` Millisekunden sind die maximale Wartezeit. Wenn die Antwort vom Server früher empfangen und verarbeitet wurde, wird das HTML-Tag, das das Ausblenden verhindert, so bald wie möglich entfernt.
