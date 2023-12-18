---
keywords: Experience Platform; home; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Beacon; Interaktionsdetails; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Datentyp "Geo-Interaktionsdetails"
description: Erfahren Sie mehr über den XDM-Datentyp "Geo Interaction Details".
exl-id: c05b098b-3f12-4283-a6d5-5ebf96b9828d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 4%

---

# [!UICONTROL Details zur Geo-Interaktion] Datentyp

[!UICONTROL Details zur Geo-Interaktion] ist ein standardmäßiger XDM-Datentyp, der den aktuellen Aufnahmestatus in einem geografisch definierten Gebiet beschreibt.

<img src="../images/data-types/geo-interaction-details.png" width="400" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL Geo-Form]](./geo-shape.md) | Beschreibt die geografische Form des Bereichs, mit dem interagiert wird. In diesem Feld kann ein Feld, ein Kreis oder ein Polygon beschrieben werden. |
| `deviceGeoAccuracy` | Double | Die Genauigkeit des Geo-Messgeräts oder -Mechanismus, gemessen in Metern. |
| `distanceToCenter` | Double | Der Abstand zum Geo-Mittelpunkt bei einem Geo-Kreis, gemessen in Metern. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)
