---
title: Adressdatentyp
description: Erfahren Sie mehr über den Datentyp "Address Experience Data Model (XDM)".
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 10%

---

# Datentyp [!UICONTROL Adresse]

[!UICONTROL Adresse] ist ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der eine Adresse beschreibt, die mithilfe von Postkonventionen (im Gegensatz zu GPS oder anderen Standortdefinitionsformaten) ausgedrückt wird. Dieser Datentyp wird gemäß den Spezifikationen von HL7 FHIR Release 5 erstellt.

![Struktur des Adressdatentyps](../../images/data-types/healthcare/address.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Zeitraum] | `period` | [[!UICONTROL Zeitraum]](../healthcare/period.md) | Zeitraum, in dem die Adresse verwendet wurde/wird. |
| [!UICONTROL Ort] | `city` | String | Name der Stadt. |
| [!UICONTROL Country] | `country` | String | Der Ländercode, der in der internationalen ISO-Norm 3166 beschrieben ist. Der Code kann entweder Alpha-2 oder Alpha-3 sein. |
| [!UICONTROL District] | `district` | String | Der Bezirksname. |
| [!UICONTROL Zeile] | `line` | String | Straßenname, Nummer, Richtung, Postfach oder Ähnliches. |
| [!UICONTROL Postleitzahl] | `postalCode` | String | Postleitzahl. |
| [!UICONTROL state] | `state` | String | Die Untereinheit eines Landes. Abkürzungen sind akzeptabel. |
| [!UICONTROL Text] | `text` | String | Die Textdarstellung der Adresse. |
| [!UICONTROL Typ] | `type` | String | Der Adresstyp. Der Wert dieser Eigenschaft muss mit einem der folgenden bekannten Enum-Werte übereinstimmen. <li> `postal` </li> <li> `physical` </li> <li> `both` </li> |
| [!UICONTROL Use] | `use` | String | Der Zweck der Adresse. Der Wert dieser Eigenschaft muss mit einem der folgenden bekannten Enum-Werte übereinstimmen. <li> `home` </li> <li> `work` </li> <li> `temp` </li> <li> `old`</li> <li> `billing`</li> |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/address.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/address.schema.json)
