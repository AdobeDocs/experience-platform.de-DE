---
title: Produktklasse
description: Erfahren Sie mehr über die Product-Klasse im Experience-Datenmodell (XDM).
exl-id: 911680ae-b761-4945-9ad3-0233eaea89b0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 16%

---

# [!UICONTROL Product]-Klasse

Im Experience-Datenmodell (XDM) erfasst die [!UICONTROL Product]-Klasse den Mindestsatz von Eigenschaften, die ein Einzelhandelsprodukt definieren.

![](../images/classes/product.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `productListPrice` | [Währung](../data-types/currency.md) | Beschreibt den Standardpreis des Produkts vor Verkauf und Rabatt. |
| `_id` | String | Eine eindeutige, systemgenerierte Zeichenfolgenkennung für den Datensatz. Dieses Feld wird verwendet, um die Eindeutigkeit eines einzelnen Datensatzes nachzuverfolgen, Doppelungen von Daten zu verhindern und diesen Datensatz in nachgelagerten Services nachzuschlagen.<br><br>Da dieses Feld systemgeneriert ist, wird bei der Datenaufnahme kein expliziter Wert bereitgestellt. Sie können jedoch auch weiterhin eigene eindeutige ID-Werte angeben, wenn Sie dies wünschen. |
| `productDescription` | String | Eine Beschreibung des Produkts. |
| `productID` | String | Eine eindeutige Kennung für das Produkt. |
| `productLastModifiedDate` | DateTime | Ein [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) Zeitstempel, der angibt, wann dieses Produkt zuletzt für Aktualisierungen geändert wurde. |
| `productManufacturedDate` | DateTime | Ein [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) Zeitstempel, der angibt, wann dieses Produkt erstellt wurde. |
| `productName` | String | Der Name des Produkts. |
| `productRating` | String | Die Bewertung des Produkts durch den Kunden. |

{style="table-layout:auto"}

## Kompatible Feldergruppen {#field-groups}

Adobe bietet mehrere Standardfeldgruppen zur Verwendung mit der Klasse [!UICONTROL Product]. Im Folgenden finden Sie eine Liste einiger häufig verwendeter Feldergruppen für die Klasse:

* [[!UICONTROL Produktkatalog]](../field-groups/product/product-catalog.md)
* [[!UICONTROL Produktkategorie]](../field-groups/product/product-category.md)
