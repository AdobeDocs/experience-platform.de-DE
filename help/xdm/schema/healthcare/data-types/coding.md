---
title: Codierungsdatentyp
description: Erfahren Sie mehr über den Datentyp Coding Experience Data Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 23b789da-1feb-4001-8268-f0d7e2e8563b
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 11%

---

# [!UICONTROL Codierung] Datentyp

[!UICONTROL Coding] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der einen Verweis auf einen von einem Terminologiesystem definierten Code beschreibt. Dieser Datentyp wird gemäß den HL7 FHIR Release 5-Spezifikationen erstellt.

![Codieren der Datentypstruktur](../../../images/healthcare/data-types/coding.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | String | Das Symbol in der vom System definierten Syntax. |
| [!UICONTROL Anzeige] | `display` | String | Die vom System definierte Darstellung. |
| [!UICONTROL System] | `system` | String | Der Namespace für den Kennungswert, dargestellt als URI. |
| [!UICONTROL wird vom Benutzer ausgewählt] | `userSelected` | Boolesch | Ein Indikator dafür, ob diese Kodierung vom Benutzer ausgewählt wurde. Der Standardwert ist „false“. |
| [!UICONTROL Version] | `version` | String | Die Version des Systems. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/coding.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/coding.schema.json)
