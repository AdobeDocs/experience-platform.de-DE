---
title: Datenelementtypen für Edge-Erweiterungen
description: Erfahren Sie, wie Sie ein Bibliotheksmodul vom Typ "Datenelement"für eine Tag-Erweiterung in einer Edge-Eigenschaft definieren.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 49%

---

# Datenelementtypen in Randerweiterungen

>[!NOTE]
>
>Adobe Experience Platform Launch wird als eine Suite von Datenerfassungstechnologien in Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Ein Bibliotheksmodul vom Datenelementtyp ruft ein Datenelement ab. Der Modulautor bestimmt, wie dieses Datenelement abgerufen wird. Sie können beispielsweise einen Datenelementtyp verwenden, um Adobe Experience Platform-Benutzern zu ermöglichen, ein Datenelement aus der XDM-Ebene oder ihrer benutzerdefinierten Datenschicht abzurufen.

>[!IMPORTANT]
>
>In diesem Dokument werden Datenelementtypen für Randerweiterungen behandelt. Wenn Sie eine Web-Erweiterung entwickeln, lesen Sie das Handbuch zu [Datenelementtypen für Web-Erweiterungen](../web/data-element-types.md).
>
>In diesem Dokument wird außerdem davon ausgegangen, dass Sie mit Bibliotheksmodulen und deren Integration in Tag-Erweiterungen vertraut sind. Wenn Sie eine Einführung benötigen, lesen Sie die Übersicht über die [Formatierung von Bibliotheksmodulen](./format.md), bevor Sie zu diesem Handbuch zurückkehren.

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
