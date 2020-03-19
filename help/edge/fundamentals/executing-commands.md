---
title: Ausführen von Befehlen
seo-title: Ausführen von Adobe Experience Platform Web SDK-Befehlen
description: Erfahren Sie, wie Sie Experience Platform Web SDK-Befehle ausführen
seo-description: Erfahren Sie, wie Sie Experience Platform Web SDK-Befehle ausführen
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Befehle ausführen

>[!IMPORTANT]
>
>Das Adobe Experience Platform Web SDK befindet sich derzeit in der Betaphase und steht nicht allen Benutzern zur Verfügung. Dokumentation und Funktionalität können sich ändern.

Nachdem der Basiscode auf Ihrer Webseite implementiert wurde, können Sie mit der Ausführung von Befehlen mit dem SDK beginnen. Sie müssen nicht warten, bis die externe Datei \(`alloy.js`\) vom Server geladen wird, bevor Befehle ausgeführt werden. Wenn das SDK noch nicht fertig geladen wurde, werden Befehle so bald wie möglich vom SDK in die Warteschlange gestellt und verarbeitet.

Befehle werden mit der folgenden Syntax ausgeführt.

```javascript
alloy("commandName", options);
```

Die `commandName` gibt dem SDK an, was zu tun ist, während `options` es die Parameter und Daten sind, die Sie an einen Befehl übergeben möchten. Da die verfügbaren Optionen vom Befehl abhängen, finden Sie in der Dokumentation weitere Informationen zu den einzelnen Befehlen.

## Ein Vermerk zu Versprechen

[Versprechungen](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) sind von grundlegender Bedeutung für die Kommunikation des SDK mit dem Code auf Ihrer Webseite. Ein Versprechen ist eine gängige Programmierstruktur und nicht spezifisch für dieses SDK oder sogar JavaScript. Ein Versprechen fungiert als Proxy für einen Wert, der beim Erstellen des Versprechens nicht bekannt ist. Sobald der Wert bekannt ist, wird das Versprechen mit dem Wert &quot;gelöst&quot;. Handler-Funktionen können mit einer Zusage verknüpft werden, sodass Sie benachrichtigt werden können, wenn die Zusage gelöst wurde oder ein Fehler im Prozess der Behebung der Zusage aufgetreten ist. Um mehr über Versprechen zu erfahren, lesen Sie bitte [dieses Tutorial](https://javascript.info/promise-basics) oder andere Ressourcen im Web.

## Umgang mit Erfolg oder Misserfolg

Jedes Mal, wenn ein Befehl ausgeführt wird, wird ein Versprechen zurückgegeben. Das Versprechen steht für den letztendlichen Abschluss des Befehls. Im Beispiel unten können Sie mithilfe `then` und `catch` Methoden bestimmen, wann der Befehl erfolgreich ausgeführt wurde oder fehlgeschlagen ist.

```javascript
alloy("commandName", options)
  .then(function(value) {
    // The command succeeded.
    // "value" is whatever the command returned
  })
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  })
```

Wenn Sie nicht wissen, wann der Befehl erfolgreich ist, können Sie den `then` Aufruf entfernen.

```javascript
alloy("commandName", options)
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  })
```

Ebenso können Sie den `catch` Aufruf entfernen, wenn Sie wissen, wann der Befehl fehlschlägt.

```javascript
alloy("commandName", options)
  .then(function(value) {
    // The command succeeded.
    // "value" will be whatever the command returned
  })
```

## Beheben von Fehlern

Wenn das Versprechen abgelehnt wird und Sie keinen `catch` Aufruf hinzugefügt haben, wird der Fehler &quot;blasen auf&quot;angezeigt und in der Entwicklerkonsole Ihres Browsers protokolliert, unabhängig davon, ob die Protokollierung im Adobe Experience Platform Web SDK aktiviert ist. Wenn dies für Sie von Belang ist, können Sie die `suppressErrors` Konfigurationsoption auf `true` wie unter [Konfigurieren des SDK](configuring-the-sdk.md)beschrieben einstellen.
