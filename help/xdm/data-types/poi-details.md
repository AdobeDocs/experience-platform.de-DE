---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;Felder;Schemata;Schemata;Schemata;poi;POI-Details;Point of Interest;Point of Interest-Details;Datentyp;Datentyp;
solution: Experience Platform
title: Datentyp „Point of Interest-Details“
description: Erfahren Sie mehr über den XDM-Datentyp „Point of Interest“.
exl-id: cab5463b-97a0-400d-a00c-0cd8bf9301a5
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 16%

---

# [!UICONTROL Details zum Point of Interest]-Datentyp

[!UICONTROL Point of Interest-Details] ist ein standardmäßiger XDM-Datentyp, der die geografischen Daten beschreibt, in denen ein Ereignis beobachtet wurde.

<img src="../images/data-types/poi-details.png" width="550" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `beaconInteractionDetails` | [[!UICONTROL Beacon]](./beacon.md) | Beschreibt die Beacon-Details, die für die POI-Interaktion aktiv sind. |
| `geoInteractionDetails` | [[!UICONTROL Details zur Geo-Interaktion]](./geo-interaction-details.md) | Beschreibt die für die POI-Interaktion aktiven geografischen Details. |
| `category` | String | Eine allgemeine Kategorie, die vom Administrator der POI-Definitionen für die Organisation der POIs zugewiesen wurde. |
| `distanceToPOICenter` | Double | Die geschätzte Entfernung vom POI-Mittelpunkt in Metern. |
| `locatingType` | String | Der Mechanismus zur Standortbestimmung. Zu den akzeptierten Werten gehören: <ul><li>`beacon`</li><li>`gps`</li><li>`ip`</li><li>`ip+wifi`</li><li>`wifi-triangulation`</li></ul> |
| `name` | String | Ein Name für den POI. |
| `poiID` | String | Eine eindeutige Kennung des POI. |
| `type` | String | Der allgemeine Typ des POI unter Verwendung eines vom Administrator der POI-Definitionen ausgewählten Typisierungsschemas. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json)
