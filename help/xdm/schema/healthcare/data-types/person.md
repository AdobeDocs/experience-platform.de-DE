---
title: Datentyp der Person
description: Erfahren Sie mehr über den Datentyp des Experience-Datenmodells (XDM) für Personen.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: a19823f2-25d0-45cb-86f4-7816041b27f9
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 8%

---

# [!UICONTROL Person] Datentyp

[!UICONTROL Person] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Informationen zu einem generischen Personendatensatz bereitstellt. Dieser Datentyp wird gemäß den HL7 FHIR Release 5-Spezifikationen erstellt.

![Struktur des Datentyps für Personen](../../../images/healthcare/data-types/person/person.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Adresse] | `address` | Array von [[!UICONTROL Adresse]](../data-types/address.md) | Eine oder mehrere Adressen für die Person. |
| [!UICONTROL Kommunikation] | `communication` | Array von Objekten | Eine Sprache, die verwendet werden kann, um mit der Person über ihre Gesundheit zu kommunizieren. Weitere Informationen finden [ im ](#communication) Abschnitt unten. |
| [!UICONTROL ID] | `identifier` | Array von [[!UICONTROL Identifier]](../data-types/identifier.md) | Eine menschliche Kennung für diese Person. |
| [!UICONTROL Personen-Link-Details] | `link` | Array von Objekten | Ein Link zu einer Ressource, die dieselbe tatsächliche Person betrifft. Weitere Informationen finden [ im ](#link) Abschnitt unten. |
| [!UICONTROL Organisation verwalten] | `managingOrganization` | [[!UICONTROL Referenz]](../data-types/reference.md) | Die Organisation, die die Patientenakte verwaltet. |
| [!UICONTROL Familienstand] | `maritalStatus` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Der Familienstand (oder der bürgerliche Status) einer Person |
| [!UICONTROL Name] | `name` | Array von [[!UICONTROL Human Name]](../data-types/human-name.md) | Die mit einer Person verknüpften Namen. |
| [!UICONTROL Kontaktdaten] | `telecom` | Array von [[!UICONTROL Contact Point]] | Die Kontaktdaten, über die die Person kontaktiert werden kann. |
| [!UICONTROL Ist aktiv] | `active` | Boolesch | Gibt an, ob der Datensatz der Person aktiv verwendet wird. |
| [!UICONTROL Geburtsdatum] | `birthDate` | Datum | Das Geburtsdatum der Person. |
| [!UICONTROL Indikator für Verstorben] | `deceasedBoolean` | Boolesch | Zeigt an, ob die Person verstorben ist oder nicht. |
| [!UICONTROL Datum/Uhrzeit des ] | `deceasedDateTime` | DateTime | Datum und Uhrzeit des Todes des Verstorbenen. |
| [!UICONTROL Geschlecht] | `gender` | String | Die Geschlechtsidentität der Person. Der Wert dieser Eigenschaft muss einem der folgenden bekannten Enum-Werte entsprechen. <li> `female` </li> <li> `male` </li> <li> `other` </li> <li> `unknown`</li> |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/identifier.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/identifier.schema.json)

## `communication` {#communication}

`communication` wird als Array von -Objekten bereitgestellt. Im Folgenden wird die Struktur der einzelnen Objekte beschrieben.

![Kommunikationsstruktur](../../../images/healthcare/data-types/person/communication.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Sprache] | `language` | [[!UICONTROL Codeable-Konzept]](../data-types/codeable-concept.md) | Die Sprache, die verwendet werden kann, um mit der Person über ihre Gesundheit zu kommunizieren. |
| [!UICONTROL Ist bevorzugte Sprache] | `preferred` | Boolesch | Gibt an, ob die Sprache die bevorzugte Sprache ist. |

## `link` {#link}

`link` wird als Array von -Objekten bereitgestellt. Im Folgenden wird die Struktur der einzelnen Objekte beschrieben.

![Relationsstruktur](../../../images/healthcare/data-types/person/link.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Zielgruppe] | `target` | [[!UICONTROL Referenz]](../data-types/reference.md) | Die Ressource, mit der diese tatsächliche Person verknüpft ist. |
| [!UICONTROL Assurance] | `assurance` | String | Die mit dem Link verknüpfte Sicherheitsstufe. Die Werte dieser Eigenschaft müssen mindestens einem der folgenden bekannten Enum-Werte entsprechen. <li> `level1` </li> <li> `level2` </li> <li> `level3` </li> <li> `level4` </li> |
