---
title: Datentyp mit Fehlerdetails
description: Erfahren Sie mehr über den Datentyp Erlebnis-Datenmodell (XDM) mit Fehlerdetails.
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 7%

---

# [!UICONTROL Informationen zu Fehlerdetails] Datentyp

[!UICONTROL Informationen zu Fehlerdetails] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Fehlerdetails beschreibt. Verwenden Sie die [!UICONTROL Informationen zu Fehlerdetails] Datentyp zum Erfassen von Details zur Fehlerquelle und Identifizierung. Die Fehler-ID identifiziert den Fehler und die Fehlerquelle gibt an, ob er aus dem Player oder einer externen Quelle stammt.

![Ein Diagramm des Datentyps Fehlerdetails .](../images/data-types/error-details-information.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|----------------|----------------|-----------|----------------------------------------------|
| [!UICONTROL Fehler-ID] | `name` | Zeichenfolge | Die Fehler-ID. |
| [!UICONTROL Fehlerquelle] | `source` | Zeichenfolge | Die Fehlerquelle. Aufzählung: &quot;player&quot;, &quot;external&quot; mit der entsprechenden Bedeutung. |

{style="table-layout:auto"}

Weiterführende Informationen zur Feldergruppe finden Sie im Abschnitt [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json)
