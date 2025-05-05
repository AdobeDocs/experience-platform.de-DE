---
title: Datentyp „Einfache Menge“
description: Erfahren Sie mehr über den Datentyp „Einfaches Quantitäts-Experience-Datenmodell (XDM)“.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 92d3d6a8-1d0f-43a4-a93f-8df79605c4e6
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 12%

---

# [!UICONTROL Einfache &#x200B;]) Datentyp

[!UICONTROL Einfache Menge] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der einen gemessenen oder messbaren Betrag bereitstellt. Dieser Datentyp wird gemäß den HL7 FHIR Release 5-Spezifikationen erstellt.

![Einfache Struktur des Datentyps „Menge“](../../../images/healthcare/data-types/simple-quantity.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | String | Die codierte Form der Einheit. |
| [!UICONTROL System] | `system` | String | Das System, das die codierte Einheitenform definiert, dargestellt als URI. |
| [!UICONTROL Einheit] | `unit` | String | Die Darstellung der Einheit. |
| [!UICONTROL Wert] | `value` | Double | Der numerische Wert. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.schema.json)
