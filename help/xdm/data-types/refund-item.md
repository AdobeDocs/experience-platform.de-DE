---
title: Datentyp "Rückerstattungselement"
description: Erfahren Sie mehr über den Datentyp "Refund Item Experience Data Model (XDM)".
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 14%

---

# [!UICONTROL Erstattungsbetrag] Datentyp

[!UICONTROL Erstattungsbetrag] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Informationen über eine mit einer Bestellung verknüpfte Erstattung erfasst.

![Ein Diagramm des Datentyps Rückerstattungselement .](../images/data-types/refund-item.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|--------------------|-----------------------|-----------|---------------------------------------------------------------------------------------------------|
| [!UICONTROL Transaktions-ID] | `transactionID` | Zeichenfolge | Die eindeutige Transaktionskennung für dieses Erstattungselement. |
| [!UICONTROL Erstattungsbetrag] | `refundAmount` | number | Der Wert der Erstattung. |
| [!UICONTROL Erstattungsgrund] | `refundReason` | Zeichenfolge | Der Grund, warum eine Erstattung gewährt wurde. |
| [!UICONTROL Art der Rückzahlung] | `refundPaymentType` | Zeichenfolge | Die Zahlungsmethode für diese Bestellung. Benutzerdefinierte Werte sind zulässig. |
| [!UICONTROL Währungscode] | `currencyCode` | Zeichenfolge | Der Währungscode nach ISO 4217, der für diesen Erstattungsbetrag verwendet wird. Beispiele: &quot;USD&quot;, &quot;EUR&quot;. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/refunditem.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/refunditem.schema.json)
