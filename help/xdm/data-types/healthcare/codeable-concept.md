---
title: Datentyp des kodierbaren Konzepts
description: Erfahren Sie mehr über den Datentyp "Codeable Concept Experience Data Model (XDM)".
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 9%

---

# Datentyp [!UICONTROL Codeable Concept]

[!UICONTROL Codeable Concept] ist ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der einen Verweis von einer Ressource zu einer anderen beschreibt. Dieser Datentyp wird gemäß den Spezifikationen von HL7 FHIR Release 5 erstellt.

![Datenstruktur des kodierbaren Konzepts](../../images/data-types/healthcare/codeable-concept.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Kodierung] | `coding` | Array von [[!UICONTROL Coding]](../healthcare/coding.md) | Von einem Terminologiesystem definierter Code. |
| [!UICONTROL Text] | `text` | String | Die Textdarstellung des Konzepts. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeableconcept.schema.json)
