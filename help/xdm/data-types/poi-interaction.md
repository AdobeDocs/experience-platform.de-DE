---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;Felder;Schemata;Schemata;Schemata;poi;Interaktion;Point of Interest;Point of Interest;Datentyp;Datentyp;
solution: Experience Platform
title: Interaktionsdatentyp „Point of Interest“
description: Erfahren Sie mehr über den XDM-Datentyp Point of Interest Interaction.
exl-id: 398f56d9-1802-458d-b565-4096beb5b014
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 3%

---

# [!UICONTROL Point of Interest]Interaktion, Datentyp

[!UICONTROL Point of Interest Interaction] ist ein standardmäßiger XDM-Datentyp, der das drahtlose Gerät beschreibt, das Identitätsinformationen an mobile Anwendungen übermittelt, wenn mobile Geräte in Reichweite kommen.

![](../images/data-types/poi-interaction.png){width=400}

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL Details zum Point of Interest]](./poi-details.md) | Beschreibt die Details des POI, der das Ereignis verursacht hat. |
| `poiEntries` | Objekt | Beschreibt, wie oft eine Person in den POI eingetreten ist. Enthält zwei Eigenschaften: <ul><li>`id`: Eine eindeutige Kennung für die Kennzahl.</li><li>`value`: Der quantifizierbare Wert der Maßnahme.</li></ul> |
| `poiExits` | Objekt | Beschreibt, wie oft eine Person den POI verlassen hat. Enthält zwei Eigenschaften: <ul><li>`id`: Eine eindeutige Kennung für die Kennzahl.</li><li>`value`: Der quantifizierbare Wert der Maßnahme.</li></ul> |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.schema.json)
