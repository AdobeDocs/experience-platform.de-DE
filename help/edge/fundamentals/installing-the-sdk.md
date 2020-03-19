---
title: Installieren des Adobe Experience Platform Web SDK
seo-title: Adobe Experience Platform Web SDK zum Installieren des SDK
description: Erfahren Sie, wie Sie das Experience Platform Web SDK installieren.
seo-description: Erfahren Sie, wie Sie das Experience Platform Web SDK installieren.
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Installieren des SDK

>[!IMPORTANT]
>
>Das Adobe Experience Platform Web SDK befindet sich derzeit in der Betaphase und steht nicht allen Benutzern zur Verfügung. Dokumentation und Funktionalität können sich ändern.

Der erste Schritt bei der Implementierung des Adobe Experience Platform Web SDK besteht darin, den folgenden &quot;Basiscode&quot;so weit wie möglich in das `<head>` Tag Ihres HTML-Codes zu kopieren und einzufügen:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="alloy.js" async></script>
```

Der Basiscode erstellt eine globale Funktion namens `alloy`. Verwenden Sie diese Funktion, um mit dem SDK zu interagieren. Wenn Sie der globalen Funktion einen anderen Namen geben möchten, können Sie den `alloy` Namen wie folgt ändern:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="alloy.js" async></script>
```

In diesem Beispiel wird die globale Funktion umbenannt `mycustomname`, anstatt `alloy`.

>[!IMPORTANT]
>Um potenzielle Probleme zu vermeiden, verwenden Sie einen Namen, der mindestens ein Zeichen enthält, das keine Ziffer ist und nicht mit dem Namen einer Eigenschaft in Konflikt steht, die bereits auf gefunden wurde `window`.

Dieser Basiscode lädt neben der Erstellung einer globalen Funktion auch zusätzlichen Code, der in einer externen Datei \(`alloy.js`\) enthalten ist, die auf einem Server gehostet wird. Standardmäßig wird dieser Code asynchron geladen, damit Ihre Webseite so leistungsfähig wie möglich ist. Dies ist die empfohlene Implementierung.

## Internet Explorer wird unterstützt

Dieses SDK nutzt Versprechungen, um die Fertigstellung asynchroner Aufgaben zu kommunizieren. Die vom SDK verwendete Implementierung von [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) wird nativ von allen Browsern der Zielgruppe mit Ausnahme von Internet Explorer unterstützt. Um das SDK in Internet Explorer verwenden zu können, müssen Sie über eine `window.Promise` Mehrfachbelegung [](https://remysharp.com/2010/10/08/what-is-a-polyfill)verfügen.

So stellen Sie fest, ob Sie bereits `window.Promise` polygefüllt haben:

1. Öffnen Sie Ihre Website in Internet Explorer.
1. Öffnen Sie die Debugging-Konsole des Browsers.
1. Geben Sie `window.Promise` in die Konsole ein und drücken Sie dann die Eingabetaste.

Wenn etwas Anderes als `undefined` angezeigt wird, haben Sie wahrscheinlich bereits mehrfach gefüllt `window.Promise`. Eine weitere Möglichkeit, um festzustellen, ob Polygefüllt `window.Promise` ist, ist das Laden Ihrer Website nach Abschluss der oben genannten Installationsanweisungen. Wenn das SDK einen Fehler ausgibt, der etwas zu einem Versprechen erwähnt, haben Sie wahrscheinlich keine Polygefüllt `window.Promise`.

Wenn Sie festgestellt haben, dass Polyfill ausgefüllt werden muss, fügen Sie das folgende Skript-Tag über dem zuvor bereitgestellten Basiscode ein: `window.Promise`

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

Dadurch wird ein Skript geladen, das sicherstellt, dass es sich um eine gültige Implementierung des Versprechens `window.Promise` handelt.

## JavaScript-Datei synchron laden

Wie bereits erläutert, lädt der Basiscode, den Sie kopiert und in den HTML-Code Ihrer Website eingefügt haben, eine externe Datei mit zusätzlichem Code. Dieser zusätzliche Code enthält die Kernfunktionalität des SDK. Jeder Befehl, den Sie ausführen möchten, während diese Datei geladen wird, wird in die Warteschlange gestellt und nach dem Laden der Datei verarbeitet. Dies ist die leistungsstärkste Installationsmethode.

Unter bestimmten Umständen möchten Sie die Datei jedoch möglicherweise synchron laden \(weitere Details zu diesen Umständen werden später dokumentiert\). Dadurch wird verhindert, dass der Rest des HTML-Dokuments vom Browser analysiert und gerendert wird, bis die externe Datei geladen und ausgeführt wurde. Diese zusätzliche Verzögerung vor der Anzeige von Primärinhalten für Benutzer wird in der Regel nicht empfohlen, kann aber je nach den Umständen sinnvoll sein.

Um die Datei synchron statt asynchron zu laden, entfernen Sie das `async` Attribut aus dem zweiten `script` -Tag, wie unten dargestellt:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="alloy.js"></script>
```
