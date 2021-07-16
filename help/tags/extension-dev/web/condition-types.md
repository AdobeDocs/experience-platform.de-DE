---
title: Bedingungstypen für Web-Erweiterungen
description: Erfahren Sie, wie Sie ein Bibliotheksmodul vom Typ Bedingung für eine Tag-Erweiterung in einer Webeigenschaft definieren.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 80%

---

# Bedingungstypen für Web-Erweiterungen

>[!NOTE]
>
>Adobe Experience Platform Launch wird als eine Suite von Datenerfassungstechnologien in Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Ein Bibliotheksmodul für einen Bedingungstyp dient einem einzigen Ziel: auswerten, ob etwas wahr oder falsch ist. Was es auswertet, legen Sie fest.

>[!NOTE]
>
>In diesem Dokument werden Bedingungstypen für Web-Erweiterungen behandelt. Wenn Sie eine Kantenerweiterung entwickeln, lesen Sie stattdessen das Handbuch zu [Bedingungstypen für Kantenerweiterungen](../edge/condition-types.md).
>
>In diesem Dokument wird außerdem davon ausgegangen, dass Sie mit Bibliotheksmodulen und deren Integration in Tag-Erweiterungen vertraut sind. Wenn Sie eine Einführung benötigen, lesen Sie die Übersicht über die [Formatierung von Bibliotheksmodulen](./format.md), bevor Sie zu diesem Handbuch zurückkehren.

Wenn Sie z. B. prüfen möchten, ob sich der Benutzer auf dem Host `example.com` befindet, könnte Ihr Modul wie folgt aussehen:

```js
module.exports = function(settings) {
  return document.location.hostname === 'example.com';
};
```

Betrachten Sie nun eine Situation, in der Sie den Hostnamen vom Adobe Experience Platform-Benutzer konfigurierbar machen möchten. Sie können dem Benutzer erlauben, einen Hostnamen einzugeben, und dann den Hostnamen im settings-Objekt speichern. Das Objekt könnte etwa so aussehen:

```js
{
  "hostname": "example.com"
}
```

Um mit dem benutzerdefinierten Hostnamen arbeiten zu können, muss das Modul wie folgt geändert werden:

```js
module.exports = function(settings) {
  return document.location.hostname === settings.hostname;
};
```

## Kontextbezogene Ereignisdaten

Ein zweites Argument wird an Ihr Modul übergeben, das Kontextinformationen zum Ereignis enthält, das die Regel ausgelöst hat. Das kann in bestimmten Fällen von Vorteil sein. Auf dieses Argument wird wie folgt zugegriffen:

```js
module.exports = function(settings, event) {
  // event contains information regarding the event that fired the rule
};
```

Das `event`-Objekt muss die folgenden Eigenschaften enthalten:

| Eigenschaft | Beschreibung |
| --- | --- |
| `$type` | Eine Zeichenfolge, die den Erweiterungsnamen und den Namen des Ereignisses beschreibt, die mit einem Punkt verbunden sind. Beispiel: `youtube.play`. |
| `$rule` | Ein Objekt, das Informationen zu der Regel enthält, die derzeit ausgeführt wird. Das Objekt muss die folgenden Untereigenschaften enthalten:<ul><li>`id`: Die ID der derzeit ausgeführten Regel.</li><li>`name`: Der Name der derzeit ausgeführten Regel.</li></ul> |

Die Erweiterung, die den Ereignistyp bereitstellt, der die Regel ausgelöst hat, kann optional weitere nützliche Informationen zu diesem `event`-Objekt hinzufügen.
