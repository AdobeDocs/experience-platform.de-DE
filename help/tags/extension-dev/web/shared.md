---
title: Gemeinsam genutzte Module in Web-Erweiterungen
description: Erfahren Sie, wie Sie in Adobe Experience Platform gemeinsame Bibliotheksmodule für Web-Erweiterungen definieren können.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: ht
source-wordcount: '272'
ht-degree: 100%

---

# Gemeinsam genutzte Module in Web-Erweiterungen

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere Terminologieänderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Ein gemeinsames Modul ist ein Mechanismus, der Ihnen ermöglicht, mit anderen Erweiterungen zu kommunizieren. Beispielsweise kann Erweiterung A ein Datenelement asynchron laden und es über ein [Versprechen](https://developer.mozilla.org/de-DE/docs/Web/JavaScript/Reference/Global_Objects/Promise) für Erweiterung B verfügbar machen.

In JavaScript-Implementierungen werden alle gemeinsam genutzten Module mit der [`getSharedModule`](../turbine.md#shared)-Methode instanziiert, die von der freien Variable `turbine` bereitgestellt wird.

Gemeinsame Module werden auch dann in Tag-Bibliotheken eingeschlossen, wenn sie nie von anderen Erweiterungen aus aufgerufen werden. Um die Bibliotheksgröße nicht unnötig zu erhöhen, sollten Sie vorsichtig damit sein, was Sie als gemeinsames Modul bereitstellen.

Gemeinsame Module verfügen nicht über eine Ansicht-Komponente.

Wenn Sie eine eigene Tag-Erweiterung entwickeln, können Sie alle gemeinsamen Module definieren, die Sie mit ihr bereitstellen möchten. Sie können beispielsweise ein Modul erstellen, das eine User-ID asynchron lädt und dann diese User-ID über ein Versprechen mit einer anderen Erweiterung teilt:

```javascript
var userIdPromise = new Promise(/* load user ID, then resolve promise */);
module.exports = userIdPromise;
```

Im [Erweiterungsmanifest](../manifest.md) müssen Sie einen Namen für dieses gemeinsame Modul angeben. Wenn Sie es `user-id-promise` nennen, kann eine andere Erweiterung wie folgt auf dieses gemeinsame Modul zugreifen:

```javascript
var userIdPromise = turbine.getSharedModule('user-extension', 'user-id-promise');
```

Gemeinsame Module können alles sein, was Sie normalerweise aus einem CommonJS-Modul exportieren könnten (z. B. Funktionen, Objekte, Zeichenfolgen, Zahlen oder Boolesche Werte).
