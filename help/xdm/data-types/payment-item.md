---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;Felder;Schemas;Schemas;Zahlungselement;Datentyp;Datentyp; Datentyp;
solution: Experience Platform
title: Datentyp des Zahlungselements
topic-legacy: overview
description: Dieses Dokument bietet eine Übersicht über den Datentyp "Payment Item Experience Data Model"(XDM).
exl-id: d25a358b-73c1-468b-a9c5-808385689932
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 24%

---

# [!UICONTROL Zahlungselement-] Datentyp

[!UICONTROL Payment ] Item ist ein standardmäßiger XDM-Datentyp (Experience Data Model), der eine Zahlung beschreibt, die mit einer Bestellung verknüpft ist, die die Art der Zahlung, den Betrag und die zugehörige Währung definiert.

<img src="../images/data-types/payment-item.PNG" width="400" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `currencyCode` | Zeichenfolge | Der für die Bestellsummen verwendete Währungscode nach ISO 4217. Alle Instanzen müssen dem regulären Ausdruck `^[A-Z]{3}$` entsprechen. Beispiele sind `USD` und `EUR`. |
| `paymentAmount` | Double | Der Betrag der Zahlung. |
| `paymentType` | Zeichenfolge | Die Zahlungsmethode für diese Bestellung. Zu den zulässigen Enum-Werten gehören: <li> `cash` </li> <li> `credit_card` </li> <li> `debit_card` </li> <li> `gift_card` </li> <li> `check` </li> <li> `paypal` </li> <li> `wire_transfer` </li> <li> `credit_card_reference` </li> <li> `other` </li> |
| `transactionID` | Zeichenfolge | Die eindeutige Transaktionskennung für diesen Zahlungsposten. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.schema.json)
