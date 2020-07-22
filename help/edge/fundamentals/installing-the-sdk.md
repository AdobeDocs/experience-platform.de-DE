---
title: Installieren des Adobe Experience Platform Web SDK
seo-title: Adobe Experience Platform Web SDK – Installieren des SDK
description: Erfahren Sie, wie Sie das Experience Platform Web SDK installieren.
seo-description: Erfahren Sie, wie Sie das Experience Platform Web SDK installieren.
translation-type: tm+mt
source-git-commit: c5afced244c661b0ec0bcf0109191a2dacf886aa
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 70%

---


# Installieren des SDK {#installing-the-sdk}

Die Adobe Experience Platform [!DNL Web SDK] steht Ihnen in einem Content Versand-Netzwerk (CDN) zur Verfügung. Sie können auf diese Datei verweisen oder sie herunterladen und in Ihrer eigenen Infrastruktur hosten. Es ist in einer minimierten und nicht-minimierten Version verfügbar. Die nicht minimierte Version ist hilfreich zum Debugging.

* Minimierte Version: [https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js](https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js)
* Nicht minimierte Version: [https://cdn1.adoberesources.net/alloy/1.0.0/alloy.js](https://cdn1.adoberesources.net/alloy/1.0.0/alloy.js)

## Code hinzufügen {#adding-the-code}

The first step in implementing the Adobe Experience Platform [!DNL Web SDK] is to copy and paste the following &quot;base code&quot; as high as possible in the `<head>` tag of your HTML:

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

## Unterstützen von Internet Explorer {#support-internet-explore}

Dieses SDK nutzt Promises, um die Fertigstellung asynchroner Aufgaben zu kommunizieren. The [Promise](https://developer.mozilla.org/de-DE/docs/Web/JavaScript/Reference/Global_Objects/Promise) implementation used by the SDK is natively supported by all target browsers except [!DNL Internet Explorer]. To use the SDK on [!DNL Internet Explorer], you need to have `window.Promise` [polyfilled](https://remysharp.com/2010/10/08/what-is-a-polyfill).

So stellen Sie fest, ob Sie bereits über ein `window.Promise`-Polyfill verfügen:

1. Open your website in [!DNL Internet Explorer].
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
>Wenn Sie sich dafür entscheiden, eine andere Promise-Implementierung zu laden, stellen Sie sicher, dass sie unterstützt `Promise.prototype.finally`.

## Synchrones Laden der JavaScript-Datei {#loading-javascript-synchronously}

As explained in the section [Adding the code](#adding-the-code), the base code you have copied and pasted into your website&#39;s HTML loads an external file with additional code. Dieser zusätzliche Code enthält die Kernfunktionalität des SDK. Jeder Befehl, den Sie ausführen möchten, während diese Datei geladen wird, wird in die Warteschlange gestellt und nach dem Laden der Datei verarbeitet. Dies ist die leistungsstärkste Installationsmethode.

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
