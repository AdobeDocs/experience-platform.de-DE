---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;Felder;Schemas;Schemas;Reihenfolge;Datentyp;Datentyp; Datentyp;
solution: Experience Platform
title: Datentyp ordnen
topic: overview
description: Dieses Dokument bietet eine Übersicht über den Datentyp des Bestellerlebnis-Datenmodells (XDM).
translation-type: tm+mt
source-git-commit: 8bbb062df47b6e94630626d0a89a179d759d922d
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 22%

---


#  Bestelldatentyp

[!UICONTROL Die ] Bestellung ist ein standardmäßiger XDM-Datentyp (Experience Data Model), der die Reihenfolge einer Produkt-Liste beschreibt.

<img src="../images/data-types/order.PNG" width="400" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `payments` | Array von [[!UICONTROL Zahlungselemente]](./payment-item.md) | Die Liste der Zahlungen für diese Bestellung. |
| `currencyCode` | Zeichenfolge | Der für die Bestellsummen verwendete Währungscode nach ISO 4217. Alle Instanzen müssen dem regulären Ausdruck `^[A-Z]{3}$` entsprechen. Beispiele sind `USD` und `EUR`. |
| `priceTotal` | Double | Der Gesamtpreis für diese Bestellung, nachdem alle Rabatte und Steuern berücksichtigt wurden. |
| `purchaseID` | Zeichenfolge | Eine vom Verkäufer für diesen Kauf oder Vertrag zugewiesene eindeutige Kennung. Da dies vom Verkäufer definiert wird, gibt es keine Garantie dafür, dass die ID eindeutig ist. |
| `purchaseOrderNumber` | Zeichenfolge | Die vom Käufer für diesen Kauf oder Vertrag zugewiesene eindeutige Kennung. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)