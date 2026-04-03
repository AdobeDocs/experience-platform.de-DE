---
title: Datentyp der Fehlerdetailsammlung
description: Erfahren Sie mehr über den Datentyp „Error Details Collection Experience Data Model (XDM)“.
exl-id: 54b03147-9bca-46af-86c8-90e42b4de26b
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 10%

---

# Datentyp der [!UICONTROL Error Details]

[!UICONTROL Error Details] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Fehlerdetails beschreibt. Verwenden Sie den Datentyp &quot;[!UICONTROL Error Details] Collection“, um Details zur Fehlerquelle und -identifizierung zu erfassen. Die Fehler-ID identifiziert den Fehler und die Fehlerquelle gibt an, ob er vom Player oder einer externen Quelle stammt.

![Abbildung des Datentyps für Fehlerdetails.](../images/data-types/error-details-collection.png)

| Anzeigename | Eigenschaft | Datentyp | Erforderlich | Beschreibung |
|----------------------------|--------------|-----------|----------|-----------------------------------------------|
| [!UICONTROL Error ID] | `name` | string | Nein | Die Fehler-ID. |
| [!UICONTROL Error Source] | `source` | string | Nein | Die Fehlerquelle. Aufgezählt: „player“, „external“ mit jeweiligen Bedeutungen. |

{style="table-layout:auto"}
