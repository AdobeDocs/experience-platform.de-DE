---
title: Menschenname-Datentyp
description: Erfahren Sie mehr über den Datentyp des Experience-Datenmodells für menschliche Namen (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 5dd6fda4-c076-4c34-bdd9-259203b6ea73
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 6%

---

# [!UICONTROL Menschenname]-Datentyp

[!UICONTROL Menschlicher Name] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Informationen zum Namen einer menschlichen oder anderen lebenden Entität bereitstellt. Dieser Datentyp wird gemäß den Spezifikationen von HL7 FHIR Release 5 erstellt.

![Struktur des Datentyps &quot;Menschenname&quot;](../../../images/healthcare/data-types/human-name.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Zeitraum] | `period` | [[!UICONTROL Zeitraum]](../data-types/period.md) | Der Zeitraum, in dem der Name verwendet wird oder war. |
| [!UICONTROL Family] | `family` | String | Familie oder Nachname. |
| [!UICONTROL given] | `given` | Zeichenfolgen-Array | Der Vorname, einschließlich etwaiger Vornamen. |
| [!UICONTROL Präfix] | `prefix` | Zeichenfolgen-Array | Alle Teile des Namens vor dem Vornamen oder Vornamen. |
| [!UICONTROL Suffix] | `suffix` | Zeichenfolgen-Array | Alle Teile des Namens nach der Familie oder dem Nachnamen. |
| [!UICONTROL Text] | `text` | String | Die Textdarstellung des vollständigen Namens. |
| [!UICONTROL Use] | `use` | String | Die Verwendung des Namens. Die Werte dieser Eigenschaft müssen mit einem oder mehreren der folgenden bekannten Enum-Werte übereinstimmen. <li> `usual` </li> <li> `offical` </li> <li> `temp` </li> <li> `nickname` </li> <li> `anonymous` </li> <li> `old` </li> <li> `maiden` </li> |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/humanname.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/humanname.schema.json)
