---
title: Datentyp Impressions
description: Erfahren Sie mehr über den XDM-Datentyp Impressions .
exl-id: 1e758043-a41e-45f7-ae8b-514990d0649e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 6%

---

# [!UICONTROL Impressions]-Datentyp

[!UICONTROL Impressions] ist ein standardmäßiger XDM-Datentyp, der eine Marketing-Impression beschreibt, eine Metrik, mit der die Anzahl der digitalen Ansichten oder Interaktionen für ein Inhaltselement wie eine Werbung, einen digitalen Beitrag oder eine Web-Seite quantifiziert wird.

![](../images/data-types/impressions.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `ID` | Zeichenfolge | Eine eindeutige ID für die Impression. |
| `displays` | Ganzzahl | Die Häufigkeit, mit der das Impressionselement einem Kunden angezeigt wurde. |
| `selected` | Ganzzahl | Die Häufigkeit, mit der das Impressionselement ausgewählt oder angeklickt wurde. |
| `type` | String | Die Art der Impression. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.schema.json)
