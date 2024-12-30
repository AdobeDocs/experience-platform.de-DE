---
title: Referenzdatentyp
description: Erfahren Sie mehr über den Referenzdatentyp „Experience-Datenmodell (XDM)“.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: eb724dbb-2918-43b5-8e50-c8aabfe6e96c
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 12%

---

# [!UICONTROL Referenz] Datentyp

[!UICONTROL Referenz] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der einen Verweis von einer Ressource zur anderen bereitstellt. Dieser Datentyp wird gemäß den HL7 FHIR Release 5-Spezifikationen erstellt.

![Struktur des Referenzdatentyps](../../../images/healthcare/data-types/reference.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL ID] | `identifier` | [[!UICONTROL ID]](../data-types/identifier.md) | Die logische Referenz, wenn die Literalreferenz nicht bekannt ist. |
| [!UICONTROL Anzeige] | `display` | String | Die Textalternative für die Referenz. |
| [!UICONTROL Referenz] | `reference` | String | Die literale Referenz, relativ, intern oder absolute URL. |
| [!UICONTROL Typ] | `type` | String | Der Typ, auf den der Verweis verweist, dargestellt als URI. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/reference.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/reference.schema.json)
