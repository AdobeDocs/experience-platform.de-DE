---
title: Adresstyp
description: Erfahren Sie mehr über den Datentyp „Experience-Adressdatenmodell“ (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 21213bd5-00f4-43cc-80cf-2c0dcf878a23
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 10%

---

# [!UICONTROL Adresse] Datentyp

[!UICONTROL Adresse] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der eine Adresse beschreibt, die mithilfe von Postkonventionen (im Gegensatz zu GPS oder anderen Standortdefinitionsformaten) ausgedrückt wird. Dieser Datentyp wird gemäß den HL7 FHIR Release 5-Spezifikationen erstellt.

![Struktur des Datentyps „Adresse“](../../../images/healthcare/data-types/address.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Zeitraum] | `period` | [[!UICONTROL Zeitraum]](../data-types/period.md) | Zeitraum, in dem die Adresse verwendet wurde/wird. |
| [!UICONTROL Stadt] | `city` | String | Name der Stadt. |
| [!UICONTROL Country] | `country` | String | Der Ländercode, der in der internationalen ISO-Norm 3166 beschrieben ist. Der Code kann entweder alpha-2 oder alpha-3 sein. |
| [!UICONTROL Bezirk] | `district` | String | Der Bezirksname. |
| [!UICONTROL Zeile] | `line` | String | Der Straßenname, die Nummer, die Richtung, das Postfach oder Ähnliches. |
| [!UICONTROL Postleitzahl] | `postalCode` | String | Die Postleitzahl. |
| [!UICONTROL state] | `state` | String | Die Untereinheit eines Landes. Abkürzungen sind zulässig. |
| [!UICONTROL Text] | `text` | String | Die Textdarstellung der Adresse. |
| [!UICONTROL Typ] | `type` | String | Der Adresstyp. Der Wert dieser Eigenschaft muss einem der folgenden bekannten Enum-Werte entsprechen. <li> `postal` </li> <li> `physical` </li> <li> `both` </li> |
| [!UICONTROL Verwenden] | `use` | String | Der Zweck der Adresse. Der Wert dieser Eigenschaft muss einem der folgenden bekannten Enum-Werte entsprechen. <li> `home` </li> <li> `work` </li> <li> `temp` </li> <li> `old`</li> <li> `billing`</li> |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/address.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/address.schema.json)
