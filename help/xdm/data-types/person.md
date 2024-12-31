---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;Felder;Schemata;Schemata;Person;Datentyp;Datentyp;Datentyp;
solution: Experience Platform
title: Datentyp der Person
description: Erfahren Sie mehr über den Datentyp des Experience-Datenmodells (XDM) für Personen.
exl-id: f28a52be-90c7-4ed0-a460-97165bb58046
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 7%

---

# [!UICONTROL Person] Datentyp

[!UICONTROL Person] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der eine einzelne Person beschreibt. Dieser Datentyp kann eine Person darstellen, die in verschiedenen Rollen agiert, z. B. als Kunde, Kontakt oder Inhaber.

<img src="../images/data-types/person.PNG" width="500" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `name` | [[!UICONTROL Personenname]](./person-name.md) | Beschreibt Details zum vollständigen Namen der Person. |
| `birthDate` | Datum | Das vollständige Datum, an dem eine Person geboren wurde. Das Datumsformat (ohne Zeit) sollte dem Standard [RFC 3339, Abschnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) entsprechen. |
| `birthDayAndMonth` | String | Der Tag und Monat, an dem eine Person geboren wurde, im Format MM-TT. Dieses Feld sollte verwendet werden, wenn der Geburtstag und -monat bekannt sind, nicht aber das Jahr. Das Format dieser Eigenschaft muss mit diesem `[0-1][0-9]-[0-9][0-9]` für reguläre Ausdrücke übereinstimmen. |
| `birthYear` | Ganzzahl | Das Jahr, in dem eine Person geboren wurde, einschließlich des Jahrhunderts (z. B. `1983`). Dieses Feld sollte verwendet werden, wenn nur das Alter der Person bekannt ist und nicht das vollständige Geburtsdatum. Dieser Wert muss zwischen 1 und 32767 liegen. |
| `gender` | String | Die Geschlechtsidentität der Person. Der Wert dieser Eigenschaft muss einem der folgenden bekannten Enum-Werte entsprechen. <li> `female` </li> <li> `male` </li> <li> `not_specified` </li> <li> `non_specific` </li> Der Standardwert für diesen Wert ist `not_specified`. |
| `maritalStatus` | String | Beschreibt die Beziehung einer Person zu einer bedeutenden anderen Person. Der Wert dieser Eigenschaft muss einem der folgenden Enum-Werte entsprechen. <li> `married` </li> <li> `single` </li> <li> `divorced` </li> <li> `widowed` </li> <li> `not_specified` </li> Der Standardwert für diesen Wert ist `not_specified`. |
| `nationality` | String | Die rechtliche Beziehung zwischen einer Person und ihrem Staat, dargestellt mit dem ISO 3166-1 Alpha-2-Code. Das Format dieser Eigenschaft muss mit diesem `^[A-Z]{2}$` für reguläre Ausdrücke übereinstimmen. |
| `taxId` | String | Die Steuernummer der Person, z. B. die Steuernummer (TIN) in den USA oder die Steuernummer (CIF/NIF) in Spanien. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.schema.json)
