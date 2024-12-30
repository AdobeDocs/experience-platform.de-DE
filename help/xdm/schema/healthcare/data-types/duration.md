---
title: Datentyp „Dauer“
description: Erfahren Sie mehr über den Datentyp „Duration Experience Data Model“ (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 01aac0d0-0503-4f8b-a306-cf3c187a76e0
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 9%

---

# [!UICONTROL Dauer] Datentyp

[!UICONTROL Duration] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der eine bestimmte Zeitdauer beschreibt. Dieser Datentyp wird gemäß den HL7 FHIR Release 5-Spezifikationen erstellt.

![Struktur des Datentyps „Dauer“](../../../images/healthcare/data-types/duration.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | String | Die codierte Form der Zeiteinheit. |
| [!UICONTROL System] | `system` | String | Das System, das die codierte Einheit beschreibt, dargestellt als URI. |
| [!UICONTROL Einheit] | `unit` | String | Die Zeiteinheit, dargestellt in Millisekunden, Sekunden, Minuten, Stunden, Tagen, Wochen, Monaten oder Jahren. Die Werte dieser Eigenschaft müssen mindestens einem der folgenden bekannten Enum-Werte entsprechen. <li> `ms` (ms) </li> <li> `s` (Sekunden) </li> <li> `min` (Minuten) </li> <li> `h` (Stunden) </li>  <li> `d` (Tage) </li> <li> `wk` (Wochen) </li> <li> `mo` (Monate) </li> <li> `a` (Jahre) </li> |
| [!UICONTROL Wert] | `value` | Double | Der numerische Wert für die Zeiteinheit. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/duration.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/duration.schema.json)
