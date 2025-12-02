---
title: setDebug
description: Aktivieren oder Deaktivieren der Debugging-Einstellung von Web SDK.
exl-id: 9faac147-b7c7-4732-8454-35102970dae0
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# `setDebug`

Mit dem Befehl `setDebug` können Sie in der Web-SDK in den Debugging-Modus wechseln oder ihn beenden. Dies ist eine von mehreren Optionen, die für das [Debugging“ verfügbar ](../../use-cases/debugging.md). Adobe empfiehlt, den Debugging-Modus in Entwicklungsumgebungen oder nur auf dem lokalen Computer in Produktionsumgebungen zu aktivieren.

Führen Sie den `setDebug` Befehl aus, wenn Sie Ihre konfigurierte Instanz der Web-SDK aufrufen. Die einzige Option im Konfigurationsobjekt ist `enabled`. Dies ist ein boolescher Wert, der bestimmt, ob der Debugging-Modus aktiviert ist.

```js
alloy("setDebug", {"enabled": true});
```

## Festlegen von Debug mit der Tag-Erweiterung „Web SDK&quot;

Rufen Sie [`_satellite.setDebug()`](/help/collection/tags/setdebug.md) in der Browser-Konsole auf einer Seite auf, auf der eine Tag-Bibliothek implementiert ist. Die Tag-Erweiterung von Web SDK bietet keine Möglichkeit, Debugoptionen in der Tag-Benutzeroberfläche umzuschalten.
