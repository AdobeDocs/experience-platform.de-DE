---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;geo;coordinates;datatype;data-type;data type;
solution: Experience Platform
title: Datentyp "Geo-Koordinaten"
topic: overview
description: Dieses Dokument bietet eine Übersicht über den XDM-Datentyp "Geo-Koordinaten".
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 17%

---


# [!UICONTROL Datentyp &quot;Geo-Koordinaten] &quot;

[!UICONTROL Geo-Koordinaten] ist ein standardmäßiger XDM-Datentyp, der die geografischen Koordinaten eines Orts beschreibt. Dieser Datentyp basiert auf der in [Schema.org](https://schema.org/GeoCoordinates)dokumentierten öffentlichen Spezifikation.

<img src="../images/data-types/geo-coordinates.png" width="400" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `_schema.description` | Zeichenfolge | Eine Beschreibung dessen, was die Koordinaten identifizieren. |
| `_schema.elevation` | Double | Die spezifische Höhe der definierten Koordinate. The value must conform to the [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) datum and is measured in meters. |
| `_schema.latitude` | Double | Die signierte vertikale Koordinate des geografischen Punkts. |
| `_schema.longitude` | Double | Die unterzeichnete horizontale Koordinate des geografischen Punkts. |
| `_id` | Zeichenfolge | Eine eindeutige, systemgenerierte ID für die Koordinaten. |
