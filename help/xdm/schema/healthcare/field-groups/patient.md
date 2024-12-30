---
title: Feldgruppe des Patientenschemas
description: Erfahren Sie mehr über die Feldergruppe des Patientenschemas.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: eba7deb3-4785-4d05-86ef-0f6691fcd2c5
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 8%

---

# [!UICONTROL Patient] Schemafeldgruppe

[!UICONTROL Patient] ist eine Standardschemafeldgruppe für die Klasse [[!DNL XDM Individual Profile] ](../../../classes/individual-profile.md). Es bietet ein einzelnes Objektfeldmodell, `healthcarePatient` demografische und andere administrative Details über eine Person oder ein Tier erfasst, die bzw. das Pflege- oder andere gesundheitsbezogene Dienstleistungen erhält.

![Feldergruppenstruktur](../../../images/healthcare/field-groups/patient/patient.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Adresse] | `address` | Array von [[!UICONTROL Adresse]](../data-types/address.md) | Die Adressinformationen für den Patienten. |
| [!UICONTROL Kommunikation] | `communication` | Array von Objekten | Eine Sprache, die verwendet werden kann, um mit dem Patienten über dessen Gesundheit zu kommunizieren. Weitere Informationen finden [ im ](#communication) Abschnitt unten. |
| [!UICONTROL Patientenkontakte] | `contact` | Array von Objekten | Die Kontaktperson eines Patienten, z. B. ein Vormund, Partner oder Freund. Weitere Informationen finden [ im ](#contact) Abschnitt unten. |
| [!UICONTROL Allgemeinmediziner] | `generalPractioner` | Array von [[!UICONTROL Referenz]](../data-types/reference.md) | Der Primärversorger des Patienten. |
| [!UICONTROL ID] | `identifier` | Array von [[!UICONTROL Identifier]](../data-types/identifier.md) | Eine Kennung für den Patienten. |
| [!UICONTROL Details zur Patientenverbindung] | `link` | Array von Objekten | Eine Relation zu einer Ressource eines Patienten oder einer mit ihm verbundenen Person, die dieselbe Person betrifft. Weitere Informationen finden [ im ](#link) Abschnitt unten. |
| [!UICONTROL Organisation verwalten] | `managingOrganization` | [[!UICONTROL Referenz]](../data-types/reference.md) | Die Aufbewahrungsorganisation der Patientenakte. |
| [!UICONTROL Familienstand] | `maritalStatus` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Der Familienstand des Patienten. |
| [!UICONTROL Name] | `name` | Array von [[!UICONTROL Menschlicher Name]](../data-types/human-name.md) | Der Name, der dem Patienten zugeordnet ist. |
| [!UICONTROL Kontaktdaten] | `telecom` | Array von [[!UICONTROL Kontaktpunkt]](../data-types/contact-point.md) | Ein Kontaktdetail, wie eine Telefonnummer oder E-Mail-Adresse, über das der Patient kontaktiert werden kann. |
| [!UICONTROL Ist aktiv] | `active` | Boolesch | Zeigt an, ob die Patientenakte aktiv verwendet wird. |
| [!UICONTROL Geburtsdatum] | `birthDate` | Datum | Das Geburtsdatum des Patienten. |
| [!UICONTROL Indikator für Verstorben] | `deceasedBoolean` | Boolesch | Zeigt an, ob der Patient verstorben ist oder nicht. |
| [!UICONTROL Datum/Uhrzeit des ] | `deceasedDateTime` | DateTime | Datum und Uhrzeit des Todes des Patienten. |
| [!UICONTROL Geschlecht] | `gender` | String | Die Geschlechtsidentität der Person. Der Wert dieser Eigenschaft muss einem der folgenden bekannten Enum-Werte entsprechen. <li> `female` </li> <li> `male` </li> <li> `other` </li> <li> `unknown`</li> |
| [!UICONTROL Ist Teil einer Mehrfachgeburt] | `multipleBirthBoolean` | Boolesch | Zeigt an, ob der Patient Teil einer Mehrfachgeburt ist. |
| [!UICONTROL Geburtsnummer] | `multipleBirthInteger` | Ganzzahl | Die Geburtsnummer in der Sequenz. |

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/patient.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/patient.schema.json)

## `communication` {#communication}

`communication` wird als Array von -Objekten bereitgestellt. Im Folgenden wird die Struktur der einzelnen Objekte beschrieben.

![Kommunikationsstruktur](../../../images/healthcare/field-groups/patient/communication.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Sprache] | `language` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Die Sprache, die verwendet werden kann, um mit der Person über ihre Gesundheit zu kommunizieren. |
| [!UICONTROL Ist bevorzugte Sprache] | `preferred` | Boolesch | Gibt an, ob die Sprache die bevorzugte Sprache ist. |

## `contact` {#contact}

`contact` wird als Array von -Objekten bereitgestellt. Im Folgenden wird die Struktur der einzelnen Objekte beschrieben.

![Kontaktstruktur](../../../images/healthcare/field-groups/patient/contact.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Kontaktadresse] | `address` | [[!UICONTROL Adresse]](../data-types/address.md) | Die Adresse der Kontaktperson. |
| [!UICONTROL Kontaktname] | `name` | [[!UICONTROL Menschlicher Name]](../data-types/human-name.md) | Der Name der Kontaktperson. |
| [!UICONTROL Kontaktorganisation] | `organization` | [[!UICONTROL Referenz]](../data-types/reference.md) | Die Organisation, die mit der Kontaktperson verknüpft ist. |
| [!UICONTROL Kontaktzeit] | `period` | [[!UICONTROL Zeitraum]](../data-types/period.md) | Der Zeitraum, in dem der Kontakt verwendet wurde oder wird. |
| [!UICONTROL Beziehung“] | `relationship` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Die Beziehung zwischen dem Patienten und der Kontaktperson. |
| [!UICONTROL Kontaktdaten] | `telecom` | Array von Objekten | Die Kontaktdaten für die Kontaktperson. Weitere Informationen finden [ im ](#telecom) Abschnitt unten. |
| [!UICONTROL Geschlecht] | `gender` | String | Die Geschlechtsidentität der Person. Der Wert dieser Eigenschaft muss einem der folgenden bekannten Enum-Werte entsprechen. <li> `female` </li> <li> `male` </li> <li> `other` </li> <li> `unknown`</li> |

### `telecom` {#telecom}

`telecom` wird als Array von -Objekten bereitgestellt. Im Folgenden wird die Struktur der einzelnen Objekte beschrieben.

![Telekom-Struktur](../../../images/healthcare/field-groups/patient/telecom.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Kontaktstelle] | `contactPoint` | [[!UICONTROL Kontaktstelle]](../data-types/contact-point.md) | Die Kontaktdaten für die Person. |

## `link` {#link}

`link` wird als Array von -Objekten bereitgestellt. Im Folgenden wird die Struktur der einzelnen Objekte beschrieben.

![Relationsstruktur](../../../images/healthcare/field-groups/patient/link.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Sonstige] | `other` | [[!UICONTROL Referenz]](../data-types/reference.md) | Eine Relation zu einer Ressource eines Patienten oder einer mit ihm verbundenen Person, die dieselbe Person betrifft. |
| [!UICONTROL Typ] | `type` | String | Die Art der Verbindung zwischen den beiden Patientenressourcen. |
