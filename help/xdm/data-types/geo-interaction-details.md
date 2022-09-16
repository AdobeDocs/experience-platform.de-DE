---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Beacon; Interaktionsdetails; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Datentyp "Geo-Interaktionsdetails"
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über den XDM-Datentyp "Geo Interaction Details".
exl-id: c05b098b-3f12-4283-a6d5-5ebf96b9828d
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 15%

---

# [!UICONTROL Details zur Geo-Interaktion] Datentyp

[!UICONTROL Details zur Geo-Interaktion] ist ein standardmäßiger XDM-Datentyp, der den aktuellen Aufnahmestatus in einem geografisch definierten Gebiet beschreibt.

<img src="../images/data-types/geo-interaction-details.png" width="400" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL Geo-Form]](./geo-shape.md) | Beschreibt die geografische Form des Bereichs, mit dem interagiert wird. In diesem Feld kann ein Feld, ein Kreis oder ein Polygon beschrieben werden. |
| `deviceGeoAccuracy` | Double | Die Genauigkeit des Geo-Messgeräts oder -Mechanismus, gemessen in Metern. |
| `distanceToCenter` | Double | Der Abstand zum Geo-Mittelpunkt bei einem Geo-Kreis, gemessen in Metern. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)
