---
keywords: Experience Platform; home; beliebte Themen; schema; XDM; Felder; Schemas; Schemas; Adresse; xdm:address; Datentyp; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Datentyp des Produktlistenelements
description: Erfahren Sie mehr über den XDM-Datentyp des Produktlistenelements.
exl-id: 056fdb5b-6782-4e29-9d62-90b270c05795
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 7%

---

# [!UICONTROL Produktlistenelement] Datentyp

[!UICONTROL Produktlistenelement] ist ein standardmäßiger XDM-Datentyp, der ein von einem Kunden ausgewähltes Produkt mit bestimmten Optionen, Preisen und Nutzungskontext für einen bestimmten Zeitpunkt beschreibt.

Die in diesem Datentyp erfassten Werte können vom Produktdatensatz abweichen. Beispielsweise enthält der Produktdatensatz Details aus dem Produktinformationssystem, die für alle Kunden einheitlich sind, wobei der Produktlistenartikel den tatsächlichen Preis aufweist, der dem Kunden zum Zeitpunkt des Kaufs angeboten wird, was aufgrund von Verkaufskampagnen oder saisonalen Preisen variieren kann.

![](../images/data-types/product-list-item.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `selectedOptions` | Array von Objekten | Enthält benutzerdefinierte Optionen, die für ein konfigurierbares Produkt ausgewählt wurden. Jedes Listenelement ist ein Objekt mit den folgenden Eigenschaften:<ul><li>`attribute`: Ein Name für das konfigurierbare Attribut.</li><li>`value`: Der -Wert des Attributs.</li></ul> |
| `SKU` | [!UICONTROL String] | Bestandseinheit (Stock Keeping Unit, SKU), die eindeutige Kennung eines vom Anbieter definierten Produkts. |
| `_id` | [!UICONTROL String] | Die Zeileneintrag-ID für diesen Produkteintrag. Das Produkt selbst wird durch `product`. |
| `currencyCode` | [!UICONTROL String] | Die [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) alphabetischer Währungscode, der für die Preisgestaltung des Produkts verwendet wird. |
| `discountAmount` | [!UICONTROL Double] | Wenn das Produkt abgezinst wird, entspricht dies der Differenz zwischen dem regulären Preis und dem Sonderpreis für das Produkt. |
| `name` | [!UICONTROL String] | Der Anzeigename für das Produkt, wie er dem Benutzer für diese Produktansicht angezeigt wird. |
| `priceTotal` | [!UICONTROL Double] | Der Gesamtpreis für den Produktzeileneintrag. |
| `product` | [!UICONTROL Zeichenfolge] (URI) | Der URI `$id` des XDM-Schemas, das das Produkt selbst erfasst. |
| `productAddMethod` | [!UICONTROL String] | Die Methode, mit der der Besucher der Liste ein Produktelement hinzugefügt hat. |
| `productImageUrl` | [!UICONTROL String] | Eine URL für das Hauptbild des Produkts. |
| `quantity` | [!UICONTROL Ganzzahl] | Die Anzahl der Einheiten, die der Kunde vom Produkt benötigt. |
| `unitOfMeasureCode` | [!UICONTROL String] | Der Standard [Maßeinheit](https://ucum.org/ucum) für das Produkt in Bezug auf die `quantity` -Eigenschaft. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp der Postanschrift finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json)
