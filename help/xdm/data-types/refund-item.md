---
title: Datentyp des Erstattungsartikels
description: Erfahren Sie mehr über den Datentyp „Rückerstattungsartikel-Experience-Datenmodell (XDM)“.
exl-id: 9968d314-c6f3-49d9-b860-709d7478c43a
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 13%

---

# [!UICONTROL Rückerstattungsartikel] Datentyp

[!UICONTROL Rückerstattungsartikel] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Informationen erfasst, die sich auf eine Rückerstattung beziehen, die mit einer Bestellung verbunden ist.

![Abbildung des Datentyps „Erstattungsartikel“.](../images/data-types/refund-item.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|--------------------|-----------------------|-----------|---------------------------------------------------------------------------------------------------|
| [!UICONTROL Transaktions-ID] | `transactionID` | Zeichenfolge | Die eindeutige Transaktionskennung für diesen Rückerstattungsartikel. |
| [!UICONTROL Erstattungsbetrag] | `refundAmount` | number | Der Wert der Erstattung. |
| [!UICONTROL Grund für die Rückerstattung] | `refundReason` | Zeichenfolge | Der Grund, warum eine Erstattung gewährt wurde. |
| [!UICONTROL Art der Rückerstattung] | `refundPaymentType` | Zeichenfolge | Die Zahlungsmethode für diese Bestellung. Benutzerdefinierte Werte sind zulässig. |
| [!UICONTROL Währungscode] | `currencyCode` | Zeichenfolge | Der ISO 4217-Währungscode, der für diesen Erstattungsartikel verwendet wird. Beispiele: „USD“, „EUR“. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/refunditem.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/refunditem.schema.json)
