---
title: Identifier-Datentyp
description: Erfahren Sie mehr über den Datentyp Identifier Experience-Datenmodell (XDM) .
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 0664f52d-bea6-4aa1-b2a5-de0bd6d5edd9
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 9%

---

# Datentyp [!UICONTROL Identifier]

[!UICONTROL Bezeichner] ist ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der eine für die Berechnung vorgesehene Kennung bereitstellt. Dieser Datentyp wird gemäß den Spezifikationen von HL7 FHIR Release 5 erstellt.

![Struktur des Bezeichnerdatentyps](../../../images/healthcare/data-types/identifier.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Zeitraum] | `period` | [[!UICONTROL Zeitraum]](../data-types/period.md) | Der Zeitraum, in dem die ID zur Verwendung gültig ist oder war. |
| [!UICONTROL Typ] | `type` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Die Beschreibung der Kennung. |
| [!UICONTROL Assigner] | `assigner` | String | Die Organisation, die die ID ausgestellt hat. |
| [!UICONTROL System] | `system` | String | Der Namespace für den Kennungswert, dargestellt als URI. |
| [!UICONTROL Use] | `use` | String | Die Verwendung der Kennung. Die Werte dieser Eigenschaft müssen mit einem oder mehreren der folgenden bekannten Enum-Werte übereinstimmen. <li> `usual` </li> <li> `offical` </li> <li> `temp` </li> <li> `secondary` </li> <li> `old` </li> |
| [!UICONTROL Wert] | `value` | String | Der eindeutige Wert der ID. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/identifier.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/identifier.schema.json)
