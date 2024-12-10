---
title: Datentyp wiederholen
description: Erfahren Sie mehr über den Datentyp "Repeat Experience Data Model (XDM)".
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 9d40bc1d-33d1-4c33-a143-13fdcf8dc255
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 7%

---

# [!UICONTROL Repeat]-Datentyp

[!UICONTROL Wiederholen] ist ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der eine Reihe von Regeln bereitstellt, die beschreiben, wann ein Ereignis geplant ist. Dieser Datentyp wird gemäß den Spezifikationen von HL7 FHIR Release 5 erstellt.

![Struktur des Datentyps wiederholen](../../../images/healthcare/data-types/reference.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL  Gebundener Zeitraum] | `boundsPeriod` | [[!UICONTROL Zeitraum]](../data-types/period.md) | Die Start- und Endzeiten. |
| [!UICONTROL Gebundener Bereich] | `boundsRange` | [[!UICONTROL Bereich]](../data-types/range.md) | Die Bereichsbegrenzung. |
| [!UICONTROL Bounddauer] | `boundsDuration` | [[!UICONTROL Dauer]](../data-types/duration.md) | Die Begrenzung der Dauer. |
| [!UICONTROL Count] | `count` | Ganzzahl | Die Anzahl der Wiederholungen mit einem Mindestwert von `0`. |
| [!UICONTROL Maximale Anzahl] | `countMax` | Ganzzahl | Die maximale Anzahl der Wiederholungen mit einem Mindestwert von `0`. |
| [!UICONTROL Wochentag] | `dayOfWeek` | Zeichenfolgen-Array | Ein Array von Zeichenfolgen, die angeben, welche Tage verfügbar sind. Die Werte dieser Eigenschaft müssen mit einem oder mehreren der folgenden bekannten Enum-Werte übereinstimmen. <li> `mon` </li> <li> `tues` </li> <li> `wed` </li> <li> `thurs`</li>  <li> `fri` </li> <li> `sat`</li> <li> `sun`</li> |
| [!UICONTROL Dauer] | `duration` | Double | Die Zeitdauer. |
| [!UICONTROL Maximale Dauer] | `durationMax` | Double | Die maximale Zeitdauer. |
| [!UICONTROL Duration Unit] | `durationUnit` | String | Die Maßeinheit für die Dauer. Die Werte dieser Eigenschaft müssen mit einem oder mehreren der folgenden bekannten Enum-Werte übereinstimmen. <li> `s` (Sekunden) </li> <li> `min` (Minuten) </li> <li> `h` (stündlich) </li> <li> `d` (täglich) </li>  <li> `wk` (Wöchentlich) </li> <li> `mo` (monatlich) </li> <li> `a` (jährlich)</li> |
| [!UICONTROL Häufigkeit] | `frequency` | Double | Die Anzahl der Wiederholungen, die innerhalb eines Zeitraums mit einem Mindestwert von `0` auftreten sollen. |
| [!UICONTROL Maximale Häufigkeit] | `frequencyMax` | Double | Die maximale Anzahl von Wiederholungen, die bei einem Punkt mit einem Mindestwert von `0` auftreten sollten. |
| [!UICONTROL offset] | `offset` | Ganzzahl | Die Minute(n) bis zum Ereignis (vor oder nach). |
| [!UICONTROL Zeitraum] | `period` | Double | Die Dauer, während der die Frequenz angewendet wird. |
| [!UICONTROL Max. Zeitraum] | `periodMax` | Double | Die Obergrenze des Zeitraums. |
| [!UICONTROL Zeiteinheit] | `periodUnit` | String | Die Zeiteinheit. Die Werte dieser Eigenschaft müssen mit einem oder mehreren der folgenden bekannten Enum-Werte übereinstimmen. <li> `s` (Sekunden) </li> <li> `min` (Minuten) </li> <li> `h` (stündlich) </li> <li> `d` (täglich) </li>  <li> `wk` (Wöchentlich) </li> <li> `mo` (monatlich) </li> <li> `a` (jährlich)</li> |
| [!UICONTROL Tageszeit] | `timeOfDay` | Zeichenfolgen-Array | Die Tageszeit für die Aktion. |
| [!UICONTROL When] | `when` | Zeichenfolgen-Array | Der Code für den Zeitraum der Aktion. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/repeat.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/repeat.schema.json)
