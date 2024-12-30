---
title: Datentyp der Anmerkung
description: Erfahren Sie mehr über den Datentyp Experience-Datenmodell (XDM) für Anmerkungen.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: f46b5fb6-d64a-4a37-91f6-b470599d9130
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 11%

---

# [!UICONTROL Anmerkung] Datentyp

[!UICONTROL Annotation] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der einen Textknoten mit einer Attribution zum Autor enthält. Dieser Datentyp wird gemäß den HL7 FHIR Release 5-Spezifikationen erstellt.

![Struktur des Datentyps für Anmerkungen](../../../images/healthcare/data-types/annotation.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Autorenreferenz] | `authorReference` | [[!UICONTROL Referenz]](../data-types/reference.md) | Ein Verweis auf den Autor. |
| [!UICONTROL author] | `authorString` | String | Die für die Anmerkung verantwortliche Person. |
| [!UICONTROL Text] | `text` | String | Der Inhalt der Anmerkung. |
| [!UICONTROL Zeit] | `time` | DateTime | Zeitpunkt, zu dem die Anmerkung erstellt wurde. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/annotation.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/annotation.schema.json)
