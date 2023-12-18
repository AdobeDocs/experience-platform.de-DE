---
title: Datentyp "Interne Site-Suche"
description: Erfahren Sie mehr über den XDM-Datentyp "Interne Site-Suche".
exl-id: 3cab9445-f641-4a44-9699-cd8a62da8a61
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 3%

---

# [!UICONTROL Interne Site-Suche] Datentyp

[!UICONTROL Interne Site-Suche] ist ein standardmäßiger XDM-Datentyp, der eine interne Site-Suche beschreibt, einschließlich aller zugehörigen Suchverhaltensweisen und -details.

![](../images/data-types/internal-site-search.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `autoCompleteClicked` | [!UICONTROL Boolesch] | Gibt an, ob ein Besucher einen vorgeschlagenen oder automatisch ausgefüllten Suchwert zur Ausführung der Suche verwendet hat. |
| `autoCompleteTypedValue` | [!UICONTROL String] | In Szenarien mit automatischem Vervollständigen verlassen Benutzer manchmal die Suche und wählen einen bestimmten Begriff aus der Dropdown-Liste aus. Mit diesem Wert wird verfolgt, was der Benutzer eingegeben hat, um den spezifischen Satz der vorgeschlagenen Suchbegriffe zu generieren. |
| `autoCompleteValue` | [!UICONTROL String] | In Fällen, in denen die Suche automatisch abgeschlossen wird, verlassen Benutzer manchmal die Suche und wählen einen bestimmten Begriff aus dem Dropdown-Menü aus. Dieser Wert wird verwendet, um die ausgewählten Begriffe zu verfolgen. |
| `instances` | [!UICONTROL Ganzzahl] | Die Häufigkeit, mit der die interne Site-Suche stattgefunden hat. |
| `locationInPage` | [!UICONTROL String] | Wenn mehrere Suchfelder auf der Seite vorhanden sind, sollte dieser Wert verwendet werden, um die spezifische Position zu identifizieren, die der Benutzer für die Suche verwendet hat. |
| `nullInstances` | [!UICONTROL Ganzzahl] | Die Häufigkeit, mit der die interne Site-Suche durchgeführt wurde und Nullergebnisse angezeigt wurden. |
| `numberOfResults` | [!UICONTROL Ganzzahl] | Die Gesamtzahl der zurückgegebenen Suchergebnisse. |
| `postalCode` | [!UICONTROL String] | Die für die Suche verwendete Postleitzahl, sofern zutreffend. |
| `productFindingMethods` | [!UICONTROL String] | Der interne Site-Suchbegriffwert mit Merchandising-Bindung. Dieser Wert gibt an, nach welchem Begriff unmittelbar vor der Anzeige eines Produkts gesucht wurde. |
| `radiusDistance` | [!UICONTROL Ganzzahl] | Kombiniert mit `radiusType`, zeigt den ausgewählten Abstand des Suchradius an. |
| `radiusType` | [!UICONTROL Ganzzahl] | Der ausgewählte Entfernungstyp von `radiusDistance`, entweder Meilen oder Kilometer. |
| `refinementInstances` | [!UICONTROL Ganzzahl] | Die Häufigkeit, mit der die interne Site-Suche optimiert wurde. |
| `refinementType` | Zeichenfolgen-Array | Listet die auf die Suchergebnisse angewendeten Verfeinerungstypen auf. Beispiele sind Abteilung, Marke, Preis, In-Store, Bewertungsbewertung, Farbe, Material usw. |
| `refinementValue` | [!UICONTROL String] | Der Wert, auf den die Suche optimiert wurde. |
| `resultsPageNumber` | [!UICONTROL Ganzzahl] | Bei paginierten Suchergebnissen verfolgt dieser Wert die Ergebnisseite, die der Besucher anzeigt. |
| `resultsPerPage` | [!UICONTROL Ganzzahl] | Bei paginierten Suchergebnissen verfolgt dieser Wert die Anzahl der pro Seite angezeigten Suchergebnisse. |
| `searchType` | [!UICONTROL String] | Erfasst gegebenenfalls die Methode der ausgeführten Suche. Beispiele sind eine vorausschauende Suche, eine direkt eingegebene Suche oder andere benutzerdefinierte Suchfunktionen, die eine Site möglicherweise aufweist. |
| `sortOrder` | [!UICONTROL String] | Kombiniert mit `sortType`, gibt die Sortierreihenfolge der Suchergebnisse an (aufsteigend oder absteigend). |
| `term` | [!UICONTROL String] | Der vom Besucher eingegebene interne Site-Suchbegriff. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im Abschnitt [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/internal-site-search.schema.json).
