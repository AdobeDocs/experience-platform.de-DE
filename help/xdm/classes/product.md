---
title: Produktklasse
description: Erfahren Sie mehr über die Produktklasse im Experience-Datenmodell (XDM).
exl-id: 911680ae-b761-4945-9ad3-0233eaea89b0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 15%

---

# [!UICONTROL Produkt] class

Im Experience-Datenmodell (XDM) wird die [!UICONTROL Produkt] -Klasse erfasst den Mindestsatz von Eigenschaften, die ein Einzelhandelsprodukt definieren.

![](../images/classes/product.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `productListPrice` | [Währung](../data-types/currency.md) | Beschreibt den Standardpreis des Produkts vor Verkauf und Rabatt. |
| `_id` | Zeichenfolge | Eine eindeutige, systemgenerierte Zeichenfolgenkennung für den Datensatz. Dieses Feld wird verwendet, um die Eindeutigkeit eines einzelnen Datensatzes zu verfolgen, Datenduplizierung zu verhindern und diesen Datensatz in nachgelagerten Diensten nachzuschlagen.<br><br>Da dieses Feld systemgeneriert ist, wird bei der Datenerfassung kein expliziter Wert angegeben. Sie können jedoch weiterhin Ihre eigenen eindeutigen ID-Werte angeben, wenn Sie möchten. |
| `productDescription` | Zeichenfolge | Eine Beschreibung des Produkts. |
| `productID` | Zeichenfolge | Eine eindeutige Kennung für das Produkt. |
| `productLastModifiedDate` | DateTime | Ein [RFC 3339](https://datatracker.ietf.org/doc/html/rfc3339) Zeitstempel der letzten Änderung dieses Produkts bei Aktualisierungen. |
| `productManufacturedDate` | DateTime | Ein [RFC 3339](https://datatracker.ietf.org/doc/html/rfc3339) Zeitstempel der Erstellung dieses Produkts. |
| `productName` | Zeichenfolge | Der Name des Produkts. |
| `productRating` | Zeichenfolge | Die Kundenüberprüfungsbewertung des Produkts. |

{style="table-layout:auto"}

## Kompatible Feldergruppen {#field-groups}

Adobe stellt mehrere Standardfeldgruppen zur Verfügung, die mit der [!UICONTROL Produkt] -Klasse. Im Folgenden finden Sie eine Liste einiger häufig verwendeter Feldergruppen für die Klasse:

* [[!UICONTROL Produktkatalog]](../field-groups/product/product-catalog.md)
* [[!UICONTROL Produktkategorie]](../field-groups/product/product-category.md)
