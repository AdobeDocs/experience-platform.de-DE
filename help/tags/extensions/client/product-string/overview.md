---
title: Adobe Analytics Product String-Erweiterung – Übersicht
description: Machen Sie sich mit der Tag-Erweiterung „Adobe Analytics Product String“ in Adobe Experience Platform vertraut.
exl-id: a49feb4e-f166-41d2-9f85-639f6ff8bb8f
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 100%

---

# Adobe Analytics Product String-Erweiterung – Übersicht

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

Die Variable `products` dient zur Verfolgung der Interaktionen von Besuchern mit Produkten auf einer Site. So kann zum Beispiel in der Variablen `products` verfolgt werden, wie oft ein Produkt angezeigt, in den Warenkorb gelegt, ausgecheckt und gekauft wird. Außerdem können Sie mit der Variablen auch die relative Effizienz von Merchandising-Kategorien auf Ihrer Site verfolgen.

Die Variable `products` sollte immer in Verbindung mit einem Erfolgsereignis festgelegt werden.

Die [!DNL Adobe Analytics Product String Builder]-Erweiterung legt die Variable `products` automatisch für Sie fest, indem sie Ihre Datenschicht durchläuft, alle erforderlichen produktbezogenen Daten erfasst und in der unten gezeigten richtigen Syntax formatiert. Sie müssen kein benutzerdefiniertes JavaScript mehr schreiben und verwalten, um diese komplexen Aktionen durchzuführen.

## Syntax der Variable „products“

```bash
Category;Product;Quantity;Price;eventN=X|eventN2=X2;eVarN=merch_category|eVarN2=merch_category2
```

Die vollständige Dokumentation finden Sie unter [Produkte](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=de).

## Anweisungen zur Erweiterung

### Aktionskonfiguration

Fügen Sie Ihrer Regel die Aktion „Adobe Analytics Product String - Set s.products“ hinzu.

![Aktionskonfiguration](./images/screenshot-action-config.png)

### Festlegen der Standard-Produktdaten

Definieren Sie anschließend die Datenschicht-Variablen. Nachdem Sie die Aktion wie im vorherigen Schritt beschrieben konfiguriert haben, wird der folgende Bildschirm angezeigt:

![Standardfelder](./images/screenshot-standard-fields.png)

Geben Sie für jeden Datenpunkt, den Sie in die Produktzeichenfolge aufnehmen möchten, den Pfad zur entsprechenden Datenschichtvariablen ein.

Angenommen, Ihre Datenschicht ist wie folgt strukturiert:

```json
digitalData = {
  "transaction": {
    "item": [{
      "productInfo": {
        "productName": "My Product"
      }
    }]
  }
};
```

Geben Sie den folgenden Pfad in das Feld „Variable for product ID/name“ ein, um die Variable `productName` zu erfassen:

```json
digitalData.transaction.item.productInfo.productName
```

>[!NOTE]
>
>Wenn Sie ein Datenelement zum Ausfüllen des Felds verwenden, sollte es mithilfe des Datenelementtyps „Constant“ oder „Custom Code“ konfiguriert werden und den obigen Pfad als Zeichenfolgenliteral zurückgeben.

### Preistyp

Der Parameter `price` in der [!DNL Adobe Analytics]-Produktzeichenfolge muss dem Gesamtpreis aller gekauften Artikel und nicht dem Stückpreis eines Produkts entsprechen. Wenn Sie das Feld „Preis“ in der Erweiterungsaktion aktivieren, müssen Sie angeben, ob Ihre Datenschicht den Gesamtpreis oder den Stückpreis anzeigt. Bei Verwendung des Stückpreises multipliziert die [!DNL Adobe Analytics Product String]-Erweiterung automatisch den Stückpreis mit der Menge, um den Gesamtpreis zu erhalten und die Produktzeichenfolge korrekt festzulegen.

![Preistyp](./images/screenshot-price-type.png)

### Benutzerspezifische Ereignisse und Merchandising-eVars

![Ereignisse und eVars](./images/screenshot-events-evars.png)

Wenn Sie bei Ihrer Implementierung benutzerdefinierte Ereignisse oder Merchandising-eVars verwenden, führen Sie die folgenden Schritte aus:

1. Klicken Sie auf die entsprechende Schaltfläche **[!UICONTROL Hinzufügen]**.
1. Wählen Sie das Ereignis oder die eVar aus der Dropdown-Liste aus, das bzw. die Sie definieren müssen.
1. Geben Sie den Pfad zur entsprechenden Datenschichtvariablen mit der oben beschriebenen Syntax ein.

### Reihenfogle der Aktionen

Diese Aktion muss von der Aktion „Adobe Analytics - Set Variables“ begleitet werden, mit der die entsprechenden Erfolgsereignisse festgelegt werden, sowie von der Aktion „Adobe Analytics - Send Beacon“. Die richtige Reihenfolge der Aktionen wird nachfolgend dargestellt.

![Standardfelder](./images/screenshot-price-type.png)

### Anforderungen

* Eine objektbasierte [Datenschicht](https://theblog.adobe.com/data-layers-buzzword-best-practice/) mit Variablen für alle produktbezogenen Daten (wie Produkt-ID, Menge, Preis). Diese Erweiterung funktioniert nicht mit Array-basierten Datenschichten.
* Die [Adobe Analytics](../analytics/overview.md)-Erweiterung muss installiert sein.
