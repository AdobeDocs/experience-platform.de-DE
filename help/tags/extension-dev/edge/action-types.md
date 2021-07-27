---
title: Aktionstypen für Edge-Erweiterungen
description: Erfahren Sie, wie Sie ein Bibliotheksmodul für Aktionstyp für eine Tag-Erweiterung in einer Edge-Eigenschaft definieren.
source-git-commit: 99780f64c8f09acea06e47ebf5cabc762e05cab2
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 45%

---

# Aktionstypen für Edge-Erweiterungen

>[!NOTE]
>
>Adobe Experience Platform Launch wird als eine Suite von Datenerfassungstechnologien in Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

In einer Tag-Regel wird eine Aktion ausgeführt, nachdem die Auswertung der Regelbedingungen abgeschlossen wurde. Aktionstypen werden von Erweiterungen bereitgestellt und ihre Auswirkungen werden vollständig vom Autor der Erweiterung definiert.

Beispielsweise könnte eine Erweiterung einen Aktionstyp „Support-Chat anzeigen“ bereitstellen, der einen Dialog mit dem Support-Chat anzeigen könnte, um Benutzern zu helfen, die beim Auschecken Probleme haben.

In diesem Dokument wird beschrieben, wie Sie Aktionstypen für eine Kantenerweiterung in Adobe Experience Platform definieren.

>[!IMPORTANT]
>
>Wenn Sie eine Web-Erweiterung entwickeln, lesen Sie stattdessen das Handbuch zu [Aktionstypen für Web-Erweiterungen](../web/action-types.md).
>
>In diesem Dokument wird außerdem davon ausgegangen, dass Sie mit Bibliotheksmodulen und deren Integration in Edge-Erweiterungen vertraut sind. Wenn Sie eine Einführung benötigen, lesen Sie die Übersicht über die [Formatierung von Bibliotheksmodulen](./format.md), bevor Sie zu diesem Handbuch zurückkehren.

Aktionstypen bestehen in der Regel aus den folgenden:

1. Eine Ansicht, die in der Datenerfassungs-Benutzeroberfläche angezeigt wird und es Benutzern ermöglicht, die Einstellungen für die Aktion zu ändern.
2. Ein Bibliotheksmodul wird in der Tag-Laufzeitbibliothek ausgegeben, um die Einstellungen zu interpretieren und eine Aktion durchzuführen.

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
