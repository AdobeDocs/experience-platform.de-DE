---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;Felder;Schemas;Schemas;Geo;Geo-Form;Datentyp;Datentyp;Datentyp;
solution: Experience Platform
title: Geo-Form-Datentyp
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über den XDM-Datentyp für Geo-Form.
exl-id: 50b9d783-a555-45eb-b154-7dc71389e224
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 36%

---

# [!UICONTROL Geo ] Shapedata-Typ

[!UICONTROL Geo ] Shapeis ist ein standardmäßiger XDM-Datentyp, der die Form eines geografischen Gebiets beschreibt. Dieser Datentyp basiert auf der in [Schema.org](https://schema.org/GeoShape) dokumentierten öffentlichen Spezifikation.

<img src="../images/data-types/geo-shape.png" width="500" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `_schema.box` | Array von [[!UICONTROL Geo-Koordinaten]](./geo-coordinates.md) | Beschreibt ein geografisches Gebiet, das von einem Rechteck umgeben ist, das aus zwei Koordinaten besteht. Die erste Koordinate ist die untere Ecke des Rechtecks und die zweite Koordinate die obere Ecke. |
| `_schema.circle` | Array von [[!UICONTROL Geo-Koordinaten]](./geo-coordinates.md) | Beschreibt einen kreisförmigen Bereich mit einem bestimmten Radius, der auf einer geografischen Koordinate zentriert ist. |
| `_schema.polygon` | [[!UICONTROL Geo-Kreis]](./geo-circle.md) | Eine Reihe von vier oder mehr Koordinaten, bei denen die ersten und letzten Koordinaten identisch sind. |
| `_schema.description` | Zeichenfolge | Eine Beschreibung, was die Form definiert. |
| `_schema.elevation` | Double | Die spezifische oder minimale Höhe der Form. Dieser Wert entspricht dem [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/)-Datum und wird in Metern gemessen. In Kombination mit `ceiling` kann mit dieser Eigenschaft ein dreidimensionaler Begrenzungsrahmen für eine Position angegeben werden. |
| `_id` | Zeichenfolge | Ein eindeutiger, systemgenerierter Bezeichner für die Form. |
| `ceiling` | Dublette | Die maximale Höhe der Form. Diese Eigenschaft ist nur gültig, wenn sie in Kombination mit `elevation` verwendet wird. Der Wert entspricht dem [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/)-Datum und wird in Metern gemessen. In Kombination mit `elevation` kann mit dieser Eigenschaft ein dreidimensionaler Begrenzungsrahmen für eine Position angegeben werden. |
