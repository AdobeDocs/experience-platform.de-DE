---
title: Satellitenobjektreferenz
description: Hier erfahren Sie mehr über das Client-seitige _satellite-Objekt und die verschiedenen Funktionen, die Sie damit in Tags ausführen können.
exl-id: f8b31c23-409b-471e-bbbc-b8f24d254761
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 95%

---

# Satellitenobjektreferenz

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Dieses Dokument dient als Referenz für das Client-seitige `_satellite`-Objekt und die verschiedenen Funktionen, die Sie damit ausführen können.

## `track`

**Code**

```javascript
_satellite.track(identifier: string [, detail: *] )
```

**Beispiel**

```javascript
_satellite.track('contact_submit', { name: 'John Doe' });
```

`track` löst alle Regeln mit dem Ereignistyp „Direktaufruf“ aus, der mit der angegebenen Kennung aus der Core-Tag-Erweiterung konfiguriert wurde. Das obige Beispiel löst alle Regeln aus, die einen Direktaufruf-Ereignistyp verwenden, bei dem die konfigurierte ID `contact_submit` lautet. Darüber hinaus wird ein optionales Objekt übergeben, das zugehörige Informationen enthält. Sie können auf das Detailobjekt zugreifen, indem Sie `%event.detail%` in ein Textfeld innerhalb einer Bedingung/Aktion eingeben oder `event.detail` im Code-Editor in einer Bedingung/Aktion für benutzerspezifischen Code eingeben.

## `getVar`

**Code**

```javascript
_satellite.getVar(name: string) => *
```

**Beispiel**

```javascript
var product = _satellite.getVar('product');
```

Wenn ein Datenelement mit dem entsprechenden Namen vorhanden ist, wird der Wert des Datenelements zurückgegeben. Wenn kein passendes Datenelement vorhanden ist, wird überprüft, ob zuvor über `_satellite.setVar()` eine benutzerdefinierte Variable mit dem jeweiligen Namen festgelegt wurde. Wenn eine passende benutzerdefinierte Variable gefunden wird, wird ihr Wert zurückgegeben.

>[!NOTE]
>
>Sie können Prozentwerte (`%`) Syntax, um Variablen für viele Formularfelder in Ihrer Tag-Implementierung zu referenzieren, wodurch der Aufruf von `_satellite.getVar()`. Verwenden Sie beispielsweise `%product%` greift auf den Wert des Produktdatenelements oder der benutzerdefinierten Variablen zu.

Wenn ein Ereignis eine Regel Trigger, können Sie die entsprechende Regel übergeben `event` Objekt in `_satellite.getVar()` wie folgt:

```javascript
// event refers to the calling rule's event
var rule = _satellite.getVar('return event rule', event);
```

## `setVar`

**Code**

```javascript
_satellite.setVar(name: string, value: *)
```

**Beispiel**

```javascript
_satellite.setVar('product', 'Circuit Pro');
```

`setVar()` legt eine benutzerdefinierte Variable mit dem angegebenen Namen und Wert fest. Der Wert der Variablen kann später mithilfe von `_satellite.getVar()` abgerufen werden.

Sie können optional mehrere Variablen auf einmal festlegen, indem Sie ein Objekt übergeben, in dem die Schlüssel die Variablennamen und die Werte die zugehörigen Variablenwerte darstellen.

```javascript
_satellite.setVar({ 'product': 'Circuit Pro', 'category': 'hobby' });
```

## `getVisitorId`

**Code**

```javascript
_satellite.getVisitorId() => Object
```

**Beispiel**

```javascript
var visitorIdInstance = _satellite.getVisitorId();
```

Wenn die [!DNL Adobe Experience Cloud ID]-Erweiterung in der Eigenschaft installiert ist, gibt diese Methode die Besucher-ID-Instanz zurück. Weitere Informationen finden Sie in der [Dokumentation zum Experience Cloud ID-Dienst](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=de).

## `logger`

**Code**

```javascript
_satellite.logger.log(message: string)
```

```javascript
_satellite.logger.info(message: string)
```

```javascript
_satellite.logger.warn(message: string)
```

```javascript
_satellite.logger.error(message: string)
```

**Beispiel**

```javascript
_satellite.logger.error('No product ID found.');
```

Das `logger`-Objekt ermöglicht die Protokollierung einer Nachricht in der Browser-Konsole. Die Meldung wird nur dann angezeigt, wenn das Tag-Debugging durch den Benutzer aktiviert wird (per Aufruf von `_satellite.setDebug(true)` oder Verwendung einer entsprechenden Browser-Erweiterung).

### Protokollierung von Warnmeldungen zu veralteten Dokumenten

```javascript
_satellite.logger.deprecation(message: string)
```

**Beispiel**

```javascript
_satellite.logger.deprecation('This method is no longer supported, please use [new example] instead.');
```

Protokolliert eine Warnung in der Browser-Konsole. Die Meldung wird unabhängig davon angezeigt, ob der Benutzer das Tag-Debugging aktiviert hat.

## `cookie` {#cookie}

`_satellite.cookie` enthält Funktionen zum Lesen und Schreiben von Cookies. Dies ist eine offengelegte Kopie des „js-cookie“ der Drittanbieter-Bibliothek. Weitere Informationen zur weitergehenden Verwendung dieser Bibliothek finden Sie in der [js-cookie-Dokumentation](https://www.npmjs.com/package/js-cookie#basic-usage).

### Setzen eines Cookies {#cookie-set}

Um ein Cookie zu setzen, verwenden Sie `_satellite.cookie.set()`.

**Code**

```javascript
_satellite.cookie.set(name: string, value: string[, attributes: Object])
```

>[!NOTE]
>
>Bei der alten Methode [`setCookie`](#setCookie) zum Setzen von Cookies war das dritte (optionale) Argument für diesen Funktionsaufruf eine Ganzzahl, die die Lebensdauer (Time-to-Live, TTL) des Cookies in Tagen angab. In dieser neuen Methode wird stattdessen ein Objekt „attributes“ als drittes Argument akzeptiert. Um eine TTL für ein Cookie mithilfe der neuen Methode festzulegen, müssen Sie im Attributobjekt die Eigenschaft `expires` angeben und sie auf den gewünschten Wert setzen. Dies wird im folgenden Beispiel demonstriert.

**Beispiel**

Der folgende Funktionsaufruf schreibt ein Cookie, das in einer Woche abläuft.

```javascript
_satellite.cookie.set('product', 'Circuit Pro', { expires: 7 });
```

### Abrufen eines Cookies {#cookie-get}

Um ein Cookie abzurufen, verwenden Sie `_satellite.cookie.get()`.

**Code**

```javascript
_satellite.cookie.get(name: string) => string
```

**Beispiel**

Der folgende Funktionsaufruf liest ein zuvor festgelegtes Cookie.

```javascript
var product = _satellite.cookie.get('product');
```

### Entfernen eines Cookies {#cookie-remove}

Um ein Cookie zu entfernen, verwenden Sie `_satellite.cookie.remove()`.

**Code**

```javascript
_satellite.cookie.remove(name: string)
```

**Beispiel**

Mit dem folgenden Funktionsaufruf wird ein zuvor festgelegtes Cookie entfernt.

```javascript
_satellite.cookie.remove('product');
```

## `buildInfo`

**Code**

```javascript
_satellite.buildInfo
```

Dieses Objekt enthält Informationen zum Build der aktuellen Tag-Laufzeitbibliothek. Das Objekt enthält die folgenden Eigenschaften:

### `turbineVersion`

Stellt die [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine)-Version bereit, die in der aktuellen Bibliothek verwendet wird.

### `turbineBuildDate`

Das ISO-8601-Datum, an dem die im aktuellen Container verwendete [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine)-Version erstellt wurde.

### `buildDate`

Das ISO-8601-Datum, an dem die aktuelle Bibliothek erstellt wurde.

Dieses Beispiel zeigt die Objektwerte:

```javascript
{
  turbineVersion: "14.0.0",
  turbineBuildDate: "2016-07-01T18:10:34Z",
  buildDate: "2016-03-30T16:27:10Z"
}
```

## `environment`

Dieses Objekt enthält Informationen über die Umgebung, in der die aktuelle Tag-Laufzeitbibliothek bereitgestellt wird.

**Code**

```javascript
_satellite.environment
```

Das Objekt enthält die folgenden Eigenschaften:

```javascript
{
  id: "ENbe322acb4fc64dfdb603254ffe98b5d3",
  stage: "development"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `id` | Die ID der Umgebung. |
| `stage` | Die Umgebung, für die diese Bibliothek erstellt wurde. Die möglichen Werte sind `development`, `staging` und `production`. |

## `notify`

>[!NOTE]
>
>Diese Methode wird nicht mehr unterstützt. Verwenden Sie stattdessen `_satellite.logger.log()`.

**Code**

```javascript
_satellite.notify(message: string[, level: number])
```

**Beispiel**

```javascript
_satellite.notify('Hello world!');
```

`notify` protokolliert eine Nachricht in der Browser-Konsole. Die Meldung wird nur angezeigt, wenn das Tag-Debugging vom Benutzer aktiviert wurde (durch Abrufen von `_satellite.setDebug(true)` oder mit einer entsprechenden Browser-Erweiterung).

Eine optionale Protokollebene kann übergeben werden, die sich auf die Formatierung und Filterung der protokollierten Nachricht auswirkt. Folgende Ebenen werden unterstützt:

3 – Informationsmeldungen

4 – Warnmeldungen

5 – Fehlermeldungen

Wenn Sie keine Protokollebene oder einen anderen Wert als die oben angezeigten angeben, wird die Nachricht als normale Meldung protokolliert.

## `setCookie` {#setCookie}

>[!IMPORTANT]
>
>Diese Methode wird nicht mehr unterstützt. Verwenden Sie stattdessen [`_satellite.cookie.set()`](#cookie-set).

**Code**

```javascript
_satellite.setCookie(name: string, value: string, days: number)
```

**Beispiel**

```javascript
_satellite.setCookie('product', 'Circuit Pro', 3);
```

Erstellt ein Cookie im Browser des Benutzers. Das Cookie wird über die angegebene Anzahl an Tagen gespeichert.

## `readCookie`

>[!IMPORTANT]
>
>Diese Methode wird nicht mehr unterstützt. Verwenden Sie stattdessen [`_satellite.cookie.get()`](#cookie-get).

**Code**

```javascript
_satellite.readCookie(name: string) => string
```

**Beispiel**

```javascript
var product = _satellite.readCookie('product');
```

Liest ein Cookie im Browser des Benutzers aus.

## `removeCookie`

>[!NOTE]
>
>Diese Methode wird nicht mehr unterstützt. Verwenden Sie stattdessen [`_satellite.cookie.remove()`](#cookie-remove).

**Code**

```javascript
_satellite.removeCookie(name: string)
```

**Beispiel**

```javascript
_satellite.removeCookie('product');
```

Entfernt ein Cookie aus dem Browser des Benutzers.

## Debugging-Funktionen

Der Zugriff auf die folgenden Funktionen sollte nicht über den Produktions-Code erfolgen. Sie dienen nur Debugging-Zwecken und ändern sich mit der Zeit nach Bedarf.

### `container`

**Code**

```javascript
_satellite._container
```

**Beispiel**

>[!IMPORTANT]
>
>Der Zugriff auf diese Funktion sollte nicht über den Produktions-Code erfolgen. Sie dient lediglich Debugging-Prozessen und ändert sich bei Bedarf im Laufe der Zeit.

### `monitor`

**Code**

```javascript
_satellite._monitors
```

**Beispiel**

>[!IMPORTANT]
>
>Der Zugriff auf diese Funktion sollte nicht über den Produktions-Code erfolgen. Sie dient lediglich Debugging-Prozessen und ändert sich bei Bedarf im Laufe der Zeit.

**Beispiel**

Fügen Sie auf Ihrer Web-Seite, auf der eine Tag-Bibliothek ausgeführt wird, dem HTML-Code ein Code-Fragment hinzu. In der Regel wird der Code in das Element `<head>` vor dem Element `<script>` eingefügt, das die Tag-Bibliothek lädt. Dadurch kann der Monitor die frühesten Systemereignisse in der Tag-Bibliothek erfassen. Beispiel:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script>
    window._satellite = window._satellite || {};
    window._satellite._monitors = window._satellite._monitors || [];
    window._satellite._monitors.push({
      ruleTriggered: function (event) {
        console.log(
          'rule triggered',
          event.rule
        );
      },
      ruleCompleted: function (event) {
        console.log(
          'rule completed',
          event.rule
        );
      },
      ruleConditionFailed: function (event) {
        console.log(
          'rule condition failed',
          event.rule,
          event.condition
        );
      }
    });
  </script>
  <script src="//assets.adobedtm.com/launch-EN5bfa516febde4b22b3e7c6f96f6b439f.min.js"
          async></script>
</head>
<body>
  <h1>Click me!</h1>
</body>
</html>
```

Da die Tag-Bibliothek noch nicht geladen wurde, wird im ersten Skriptelement das anfängliche `_satellite`-Objekt erstellt und ein Array wird auf `_satellite._monitors` initialisiert. Das Skript fügt diesem Array dann ein Monitorobjekt hinzu. Das Monitorobjekt kann die folgenden Methoden angeben, die später von der Tag-Bibliothek aufgerufen werden:

### `ruleTriggered`

Die Funktion wird aufgerufen, nachdem ein Ereignis eine Regel ausgelöst hat, aber bevor die Bedingungen und Aktionen der Regel verarbeitet wurden. Das Ereignisobjekt, das an `ruleTriggered` übergeben wird, enthält Informationen zu der ausgelösten Regel.

### `ruleCompleted`

Diese Funktion wird aufgerufen, nachdem eine Regel vollständig verarbeitet wurde. Das heißt, das Ereignis ist eingetreten, alle Bedingungen wurden übergeben und alle Aktionen ausgeführt. Das an `ruleCompleted` übergebene Ereignisobjekt enthält Informationen über die abgeschlossene Regel.

### `ruleConditionFailed`

Diese Funktion wird aufgerufen, nachdem eine Regel ausgelöst wurde und eine der Bedingungen fehlgeschlagen ist. Das Ereignisobjekt, das an `ruleConditionFailed` übergeben wird, enthält Informationen zu der ausgelösten Regel und der fehlgeschlagenen Bedingung.

Wenn `ruleTriggered` aufgerufen wird, werden kurz darauf auch `ruleCompleted` oder `ruleConditionFailed` aufgerufen.

>[!NOTE]
>
>Der Monitor muss nicht mehr alle drei Methoden festlegen (`ruleTriggered`, `ruleCompleted` und `ruleConditionFailed`). Tags in Adobe Experience Platform funktionieren mit allen unterstützten Methoden, die vom Monitor bereitgestellt wurden.

### Testen des Monitors

Im obigen Beispiel werden alle drei Methoden im Monitor angegeben. Wenn sie aufgerufen werden, zeigt der Monitor relevante Informationen an. Um dies zu testen, richten Sie zwei Regeln in der Tag-Bibliothek ein:

1. Eine Regel mit einem Klick-Ereignis und eine Browser-Bedingung, die nur dann übergeben wird, wenn der Browser [!DNL Chrome] ist.
1. Eine Regel mit einem Klick-Ereignis und eine Browser-Bedingung, die nur dann übergeben wird, wenn der Browser [!DNL Firefox] ist.

Wenn Sie die Seite in [!DNL Chrome] öffnen, die Browser-Konsole öffnen und auf die Seite klicken, wird Folgendes in der Konsole angezeigt:

![](../../images/debug.png)

Sie können diesen Handlern nach Bedarf zusätzliche Hooks und Informationen hinzufügen.
