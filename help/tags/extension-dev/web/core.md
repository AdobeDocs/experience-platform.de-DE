---
title: Die wichtigsten Bibliotheksmodule für Web-Erweiterungen
description: Hier erfahren Sie mehr über die wichtigsten Bibliotheksmodule, die Sie in Ihren Web-Erweiterungen verwenden können.
exl-id: 7fb63208-aed0-4add-b6da-8e4aea063d0a
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 100%

---

# Die wichtigsten Bibliotheksmodule für Web-Erweiterungen

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Dieses Dokument enthält eine Liste der wichtigsten Module, die Sie in Ihren Web-Erweiterungen verwenden können. Sie können mit `require('@adobe/{MODULE}')` auf diese Module zugreifen, wobei `{MODULE}` für den Namen des zu verwendenden Hauptmoduls steht.

## [!DNL reactor-object-assign]

`reactor-object-assign` imitiert die native [`Object.assign`](https://developer.mozilla.org/de-DE/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)-Methode, indem Eigenschaften von Quellobjekten in ein Zielobjekt kopiert werden.

```javascript
var objectAssign = require('@adobe/reactor-object-assign');
var all = objectAssign({ a: 'a' }, { b: 'b' });
```

## [!DNL reactor-cookie]

Das `reactor-cookie`-Objekt ist ein Dienstprogramm zum Lesen und Schreiben von Cookies. Weitere Informationen finden Sie im npm-Paket [js-cookie](https://www.npmjs.com/package/js-cookie).

```javascript
var cookie = require('@adobe/reactor-cookie');
cookie.set('foo', 'bar');
console.log(cookie.get('foo'));
cookie.remove('foo');
```

### [!DNL reactor-document]

`reactor-document` stellt das [`Document`](https://developer.mozilla.org/de-DE/docs/Web/API/Document)-Objekt dar. Dies kann beim Testen des Moduls nützlich sein, da Tests die Imitation eines `document`-Objekts mithilfe von Dienstprogrammen wie [`inject-loader`](https://www.npmjs.com/package/inject-loader) injizieren können.

```javascript
var document = require('@adobe/reactor-document');
console.log(document.location);
```

### [!DNL reactor-query-string]

`reactor-query-string` ist ein Dienstprogramm zum Analysieren und Serialisieren von [Abfragezeichenfolgen](https://developer.mozilla.org/en-US/docs/Web/API/HTMLHyperlinkElementUtils/search).

```javascript
var queryString = require('@adobe/reactor-query-string');
var parsed = queryString.parse(location.search);
console.log(parsed.campaign);
var obj = {
  campaign: 'Campaign A'
};
var stringified = queryString.stringify(obj);
```

Das Dienstprogramm verfügt über die folgenden Methoden:

* `queryString.parse({STRING})`: Analysiert eine Abfragezeichenfolge in ein Objekt. Gegebenenfalls vorhandene Zeichen `?`, `#` und `&` am Anfang der Abfragezeichenfolge werden ignoriert.
* `queryString.stringify({OBJECT})`: Verwandelt ein Objekt in eine Abfragezeichenfolge.

### [!DNL reactor-load-script]

`reactor-load-script` ist eine Funktion, die ein Skript lädt, wenn ihr eine URL übergeben wird. Es wird ein Script-Tag erstellt und in den `head`-Knoten des Dokuments eingefügt. Es wird ein [promise](https://developer.mozilla.org/de-DE/docs/Web/JavaScript/Reference/Global_Objects/Promise)-Objekt zurückgegeben, mit dem Sie bestimmen können, wann das Laden des Skripts erfolgreich ist oder fehlschlägt.

```javascript
var loadScript = require('@adobe/reactor-load-script');
var url = 'http://code.jquery.com/jquery-3.1.1.js';
loadScript(url).then(function() {
  // Do something ...
})
```

### [!DNL reactor-promise]

`reactor-promise` ist ein Konstruktor, der die native [Promise-API](https://developer.mozilla.org/de-DE/docs/Web/JavaScript/Reference/Global_Objects/Promise) in ECMAScript 6 imitiert. Wenn die native Promise-API verfügbar ist, wird sie stattdessen zurückgegeben.

```javascript
var Promise = require('@adobe/reactor-promise');
new Promise(function(resolve) {
  resolve();
}, function(err) {
  console.error(err);
});
```

### [!DNL reactor-window]

`reactor-window` stellt das [`Window`](https://developer.mozilla.org/de-DE/docs/Web/API/Window)-Objekt dar. Dies kann beim Testen des Moduls nützlich sein, da Tests die Imitation eines `Window`-Objekts mithilfe von Dienstprogrammen wie [`inject-loader`](https://www.npmjs.com/package/inject-loader) injizieren können.

```javascript
var window = require('@adobe/reactor-window');
console.log(window.document);
```
