---
keywords: Experience Platform; home; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Geo; Koordinaten; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Datentyp "Geo-Koordinaten"
description: Erfahren Sie mehr über den XDM-Datentyp "Geo-Koordinaten".
exl-id: 3c80eb44-852f-4a95-bd13-b6197ffe62da
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 13%

---

# [!UICONTROL Geo-Koordinaten] Datentyp

[!UICONTROL Geo-Koordinaten] ist ein standardmäßiger XDM-Datentyp, der die geografischen Koordinaten eines Orts beschreibt. Dieser Datentyp basiert auf der öffentlichen Spezifikation, die dokumentiert ist unter [schema.org](https://schema.org/GeoCoordinates).

<img src="../images/data-types/geo-coordinates.png" width="400" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `_schema.description` | Zeichenfolge | Eine Beschreibung dessen, was die Koordinaten identifizieren. |
| `_schema.elevation` | Double | Die spezifische Höhe der definierten Koordinate. Der Wert muss mit der Variablen [WGS 84](https://gisgeography.com/wgs84-world-geodetic-system/) Datum und wird in Metern gemessen. |
| `_schema.latitude` | Double | Die vorzeichenbehaftete vertikale Koordinate des geografischen Punkts. |
| `_schema.longitude` | Double | Die vorzeichenbehaftete horizontale Koordinate des geografischen Punkts. |
| `_id` | Zeichenfolge | Eine eindeutige, systemgenerierte ID für die Koordinaten. |
