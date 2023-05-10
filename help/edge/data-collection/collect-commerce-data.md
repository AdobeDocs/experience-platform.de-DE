---
title: Erfassen von Commerce- und Produktinformationen mit dem Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie mit dem Adobe Experience Platform Web SDK Daten zu Produkten oder einem Warenkorb hinzufügen.
keywords: Produkte;Commerce;Maßnahmen;Maßnahme;Bestellung;cartAbandons;Checkouts;productListAdds;productListOpens;productListRemovals;productListReopens;productListViews;productViews;Einkäufe;saveForLaters;currencyCode;Zahlungen;paymentAmount;paymentType;transactionID;priceTotal;purchaseID;purchaseOrderNumber;
exl-id: 3c79e776-89ef-494b-a2ea-3c23efce09ae
source-git-commit: 51a18ca3a9d0817eafeecea328900eb2f4d1d9a4
workflow-type: tm+mt
source-wordcount: '1326'
ht-degree: 91%

---

# Erfassen von Commerce- und Produktinformationen

Wenn Sie Produkte auf Ihrer Site haben, ist dies ein Standardsatz, den Sie möglicherweise senden möchten, um die meisten Funktionen von Adobe zu aktivieren. Dies ist nur ein Vorschlag, Sie verfügen damit jedoch von Anfang an über einen sehr starken Datensatz.

Dieses Dokument verwendet die [ExperienceEvent Commerce-Details](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) Schemafeldgruppe. Die `commerce` Die Feldergruppe besteht aus zwei Teilen: die `commerce` -Objekt und `productListItems` Array. Mit dem `commerce`-Objekt können Sie angeben, welche Aktionen auf das `productListItems`-Array angewendet werden.

>[!TIP]
>
>Wenn Sie mit Adobe Analytics vertraut sind, ist `commerce` am ehesten mit der `events`-Variablen vergleichbar. `productListItems` ist eher mit der `products`-Variablen vergleichbar.

## Aktionen im Zusammenhang mit Produkten

Nachstehend finden Sie eine Liste der Maßnahmen (`measures`), die im `commerce`-Objekt verfügbar sind.

>[!TIP]
>
>Eine Maßnahme umfasst zwei Bereiche: `id` und `value`. In den meisten Fällen verwenden Sie nur das `value`-Feld (z. B. `'value':1`). Mit dem `id`-Feld können Sie eine eindeutige Kennung festlegen, mit der Sie verfolgen können, wann die Maßnahme gesendet wurde. Siehe XDM-Dokumentation für [Maßnahme](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/measure.schema.md).

| **Maßnahme** | **Empfehlung** | **Beschreibung** |
|---|---|---|
| [cartAbandons](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcartabandons) | Optional | Ein Warenkorb kann vom Nutzer nicht mehr aufgerufen oder gekauft werden. |
| [checkouts](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmcheckouts) | Dringend empfohlen | Ein Nutzer sucht nicht mehr nach Produkten, sondern kauft gerade ein Produkt. |
| [productListAdds](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistadds) | Dringend empfohlen | Ein Produkt wird einer Liste hinzugefügt. Stellen Sie das Produkt gleichzeitig in `productListItems` ein. |
| [productListOpens](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistopens) | Optional | Eine neue Produktliste wird erstellt. (Beispielsweise wird ein neuer Warenkorb erstellt.) |
| [productListRemovals](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistremovals) | Dringend empfohlen | Ein Produkt wird aus einer Produktliste entfernt. |
| [productListReopens](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistreopens) | Optional | Eine Produktliste wird vom Nutzer reaktiviert. Dies geschieht häufig bei Remarketing-Kampagnen. |
| [productListViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductlistviews) | Dringend empfohlen | Eine Liste von Produkten wird angezeigt. |
| [productViews](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmproductviews) | Dringend empfohlen | Ein Produkt wurde angesehen. Stellen Sie das angesehene Produkt in `productListItems` ein. |
| [purchases](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmpurchases) | Dringend empfohlen | Eine Bestellung wird angenommen. Muss eine Produktliste haben. |
| [saveForLaters](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/commerce.schema.md#xdmsaveforlaters) | Optional | Ein Produkt wird für die zukünftige Verwendung gespeichert. |

Hier ist ein Beispiel, wie Sie diese Maßnahmen (`Measures`) im SDK festlegen.

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

Das Commerce-Objekt verfügt auch über ein spezielles Feld zum Sammeln von Bestelldetails namens `order`.

| **Auftrag** | **Option** | **Empfehlung** | **Beschreibung** |
|---|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) |  |  | Die [ISO 4217](https://de.wikipedia.org/wiki/ISO_4217)-Währung für die Bestellsumme. |
| [payments[paymentItems]](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpayments) |  |  | Die Liste der Zahlungen für eine Bestellung. Ein [paymentItem](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#payment-item-schema) beinhaltet Folgendes. |
|  | [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmcurrencycode) | Optional | Die [ISO 4217](https://de.wikipedia.org/wiki/ISO_4217)-Währung für diese Zahlungsmethode. |
|  | [paymentAmount](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymentamount) | Dringend empfohlen | Der Wert der Zahlung im angegebenen Währungs-Code. |
|  | [paymentType](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype) | Dringend empfohlen | Die Art der Zahlung (z. B. `credit_card`, `gift_card`, `paypal`). Weitere Informationen finden Sie in der Liste der [bekannten Werte](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmpaymenttype-known-values). |
|  | [transactionID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/paymentitem.schema.md#xdmtransactionid) | Optional | Eine eindeutige Kennung für diesen Zahlungsvorgang. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpricetotal) |  | Dringend empfohlen | Die Summe für diese Bestellung, nachdem alle Rabatte und Steuern berücksichtigt wurden. |
| [purchaseID](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseid) |  | Dringend empfohlen | Die eindeutige Kennung, die der Verkäufer diesem Kauf zugewiesen hat. |
| [purchaseOrderNumber](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/data/order.schema.md#xdmpurchaseordernumber) |  | Optional | Eine eindeutige Kennung, die der Käufer diesem Kauf zugewiesen hat. |

Hier ein Beispiel für einen typischen Kauf im SDK.

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

## Produktlisten

Die Produktliste gibt an, welche Produkte mit der entsprechenden Aktion in Verbindung stehen. Es handelt sich um eine Liste von [productListItems](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md). Jedes Produkt verfügt über eine Reihe optionaler Felder.

| **Feld** | **Empfehlung** | **Beschreibung** |
|---|---|---|
| [currencyCode](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmcurrencycode) | Optional | Die [ISO 4217](https://de.wikipedia.org/wiki/ISO_4217)-Währung für das Produkt. Dies ist nur dann nützlich, wenn Sie Produkte mit unterschiedlichen Währungs-Codes haben können und wenn es anwendbar ist. Wenn es beispielsweise einen Kauf gibt oder eine Artikel zum Warenkorb hinzugefügt wird. |
| [priceTotal](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmpricetotal) | Dringend empfohlen | Sollte nur sofern zutreffend eingestellt werden. So ist es beispielsweise möglicherweise nicht möglich, `productView` -Ereignis eintreten, da unterschiedliche Produktvarianten unterschiedliche Preise haben können, jedoch auf einer `productListAdds` -Ereignis. |
| [product](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproduct) | Dringend empfohlen | Die XDM-ID für das Produkt. |
| [productAddMethod](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmproductaddmethod) | Dringend empfohlen | Die Methode, mit der der Besucher der Liste ein Produktelement hinzufügen konnte. Wird mit `productListAdds`-Maßnahmen eingestellt und sollte nur verwendet werden, wenn ein Produkt der Liste hinzugefügt wird. Beispiele sind `add to cart button`, `quick add` und `upsell`. |
| [productName](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmname) | Dringend empfohlen | Dies wird auf den Anzeigenamen oder den für Menschen lesbaren Namen des Produkts festgelegt. |
| [quantity](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md#xdmquantity) | Dringend empfohlen | Die Anzahl der Einheiten, die der Kunde vom Produkt benötigt. Sollte auf `productListAdds`, `productListRemoves`, `purchases`, `saveForLaters` usw. eingestellt werden. |
| [SKU](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/content/productlistitem.schema.md) | Dringend empfohlen | Bestandseinheit. Dies ist die eindeutige Kennung für das Produkt. |

## Beispiele

`productViews`-Ereignis

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

`productListAdds`-Ereignis

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

`checkouts`-Ereignis

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

`order`-Ereignis

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
