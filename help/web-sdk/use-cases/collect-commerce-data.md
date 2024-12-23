---
title: Erfassen von Commerce-, Produkt- und Bestellinformationen mit dem Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie mit dem Adobe Experience Platform Web SDK Daten zu Produkten oder einem Warenkorb hinzufügen.
exl-id: 3c79e776-89ef-494b-a2ea-3c23efce09ae
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 37%

---

# Erfassen von Commerce-, Produkt- und Bestellinformationen

Wenn Ihr Unternehmen Produkte oder Dienstleistungen verkauft, können Sie diese Seite als Leitfaden zur Verfolgung dieser Produkte und Dienste verwenden.

Auf dieser Seite wird die Feldergruppe XDM [Commerce-Schema](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md) verwendet.

Diese Feldergruppe besteht aus zwei Hauptteilen:

* Das `commerce` -Objekt. Mit diesem Objekt können Sie angeben, welche Aktionen auf das `productListItems` -Array angewendet werden.
* Das `productListItems` -Array.

>[!TIP]
>
>Wenn Sie mit Adobe Analytics vertraut sind, enthält das `commerce` -Objekt Daten, die den Commerce-Ereignissen in der `events` -Variablen ähneln. Das Objekt-Array `productListItems` enthält Daten, die der Variablen `products` ähneln.

## Das Objekt `commerce` {#commerce-object}

In diesem Abschnitt werden die im Objekt `commerce` verfügbaren Felder beschrieben.

>[!TIP]
>
>Eine Maßnahme umfasst zwei Bereiche: `id` und `value`. Meistens verwenden Sie nur das Feld `value` (z. B. `'value':1`). Im Feld `id` können Sie eine eindeutige Kennung für das Tracking zum Zeitpunkt des Versands der Kennzahl festlegen. Weitere Informationen finden Sie in der XDM-Dokumentation für [Maßnahme](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/measure.schema.md) .

| Maßnahme | Empfehlung | Beschreibung |
|---|---|---|
| [`cartAbandons`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmcartabandons) | Optional | Ein Warenkorb kann vom Nutzer nicht mehr aufgerufen oder gekauft werden. |
| [`checkouts`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmcheckouts) | Dringend empfohlen | Ein Nutzer sucht nicht mehr nach Produkten, sondern kauft gerade ein Produkt. |
| [`productListAdds`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistadds) | Dringend empfohlen | Ein Produkt wird einer Liste hinzugefügt. Stellen Sie das Produkt gleichzeitig in `productListItems` ein. |
| [`productListOpens`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistopens) | Optional | Eine neue Produktliste wird erstellt. Beispielsweise wird ein neuer Warenkorb erstellt. |
| [`productListRemovals`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistremovals) | Dringend empfohlen | Ein Produkt wird aus einer Produktliste entfernt. |
| [`productListReopens`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistreopens) | Optional | Eine Produktliste wird vom Nutzer reaktiviert. Diese Aktion tritt oft bei Remarketing-Kampagnen auf. |
| [`productListViews`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistviews) | Dringend empfohlen | Eine Liste von Produkten wird angezeigt. |
| [`productViews`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductviews) | Dringend empfohlen | Eine Ansicht eines Produkts ist aufgetreten. Stellen Sie das angesehene Produkt in `productListItems` ein. |
| [`purchases`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmpurchases) | Dringend empfohlen | Eine Bestellung wird angenommen. Muss eine Produktliste haben. |
| [`saveForLaters`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmsaveforlaters) | Optional | Ein Produkt wird für die zukünftige Verwendung gespeichert. |

{style="table-layout:auto"}

### `Commerce` Objektbeispiele

Erweitern Sie den folgenden Abschnitt, um ein Beispiel für einen Web SDK-Befehl mit einem Feld aus dem `commerce` -Objekt anzuzeigen.

+++`productViews`

Ein einfacher Web SDK `sendEvent` -Aufruf, durch den das `productViews` -Feld auf `1` gesetzt wird:

```javascript
alloy("sendEvent", {
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    }
  }
});
```

+++

## Das Objekt `order` {#order-object}

Das Objekt `commerce` enthält ein dediziertes Objekt zum Erfassen der Bestelldetails. Dies wird als `order` -Objekt bezeichnet.

In diesem Abschnitt werden alle Felder beschrieben, die vom Objekt `order` unterstützt werden.

| Feld | Option | Empfehlung | Beschreibung |
|---|---|---|---|
| [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmcurrencycode) |  |  | Die [ISO 4217](https://de.wikipedia.org/wiki/ISO_4217)-Währung für die Bestellsumme. |
| [`payments[]`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpayments) |  |  | Die Liste der Zahlungen für eine Bestellung. Ein [paymentItem](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md) beinhaltet Folgendes. |
|  | [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmcurrencycode) | Optional | Die [ISO 4217](https://de.wikipedia.org/wiki/ISO_4217)-Währung für diese Zahlungsmethode. |
|  | [`paymentAmount`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymentamount) | Dringend empfohlen | Der Wert der Zahlung im angegebenen Währungs-Code. |
|  | [`paymentType`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymenttype) | Dringend empfohlen | Die Art der Zahlung (z. B. `credit_card`, `gift_card`, `paypal`). Weitere Informationen finden Sie in der Liste der [bekannten Werte](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymenttype-known-values). |
|  | [`transactionID`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmtransactionid) | Optional | Eine eindeutige Kennung für diesen Zahlungsvorgang. |
| [`priceTotal`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpricetotal) |  | Dringend empfohlen | Die Summe für diese Bestellung, nachdem alle Rabatte und Steuern berücksichtigt wurden. |
| [`purchaseID`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpurchaseid) |  | Dringend empfohlen | Die eindeutige Kennung, die der Verkäufer diesem Kauf zugewiesen hat. |
| [`purchaseOrderNumber`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpurchaseordernumber) |  | Optional | Eine eindeutige Kennung, die der Käufer diesem Kauf zugewiesen hat. |

### Objektbeispiele sortieren

Erweitern Sie den folgenden Abschnitt, um ein Beispiel für einen Web SDK-Befehl mit dem Objekt `commerce` anzuzeigen.

+++Beispiel für `Order`-Objekt

Ein Web SDK `sendEvent` -Aufruf, mit dem das `order` -Objekt festgelegt wird, das für mehrere Produkte im `productListItems` -Array gilt:

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "order":{
        "purchaseID":"123456789",
        "currencyCode":"USD",
        "priceTotal":39.98,
        "payments":[
          {
            "transactionID":"amx12345",
            "paymentAmount":39.98,
            "paymentType":"credit_card",
            "currencyCode":"USD"
          }
        ]
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "priceTotal":29.99,
        "quantity":1
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "priceTotal":9.99,
        "quantity":1
      }
    ]
  }
});
```

+++

## Das Produktlistenobjekt {#product-list-object}

Die Produktliste gibt an, welche Produkte mit der entsprechenden Aktion in Verbindung stehen. Es handelt sich um eine Liste von [productListItems](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md). Jedes Produkt verfügt über mehrere optionale Felder.

| Feld | Empfehlung | Beschreibung |
|---|---|---|
| [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmcurrencycode) | Optional | Die [ISO 4217](https://de.wikipedia.org/wiki/ISO_4217) -Währung für das Produkt. Dieses Feld gilt normalerweise nur, wenn die Produktliste mehrere Produkte mit unterschiedlichen Währungs-Codes enthält. |
| [`priceTotal`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmpricetotal) | Dringend empfohlen | Legen Sie dieses Feld nur fest, wenn zutreffend. So ist es beispielsweise u. U. nicht möglich, ein `productView` -Ereignis festzulegen, da unterschiedliche Varianten des Produkts unterschiedliche Preise haben können, jedoch nicht für ein `productListAdds` -Ereignis. |
| [`product`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmproduct) | Dringend empfohlen | Die XDM-ID für das Produkt. |
| [`productAddMethod`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmproductaddmethod) | Dringend empfohlen | Die Methode, mit der der Besucher der Liste ein Produktelement hinzufügen konnte. Wird mit `productListAdds` -Messungen eingestellt und wird nur verwendet, wenn ein Produkt zur Liste hinzugefügt wird. Beispiele sind `add to cart button`, `quick add` und `upsell`. |
| [`productName`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmname) | Dringend empfohlen | Der Anzeigename oder der für Menschen lesbare Name des Produkts. |
| [`quantity`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmquantity) | Dringend empfohlen | Die Anzahl der Einheiten, die der Kunde vom Produkt benötigt. Sollte auf `productListAdds`, `productListRemoves`, `purchases`, `saveForLaters` usw. eingestellt werden. |
| [`SKU`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmsku) | Dringend empfohlen | Bestandseinheit. Dies ist die eindeutige Kennung für das Produkt. |

### Beispiele für Produktlisten

Erweitern Sie die folgenden Abschnitte, um Beispiele für Web SDK-Befehle mit dem Objekt `productListItems` anzuzeigen.

+++Beispiel für `productListItems`

Ein Web SDK `sendEvent` -Aufruf, mit dem der Wert `productViews` für mehrere Produkte im Array `productListItems` festgelegt wird:

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
      }
    ]
  }
});
```

+++

+++`productListAdds` Beispiel

Ein Web SDK `sendEvent` -Aufruf, mit dem das `productListAdds` -Ereignis für mehrere Produkte im `productListItems` -Array festgelegt wird:

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "productListAdds":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "quantity":1,
        "priceTotal":29.99,
        "productAddMethod":"Add to Cart Button"
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "quantity":1,
        "priceTotal":9.99,
        "productAddMethod":"Add-on"
      }
    ]
  }
});
```

+++

+++Beispiel für `checkouts`

Ein Web SDK `sendEvent` -Aufruf, mit dem das `checkouts` -Ereignis für mehrere Produkte im `productListItems` -Array festgelegt wird:

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "checkouts":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"The Big Floppy Hat",
        "quantity":1,
        "priceTotal":29.99
      },
      {
        "SKU":"HT104",
        "name":"The Small Floppy Hat",
        "quantity":1,
        "priceTotal":9.99
      }
    ]
  }
});
```

+++
