---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Adresse; xdm:address; Datentyp; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Datentyp des Produktlistenelements
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über den XDM-Datentyp des Produktlistenelements.
exl-id: 056fdb5b-6782-4e29-9d62-90b270c05795
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 17%

---

# [!UICONTROL Produktlistenelement] Datentyp

[!UICONTROL Produktlistenelement] ist ein standardmäßiger XDM-Datentyp, der ein von einem Kunden ausgewähltes Produkt mit bestimmten Optionen, Preisen und Nutzungskontext für einen bestimmten Zeitpunkt beschreibt.

Die in diesem Datentyp erfassten Werte können vom Produktdatensatz abweichen. Beispielsweise enthält der Produktdatensatz Details aus dem Produktinformationssystem, die für alle Kunden einheitlich sind, wobei der Produktlistenartikel den tatsächlichen Preis aufweist, der dem Kunden zum Zeitpunkt des Kaufs angeboten wird, was aufgrund von Verkaufskampagnen oder saisonalen Preisen variieren kann.

![](../images/data-types/product-list-item.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `SKU` | [!UICONTROL Zeichenfolge] | Bestandseinheit (Stock Keeping Unit, SKU), die eindeutige Kennung für ein vom Anbieter definiertes Produkt. |
| `_id` | [!UICONTROL Zeichenfolge] | Die Zeileneintrag-ID für diesen Produkteintrag. Das Produkt selbst wird durch `product`. |
| `currencyCode` | [!UICONTROL Zeichenfolge] | Die [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) alphabetischer Währungscode, der für die Preisgestaltung des Produkts verwendet wird. |
| `name` | [!UICONTROL Zeichenfolge] | Der Anzeigename für das Produkt, wie er dem Benutzer für diese Produktansicht angezeigt wird. |
| `priceTotal` | [!UICONTROL Double] | Der Gesamtpreis für den Produktzeileneintrag. |
| `product` | [!UICONTROL Zeichenfolge] (URI) | Der URI `$id` des XDM-Schemas, das das Produkt selbst erfasst. |
| `productAddMethod` | [!UICONTROL Zeichenfolge] | Die Methode, mit der der Besucher der Liste ein Produktelement hinzufügen konnte. |
| `quantity` | [!UICONTROL Ganzzahl] | Die Anzahl der Einheiten, die der Kunde vom Produkt benötigt. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zum Datentyp der Postanschrift finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json)
