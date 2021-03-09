---
title: Adobe Experience Platform Web SDK installieren
description: Erfahren Sie, wie Sie das Experience Platform Web SDK installieren.
keywords: Web-SDK-Installation;Installieren von Web-SDK;Internet-Explorer;Versprechen;npm-Paket
translation-type: tm+mt
source-git-commit: 63c0c5cae5ca2800b1f049b2b33e2a6f36ee7255
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 32%

---


# SDK {#installing-the-sdk} installieren

Es werden drei Möglichkeiten zur Verwendung des Adobe Experience Platform Web SDK unterstützt:

1. Die bevorzugte Methode zur Verwendung des Adobe Experience Platform Web SDK ist [Adobe Experience Platform Launch](https://launch.adobe.com/).
1. Adobe Experience Platform Web SDK steht Ihnen auch in einem Content Versand-Netzwerk (CDN) zur Verfügung.
1. Verwenden Sie die NPM-Bibliothek, die EcmaScript 5- und EcmaScript 2015 (ES6)-Module exportiert.

## Option 1: Installieren der Adobe Experience Platform Launch-Erweiterung

Eine Dokumentation zur Adobe Experience Platform Launch-Erweiterung finden Sie in der [Startdokumentation](https://docs.adobe.com/content/help/de-DE/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html)

## Option 2: Installieren der vordefinierten eigenständigen Version

Die vordefinierte Version ist auf einem CDN verfügbar. Sie können die Bibliothek im CDN direkt auf Ihrer Seite referenzieren oder sie herunterladen und in Ihrer eigenen Infrastruktur hosten. Es ist in minimierten und unminimierten Formaten erhältlich. Die nicht minimierte Version ist hilfreich zum Debugging.

URL-Struktur: https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js OR benzyl.js für die nicht minimierte Version.

Beispiel:


* Minimiert: [https://cdn1.adoberesources.net/alloy/2.4.0/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.4.0/alloy.min.js)
* Nicht minimiert: [https://cdn1.adoberesources.net/alloy/2.4.0/alloy.js](https://cdn1.adoberesources.net/alloy/2.4.0/alloy.js)


### Code {#adding-the-code} hinzufügen

Die vordefinierte Standalone-Version erfordert einen &quot;Basiscode&quot;, der direkt zur Seite hinzugefügt wird. Kopieren Sie den folgenden &quot;Basiscode&quot;so hoch wie möglich im `<head>`-Tag Ihres HTML:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.4.0/alloy.min.js" async></script>
```

Der &quot;Basiscode&quot; erstellt eine globale Funktion mit dem Namen `alloy`. Verwenden Sie diese Funktion, um mit dem SDK zu interagieren. Wenn Sie der globalen Funktion einen anderen Namen geben möchten, ändern Sie den Namen `alloy` wie folgt:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.4.0/alloy.min.js" async></script>
```

In diesem Beispiel wird die globale Funktion in `mycustomname` anstatt `alloy` umbenannt.

>[!IMPORTANT]
>
>Um potenzielle Probleme zu vermeiden, verwenden Sie einen Namen, der mindestens ein Zeichen enthält, das keine Ziffer ist und nicht mit dem Namen einer Eigenschaft in Konflikt steht, die bereits unter `window` gefunden wurde.

Dieser Basis-Code lädt neben der Erstellung einer globalen Funktion auch zusätzlichen Code, der in einer externen Datei \(`alloy.js`\) enthalten ist, die auf einem Server gehostet wird. Standardmäßig wird dieser Code asynchron geladen, damit Ihre Web-Seite so leistungsfähig wie möglich ist. Dies ist die empfohlene Implementierung.

### Unterstützen von Internet Explorer {#support-internet-explore}

Dieses SDK verwendet Versprechungen, die eine Methode darstellen, um den Abschluss asynchroner Aufgaben zu kommunizieren. Die vom SDK verwendete Implementierung von [Promise](https://developer.mozilla.org/de-DE/docs/Web/JavaScript/Reference/Global_Objects/Promise) wird nativ von allen Browsern der Zielgruppe mit Ausnahme von [!DNL Internet Explorer] unterstützt. Um das SDK für [!DNL Internet Explorer] zu verwenden, müssen Sie `window.Promise` [polygefüllt](https://remysharp.com/2010/10/08/what-is-a-polyfill) haben.

So stellen Sie fest, ob Sie bereits über ein `window.Promise`-Polyfill verfügen:

1. Öffnen Sie Ihre Website in [!DNL Internet Explorer].
1. Öffnen Sie die Debugging-Konsole des Browsers.
1. Geben Sie `window.Promise` in die Konsole ein und drücken Sie die Eingabetaste.

Wenn etwas anderes als `undefined` angezeigt wird, verfügen Sie vermutlich bereits über ein `window.Promise`-Polyfill. Eine weitere Möglichkeit, um festzustellen, ob ein `window.Promise`-Polyfill vorliegt, ist das Laden Ihrer Website nach Abschluss der oben genannten Installationsanweisungen. Wenn das SDK einen Fehler ausgibt, in dem ein Promise erwähnt wird, verfügen Sie vermutlich über kein `window.Promise`-Polyfill.

Wenn Sie festgestellt haben, dass Sie das Polyfill `window.Promise` verwenden müssen, fügen Sie das folgende Skript-Tag über dem zuvor bereitgestellten Basiscode hinzu:

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

Dieses Tag lädt ein Skript, das sicherstellt, dass `window.Promise` eine gültige Promise-Implementierung ist.

>[!NOTE]
>
>Wenn Sie eine andere Promise-Implementierung laden möchten, stellen Sie sicher, dass `Promise.prototype.finally` unterstützt wird.

### Synchrones Laden der JavaScript-Datei {#loading-javascript-synchronously}

Wie im Abschnitt [Code](#adding-the-code) hinzugefügt, lädt der Basiscode, den Sie kopiert und in den HTML Ihrer Website eingefügt haben, eine externe Datei. Die externe Datei enthält die Kernfunktionalität des SDK. Jeder Befehl, den Sie ausführen möchten, während diese Datei geladen wird, wird in die Warteschlange gestellt und nach dem Laden der Datei verarbeitet. Das asynchrone Laden der Datei ist die leistungsfähigste Installationsmethode.

Unter bestimmten Umständen möchten Sie die Datei jedoch möglicherweise synchron laden \(weitere Details zu diesen Umständen werden später dokumentiert\). Dadurch wird verhindert, dass der Rest des HTML-Dokuments vom Browser analysiert und gerendert wird, bis die externe Datei geladen und ausgeführt wurde. Diese zusätzliche Verzögerung vor der Anzeige von Primärinhalten für Nutzer wird in der Regel nicht empfohlen, kann aber je nach den Umständen sinnvoll sein.

Um die Datei synchron statt asynchron zu laden, entfernen Sie das `async`-Attribut aus dem zweiten `script`-Tag, wie nachstehend dargestellt:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.4.0/alloy.min.js"></script>
```

## Option 3: Verwenden des NPM-Pakets

Adobe Experience Platform Web SDK ist auch als NPM-Paket verfügbar. [](https://www.npmjs.com) NPMist der Package Manager für JavaScript. Durch die Installation des NPM-Pakets können Sie den Build-Prozess für das Adobe Experience Platform Web SDK JavaScript steuern. Das NPM-Paket stellt EcmaScript Version 5 Module oder EcmaScript Version 2015 (ES6) Module zur Verfügung, die im Browser ausgeführt werden sollen.

```bash
npm install @adobe/alloy
```

Das NPM-Paket des Adobe Experience Platform Web SDK stellt eine `createInstance`-Funktion bereit. Diese Funktion wird zum Erstellen einer Instanz verwendet. Die Namensoption, die an die Funktion übergeben wird, steuert das bei der Protokollierung verwendete Präfix. Im Folgenden finden Sie einige Beispiele für die Verwendung des Pakets.

### Verwenden des Pakets als ECMAScript 2015 (ES6)-Modul

```javascript
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

### Verwenden des Pakets als ECMAScript 5-Modul

```javascript
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

### Unterstützen von Internet Explorer

Das Adobe Experience Platform SDK verwendet Versprechungen, die eine Methode darstellen, um den Abschluss asynchroner Aufgaben zu kommunizieren. Die vom SDK verwendete Implementierung von [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) wird nativ von allen Browsern der Zielgruppe mit Ausnahme von [!DNL Internet Explorer] unterstützt. Um das SDK für [!DNL Internet Explorer] zu verwenden, müssen Sie `window.Promise` [polygefüllt](https://remysharp.com/2010/10/08/what-is-a-polyfill) haben.

Eine Bibliothek, die Sie verwenden können, um Versprechen zu mehren, ist Versprechen-Polyfill. Weitere Informationen zur Installation mit NPM finden Sie in der [Versprechen-Polyfill-Dokumentation](https://www.npmjs.com/package/promise-polyfill).

>[!NOTE]
>
>Wenn Sie eine andere Promise-Implementierung laden möchten, stellen Sie sicher, dass `Promise.prototype.finally` unterstützt wird.