---
title: Datenerfassungstyp für Fehlerdetails
description: Erfahren Sie mehr über den Datentyp "Error Details Collection Experience Data Model (XDM)".
source-git-commit: 899c656a7295896b291ac5c80df873711bc6f149
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 9%

---

# [!UICONTROL Fehlerdetails] Sammlungsdatentyp

[!UICONTROL Fehlerdetails] Die Sammlung ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Fehlerdetails beschreibt. Verwenden Sie die [!UICONTROL Fehlerdetails] Sammlungsdatentyp zum Erfassen von Details für die Fehlerquelle und die Identifizierung. Die Fehler-ID identifiziert den Fehler und die Fehlerquelle gibt an, ob er aus dem Player oder einer externen Quelle stammt.

![Ein Diagramm des Datentyps Fehlerdetails .](../images/data-types/error-details-collection.png)

| Anzeigename | Eigenschaft | Datentyp | Erforderlich | Beschreibung |
|----------------------------|--------------|-----------|----------|-----------------------------------------------|
| [!UICONTROL Fehler-ID] | `name` | Zeichenfolge | Nein | Die Fehler-ID. |
| [!UICONTROL Fehlerquelle] | `source` | Zeichenfolge | Nein | Die Fehlerquelle. Aufzählung: &quot;player&quot;, &quot;external&quot; mit der entsprechenden Bedeutung. |

{style="table-layout:auto"}
