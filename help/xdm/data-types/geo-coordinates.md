---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;Felder;Schemata;Schemata;Geo;Koordinaten;Datentyp;Datentyp;Datentyp;
solution: Experience Platform
title: Datentyp Geokoordinaten
description: Erfahren Sie mehr über den XDM-Datentyp Geokoordinaten .
exl-id: 3c80eb44-852f-4a95-bd13-b6197ffe62da
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 12%

---

# [!UICONTROL Geokoordinaten] Datentyp

[!UICONTROL Geokoordinaten] ist ein standardmäßiger XDM-Datentyp, der die geografischen Koordinaten eines Ortes beschreibt. Dieser Datentyp basiert auf der öffentlichen Spezifikation, die in [schema.org](https://schema.org/GeoCoordinates) dokumentiert ist.

![](../images/data-types/geo-coordinates.png){width=400}

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `_schema.description` | Zeichenfolge | Eine Beschreibung dessen, was die Koordinaten identifizieren. |
| `_schema.elevation` | Double | Die spezifische Höhe der definierten Koordinate. Der Wert muss mit dem [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/)-Datum übereinstimmen und wird in Metern gemessen. |
| `_schema.latitude` | Double | Die vorzeichenbehaftete vertikale Koordinate des geografischen Punkts. |
| `_schema.longitude` | Double | Die vorzeichenbehaftete horizontale Koordinate des geografischen Punkts. |
| `_id` | String | Eine eindeutige, systemgenerierte ID für die Koordinaten. |
