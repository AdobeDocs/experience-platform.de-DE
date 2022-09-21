---
title: Installieren des Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie das Experience Platform Web SDK installieren.
keywords: Web SDK-Installation;Web SDK installieren;Internet Explorer;Zusage;npm-Paket
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 30%

---

# Installieren des SDK {#installing-the-sdk}

Es werden drei Möglichkeiten zur Verwendung des Adobe Experience Platform Web SDK unterstützt:

1. Die bevorzugte Methode zur Verwendung des Adobe Experience Platform Web SDK besteht über die Datenerfassungs-Benutzeroberfläche oder die Benutzeroberfläche der Experience Platform.
1. Das Adobe Experience Platform Web SDK ist auch in einem Inhaltsbereitstellungsnetzwerk (Content Delivery Network, CDN) verfügbar, das Sie verwenden können.
1. Verwenden Sie die NPM-Bibliothek, die EcmaScript 5- und EcmaScript 2015 (ES6)-Module exportiert.

## Option 1: Installieren der Tag-Erweiterung

Die Dokumentation zur Tag-Erweiterung finden Sie unter [Launch-Dokumentation](../../tags/extensions/web/sdk/overview.md)

## Option 2: Installieren der vordefinierten eigenständigen Version

Die vordefinierte Version ist in einem CDN verfügbar. Sie können die Bibliothek im CDN direkt auf Ihrer Seite referenzieren oder sie herunterladen und in Ihrer eigenen Infrastruktur hosten. Es ist in minimierten und nicht minimierten Formaten verfügbar. Die nicht minimierte Version ist für Debugging-Zwecke hilfreich.

URL-Struktur: https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js ODER legierungen.js für die nicht minimierte Version.

Beispiel:


* Minimiert: [https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js)
* Nicht minimiert: [https://cdn1.adoberesources.net/alloy/2.6.4/alloy.js](https://cdn1.adoberesources.net/alloy/2.6.4/alloy.js)


### Code hinzufügen {#adding-the-code}

Die vordefinierte eigenständige Version erfordert einen &quot;Basis-Code&quot;, der direkt zur Seite hinzugefügt wird. Kopieren Sie den folgenden &quot;Basis-Code&quot;und fügen Sie ihn so weit wie möglich in die `<head>` -Tag Ihrer HTML:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js" async></script>
```

Der &quot;Basis-Code&quot;erstellt eine globale Funktion mit dem Namen `alloy`. Verwenden Sie diese Funktion, um mit dem SDK zu interagieren. Wenn Sie der globalen Funktion einen anderen Namen geben möchten, ändern Sie die `alloy` name wie folgt:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js" async></script>
```

In diesem Beispiel wird die globale Funktion in `mycustomname` anstatt `alloy` umbenannt.

>[!IMPORTANT]
>
>Um potenzielle Probleme zu vermeiden, verwenden Sie einen Namen, der mindestens ein Zeichen enthält, das keine Ziffer ist und nicht mit dem Namen einer Eigenschaft in Konflikt steht, die bereits unter `window` gefunden wurde.

Dieser Basis-Code lädt neben der Erstellung einer globalen Funktion auch zusätzlichen Code, der in einer externen Datei \(`alloy.js`\) enthalten ist, die auf einem Server gehostet wird. Standardmäßig wird dieser Code asynchron geladen, damit Ihre Web-Seite so leistungsfähig wie möglich ist. Dies ist die empfohlene Implementierung.

### Unterstützen von Internet Explorer {#support-internet-explore}

Dieses SDK verwendet Versprechen, die eine Methode zur Mitteilung des Abschlusses asynchroner Aufgaben darstellen. Die [Promise](https://developer.mozilla.org/de-DE/docs/Web/JavaScript/Reference/Global_Objects/Promise) Die vom SDK verwendete Implementierung wird nativ von allen Ziel-Browsern unterstützt, mit Ausnahme von [!DNL Internet Explorer]. So verwenden Sie das SDK in [!DNL Internet Explorer], müssen Sie `window.Promise` [Polyfill](https://remysharp.com/2010/10/08/what-is-a-polyfill).

So stellen Sie fest, ob Sie bereits über ein `window.Promise`-Polyfill verfügen:

1. Öffnen Sie Ihre Website in [!DNL Internet Explorer].
1. Öffnen Sie die Debugging-Konsole des Browsers.
1. Geben Sie `window.Promise` in die Konsole ein und drücken Sie die Eingabetaste.

Wenn etwas anderes als `undefined` angezeigt wird, verfügen Sie vermutlich bereits über ein `window.Promise`-Polyfill. Eine weitere Möglichkeit, um festzustellen, ob ein `window.Promise`-Polyfill vorliegt, ist das Laden Ihrer Website nach Abschluss der oben genannten Installationsanweisungen. Wenn das SDK einen Fehler ausgibt, in dem ein Promise erwähnt wird, verfügen Sie vermutlich über kein `window.Promise`-Polyfill.

Wenn Sie festgestellt haben, müssen Sie ein Polyfill `window.Promise`, fügen Sie das folgende Skript-Tag über dem zuvor bereitgestellten Basis-Code ein:

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

Dieses Tag lädt ein Skript, das sicherstellt, dass `window.Promise` ist eine gültige Implementierung von Promise.

>[!NOTE]
>
>Wenn Sie eine andere Promise-Implementierung laden, stellen Sie sicher, dass sie `Promise.prototype.finally`.

### Synchrones Laden der JavaScript-Datei {#loading-javascript-synchronously}

Wie im Abschnitt beschrieben [Code hinzufügen](#adding-the-code), lädt der Basis-Code, den Sie kopiert und in die HTML Ihrer Website eingefügt haben, eine externe Datei. Die externe Datei enthält die Kernfunktionalität des SDK. Jeder Befehl, den Sie beim Laden dieser Datei ausführen möchten, wird in die Warteschlange gestellt und nach dem Laden der Datei verarbeitet. Das asynchrone Laden der Datei ist die leistungsfähigste Installationsmethode.

Unter bestimmten Umständen möchten Sie die Datei jedoch möglicherweise synchron laden \(weitere Details zu diesen Umständen werden später dokumentiert\). Dadurch wird verhindert, dass der Rest des HTML-Dokuments vom Browser analysiert und gerendert wird, bis die externe Datei geladen und ausgeführt wurde. Diese zusätzliche Verzögerung vor der Anzeige von Primärinhalten für Nutzer wird in der Regel nicht empfohlen, kann aber je nach den Umständen sinnvoll sein.

Um die Datei synchron statt asynchron zu laden, entfernen Sie das `async`-Attribut aus dem zweiten `script`-Tag, wie nachstehend dargestellt:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js"></script>
```

## Option 3: Verwenden des NPM-Pakets

Das Adobe Experience Platform Web SDK ist auch als NPM-Paket verfügbar. [NPM](https://www.npmjs.com) ist der Paketmanager für JavaScript. Durch die Installation des NPM-Pakets können Sie den Build-Prozess für das Adobe Experience Platform Web SDK-JavaScript steuern. Das NPM-Paket stellt EcmaScript Version 5 Module oder EcmaScript Version 2015 (ES6) Module zur Verfügung, die im Browser ausgeführt werden sollen.

```bash
npm install @adobe/alloy
```

Das NPM-Paket des Adobe Experience Platform Web SDK stellt eine `createInstance` -Funktion. Diese Funktion wird zum Erstellen einer Instanz verwendet. Die an die Funktion übergebene Namensoption steuert das bei der Protokollierung verwendete Präfix. Im Folgenden finden Sie Beispiele für die Verwendung des Pakets.

### Verwenden des Pakets als ECMAScript 2015 (ES6)-Modul

```javascript
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>Das NPM-Paket beruht auf CommonJS-Modulen. Stellen Sie daher bei Verwendung eines Bundlers sicher, dass der Bundler CommonJS-Module unterstützt. Einige Bundler, wie [Datenaggregation](https://rollupjs.org), erfordert eine [plugin](https://www.npmjs.com/package/@rollup/plugin-commonjs) , die Unterstützung für CommonJS bietet.

### Verwenden des Pakets als ECMAScript 5-Modul

```javascript
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

### Unterstützen von Internet Explorer

Das Adobe Experience Platform-SDK verwendet Versprechen, die eine Methode darstellen, um den Abschluss asynchroner Aufgaben zu kommunizieren. Die [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) Die vom SDK verwendete Implementierung wird nativ von allen Ziel-Browsern unterstützt, mit Ausnahme von [!DNL Internet Explorer]. So verwenden Sie das SDK in [!DNL Internet Explorer], müssen Sie `window.Promise` [Polyfill](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Eine Bibliothek, die Sie zum Polyfill-Promise verwenden können, ist Promise-Polyfill. Siehe [Promise-Polyfill-Dokumentation](https://www.npmjs.com/package/promise-polyfill) für weitere Informationen zur Installation mit NPM.

>[!NOTE]
>
>Wenn Sie eine andere Promise-Implementierung laden, stellen Sie sicher, dass sie `Promise.prototype.finally`.
