---
title: Installieren des Web SDK mit dem NPM-Paket
description: Verwenden Sie ein NPM-Paket, um die Web SDK-Bibliothek zu installieren und darauf zu verweisen.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---


# Installieren des Web SDK mit dem NPM-Paket

Adobe Experience Platform Web SDK ist als [NPM-Paket](https://www.npmjs.com). Durch die Installation des NPM-Pakets können Sie den Build-Prozess für die Adobe Experience Platform Web SDK-JavaScript-Bibliothek steuern. Das NPM-Paket stellt EcmaScript Version 5 Module oder EcmaScript Version 2015 (ES6) Module zur Verfügung, die im Browser ausgeführt werden sollen.

```bash
npm install @adobe/alloy
```

Das NPM-Paket des Adobe Experience Platform Web SDK stellt eine `createInstance` -Funktion. Die an die Funktion übergebene Namensoption steuert das bei der Protokollierung verwendete Präfix. Im Folgenden finden Sie Beispiele für die Verwendung des -Pakets.

## Verwenden des Pakets als ECMAScript 2015 (ES6)-Modul

```js
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>Das NPM-Paket basiert auf CommonJS-Modulen. Stellen Sie daher bei Verwendung eines Bundlers sicher, dass der Bundler CommonJS-Module unterstützt. Einige Bundler, z. B. [Datenaggregation](https://rollupjs.org), erfordert eine [plugin](https://www.npmjs.com/package/@rollup/plugin-commonjs) , die Unterstützung für CommonJS bietet.

## Verwenden des Pakets als ECMAScript 5-Modul

```js
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```
