---
title: Datenelementtypen für Web-Erweiterungen
description: Erfahren Sie, wie Sie ein Bibliotheksmodul vom Typ "Datenelement"für eine Tag-Erweiterung in einer Web-Eigenschaft definieren.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 70%

---

# Datenelementtypen für Edge-Erweiterungen

>[!NOTE]
>
>Adobe Experience Platform Launch wird als eine Suite von Datenerfassungstechnologien in Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Ein Datenelementtyp-Bibliotheksmodul dient dem Abrufen von Daten. Die Methode für diesen Abruf kann angepasst werden. Verschiedene Datenelementtypen ermöglichen es Adobe Experience Platform-Benutzern, Daten aus dem lokalen Speicher, einem Cookie oder einem DOM-Element abzurufen.

>[!IMPORTANT]
>
>Dieses Dokument enthält Informationen zu Datenelementtypen für Web-Erweiterungen. Wenn Sie eine Kantenerweiterung entwickeln, lesen Sie stattdessen das Handbuch zu [Datenelementtypen für Kantenerweiterungen](../edge/data-element-types.md).
>
>In diesem Dokument wird außerdem davon ausgegangen, dass Sie mit Bibliotheksmodulen und deren Integration in Tag-Erweiterungen vertraut sind. Wenn Sie eine Einführung benötigen, lesen Sie die Übersicht über die [Formatierung von Bibliotheksmodulen](./format.md), bevor Sie zu diesem Handbuch zurückkehren.

Stellen Sie sich eine Situation vor, in der Sie den Benutzern erlauben möchten, ein Datenelement aus einem lokalen Speicherelement namens `productName` abzurufen. Ihr Modul könnte wie folgt aussehen:

```js
module.exports = function(settings) {
  return localStorage.getItem('productName');
}
```

Wenn Sie möchten, dass der Adobe Experience Platform-Benutzer den Elementnamen des lokalen Datenspeichers konfigurieren kann, können Sie dem Benutzer erlauben, einen Namen einzugeben und diesen dann im `settings` -Objekt zu speichern. Das Objekt könnte etwa so aussehen:

```js
{
  itemName: "campaignId"
}
```

Um mit dem benutzerdefinierten Namen des lokalen Datenspeichers arbeiten zu können, muss Ihr Modul wie folgt geändert werden:

```js
module.exports = function(settings) {
  return localStorage.getItem(settings.itemName);
}
```

## Unterstützung von Standardwerten

Beachten Sie, dass Benutzer die Möglichkeit haben, einen Standardwert für ein Datenelement zu konfigurieren. Wenn Ihr Datenelement-Bibliotheksmodul den Wert `undefined` oder `null` zurückgibt, wird dieser automatisch durch den Standardwert ersetzt, den der Benutzer für das Datenelement konfiguriert hat.

## Kontextbezogene Ereignisdaten

Wenn das Datenelement als Ergebnis einer ausgelösten Regel abgerufen wird (z. B. wenn Datenelemente in den Bedingungen und Aktionen der Regel verwendet werden), wird ein zweites Argument an Ihr Modul übergeben, das Kontextinformationen zu dem Ereignis enthält, das die Regel ausgelöst hat. Das kann in bestimmten Fällen von Vorteil sein. Auf dieses Argument wird wie folgt zugegriffen:

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
