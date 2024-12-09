---
title: Timing-Datentyp
description: Erfahren Sie mehr über den XDM-Datentyp (Timing Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 0640d0c2daab67ad7a77d3265ccae45851ba45b8
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 9%

---

# [!UICONTROL Timing]-Datentyp

[!UICONTROL Timing] ist ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der einen Zeitplan beschreibt, der Informationen zu einem Ereignis bereitstellt, das mehrere Male auftreten kann. Dieser Datentyp wird gemäß den Spezifikationen von HL7 FHIR Release 5 erstellt.

![Struktur des Datentyps für die Zeitplanung](../../images/data-types/healthcare/timing.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Ereignis] | `event` | Array of DateTime | Wenn das Ereignis eintritt. |
| [!UICONTROL Wiederholen] | `repeat` | [[!UICONTROL Wiederholen]](../healthcare/repeat.md) | Informationen darüber, wann das Ereignis eintritt. |
| [!UICONTROL Code] | `code` | [[!UICONTROL Codeable Concept]](../healthcare/codeable-concept.md) | Der Code für das Ereignis. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/timing.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/timing.schema.json)
