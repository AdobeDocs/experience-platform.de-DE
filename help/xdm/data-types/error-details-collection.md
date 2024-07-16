---
title: Datenerfassungstyp für Fehlerdetails
description: Erfahren Sie mehr über den Datentyp "Error Details Collection Experience Data Model (XDM)".
exl-id: 54b03147-9bca-46af-86c8-90e42b4de26b
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 12%

---

# [!UICONTROL Fehlerdetails] Sammlungsdatentyp

[!UICONTROL Fehlerdetails] Sammlung ist ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der Fehlerdetails beschreibt. Verwenden Sie den Sammlungstyp [!UICONTROL Fehlerdetails] , um Details zur Fehlerquelle und Identifizierung zu erfassen. Die Fehler-ID identifiziert den Fehler und die Fehlerquelle gibt an, ob er aus dem Player oder einer externen Quelle stammt.

![Ein Diagramm des Datentyps Fehlerdetails.](../images/data-types/error-details-collection.png)

| Anzeigename | Eigenschaft | Datentyp | Erforderlich | Beschreibung |
|----------------------------|--------------|-----------|----------|-----------------------------------------------|
| [!UICONTROL Fehler-ID] | `name` | Zeichenfolge | Nein | Die Fehler-ID. |
| [!UICONTROL Fehler-Source] | `source` | Zeichenfolge | Nein | Die Fehlerquelle. Aufzählung: &quot;player&quot;, &quot;external&quot; mit der entsprechenden Bedeutung. |

{style="table-layout:auto"}
