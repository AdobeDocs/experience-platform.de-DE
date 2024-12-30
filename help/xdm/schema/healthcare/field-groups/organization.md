---
title: Feldergruppe des Organisationsschemas
description: Erfahren Sie mehr über die Schemafeldgruppe der Organisation.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: b0698d36-ebc3-4b76-adcc-1deb2cbb1564
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 7%

---

# [!UICONTROL Organisation] Schemafeldgruppe

[!UICONTROL Organisation] ist eine Standardschemafeldgruppe für die [[!DNL XDM Individual Profile] Klasse](../../../classes/individual-profile.md) und die [[!DNL Provider class]](../../../classes/provider.md). Es bietet ein einzelnes `healthcareOrganization` vom Typ „Objekt“, das Informationen zu Gruppierungen von Personen oder Organisationen mit einem gemeinsamen Zweck enthält.

![Feldergruppenstruktur](../../../images/healthcare/field-groups/organization/organization.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| ---| --- | --- | --- |
| [!UICONTROL Kontaktdaten] | `contact` | Array von [[!UICONTROL erweiterten Kontaktdetails]](../data-types/extended-contact-detail.md) | Die Kontaktdaten der Kommunikationsgeräte, die für die jeweilige Organisation verfügbar sind. Dazu können Adressen, Telefonnummern, Faxnummern, Mobiltelefonnummern, E-Mail-Adressen und Websites gehören. |
| [!UICONTROL Endpunkt] | `endpoint` | Array von [[!UICONTROL Referenz]](../data-types/reference.md) | Technische Endpunkte, die Zugriff auf Services bieten, die für die Organisation betrieben werden. |
| [!UICONTROL ID] | `indentifier` | Array von [[!UICONTROL Identifier]](../data-types/identifier.md) | Die Kennung, die verwendet wird, um die Organisation über mehrere unterschiedliche Systeme hinweg zu identifizieren. |
| [!UICONTROL Teil der Organisation] | `partOf` | [[!UICONTROL Referenz]](../data-types/reference.md) | Die Organisation, der diese Organisation angehört. |
| [!UICONTROL Qualifizierung] | `qualification` | Array von Objekten | Die offiziellen Zertifizierungen, Akkreditierungen, Schulungen, Benennungen und Lizenzen, die die Versorgung durch die Organisation genehmigen und/oder anderweitig bestätigen. Weitere Informationen finden [ im ](#qualification) Abschnitt unten. |
| [!UICONTROL Typ] | `type` | Array von [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Die Art der Organisation, die es ist. |
| [!UICONTROL aktiv] | `active` | Boolesch | Ob der Datensatz des Unternehmens noch aktiv verwendet wird. |
| [!UICONTROL Alias] | `alias` | Zeichenfolgen-Array | Eine Liste alternativer Namen, als die Organisation bekannt ist oder in der Vergangenheit bekannt war. |
| [!UICONTROL Beschreibung] | `description` | String | Die Beschreibung der Organisation, die dabei hilft, einen allgemeinen Kontext bereitzustellen, um sicherzustellen, dass die richtige Organisation ausgewählt ist. |
| [!UICONTROL Name] | `name` | String | Der Name, der der Organisation zugeordnet ist. |

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/coverage.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/coverage.schema.json)

## `qualification` {#qualification}

`qualification` wird als Array von -Objekten bereitgestellt. Im Folgenden wird die Struktur der einzelnen Objekte beschrieben.

![Qualifizierungsstruktur](../../../images/healthcare/field-groups/organization/qualification.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Codierte Darstellung der Qualifikation. |
| [!UICONTROL ID] | `identifier` | Array von [[!UICONTROL Identifier]](../data-types/identifier.md) | Eine Kennung, die dieser Qualifizierung für diese Organisation zugewiesen ist. |
| [!UICONTROL Aussteller] | `issuer` | [[!UICONTROL Referenz]](../data-types/reference.md) | Organisation, die die Qualifizierung reguliert und ausstellt. |
| [!UICONTROL Zeitraum] | `period` | [[!UICONTROL Zeitraum]](../data-types/period.md) | Gültigkeitsdauer der Qualifikation. |
