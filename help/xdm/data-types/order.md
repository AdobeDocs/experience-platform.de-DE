---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;Felder;Schemas;Schemas;Reihenfolge;Datentyp;Datentyp; Datentyp;
solution: Experience Platform
title: Datentyp ordnen
topic-legacy: overview
description: Dieses Dokument bietet eine Übersicht über den Datentyp des Bestellerlebnis-Datenmodells (XDM).
exl-id: abfc6d53-ffe6-4692-ad65-03d556831fa0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
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
