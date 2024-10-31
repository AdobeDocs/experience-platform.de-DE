---
title: Überwachungshaken für das Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie mithilfe der vom Adobe Experience Platform Web SDK bereitgestellten Überwachungshooks Ihre Implementierung debuggen und Web SDK-Protokolle erfassen können.
source-git-commit: 3dacc991fd7760c1c358bec07aca83ffeb4f4f4d
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 6%

---


# Überwachungshooks für Web SDK

Das Adobe Experience Platform Web SDK enthält Überwachungshooks, mit denen Sie verschiedene Systemereignisse überwachen können. Diese Tools sind nützlich für die Entwicklung Ihrer eigenen Debugging-Tools und zum Erfassen von Web SDK-Protokollen.

Das Web SDK Trigger die Überwachungsfunktionen unabhängig davon, ob Sie [Debugging](commands/configure/debugenabled.md) aktiviert haben.

## `onInstanceCreated` {#onInstanceCreated}

Diese Rückruffunktion wird ausgelöst, wenn Sie erfolgreich eine neue Web SDK-Instanz erstellt haben. Weitere Informationen zu den Funktionsparametern finden Sie im folgenden Beispiel.

```js
onInstanceCreated(data) {
    // data.instanceName
    // data.instance
}
```

| Parameter | Typ | Beschreibung |
|---------|----------|----------|
| `data.instanceName` | Zeichenfolge | Der Name der globalen Variablen, in der die Web SDK-Instanz gespeichert wird. |
| `data.instance` | Funktion | Die Instanzfunktion, mit der Web SDK-Befehle aufgerufen werden. |

## `onInstanceConfigured` {#onInstanceConfigured}

Diese Rückruffunktion wird vom Web SDK ausgelöst, wenn der Befehl [`configure`](commands/configure/overview.md) erfolgreich aufgelöst wurde. Weitere Informationen zu den Funktionsparametern finden Sie im folgenden Beispiel.

```js
 onInstanceConfigured(data) {
     // data.instanceName
     // data.config
 }
```

| Parameter | Typ | Beschreibung |
|---------|----------|----------|
| `data.instanceName` | Zeichenfolge | Der Name der globalen Variablen, in der die Web SDK-Instanz gespeichert wird. |
| `data.config` | Objekt | Ein Objekt, das die für Ihre Web SDK-Instanz verwendete Konfiguration enthält. Dies sind die Optionen, die an den Befehl [`configure`](commands/configure/overview.md) übergeben werden, wobei alle Standardwerte hinzugefügt werden. |

## `onBeforeCommand` {#onBeforeCommand}

Diese Rückruffunktion wird vom Web SDK ausgelöst, bevor ein anderer Befehl ausgeführt wird. Mit dieser Funktion können Sie die Konfigurationsoptionen eines bestimmten Befehls abrufen. Weitere Informationen zu den Funktionsparametern finden Sie im folgenden Beispiel.

```js
onBeforeCommand(data) {
    // data.instanceName
    // data.commandName
    // data.options
}
```

| Parameter | Typ | Beschreibung |
|---------|----------|----------|
| `data.instanceName` | Zeichenfolge | Der Name der globalen Variablen, in der die Web SDK-Instanz gespeichert wird. |
| `data.commandName` | String | Der Name des Web SDK-Befehls, vor dem diese Funktion ausgeführt wird. |
| `data.options` | Objekt | Ein Objekt, das die Optionen enthält, die an den Web SDK-Befehl übergeben werden. |

## `onCommandResolved` {#onCommandResolved}

Diese Rückruffunktion wird beim Auflösen von Befehlsversprechen ausgelöst. Sie können diese Funktion verwenden, um die Befehlsoptionen und das Ergebnis anzuzeigen. Weitere Informationen zu den Funktionsparametern finden Sie im folgenden Beispiel.

```js
onCommandResolved(data) {
    // data.instanceName
    // data.commandName
    // data.options
    // data.result
},
```

| Parameter | Typ | Beschreibung |
|---------|----------|----------|
| `data.instanceName` | Zeichenfolge | Der Name der globalen Variablen, in der die Web SDK-Instanz gespeichert wird. |
| `data.commandName` | String | Der Name des ausgeführten Web SDK-Befehls. |
| `data.options` | Objekt | Ein Objekt, das die Optionen enthält, die an den Web SDK-Befehl übergeben werden. |
| `data.result` | Objekt | Ein Objekt, das das Ergebnis des Web SDK-Befehls enthält. |

## `onCommandRejected` {#onCommandRejected}

Diese Rückruffunktion wird ausgelöst, bevor ein Befehlsversprechen zurückgewiesen wird. Sie enthält Informationen zum Grund der Ablehnung des Befehls. Weitere Informationen zu den Funktionsparametern finden Sie im folgenden Beispiel.

```js
onCommandRejected(data) {
    // data.instanceName
    // data.commandName
    // data.options
    // data.error
}
```

| Parameter | Typ | Beschreibung |
|---------|----------|----------|
| `data.instanceName` | Zeichenfolge | Der Name der globalen Variablen, in der die Web SDK-Instanz gespeichert wird. |
| `data.commandName` | String | Der Name des ausgeführten Web SDK-Befehls. |
| `data.options` | Objekt | Ein Objekt, das die Optionen enthält, die an den Web SDK-Befehl übergeben werden. |
| `data.error` | Objekt | Ein Objekt, das die vom Netzwerkaufruf des Browsers zurückgegebene Fehlermeldung enthält (`fetch` in den meisten Fällen), zusammen mit dem Grund, warum der Befehl abgelehnt wurde. |

## `onBeforeNetworkRequest` {#onBeforeNetworkRequest}

Diese Rückruffunktion wird ausgelöst, bevor eine Netzwerkanforderung ausgeführt wird. Weitere Informationen zu den Funktionsparametern finden Sie im folgenden Beispiel.

```js
onBeforeNetworkRequest(data) {
    // data.instanceName
    // data.requestId
    // data.url
    // data.payload
}
```

| Parameter | Typ | Beschreibung |
|---------|----------|----------|
| `data.instanceName` | Zeichenfolge | Der Name der globalen Variablen, in der die Web SDK-Instanz gespeichert wird. |
| `data.requestId` | String | Der vom Web SDK generierte `requestId` , um das Debugging zu aktivieren. |
| `data.url` | String | Die angeforderte URL. |
| `data.payload` | Objekt | Das Nutzlastobjekt der Netzwerkanforderung, das durch eine `POST` -Methode in das JSON-Format konvertiert und im Hauptteil der Anfrage gesendet wird. |

## `onNetworkResponse` {#onNetworkResponse}

Diese Rückruffunktion wird ausgelöst, wenn der Browser eine Antwort erhält. Weitere Informationen zu den Funktionsparametern finden Sie im folgenden Beispiel.

```js
onNetworkResponse(data) {
    // data.instanceName
    // data.requestId
    // data.url
    // data.payload
    // data.body
    // data.parsedBody
    // data.status
    // data.retriesAttempted
}
```

| Parameter | Typ | Beschreibung |
|---------|----------|----------|
| `data.instanceName` | Zeichenfolge | Der Name der globalen Variablen, in der die Web SDK-Instanz gespeichert wird. |
| `data.requestId` | String | Der vom Web SDK generierte `requestId` , um das Debugging zu aktivieren. |
| `data.url` | String | Die angeforderte URL. |
| `data.payload` | Objekt | Das Payload-Objekt, das durch eine `POST` -Methode in das JSON-Format konvertiert und im Hauptteil der Anfrage gesendet wird. |
| `data.body` | String | Der Antworttext im Zeichenfolgenformat. |
| `data.parsedBody` | Objekt | Ein Objekt, das den analysierten Antworttext enthält. Wenn beim Analysieren des Antworttextes ein Fehler auftritt, ist dieser Parameter nicht definiert. |
| `data.status` | String | Der Antwort-Code im ganzzahligen Format. |
| `data.retriesAttempted` | Ganzzahl | Die Anzahl der Wiederholungsversuche, die beim Senden der Anfrage versucht wurden. Null bedeutet, dass die Anfrage beim ersten Versuch erfolgreich war. |

## `onNetworkError` {#onNetworkError}

Diese Rückruffunktion wird ausgelöst, wenn die Netzwerkanforderung fehlgeschlagen ist. Weitere Informationen zu den Funktionsparametern finden Sie im folgenden Beispiel.

```js
onNetworkError(data) {
    // data.instanceName
    // data.requestId
    // data.url
    // data.payload
    // data.error
},
```

| Parameter | Typ | Beschreibung |
|---------|----------|----------|
| `data.instanceName` | Zeichenfolge | Der Name der globalen Variablen, in der die Web SDK-Instanz gespeichert wird. |
| `data.requestId` | String | Der vom Web SDK generierte `requestId` , um das Debugging zu aktivieren. |
| `data.url` | String | Die angeforderte URL. |
| `data.payload` | Objekt | Das Payload-Objekt, das durch eine `POST` -Methode in das JSON-Format konvertiert und im Hauptteil der Anfrage gesendet wird. |
| `data.error` | Objekt | Ein Objekt, das die vom Netzwerkaufruf des Browsers zurückgegebene Fehlermeldung enthält (`fetch` in den meisten Fällen), zusammen mit dem Grund, warum der Befehl abgelehnt wurde. |

## `onBeforeLog` {#onBeforeLog}

Diese Rückruffunktion wird ausgelöst, bevor das Web SDK alles in der Konsole protokolliert. Weitere Informationen zu den Funktionsparametern finden Sie im folgenden Beispiel.

```js
onBeforeLog(data) {
    // data.instanceName
    // data.componentName
    // data.level
    // data.arguments
}
```

| Parameter | Typ | Beschreibung |
|---------|----------|----------|
| `data.instanceName` | Zeichenfolge | Der Name der globalen Variablen, in der die Web SDK-Instanz gespeichert wird. |
| `data.componentName` | String | Der Name der Komponente, die die Protokollmeldung generiert hat. |
| `data.level` | String | Die Protokollierungsebene. Unterstützte Ebenen: `log`, `info`, `warn`, `error`. |
| `data.arguments` | Zeichenfolgen-Array | Die Argumente der Protokollmeldung. |


## `onContentRendering` {#onContentRendering}

Diese Rückruffunktion wird in verschiedenen Phasen des Renderns von der Komponente `personalization` ausgelöst. Die Payload kann je nach dem Parameter `status` unterschiedlich ausfallen. Weitere Informationen zu den Funktionsparametern finden Sie im folgenden Beispiel.

```js
 onContentRendering(data) {
     // data.instanceName
     // data.componentName
     // data.payload
     // data.status
}
```

| Parameter | Typ | Beschreibung |
|---------|----------|----------|
| `data.instanceName` | Zeichenfolge | Der Name der globalen Variablen, in der die Web SDK-Instanz gespeichert wird. |
| `data.componentName` | String | Der Name der Komponente, die die Protokollmeldung generiert hat. |
| `data.payload` | Objekt | Das Payload-Objekt, das durch eine `POST` -Methode in das JSON-Format konvertiert und im Hauptteil der Anfrage gesendet wird. |
| `data.status` | String | Die Komponente `personalization` benachrichtigt das Web SDK über den Status des Renderings.  Unterstützte Werte: <ul><li>`rendering-started`: Gibt an, dass das Web SDK im Begriff ist, Vorschläge zu rendern. Bevor das Web SDK beginnt, einen Entscheidungsbereich oder eine Ansicht zu rendern, können Sie im `data` -Objekt die Vorschläge sehen, die von der `personalization` -Komponente gerendert werden sollen, sowie den Bereichsnamen.</li><li>`no-offers`: Gibt an, dass für die angeforderten Parameter keine Payload empfangen wurde.</li> <li>`rendering-failed`: Gibt an, dass das Web SDK einen Vorschlag nicht rendern konnte.</li><li>`rendering-succeeded`: Gibt an, dass das Rendering für einen Entscheidungsbereich abgeschlossen wurde.</li> <li>`rendering-redirect`: Gibt an, dass das Web SDK einen Weiterleitungsantrag rendert.</li></ul> |

## `onContentHiding` {#onContentHiding}

Diese Rückruffunktion wird ausgelöst, wenn ein Stil zum Vorab-Ausblenden angewendet oder entfernt wird.

```js
onContentHiding(data) {
    // data.instanceName
    // data.componentName
    // data.status
}
```

| Parameter | Typ | Beschreibung |
|---------|----------|----------|
| `data.instanceName` | Zeichenfolge | Der Name der globalen Variablen, in der die Web SDK-Instanz gespeichert wird. |
| `data.componentName` | String | Der Name der Komponente, die die Protokollmeldung generiert hat. |
| `data.status` | String | Die Komponente `personalization` benachrichtigt das Web SDK über den Status des Renderings. Unterstützte Werte: <ul><li>`hide-containers`</li><li>`show-containers`</ul> |

## Angeben von Überwachungshooks bei Verwendung des NPM-Pakets {#specify-monitoris-npm}

Wenn Sie das Web SDK über das Paket [NPM](install/npm.md) verwenden, können Sie Überwachungshooks in der Funktion `createInstasnce` angeben, wie unten dargestellt.

```js
var monitor = {
  onBeforeCommand(data) {
    console.log(data);
  },
  ...
};
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy", monitors: [monitor] });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

## Beispiel {#example}

Das Web SDK sucht nach einem Array von Objekten in einer globalen Variablen namens `__alloyMonitors`.

Um alle Web SDK-Ereignisse zu erfassen, müssen Sie Ihre Monitoring-Hooks definieren, bevor der Web SDK-Code auf Ihrer Seite geladen wird. Jede Überwachungsmethode erfasst ein Web SDK-Ereignis.

Sie können Überwachungs-Hooks *nach dem Laden von* Web SDK-Code auf Ihrer Seite definieren, aber alle Hooks, die vor dem Laden der Seite ausgelöst wurden, werden *nicht* erfasst.

Wenn Sie Ihr Überwachungs-Hook-Objekt definieren, müssen Sie nur die Methoden definieren, für die Sie eine spezielle Logik definieren möchten.
Wenn Sie sich beispielsweise nur für `onContentRendering` interessieren, können Sie diese Methode einfach definieren. Sie müssen nicht alle Überwachungshooks gleichzeitig verwenden.

Sie können mehrere Überwachungs-Hook-Objekte definieren. Alle Objekte mit der angegebenen Methode werden aufgerufen, wenn das entsprechende Ereignis ausgelöst wird.

>[!TIP]
>
>Unten finden Sie eine Beispielseite mit allen implementierten Monitoring-Hooks.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script>
    window.__alloyMonitors = window.__alloyMonitors || [];
    window.__alloyMonitors.push({
      onInstanceCreated(data) {
        // data.instanceName
        // data.instance
      },
      onInstanceConfigured(data) {
        // data.instanceName
        // data.config
      },
      onBeforeCommand(data) {
        // data.instanceName
        // data.commandName
        // data.options
      },
      // Added in version 2.4.0
      onCommandResolved(data) {
        // data.instanceName
        // data.commandName
        // data.options
        // data.result
      },
      // Added in version 2.4.0
      onCommandRejected(data) {
        // data.instanceName
        // data.commandName
        // data.options
        // data.error
      },
      onBeforeNetworkRequest(data) {
        // data.instanceName
        // data.requestId
        // data.url
        // data.payload
      },
      onNetworkResponse(data) {
        // data.instanceName
        // data.requestId
        // data.url
        // data.payload
        // data.body
        // data.parsedBody
        // data.status
        // data.retriesAttempted
      },
      onNetworkError(data) {
        // data.instanceName
        // data.requestId
        // data.url
        // data.payload
        // data.error
      },
      onBeforeLog(data) {
        // data.instanceName
        // data.componentName
        // data.level
        // data.arguments
      }
      onContentRendering(data) {
        // data.instanceName
        // data.componentName
        // data.payload
        // data.status
      },
      onContentHiding(data) {
        // data.instanceName
        // data.componentName
        // data.status
      }
    });
  </script>
  <script>
      !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
      []).push(o),n[o]=function(){var u=arguments;return new Promise(
      function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
      (window,["alloy"]);
    </script>
    <script src="alloy.js" async></script>
</head>
<body>
  <h1>Monitor Test</h1>
</body>
</html>
```
