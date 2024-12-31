---
title: Verwalten von Flackern für personalisierte Erlebnisse mit der Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie das Flackern von Benutzererlebnissen mit der Adobe Experience Platform Web SDK verwalten.
keywords: target;flimmern;prehidingStyle;asynchron;asynchron;
exl-id: f4b59109-df7c-471b-9bd6-7082e00c293b
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 53%

---

# Verwalten von Flackern

Beim Versuch, Personalisierungsinhalte zu rendern, muss das SDK sicherstellen, dass kein Flackern auftritt. Ein Flackern, auch FOOC (Flash des Originalinhalts) genannt, tritt auf, wenn ein Originalinhalt kurz angezeigt wird, bevor die Alternative während des Tests/der Personalisierung angezeigt wird. Das SDK versucht, CSS-Stile auf Elemente der Seite anzuwenden, um sicherzustellen, dass diese Elemente ausgeblendet werden, bis der Personalisierungsinhalt erfolgreich gerendert wird.

Die Verwaltung von Flackern hängt davon ab, ob Sie Web SDK synchron oder asynchron bereitstellen. Überprüfen Sie das `<head>` Tag, in dem Sie `alloy.js` bereitstellen, oder den Tag-Loader. Das Vorhandensein des `async`-Attributs im `<script>`-Tag bestimmt, ob die Web-SDK asynchron geladen wird.

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

## Verwalten von Flackern bei synchronen Bereitstellungen

Die synchrone Flimmerverwaltung ist in drei Phasen unterteilt:

1. Vorabausblenden
1. Vorverarbeitung
1. Rendern

Während der **Ausblendphase** erstellt der SDK mithilfe der [`prehidingStyle`](../commands/configure/prehidingstyle.md)-Konfigurationseigenschaft ein HTML-Stil-Tag und hängt es an das DOM an, um sicherzustellen, dass die gewünschten Abschnitte der Seite ausgeblendet sind. Wenn Sie sich nicht sicher sind, welche Teile der Seite personalisiert werden, sollten Sie `prehidingStyle` auf `body { opacity: 0 !important }` einstellen. Dadurch wird sichergestellt, dass die gesamte Seite ausgeblendet wird. Dies hat jedoch den Nachteil, dass es zu einer schlechteren Rendering-Leistung der Seite führt, die von Tools wie Lighthouse, Web-Seitentests usw. gemeldet wird. Um die beste Performance beim Seiten-Rendering zu erzielen, wird empfohlen, `prehidingStyle` auf eine Liste von Container-Elementen einzustellen, die die Seitenabschnitte enthalten, die personalisiert werden.

Angenommen, Sie verfügen über eine HTML-Seite wie die folgende und Sie wissen, dass nur `bar` und `bazz` Container-Elemente jemals personalisiert werden:

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

Sobald der SDK personalisierte Inhalte vom Server erhalten hat, beginnt **Vorverarbeitungsphase**. Während dieser Phase wird die Antwort vorverarbeitet, um sicherzustellen, dass Elemente, die personalisierte Inhalte enthalten müssen, ausgeblendet werden. Nachdem diese Elemente ausgeblendet wurden, wird das HTML-Tag, das anhand der `prehidingStyle`-Konfigurationsoption erstellt wurde, entfernt und der HTML-Textkörper oder die verborgenen Container-Elemente werden angezeigt.

Nachdem alle Personalisierungsinhalte erfolgreich gerendert wurden oder ein Fehler aufgetreten ist, beginnt die **Rendering-Phase**. Alle zuvor ausgeblendeten Elemente werden angezeigt, um sicherzustellen, dass es auf der Seite keine ausgeblendeten Elemente gibt, die von SDK ausgeblendet wurden.

## Verwalten von Flackern bei asynchronen Bereitstellungen

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
