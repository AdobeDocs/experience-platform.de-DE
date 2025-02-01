---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;Felder;Schemata;Schemata;Geo;Geo-Form;Datentyp;Datentyp;Datentyp;
solution: Experience Platform
title: Geo-Shape-Datentyp
description: Erfahren Sie mehr über den XDM-Datentyp Geo-Form .
exl-id: 50b9d783-a555-45eb-b154-7dc71389e224
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 31%

---

# [!UICONTROL Geo-Form] Datentyp

[!UICONTROL Geo-Form] ist ein standardmäßiger XDM-Datentyp, der die Form eines geografischen Gebiets beschreibt. Dieser Datentyp basiert auf der öffentlichen Spezifikation, die in [schema.org](https://schema.org/GeoShape) dokumentiert ist.

![](../images/data-types/geo-shape.png){width=500}

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `_schema.box` | Array von [[!UICONTROL Geo-Koordinaten]](./geo-coordinates.md) | Beschreibt ein geografisches Gebiet, das von einem Rechteck umgeben ist, das aus zwei Koordinaten gebildet wird. Die erste Koordinate ist die untere Ecke des Rechtecks und die zweite Koordinate die obere Ecke. |
| `_schema.circle` | Array von [[!UICONTROL Geo-Koordinaten]](./geo-coordinates.md) | Beschreibt einen kreisförmigen Bereich mit einem bestimmten Radius, der auf einer geografischen Koordinate zentriert ist. |
| `_schema.polygon` | [[!UICONTROL Geo-Kreis]](./geo-circle.md) | Eine Reihe von vier oder mehr Koordinaten, bei denen die ersten und letzten Koordinaten identisch sind. |
| `_schema.description` | String | Eine Beschreibung dessen, was die Form definiert. |
| `_schema.elevation` | Double | Die spezifische oder minimale Höhe der Form. Dieser Wert entspricht dem [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/)-Datum und wird in Metern gemessen. In Kombination mit `ceiling` kann mit dieser Eigenschaft ein dreidimensionaler Begrenzungsrahmen für eine Position angegeben werden. |
| `_id` | String | Eine eindeutige, systemgenerierte Kennung für die Form. |
| `ceiling` | Double | Die maximale Höhe der Form. Diese Eigenschaft ist nur gültig, wenn sie in Kombination mit `elevation` verwendet wird. Der Wert entspricht dem [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/)-Datum und wird in Metern gemessen. In Kombination mit `elevation` kann mit dieser Eigenschaft ein dreidimensionaler Begrenzungsrahmen für eine Position angegeben werden. |
