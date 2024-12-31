---
title: Datentyp der Fehlerdetailsammlung
description: Erfahren Sie mehr über den Datentyp „Error Details Collection Experience Data Model (XDM)“.
exl-id: 54b03147-9bca-46af-86c8-90e42b4de26b
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 12%

---

# [!UICONTROL Fehlerdetails] Sammlungsdatentyp

[!UICONTROL Fehlerdetails] Die Sammlung ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Fehlerdetails beschreibt. Verwenden Sie den Datentyp [!UICONTROL Fehlerdetails] Sammlung, um Details zur Fehlerquelle und -identifizierung zu erfassen. Die Fehler-ID identifiziert den Fehler und die Fehlerquelle gibt an, ob er vom Player oder einer externen Quelle stammt.

![Abbildung des Datentyps für Fehlerdetails.](../images/data-types/error-details-collection.png)

| Anzeigename | Eigenschaft | Datentyp | Erforderlich | Beschreibung |
|----------------------------|--------------|-----------|----------|-----------------------------------------------|
| [!UICONTROL Fehler-ID] | `name` | Zeichenfolge | Nein | Die Fehler-ID. |
| [!UICONTROL Fehler Source] | `source` | Zeichenfolge | Nein | Die Fehlerquelle. Aufgezählt: „player“, „external“ mit jeweiligen Bedeutungen. |

{style="table-layout:auto"}
