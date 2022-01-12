---
title: Bibliotheksmodule in Edge-Erweiterungen
description: Formatieren Sie Bibliotheksmodule für Tag-Erweiterungen in einer Edge-Eigenschaft.
exl-id: 82b98972-6fa2-4143-bcf4-c5dac1ca0e7f
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 98%

---

# Bibliotheksmodule in Edge-Erweiterungen

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

>[!IMPORTANT]
>
>Dieses Dokument behandelt das Bibliotheksmodulformat für Edge-Erweiterungen. Wenn Sie eine Web-Erweiterung entwickeln, lesen Sie stattdessen das Handbuch für das [Formatieren von Web-Erweiterungsmodulen](../web/format.md).

Ein Bibliotheksmodul ist wiederverwendbarer Code, der von einer Erweiterung bereitgestellt wird, die in der Tag-Laufzeitbibliothek (der Bibliothek, die auf dem Edge-Knoten ausgeführt wird) ausgegeben wird. Ein `sendBeacon`-Aktionstyp verfügt beispielsweise über ein Bibliotheksmodul, das auf dem Edge-Knoten ausgeführt wird und einen Beacon sendet.

Das Bibliotheksmodul hat die Struktur eines [CommonJS-Moduls](https://nodejs.org/api/modules.html#modules-commonjs-modules). In einem CommonJS-Modul stehen die folgenden Variablen zur Verwendung zur Verfügung:

## [!DNL require]

Es steht eine `require`-Funktion zum Zugriff auf Module innerhalb Ihrer Erweiterung zur Verfügung. Über einen relativen Pfad kann auf jedes Modul in Ihrer Erweiterung zugegriffen werden. Der relative Pfad muss mit `./` oder `../` beginnen.

Beispiel:

```js
var transformHelper = require('../helpers/transform');
transformHelper.execute({a: 'b'});
```

## [!DNL module]

Es ist eine freie Variable namens `module` verfügbar, mit der Sie die API des Moduls exportieren können.

Beispiel:

```js
module.exports = (…) => { … }
```

## [!DNL exports]

Es ist eine freie Variable namens `exports` verfügbar, mit der Sie die API des Moduls exportieren können.

Beispiel:

```js
exports.sayHello = (…) => { … }
```

Dies ist eine Alternative zu `module.exports`, die in ihrer Verwendung jedoch eingeschränkter ist. Lesen Sie [Understanding module.exports and exports in node.js](https://www.sitepoint.com/understanding-module-exports-exports-node-js/), um die Unterschiede zwischen `module.exports` und `exports` sowie die mit der Verwendung von `exports` verbundenen Vorbehalte besser zu verstehen. Im Zweifelsfall verwenden Sie `module.exports` statt `exports`, da dies einfacher ist.

## Unterschrift des Server-seitigen Moduls

Alle von Ihrer Erweiterung bereitgestellten Modultypen (Datenelemente, Bedingungen oder Aktionen) werden mit denselben Parametern aufgerufen: [context](./context.md).

```js
exports.sayHello = (context) => { … }
```
