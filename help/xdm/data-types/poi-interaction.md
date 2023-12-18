---
keywords: Experience Platform; home; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; poi; Interaktion; Zielpunkt; Zielpunkt; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: POI-Interaktionsdatentyp
description: Erfahren Sie mehr über den XDM-Datentyp von POI Interaction.
exl-id: 398f56d9-1802-458d-b565-4096beb5b014
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 3%

---

# [!UICONTROL Interaktion mit Zielpunkten] Datentyp

[!UICONTROL Interaktion mit Zielpunkten] ist ein standardmäßiger XDM-Datentyp, der das drahtlose Gerät beschreibt, das Identitätsinformationen an mobile Anwendungen weitergibt, wenn mobile Geräte in Reichweite sind.

<img src="../images/data-types/poi-interaction.png" width="400" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL Details zum POI]](./poi-details.md) | Beschreibt die Details des POI, der das Ereignis verursacht hat. |
| `poiEntries` | Objekt | Beschreibt, wie oft eine Person am POI teilgenommen hat. Enthält zwei Eigenschaften: <ul><li>`id`: Eine eindeutige Kennung für die Kennzahl.</li><li>`value`: Der quantifizierbare Wert der Maßnahme.</li></ul> |
| `poiExits` | Objekt | Beschreibt, wie oft eine Person den POI verlassen hat. Enthält zwei Eigenschaften: <ul><li>`id`: Eine eindeutige Kennung für die Kennzahl.</li><li>`value`: Der quantifizierbare Wert der Maßnahme.</li></ul> |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.schema.json)
