---
title: Installieren des Adobe Experience Platform Web SDK
seo-title: Adobe Experience Platform Web SDK – Installieren des SDK
description: Erfahren Sie, wie Sie das Experience Platform Web SDK installieren.
seo-description: Erfahren Sie, wie Sie das Experience Platform Web SDK installieren.
translation-type: tm+mt
source-git-commit: e0dee4e39143ae9d7f5e4aaf9c352555f1c7f5d0
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 87%

---


# Installieren des SDK

Das Adobe Experience Platform Web SDK steht Ihnen in einem Content Versand-Netzwerk (CDN) zur Verfügung. Sie können auf diese Datei verweisen oder sie herunterladen und in Ihrer eigenen Infrastruktur hosten. Es ist in einer minimierten und nicht-minimierten Version verfügbar. Die nicht minimierte Version ist hilfreich zum Debugging.

[https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js](https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js)[https://cdn1.adoberesources.net/alloy/1.0.0/alloy.js](https://cdn1.adoberesources.net/alloy/1.0.0/alloy.js)

## Code hinzufügen

Der erste Schritt bei der Implementierung des Adobe Experience Platform Web SDK besteht darin, den folgenden „Basis-Code“ so weit wie möglich in das `<head>`-Tag Ihres HTML-Codes einzufügen:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js" async></script>
```

Der Basis-Code erstellt eine globale Funktion namens `alloy`. Verwenden Sie diese Funktion, um mit dem SDK zu interagieren. Wenn Sie der globalen Funktion einen anderen Namen geben möchten, können Sie den `alloy`-Namen wie folgt ändern:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js" async></script>
```

In diesem Beispiel wird die globale Funktion in `mycustomname` anstatt `alloy` umbenannt.

>[!IMPORTANT]
>Um potenzielle Probleme zu vermeiden, verwenden Sie einen Namen, der mindestens ein Zeichen enthält, das keine Ziffer ist und nicht mit dem Namen einer Eigenschaft in Konflikt steht, die bereits unter `window` gefunden wurde.

Dieser Basis-Code lädt neben der Erstellung einer globalen Funktion auch zusätzlichen Code, der in einer externen Datei \(`alloy.js`\) enthalten ist, die auf einem Server gehostet wird. Standardmäßig wird dieser Code asynchron geladen, damit Ihre Web-Seite so leistungsfähig wie möglich ist. Dies ist die empfohlene Implementierung.

## Unterstützen von Internet Explorer

Dieses SDK nutzt Promises, um die Fertigstellung asynchroner Aufgaben zu kommunizieren. Die vom SDK verwendete Implementierung von [Promises](https://developer.mozilla.org/de-DE/docs/Web/JavaScript/Reference/Global_Objects/Promise) wird nativ von allen Ziel-Browsern mit Ausnahme von Internet Explorer unterstützt. Um das SDK in Internet Explorer verwenden zu können, benötigen Sie ein `window.Promise`-[Polyfill](https://remysharp.com/2010/10/08/what-is-a-polyfill).

So stellen Sie fest, ob Sie bereits über ein `window.Promise`-Polyfill verfügen:

1. Öffnen Sie Ihre Website in Internet Explorer.
1. Öffnen Sie die Debugging-Konsole des Browsers.
1. Geben Sie `window.Promise` in die Konsole ein und drücken Sie die Eingabetaste.

Wenn etwas anderes als `undefined` angezeigt wird, verfügen Sie vermutlich bereits über ein `window.Promise`-Polyfill. Eine weitere Möglichkeit, um festzustellen, ob ein `window.Promise`-Polyfill vorliegt, ist das Laden Ihrer Website nach Abschluss der oben genannten Installationsanweisungen. Wenn das SDK einen Fehler ausgibt, in dem ein Promise erwähnt wird, verfügen Sie vermutlich über kein `window.Promise`-Polyfill.

Wenn Sie festgestellt haben, dass Sie ein `window.Promise`-Polyfill benötigen, fügen Sie das folgende Skript-Tag über dem zuvor bereitgestellten Basis-Code ein:

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

Dadurch wird ein Skript geladen, das sicherstellt, dass `window.Promise` eine gültige Implementierung des Promise ist.

## Synchrones Laden der JavaScript-Datei

Wie bereits erläutert, lädt der Basis-Code, den Sie kopiert und in den HTML-Code Ihrer Website eingefügt haben, eine externe Datei mit zusätzlichem Code. Dieser zusätzliche Code enthält die Kernfunktionalität des SDK. Jeder Befehl, den Sie ausführen möchten, während diese Datei geladen wird, wird in die Warteschlange gestellt und nach dem Laden der Datei verarbeitet. Dies ist die leistungsstärkste Installationsmethode.

Unter bestimmten Umständen möchten Sie die Datei jedoch möglicherweise synchron laden \(weitere Details zu diesen Umständen werden später dokumentiert\). Dadurch wird verhindert, dass der Rest des HTML-Dokuments vom Browser analysiert und gerendert wird, bis die externe Datei geladen und ausgeführt wurde. Diese zusätzliche Verzögerung vor der Anzeige von Primärinhalten für Nutzer wird in der Regel nicht empfohlen, kann aber je nach den Umständen sinnvoll sein.

Um die Datei synchron statt asynchron zu laden, entfernen Sie das `async`-Attribut aus dem zweiten `script`-Tag, wie nachstehend dargestellt:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js"></script>
```
