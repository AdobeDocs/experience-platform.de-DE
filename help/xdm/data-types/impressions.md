---
title: Impressions-Datentyp
description: Dieses Dokument bietet einen Überblick über den XDM-Datentyp "Impressionen".
source-git-commit: 7fc16546176d196582a3cdfcee51f799eeef9788
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 7%

---

#  Impressions-Datentyp

 Impressionsis ist ein standardmäßiger XDM-Datentyp, der eine Marketing-Impression beschreibt. Hierbei handelt es sich um eine Metrik, mit der die Anzahl der digitalen Ansichten oder Interaktionen für einen Inhaltsabschnitt wie Werbung, einen digitalen Beitrag oder eine Webseite quantifiziert wird.

![](../images/data-types/impressions.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `ID` | Zeichenfolge | Eine eindeutige ID für die Impression. |
| `displays` | Ganzzahl | Die Häufigkeit, mit der das Impressionselement einem Kunden angezeigt wurde. |
| `selected` | Ganzzahl | Die Häufigkeit, mit der das Impressionselement ausgewählt oder angeklickt wurde. |
| `type` | Zeichenfolge | Die Art der Impression. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.schema.json)
