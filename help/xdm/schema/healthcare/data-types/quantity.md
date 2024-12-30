---
title: Datentyp der Menge
description: Erfahren Sie mehr über den Datentyp „Quantity Experience-Datenmodell (XDM)“.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 881fe8a4-0253-4b75-9833-b97bb50cc87e
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 11%

---

# [!UICONTROL Menge] Datentyp

[!UICONTROL Quantity] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der einen gemessenen oder messbaren Betrag bereitstellt. Dieser Datentyp wird gemäß den HL7 FHIR Release 5-Spezifikationen erstellt.

![Struktur des Datentyps „Menge](../../../images/healthcare/data-types/quantity.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | String | Die codierte Form der Einheit. |
| [!UICONTROL Vergleicher] | `comparator` | String | Der Vergleichsoperator. Der Wert dieser Eigenschaft muss einem der folgenden bekannten Enum-Werte entsprechen. <li> `<` </li> <li> `<=` </li> <li> `>=` </li> <li> `>`</li> <li> `ad`</li> |
| [!UICONTROL System] | `system` | String | Das System, das die codierte Formulareinheit definiert, dargestellt als URI. |
| [!UICONTROL Einheit] | `unit` | String | Die Einheitendarstellung. |
| [!UICONTROL Wert] | `value` | Double | Der numerische Wert. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/quantity.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/quantity.schema.json)
