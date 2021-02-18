---
title: Adobe Experience Platform Web SDK installieren
description: Erfahren Sie, wie Sie das Experience Platform Web SDK installieren.
keywords: Web-SDK-Installation;Installieren von Web-SDK;Internet-Explorer;Versprechen;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 61%

---


# SDK {#installing-the-sdk} installieren

Die bevorzugte Methode zur Verwendung des Adobe Experience Platform Web SDK ist [Adobe Experience Platform Launch](http://launch.adobe.com/de). Suchen Sie im Erweiterungskatalog nach `AEP Web SDK`, installieren Sie die Erweiterung und konfigurieren Sie sie.

Adobe Experience Platform Web SDK steht Ihnen auch als CDN zur Verfügung. Sie können auf diese Datei verweisen oder sie herunterladen und in Ihrer eigenen Infrastruktur hosten. Es ist in einer minimierten und nicht-minimierten Version verfügbar. Die nicht minimierte Version ist hilfreich zum Debugging.

URL-Struktur: https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js OR benzyl.js für die nicht minimierte Version.

Beispiel:

* Minimiert: [https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js)
* Nicht minimiert: [https://cdn1.adoberesources.net/alloy/2.3.0/alloy.js](https://cdn1.adoberesources.net/alloy/2.3.0/alloy.js)

## Code {#adding-the-code} hinzufügen

Der erste Schritt bei der Implementierung von Adobe Experience Platform [!DNL Web SDK] besteht darin, den folgenden &quot;Basiscode&quot;so hoch wie möglich im `<head>`-Tag Ihres HTML-Codes zu kopieren und einzufügen:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js" async></script>
```

Der Basis-Code erstellt eine globale Funktion namens `alloy`. Verwenden Sie diese Funktion, um mit dem SDK zu interagieren. Wenn Sie der globalen Funktion einen anderen Namen geben möchten, können Sie den `alloy`-Namen wie folgt ändern:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js" async></script>
```

In diesem Beispiel wird die globale Funktion in `mycustomname` anstatt `alloy` umbenannt.

>[!IMPORTANT]
>
>Um potenzielle Probleme zu vermeiden, verwenden Sie einen Namen, der mindestens ein Zeichen enthält, das keine Ziffer ist und nicht mit dem Namen einer Eigenschaft in Konflikt steht, die bereits unter `window` gefunden wurde.

Dieser Basis-Code lädt neben der Erstellung einer globalen Funktion auch zusätzlichen Code, der in einer externen Datei \(`alloy.js`\) enthalten ist, die auf einem Server gehostet wird. Standardmäßig wird dieser Code asynchron geladen, damit Ihre Web-Seite so leistungsfähig wie möglich ist. Dies ist die empfohlene Implementierung.

## Unterstützen von Internet Explorer {#support-internet-explore}

Dieses SDK nutzt Promises, um die Fertigstellung asynchroner Aufgaben zu kommunizieren. Die vom SDK verwendete Implementierung von [Promise](https://developer.mozilla.org/de-DE/docs/Web/JavaScript/Reference/Global_Objects/Promise) wird nativ von allen Browsern der Zielgruppe mit Ausnahme von [!DNL Internet Explorer] unterstützt. Um das SDK für [!DNL Internet Explorer] zu verwenden, müssen Sie `window.Promise` [polygefüllt](https://remysharp.com/2010/10/08/what-is-a-polyfill) haben.

So stellen Sie fest, ob Sie bereits über ein `window.Promise`-Polyfill verfügen:

1. Öffnen Sie Ihre Website in [!DNL Internet Explorer].
1. Öffnen Sie die Debugging-Konsole des Browsers.
1. Geben Sie `window.Promise` in die Konsole ein und drücken Sie die Eingabetaste.

Wenn etwas anderes als `undefined` angezeigt wird, verfügen Sie vermutlich bereits über ein `window.Promise`-Polyfill. Eine weitere Möglichkeit, um festzustellen, ob ein `window.Promise`-Polyfill vorliegt, ist das Laden Ihrer Website nach Abschluss der oben genannten Installationsanweisungen. Wenn das SDK einen Fehler ausgibt, in dem ein Promise erwähnt wird, verfügen Sie vermutlich über kein `window.Promise`-Polyfill.

Wenn Sie festgestellt haben, dass Sie ein `window.Promise`-Polyfill benötigen, fügen Sie das folgende Skript-Tag über dem zuvor bereitgestellten Basis-Code ein:

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

Dadurch wird ein Skript geladen, das sicherstellt, dass `window.Promise` eine gültige Implementierung des Promise ist.

>[!NOTE]
>
>Wenn Sie eine andere Promise-Implementierung laden möchten, stellen Sie sicher, dass `Promise.prototype.finally` unterstützt wird.

## Synchrones Laden der JavaScript-Datei {#loading-javascript-synchronously}

Wie im Abschnitt [Code](#adding-the-code) hinzugefügt, lädt der Basiscode, den Sie kopiert und in den HTML Ihrer Website eingefügt haben, eine externe Datei mit zusätzlichem Code. Dieser zusätzliche Code enthält die Kernfunktionalität des SDK. Jeder Befehl, den Sie ausführen möchten, während diese Datei geladen wird, wird in die Warteschlange gestellt und nach dem Laden der Datei verarbeitet. Dies ist die leistungsstärkste Installationsmethode.

Unter bestimmten Umständen möchten Sie die Datei jedoch möglicherweise synchron laden \(weitere Details zu diesen Umständen werden später dokumentiert\). Dadurch wird verhindert, dass der Rest des HTML-Dokuments vom Browser analysiert und gerendert wird, bis die externe Datei geladen und ausgeführt wurde. Diese zusätzliche Verzögerung vor der Anzeige von Primärinhalten für Nutzer wird in der Regel nicht empfohlen, kann aber je nach den Umständen sinnvoll sein.

Um die Datei synchron statt asynchron zu laden, entfernen Sie das `async`-Attribut aus dem zweiten `script`-Tag, wie nachstehend dargestellt:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js"></script>
```
