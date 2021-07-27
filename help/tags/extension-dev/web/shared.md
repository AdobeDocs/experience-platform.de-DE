---
title: Gemeinsam genutzte Module in Web-Erweiterungen
description: Erfahren Sie, wie Sie gemeinsame Bibliotheksmodule für Web-Erweiterungen in Adobe Experience Platform definieren.
source-git-commit: 99780f64c8f09acea06e47ebf5cabc762e05cab2
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 72%

---

# Gemeinsam genutzte Module in Web-Erweiterungen

>[!NOTE]
>
>Adobe Experience Platform Launch wird als eine Suite von Datenerfassungstechnologien in Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Ein gemeinsames Modul ist ein Mechanismus, der Ihnen ermöglicht, mit anderen Erweiterungen zu kommunizieren. Beispielsweise kann Erweiterung A ein Datenelement asynchron laden und es über ein [Versprechen](https://developer.mozilla.org/de-DE/docs/Web/JavaScript/Reference/Global_Objects/Promise) für Erweiterung B verfügbar machen.

In JavaScript-Implementierungen werden alle gemeinsam genutzten Module mit der [`getSharedModule`](../turbine.md#shared)-Methode instanziiert, die von der freien Variable `turbine` bereitgestellt wird.

Gemeinsame Module werden in Tag-Bibliotheken eingeschlossen, selbst wenn sie nie aus anderen Erweiterungen heraus aufgerufen werden. Um die Bibliotheksgröße nicht unnötig zu erhöhen, sollten Sie vorsichtig damit sein, was Sie als gemeinsames Modul bereitstellen.

Gemeinsame Module verfügen nicht über eine Ansicht-Komponente.

Bei der Entwicklung Ihrer eigenen Tag-Erweiterung können Sie alle freigegebenen Module definieren, die Sie damit bereitstellen möchten. Sie können beispielsweise ein Modul erstellen, das eine User-ID asynchron lädt und dann diese User-ID über ein Versprechen mit einer anderen Erweiterung teilt:

```javascript
var userIdPromise = new Promise(/* load user ID, then resolve promise */);
module.exports = userIdPromise;
```

Im [Erweiterungsmanifest](../manifest.md) müssen Sie einen Namen für dieses gemeinsame Modul angeben. Wenn Sie es `user-id-promise` nennen, kann eine andere Erweiterung wie folgt auf dieses gemeinsame Modul zugreifen:

```javascript
var userIdPromise = turbine.getSharedModule('user-extension', 'user-id-promise');
```

Gemeinsame Module können alles sein, was Sie normalerweise aus einem CommonJS-Modul exportieren könnten (z. B. Funktionen, Objekte, Zeichenfolgen, Zahlen oder Boolesche Werte).
