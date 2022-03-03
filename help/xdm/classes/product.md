---
title: Produktklasse
description: Dieses Dokument bietet einen Überblick über die Produktklasse im Experience-Datenmodell (XDM).
source-git-commit: c0437b8f9d93c46dbec991a33a893a5b9e0cdf2c
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 15%

---

# [!UICONTROL Produkt] class

Im Experience-Datenmodell (XDM) wird die [!UICONTROL Produkt] -Klasse erfasst den Mindestsatz von Eigenschaften, die ein Produkt definieren.

![](../images/classes/product.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `productListPrice` | [Währung](../data-types/currency.md) | Beschreibt den Standardpreis des Produkts vor Verkauf und Rabatt. |
| `_id` | Zeichenfolge | Eine eindeutige, systemgenerierte Zeichenfolgenkennung für den Datensatz. Dieses Feld wird verwendet, um die Eindeutigkeit eines einzelnen Datensatzes zu verfolgen, Datenduplizierung zu verhindern und diesen Datensatz in nachgelagerten Diensten nachzuschlagen.<br><br>Da dieses Feld systemgeneriert wird, wird bei der Datenerfassung kein expliziter Wert angegeben. Sie können jedoch weiterhin Ihre eigenen eindeutigen ID-Werte angeben, wenn Sie möchten. |
| `productDescription` | Zeichenfolge | Eine Beschreibung des Produkts. |
| `productID` | Zeichenfolge | Eine eindeutige Kennung für das Produkt. |
| `productLastModifiedDate` | DateTime | Ein [RFC 3339](https://datatracker.ietf.org/doc/html/rfc3339) Zeitstempel der letzten Änderung dieses Produkts bei Aktualisierungen. |
| `productManufacturedDate` | DateTime | Ein [RFC 3339](https://datatracker.ietf.org/doc/html/rfc3339) Zeitstempel der Erstellung dieses Produkts. |
| `productName` | Zeichenfolge | Der Name des Produkts. |
| `productRating` | Zeichenfolge | Die Kundenüberprüfungsbewertung des Produkts. |

{style=&quot;table-layout:auto&quot;}

## Kompatible Feldergruppen {#field-groups}

Adobe bietet mehrere Standardfeldgruppen zur Verwendung mit der [!DNL XDM Individual Profile] -Klasse. Im Folgenden finden Sie eine Liste einiger häufig verwendeter Feldergruppen für die Klasse:

* [[!UICONTROL Produktkatalog]](../field-groups/product/product-catalog.md)
* [[!UICONTROL Produktkategorie]](../field-groups/product/product-category.md)
