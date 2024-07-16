---
title: Versanddatentyp
description: Erfahren Sie mehr über den XDM-Datentyp (Shipping Experience Data Model).
exl-id: c3a58e46-c80e-4896-b21c-47dc5a6c869b
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 19%

---

# Datentyp [!UICONTROL Versand]

[!UICONTROL Versand] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Details zum Versand eines oder mehrerer Produkte liefert. Sie enthält Details zur Logistik und Details zur Lieferung von bestellten Artikeln.


![Ein Diagramm des Datentyps [!UICONTROL Shipping].](../images/data-types/shipping.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|----------------------|-----------------------|-----------|------------------------------------------------------|
| [!UICONTROL Versandmethode] | `shippingMethod` | Zeichenfolge | Die vom Kunden gewählte Versandmethode. |
| [!UICONTROL Versandbetrag] | `shippingAmount` | number | Der Betrag, den der Kunde für die Lieferung zahlen musste. |
| [!UICONTROL Währungscode] | `currencyCode` | Zeichenfolge | Der alphabetische ISO 4217-Währungscode, der für die Preisgestaltung des Produkts verwendet wird. |
| [!UICONTROL Versandziel] | `shippingDestination` | Zeichenfolge | Das vom Benutzer angegebene Schiff zum Ziel (z. B. zu Hause, im Speicher usw.). |
| [!UICONTROL Versanddatum] | `shipDate` | Zeichenfolge | Das Datum, an dem ein oder mehrere Artikel aus einer Bestellung versandt werden. |
| [!UICONTROL Versandadresse] | `address` | [[!UICONTROL address]](./address.md) | Die Lieferadresse. |
| [!UICONTROL Tracking Number] | `trackingNumber` | number | Die vom Versandunternehmen angegebene Trackingnummer. |
| [!UICONTROL Tracking-URL] | `trackingURL` | Zeichenfolge | Die URL zur Verfolgung des Versandstatus eines Bestellartikels. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json)
