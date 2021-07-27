---
title: Datenelementtypen für Edge-Erweiterungen
description: Erfahren Sie, wie Sie ein Bibliotheksmodul vom Typ "Datenelement"für eine Tag-Erweiterung in einer Edge-Eigenschaft definieren.
source-git-commit: 99780f64c8f09acea06e47ebf5cabc762e05cab2
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 28%

---

# Datenelementtypen in Edge-Erweiterungen

>[!NOTE]
>
>Adobe Experience Platform Launch wird als eine Suite von Datenerfassungstechnologien in Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

In -Tags sind Datenelemente Aliase für Datenelemente auf einer Web- oder mobilen Seite, unabhängig davon, wo sich diese Daten innerhalb des vom Server empfangenen Ereignisses befinden. Ein Datenelement kann durch Regeln referenziert werden und dient als Abstraktion für den Zugriff auf diese Daten. Wenn sich der Speicherort der Daten in Zukunft ändert (z. B. beim Ändern des Ereignisschlüssels, der den Wert enthält), kann ein einzelnes Datenelement neu konfiguriert werden, während alle Regeln, die auf dieses Datenelement verweisen, unverändert bleiben können.

Datenelementtypen werden von Erweiterungen bereitgestellt und der Erweiterungsautor bestimmt, wie diese Datenelemente abgerufen werden. Sie können beispielsweise einen Datenelementtyp verwenden, um Adobe Experience Platform-Benutzern zu ermöglichen, ein Datenelement aus der XDM-Ebene oder ihrer benutzerdefinierten Datenschicht abzurufen.

In diesem Dokument wird beschrieben, wie Sie Datenelementtypen für eine Edge-Erweiterung in Adobe Experience Platform definieren.

>[!IMPORTANT]
>
>Wenn Sie eine Web-Erweiterung entwickeln, lesen Sie stattdessen das Handbuch zu [Datenelementtypen für Web-Erweiterungen](../web/data-element-types.md) .
>
>In diesem Dokument wird außerdem davon ausgegangen, dass Sie mit Bibliotheksmodulen und deren Integration in Edge-Erweiterungen vertraut sind. Wenn Sie eine Einführung benötigen, lesen Sie die Übersicht über die [Formatierung von Bibliotheksmodulen](./format.md), bevor Sie zu diesem Handbuch zurückkehren.

Datenelementtypen bestehen in der Regel aus Folgendem:

1. Eine Ansicht, die in der Datenerfassungs-Benutzeroberfläche angezeigt wird und es Benutzern ermöglicht, die Einstellungen für das Datenelement zu ändern.
2. Ein Bibliotheksmodul wird in der Tag-Laufzeitbibliothek ausgegeben, um die Einstellungen zu interpretieren und Datenteile abzurufen.

Wenn Sie Benutzern erlauben möchten, ein Datenelement aus der benutzerdefinierten Datenschicht abzurufen, könnte Ihr Modul wie im folgenden Beispiel aussehen.

```js
module.exports = (context) => {
  const productName = context.arc.event.data.productName;
  return productName;
};
```

Wenn Sie möchten, dass der Adobe Experience Platform-Benutzer die für die Datenschicht zurückgegebenen Daten konfigurierbar macht, können Sie dem Benutzer die Eingabe eines Schlüsselnamens gestatten und diesen Namen dann im `settings`-Objekt speichern. Das Objekt könnte etwa so aussehen.

```js
{
  keyName: "campaignId"
}
```

Um mit dem benutzerdefinierten Namen des lokalen Datenspeichers arbeiten zu können, muss Ihr Modul wie folgt geändert werden:

```js
module.exports = (context) => {
  const data = context.arc.event.data;
  return data[keyName];
};
```

## Kontext des Bibliotheksmoduls

Alle Datenelementmodule haben Zugriff auf eine `context`-Variable, die beim Aufruf des Moduls bereitgestellt wird. Weitere Informationen finden Sie [hier](./context.md).
