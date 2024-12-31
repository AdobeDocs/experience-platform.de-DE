---
title: Versanddatentyp
description: Erfahren Sie mehr über den Datentyp Versand-Experience-Datenmodell (XDM) .
exl-id: c3a58e46-c80e-4896-b21c-47dc5a6c869b
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 19%

---

# [!UICONTROL Versand] Datentyp

[!UICONTROL Shipping] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Details zum Versand eines oder mehrerer Produkte bereitstellt. Sie enthält Details zur Logistik und Details zur Lieferung bestellter Artikel.


![Diagramm des Datentyps [!UICONTROL Versand].](../images/data-types/shipping.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|----------------------|-----------------------|-----------|------------------------------------------------------|
| [!UICONTROL Versandart] | `shippingMethod` | Zeichenfolge | Die vom Kunden gewählte Versandart. |
| [!UICONTROL Lieferbetrag] | `shippingAmount` | number | Der Betrag, den der Kunde für die Lieferung zahlen musste. |
| [!UICONTROL Währungscode] | `currencyCode` | Zeichenfolge | Der alphabetische ISO 4217-Währungscode, der für die Preisgestaltung des Produkts verwendet wird. |
| [!UICONTROL Versandziel] | `shippingDestination` | Zeichenfolge | Die vom Benutzer angegebene Lieferadresse (z. B. Startseite, Geschäft usw.). |
| [!UICONTROL Lieferdatum] | `shipDate` | Zeichenfolge | Das Datum, an dem ein oder mehrere Artikel aus einer Bestellung versendet werden. |
| [!UICONTROL Lieferadresse] | `address` | [[!UICONTROL Adresse]](./address.md) | Die Lieferadresse. |
| [!UICONTROL Tracking-Nummer] | `trackingNumber` | number | Die vom Versandunternehmen angegebene Tracking-Nummer. |
| [!UICONTROL Tracking-URL] | `trackingURL` | Zeichenfolge | Die URL zum Nachverfolgen des Versandstatus eines Bestellartikels. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json)
