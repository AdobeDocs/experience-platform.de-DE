---
title: Datenelementtypen für Edge-Erweiterungen
description: Lernen Sie, wie Sie ein Bibliotheksmodul vom Typ „data-element-type“ für eine Tag-Erweiterung in einer Edge-Eigenschaft definieren.
exl-id: ddbc3912-1c25-4d21-bde8-e40e583b4278
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 94%

---

# Datenelementtypen für Edge-Erweiterungen

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

In Tags handelt es sich bei Datenelementen im Wesentlichen um Aliase zu Datensegmenten auf einer Web- oder Mobile-Seite, unabhängig davon, wo sich diese Daten im vom Server empfangenen Ereignis befinden. Ein Datenelement kann durch Regeln referenziert werden und dient als Abstraktion für den Zugriff auf diese Daten. Wenn sich der Speicherort der Daten in Zukunft ändert (beispielsweise weil der Ereignisschlüssel, der den Wert enthält, geändert wird), kann ein einzelnes Datenelement neu konfiguriert werden, wobei alle Regeln, die auf dieses Datenelement verweisen, unverändert bleiben können.

Datenelementtypen werden von Erweiterungen bereitgestellt und der Erweiterungsautor bestimmt, wie diese Datenelemente abgerufen werden. Sie können beispielsweise einen Datenelementtyp verwenden, damit Benutzer von Adobe Experience Platform Daten aus der XDM-Ebene oder ihrer benutzerdefinierten Datenschicht abrufen können.

In diesem Dokument wird beschrieben, wie Sie Datenelementtypen für eine Edge-Erweiterung in Adobe Experience Platform definieren.

>[!IMPORTANT]
>
>Wenn Sie eine Web-Erweiterung entwickeln, lesen Sie stattdessen das Handbuch zu [Datenelementtypen für Web-Erweiterungen](../web/data-element-types.md).
>
>In diesem Dokument wird auch davon ausgegangen, dass Sie mit Bibliotheksmodulen und deren Integration in Edge-Erweiterungen vertraut sind. Wenn Sie eine Einführung benötigen, lesen Sie die Übersicht über die [Formatierung von Bibliotheksmodulen](./format.md), bevor Sie zu diesem Handbuch zurückkehren.

Datenelementtypen bestehen in der Regel aus Folgendem:

1. Eine Ansicht, die in der Experience Platform-Benutzeroberfläche und der Datenerfassungs-Benutzeroberfläche angezeigt wird und es Benutzern ermöglicht, die Einstellungen für das Datenelement zu ändern.
2. Ein Bibliotheksmodul, das in der Tag-Laufzeitbibliothek ausgegeben wird, um die Einstellungen zu interpretieren und Datensegmente abzurufen.

Wenn Sie Benutzern erlauben möchten, ein Datenelement aus der benutzerdefinierten Datenschicht abzurufen, könnte Ihr Modul wie im folgenden Beispiel aussehen.

```js
module.exports = (context) => {
  const productName = context.arc.event.data.productName;
  return productName;
};
```

Wenn Sie möchten, dass der Adobe Experience Platform-Benutzer die von der Datenschicht zurückgegebenen Daten konfigurieren kann, können Sie dem Benutzer erlauben, einen Schlüsselnamen einzugeben und diesen im `settings`-Objekt zu speichern. Das Objekt könnte etwa so aussehen.

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
