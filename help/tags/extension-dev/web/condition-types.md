---
title: Bedingungstypen für Web-Erweiterungen
description: Erfahren Sie, wie Sie ein Bibliotheksmodul vom Typ „condition-type“ für eine Tag-Erweiterung in einer Web-Eigenschaft definieren.
exl-id: db504455-858b-4ac8-aa42-de516b0f1d5a
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Bedingungstypen für Web-Erweiterungen

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Im Kontext einer Regel wird eine Bedingung ausgewertet, nachdem ein Ereignis aufgetreten ist. Alle Bedingungen müssen „true“ zurückgeben, damit die Regel weiter verarbeitet wird. Eine Ausnahme besteht, wenn Benutzer Bedingungen explizit in einem „Ausnahme“-Bereich platzieren. In diesem Fall müssen alle Bedingungen innerhalb dieses Bereichs „false“ zurückgeben, damit die Regel weiter verarbeitet werden kann.

Beispielsweise könnte eine Erweiterung einen Bedinungstyp „Viewport enthält“ bereitstellen, bei dem der Benutzer einen CSS-Selektor angeben kann. Wenn diese Bedingung auf der Website des Kunden ausgewertet wird, kann die Erweiterung nach Elementen suchen, die mit der CSS-Auswahl übereinstimmen, und die Information zurückgeben, ob sich eines davon im Ansichtsfenster des Benutzers befindet.

In diesem Dokument wird beschrieben, wie Sie Bedingungstypen für eine Web-Erweiterung in Adobe Experience Platform definieren.

>[!NOTE]
>
>Wenn Sie eine Kantenerweiterung entwickeln, lesen Sie stattdessen das Handbuch zu [Bedingungstypen für Kantenerweiterungen](../edge/condition-types.md).
>
>In diesem Dokument wird davon ausgegangen, dass Sie mit Bibliotheksmodulen und deren Integration in Web-Erweiterungen vertraut sind. Wenn Sie eine Einführung benötigen, lesen Sie die Übersicht über die [Formatierung von Bibliotheksmodulen](./format.md), bevor Sie zu diesem Handbuch zurückkehren.

Bedingungstypen bestehen in der Regel aus Folgendem:

1. Eine [Ansicht](./views.md), die in der Datenerfassungs-Benutzeroberfläche angezeigt wird und es Benutzern ermöglicht, die Einstellungen für die Bedingung zu ändern.
2. Ein Bibliotheksmodul, das in der Tag-Laufzeitbibliothek ausgegeben wird, um die Einstellungen zu interpretieren und eine Bedingung auszuwerten.

Ein Bibliotheksmodul vom Bedingungstyp dient einem einzigen Ziel: auswerten, ob etwas wahr oder falsch ist. Was es auswertet, legen Sie fest.

Wenn Sie z. B. prüfen möchten, ob sich der Benutzer auf dem Host `example.com` befindet, könnte Ihr Modul wie folgt aussehen:

```js
module.exports = function(settings) {
  return document.location.hostname === 'example.com';
};
```

Betrachten Sie nun eine Situation, in der Sie dem Adobe Experience Platform-Benutzer das Konfigurieren des Host-Namens erlauben möchten. Sie können dem Benutzer erlauben, einen Hostnamen einzugeben, und dann den Hostnamen im Einstellungsobjekt speichern. Das Objekt könnte etwa so aussehen:

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
