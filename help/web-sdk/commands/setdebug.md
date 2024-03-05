---
title: setDebug
description: Aktivieren oder deaktivieren Sie die Debug-Einstellung des Web SDK.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# `setDebug`

Die `setDebug` -Befehl können Sie im Web SDK in den Debugging-Modus wechseln oder diesen beenden. Es ist eine von mehreren verfügbaren Optionen für [Debugging](../use-cases/debugging.md). Adobe empfiehlt, den Debugging-Modus in Entwicklungsumgebungen oder auf Ihrem lokalen Computer in Produktionsumgebungen zu aktivieren.

## Festlegen von Debugging mithilfe der Web SDK-Tag-Erweiterung

Die Tag-Erweiterung bietet nicht die Möglichkeit, Debugging-Optionen in der Benutzeroberfläche umzuschalten. Sie können entweder den Editor für benutzerdefinierten Code mit JavaScript-Syntax verwenden oder den JavaScript-Code in der Browser-Konsole eingeben, während Sie sich auf Ihrer Site befinden.

## Debugging mithilfe der Web SDK-JavaScript-Bibliothek festlegen

Führen Sie die `setDebug` beim Aufruf Ihrer konfigurierten Instanz des Web SDK. Die einzige Option im Konfigurationsobjekt ist `enabled`: ein boolescher Wert, der bestimmt, ob der Debug-Modus aktiviert ist.

```js
alloy("setDebug", {"enabled": true});
```
