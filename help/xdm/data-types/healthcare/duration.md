---
title: Datentyp der Dauer
description: Erfahren Sie mehr über den Datentyp "Duration Experience Data Model (XDM)".
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 9%

---

# Datentyp [!UICONTROL Dauer]

[!UICONTROL Dauer] ist ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der eine Zeitdauer beschreibt. Dieser Datentyp wird gemäß den Spezifikationen von HL7 FHIR Release 5 erstellt.

![Struktur des Datentyps Dauer](../../images/data-types/healthcare/duration.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | String | Die codierte Form der Zeiteinheit. |
| [!UICONTROL System] | `system` | String | Das System, das die codierte Einheit beschreibt, dargestellt als URI. |
| [!UICONTROL Unit] | `unit` | String | Die Zeiteinheit, die in Millisekunden, Sekunden, Minuten, Stunden, Tagen, Wochen, Monaten oder Jahren dargestellt wird. Die Werte dieser Eigenschaft müssen mit einem oder mehreren der folgenden bekannten Enum-Werte übereinstimmen. <li> `ms` (Millisekunden) </li> <li> `s` (Sekunden) </li> <li> `min` (Minuten) </li> <li> `h` (Stunden) </li>  <li> `d` (Tage) </li> <li> `wk` (Wochen) </li> <li> `mo` (months) </li> <li> `a` (Jahre) </li> |
| [!UICONTROL Wert] | `value` | Double | Der numerische Wert für die Zeiteinheit. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/duration.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/duration.schema.json)
