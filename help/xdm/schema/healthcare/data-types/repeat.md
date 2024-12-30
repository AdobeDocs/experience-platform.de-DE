---
title: Datentyp wiederholen
description: Erfahren Sie mehr über den Datentyp „Wiederholtes Experience-Datenmodell (XDM)“.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 9d40bc1d-33d1-4c33-a143-13fdcf8dc255
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 7%

---

# [!UICONTROL REPEAT] Datentyp

[!UICONTROL repeat] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der einen Regelsatz bereitstellt, der beschreibt, wann ein Ereignis geplant wird. Dieser Datentyp wird gemäß den HL7 FHIR Release 5-Spezifikationen erstellt.

![Struktur des Datentyps wiederholen](../../../images/healthcare/data-types/reference.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL gebundener Zeitraum] | `boundsPeriod` | [[!UICONTROL Zeitraum]](../data-types/period.md) | Start- und Endzeit. |
| [!UICONTROL gebundener Bereich] | `boundsRange` | [[!UICONTROL Bereich]](../data-types/range.md) | Die Bereichsbegrenzung. |
| [!UICONTROL Gebundene Dauer] | `boundsDuration` | [[!UICONTROL Dauer]](../data-types/duration.md) | Die maximale Dauer. |
| [!UICONTROL Count] | `count` | Ganzzahl | Die Anzahl der Wiederholungen mit einem Mindestwert von `0`. |
| [!UICONTROL Maximale Anzahl] | `countMax` | Ganzzahl | Die maximale Anzahl der Wiederholungen mit einem Mindestwert von `0`. |
| [!UICONTROL Wochentag] | `dayOfWeek` | Zeichenfolgen-Array | Ein Array von Zeichenfolgen, die angeben, welche Tage verfügbar sind. Die Werte dieser Eigenschaft müssen mindestens einem der folgenden bekannten Enum-Werte entsprechen. <li> `mon` </li> <li> `tues` </li> <li> `wed` </li> <li> `thurs`</li>  <li> `fri` </li> <li> `sat`</li> <li> `sun`</li> |
| [!UICONTROL Dauer] | `duration` | Double | Die Dauer. |
| [!UICONTROL Maximale Dauer] | `durationMax` | Double | Die maximale Zeitdauer. |
| [!UICONTROL Dauer Einheit] | `durationUnit` | String | Die Einheit der Dauer. Die Werte dieser Eigenschaft müssen mindestens einem der folgenden bekannten Enum-Werte entsprechen. <li> `s` (Sekunden) </li> <li> `min` (Minuten) </li> <li> `h` (pro Stunde) </li> <li> `d` (täglich) </li>  <li> `wk` (wöchentlich) </li> <li> `mo` (monatlich) </li> <li> `a` (jährlich)</li> |
| [!UICONTROL Häufigkeit] | `frequency` | Double | Die Anzahl der Wiederholungen, die innerhalb eines Zeitraums auftreten sollen, mit einem Mindestwert von `0`. |
| [!UICONTROL Höchstfrequenz] | `frequencyMax` | Double | Die maximale Anzahl von Wiederholungen, die mit einem Punkt auftreten sollen, mit einem Mindestwert von `0`. |
| [!UICONTROL Versatz] | `offset` | Ganzzahl | Die Minute(n) bis zum Ereignis (vor oder nach dem Ereignis). |
| [!UICONTROL Zeitraum] | `period` | Double | Die Dauer, während der die Häufigkeit gilt. |
| [!UICONTROL Maximaler Zeitraum] | `periodMax` | Double | Die Obergrenze des Zeitraums. |
| [!UICONTROL Periodeneinheit] | `periodUnit` | String | Die Zeiteinheit. Die Werte dieser Eigenschaft müssen mindestens einem der folgenden bekannten Enum-Werte entsprechen. <li> `s` (Sekunden) </li> <li> `min` (Minuten) </li> <li> `h` (pro Stunde) </li> <li> `d` (täglich) </li>  <li> `wk` (wöchentlich) </li> <li> `mo` (monatlich) </li> <li> `a` (jährlich)</li> |
| [!UICONTROL Tageszeit] | `timeOfDay` | Zeichenfolgen-Array | Die Tageszeit, zu der die Aktion stattfindet. |
| [!UICONTROL When] | `when` | Zeichenfolgen-Array | Der Code für den Zeitraum der Aktion. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/repeat.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/repeat.schema.json)
