---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;Felder;Schemas;Schemas;Poi;Interaktion;Zielpunkt;Zielpunkt;Datentyp;Datentyp;Datentyp;
solution: Experience Platform
title: Interaktionsdatentyp des Zielpunkts
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über den XDM-Datentyp von Point-of-Interest-Interaktion.
exl-id: 398f56d9-1802-458d-b565-4096beb5b014
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 3%

---

# [!UICONTROL Interaktionsdatentyp ] des Zielpunkts

[!UICONTROL Point-of-Interaction ] ist ein standardmäßiger XDM-Datentyp, der das Wireless-Gerät beschreibt, das Identitätsinformationen an mobile Anwendungen weiterleitet, wenn mobile Geräte in Reichweite liegen.

<img src="../images/data-types/poi-interaction.png" width="400" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL Details zum Interessenbereich]](./poi-details.md) | Beschreibt die Details des POI, der das Ereignis verursacht hat. |
| `poiEntries` | Objekt | Beschreibt, wie oft eine Person in den POI eingereist ist. Enthält zwei Eigenschaften: <ul><li>`id`: Eine eindeutige ID für die Maßnahme.</li><li>`value`: Der quantifizierbare Wert der Maßnahme.</li></ul> |
| `poiExits` | Objekt | Beschreibt, wie oft eine Person den POI verlassen hat. Enthält zwei Eigenschaften: <ul><li>`id`: Eine eindeutige ID für die Maßnahme.</li><li>`value`: Der quantifizierbare Wert der Maßnahme.</li></ul> |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.schema.json)
