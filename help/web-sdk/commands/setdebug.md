---
title: setDebug
description: Aktivieren oder Deaktivieren der Debugging-Einstellung von Web SDK.
exl-id: 9faac147-b7c7-4732-8454-35102970dae0
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# `setDebug`

Mit dem Befehl `setDebug` können Sie in der Web-SDK in den Debugging-Modus wechseln oder ihn beenden. Dies ist eine von mehreren Optionen, die für das [Debugging“ verfügbar &#x200B;](../use-cases/debugging.md). Adobe empfiehlt, den Debugging-Modus in Entwicklungsumgebungen oder nur auf dem lokalen Computer in Produktionsumgebungen zu aktivieren.

## Festlegen von Debug mit der Tag-Erweiterung „Web SDK&quot;

Die Tag-Erweiterung bietet keine Möglichkeit, in der Benutzeroberfläche Debugging-Optionen umzuschalten. Sie können entweder den Editor für benutzerspezifischen Code mit JavaScript-Syntax verwenden oder den JavaScript-Code in der Browser-Konsole eingeben, während Sie sich auf Ihrer Site befinden.

## Festlegen des Debugging-Modus mit der Web SDK JavaScript-Bibliothek

Führen Sie den `setDebug` Befehl aus, wenn Sie Ihre konfigurierte Instanz der Web-SDK aufrufen. Die einzige Option im Konfigurationsobjekt ist `enabled`. Dies ist ein boolescher Wert, der bestimmt, ob der Debugging-Modus aktiviert ist.

```js
alloy("setDebug", {"enabled": true});
```
