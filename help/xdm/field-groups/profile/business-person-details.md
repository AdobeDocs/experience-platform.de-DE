---
title: XDM Business Person Details Schema Field Group
description: Dieses Dokument bietet einen Überblick über die Schemakontrollgruppe "XDM Business Person Details".
exl-id: e9da5c1c-5a30-4cbc-beb2-cc5efe57cab0
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 16%

---

# [!UICONTROL XDM-Geschäftspersonendetails] Schemafeldgruppe

[!UICONTROL XDM-Geschäftspersonendetails] ist eine Standardschemafeldgruppe für die [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md) die Informationen über eine Person im Kontext eines B2B-Unternehmens (Business-to-Business) erfasst.

![](../../images/field-groups/business-person-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `b2b` | Objekt | Ein Objekt, das die B2B-spezifischen Details zur Person erfasst. |
| `b2b.accountKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für das Geschäftskonto, das mit der Person verbunden ist. |
| `b2b.convertedContactKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für den zugehörigen Kontakt, wenn der Lead konvertiert wurde. |
| `b2b.personKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Person oder das Profilfragment. |
| `b2b.accountID` | Zeichenfolge | Eine eindeutige ID für das Geschäftskonto, mit dem diese Person verknüpft ist. |
| `b2b.blockedCause` | Zeichenfolge | Wenn die Person blockiert ist, liefert diese Eigenschaft den Grund. |
| `b2b.convertedContactID` | Zeichenfolge | Die Kontakt-ID, wenn der Lead erfolgreich konvertiert wurde. |
| `b2b.convertedDate` | DateTime | Das Datum der Konvertierung, wenn der Lead erfolgreich konvertiert wurde. |
| `b2b.isBlocked` | Boolesch | Gibt an, ob die Person blockiert ist. |
| `b2b.isConverted` | Boolesch | Gibt an, ob der Lead konvertiert wird. |
| `b2b.isMarketingSuspended` | Boolesch | Gibt an, ob die Vermarktung für die Person ausgesetzt wurde. |
| `b2b.marketingSuspendedCause` | Zeichenfolge | Wenn das Marketing für die Person unterbrochen wird, liefert diese Eigenschaft den Grund. |
| `b2b.personGroupID` | Zeichenfolge | Eine Gruppenkennung für die Person. |
| `b2b.personScore` | Double | Ein von einem CRM-System für die Person generierter Wert. |
| `b2b.personSource` | Zeichenfolge | Die Quelle, von der die Informationen der Person empfangen wurden. |
| `b2b.personStatus` | Zeichenfolge | Der aktuelle Marketing- oder Verkaufsstatus der Person. |
| `b2b.personType` | Zeichenfolge | Die Art der B2B-Person. |
| `extSourceSystemAudit` | [Audit-Attribute des externen Quellsystems](../../data-types/external-source-system-audit-attributes.md) | Wenn die geschäftliche Personenbeziehung aus einem externen Quellsystem stammt, erfasst dieses Objekt Prüfattribute für dieses System. |
| `extendedWorkDetails` | Objekt | Erfasst zusätzliche arbeitsbezogene Details über die Person. |
| `extendedWorkDetails.assistantDetails` | Objekt | Erfasst die folgenden Attribute in Bezug auf die Assistenzkraft der Person: <ul><li>`name`: ([Personenname](../../data-types/person-name.md)) Der vollständige Name der Assistenzkraft.</li><li>`phone`: ([Telefonnummer](../../data-types/phone-number.md)) Die Telefonnummer der Assistenzkraft.</li></ul> |
| `extendedWorkDetails.departments` | Zeichenfolgen-Array | Eine Liste der Abteilungsnamen, in denen die Person arbeitet. |
| `extendedWorkDetails.jobTitle` | Zeichenfolge | Die Berufsbezeichnung der Person. |
| `extendedWorkDetails.photoUrl` | Zeichenfolge | Eine URL zu einem Foto der Person. |
| `extendedWorkDetails.reportsToID` | Zeichenfolge | Eine Kennung für den Reporting-Manager der Person. |
| `faxPhone` | [Telefonnummer](../../data-types/phone-number.md) | Die Faxnummer der Person. |
| `homeAddress` | [Postadresse](../../data-types/postal-address.md) | Die Privatadresse der Person. |
| `homePhone` | [Telefonnummer](../../data-types/phone-number.md) | Die Privattelefonnummer der Person. |
| `mobilePhone` | [Telefonnummer](../../data-types/phone-number.md) | Die Mobiltelefonnummer der Person. |
| `otherAddress` | [Postadresse](../../data-types/postal-address.md) | Eine alternative Adresse für die Person. |
| `otherPhone` | [Telefonnummer](../../data-types/phone-number.md) | Eine alternative Telefonnummer für die Person. |
| `person` | [Person](../../data-types/person.md) | Ein einzelner Akteur, Ansprechpartner oder Inhaber. |
| `personalEmail` | [E-Mail-Adresse](../../data-types/email-address.md) | Die persönliche E-Mail-Adresse der Person. |
| `workAddress` | [Postadresse](../../data-types/postal-address.md) | Die Arbeitsadresse der Person. |
| `workEmail` | [E-Mail-Adresse](../../data-types/email-address.md) | Die geschäftliche E-Mail-Adresse der Person. |
| `workPhone` | [Telefonnummer](../../data-types/phone-number.md) | Die Telefonnummer der Person am Arbeitsplatz. |
| `identityMap` | Zuordnung | Ein map -Feld, das eine Reihe von Namespaced-Identitäten für die Person enthält. Dieses Feld wird vom System automatisch aktualisiert, da Identitätsdaten erfasst werden. Um dieses Feld ordnungsgemäß zu verwenden, verwenden Sie [Echtzeit-Kundenprofil](../../../profile/home.md)versuchen Sie nicht, den Inhalt des Felds in Ihren Datenvorgängen manuell zu aktualisieren.<br /><br />Siehe Abschnitt zu Identitätszuordnungen in [Grundlagen der Schemakomposition](../../schema/composition.md#identityMap) für weitere Informationen zu ihrem Anwendungsfall. |
| `isDeleted` | Boolesch | Gibt an, ob diese Person in Marketo Engage gelöscht wurde.<br><br>Bei Verwendung von [Marketo-Quell-Connector](../../../sources/connectors/adobe-applications/marketo/marketo.md), werden alle in Marketo gelöschten Datensätze automatisch in das Echtzeit-Kundenprofil übernommen. Datensätze, die sich auf diese Profile beziehen, können jedoch im Data Lake bestehen bleiben. Durch Festlegen von `isDeleted` nach `true`können Sie mithilfe des Felds herausfiltern, welche Datensätze bei der Abfrage des Data Lake aus Ihren Quellen gelöscht wurden. |
| `organizations` | Zeichenfolgen-Array | Eine Liste der Organisationsnamen, in denen die Person arbeitet. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.schema.json)
