---
title: Praktische Schemafeldgruppe
description: Erfahren Sie mehr über die Feldergruppe Praktioner-Schema .
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 71210303-a3dd-458c-9c8a-ac8b546c2b1d
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 8%

---

# [!UICONTROL Praktioner] Schemafeldgruppe

[!UICONTROL Praktioner] ist eine Standardschemafeldgruppe für die [[!DNL XDM Individual Profile] Klasse](../../../classes/individual-profile.md) und die [[!DNL Provider class]](../../../classes/provider.md). Es stellt ein einzelnes Objektfeld `healthcarePractioner` bereit, das Informationen über eine Person enthält, die direkt oder indirekt an der Bereitstellung von Gesundheitsdienstleistungen oder verwandten Dienstleistungen beteiligt ist.

![Feldgruppenstruktur](../../../images/healthcare/field-groups/practitioner/practitioner.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Adresse] | `address` | Array von [[!UICONTROL Adresse]](../data-types/address.md) | Anschrift(en) des Praktikanten, die außerhalb seines Arbeitsplatzes liegen, z. B. Hausanschrift. |
| [!UICONTROL Kommunikation] | `communication` | Array von Objekten | Eine Sprache, die zur Kommunikation mit dem Praktiker verwendet werden kann. Weitere Informationen finden Sie im Abschnitt [unter ](#communication) . |
| [!UICONTROL ID] | `identifier` | Array von [[!UICONTROL Bezeichner]](../data-types/identifier.md) | Eine Kennung, die für diese Person in dieser Rolle gilt. |
| [!UICONTROL Name] | `name` | Array von [[!UICONTROL Human Name]](../data-types/human-name.md) | Die mit dem Praktiker verknüpften Namen. |
| [!UICONTROL Qualifikation] | `qualification` | Array von Objekten | Die amtlichen Qualifikationen, Zertifizierungen, Akkreditierungen, Schulungen, Lizenzen oder Ähnliches, die die Betreuung durch den Praktiker zulassen oder anderweitig betreffen. Weitere Informationen finden Sie im Abschnitt [unter ](#qualification) . |
| [!UICONTROL Kontaktdetails] | `telecom` | Array von [[!UICONTROL Kontaktpunkt]](../data-types/contact-point.md) | Die Kontaktdaten für den Praktiker. |
| [!UICONTROL Aktiv] | `active` | Boolesch | Gibt an, ob der von den Praktikern aufgenommene Eintrag aktiv verwendet wird. |
| [!UICONTROL Geburtsdatum] | `birthDate` | Datum | Das Geburtsdatum des Praktikanten. |
| [!UICONTROL  veralteter Indikator] | `deceasedBoolean` | Boolesch | Gibt an, ob der Praktiker verstorben ist. |
| [!UICONTROL Verfallsdatum/Uhrzeit] | `deceasedDateTime` | DateTime | Datum und Uhrzeit des Todes des Praktikanten. |
| [!UICONTROL Geschlecht] | `gender` | String | Die Geschlechtsidentität der Person. Der Wert dieser Eigenschaft muss mit einem der folgenden bekannten Enum-Werte übereinstimmen. <li> `female` </li> <li> `male` </li> <li> `other` </li> <li> `unknown`</li> |

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/practitioner.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/practitioner.schema.json)

## `communication` {#communication}

`communication` wird als Array von Objekten bereitgestellt. Die Struktur der einzelnen Objekte wird nachfolgend beschrieben.

![Kommunikationsstruktur](../../../images/healthcare/field-groups/practitioner/communication.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Sprache] | `language` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Die Sprache, die zur Kommunikation mit der Person über ihre Gesundheit verwendet werden kann. |
| [!UICONTROL Ist bevorzugte Sprache] | `preferred` | Boolesch | Gibt an, ob die Sprache ihre bevorzugte Sprache ist oder nicht. |

## `qualification` {#qualification}

`qualification` wird als Array von Objekten bereitgestellt. Die Struktur der einzelnen Objekte wird nachfolgend beschrieben.

![Qualifikationsstruktur](../../../images/healthcare/field-groups/practitioner/qualification.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Die kodierte Darstellung der Qualifizierung. |
| [!UICONTROL ID] | `identifier` | Array von [[!UICONTROL Bezeichner]](../data-types/identifier.md) | Eine Kennung für die Qualifikation. |
| [!UICONTROL Aussteller] | `issuer` | [[!UICONTROL Referenz]](../data-types/reference.md) | Die Organisation, die die Qualifikation reguliert und ausstellt. |
| [!UICONTROL Zeitraum] | `period` | [[!UICONTROL Zeitraum]](../data-types/period.md) | Der Gültigkeitszeitraum der Qualifikation. |
