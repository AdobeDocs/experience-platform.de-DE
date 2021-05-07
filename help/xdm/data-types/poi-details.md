---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;Felder;Schemas;Schemas;Poi;Poi-Details;Point-of-Interest;Point-of-Interest;Datentyp;Datentyp;
solution: Experience Platform
title: Datentyp "Point-Interest-Details"
topic-legacy: overview
description: Dieses Dokument bietet eine Übersicht über den XDM-Datentyp "Point of Interest Details".
exl-id: cab5463b-97a0-400d-a00c-0cd8bf9301a5
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 13%

---

# [!UICONTROL Point-Interest-] Detaildatentyp

[!UICONTROL Point-of-Interest-] Details bilden einen Standard-XDM-Datentyp, der die geografischen Daten beschreibt, in denen ein Ereignis beobachtet wurde.

<img src="../images/data-types/poi-details.png" width="550" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `beaconInteractionDetails` | [[!UICONTROL Beacon]](./beacon.md) | Beschreibt die für die POI-Interaktion aktiven Beacon-Details. |
| `geoInteractionDetails` | [[!UICONTROL Details zur Geo-Interaktion]](./geo-interaction-details.md) | Beschreibt die geografischen Details, die für die POI-Interaktion aktiv sind. |
| `category` | Zeichenfolge | Eine allgemeine Kategorie, die vom Administrator der POI-Definitionen für die Organisation der POIs zugewiesen wurde. |
| `distanceToPOICenter` | Double | Die geschätzte Entfernung vom POI-Zentrum in Metern. |
| `locatingType` | Zeichenfolge | Der Mechanismus zur Bestimmung des Standorts. Zu den zulässigen Werten gehören: <ul><li>`beacon`</li><li>`gps`</li><li>`ip`</li><li>`ip+wifi`</li><li>`wifi-triangulation`</li></ul> |
| `name` | Zeichenfolge | Ein Name, der der POI gegeben wird. |
| `poiID` | Zeichenfolge | Eine eindeutige Kennung des POI. |
| `type` | Zeichenfolge | Der allgemeine Typ des POI unter Verwendung eines vom Administrator der POI-Definitionen ausgewählten Typisierungsschemas. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json)
