---
title: Impressions-Datentyp
description: Dieses Dokument bietet einen Überblick über den XDM-Datentyp "Impressionen".
exl-id: 1e758043-a41e-45f7-ae8b-514990d0649e
source-git-commit: afdac5ce2ed967b4688d456a586c946bc2cf4179
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 5%

---

# [!UICONTROL Impressionen] Datentyp

[!UICONTROL Impressionen] ist ein standardmäßiger XDM-Datentyp, der eine Marketing-Impression beschreibt. Hierbei handelt es sich um eine Metrik, mit der die Anzahl der digitalen Ansichten oder Interaktionen für einen Inhaltselement wie Werbung, digitaler Beitrag oder Webseite quantifiziert wird.

![](../images/data-types/impressions.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `ID` | Zeichenfolge | Eine eindeutige ID für die Impression. |
| `displays` | Ganzzahl | Die Häufigkeit, mit der das Impressionselement einem Kunden angezeigt wurde. |
| `selected` | Ganzzahl | Die Häufigkeit, mit der das Impressionselement ausgewählt oder angeklickt wurde. |
| `type` | Zeichenfolge | Die Art der Impression. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.schema.json)
