---
title: Aktionstypen für Web-Erweiterungen
description: Erfahren Sie, wie Sie ein Bibliotheksmodul für einen Aktionstyp für eine Tag-Erweiterung in einer Webeigenschaft definieren.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 65%

---

# Aktionstypen für Web-Erweiterungen

>[!NOTE]
>
>Adobe Experience Platform Launch wird als eine Suite von Datenerfassungstechnologien in Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Ein Bibliotheksmodul für Aktionstypen ist für eine vordefinierte Aktion vorgesehen. Was diese Aktion tut, liegt ganz bei Ihnen. Möchten Sie einen Beacon senden, ein Angebot anzeigen, dem Benutzer für seinen Besuch danken, ein Cookie speichern oder einen Support-Chat öffnen?

>[!IMPORTANT]
>
>In diesem Dokument werden Aktionstypen für Web-Erweiterungen behandelt. Wenn Sie eine Kantenerweiterung entwickeln, lesen Sie stattdessen das Handbuch zu [Aktionstypen für Kantenerweiterungen](../edge/action-types.md).
>
>In diesem Dokument wird außerdem davon ausgegangen, dass Sie mit Bibliotheksmodulen und deren Integration in Tag-Erweiterungen vertraut sind. Wenn Sie eine Einführung benötigen, lesen Sie die Übersicht über die [Formatierung von Bibliotheksmodulen](./format.md), bevor Sie zu diesem Handbuch zurückkehren.

```js
module.exports = function(settings) {
  alert('Thanks for visiting our site!');
};
```

Damit die Nachricht beispielsweise vom Adobe Experience Platform-Benutzer konfiguriert werden kann, können Sie dem Benutzer die Eingabe und Speicherung einer Nachricht im settings-Objekt ermöglichen. Das Objekt sieht ungefähr so aus:

```json
{
  "message": "Thank you for being one of our VIP members!"
}
```

Um mit der benutzerdefinierten Meldung arbeiten zu können, muss Ihr Modul Folgendes ändern:

```js
module.exports = function(settings) {
  alert(settings.message);
}
```

## Kontextbezogene Ereignisdaten

Dann muss ein zweites Argument an Ihr Modul übergeben werden, das die Kontextinformationen über das Ereignis enthält, das die Regel auslöst. Das kann in bestimmten Fällen von Vorteil sein. Auf dieses Argument wird wie folgt zugegriffen:

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
