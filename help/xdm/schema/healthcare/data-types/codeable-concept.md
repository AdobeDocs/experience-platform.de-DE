---
title: Datentyp des kodierbaren Konzepts
description: Erfahren Sie mehr über den Datentyp "Codeable Concept Experience Data Model (XDM)".
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: c172a7cd-24c6-484b-8552-8745dfd3a8e9
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 9%

---

# Datentyp [!UICONTROL Codeable Concept]

[!UICONTROL Codeable Concept] ist ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der einen Verweis von einer Ressource zu einer anderen beschreibt. Dieser Datentyp wird gemäß den Spezifikationen von HL7 FHIR Release 5 erstellt.

![Datenstruktur des kodierbaren Konzepts](../../../images/healthcare/data-types/codeable-concept.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Kodierung] | `coding` | Array von [[!UICONTROL Coding]](../data-types/coding.md) | Von einem Terminologiesystem definierter Code. |
| [!UICONTROL Text] | `text` | String | Die Textdarstellung des Konzepts. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeableconcept.schema.json)
