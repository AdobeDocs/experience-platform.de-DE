---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;Felder;Schemata;Schemata;Beacon;Interaktionsdetails;Datentyp;Datentyp;Datentyp;
solution: Experience Platform
title: Datentyp Geo Interaction-Details
description: Erfahren Sie mehr über den XDM-Datentyp „Geo Interaction Details“.
exl-id: c05b098b-3f12-4283-a6d5-5ebf96b9828d
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 13%

---

# [!UICONTROL Geo-Interaktionsdetails] Datentyp

[!UICONTROL Geo-Interaktionsdetails] ist ein standardmäßiger XDM-Datentyp, der den aktuellen Status der Einbeziehung in einem geografisch definierten Bereich beschreibt.

![](../images/data-types/geo-interaction-details.png){width=400}

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL Geo-Form]](./geo-shape.md) | Beschreibt die Geo-Form des Bereichs, mit dem interagiert wird. Dieses Feld kann eine Box, einen Kreis oder ein Polygon beschreiben. |
| `deviceGeoAccuracy` | Double | Die Genauigkeit des Geo-Messgeräts oder -Mechanismus; gemessen in Metern. |
| `distanceToCenter` | Double | Der Abstand zum Geo-Mittelpunkt bei einem Geo-Kreis, gemessen in Metern. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)
