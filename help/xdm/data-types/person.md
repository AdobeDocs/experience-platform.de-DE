---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Person; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Datentyp Person
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über den Daten-Typ des Personen-Experience-Datenmodells (XDM).
exl-id: f28a52be-90c7-4ed0-a460-97165bb58046
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 21%

---

# [!UICONTROL Person] Datentyp

[!UICONTROL Person] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der eine Person beschreibt. Dieser Datentyp kann eine Person darstellen, die in verschiedenen Rollen agiert, z. B. ein Kunde, ein Kontakt oder ein Eigentümer.

<img src="../images/data-types/person.PNG" width="500" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `name` | [[!UICONTROL Personenname]](./person-name.md) | Beschreibt Details zum vollständigen Namen der Person. |
| `birthDate` | Datum | Das vollständige Datum, an dem eine Person geboren wurde. Das Datumsformat (ohne Uhrzeit) sollte dem [RFC 3339, Abschnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) Standard. |
| `birthDayAndMonth` | Zeichenfolge | Der Tag und Monat, an dem eine Person geboren wurde, im Format MM-TT. Dieses Feld sollte verwendet werden, wenn der Geburtstag und -monat bekannt sind, nicht aber das Jahr. Das Format dieser Eigenschaft muss diesem regulären Ausdruck entsprechen `[0-1][0-9]-[0-9][0-9]`. |
| `birthYear` | Ganzzahl | Das Jahr, in dem eine Person geboren wurde, einschließlich des Jahrhunderts (z. B. `1983`). Dieses Feld sollte verwendet werden, wenn nur das Alter der Person bekannt ist und nicht das vollständige Geburtsdatum. Dieser Wert muss zwischen 1 und 32767 liegen. |
| `gender` | Zeichenfolge | Die Geschlechtsidentität der Person. Der Wert dieser Eigenschaft muss mit einem der folgenden bekannten Enum-Werte übereinstimmen. <li> `female` </li> <li> `male` </li> <li> `not_specified` </li> <li> `non_specific` </li> Der Standardwert für diesen Wert ist `not_specified`. |
| `maritalStatus` | Zeichenfolge | Beschreibt die Beziehung einer Person zu einer wichtigen anderen. Der Wert dieser Eigenschaft muss mit einem der folgenden Enum-Werte übereinstimmen. <li> `married` </li> <li> `single` </li> <li> `divorced` </li> <li> `widowed` </li> <li> `not_specified` </li> Der Standardwert für diesen Wert ist `not_specified`. |
| `nationality` | Zeichenfolge | Die Rechtsbeziehung zwischen einer Person und ihrem Staat, der anhand des ISO 3166-1 Alpha-2-Codes dargestellt wird. Das Format dieser Eigenschaft muss diesem regulären Ausdruck entsprechen `^[A-Z]{2}$`. |
| `taxId` | Zeichenfolge | Die Steuer- oder Steuerkennung der Person, wie z. B. die Identifikationsnummer des Steuerpflichtigen (TIN) in den USA oder das Certificate de Identificación Fiscal (CIF/NIF) in Spanien. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.schema.json)
