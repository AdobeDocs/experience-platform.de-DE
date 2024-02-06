---
title: Ausführen von Adobe Experience Platform Web SDK-Befehlen
description: Erfahren Sie, wie Sie Experience Platform Web SDK-Befehle ausführen
keywords: Ausführen von Befehlen;commandName;Promises;getLibraryInfo;Antwortobjekte;Zustimmung;
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: ffc60e83285188bc5b0f6eb7a20fafee16d51d4d
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 70%

---

# Ausführen von Befehlen


Nachdem der Basis-Code auf Ihrer Web-Seite implementiert wurde, können Sie mit der Ausführung von Befehlen mit dem SDK beginnen. Sie müssen nicht auf die externe Datei (`alloy.js`) vom Server geladen werden, bevor Befehle ausgeführt werden. Wenn das SDK noch nicht fertig geladen wurde, werden Befehle in die Warteschlange gestellt und so bald wie möglich vom SDK verarbeitet.

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
    // "result" is whatever the command returned
  })
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

Wenn es für Sie unwichtig ist, wann der Befehl erfolgreich ist, können Sie den `then`-Abruf entfernen.

```javascript
alloy("commandName", options)
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

Ebenso können Sie den `catch`-Abruf entfernen, wenn es für Sie unwichtig ist, wann der Befehl fehlschlägt.

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" will be whatever the command returned
  });
```

### Antwortobjekte

Alle von Befehlen zurückgegebenen Zusagen werden mit einem `result` -Objekt. Das Ergebnisobjekt enthält Daten, die vom Befehl und der Zustimmung des Benutzers abhängen. Beispielsweise werden Bibliotheksinformationen im folgenden Befehl als Eigenschaft des Ergebnisobjekts übergeben.

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

### Einverständnis

Wenn ein Benutzer seine Zustimmung zu einem bestimmten Zweck nicht gegeben hat, wird das promise-Objekt dennoch aufgelöst. Das Antwortobjekt enthält jedoch nur die Informationen, die im Kontext dessen bereitgestellt werden können, was der Benutzer zugestimmt hat.
