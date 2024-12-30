---
title: Datentyp des codierbaren Konzepts
description: Erfahren Sie mehr über den Datentyp Codeable Concept Experience Data Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: c172a7cd-24c6-484b-8552-8745dfd3a8e9
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 9%

---

# [!UICONTROL Codeable Concept] Datentyp

[!UICONTROL Codeable Concept] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der einen Verweis von einer Ressource zur anderen beschreibt. Dieser Datentyp wird gemäß den HL7 FHIR Release 5-Spezifikationen erstellt.

![Codeable Concept-Datentypstruktur](../../../images/healthcare/data-types/codeable-concept.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Kodierung] | `coding` | Array von [[!UICONTROL Codierung]](../data-types/coding.md) | Durch ein Terminologiesystem definierter Code |
| [!UICONTROL Text] | `text` | String | Die Textdarstellung des Konzepts. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeableconcept.schema.json)
