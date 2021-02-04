---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;Felder;Schemas;Schemas;Beacon;Interaktionsdetails;Datentyp;Datentyp;Datentyp;
solution: Experience Platform
title: Datentyp für Geo-Interaktionsdetails
topic: overview
description: Dieses Dokument bietet eine Übersicht über den XDM-Datentyp für Geo-Interaktionsdetails.
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 5%

---


# [!UICONTROL Datentyp ] der Geo-Interaktion

[!UICONTROL Geo-Interaktionsdetails ] sind ein standardmäßiger XDM-Datentyp, der den aktuellen Aufnahmezustand in einem geografisch definierten Bereich beschreibt.

<img src="../images/data-types/geo-interaction-details.png" width="400" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL Geo-Form]](./geo-shape.md) | Beschreibt die geografische Form des Bereichs, mit dem interagiert wird. Dieses Feld kann ein Feld, einen Kreis oder ein Polygon beschreiben. |
| `deviceGeoAccuracy` | Double | Die Genauigkeit des Geo-Messgeräts oder -Mechanismus, gemessen in Metern. |
| `distanceToCenter` | Dublette | Der Abstand zum Zentrum des Geo bei einem Geo-Kreis, gemessen in Metern. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)
