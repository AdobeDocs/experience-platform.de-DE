---
title: Datenelementtypen für Web-Erweiterungen
description: Erfahren Sie, wie Sie ein Bibliotheksmodul vom Typ „data-element“ für eine Tag-Erweiterung in einer Web-Eigenschaft definieren.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 70%

---

# Datenelementtypen für Web-Erweiterungen

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere Terminologieänderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

In Datenerfassungs-Tags sind Datenelemente im Wesentlichen Aliase zu Datenteilen auf einer Seite. Diese Daten finden Sie in Abfragezeichenfolgenparametern, Cookies, DOM-Elementen oder anderen Speicherorten. Ein Datenelement kann durch Regeln referenziert werden und dient als Abstraktion für den Zugriff auf diese Daten.

Datenelementtypen werden von Erweiterungen bereitgestellt und ermöglichen es Benutzern, Datenelemente so zu konfigurieren, dass sie auf bestimmte Datenteile zugreifen können. Als Beispiel könnte eine Erweiterung einen Datenelementtyp „Lokales Speicherelement“ bereitstellen, bei dem der Benutzer einen lokalen Speicherelementnamen angeben kann. Wenn das Datenelement durch eine Regel referenziert wird, kann die Erweiterung den Elementwert der lokalen Datenspeicherung mithilfe des Elementnamens der lokalen Datenspeicherung suchen, den der Benutzer beim Konfigurieren des Datenelements angegeben hat.

In diesem Dokument wird beschrieben, wie Sie Datenelementtypen für eine Web-Erweiterung in Adobe Experience Platform definieren.

>[!IMPORTANT]
>
>Wenn Sie eine Kantenerweiterung entwickeln, lesen Sie stattdessen das Handbuch zu [Datenelementtypen für Kantenerweiterungen](../edge/data-element-types.md) .
>
>In diesem Dokument wird außerdem davon ausgegangen, dass Sie mit Bibliotheksmodulen und deren Integration in Web-Erweiterungen vertraut sind. Wenn Sie eine Einführung benötigen, lesen Sie die Übersicht über die [Formatierung von Bibliotheksmodulen](./format.md), bevor Sie zu diesem Handbuch zurückkehren.

Datenelementtypen bestehen in der Regel aus Folgendem:

1. Eine [Ansicht](./views.md), die in der Datenerfassungs-Benutzeroberfläche angezeigt wird und es Benutzern ermöglicht, die Einstellungen für das Datenelement zu ändern.
2. Ein Bibliotheksmodul wird in der Tag-Laufzeitbibliothek ausgegeben, um die Einstellungen zu interpretieren und Datenteile abzurufen.

Stellen Sie sich eine Situation vor, in der Sie den Benutzern erlauben möchten, ein Datenelement aus einem lokalen Speicherelement namens `productName` abzurufen. Ihr Modul könnte wie folgt aussehen:

```js
module.exports = function(settings) {
  return localStorage.getItem('productName');
}
```

Wenn Sie möchten, dass der Adobe Experience Platform-Benutzer den Elementnamen des lokalen Datenspeichers konfigurieren kann, können Sie den Benutzer einen Namen eingeben und diesen im `settings`-Objekt speichern lassen. Das Objekt könnte etwa so aussehen:

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
