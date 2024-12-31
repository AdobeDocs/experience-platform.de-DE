---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;Felder;Schemata;Schemata;Reihenfolge;Datentyp;Datentyp;Datentyp;
solution: Experience Platform
title: Datentyp der Bestellung
description: Erfahren Sie mehr über den Datentyp Order Experience-Datenmodell (XDM).
exl-id: abfc6d53-ffe6-4692-ad65-03d556831fa0
source-git-commit: 09ca510da0819ab38687edadbcc632ccbbe8ef83
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 13%

---

# [!UICONTROL Reihenfolge] Datentyp

[!UICONTROL Order] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der die für eine Produktliste aufgegebene Reihenfolge beschreibt.

![Ein Diagramm des Datentyps [!UICONTROL Bestellung].](../images/data-types/order.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|-------------------------|-------------------------|-----------|------------------------------------------------------------------------------------------------------------------|
| Kauf-ID | `purchaseID` | String | Eine eindeutige Kennung, die vom Verkäufer für diesen Kauf oder Vertrag zugewiesen wurde. Es gibt keine Garantie dafür, dass die ID eindeutig ist, da die ID vom Verkäufer definiert wird. |
| Bestellnummer | `purchaseOrderNumber` | String | Eine eindeutige Kennung, die vom Käufer für diesen Kauf oder Vertrag zugewiesen wird. |
| Zahlungsliste | `payments` | Array von [[!UICONTROL Zahlungselementen]](./payment-item.md) | Die Liste der Zahlungen für diese Bestellung. Zahlungen werden in der Spezifikation [!UICONTROL Zahlungselemente] beschrieben. |
| Erstattungsliste | `refunds` | Array von [[!UICONTROL Erstattungselementen]](./refund-item.md) | Die Liste der Erstattungen für diese Bestellung. Erstattungen sind in der Spezifikation [!UICONTROL Erstattungsgegenstände] aufgeführt. |
| Rückgabeinformationen | `returns` | [[!UICONTROL Rückgabeinformationen]](./return.md) | Die RMA (Return Merchandising Authorization). Rücksendungen werden in der Spezifikation [!UICONTROL Rückgabeinformationen] beschrieben. |
| Währung | `currencyCode` | String | Der ISO 4217-Währungscode, der für die Bestellsummen verwendet wird. Beispiele sind `USD` und `EUR`. Alle Instanzen müssen dem Muster `^[A-Z]{3}$` entsprechen. |
| Steuerbetrag | `taxAmount` | Zahl | Der vom Käufer als Teil der Abschlusszahlung gezahlte Steuerbetrag. |
| Rabattbetrag | `discountAmount` | Zahl | Die Differenz zwischen dem regulären Preis und dem Sonderpreis galt für die gesamte Bestellung und nicht für einzelne Produkte. |
| Gesamtpreis | `priceTotal` | Zahl | Der Gesamtpreis für diese Bestellung, nachdem alle Rabatte und Steuern berücksichtigt wurden. |
| Auftragstyp | `orderType` | String | Der Typ der aufgegebenen Bestellung. Mögliche Werte sind `checkout` und `instant_purchase`. |
| Datum der letzten Aktualisierung | `lastUpdatedDate` | String | Der Zeitpunkt, zu dem ein bestimmter Bestelldatensatz im Commerce-System zuletzt aktualisiert wurde. Format: Datum-Uhrzeit. |
| Datum erstellen | `createdDate` | String | Der Zeitpunkt/das Datum, zu dem eine neue Bestellung im Commerce-System erstellt wird. Format: Datum-Uhrzeit. |
| Abbruchdatum | `cancelDate` | String | Das Datum/die Uhrzeit, zu dem/der eine Stornierung der Bestellung vom Einkäufer initiiert wird. Format: Datum-Uhrzeit. |
| Rückerstatteter Gesamtbetrag | `refundTotal` | Zahl | Der Gesamtbetrag in dieser Rückerstattung auf die Bestellung, kombiniert alle zurückerstatteten Artikel und nach allen Rabatten usw. wurden angewendet. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)
