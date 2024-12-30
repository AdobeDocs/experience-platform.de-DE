---
title: Datentyp des menschlichen Namens
description: Erfahren Sie mehr über den Datentyp des menschlichen Experience-Datenmodells (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 5dd6fda4-c076-4c34-bdd9-259203b6ea73
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 6%

---

# [!UICONTROL Menschlicher Name] Datentyp

[!UICONTROL Menschlicher Name] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Informationen zum Namen eines Menschen oder einer anderen lebenden Entität bereitstellt. Dieser Datentyp wird gemäß den HL7 FHIR Release 5-Spezifikationen erstellt.

![Datentypstruktur „Menschlicher Name](../../../images/healthcare/data-types/human-name.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Zeitraum] | `period` | [[!UICONTROL Zeitraum]](../data-types/period.md) | Der Zeitraum, in dem der Name verwendet wird oder wurde. |
| [!UICONTROL Familie] | `family` | String | Die Familie oder der Familienname. |
| [!UICONTROL Vorgegeben] | `given` | Zeichenfolgen-Array | Der Vorname, einschließlich aller zweiten Vornamen. |
| [!UICONTROL Präfix] | `prefix` | Zeichenfolgen-Array | Alle Teile des Namens vor dem Vor- oder Vornamen. |
| [!UICONTROL Suffix] | `suffix` | Zeichenfolgen-Array | Alle Teile des Namens nach der Familie oder dem Nachnamen. |
| [!UICONTROL Text] | `text` | String | Die Textdarstellung des vollständigen Namens. |
| [!UICONTROL Verwenden] | `use` | String | Die Verwendung des Namens. Die Werte dieser Eigenschaft müssen mindestens einem der folgenden bekannten Enum-Werte entsprechen. <li> `usual` </li> <li> `offical` </li> <li> `temp` </li> <li> `nickname` </li> <li> `anonymous` </li> <li> `old` </li> <li> `maiden` </li> |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/humanname.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/humanname.schema.json)
