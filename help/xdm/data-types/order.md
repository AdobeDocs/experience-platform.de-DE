---
keywords: Experience Platform; home; beliebte Themen; schema; XDM; Felder; Schemas; Schemas; Reihenfolge; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Auftragsdatentyp
description: Erfahren Sie mehr über den Datentyp Order Experience Data Model (XDM) .
exl-id: abfc6d53-ffe6-4692-ad65-03d556831fa0
source-git-commit: 09ca510da0819ab38687edadbcc632ccbbe8ef83
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 13%

---

# [!UICONTROL Bestellung] Datentyp

[!UICONTROL Bestellung] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der die für eine Produktliste platzierte Reihenfolge beschreibt.

![Ein Diagramm des [!UICONTROL Bestellung] Datentyp.](../images/data-types/order.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|-------------------------|-------------------------|-----------|------------------------------------------------------------------------------------------------------------------|
| Kauf-ID | `purchaseID` | Zeichenfolge | Eine eindeutige Kennung, die vom Verkäufer für diesen Kauf oder Vertrag zugewiesen wird. Es gibt keine Garantie dafür, dass die ID eindeutig ist, da die ID vom Verkäufer definiert wird. |
| Bestellnummer | `purchaseOrderNumber` | Zeichenfolge | Eine eindeutige Kennung, die vom Käufer für diesen Kauf oder Vertrag zugewiesen wird. |
| Zahlungsliste | `payments` | Array von [[!UICONTROL Zahlungselemente]](./payment-item.md) | Die Liste der Zahlungen für diese Bestellung. Die Zahlungen sind im Abschnitt [!UICONTROL Zahlungselemente] Spezifikation. |
| Erstattungsliste | `refunds` | Array von [[!UICONTROL Erstattungsbeträge]](./refund-item.md) | Die Liste der Erstattungen für diese Bestellung. Die Erstattungen sind im Abschnitt [!UICONTROL Erstattungsbeträge] Spezifikation. |
| Rückkehrinformationen | `returns` | [[!UICONTROL Rückkehrinformationen]](./return.md) | RMA (Return Merchandise Authorization) ausgestellt. Die Rückgaben werden im Abschnitt [!UICONTROL Rückkehrinformationen] Spezifikation. |
| Währung | `currencyCode` | Zeichenfolge | Der für die Bestellsummen verwendete Währungscode nach ISO 4217. Beispiele sind `USD` und `EUR`. Alle Instanzen müssen dem Muster entsprechen `^[A-Z]{3}$`. |
| Steuerbetrag | `taxAmount` | Zahl | Der vom Käufer im Rahmen der Abschlusszahlung entrichtete Steuerbetrag. |
| Rabattbetrag | `discountAmount` | Zahl | Der Unterschied zwischen dem regulären Preis und dem Sonderpreis, der auf die gesamte Bestellung und nicht auf einzelne Produkte angewandt wird. |
| Gesamtpreis | `priceTotal` | Zahl | Der Gesamtpreis für diese Bestellung, nachdem alle Rabatte und Steuern berücksichtigt wurden. |
| Auftragstyp | `orderType` | Zeichenfolge | Die Art der Reihenfolge, die platziert wurde. Mögliche Werte sind `checkout` und `instant_purchase`. |
| Datum der letzten Aktualisierung | `lastUpdatedDate` | Zeichenfolge | Der Zeitpunkt, zu dem ein bestimmter Bestelldatensatz zuletzt im Commerce-System aktualisiert wird. Format: Datum/Uhrzeit. |
| Datum erstellen | `createdDate` | Zeichenfolge | Der Zeitpunkt/das Datum, an dem eine neue Bestellung im Commerce-System erstellt wird. Format: Datum/Uhrzeit. |
| Datum abbrechen | `cancelDate` | Zeichenfolge | Datum/Uhrzeit, zu der die Stornierung einer Bestellung durch den Käufer eingeleitet wird. Format: Datum/Uhrzeit. |
| Erstatteter Gesamtbetrag | `refundTotal` | Zahl | Der Gesamtbetrag, der in dieser Erstattung für die Bestellung angegeben wird, wobei alle erstatteten Artikel und nach etwaigen Rabatten usw. zusammengefasst werden. angewendet wurden. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)
