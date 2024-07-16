---
keywords: Experience Platform; home; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Geo; Geo-Form; Datentyp; Datentyp; Datentyp
solution: Experience Platform
title: Geo-Form-Datentyp
description: Erfahren Sie mehr über den XDM-Datentyp "Geo-Form".
exl-id: 50b9d783-a555-45eb-b154-7dc71389e224
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 31%

---

# Datentyp [!UICONTROL Geo-Form]

[!UICONTROL Geo-Form] ist ein standardmäßiger XDM-Datentyp, der die Form eines geografischen Gebiets beschreibt. Dieser Datentyp basiert auf der öffentlichen Spezifikation, die in [schema.org](https://schema.org/GeoShape) dokumentiert ist.

<img src="../images/data-types/geo-shape.png" width="500" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `_schema.box` | Array von [[!UICONTROL Geo-Koordinaten]](./geo-coordinates.md) | Beschreibt ein geografisches Gebiet, das von einem durch zwei Koordinaten gebildeten Rechteck eingeschlossen ist. Die erste Koordinate ist die untere Ecke des Rechtecks und die zweite Koordinate die obere Ecke. |
| `_schema.circle` | Array von [[!UICONTROL Geo-Koordinaten]](./geo-coordinates.md) | Beschreibt einen kreisförmigen Bereich mit einem bestimmten Radius, der auf einer geografischen Koordinate zentriert ist. |
| `_schema.polygon` | [[!UICONTROL Geo-Kreis]](./geo-circle.md) | Eine Reihe von vier oder mehr Koordinaten, bei denen die ersten und letzten Koordinaten identisch sind. |
| `_schema.description` | Zeichenfolge | Eine Beschreibung dessen, was die Form definiert. |
| `_schema.elevation` | Double | Die spezifische oder minimale Höhe der Form. Dieser Wert entspricht dem [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/)-Datum und wird in Metern gemessen. In Kombination mit `ceiling` kann mit dieser Eigenschaft ein dreidimensionaler Begrenzungsrahmen für eine Position angegeben werden. |
| `_id` | Zeichenfolge | Eine eindeutige, systemgenerierte Kennung für die Form. |
| `ceiling` | Double | Die maximale Höhe der Form. Diese Eigenschaft ist nur gültig, wenn sie in Kombination mit `elevation` verwendet wird. Der Wert entspricht dem [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) -Datum und wird in Metern gemessen. In Kombination mit `elevation` kann mit dieser Eigenschaft ein dreidimensionaler Begrenzungsrahmen für eine Position angegeben werden. |
