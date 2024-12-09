---
title: Datentyp "Quantität"
description: Erfahren Sie mehr über den Datentyp "Quantity Experience Data Model (XDM)".
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 11%

---

# Datentyp [!UICONTROL Quantity]

[!UICONTROL Quantity] ist ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der einen gemessenen oder messbaren Betrag liefert. Dieser Datentyp wird gemäß den Spezifikationen von HL7 FHIR Release 5 erstellt.

![Struktur des Datentyps Quantität](../../images/data-types/healthcare/quantity.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | String | Die codierte Form der Einheit. |
| [!UICONTROL Comparator] | `comparator` | String | Der Vergleichsoperator. Der Wert dieser Eigenschaft muss mit einem der folgenden bekannten Enum-Werte übereinstimmen. <li> `<` </li> <li> `<=` </li> <li> `>=` </li> <li> `>`</li> <li> `ad`</li> |
| [!UICONTROL System] | `system` | String | Das System, das das kodierte Einheitenformular definiert, das als URI dargestellt wird. |
| [!UICONTROL Unit] | `unit` | String | Die Einheitendarstellung. |
| [!UICONTROL Wert] | `value` | Double | Der numerische Wert. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/quantity.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/quantity.schema.json)
