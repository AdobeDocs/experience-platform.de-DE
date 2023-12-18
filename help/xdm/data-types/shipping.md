---
title: Versanddatentyp
description: Erfahren Sie mehr über den XDM-Datentyp (Shipping Experience Data Model).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 11%

---

# [!UICONTROL Versand] Datentyp

[!UICONTROL Versand] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Details zum Versand eines oder mehrerer Produkte bereitstellt. Sie enthält Details zur Logistik und Details zur Lieferung von bestellten Artikeln.


![Ein Diagramm des [!UICONTROL Versand] Datentyp.](../images/data-types/shipping.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|----------------------|-----------------------|-----------|------------------------------------------------------|
| [!UICONTROL Versandart] | `shippingMethod` | Zeichenfolge | Die vom Kunden gewählte Versandmethode. |
| [!UICONTROL Versandbetrag] | `shippingAmount` | number | Der Betrag, den der Kunde für den Versand zahlen musste. |
| [!UICONTROL Währungscode] | `currencyCode` | Zeichenfolge | Der alphabetische ISO 4217-Währungscode, der zur Preisbildung für das Produkt verwendet wird. |
| [!UICONTROL Versandziel] | `shippingDestination` | Zeichenfolge | Das vom Benutzer angegebene Schiff zum Ziel (z. B. zu Hause, im Speicher usw.). |
| [!UICONTROL Versanddatum] | `shipDate` | Zeichenfolge | Das Datum, an dem ein oder mehrere Artikel aus einer Bestellung versandt werden. |
| [!UICONTROL Lieferadresse] | `address` | [[!UICONTROL Adresse]](./address.md) | Die Lieferadresse. |
| [!UICONTROL Tracking-Nummer] | `trackingNumber` | number | Die vom Versandunternehmen angegebene Trackingnummer. |
| [!UICONTROL Tracking-URL] | `trackingURL` | Zeichenfolge | Die URL zur Verfolgung des Versandstatus eines Bestellartikels. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json)
