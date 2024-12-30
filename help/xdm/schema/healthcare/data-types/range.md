---
title: Datentyp des Bereichs
description: Erfahren Sie mehr über den Datentyp Experience-Datenmodell (XDM) .
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 66f8b574-04d9-435f-8743-4ff89c4c0079
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 8%

---

# [!UICONTROL Bereich] Datentyp

[!UICONTROL Range] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der einen Satz von Werten bereitstellt, die an niedrige und hohe Werte gebunden sind. Dieser Datentyp wird gemäß den HL7 FHIR Release 5-Spezifikationen erstellt.

![Struktur des Datentyps „Range](../../../images/healthcare/data-types/range.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Hoch] | `high` | [[!UICONTROL Einfache Menge]](../data-types/simple-quantity.md) | Die höchste Grenze. |
| [!UICONTROL Niedrig] | `low` | [[!UICONTROL Einfache Menge]](../data-types/simple-quantity.md) | Die niedrigste Grenze. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/range.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/range.schema.json)
