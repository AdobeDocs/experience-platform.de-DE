---
title: Feldergruppe "Immunisierungsschema"
description: Erfahren Sie mehr über die Feldergruppe Immunisierungs-Schema .
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: a392e26b-7631-4f54-b9ad-cc4586673ac5
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 8%

---

# [!UICONTROL Immunisierung] Schemafeldgruppe

[!UICONTROL Immunisierung] ist eine Standardschemafeldgruppe für die [[!DNL XDM Experience Event] Klasse](../../../classes/experienceevent.md). Es stellt ein einzelnes Objektfeld `healthcareImmunization` bereit, das Informationen zu Impfereignissen erfasst.

![Feldgruppenstruktur](../../../images/healthcare/field-groups/immunization/immunization.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Verwaltetes Produkt] | `administeredProduct` | [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | Das verabreichte Produkt. |
| [!UICONTROL basierend auf ] | `basedOn` | Array von [[!UICONTROL Verweis]](../data-types/reference.md) | Die Autorität, auf der das Immunisierungsereignis basiert. |
| [!UICONTROL Dosismenge] | `doseQuantity` | [[!UICONTROL Einfache Menge]](../data-types/simple-quantity.md) | Die verabreichte Impfstoffmenge. |
| [!UICONTROL Encounter] | `encounter` | [[!UICONTROL Referenz]](../data-types/reference.md) | Die Begegnung mit der Immunisierung war Teil des Projekts. |
| [!UICONTROL Source finanzieren] | `fundingSource` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Die Finanzierungsquelle für den Impfstoff. |
| [!UICONTROL ID] | `identifier` | Array von [[!UICONTROL Bezeichner]](../data-types/identifier.md) | Die Geschäftskennung. |
| [!UICONTROL Information Source] | `informationSource` | [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | Gibt die Quelle des gemeldeten Datensatzes an. |
| [!UICONTROL Ort] | `location` | [[!UICONTROL Referenz]](../data-types/reference.md) | Der Ort, an dem die Immunisierung erfolgte. |
| [!UICONTROL Hersteller] | `manufacturer` | [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | Der Impfstoffhersteller. |
| [!UICONTROL Hinweis] | `note` | Array von [[!UICONTROL Anmerkung]](../data-types/annotation.md) | Zusätzliche Hinweise zur Immunisierung. |
| [!UICONTROL Patient] | `patient` | [[!UICONTROL Referenz]](../data-types/reference.md) | Wer war immun. |
| [!UICONTROL Batch] | `performer` | Array von Objekten | Personen, die die Immunisierung durchgeführt haben. Weitere Informationen finden Sie im Abschnitt [unter ](#performer) . |
| [!UICONTROL Programmteilnahmeberechtigung] | `programEligibility` | Array von Objekten | Der Patient ist für ein spezifisches Impfprogramm qualifiziert. Weitere Informationen finden Sie im Abschnitt [unter ](#program-eligibility) . |
| [!UICONTROL Angewandtes Protokoll] | `protocolApplied` | Array von Objekten | Das vom Provider bereitgestellte Protokoll. Weitere Informationen finden Sie im Abschnitt [unter ](#protocol-applied) . |
| [!UICONTROL Reaction] | `reaction` | Array von Objekten | Die Details einer Reaktion nach der Immunisierung. Weitere Informationen finden Sie im Abschnitt [unter ](#reaction) . |
| [!UICONTROL Grund] | `reason` | Array von [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | Der Grund für die Immunisierung. |
| [!UICONTROL Route] | `route` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Wie der Impfstoff in den Körper gelangt ist. |
| [!UICONTROL Site] | `site` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Die Körperstelle, an der der Impfstoff verabreicht wurde |
| [!UICONTROL Statusgrund] | `statusReason` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Der Grund für den aktuellen Status. |
| [!UICONTROL Subpotenzgrund] | `subpotentReason` | Array von [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Der Grund dafür, dass der Impfstoff subaktiv ist. |
| [!UICONTROL Unterstützende Informationen] | `supportingInformation` | Array von [[!UICONTROL Verweis]](../data-types/reference.md) | Zusätzliche Informationen zur Unterstützung der Immunisierung. |
| [!UICONTROL Impfcode] | `vaccineCode` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Der Code für den verabreichten Impfstoff. |
| [!UICONTROL Ablaufdatum] | `expirationDate` | Datum | Das Ablaufdatum des Impfstoffes. |
| [!UICONTROL Is Subpotent] | `isSubpotent` | Boolesch | Der Indikator dafür, ob der Impfstoff subaktiv ist. |
| [!UICONTROL Nummer des Lots] | `lotNumber` | String | Die Chargennummer des Impfstoffs. |
| [!UICONTROL Datum/Uhrzeit des Vorkommens] | `occurenceDateTime` | DateTime | Datum der Verabreichung des Impfstoffes. |
| [!UICONTROL Vorkommenszeichenfolge] | `occurenceString` | String | Datum der Verabreichung des Impfstoffes. |
| [!UICONTROL Primärer Source] | `primarySource` | Boolesch | Gibt an, ob die Daten aus einer Primärquelle erfasst wurden. |
| [!UICONTROL Status] | `status` | String | Der Status der Immunisierung. Der Wert dieser Eigenschaft muss mit einem der folgenden bekannten Enum-Werte übereinstimmen. <li> `completed` </li> <li> `entered-in-error` </li> <li> `not-done` </li> |

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/immunization.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/immunization.schema.json)

## `performer` {#performer}

`performer` wird als Array von Objekten bereitgestellt. Die Struktur der einzelnen Objekte wird nachfolgend beschrieben.

![performer structure](../../../images/healthcare/field-groups/immunization/performer.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Akteur] | `actor` | [[!UICONTROL Referenz]](../data-types/reference.md) | Die Person oder Organisation, die die Aktion durchgeführt hat. |
| [!UICONTROL Funktion] | `function` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Welche Art von Leistung wurde erzielt? |

## `programEligibility` {#program-eligibility}

`programEligibility` wird als Array von Objekten bereitgestellt. Die Struktur der einzelnen Objekte wird nachfolgend beschrieben.

![Struktur der Programmteilnahmeberechtigung](../../../images/healthcare/field-groups/immunization/program-eligibility.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Programm] | `program` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Das Programm, für das die Zuschussfähigkeit erklärt wurde. |
| [!UICONTROL Programmstatus] | `programStatus` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Der Berechtigungsstatus des Patienten für das Programm. |

## `protocolApplied` {#protocol-applied}

`protocolApplied` wird als Array von Objekten bereitgestellt. Die Struktur der einzelnen Objekte wird nachfolgend beschrieben.

![protocolApplied structure](../../../images/healthcare/field-groups/immunization/protocol-applied.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Authority] | `authority` | [[!UICONTROL Referenz]](../data-types/reference.md) | Wer ist für die Veröffentlichung der Empfehlungen verantwortlich. |
| [!UICONTROL Target-Krankheit] | `targetDisease` | Array von [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Die vermeidbare Krankheit, auf die sich der Impfstoff bezieht. |
| [!UICONTROL Dosiernummer] | `doseNumber` | String | Die Dosisnummer innerhalb der Dosisreihe. |
| [!UICONTROL Series] | `series` | String | Der Name der Impfserie. |
| [!UICONTROL Seriendosen] | `seriesDoses` | String | Empfohlene Anzahl von Dosen zur Immunität. |

## `reaction` {#reaction}

`reaction` wird als Array von Objekten bereitgestellt. Die Struktur der einzelnen Objekte wird nachfolgend beschrieben.

![Reaktionsstruktur](../../../images/healthcare/field-groups/immunization/reaction.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Manifestation] | `manifestation` | [[!UICONTROL Codeable Reference]](../data-types/codeable-concept.md) | Zusätzliche Informationen über die Reaktion. |
| [!UICONTROL Datum] | `date` | DateTime | Wann die Reaktion begann. |
| [!UICONTROL Gemeldet] | `reported` | String | Gibt an, ob die Reaktion selbst gemeldet wurde. |
