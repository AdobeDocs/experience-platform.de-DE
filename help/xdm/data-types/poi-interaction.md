---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;poi;interaction;point of interest;point-of-interest;datatype;data-type;data type;
solution: Experience Platform
title: Interaktionsdatentyp des Point-Interest
topic: overview
description: Dieses Dokument bietet einen Überblick über den XDM-Datentyp von Point-of-Interest-Interaktion.
translation-type: tm+mt
source-git-commit: 032adc72db7f094b268f14e8f7d48810830a84e4
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 3%

---


# [!UICONTROL Interaktionsdatentyp des] Point-Interaktion

[!UICONTROL Point-of-Interest-Interaktion] ist ein standardmäßiger XDM-Datentyp, der das Wireless-Gerät beschreibt, das Identitätsinformationen an mobile Anwendungen weiterleitet, wenn mobile Geräte in Reichweite kommen.

<img src="../images/data-types/poi-interaction.png" width="400" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL Details zum Interessenbereich]](./poi-details.md) | Beschreibt die Details des POI, der das Ereignis verursacht hat. |
| `poiEntries` | Objekt | Beschreibt, wie oft eine Person in den POI eingereist ist. Enthält zwei Eigenschaften: <ul><li>`id`: Eine eindeutige ID für die Maßnahme.</li><li>`value`: Der quantifizierbare Wert der Maßnahme.</li></ul> |
| `poiExits` | Objekt | Beschreibt, wie oft eine Person den POI verlassen hat. Enthält zwei Eigenschaften: <ul><li>`id`: Eine eindeutige ID für die Maßnahme.</li><li>`value`: Der quantifizierbare Wert der Maßnahme.</li></ul> |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.schema.json)
