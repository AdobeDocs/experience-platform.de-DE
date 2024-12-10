---
title: Anmerkungsdatentyp
description: Erfahren Sie mehr über den Datentyp des Experience-Datenmodells für Anmerkungen (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: f46b5fb6-d64a-4a37-91f6-b470599d9130
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 11%

---

# Datentyp [!UICONTROL Anmerkung]

[!UICONTROL Anmerkung] ist ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der einen Textknoten mit Attribution zum Autor enthält. Dieser Datentyp wird gemäß den Spezifikationen von HL7 FHIR Release 5 erstellt.

![Struktur des Anmerkungstyps](../../../images/healthcare/data-types/annotation.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Autorenreferenz] | `authorReference` | [[!UICONTROL Referenz]](../data-types/reference.md) | Ein Verweis auf den Autor. |
| [!UICONTROL Autor] | `authorString` | String | Der für die Anmerkung verantwortliche Benutzer. |
| [!UICONTROL Text] | `text` | String | Der Inhalt der Anmerkung. |
| [!UICONTROL Zeit] | `time` | DateTime | Wann die Anmerkung gemacht wurde |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/annotation.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/annotation.schema.json)
