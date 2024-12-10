---
title: Datentyp "Kontaktpunkt"
description: Erfahren Sie mehr über den Datentyp "Contact Point Experience Data Model (XDM)".
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: bbb9a5e1-b0d5-4c07-93a9-c1573dacad73
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 7%

---

# Datentyp [!UICONTROL Kontaktpunkt]

[!UICONTROL Kontaktpunkt] ist ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der Kontaktdetails für eine Person beschreibt. Dieser Datentyp wird gemäß den Spezifikationen von HL7 FHIR Release 5 erstellt.

![Datentypstruktur für Kontaktpunkte](../../../images/healthcare/data-types/contact-point.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Zeitraum] | `period` | [[!UICONTROL Zeitraum]](../data-types/period.md) | Der Zeitraum, in dem der Kontaktpunkt verwendet wurde/wird. |
| [!UICONTROL Rang] | `rank` | Ganzzahl | Der Rang, der die bevorzugte Verwendung des Kontaktpunkts angibt. Der Mindestwert ist `1` und der Höchstwert ist `2147483647`, wobei `1` die höchste Spezifität ist. |
| [!UICONTROL System] | `system` | String | Das System, über das sie kontaktiert werden können. Der Wert dieser Eigenschaft muss mit einem der folgenden bekannten Enum-Werte übereinstimmen. <li> `phone` </li> <li> `fax` </li> <li> `email` </li> <li> `pager`</li> <li> `url`</li> <li> `sms`</li> <li> `other`</li> |
| [!UICONTROL Use] | `use` | String | Der Zweck der Kontaktstelle. Der Wert dieser Eigenschaft muss mit einem der folgenden bekannten Enum-Werte übereinstimmen. <li> `home` </li> <li> `work` </li> <li> `temp` </li> <li> `old`</li> <li> `mobile`</li> |
| [!UICONTROL Wert] | `value` | String | Die Details der Kontaktstelle. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/contactpoint.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/contactpoint.schema.json)
