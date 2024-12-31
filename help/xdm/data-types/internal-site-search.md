---
title: Datentyp der internen Site-Suche
description: Erfahren Sie mehr über den XDM-Datentyp „Interne Site-Suche“.
exl-id: 3cab9445-f641-4a44-9699-cd8a62da8a61
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 3%

---

# [!UICONTROL Interne Site-Suche] Datentyp

[!UICONTROL Interne Site-Suche] ist ein standardmäßiger XDM-Datentyp, der eine interne Site-Suche beschreibt, einschließlich aller zugehörigen Suchverhaltensweisen und Details.

![](../images/data-types/internal-site-search.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `autoCompleteClicked` | [!UICONTROL Boolesch] | Gibt an, ob ein Besucher einen vorgeschlagenen oder automatisch vervollständigten Suchwert verwendet hat, um die Suche auszuführen. |
| `autoCompleteTypedValue` | [!UICONTROL String] | Bei Szenarien mit automatischer Vervollständigung brechen Benutzer manchmal ihre Suche ab und wählen einen bestimmten Begriff aus dem Dropdown-Menü aus. Dieser Wert verfolgt, was Benutzende zu tippen begonnen haben, um den spezifischen Satz empfohlener Suchbegriffe zu generieren. |
| `autoCompleteValue` | [!UICONTROL String] | Bei Szenarien mit automatischer Vervollständigung brechen Benutzer manchmal ihre Suche ab und wählen einen bestimmten Begriff aus dem Dropdown-Menü aus. Dieser Wert wird verwendet, um die ausgewählten spezifischen Begriffe zu verfolgen. |
| `instances` | [!UICONTROL Integer] | Die Häufigkeit, mit der die interne Site-Suche stattgefunden hat. |
| `locationInPage` | [!UICONTROL String] | Wenn mehrere Suchfelder auf der Seite vorhanden sind, sollte dieser Wert verwendet werden, um die spezifische Position zu identifizieren, die der Benutzer zum Suchen verwendet hat. |
| `nullInstances` | [!UICONTROL Integer] | Die Häufigkeit, mit der die interne Site-Suche stattgefunden hat, die null Ergebnisse lieferte. |
| `numberOfResults` | [!UICONTROL Integer] | Die Gesamtzahl der zurückgegebenen Suchergebnisse. |
| `postalCode` | [!UICONTROL String] | Die für die Suche verwendete Postleitzahl, falls zutreffend. |
| `productFindingMethods` | [!UICONTROL String] | Der Wert des internen Site-Suchbegriffs mit Merchandising-Bindung. Dieser Wert gibt an, nach welchem Begriff unmittelbar vor der Anzeige eines Produkts gesucht wurde. |
| `radiusDistance` | [!UICONTROL Integer] | Kombiniert mit `radiusType` zeigt die ausgewählte Entfernung des Suchradius an. |
| `radiusType` | [!UICONTROL Integer] | Der ausgewählte Entfernungstyp von `radiusDistance`, entweder Meilen oder Kilometer. |
| `refinementInstances` | [!UICONTROL Integer] | Die Häufigkeit, mit der die interne Site-Suche verfeinert wurde. |
| `refinementType` | Zeichenfolgen-Array | Listet die Verfeinerungstypen auf, die auf die Suchergebnisse angewendet wurden. Beispiele sind Abteilung, Marke, Preis, In-Store, Bewertung, Farbe, Material usw. |
| `refinementValue` | [!UICONTROL String] | Der Wert, auf den die Suche verfeinert wurde. |
| `resultsPageNumber` | [!UICONTROL Integer] | Bei paginierten Suchergebnissen verfolgt dieser Wert die Ergebnisseite, die der Besucher anzeigt. |
| `resultsPerPage` | [!UICONTROL Integer] | Bei paginierten Suchergebnissen verfolgt dieser Wert die Anzahl der pro Seite angezeigten Suchergebnisse. |
| `searchType` | [!UICONTROL String] | Erfasst die Methode der ausgeführten Suche, falls zutreffend. Beispiele sind eine Suche mit automatischer Textvervollständigung, eine direkt eingegebene Suche oder jede andere Art von benutzerdefinierter Suchfunktion, über die eine Site verfügen könnte. |
| `sortOrder` | [!UICONTROL String] | Kombiniert mit `sortType` gibt die Sortierreihenfolge der Suchergebnisse an, entweder aufsteigend oder absteigend. |
| `term` | [!UICONTROL String] | Der vom Besucher eingegebene interne Site-Suchbegriff. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie unter [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/internal-site-search.schema.json).
