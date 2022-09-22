---
title: Bibliotheksmodule in Web-Erweiterungen
description: Erfahren Sie, wie Sie Bibliotheksmodule für Web-Erweiterungen in Adobe Experience Platform formatieren.
exl-id: 08f2bb01-9071-49c5-a0ff-47d592cc34a5
source-git-commit: b3754c94843f32ba58aa1e020dface1179372de3
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 100%

---

# Bibliotheksmodule in Web-Erweiterungen

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

>[!IMPORTANT]
>
>Dieses Dokument behandelt das Bibliotheksmodulformat für Web-Erweiterungen. Wenn Sie eine Kantenerweiterung entwickeln, lesen Sie stattdessen das Handbuch zum [Formatieren von Kantenerweiterungsmodulen](../edge/format.md).

Ein Bibliotheksmodul ist ein Teil des wiederverwendbaren Codes, der von einer Erweiterung bereitgestellt wird, die innerhalb der Tag-Laufzeitbibliothek in Adobe Experience Platform ausgegeben wird. Diese Bibliothek wird dann auf der Website des Kunden ausgeführt. Beispielsweise verfügt der Ereignistyp `gesture` über ein Bibliotheksmodul, das auf der Website des Client ausgeführt wird und Benutzergesten erkennt.

Das Bibliotheksmodul hat die Struktur eines [CommonJS-Moduls](https://nodejs.org/api/modules.html#modules-commonjs-modules). In einem CommonJS-Modul stehen die folgenden Variablen zur Verwendung zur Verfügung:

## `require`

Die Funktion `require` ist verfügbar zum Zugriff auf:

1. Hauptmodule, die von Tags bereitgestellt werden. Auf diese Module kann mit `require('@adobe/reactor-name-of-module')` zugegriffen werden. Weitere Informationen finden Sie im Dokument zu verfügbaren [Hauptmodulen](./core.md).
1. Andere Module in Ihrer Erweiterung. Über einen relativen Pfad kann auf jedes Modul in Ihrer Erweiterung zugegriffen werden. Der relative Pfad muss mit `./` oder `../` beginnen.

Beispiel:

```javascript
var cookie = require('@adobe/reactor-cookie');
cookie.set('foo', 'bar');
```

## `module`

Es ist eine freie Variable namens `module` verfügbar, mit der Sie die API des Moduls exportieren können.

Beispiel:

```javascript
module.exports = function(…) { … }
```

## `exports` {#exports-variable}

Es ist eine freie Variable namens `exports` verfügbar, mit der Sie die API des Moduls exportieren können.

Beispiel:

```javascript
exports.sayHello = function(…) { … }
```

Dies ist eine Alternative zu `module.exports`, die in ihrer Verwendung jedoch eingeschränkter ist. Lesen Sie [Understanding module.exports and exports in node.js](https://www.sitepoint.com/understanding-module-exports-exports-node-js/), um die Unterschiede zwischen `module.exports` und `exports` sowie die mit der Verwendung von `exports` verbundenen Vorbehalte besser zu verstehen. Im Zweifelsfall verwenden Sie `module.exports` statt `exports`, da dies einfacher ist.

## Ausführung und Caching

Wenn die Tag-Laufzeitbibliothek ausgeführt wird, werden die Module sofort „installiert“ und ihre Exporte zwischengespeichert. Angenommen, Sie haben folgendes Modul:

```javascript
console.log('runs on startup');

module.exports = function(settings) {
  console.log('runs when necessary');
}
```

`runs on startup` wird sofort protokolliert, während `runs when necessary` erst protokolliert wird, wenn die exportierte Funktion von der Tag-Engine aufgerufen wird. Obwohl dies für die Zwecke Ihres speziellen Moduls möglicherweise nicht erforderlich ist, können Sie es nutzen, indem Sie vor dem Exportieren der Funktion alle erforderlichen Einstellungen vornehmen.
