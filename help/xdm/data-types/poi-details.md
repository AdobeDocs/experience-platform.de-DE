---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; POI; POI-Details; POI-Details; POI-Details; Point-of-Interest-Details; Datentyp; Datentyp;
solution: Experience Platform
title: Datentyp "Point of Interest Details"
description: Dieses Dokument bietet einen Überblick über den XDM-Datentyp "Point of Interest Details".
exl-id: cab5463b-97a0-400d-a00c-0cd8bf9301a5
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 26%

---

# [!UICONTROL Details zum POI] Datentyp

[!UICONTROL Details zum POI] ist ein standardmäßiger XDM-Datentyp, der die geografischen Daten beschreibt, in denen ein Ereignis beobachtet wurde.

<img src="../images/data-types/poi-details.png" width="550" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `beaconInteractionDetails` | [[!UICONTROL Beacon]](./beacon.md) | Beschreibt die Beacon-Details, die für die POI-Interaktion aktiv sind. |
| `geoInteractionDetails` | [[!UICONTROL Details zur Geo-Interaktion]](./geo-interaction-details.md) | Beschreibt die für die POI-Interaktion aktiven Geodetails. |
| `category` | Zeichenfolge | Eine allgemeine Kategorie, die vom Administrator der POI-Definitionen für die Organisation der POIs zugewiesen wurde. |
| `distanceToPOICenter` | Double | Die geschätzte Entfernung vom POI-Zentrum in Metern. |
| `locatingType` | Zeichenfolge | Der Mechanismus zur Bestimmung des Standorts. Zu den zulässigen Werten gehören: <ul><li>`beacon`</li><li>`gps`</li><li>`ip`</li><li>`ip+wifi`</li><li>`wifi-triangulation`</li></ul> |
| `name` | Zeichenfolge | Ein Name für den POI. |
| `poiID` | Zeichenfolge | Eine eindeutige Kennung des POI. |
| `type` | Zeichenfolge | Der allgemeine Typ des POI unter Verwendung eines vom Administrator der POI-Definitionen ausgewählten Typisierungsschemas. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json)
