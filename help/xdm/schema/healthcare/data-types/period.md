---
title: Periodendatentyp
description: Erfahren Sie mehr über den Datentyp „Experience-Datenmodell“ (XDM) für Zeiträume.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: aecd09e4-2797-4d2d-be62-acad28fb7bba
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 12%

---

# [!UICONTROL Zeitraum] Datentyp

[!UICONTROL Zeitraum] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der einen Zeitraum bereitstellt, der durch ein Start- und Enddatum/-zeit definiert ist. Dieser Datentyp wird gemäß den HL7 FHIR Release 5-Spezifikationen erstellt.

![Period-Datentypstruktur](../../../images/healthcare/data-types/period.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Ende] | `end` | DateTime | Enddatum und -zeit |
| [!UICONTROL Starten] | `start` | DateTime | Startdatum und -zeit |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/period.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/period.schema.json)
