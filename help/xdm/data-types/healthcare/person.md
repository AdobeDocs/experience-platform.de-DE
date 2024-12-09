---
title: Personendatentyp
description: Erfahren Sie mehr über den Datentyp des Personen-Experience-Datenmodells (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 8%

---

# Datentyp [!UICONTROL Person]

[!UICONTROL Person] ist ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der Informationen zu einem generischen Personendatensatz bereitstellt. Dieser Datentyp wird gemäß den Spezifikationen von HL7 FHIR Release 5 erstellt.

![Struktur des Datentyps &quot;Person&quot;](../../images/data-types/healthcare/person/person.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Adresse] | `address` | Array von [[!UICONTROL Adresse]](../healthcare/address.md) | Eine oder mehrere Adressen für die Person. |
| [!UICONTROL Kommunikation] | `communication` | Array von Objekten | Eine Sprache, die zur Kommunikation mit der Person über ihre Gesundheit verwendet werden kann. Weitere Informationen finden Sie im Abschnitt [unter ](#communication) . |
| [!UICONTROL ID] | `identifier` | Array von [[!UICONTROL Bezeichner]](../healthcare/identifier.md) | Eine menschliche Kennung für diese Person. |
| [!UICONTROL Details des Personen-Links] | `link` | Array von Objekten | Ein Link zu einer Ressource, die dieselbe Person betrifft. Weitere Informationen finden Sie im Abschnitt [unter ](#link) . |
| [!UICONTROL Verwalten der Organisation] | `managingOrganization` | [[!UICONTROL Referenz]](../healthcare/reference.md) | Die Organisation, die den Hüter des Patientendatensatzes ist. |
| [!UICONTROL Familienstand] | `maritalStatus` | [[!UICONTROL Codeable Concept]](../healthcare/codeable-concept.md) | Familienstand (oder zivil) einer Person |
| [!UICONTROL Name] | `name` | Array von [[!UICONTROL Human Name]](../healthcare/human-name.md) | Die Namen, die mit einer Person verknüpft sind. |
| [!UICONTROL Kontaktdetails] | `telecom` | Array von [[!UICONTROL Kontaktpunkt]] | Kontaktdaten, mit denen die Person kontaktiert werden kann. |
| [!UICONTROL ist aktiv] | `active` | Boolesch | Gibt an, ob der Datensatz der Person aktiv verwendet wird. |
| [!UICONTROL Geburtsdatum] | `birthDate` | Datum | Das Geburtsdatum der Person. |
| [!UICONTROL  veralteter Indikator] | `deceasedBoolean` | Boolesch | Gibt an, ob die Person verstorben ist oder nicht. |
| [!UICONTROL Verfallsdatum/Uhrzeit] | `deceasedDateTime` | DateTime | Datum und Uhrzeit des Todes, wenn die Person verstorben ist. |
| [!UICONTROL Geschlecht] | `gender` | String | Die Geschlechtsidentität der Person. Der Wert dieser Eigenschaft muss mit einem der folgenden bekannten Enum-Werte übereinstimmen. <li> `female` </li> <li> `male` </li> <li> `other` </li> <li> `unknown`</li> |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/identifier.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/identifier.schema.json)

## `communication` {#communication}

`communication` wird als Array von Objekten bereitgestellt. Die Struktur der einzelnen Objekte wird nachfolgend beschrieben.

![Kommunikationsstruktur](../../images/data-types/healthcare/person/communication.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Sprache] | `language` | [[!UICONTROL Codeable concept]](../../data-types/healthcare/codeable-concept.md) | Die Sprache, die zur Kommunikation mit der Person über ihre Gesundheit verwendet werden kann. |
| [!UICONTROL Ist bevorzugte Sprache] | `preferred` | Boolesch | Gibt an, ob die Sprache ihre bevorzugte Sprache ist oder nicht. |

## `link` {#link}

`link` wird als Array von Objekten bereitgestellt. Die Struktur der einzelnen Objekte wird nachfolgend beschrieben.

![Linkstruktur](../../images/data-types/healthcare/person/link.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Zielgruppe] | `target` | [[!UICONTROL Referenz]](../../data-types/healthcare/reference.md) | Die Ressource, mit der diese tatsächliche Person verknüpft ist. |
| [!UICONTROL Assurance] | `assurance` | String | Die mit dem Link verbundene Sicherheitsstufe. Die Werte dieser Eigenschaft müssen mit einem oder mehreren der folgenden bekannten Enum-Werte übereinstimmen. <li> `level1` </li> <li> `level2` </li> <li> `level3` </li> <li> `level4` </li> |
