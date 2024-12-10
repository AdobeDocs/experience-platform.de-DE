---
title: Einfacher Datentyp "Menge"
description: Erfahren Sie mehr über den Datentyp "Simple Quantity Experience Data Model (XDM)".
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 92d3d6a8-1d0f-43a4-a93f-8df79605c4e6
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 12%

---

# Datentyp [!UICONTROL Einfache Menge]

[!UICONTROL Einfache Menge] ist ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der einen gemessenen oder messbaren Betrag liefert. Dieser Datentyp wird gemäß den Spezifikationen von HL7 FHIR Release 5 erstellt.

![Struktur des einfachen Datentyps &quot;Menge&quot;](../../../images/healthcare/data-types/simple-quantity.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | String | Die codierte Form der Einheit. |
| [!UICONTROL System] | `system` | String | Das System, das das kodierte Einheitenformular definiert, das als URI dargestellt wird. |
| [!UICONTROL Unit] | `unit` | String | Die Darstellung der Einheit. |
| [!UICONTROL Wert] | `value` | Double | Der numerische Wert. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.schema.json)
