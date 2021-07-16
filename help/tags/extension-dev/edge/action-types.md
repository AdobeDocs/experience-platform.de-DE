---
title: Aktionstypen für Edge-Erweiterungen
description: Erfahren Sie, wie Sie ein Bibliotheksmodul für Aktionstyp für eine Tag-Erweiterung in einer Edge-Eigenschaft definieren.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 49%

---

# Aktionstypen für Edge-Erweiterungen

>[!NOTE]
>
>Adobe Experience Platform Launch wird als eine Suite von Datenerfassungstechnologien in Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Ein Bibliotheksmodul für Aktionstypen ist für eine vordefinierte Aktion konzipiert. Die Wirkung dieser Aktion wird vom Autor vollständig definiert. Das Modul kann als Beacon erstellt werden oder sogar einige Daten aus dem Ereignis transformieren.

>[!IMPORTANT]
>
>In diesem Dokument werden Aktionstypen für Erweiterungen von Kanten behandelt. Wenn Sie eine Web-Erweiterung entwickeln, lesen Sie stattdessen das Handbuch zu [Aktionstypen für Web-Erweiterungen](../web/action-types.md).
>
>In diesem Dokument wird außerdem davon ausgegangen, dass Sie mit Bibliotheksmodulen und deren Integration in Tag-Erweiterungen vertraut sind. Wenn Sie eine Einführung benötigen, lesen Sie die Übersicht über die [Formatierung von Bibliotheksmodulen](./format.md), bevor Sie zu diesem Handbuch zurückkehren.

Ein Modul zum Weiterleiten einiger Daten an einen Drittanbieter-Endpunkt könnte beispielsweise wie folgt aussehen:

```js
module.exports = (context) {
  const { arc, utils } = context;
  const { fetch } = utils;
  const { event: { xdm } } = arc;
  return fetch('http://someendpoint.com', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(xdm)
  })
};
```

Wenn Sie möchten, dass der Endpunkt vom Benutzer konfiguriert werden kann, und die Eingabe und Persistenz eines Endpunkts für das settings-Objekt innerhalb des Moduls zulassen möchten, würde das Objekt in etwa so aussehen.

```json
{
  "endpoint": "http://someendpoint.com"
}
```

Um mit dem benutzerdefinierten Endpunkt arbeiten zu können, muss Ihr Modul in das folgende Beispiel geändert werden.

```js
module.exports = (context) {
  const { arc, utils } = context;
  const { fetch } = utils;
  const { event: { xdm } } = arc;
  const  { endpoint } = settings;
  return fetch(endpoint, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(xdm)
  })
};
```

## Aktionsergebnis

Das von einem Aktionsmodul zurückgegebene Ergebnis kann jeglicher Art sein. Wenn die Aktion eine asynchrone Aufgabe ausführen muss, können Sie ein [Versprechen](https://developer.mozilla.org/de-DE/docs/Web/JavaScript/Reference/Global_Objects/Promise) zurückgeben, das das gewünschte Ergebnis nach Auflösung zurückgibt.

Das Aktionsergebnis wird innerhalb eines Schlüssels `ruleStash` gespeichert, der allen Modulen über den Parameter `context` (`context.arc.ruleStash`) zur Verfügung gestellt wird. Weitere Informationen zu `ruleStash` finden Sie [hier](./context.md#rulestash).
