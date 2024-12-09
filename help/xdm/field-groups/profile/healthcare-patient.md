---
title: Patientenschema-Feldergruppe
description: Erfahren Sie mehr über die Feldgruppe Patientenschema .
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: e01a6cd4cf42338f87222a5e2871cd6c3683309a
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 8%

---

# [!UICONTROL Patienten] Schemafeldgruppe

[!UICONTROL Patient] ist eine Standardschemafeldgruppe für die [[!DNL XDM Individual Profile] Klasse](../../classes/individual-profile.md). Es bietet ein einzelnes Objektfeld `healthcarePatient` , das die demografischen Daten und andere Verwaltungsdetails über eine Person oder ein Tier erfasst, die bzw. das Pflege oder andere gesundheitsbezogene Dienstleistungen erhält.

![Feldgruppenstruktur](../../images/field-groups/patient.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Adresse] | `address` | Array von [[!UICONTROL Adresse]](../../data-types/healthcare/address.md) | Die Adressinformationen für den Patienten. |
| [!UICONTROL Kommunikation] | `communication` | Array von Objekten | Eine Sprache, die zur Kommunikation mit dem Patienten über seine Gesundheit verwendet werden kann. Weitere Informationen finden Sie im Abschnitt [unter ](#communication) . |
| [!UICONTROL Patientenkontakte] | `contact` | Array von Objekten | eine Kontaktperson des Patienten, z. B. einen Vormund, Partner oder Freund. Weitere Informationen finden Sie im Abschnitt [unter ](#contact) . |
| [!UICONTROL General Practitioner] | `generalPractioner` | Array von [[!UICONTROL Verweis]](../../data-types/healthcare/reference.md) | Der primäre Pflegedienst des Patienten. |
| [!UICONTROL ID] | `identifier` | Array von [[!UICONTROL Bezeichner]](../../data-types/healthcare/identifier.md) | Eine Kennung für den Patienten. |
| [!UICONTROL Details zum Patientenlink] | `link` | Array von Objekten | Ein Link zur Ressource eines Patienten oder einer verwandten Person, der bzw. die dieselbe Person betrifft. Weitere Informationen finden Sie im Abschnitt [unter ](#link) . |
| [!UICONTROL Verwalten der Organisation] | `managingOrganization` | [[!UICONTROL Referenz]](../../data-types/healthcare/reference.md) | Die freiheitsentziehende Organisation der Patientenakte. |
| [!UICONTROL Familienstand] | `maritalStatus` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Der Familienstand des Patienten. |
| [!UICONTROL Name] | `name` | Array von [[!UICONTROL Human name]](../../data-types/healthcare/human-name.md) | Der mit dem Patienten verbundene Name. |
| [!UICONTROL Kontaktdetails] | `telecom` | Array von [[!UICONTROL Kontaktpunkt]](../../data-types/healthcare/contact-point.md) | Angabe des Kontakts, z. B. Telefonnummer oder E-Mail-Adresse, über die der Patient kontaktiert werden kann. |
| [!UICONTROL ist aktiv] | `active` | Boolesch | Gibt an, ob der Datensatz des Patienten aktiv verwendet wird. |
| [!UICONTROL Geburtsdatum] | `birthDate` | Datum | Das Geburtsdatum des Patienten. |
| [!UICONTROL  veralteter Indikator] | `deceasedBoolean` | Boolesch | Gibt an, ob der Patient verstorben ist oder nicht. |
| [!UICONTROL Verfallsdatum/Uhrzeit] | `deceasedDateTime` | DateTime | Datum und Uhrzeit des Todes des Patienten. |
| [!UICONTROL Geschlecht] | `gender` | String | Die Geschlechtsidentität der Person. Der Wert dieser Eigenschaft muss mit einem der folgenden bekannten Enum-Werte übereinstimmen. <li> `female` </li> <li> `male` </li> <li> `other` </li> <li> `unknown`</li> |
| [!UICONTROL ist Teil einer mehrfachen Geburt] | `multipleBirthBoolean` | Boolesch | Gibt an, ob der Patient Teil einer Mehrfachgeburt ist. |
| [!UICONTROL Geburtsnummer] | `multipleBirthInteger` | Ganzzahl | Die Geburtsnummer in der Sequenz. |

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/patient.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/patient.schema.json)

## `communication` {#communication}

`communication` wird als Array von Objekten bereitgestellt. Die Struktur der einzelnen Objekte wird nachfolgend beschrieben.

![Kommunikationsstruktur](../../images/field-groups/healthcare-patient/communication.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Sprache] | `language` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Die Sprache, die zur Kommunikation mit der Person über ihre Gesundheit verwendet werden kann. |
| [!UICONTROL Ist bevorzugte Sprache] | `preferred` | Boolesch | Gibt an, ob die Sprache ihre bevorzugte Sprache ist oder nicht. |

## `contact` {#contact}

`contact` wird als Array von Objekten bereitgestellt. Die Struktur der einzelnen Objekte wird nachfolgend beschrieben.

![Kontaktstruktur](../../images/field-groups/healthcare-patient/contact.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Kontaktadresse] | `address` | [[!UICONTROL Adresse]](../../data-types/healthcare/address.md) | Die Adresse der Kontaktperson. |
| [!UICONTROL Kontaktname] | `name` | [[!UICONTROL Menschenname]](../../data-types/healthcare/human-name.md) | Der Name der Kontaktperson. |
| [!UICONTROL Kontaktorganisation] | `organization` | [[!UICONTROL Referenz]](../../data-types/healthcare/reference.md) | Die mit der Kontaktperson verbundene Organisation. |
| [!UICONTROL Kontaktzeitraum] | `period` | [[!UICONTROL Zeitraum]](../../data-types/healthcare/period.md) | Der Zeitraum, in dem der Kontakt verwendet wurde oder wird. |
| [!UICONTROL Beziehung&#39;] | `relationship` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Beziehung zwischen Patient und Kontaktperson. |
| [!UICONTROL Kontaktdetails] | `telecom` | Array von Objekten | Die Kontaktdaten für die Kontaktperson. Weitere Informationen finden Sie im Abschnitt [unter ](#telecom) . |
| [!UICONTROL Geschlecht] | `gender` | String | Die Geschlechtsidentität der Person. Der Wert dieser Eigenschaft muss mit einem der folgenden bekannten Enum-Werte übereinstimmen. <li> `female` </li> <li> `male` </li> <li> `other` </li> <li> `unknown`</li> |

### `telecom` {#telecom}

`telecom` wird als Array von Objekten bereitgestellt. Die Struktur der einzelnen Objekte wird nachfolgend beschrieben.

![Telekommunikationsstruktur](../../images/field-groups/healthcare-patient/telecom.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Kontaktpunkt] | `contactPoint` | [[!UICONTROL Kontaktpunkt]](../../data-types/healthcare/contact-point.md) | Die Kontaktdaten für die Person. |

## `link` {#link}

`link` wird als Array von Objekten bereitgestellt. Die Struktur der einzelnen Objekte wird nachfolgend beschrieben.

![Linkstruktur](../../images/field-groups/healthcare-patient/link.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Sonstige] | `other` | [[!UICONTROL Referenz]](../../data-types/healthcare/reference.md) | Ein Link zur Ressource eines Patienten oder einer verwandten Person, der bzw. die dieselbe Person betrifft. |
| [!UICONTROL Typ] | `type` | String | Die Art des Zusammenhangs zwischen den beiden Patientenressourcen. |
