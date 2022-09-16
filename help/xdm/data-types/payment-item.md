---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Zahlungselement; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Datentyp des Zahlungselements
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über den Datentyp "Payment Item Experience Data Model (XDM)".
exl-id: d25a358b-73c1-468b-a9c5-808385689932
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 34%

---

# [!UICONTROL Zahlungselement] Datentyp

[!UICONTROL Zahlungselement] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der eine Zahlung beschreibt, die mit einer Bestellung verbunden ist, die die Art der Zahlung, den Betrag und die zugehörige Währung definiert.

<img src="../images/data-types/payment-item.PNG" width="400" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `currencyCode` | Zeichenfolge | Der für die Bestellsummen verwendete Währungscode nach ISO 4217. Alle Instanzen müssen dem regulären Ausdruck entsprechen `^[A-Z]{3}$`. Beispiele sind `USD` und `EUR`. |
| `paymentAmount` | Double | Der Betrag der Zahlung. |
| `paymentType` | Zeichenfolge | Die Zahlungsmethode für diese Bestellung. Zu den zulässigen Enum-Werten gehören: <li> `cash` </li> <li> `credit_card` </li> <li> `debit_card` </li> <li> `gift_card` </li> <li> `check` </li> <li> `paypal` </li> <li> `wire_transfer` </li> <li> `credit_card_reference` </li> <li> `other` </li> |
| `transactionID` | Zeichenfolge | Die eindeutige Transaktionskennung für diesen Zahlungsposten. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.schema.json)
