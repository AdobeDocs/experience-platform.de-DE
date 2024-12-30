---
title: Zeitdatentyp
description: Erfahren Sie mehr über den Datentyp Timing Experience-Datenmodell (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: e1bc16ed-4dd8-4316-b3c8-88d49d393859
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 9%

---

# [!UICONTROL Timing] Datentyp

[!UICONTROL Timing] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der einen Zeitplan beschreibt, der Informationen zu einem Ereignis bereitstellt, das mehrmals auftreten kann. Dieser Datentyp wird gemäß den HL7 FHIR Release 5-Spezifikationen erstellt.

![Struktur des Datentyps für Zeitplanung](../../../images/healthcare/data-types/timing.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Ereignis] | `event` | Array von DateTime | Wenn das Ereignis eintritt. |
| [!UICONTROL Wiederholen] | `repeat` | [[!UICONTROL Wiederholen]](../data-types/repeat.md) | Informationen über den Zeitpunkt des Ereignisses. |
| [!UICONTROL Code] | `code` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Der Code zum Ereignis. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/timing.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/timing.schema.json)
