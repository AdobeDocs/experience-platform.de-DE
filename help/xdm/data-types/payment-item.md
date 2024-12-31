---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;Felder;Schemata;Schemata;Zahlungsposten;Datentyp;Datentyp;
solution: Experience Platform
title: Datentyp des Zahlungspostens
description: Erfahren Sie mehr über den Datentyp „Zahlungsposten-Experience-Datenmodell (XDM)“.
exl-id: d25a358b-73c1-468b-a9c5-808385689932
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 20%

---

# [!UICONTROL Zahlungsartikel] Datentyp

[!UICONTROL Zahlungsposten] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der eine Zahlung beschreibt, die mit einer Bestellung verknüpft ist und die die Art der Zahlung, den Betrag und die zugehörige Währung definiert.

<img src="../images/data-types/payment-item.PNG" width="400" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `currencyCode` | Zeichenfolge | Der ISO 4217-Währungscode, der für die Bestellsummen verwendet wird. Alle Instanzen müssen dem `^[A-Z]{3}$` für reguläre Ausdrücke entsprechen. Beispiele sind `USD` und `EUR`. |
| `paymentAmount` | Double | Der Betrag der Zahlung. |
| `paymentType` | String | Die Zahlungsmethode für diese Bestellung. Zu den akzeptierten Enum-Werten gehören: <li> `cash` </li> <li> `credit_card` </li> <li> `debit_card` </li> <li> `gift_card` </li> <li> `check` </li> <li> `paypal` </li> <li> `wire_transfer` </li> <li> `credit_card_reference` </li> <li> `other` </li> |
| `transactionID` | String | Die eindeutige Transaktionskennung für diesen Zahlungsposten. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.schema.json)
