---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;Felder;Schemata;Schemata;Geo;Kreis;Datentyp;Datentyp;Datentyp;
solution: Experience Platform
title: Geo-Kreis-Datentyp
description: Erfahren Sie mehr über den XDM-Datentyp „Geo-Kreis“.
exl-id: fa041f4f-9955-44e9-b235-a643e07d402c
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 17%

---

# [!UICONTROL Geo-Kreis] Datentyp

[!UICONTROL Geo Circle] ist ein standardmäßiger XDM-Datentyp, der eine zirkuläre geografische Region beschreibt, wenn ein bestimmter Radius auf einen bestimmten Satz von Koordinaten zentriert ist. Dieser Datentyp basiert auf der öffentlichen Spezifikation, die in [schema.org](https://schema.org/GeoCircle) dokumentiert ist.

![](../images/data-types/geo-circle.png){width=400}

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL Geo-Koordinaten]](./geo-coordinates.md) | Beschreibt die geografischen Koordinaten des Zentrums des Kreises. |
| `_schema.description` | String | Eine Beschreibung dessen, was der Kreis enthält. |
| `_schema.radius` | Double | Die Länge des Radius des Kreises. Dieser Wert entspricht dem [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/)-Datum und wird in Metern gemessen. |
| `_id` | String | Eine eindeutige, systemgenerierte ID für den Kreis. |
