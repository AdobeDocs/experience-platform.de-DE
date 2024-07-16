---
title: Datentyp "Rückerstattungselement"
description: Erfahren Sie mehr über den Datentyp "Refund Item Experience Data Model (XDM)".
exl-id: 9968d314-c6f3-49d9-b860-709d7478c43a
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 13%

---

# Datentyp [!UICONTROL Rückerstattungselement]

[!UICONTROL Rückerstattungselement] ist ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der Informationen über eine Rückerstattung im Zusammenhang mit einer Bestellung erfasst.

![Ein Diagramm des Datentyps &quot;Rückerstattungselement&quot;.](../images/data-types/refund-item.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|--------------------|-----------------------|-----------|---------------------------------------------------------------------------------------------------|
| [!UICONTROL Transaktions-ID] | `transactionID` | Zeichenfolge | Die eindeutige Transaktionskennung für dieses Erstattungselement. |
| [!UICONTROL Erstattungsbetrag] | `refundAmount` | number | Der Wert der Erstattung. |
| [!UICONTROL Rückerstattungsgrund] | `refundReason` | Zeichenfolge | Der Grund, warum eine Erstattung gewährt wurde. |
| [!UICONTROL Rückerstattungstyp] | `refundPaymentType` | Zeichenfolge | Die Zahlungsmethode für diese Bestellung. Benutzerdefinierte Werte sind zulässig. |
| [!UICONTROL Währungscode] | `currencyCode` | Zeichenfolge | Der Währungscode nach ISO 4217, der für diesen Erstattungsbetrag verwendet wird. Beispiele: &quot;USD&quot;, &quot;EUR&quot;. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/refunditem.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/refunditem.schema.json)
