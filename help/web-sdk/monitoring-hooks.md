---
title: Überwachungs-Hooks für Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie mit den von Adobe Experience Platform Web SDK bereitgestellten Überwachungs-Hooks Ihre Implementierung debuggen und Web SDK-Protokolle erfassen können.
exl-id: 56633311-2f89-4024-8524-57d45c7d38f7
source-git-commit: 5550e757eae95e529d74115df9bbe9b635d25ec8
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 6%

---

# Überwachungs-Hooks für Web SDK

Adobe Experience Platform Web SDK enthält Überwachungs-Hooks, mit denen Sie verschiedene Systemereignisse überwachen können. Diese Tools sind nützlich, um eigene Debugging-Tools zu entwickeln und Web SDK-Protokolle zu erfassen.

Die Web SDK-Trigger übernehmen die Überwachungsfunktionen unabhängig davon, ob Sie „Debugging[ aktiviert ](commands/configure/debugenabled.md).

## `onInstanceCreated` {#onInstanceCreated}

Diese Rückruffunktion wird ausgelöst, wenn Sie erfolgreich eine neue Web SDK-Instanz erstellt haben. Siehe folgendes Beispiel für Details zu den Funktionsparametern.

```js
onInstanceCreated(data) {
    // data.instanceName
    // data.instance
}
```

| Parameter | Typ | Beschreibung |
|---------|----------|----------|
| `data.instanceName` | Zeichenfolge | Der Name der globalen Variablen, in der die Web-SDK-Instanz gespeichert ist. |
| `data.instance` | Funktion | Die zum Aufrufen von Web-SDK-Befehlen verwendete Instanzfunktion. |

## `onInstanceConfigured` {#onInstanceConfigured}

Diese Rückruffunktion wird von der Web-SDK ausgelöst, wenn der [`configure`](commands/configure/overview.md) erfolgreich aufgelöst wurde. Siehe folgendes Beispiel für Details zu den Funktionsparametern.

```js
 onInstanceConfigured(data) {
     // data.instanceName
     // data.config
 }
```

| Parameter | Typ | Beschreibung |
|---------|----------|----------|
| `data.instanceName` | Zeichenfolge | Der Name der globalen Variablen, in der die Web-SDK-Instanz gespeichert ist. |
| `data.config` | Objekt | Ein Objekt, das die Konfiguration enthält, die Sie für Ihre SDK-Webinstanz verwendet haben. Dies sind die Optionen, die an den [`configure`](commands/configure/overview.md)-Befehl übergeben werden, wobei alle Standardwerte hinzugefügt werden. |

## `onBeforeCommand` {#onBeforeCommand}

Diese Rückruffunktion wird von Web SDK ausgelöst, bevor ein anderer Befehl ausgeführt wird. Mit dieser Funktion können Sie die Konfigurationsoptionen eines bestimmten Befehls abrufen. Siehe folgendes Beispiel für Details zu den Funktionsparametern.

```js
onBeforeCommand(data) {
    // data.instanceName
    // data.commandName
    // data.options
}
```

| Parameter | Typ | Beschreibung |
|---------|----------|----------|
| `data.instanceName` | Zeichenfolge | Der Name der globalen Variablen, in der die Web-SDK-Instanz gespeichert ist. |
| `data.commandName` | String | Der Name des Web-SDK-Befehls, vor dem diese Funktion ausgeführt wird. |
| `data.options` | Objekt | Ein -Objekt, das die Optionen enthält, die an den Web SDK-Befehl übergeben werden. |

## `onCommandResolved` {#onCommandResolved}

Diese Rückruffunktion wird ausgelöst, wenn Befehlszusagen aufgelöst werden. Sie können diese Funktion verwenden, um die Befehlsoptionen und das Ergebnis anzuzeigen. Siehe folgendes Beispiel für Details zu den Funktionsparametern.

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
| `data.instanceName` | Zeichenfolge | Der Name der globalen Variablen, in der die Web-SDK-Instanz gespeichert ist. |
| `data.commandName` | String | Der Name des ausgeführten Web SDK-Befehls. |
| `data.options` | Objekt | Ein -Objekt, das die Optionen enthält, die an den Web SDK-Befehl übergeben werden. |
| `data.result` | Objekt | Ein Objekt, das das Ergebnis des Web-SDK-Befehls enthält. |

## `onCommandRejected` {#onCommandRejected}

Diese Rückruffunktion wird ausgelöst, bevor eine Befehlszusage abgelehnt wird, und enthält Informationen über den Grund, warum der Befehl abgelehnt wurde. Siehe folgendes Beispiel für Details zu den Funktionsparametern.

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
| `data.instanceName` | Zeichenfolge | Der Name der globalen Variablen, in der die Web-SDK-Instanz gespeichert ist. |
| `data.commandName` | String | Der Name des ausgeführten Web SDK-Befehls. |
| `data.options` | Objekt | Ein -Objekt, das die Optionen enthält, die an den Web SDK-Befehl übergeben werden. |
| `data.error` | Objekt | Ein Objekt, das die Fehlermeldung enthält, die vom Netzwerkaufruf des Browsers zurückgegeben wurde (in den meisten Fällen `fetch`), zusammen mit dem Grund, warum der Befehl abgelehnt wurde. |

## `onBeforeNetworkRequest` {#onBeforeNetworkRequest}

Diese Rückruffunktion wird ausgelöst, bevor eine Netzwerkanfrage ausgeführt wird. Siehe folgendes Beispiel für Details zu den Funktionsparametern.

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
| `data.instanceName` | Zeichenfolge | Der Name der globalen Variablen, in der die Web-SDK-Instanz gespeichert ist. |
| `data.requestId` | String | Die von Web SDK generierte `requestId`, um das Debugging zu aktivieren. |
| `data.url` | String | Die angeforderte URL. |
| `data.payload` | Objekt | Das Payload-Objekt der Netzwerkanfrage, das in das JSON-Format konvertiert und über eine `POST`-Methode im Hauptteil der Anfrage gesendet wird. |

## `onNetworkResponse` {#onNetworkResponse}

Diese Rückruffunktion wird ausgelöst, wenn der Browser eine Antwort erhält. Siehe folgendes Beispiel für Details zu den Funktionsparametern.

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
| `data.instanceName` | Zeichenfolge | Der Name der globalen Variablen, in der die Web-SDK-Instanz gespeichert ist. |
| `data.requestId` | String | Die von Web SDK generierte `requestId`, um das Debugging zu aktivieren. |
| `data.url` | String | Die angeforderte URL. |
| `data.payload` | Objekt | Das Payload-Objekt, das in das JSON-Format konvertiert und über eine `POST`-Methode im Hauptteil der Anfrage gesendet wird. |
| `data.body` | String | Der Antworttext im Zeichenfolgenformat. |
| `data.parsedBody` | Objekt | Ein Objekt, das den analysierten Antworttext enthält. Wenn beim Analysieren des Antworttextes ein Fehler auftritt, ist dieser Parameter nicht definiert. |
| `data.status` | String | Der Antwort-Code im ganzzahligen Format. |
| `data.retriesAttempted` | Ganzzahl | Die Anzahl weiterer Versuche, die beim Senden der Anfrage unternommen wurden. Null bedeutet, dass die Anfrage beim ersten Versuch erfolgreich war. |

## `onNetworkError` {#onNetworkError}

Diese Rückruffunktion wird ausgelöst, wenn die Netzwerkanfrage fehlgeschlagen ist. Siehe folgendes Beispiel für Details zu den Funktionsparametern.

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
| `data.instanceName` | Zeichenfolge | Der Name der globalen Variablen, in der die Web-SDK-Instanz gespeichert ist. |
| `data.requestId` | String | Die von Web SDK generierte `requestId`, um das Debugging zu aktivieren. |
| `data.url` | String | Die angeforderte URL. |
| `data.payload` | Objekt | Das Payload-Objekt, das in das JSON-Format konvertiert und über eine `POST`-Methode im Hauptteil der Anfrage gesendet wird. |
| `data.error` | Objekt | Ein Objekt, das die Fehlermeldung enthält, die vom Netzwerkaufruf des Browsers zurückgegeben wurde (in den meisten Fällen `fetch`), zusammen mit dem Grund, warum der Befehl abgelehnt wurde. |

## `onBeforeLog` {#onBeforeLog}

Diese Rückruffunktion wird ausgelöst, bevor Web SDK etwas in der Konsole protokolliert. Siehe folgendes Beispiel für Details zu den Funktionsparametern.

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
| `data.instanceName` | Zeichenfolge | Der Name der globalen Variablen, in der die Web-SDK-Instanz gespeichert ist. |
| `data.componentName` | String | Der Name der Komponente, die die Protokollmeldung generiert hat. |
| `data.level` | String | Die Protokollierungsebene. Unterstützte Ebenen: `log`, `info`, `warn`, `error`. |
| `data.arguments` | Zeichenfolgen-Array | Die Argumente der Protokollmeldung. |


## `onContentRendering` {#onContentRendering}

Diese Rückruffunktion wird von der `personalization`-Komponente in verschiedenen Renderingphasen ausgelöst. Die Payload kann je nach `status` unterschiedlich sein. Siehe folgendes Beispiel für Details zu den Funktionsparametern.

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
| `data.instanceName` | Zeichenfolge | Der Name der globalen Variablen, in der die Web-SDK-Instanz gespeichert ist. |
| `data.componentName` | String | Der Name der Komponente, die die Protokollmeldung generiert hat. |
| `data.payload` | Objekt | Das Payload-Objekt, das in das JSON-Format konvertiert und über eine `POST`-Methode im Hauptteil der Anfrage gesendet wird. |
| `data.status` | String | Die `personalization` benachrichtigt die Web-SDK über den Rendering-Status.  Unterstützte Werte: <ul><li>`rendering-started`: Gibt an, dass Web SDK Vorschläge rendern wird. Bevor Web SDK mit dem Rendern eines Entscheidungsumfangs oder einer Ansicht beginnt, können Sie im `data` die Vorschläge sehen, die von der `personalization` gerendert werden sollen, sowie den Namen des Bereichs.</li><li>`no-offers`: Gibt an, dass für die angeforderten Parameter keine Payload empfangen wurde.</li> <li>`rendering-failed`: Gibt an, dass Web SDK einen Vorschlag nicht rendern konnte.</li><li>`rendering-succeeded`: Gibt an, dass das Rendering für einen Entscheidungsumfang abgeschlossen ist.</li> <li>`rendering-redirect`: Gibt an, dass Web SDK einen Umleitungsvorschlag rendert.</li></ul> |

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
| `data.instanceName` | Zeichenfolge | Der Name der globalen Variablen, in der die Web-SDK-Instanz gespeichert ist. |
| `data.componentName` | String | Der Name der Komponente, die die Protokollmeldung generiert hat. |
| `data.status` | String | Die `personalization` benachrichtigt die Web-SDK über den Rendering-Status. Unterstützte Werte: <ul><li>`hide-containers`</li><li>`show-containers`</ul> |

## Angeben von Überwachungs-Hooks bei Verwendung des NPM-Pakets {#specify-monitoris-npm}

Wenn Sie Web SDK über das [NPM-Paket](install/npm.md) verwenden, können Sie Überwachungs-Hooks in der `createInstasnce` angeben, wie unten dargestellt.

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

Web SDK sucht in einer globalen Variablen namens `__alloyMonitors` nach einem Array von Objekten.

Um alle Web SDK-Ereignisse zu erfassen, müssen Sie Ihre Überwachungs-Hooks definieren, bevor der Web SDK-Code auf Ihrer Seite geladen wird. Jede Überwachungsmethode erfasst ein Web SDK-Ereignis.

Sie können Überwachungs-Hooks (*)* Laden von Web SDK-Code auf Ihrer Seite definieren, aber alle Hooks, die vor dem Laden der Seite ausgelöst wurden, *nicht*.

Wenn Sie Ihr Überwachungs-Hook-Objekt definieren, müssen Sie nur die Methoden definieren, für die Sie eine spezielle Logik definieren möchten.
Wenn Ihnen beispielsweise nur `onContentRendering` wichtig ist, können Sie einfach diese Methode definieren. Sie müssen nicht alle Überwachungs-Hooks gleichzeitig verwenden.

Sie können mehrere Überwachungs-Hook-Objekte definieren. Alle Objekte mit der angegebenen Methode werden aufgerufen, wenn das entsprechende Ereignis ausgelöst wird.

>[!TIP]
>
>Unten finden Sie eine Beispielseite mit allen implementierten Überwachungs-Hooks.

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
