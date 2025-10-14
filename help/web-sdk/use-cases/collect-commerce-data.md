---
title: Erfassen von Handels-, Produkt- und Bestellinformationen mithilfe der Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie mit der Adobe Experience Platform Web SDK Daten zu Produkten oder einem Warenkorb hinzufügen.
exl-id: 3c79e776-89ef-494b-a2ea-3c23efce09ae
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 37%

---

# Erfassen von Handels-, Produkt- und Bestellinformationen

Wenn Ihr Unternehmen Produkte oder Services verkauft, können Sie diese Seite als Anleitung zum Nachverfolgen dieser Produkte und Services verwenden.

Auf dieser Seite wird die Feldergruppe XDM [Commerce](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md)Schema verwendet.

Diese Feldergruppe besteht aus zwei Hauptteilen:

* Das `commerce`. Mit diesem Objekt können Sie angeben, welche Aktionen mit dem `productListItems`-Array durchgeführt werden.
* Das `productListItems`-Array.

>[!TIP]
>
>Wenn Sie mit Adobe Analytics vertraut sind, enthält das `commerce`-Objekt Daten, die Commerce-Ereignissen in der `events`-Variablen ähnlich sind. Das `productListItems`-Objekt-Array enthält Daten, die der `products`-Variablen ähnlich sind.

## Das `commerce` {#commerce-object}

In diesem Abschnitt werden die im `commerce`-Objekt verfügbaren Felder beschrieben.

>[!TIP]
>
>Eine Maßnahme umfasst zwei Bereiche: `id` und `value`. Meistens verwenden Sie nur das Feld `value` (z. B. `'value':1`). Mit dem Feld `id` können Sie eine eindeutige Kennung für das Tracking festlegen, wann die Kennzahl gesendet wurde. Weitere Informationen finden Sie in der XDM[Dokumentation &#x200B;](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/measure.schema.md)Measure).

| Maßnahme | Empfehlung | Beschreibung |
|---|---|---|
| [`cartAbandons`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmcartabandons) | Optional | Ein Warenkorb kann vom Nutzer nicht mehr aufgerufen oder gekauft werden. |
| [`checkouts`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmcheckouts) | Sehr empfehlenswert | Ein Nutzer sucht nicht mehr nach Produkten, sondern kauft gerade ein Produkt. |
| [`productListAdds`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistadds) | Sehr empfehlenswert | Ein Produkt wird einer Liste hinzugefügt. Stellen Sie das Produkt gleichzeitig in `productListItems` ein. |
| [`productListOpens`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistopens) | Optional | Eine neue Produktliste wird erstellt. Beispielsweise wird ein neuer Warenkorb erstellt. |
| [`productListRemovals`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistremovals) | Sehr empfehlenswert | Ein Produkt wird aus einer Produktliste entfernt. |
| [`productListReopens`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistreopens) | Optional | Eine Produktliste wird vom Nutzer reaktiviert. Diese Aktion tritt häufig in Remarketing-Kampagnen auf. |
| [`productListViews`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductlistviews) | Sehr empfehlenswert | Eine Liste von Produkten wird angezeigt. |
| [`productViews`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmproductviews) | Sehr empfehlenswert | Ein Blick auf ein Produkt geschah. Stellen Sie das angesehene Produkt in `productListItems` ein. |
| [`purchases`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmpurchases) | Sehr empfehlenswert | Eine Bestellung wird angenommen. Muss eine Produktliste haben. |
| [`saveForLaters`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/commerce.schema.md#xdmsaveforlaters) | Optional | Ein Produkt wird für die zukünftige Verwendung gespeichert. |

{style="table-layout:auto"}

### Beispiele für `Commerce`

Erweitern Sie den folgenden Abschnitt, um ein Beispiel für einen Web SDK-Befehl mit einem Feld aus dem `commerce`-Objekt zu sehen.

+++`productViews`

Ein einfacher Web SDK-`sendEvent`-Aufruf, der das `productViews` auf `1` setzt:

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

## Das `order` {#order-object}

Das `commerce`-Objekt enthält ein dediziertes Objekt zum Erfassen von Auftragsdetails. Dies wird als `order`-Objekt bezeichnet.

In diesem Abschnitt werden alle Felder beschrieben, die vom `order`-Objekt unterstützt werden.

| Feld | Option | Empfehlung | Beschreibung |
|---|---|---|---|
| [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmcurrencycode) |  |  | Die [ISO 4217](https://de.wikipedia.org/wiki/ISO_4217)-Währung für die Bestellsumme. |
| [`payments[]`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpayments) |  |  | Die Liste der Zahlungen für eine Bestellung. Ein [paymentItem](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md) beinhaltet Folgendes. |
|  | [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmcurrencycode) | Optional | Die [ISO 4217](https://de.wikipedia.org/wiki/ISO_4217)-Währung für diese Zahlungsmethode. |
|  | [`paymentAmount`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymentamount) | Sehr empfehlenswert | Der Wert der Zahlung im angegebenen Währungs-Code. |
|  | [`paymentType`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymenttype) | Sehr empfehlenswert | Die Art der Zahlung (z. B. `credit_card`, `gift_card`, `paypal`). Weitere Informationen finden Sie in der Liste der [bekannten Werte](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmpaymenttype-known-values). |
|  | [`transactionID`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/paymentitem.schema.md#xdmtransactionid) | Optional | Eine eindeutige Kennung für diesen Zahlungsvorgang. |
| [`priceTotal`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpricetotal) |  | Sehr empfehlenswert | Die Summe für diese Bestellung, nachdem alle Rabatte und Steuern berücksichtigt wurden. |
| [`purchaseID`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpurchaseid) |  | Sehr empfehlenswert | Die eindeutige Kennung, die der Verkäufer diesem Kauf zugewiesen hat. |
| [`purchaseOrderNumber`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/data/order.schema.md#xdmpurchaseordernumber) |  | Optional | Eine eindeutige Kennung, die der Käufer diesem Kauf zugewiesen hat. |

### Beispiele für Bestellobjekte

Erweitern Sie den folgenden Abschnitt, um ein Beispiel für einen Web SDK-Befehl mit dem `commerce`-Objekt zu sehen.

+++Beispiel für ein `Order`

Ein Web SDK-`sendEvent` ruft auf, indem das `order`-Objekt festgelegt wird, das für mehrere Produkte im `productListItems`-Array gilt:

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
| [`currencyCode`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmcurrencycode) | Optional | Die [ISO 4217](https://de.wikipedia.org/wiki/ISO_4217) Währung für das Produkt. Dieses Feld gilt in der Regel nur, wenn sich mehrere Produkte in der Produktliste mit unterschiedlichen Währungscodes befinden. |
| [`priceTotal`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmpricetotal) | Sehr empfehlenswert | Legen Sie dieses Feld nur fest, wenn zutreffend. Beispielsweise kann es nicht möglich sein, für `productView` Ereignis festzulegen, da verschiedene Varianten des Produkts unterschiedliche Preise aufweisen können, sondern bei einem `productListAdds` Ereignis. |
| [`product`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmproduct) | Sehr empfehlenswert | Die XDM-ID für das Produkt. |
| [`productAddMethod`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmproductaddmethod) | Sehr empfehlenswert | Die Methode, mit der der Besucher der Liste ein Produktelement hinzufügen konnte. Mit `productListAdds` Kennzahlen festgelegt und nur verwendet, wenn ein Produkt zur Liste hinzugefügt wird. Beispiele sind `add to cart button`, `quick add` und `upsell`. |
| [`productName`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmname) | Sehr empfehlenswert | Der Anzeigename oder der für Menschen lesbare Name des Produkts. |
| [`quantity`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmquantity) | Sehr empfehlenswert | Die Anzahl der Einheiten, die der Kunde vom Produkt benötigt. Sollte auf `productListAdds`, `productListRemoves`, `purchases`, `saveForLaters` usw. eingestellt werden. |
| [`SKU`](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/productlistitem.schema.md#xdmsku) | Sehr empfehlenswert | Bestandseinheit. Dies ist die eindeutige Kennung für das Produkt. |

### Beispiele für Produktlisten

Erweitern Sie die folgenden Abschnitte, um Beispiele für Web SDK-Befehle mit dem `productListItems`-Objekt anzuzeigen.

+++`productListItems` Beispiel

Ein Web SDK-`sendEvent` ruft auf, indem der `productViews` für mehrere Produkte im `productListItems`-Array festgelegt wird:

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

Ein Web SDK-`sendEvent` ruft auf, indem das `productListAdds`-Ereignis für mehrere Produkte im `productListItems`-Array festgelegt wird:

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

+++`checkouts` Beispiel

Ein Web SDK-`sendEvent` ruft auf, indem das `checkouts`-Ereignis für mehrere Produkte im `productListItems`-Array festgelegt wird:

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
