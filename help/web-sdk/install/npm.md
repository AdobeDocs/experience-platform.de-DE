---
title: Installieren von Web SDK mithilfe des NPM-Pakets
description: Verwenden Sie ein NPM-Paket, um die Web-SDK-Bibliothek zu installieren und zu referenzieren.
exl-id: 4c70ec5d-33fd-4ef7-ba9e-5b92ff6c3e86
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Installieren von Web SDK mithilfe des NPM-Pakets

Adobe Experience Platform Web SDK ist als NPM[Paket ](https://www.npmjs.com). Durch die Installation des NPM-Pakets können Sie den Build-Prozess für die Adobe Experience Platform Web SDK JavaScript-Bibliothek steuern. Das NPM-Paket stellt EcmaScript-Module der Version 5 oder EcmaScript-Module der Version 2015 (ES6) bereit, die im Browser ausgeführt werden sollen.

```bash
npm install @adobe/alloy
```

Das NPM-Paket der Adobe Experience Platform Web SDK stellt eine `createInstance` zur Verfügung. Die an die Funktion übergebene Namensoption steuert das Präfix, das bei der Protokollierung verwendet wird. Im Folgenden finden Sie Beispiele für die Verwendung des Pakets.

## Verwenden des Pakets als ECMAScript 2015 (ES6)-Modul

```js
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>Das NPM-Paket beruht auf CommonJS-Modulen. Stellen Sie daher bei der Verwendung eines Bundlers sicher, dass der Bundler CommonJS-Module unterstützt. Einige Bundler, wie [Rollup](https://rollupjs.org), erfordern ein [Plug-in](https://www.npmjs.com/package/@rollup/plugin-commonjs) das CommonJS-Unterstützung bietet.

## Verwenden des Pakets als ECMAScript 5-Modul

```js
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```
