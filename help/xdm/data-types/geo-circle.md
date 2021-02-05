---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;Felder;Schemas;Schemas;Geo;Kreis;Datentyp;Datentyp;Datentyp;
solution: Experience Platform
title: Geo-Kreisdatentyp
topic: overview
description: Dieses Dokument bietet einen Überblick über den XDM-Datentyp für Geo Circle.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 23%

---


# [!UICONTROL Geo ] Circledata-Typ

[!UICONTROL Geo ] Circleis ist ein standardmäßiger XDM-Datentyp, der eine kreisförmige geografische Region beschreibt, wobei ein bestimmter Radius auf einem bestimmten Koordinatensatz zentriert ist. Dieser Datentyp basiert auf der in [Schema.org](http://schema.org/GeoCircle) dokumentierten öffentlichen Spezifikation.

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL Geo-Koordinaten]](./geo-coordinates.md) | Beschreibt die geografischen Koordinaten des Kreiszentrums. |
| `_schema.description` | Zeichenfolge | Eine Beschreibung, was der Kreis enthält. |
| `_schema.radius` | Double | Die Länge des Radius des Kreises. Dieser Wert entspricht dem [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/)-Datum und wird in Metern gemessen. |
| `_id` | Zeichenfolge | Eine eindeutige, systemgenerierte ID für den Kreis. |
