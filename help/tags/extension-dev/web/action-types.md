---
title: Aktionstypen für Web-Erweiterungen
description: Erfahren Sie, wie Sie ein Bibliotheksmodul vom Typ „action-type“ für eine Tag-Erweiterung in einer Web-Eigenschaft definieren.
exl-id: d4539132-a72c-40b0-84b6-50cbe3785d2d
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 94%

---

# Aktionstypen für Web-Erweiterungen

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Im Kontext von Datenerfassungs-Tags wird eine Aktion ausgeführt, nachdem ein Regelereignis aufgetreten ist und bei der Auswertung alle Bedingungen erfüllt waren.

Beispielsweise könnte eine Erweiterung einen Aktionstyp „Support-Chat anzeigen“ bereitstellen, der einen Dialog mit dem Support-Chat anzeigen könnte, um Benutzern zu helfen, die beim Auschecken Probleme haben.

In diesem Dokument wird beschrieben, wie Sie Aktionstypen für eine Web-Erweiterung in Adobe Experience Platform definieren.

>[!IMPORTANT]
>
>In diesem Dokument werden Aktionstypen für Web-Erweiterungen behandelt. Wenn Sie eine Kantenerweiterung entwickeln, lesen Sie stattdessen das Handbuch zu [Aktionstypen für Kantenerweiterungen](../edge/action-types.md).
>
>In diesem Dokument wird auch davon ausgegangen, dass Sie mit Bibliotheks-Modulen und deren Integration in Web-Erweiterungen vertraut sind. Wenn Sie eine Einführung benötigen, lesen Sie die Übersicht über die [Formatierung von Bibliotheksmodulen](./format.md), bevor Sie zu diesem Handbuch zurückkehren.

Aktionstypen bestehen in der Regel aus dem Folgenden:

1. A [Ansicht](./views.md) wird in der Experience Platform-Benutzeroberfläche und der Datenerfassungs-Benutzeroberfläche angezeigt, über die Benutzer die Aktionseinstellungen ändern können.
2. Ein Bibliotheksmodul, das in der Tag-Laufzeitbibliothek ausgegeben wird, um die Einstellungen zu interpretieren und eine Aktion durchzuführen.

```js
module.exports = function(settings) {
  alert('Thanks for visiting our site!');
};
```

Damit die Nachricht beispielsweise vom Adobe Experience Platform-Benutzer konfiguriert werden kann, können Sie dem Benutzer die Eingabe und Speicherung einer Nachricht im Einstellungsobjekt ermöglichen. Das Objekt sieht ungefähr so aus:

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
