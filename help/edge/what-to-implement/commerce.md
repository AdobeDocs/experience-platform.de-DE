---
title: Produkte
seo-title: Unterstützende Produkte mit dem Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie mit dem Experience Platform Web SDK Daten hinzufügen können, wenn Sie über Produkte oder einen Einkaufswagen verfügen
seo-description: Erfahren Sie, wie Sie mit dem Experience Platform Web SDK Daten hinzufügen können, wenn Sie über Produkte oder einen Einkaufswagen verfügen
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Produkte

>[!IMPORTANT]
>
>Das Adobe Experience Platform Web SDK befindet sich derzeit in der Betaphase und steht nicht allen Benutzern zur Verfügung. Dokumentation und Funktionalität können sich ändern.

Wenn Sie Produkte auf Ihrer Site haben, ist dies ein Standardsatz, den Sie möglicherweise senden möchten, um die meisten Funktionen von Adobe zu aktivieren. Obwohl dies eine Empfehlung ist, bietet sie einen sehr starken Datensatz vom Beginn aus.

Dieses Dokument verwendet das [ExperienceEvent Commerce-Details](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) -Mixin. Die `commerce` Mischung wird in zwei Teile aufgeteilt: das `commerce` Objekt und das `productListItems` Array. Mit dem `commerce` Objekt können Sie angeben, welche Aktionen mit dem `productListItems` Array ausgeführt werden.

>[!Tip]
>Wenn Sie mit Adobe Analytics vertraut sind, `commerce` ist die Variable am engsten mit der `events` Variablen verwandt. Die Variable `productListItems` ist enger mit der `products` Variablen verwandt.

## Maßnahmen im Zusammenhang mit Produkten

Unten finden Sie eine Liste der `measures` verfügbaren `commerce` Objekte.

>[!Tip]
>Eine Maßnahme umfasst zwei Bereiche: `id` und `value`. In den meisten Fällen verwenden Sie nur das `value` Feld (z. B. `'value':1`). Mit dem `id` Feld können Sie einen eindeutigen Bezeichner festlegen, mit dem Sie verfolgen können, wann die Maßnahme gesendet wurde. Siehe XDM-Dokumentation für [Measure](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/measure.schema.md).

| **Maßnahme** | **Empfehlung** | **Beschreibung** |
|---|---|---|
| [cartAbandons](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcartabandons) | Optional | Ein Warenkorb kann vom Benutzer nicht mehr aufgerufen oder gekauft werden. |
| [Checkouts](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcheckouts) | Dringend empfohlen | Ein Benutzer sucht nicht mehr nach Produkten, sondern kauft gerade ein Produkt. |
| [productListAdds](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistadds) | Dringend empfohlen | Ein Produkt wird einer Liste hinzugefügt. Stellen Sie sicher, dass Sie das Produkt in der `productListItems` gleichen Zeit einstellen. |
| [productListOpen](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistopens) | Optional | Es wird eine neue Produkt-Liste erstellt. (Beispielsweise wird ein neuer Warenkorb erstellt.) |
| [productListRemovals](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistremovals) | Dringend empfohlen | Ein Produkt wird aus einer Liste entfernt. |
| [productListReopen](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistreopens) | Optional | Eine Liste wird vom Benutzer reaktiviert. Das passiert oft bei Remarketing-Kampagnen. |
| [productListViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistviews) | Dringend empfohlen | Eine Liste von Produkten wird angezeigt. |
| [productViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductviews) | Dringend empfohlen | Eine Ansicht eines Produkts ist aufgetreten. Stellen Sie sicher, dass Sie das angezeigte Produkt im `productListItems`Menü einstellen. |
| [Einkäufe](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmpurchases) | Dringend empfohlen | Eine Bestellung wird akzeptiert. Muss eine Produkt-Liste haben. |
| [saveForLaters](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmsaveforlaters) | Optional | Ein Produkt wird für die zukünftige Verwendung gespeichert. |

Hier ist ein Beispiel, wie Sie diese `Measures` im SDK festlegen würden.

```javascript
alloy("event", {
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    }
  }
});
```

Das commerce-Objekt verfügt auch über ein spezielles Feld zum Sammeln von Bestelldetails namens `order`.

| **Bestellung** | **Option** | **Empfehlung** | **Beschreibung** |
|---|---|---|---|
| [„currencyCode“](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) |  |  | Die [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) Währung für die Bestellsumme. |
| [Payment[PaymentItems]](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpayments) |  |  | Die Liste der Zahlungen auf eine Bestellung. Ein [PaymentItem](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#payment-item-schema) beinhaltet Folgendes. |
|  | [„currencyCode“](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) | Optional | Die [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) Währung für diese Zahlungsmethode. |
|  | [paymentAmount](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymentamount) | Dringend empfohlen | Der Wert der Zahlung im angegebenen Währungscode. |
|  | [payType](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype) | Dringend empfohlen | Die Art der Zahlung (z. B. `credit_card`, `gift_card`, `paypal`). Weitere Informationen finden Sie in der Liste der [bekannten Werte](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype-known-values) . |
|  | [transactionID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmtransactionid) | Optional | Eine eindeutige ID für diesen Zahlungsvorgang. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpricetotal) |  | Dringend empfohlen | Die Summe für diese Bestellung, nachdem alle Rabatte und Steuern angewendet wurden. |
| [purchaseID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseid) |  | Hoch empfohlen | Die eindeutige Kennung, die der Verkäufer für diesen Kauf zugewiesen hat. |
| [purchaseOrderNumber](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseordernumber) |  | Optional | Eine eindeutige ID, die vom Käufer für diesen Kauf zugewiesen wird. |

Hier ein Beispiel für einen typischen Kauf im SDK.

```javascript
alloy("event",{
  "xdm":{
    "commerce":{
      "order":{
        "purchaseID":"123456789",
        "currenceCode":"USD",
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
        "qauntity":1
      }
    ]
  }
});
```

## Listen von Erzeugnissen

Die Liste des Produkts gibt an, welche Produkte mit der entsprechenden Aktion in Verbindung stehen. Es handelt sich um eine Liste von [productListItems](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md). Jedes Produkt verfügt über eine Reihe optionaler Felder.

| **Feld** | **Empfehlung** | **Beschreibung** |
|---|---|---|
| [„currencyCode“](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmcurrencycode) | Optional | Die [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) Währung für das Produkt. Dies ist nur dann nützlich, wenn Sie Produkte mit unterschiedlichen Währungscodes haben können und wenn es anwendbar ist. Wenn es beispielsweise einen Kauf gibt oder der Warenkorb hinzugefügt wird. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmpricetotal) | Dringend empfohlen | Sollte nur eingestellt werden, wenn zutreffend. So ist es zum Beispiel nicht möglich, eine Einstellung vorzunehmen, `productView` weil unterschiedliche Produktvarianten unterschiedliche Preise haben können, jedoch auf einem `productListAdds`. |
| [Produkt](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproduct) | Dringend empfohlen | Die XDM-ID für das Produkt. |
| [productAddMethod](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproductaddmethod) | Dringend empfohlen | Die Methode, mit der der Besucher der Liste ein Produktelement hinzufügen konnte. Wird mit `productListAdds` Maßnahmen eingestellt und sollte nur verwendet werden, wenn ein Produkt der Liste hinzugefügt wird. Beispiele sind `add to cart button`, `quick add`und `upsell`. |
| [productName](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmname) | Dringend empfohlen | Dies wird auf den Anzeigenamen oder den für Menschen lesbaren Namen des Produkts festgelegt. |
| [quantity](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmquantity) | Dringend empfohlen | Die Anzahl der Einheiten, die der Kunde für das Produkt angegeben hat. Sollte auf `productListAdds`, `productListRemoves`, `purchases`, `saveForLaters`usw. eingestellt werden. |
| [SKU](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md) | Dringend empfohlen | Aufbewahrungseinheit im Speicher. Es ist der eindeutige Bezeichner für das Produkt. |

## Beispiele

`productView`-Ereignis 

```javascript
alloy("event",{
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

`productView`-Ereignis 

```javascript
alloy("event",{
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

`checkout`-Ereignis 

```javascript
alloy("event",{
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

`purchase`-Ereignis 

```javascript
alloy("event",{
  "xdm":{
    "commerce":{
      "order":{
        "purchaseID":"123456789",
        "currenceCode":"USD",
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
        "qauntity":1
      }
    ]
  }
});
```
