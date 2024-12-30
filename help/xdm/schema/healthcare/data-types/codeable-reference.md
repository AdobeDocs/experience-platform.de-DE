---
title: Codierbarer Referenzdatentyp
description: Erfahren Sie mehr über den Datentyp Codeable Reference Experience Data Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 5ac4bc82-3c8e-4622-8a4e-c954bd6e6411
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 7%

---

# [!UICONTROL Codeable Reference] Datentyp

[!UICONTROL Codeable Reference] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der einen Verweis auf eine Ressource oder ein Konzept beschreibt. Dieser Datentyp wird gemäß den HL7 FHIR Release 5-Spezifikationen erstellt.

![Codeable Reference-Datentypstruktur](../../../images/healthcare/data-types/codeable-reference.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Konzept] | `concept` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Ein Verweis auf ein Konzept (nach Klasse). |
| [!UICONTROL Referenz] | `reference` | [[!UICONTROL Referenz]](../data-types/reference.md) | Ein Verweis auf eine Ressource. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.schema.json)
