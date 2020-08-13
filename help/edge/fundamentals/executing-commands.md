---
title: Ausführen von Befehlen
seo-title: Ausführen von Adobe Experience Platform Web SDK-Befehlen
description: Erfahren Sie, wie Sie Experience Platform Web SDK-Befehle ausführen
seo-description: Erfahren Sie, wie Sie Experience Platform Web SDK-Befehle ausführen
translation-type: tm+mt
source-git-commit: bf4194e1449bddd662f2152f84dbbe90060b5d30
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 79%

---


# Ausführen von Befehlen

Nachdem der Basis-Code auf Ihrer Web-Seite implementiert wurde, können Sie mit der Ausführung von Befehlen mit dem SDK beginnen. Sie müssen nicht warten, bis die externe Datei \(`alloy.js`\) vom Server geladen wird, damit Befehle ausgeführt werden können. Wenn das SDK noch nicht fertig geladen wurde, werden Befehle in die Warteschlange gestellt und so bald wie möglich vom SDK verarbeitet.

Befehle werden mit der folgenden Syntax ausgeführt.

```javascript
alloy("commandName", options);
```

`commandName` gibt dem SDK an, was zu tun ist, während `options` die Parameter und Daten sind, die Sie an einen Befehl übergeben möchten. Da die verfügbaren Optionen vom Befehl abhängen, finden Sie in der Dokumentation weitere Informationen zu den einzelnen Befehlen.

## Ein Hinweis zu Promises

[Promises](https://developer.mozilla.org/de-DE/docs/Web/JavaScript/Reference/Global_Objects/Promise) sind von grundlegender Bedeutung für die Kommunikation des SDK mit dem Code auf Ihrer Web-Seite. Ein Promise ist eine gängige Programmierstruktur und nicht spezifisch für dieses SDK oder gar JavaScript. Ein Promise fungiert als Proxy für einen Wert, der beim Erstellen des Promise nicht bekannt ist. Sobald der Wert bekannt ist, wird das Promise mit dem Wert „aufgelöst“. Handler-Funktionen können mit einem Promise verknüpft werden, sodass Sie benachrichtigt werden können, wenn das Promise aufgelöst wurde oder ein Fehler im Prozess der Promise-Auflösung aufgetreten ist. Um mehr über Promises zu erfahren, lesen Sie [dieses Tutorial](https://javascript.info/promise-basics) oder andere Ressourcen im Web.

## Umgang mit Erfolg oder Misserfolg {#handling-success-or-failure}

Jedes Mal, wenn ein Befehl ausgeführt wird, wird ein Promise zurückgegeben. Das Promise steht für den letztendlichen Abschluss des Befehls. Im Beispiel unten können Sie mithilfe der `then`- und `catch`-Methoden bestimmen, wann der Befehl erfolgreich ausgeführt wurde oder fehlgeschlagen ist.

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" is whatever the command returned
  })
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  })
```

Wenn es für Sie unwichtig ist, wann der Befehl erfolgreich ist, können Sie den `then`-Abruf entfernen.

```javascript
alloy("commandName", options)
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  })
```

Ebenso können Sie den `catch`-Abruf entfernen, wenn es für Sie unwichtig ist, wann der Befehl fehlschlägt.

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" will be whatever the command returned
  })
```

### Response objects

All promises returned from commands are resolved with a `result` object. The result object will contain data depending on the command and the user&#39;s consent. For example, library info is passed as a property of the results object in the following command.

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(results.libraryInfo.version);
});
```

### Consent

If a user has not given their consent for a particular purpose, the promise will still be resolved; however, the response object will only contain the information that can be provided in the context of what the user has consented to.
