---
title: Zeitraum-Datentyp
description: Erfahren Sie mehr über den Datentyp "Period Experience Data Model"(XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 12%

---

# Datentyp [!UICONTROL Zeitraum]

[!UICONTROL Zeitraum] ist ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der einen Zeitraum bereitstellt, der durch ein Start- und Enddatum/-zeit definiert wird. Dieser Datentyp wird gemäß den Spezifikationen von HL7 FHIR Release 5 erstellt.

![Struktur des Datentyps &quot;Zeitraum&quot;](../../images/data-types/healthcare/period.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Ende] | `end` | DateTime | Enddatum und -zeit. |
| [!UICONTROL Starten] | `start` | DateTime | Startdatum und -zeit. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/period.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/period.schema.json)
