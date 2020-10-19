---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;geo;circle;datatype;data-type;data type;
solution: Experience Platform
title: Geo Circle-Datentyp
topic: overview
description: Dieses Dokument bietet einen Überblick über den XDM-Datentyp für Geo Circle.
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 26%

---


# [!UICONTROL Geo Circle] -Datentyp

[!UICONTROL Geo Circle] ist ein standardmäßiger XDM-Datentyp, der eine kreisförmige geografische Region beschreibt, sofern ein bestimmter Radius auf einem bestimmten Satz von Koordinaten zentriert ist. Dieser Datentyp basiert auf der in [Schema.org](http://schema.org/GeoCircle)dokumentierten öffentlichen Spezifikation.

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL Geo-Koordinaten]](./geo-coordinates.md) | Beschreibt die geografischen Koordinaten des Kreiszentrums. |
| `_schema.description` | Zeichenfolge | Eine Beschreibung, was der Kreis enthält. |
| `_schema.radius` | Double | Die Länge des Radius des Kreises. Dieser Wert entspricht dem [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/)-Datum und wird in Metern gemessen. |
| `_id` | Zeichenfolge | Eine eindeutige, systemgenerierte ID für den Kreis. |
