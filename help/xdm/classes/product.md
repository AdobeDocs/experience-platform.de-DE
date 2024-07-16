---
title: Produktklasse
description: Erfahren Sie mehr über die Produktklasse im Experience-Datenmodell (XDM).
exl-id: 911680ae-b761-4945-9ad3-0233eaea89b0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 15%

---

# [!UICONTROL Product] class

Im Experience-Datenmodell (XDM) erfasst die Klasse [!UICONTROL Produkt] den Mindestsatz von Eigenschaften, die ein Einzelhandelsprodukt definieren.

![](../images/classes/product.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `productListPrice` | [Währung](../data-types/currency.md) | Beschreibt den Standardpreis des Produkts vor Verkauf und Rabatt. |
| `_id` | Zeichenfolge | Eine eindeutige, systemgenerierte Zeichenfolgenkennung für den Datensatz. Dieses Feld wird verwendet, um die Eindeutigkeit eines einzelnen Datensatzes zu verfolgen, Datenduplizierung zu verhindern und diesen Datensatz in nachgelagerten Diensten nachzuschlagen.<br><br>Da dieses Feld systemseitig generiert wird, wird bei der Datenerfassung kein expliziter Wert angegeben. Sie können jedoch weiterhin Ihre eigenen eindeutigen ID-Werte angeben, wenn Sie möchten. |
| `productDescription` | Zeichenfolge | Eine Beschreibung des Produkts. |
| `productID` | Zeichenfolge | Eine eindeutige Kennung für das Produkt. |
| `productLastModifiedDate` | DateTime | Ein [RFC339](https://datatracker.ietf.org/doc/html/rfc3339)-Zeitstempel, mit dem festgelegt wurde, wann dieses Produkt zuletzt für alle Aktualisierungen geändert wurde. |
| `productManufacturedDate` | DateTime | Ein [RFC339](https://datatracker.ietf.org/doc/html/rfc3339)-Zeitstempel des Zeitpunkts der Erstellung dieses Produkts. |
| `productName` | Zeichenfolge | Der Name des Produkts. |
| `productRating` | Zeichenfolge | Die Kundenüberprüfungsbewertung des Produkts. |

{style="table-layout:auto"}

## Kompatible Feldergruppen {#field-groups}

Adobe stellt mehrere Standardfeldgruppen für die Verwendung mit der Klasse [!UICONTROL Produkt] bereit. Im Folgenden finden Sie eine Liste einiger häufig verwendeter Feldergruppen für die Klasse:

* [[!UICONTROL Produktkatalog]](../field-groups/product/product-catalog.md)
* [[!UICONTROL Produktkategorie]](../field-groups/product/product-category.md)
