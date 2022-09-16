---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Geo; Kreis; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Geo-Kreis-Datentyp
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über den XDM-Datentyp "Geo Circle".
exl-id: fa041f4f-9955-44e9-b235-a643e07d402c
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 21%

---

# [!UICONTROL Geo-Kreis] Datentyp

[!UICONTROL Geo-Kreis] ist ein standardmäßiger XDM-Datentyp, der eine zirkuläre geografische Region beschreibt, mit einem bestimmten Radius, der auf einen bestimmten Koordinatensatz zentriert ist. Dieser Datentyp basiert auf der öffentlichen Spezifikation, die dokumentiert ist unter [schema.org](https://schema.org/GeoCircle).

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL Geo-Koordinaten]](./geo-coordinates.md) | Beschreibt die geografischen Koordinaten des Kreiszentrums. |
| `_schema.description` | Zeichenfolge | Eine Beschreibung dessen, was der Kreis enthält. |
| `_schema.radius` | Double | Die Länge des Radius des Kreises. Dieser Wert entspricht dem [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/)-Datum und wird in Metern gemessen. |
| `_id` | Zeichenfolge | Eine eindeutige, systemgenerierte ID für den Kreis. |
