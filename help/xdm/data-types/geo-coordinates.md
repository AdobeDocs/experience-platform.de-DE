---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;Felder;Schemas;Schemas;Geo;Koordinaten;Datentyp;Datentyp;Datentyp
solution: Experience Platform
title: Datentyp "Geo-Koordinaten"
topic-legacy: overview
description: Dieses Dokument bietet eine Übersicht über den XDM-Datentyp "Geo-Koordinaten".
exl-id: 3c80eb44-852f-4a95-bd13-b6197ffe62da
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 15%

---

# [!UICONTROL Geo-] KoordinatenDatentyp

[!UICONTROL Geo-] Koordinate ist ein standardmäßiger XDM-Datentyp, der die geografischen Koordinaten eines Orts beschreibt. Dieser Datentyp basiert auf der in [Schema.org](https://schema.org/GeoCoordinates) dokumentierten öffentlichen Spezifikation.

<img src="../images/data-types/geo-coordinates.png" width="400" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `_schema.description` | Zeichenfolge | Eine Beschreibung dessen, was die Koordinaten identifizieren. |
| `_schema.elevation` | Double | Die spezifische Höhe der definierten Koordinate. Der Wert muss dem [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/)-Datum entsprechen und in Metern gemessen werden. |
| `_schema.latitude` | Dublette | Die signierte vertikale Koordinate des geografischen Punkts. |
| `_schema.longitude` | Dublette | Die unterzeichnete horizontale Koordinate des geografischen Punkts. |
| `_id` | Zeichenfolge | Eine eindeutige, systemgenerierte ID für die Koordinaten. |
