---
title: Schemafeldgruppe des/r Praktizierenden
description: Erfahren Sie mehr über die Schemafeldgruppe „Anwender“.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 71210303-a3dd-458c-9c8a-ac8b546c2b1d
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 8%

---

# [!UICONTROL Practitioner] Schemafeldgruppe

[!UICONTROL Practitioner] ist eine Standardschemafeldgruppe für die [[!DNL XDM Individual Profile] class](../../../classes/individual-profile.md) und die [[!DNL Provider class]](../../../classes/provider.md). Es bietet ein einzelnes Objekttyp-Feld, `healthcarePractioner` Informationen über eine Person enthält, die direkt oder indirekt an der Bereitstellung von Gesundheitsdienstleistungen oder damit zusammenhängenden Dienstleistungen beteiligt ist.

![Feldergruppenstruktur](../../../images/healthcare/field-groups/practitioner/practitioner.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Adresse] | `address` | Array von [[!UICONTROL Adresse]](../data-types/address.md) | Anschrift(en) des Arztes, die außerhalb seines Arbeitsplatzes liegen, wie z. B. eine Privatanschrift. |
| [!UICONTROL Kommunikation] | `communication` | Array von Objekten | Eine Sprache, die für die Kommunikation mit dem Arzt verwendet werden kann. Weitere Informationen finden [ im ](#communication) Abschnitt unten |
| [!UICONTROL ID] | `identifier` | Array von [[!UICONTROL Identifier]](../data-types/identifier.md) | Eine Kennung, die für diese Person in dieser Rolle gilt. |
| [!UICONTROL Name] | `name` | Array von [[!UICONTROL Human Name]](../data-types/human-name.md) | Die Namen, die mit dem Praktizierenden verknüpft sind. |
| [!UICONTROL Qualifizierung] | `qualification` | Array von Objekten | Die offiziellen Qualifikationen, Zertifizierungen, Akkreditierungen, Schulungen, Lizenzen oder Ähnliches, die die Versorgung durch den Arzt genehmigen oder anderweitig betreffen. Weitere Informationen finden [ im ](#qualification) Abschnitt unten. |
| [!UICONTROL Kontaktdaten] | `telecom` | Array von [[!UICONTROL Kontaktpunkt]](../data-types/contact-point.md) | Die Kontaktdaten für den Arzt. |
| [!UICONTROL aktiv] | `active` | Boolesch | Gibt an, ob der Datensatz der medizinischen Fachkräfte aktiv verwendet wird. |
| [!UICONTROL Geburtsdatum] | `birthDate` | Datum | Das Geburtsdatum des Praktizierenden. |
| [!UICONTROL Indikator für Verstorben] | `deceasedBoolean` | Boolesch | Zeigt an, ob der Arzt verstorben ist. |
| [!UICONTROL Datum/Uhrzeit des ] | `deceasedDateTime` | DateTime | Datum und Uhrzeit des Todes des Praktizierenden. |
| [!UICONTROL Geschlecht] | `gender` | String | Die Geschlechtsidentität der Person. Der Wert dieser Eigenschaft muss einem der folgenden bekannten Enum-Werte entsprechen. <li> `female` </li> <li> `male` </li> <li> `other` </li> <li> `unknown`</li> |

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/practitioner.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/practitioner.schema.json)

## `communication` {#communication}

`communication` wird als Array von -Objekten bereitgestellt. Im Folgenden wird die Struktur der einzelnen Objekte beschrieben.

![Kommunikationsstruktur](../../../images/healthcare/field-groups/practitioner/communication.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Sprache] | `language` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Die Sprache, die verwendet werden kann, um mit der Person über ihre Gesundheit zu kommunizieren. |
| [!UICONTROL Ist bevorzugte Sprache] | `preferred` | Boolesch | Gibt an, ob die Sprache die bevorzugte Sprache ist. |

## `qualification` {#qualification}

`qualification` wird als Array von -Objekten bereitgestellt. Im Folgenden wird die Struktur der einzelnen Objekte beschrieben.

![Qualifizierungsstruktur](../../../images/healthcare/field-groups/practitioner/qualification.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Die codierte Darstellung der Qualifizierung. |
| [!UICONTROL ID] | `identifier` | Array von [[!UICONTROL Identifier]](../data-types/identifier.md) | Eine Kennung für die Qualifizierung. |
| [!UICONTROL Aussteller] | `issuer` | [[!UICONTROL Referenz]](../data-types/reference.md) | Die Organisation, die die Qualifizierung reguliert und ausstellt. |
| [!UICONTROL Zeitraum] | `period` | [[!UICONTROL Zeitraum]](../data-types/period.md) | Der Zeitraum, in dem die Qualifikation gültig ist. |
