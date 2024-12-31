---
title: Schemafeldgruppe „XDM-Geschäftspersonendetails“
description: Erfahren Sie mehr über die Schemafeldgruppe „XDM-Geschäftspersonendetails“.
exl-id: e9da5c1c-5a30-4cbc-beb2-cc5efe57cab0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 11%

---

# Schemafeldgruppe [!UICONTROL XDM Business Person Details]

[!UICONTROL XDM Business Person Details] ist eine Standardschemafeldgruppe für die [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md), die Informationen über eine einzelne Person im Kontext eines B2B-Unternehmens (Business-to-Business) erfasst.

![](../../images/field-groups/business-person-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `b2b` | Objekt | Ein Objekt, das die B2B-spezifischen Details zur Person erfasst. |
| `b2b.accountKey` | [[!UICONTROL B2B-Source]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für das mit der Person verknüpfte Geschäftskonto. |
| `b2b.convertedContactKey` | [[!UICONTROL B2B-Source]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für den zugehörigen Kontakt, wenn der Lead konvertiert wurde. |
| `b2b.personKey` | [[!UICONTROL B2B-Source]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Person oder das Profilfragment. |
| `b2b.accountID` | String | Eine eindeutige ID für das Geschäftskonto, mit dem diese Person verknüpft ist. |
| `b2b.blockedCause` | String | Wenn die Person gesperrt ist, gibt diese Eigenschaft den Grund dafür an. |
| `b2b.convertedContactID` | String | Die Kontakt-ID, wenn der Lead erfolgreich konvertiert wurde. |
| `b2b.convertedDate` | DateTime | Das Datum der Konversion, wenn der Lead erfolgreich konvertiert wurde. |
| `b2b.isBlocked` | Boolesch | Gibt an, ob die Person gesperrt ist. |
| `b2b.isConverted` | Boolesch | Gibt an, ob der Lead konvertiert wurde. |
| `b2b.isMarketingSuspended` | Boolesch | Gibt an, ob das Marketing für die Person ausgesetzt ist. |
| `b2b.marketingSuspendedCause` | String | Wenn das Marketing für die Person ausgesetzt wird, gibt diese Eigenschaft den Grund dafür an. |
| `b2b.personGroupID` | String | Eine Gruppenkennung für die Person. |
| `b2b.personScore` | Double | Ein von einem CRM-System für die Person generierter Score. |
| `b2b.personSource` | String | Die Quelle, von der die Informationen der Person empfangen wurden. |
| `b2b.personStatus` | String | Der aktuelle Marketing- oder Verkaufsstatus der Person. |
| `b2b.personType` | String | Der Typ der B2B-Person. |
| `extSourceSystemAudit` | [Audit-Attribute des externen Source-Systems](../../data-types/external-source-system-audit-attributes.md) | Wenn die Geschäftspersonenbeziehung von einem externen Quellsystem stammt, erfasst dieses Objekt Audit-Attribute für dieses System. |
| `extendedWorkDetails` | Objekt | Erfasst zusätzliche arbeitsbezogene Details zur Person. |
| `extendedWorkDetails.assistantDetails` | Objekt | Erfasst die folgenden Attribute im Zusammenhang mit dem Assistenten der Person: <ul><li>`name`: ([Personenname](../../data-types/person-name.md)) Der vollständige Name des Assistenten.</li><li>`phone`: ([Telefonnummer](../../data-types/phone-number.md)) Die Telefonnummer des Assistenten.</li></ul> |
| `extendedWorkDetails.departments` | Zeichenfolgen-Array | Eine Liste der Abteilungsnamen, in denen die Person arbeitet. |
| `extendedWorkDetails.jobTitle` | String | Die Berufsbezeichnung der Person. |
| `extendedWorkDetails.photoUrl` | String | Eine URL zu einem Foto der Person. |
| `extendedWorkDetails.reportsToID` | String | Eine Kennung für den Reporting-Manager der Person. |
| `faxPhone` | [Telefonnummer](../../data-types/phone-number.md) | Die Faxnummer der Person. |
| `homeAddress` | [Anschrift](../../data-types/postal-address.md) | Die Privatadresse der Person. |
| `homePhone` | [Telefonnummer](../../data-types/phone-number.md) | Die private Telefonnummer der Person. |
| `mobilePhone` | [Telefonnummer](../../data-types/phone-number.md) | Die Mobiltelefonnummer der Person. |
| `otherAddress` | [Anschrift](../../data-types/postal-address.md) | Eine alternative Adresse für die Person. |
| `otherPhone` | [Telefonnummer](../../data-types/phone-number.md) | Eine alternative Telefonnummer für die Person. |
| `person` | [Person](../../data-types/person.md) | Ein einzelner Akteur, Ansprechpartner oder Inhaber. |
| `personalEmail` | [E-Mail-Adresse](../../data-types/email-address.md) | Die persönliche E-Mail-Adresse der Person. |
| `workAddress` | [Anschrift](../../data-types/postal-address.md) | Die geschäftliche Adresse der Person. |
| `workEmail` | [E-Mail-Adresse](../../data-types/email-address.md) | Die geschäftliche E-Mail-Adresse der Person. |
| `workPhone` | [Telefonnummer](../../data-types/phone-number.md) | Die geschäftliche Telefonnummer der Person. |
| `identityMap` | Zuordnung | Ein Zuordnungsfeld, das einen Satz von Identitäten mit Namespace für die Person enthält. Dieses Feld wird vom System automatisch aktualisiert, da Identitätsdaten erfasst werden. Damit dieses Feld ordnungsgemäß für das [Echtzeit-Kundenprofil](../../../profile/home.md) verwendet werden kann, darf nicht versucht werden, bei Datenvorgängen den Inhalt des Felds manuell zu aktualisieren.<br /><br />Siehe Abschnitt zu Identitätszuordnungen in [Grundlagen der Schemakomposition](../../schema/composition.md#identityMap) für weitere Informationen zu ihrem Anwendungsfall. |
| `isDeleted` | Boolesch | Gibt an, ob diese Person auf Marketo Engage gelöscht wurde.<br><br>Bei Verwendung des [Marketo-Quell](../../../sources/connectors/adobe-applications/marketo/marketo.md)Connectors werden alle in Marketo gelöschten Datensätze automatisch im Echtzeit-Kundenprofil angezeigt. Datensätze, die sich auf diese Profile beziehen, können jedoch weiterhin im Data Lake vorhanden sein. Wenn Sie `isDeleted` auf `true` setzen, können Sie das Feld verwenden, um herauszufiltern, welche Datensätze aus Ihren Quellen gelöscht wurden, wenn Sie den Data Lake abfragen. |
| `organizations` | Zeichenfolgen-Array | Eine Liste der Organisationsnamen, in denen die Person arbeitet. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.schema.json)
