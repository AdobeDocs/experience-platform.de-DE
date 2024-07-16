---
title: setDebug
description: Aktivieren oder deaktivieren Sie die Debug-Einstellung des Web SDK.
exl-id: 9faac147-b7c7-4732-8454-35102970dae0
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# `setDebug`

Mit dem Befehl `setDebug` können Sie im Web SDK in den Debugging-Modus wechseln oder diesen beenden. Es ist eine von mehreren Optionen, die für [Debugging](../use-cases/debugging.md) verfügbar sind. Adobe empfiehlt, den Debugging-Modus in Entwicklungsumgebungen oder auf Ihrem lokalen Computer in Produktionsumgebungen zu aktivieren.

## Festlegen von Debugging mithilfe der Web SDK-Tag-Erweiterung

Die Tag-Erweiterung bietet nicht die Möglichkeit, Debugging-Optionen in der Benutzeroberfläche umzuschalten. Sie können entweder den Editor für benutzerdefinierten Code mit der JavaScript-Syntax verwenden oder den JavaScript-Code in der Browser-Konsole eingeben, während Sie sich auf Ihrer Site befinden.

## Festlegen von Debugging mithilfe der Web SDK JavaScript-Bibliothek

Führen Sie den Befehl `setDebug` aus, wenn Sie Ihre konfigurierte Instanz des Web SDK aufrufen. Die einzige Option im Konfigurationsobjekt ist `enabled`, ein boolescher Wert, der bestimmt, ob der Debug-Modus aktiviert ist.

```js
alloy("setDebug", {"enabled": true});
```
