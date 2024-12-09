---
title: Anmerkungsdatentyp
description: Erfahren Sie mehr über den Datentyp des Experience-Datenmodells für Anmerkungen (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 11%

---

# Datentyp [!UICONTROL Anmerkung]

[!UICONTROL Anmerkung] ist ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der einen Textknoten mit Attribution zum Autor enthält. Dieser Datentyp wird gemäß den Spezifikationen von HL7 FHIR Release 5 erstellt.

![Struktur des Anmerkungstyps](../../images/data-types/healthcare/annotation.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Autorenreferenz] | `authorReference` | [[!UICONTROL Referenz]](../healthcare/reference.md) | Ein Verweis auf den Autor. |
| [!UICONTROL Autor] | `authorString` | String | Der für die Anmerkung verantwortliche Benutzer. |
| [!UICONTROL Text] | `text` | String | Der Inhalt der Anmerkung. |
| [!UICONTROL Zeit] | `time` | DateTime | Wann die Anmerkung gemacht wurde |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/annotation.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/annotation.schema.json)
