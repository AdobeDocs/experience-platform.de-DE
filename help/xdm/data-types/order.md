---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Reihenfolge; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Auftragsdatentyp
description: Dieses Dokument bietet einen Überblick über den Datentyp "Order Experience Data Model (XDM)".
exl-id: abfc6d53-ffe6-4692-ad65-03d556831fa0
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 30%

---

# [!UICONTROL Bestellung] Datentyp

[!UICONTROL Bestellung] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der die für eine Produktliste platzierte Reihenfolge beschreibt.

<img src="../images/data-types/order.PNG" width="400" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `payments` | Array von [[!UICONTROL Zahlungselemente]](./payment-item.md) | Die Liste der Zahlungen für diese Bestellung. |
| `currencyCode` | Zeichenfolge | Der für die Bestellsummen verwendete Währungscode nach ISO 4217. Alle Instanzen müssen dem regulären Ausdruck entsprechen `^[A-Z]{3}$`. Beispiele sind `USD` und `EUR`. |
| `priceTotal` | Double | Der Gesamtpreis für diese Bestellung, nachdem alle Rabatte und Steuern berücksichtigt wurden. |
| `purchaseID` | Zeichenfolge | Eine eindeutige Kennung, die vom Verkäufer für diesen Kauf oder Vertrag zugewiesen wird. Da dies vom Verkäufer definiert wird, gibt es keine Garantie, dass die ID eindeutig ist. |
| `purchaseOrderNumber` | Zeichenfolge | Die eindeutige Kennung, die der Käufer diesem Kauf oder Vertrag zugewiesen hat. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)
