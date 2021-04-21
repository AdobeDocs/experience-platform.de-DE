---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;Felder;Schemas;Schemas;Person;Datentyp;Datentyp; Datentyp;
solution: Experience Platform
title: Datentyp der Person
topic-legacy: overview
description: Dieses Dokument bietet eine Übersicht über den Datentyp des Personenerlebnis-Datenmodells (XDM).
exl-id: f28a52be-90c7-4ed0-a460-97165bb58046
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 16%

---

#  Persondata-Typ

 Personis a standard Experience Data Model (XDM) data type, der eine Person beschreibt. Dieser Datentyp kann eine Person darstellen, die in verschiedenen Rollen handelt, z. B. Kunden, Ansprechpartner oder Eigentümer.

<img src="../images/data-types/person.PNG" width="500" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `name` | [[!UICONTROL Personenname]](./person-name.md) | Beschreibt Details zum vollständigen Namen der Person. |
| `birthDate` | Datum | Das vollständige Datum, an dem eine Person geboren wurde. Das Datumsformat (ohne Uhrzeit) sollte dem Standard [RFC 3339, Abschnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) entsprechen. |
| `birthDayAndMonth` | Zeichenfolge | Der Tag und Monat, an dem eine Person geboren wurde, im Format MM-TT. Dieses Feld sollte verwendet werden, wenn der Geburtstag und -monat bekannt sind, nicht aber das Jahr. Das Format dieser Eigenschaft muss diesem regulären Ausdruck `[0-1][0-9]-[0-9][0-9]` entsprechen. |
| `birthYear` | Ganzzahl | Das Jahr, in dem eine Person geboren wurde, einschließlich des Jahrhunderts (z. B. `1983`). Dieses Feld sollte verwendet werden, wenn nur das Alter der Person bekannt ist und nicht das vollständige Geburtsdatum. Dieser Wert muss zwischen 1 und 32767 liegen. |
| `gender` | Zeichenfolge | Die Geschlechtsidentität der Person. Der Wert dieser Eigenschaft muss mit einem der folgenden bekannten Enum-Werte übereinstimmen. <li> `female` </li> <li> `male` </li> <li> `not_specified` </li> <li> `non_specific` </li> Der Standardwert für diesen Wert ist `not_specified`. |
| `maritalStatus` | Zeichenfolge | Beschreibt die Beziehung einer Person zu einer bedeutenden anderen Person. Der Wert dieser Eigenschaft muss mit einem der folgenden Enum-Werte übereinstimmen. <li> `married` </li> <li> `single` </li> <li> `divorced` </li> <li> `widowed` </li> <li> `not_specified` </li> Der Standardwert für diesen Wert ist `not_specified`. |
| `nationality` | Zeichenfolge | Die Rechtsbeziehung zwischen einer Person und ihrem Status, die durch den ISO-Code 3166-1 Alpha-2 repräsentiert wird. Das Format dieser Eigenschaft muss diesem regulären Ausdruck `^[A-Z]{2}$` entsprechen. |
| `taxId` | Zeichenfolge | Steuer- oder Steuer-/Steuer-ID der Person, z. B. TIN (Taxpayer Identification Number) in den USA oder Certificado de Identificación Fiscal (CIF/NIF) in Spanien. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.schema.json)
