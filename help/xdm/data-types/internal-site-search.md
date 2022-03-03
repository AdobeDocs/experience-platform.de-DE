---
title: Datentyp "Interne Site-Suche"
description: Dieses Dokument bietet einen Überblick über den XDM-Datentyp "Interne Site-Suche".
source-git-commit: eaea904ddda6b7ffee6f52cd4af897c2a8885714
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 6%

---

# [!UICONTROL Interne Site-Suche] Datentyp

[!UICONTROL Interne Site-Suche] ist ein standardmäßiger XDM-Datentyp, der eine interne Site-Suche beschreibt, einschließlich aller zugehörigen Suchverhaltensweisen und -details.

![](../images/data-types/internal-site-search.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `autoCompleteClicked` | [!UICONTROL Boolesch] | Gibt an, ob ein Besucher einen vorgeschlagenen oder automatisch ausgefüllten Suchwert verwendet hat, um die Suche auszuführen. |
| `autoCompleteTypedValue` | [!UICONTROL Zeichenfolge] | In Fällen, in denen die Suche automatisch abgeschlossen wird, verlassen Benutzer manchmal die Suche und wählen einen bestimmten Begriff aus der Dropdown-Liste aus. Mit diesem Wert wird verfolgt, was der Benutzer eingegeben hat, um den spezifischen Satz der vorgeschlagenen Suchbegriffe zu generieren. |
| `autoCompleteValue` | [!UICONTROL Zeichenfolge] | In Fällen, in denen die Suche automatisch abgeschlossen wird, verlassen Benutzer manchmal die Suche und wählen einen bestimmten Begriff aus dem Dropdown-Menü aus. Dieser Wert wird verwendet, um die ausgewählten Begriffe zu verfolgen. |
| `instances` | [!UICONTROL Ganzzahl] | Die Häufigkeit, mit der die interne Site-Suche stattgefunden hat. |
| `locationInPage` | [!UICONTROL Zeichenfolge] | Wenn mehrere Suchfelder auf der Seite vorhanden sind, sollte dieser Wert verwendet werden, um die spezifische Position zu identifizieren, die der Benutzer für die Suche verwendet hat. |
| `nullInstances` | [!UICONTROL Ganzzahl] | Die Häufigkeit, mit der die interne Site-Suche durchgeführt wurde und Nullergebnisse angezeigt wurden. |
| `numberOfResults` | [!UICONTROL Ganzzahl] | Die Gesamtzahl der zurückgegebenen Suchergebnisse. |
| `postalCode` | [!UICONTROL Zeichenfolge] | Die für die Suche verwendete Postleitzahl, sofern zutreffend. |
| `productFindingMethods` | [!UICONTROL Zeichenfolge] | Der interne Site-Suchbegriffwert mit Merchandising-Bindung. Dieser Wert gibt an, nach welchem Begriff unmittelbar vor der Anzeige eines Produkts gesucht wurde. |
| `radiusDistance` | [!UICONTROL Ganzzahl] | Kombiniert mit `radiusType`, zeigt den ausgewählten Abstand des Suchradius an. |
| `radiusType` | [!UICONTROL Ganzzahl] | Der ausgewählte Entfernungstyp von `radiusDistance`, entweder Meilen oder Kilometer. |
| `refinementInstances` | [!UICONTROL Ganzzahl] | Die Häufigkeit, mit der die interne Site-Suche optimiert wurde. |
| `refinementType` | Zeichenfolgen-Array | Listet die auf die Suchergebnisse angewendeten Verfeinerungstypen auf. Beispiele sind Abteilung, Marke, Preis, In-Store, Bewertungsbewertung, Farbe, Material usw. |
| `refinementValue` | [!UICONTROL Zeichenfolge] | Der Wert, auf den die Suche optimiert wurde. |
| `resultsPageNumber` | [!UICONTROL Ganzzahl] | Bei paginierten Suchergebnissen verfolgt dieser Wert die Ergebnisseite, die der Besucher anzeigt. |
| `resultsPerPage` | [!UICONTROL Ganzzahl] | Bei paginierten Suchergebnissen verfolgt dieser Wert die Anzahl der pro Seite angezeigten Suchergebnisse. |
| `searchType` | [!UICONTROL Zeichenfolge] | Erfasst gegebenenfalls die Methode der ausgeführten Suche. Beispiele sind eine vorausschauende Suche, eine direkt eingegebene Suche oder andere benutzerdefinierte Suchfunktionen, die eine Site möglicherweise aufweist. |
| `sortOrder` | [!UICONTROL Zeichenfolge] | Kombiniert mit `sortType`, gibt die Sortierreihenfolge der Suchergebnisse an (aufsteigend oder absteigend). |
| `term` | [!UICONTROL Zeichenfolge] | Der vom Besucher eingegebene interne Site-Suchbegriff. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zum Datentyp finden Sie im Abschnitt [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/internal-site-search.schema.json).
