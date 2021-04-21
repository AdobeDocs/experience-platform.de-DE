---
keywords: Experience Platform;Home;beliebte Themen;Marketo Engage;Marketing für Interaktion;Marketo;Zuordnung
solution: Experience Platform
title: Zuordnen von Feldern für die Marketo Engage-Quelle
topic-legacy: overview
description: Die folgenden Tabellen enthalten die Zuordnungen zwischen den Feldern in den Marketo-Datensätzen und den zugehörigen XDM-Feldern.
translation-type: tm+mt
source-git-commit: f12baaa9d4b37f1101792a4ae479b5a62893eb68
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 3%

---


# (Beta) [!DNL Marketo Engage]-Feldzuordnungen

>[!IMPORTANT]
>
>Die [!DNL Marketo Engage]-Quelle befindet sich derzeit in der Betaphase. Seine Funktionen und die Dokumentation können sich ändern.

Die folgenden Tabellen enthalten die Zuordnungen zwischen den Feldern in den neun Datasets [!DNL Marketo] und den zugehörigen XDM-Feldern (Experience Data Model).

## Aktivitäten {#activities}

| Quell-Datensatz | XDM-Zielgruppe | Anmerkungen |
| -------------- | ---------------- | ----- |
| `_id` | `_id` |
| `personID` | `personID` | Primär |
| `eventType` | `eventType` |
| `timeStamp` | `timestamp` |
| `web.webPageDetails._marketo.URL` | `web.webPageDetails._marketo.URL` |
| `environment.browserDetails.userAgent` | `environment.browserDetails.userAgent` |
| `environment.ipV4` | `environment.ipV4` |
| `search.keywords` | `search.keywords` |
| `search.searchEngine` | `search.searchEngine` |
| `web.webPageDetails.webPageID` | `web.webPageDetails.webPageID` |
| `web.webPageDetails.name` | `web.webPageDetails.name` |
| `web.webPageDetails.isPersonalizedURL` | `web.webPageDetails.isPersonalizedURL` |
| `web.webPageDetails.queryParameters` | `web.webPageDetails.queryParameters` |
| `web.webReferrer.URL` | `web.webReferrer.URL` |
| `listOperations.listID` | `listOperations.listID` |
| `opportunityEvent.isPrimary` | `opportunityEvent.isPrimary` |
| `opportunityEvent.opportunityID` | `opportunityEvent.opportunityID` |
| `opportunityEvent.role` | `opportunityEvent.role` |
| `leadOperation.newLead.createdDate` | `leadOperation.newLead.createdDate` |
| `leadOperation.newLead.formName` | `leadOperation.newLead.formName` |
| `leadOperation.newLead.leadSource` | `leadOperation.newLead.leadSource` |
| `leadOperation.newLead.listName` | `leadOperation.newLead.listName` |
| `leadOperation.newLead.sfdcType` | `leadOperation.newLead.sfdcType` |
| `leadOperation.newLead.sourceType` | `leadOperation.newLead.sourceType` |
| `leadOperation.convertLead.assignTo` | `leadOperation.convertLead.assignTo` |
| `leadOperation.convertLead.convertedStatus` | `leadOperation.convertLead.convertedStatus` |
| `leadOperation.convertLead.isSentNotificationEmail` | `leadOperation.convertLead.isSentNotificationEmail` |
| `directMarketing.mailingID` | `directMarketing.mailingID` |
| `directMarketing.mailingName` | `directMarketing.mailingName` |
| `directMarketing.testVariantID` | `directMarketing.testVariantID` |
| `directMarketing.testVariantName` | `directMarketing.testVariantName` |
| `directMarketing.emailBouncedCode` | `directMarketing.emailBouncedCode` |
| `directMarketing.emailBouncedDetails` | `directMarketing.emailBouncedDetails` |
| `directMarketing.email` | `directMarketing.email` |
| `device.isMobileDevice` | `device.isMobileDevice` |
| `device.model` | `device.model` |
| `environment.operatingSystem` | `environment.operatingSystem` |
| `directMarketing.linkURL` | `directMarketing.linkURL` |
| `web.webInteraction.linkID` | `web.webInteraction.linkID` |
| `web.fillOutForm.webFormID` | `web.fillOutForm.webFormID` |
| `web.fillOutForm.webFormName` | `web.fillOutForm.webFormName` |
| `web.webInteraction.linkURL` | `web.webInteraction.linkURL` |
| `leadOperation.changeScore.changeValue` | `leadOperation.changeScore.changeValue` |
| `leadOperation.changeScore.newValue` | `leadOperation.changeScore.newValue` |
| `leadOperation.changeScore.oldValue` | `leadOperation.changeScore.oldValue` |
| `leadOperation.changeScore.priority` | `leadOperation.changeScore.priority` |
| `leadOperation.changeScore.reason` | `leadOperation.changeScore.reason` |
| `leadOperation.changeScore.relativeScore` | `leadOperation.changeScore.relativeScore` |
| `leadOperation.changeScore.relativeUrgency` | `leadOperation.changeScore.relativeUrgency` |
| `leadOperation.changeScore.scoreAttributeID` | `leadOperation.changeScore.scoreAttributeID` |
| `leadOperation.changeScore.scoreAttributeName` | `leadOperation.changeScore.scoreAttributeName` |
| `leadOperation.changeScore.urgency` | `leadOperation.changeScore.urgency` |
| `opportunityEvent.dataValueChanges.attributeName` | `opportunityEvent.dataValueChanges.attributeName` |
| `opportunityEvent.dataValueChanges.newValue` | `opportunityEvent.dataValueChanges.newValue` |
| `opportunityEvent.dataValueChanges.oldValue` | `opportunityEvent.dataValueChanges.oldValue` |
| `opportunityEvent.opportunityID` | `opportunityEvent.opportunityID` |
| `leadOperation.campaignProgression.campaignID` | `leadOperation.campaignProgression.campaignID` |
| `leadOperation.campaignProgression.isAcquiredBy` | `leadOperation.campaignProgression.isAcquiredBy` |
| `leadOperation.campaignProgression.isSuccessful` | `leadOperation.campaignProgression.isSuccessful` |
| `leadOperation.campaignProgression.newStatusID` | `leadOperation.campaignProgression.newStatusID` |
| `leadOperation.campaignProgression.newStatusName` | `leadOperation.campaignProgression.newStatusName` |
| `leadOperation.campaignProgression.oldStatusID` | `leadOperation.campaignProgression.oldStatusID` |
| `leadOperation.campaignProgression.oldStatusName` | `leadOperation.campaignProgression.oldStatusName` |
| `leadOperation.campaignProgression.reason` | `leadOperation.campaignProgression.reason` |

{style=&quot;table-layout:auto&quot;}

## Programme {#programs}

| Quell-Datensatz | XDM-Zielgruppe | Anmerkungen |
| -------------- | ---------------- | ----- |
| `id` | `campaignID` | Primär |
| `sfdcId` | `extSourceSystemAudit.externalID` | Sekundär |
| `name` | `campaignName` |
| `description` | `campaignDescription` |
| `type` | `campaignType` |
| `status` | `campaignStatus` |
| `channel` | `channelName` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `cost` | `actualCost.amount` |
| `parentProgramId` | `parentCampaignID` |
| `integrationPartner` | `integrationPartnerName` |
| `startDate` | `campaignStartDate` |
| `endDate` | `campaignEndDate` |

{style=&quot;table-layout:auto&quot;}

## Programm-Mitgliedschaft {#program-memberships}

| Quell-Datensatz | XDM-Zielgruppe | Anmerkungen |
| -------------- | ---------------- | ----- |
| `id` | `campaignMemberID` | Primär |
| `programId` | `campaignID` | Beziehung |
| `leadId` | `personID` | Beziehung |
| `acquiredByCampaignID` | `acquiredByCampaignID` |
| `reachedSuccess` | `hasReachedSuccess` |
| `isExhausted` | `isExhausted` |
| `statusName` | `memberStatus` |
| `statusReason` | `memberStatusReason` |
| `membershipDate` | `membershipDate` |
| `nurtureCadence` | `nurtureCadence` |
| `trackName` | `nurtureTrackName` |
| `webinarUrl` | `webinarConfirmationUrl` |
| `registrationCode` | `webinarRegistrationID` |
| `reachedSuccessDate` | `reachedSuccessDate` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |

{style=&quot;table-layout:auto&quot;}

## Firmen {#companies}

| Quell-Datensatz | XDM-Zielgruppe | Anmerkungen |
| -------------- | ---------------- | ----- |
| `id` | `accountID` | Primär |
| `mktoCdpExternalId` | `extSourceSystemAudit.externalID` | Sekundär |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `billingCity` | `accountBillingAddress.city` |
| `billingCountry` | `accountBillingAddress.country` |
| `billingPostalCode` | `accountBillingAddress.postalCode` |
| `billingState` | `accountBillingAddress.state` |
| `billingStreet` | `accountBillingAddress.street1` |
| `annualRevenue` | `accountOrganization.annualRevenue.amount` |
| `sicCode` | `accountOrganization.SICCode` |
| `industry` | `accountOrganization.industry` |
| `numberOfEmployees` | `accountOrganization.numberOfEmployees` |
| `website` | `accountOrganization.website` |
| `mainPhone` | `accountPhone.number` |
| `company` | `accountName` |
| `companyNotes` | `accountDescription` |
| `site` | `accountSite` |

{style=&quot;table-layout:auto&quot;}

## Statische Listen {#static-lists}

| Quell-Datensatz | XDM-Zielgruppe | Anmerkungen |
| -------------- | ---------------- | ----- |
| `id` | `marketingListID` | Primär |
| `name` | `marketingListName` |
| `description` | `marketingListDescription` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |

{style=&quot;table-layout:auto&quot;}

## Mitgliedschaft in statischen Listen {#static-list-memnberships}

| Quell-Datensatz | XDM-Zielgruppe | Anmerkungen |
| -------------- | ---------------- | ----- |
| `marketingListMemberID` | `staticListMemberID` | Primär |
| `marketingListID` | `staticListID` | Beziehung |
| `personID` | `personID` | Beziehung |
| `createdAt` | `extSourceSystemAudit.createdDate` |

{style=&quot;table-layout:auto&quot;}

## Benannte Konten {#named-accounts}

>[!IMPORTANT]
>
>Der benannte Kontodatensatz ist nur mit der Kontoverwaltungsfunktion von Marketo erforderlich. Wenn Sie ABM nicht verwenden, müssen Sie keine Zuordnungen für benannte Konten einrichten.

| Quell-Datensatz | XDM-Zielgruppe | Anmerkungen |
| -------------- | ---------------- | ----- |
| `id` | `accountID` | Primär |
| `crmGuid` | `extSourceSystemAudit.externalID` | Sekundär |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `city` | `accountBillingAddress.city` |
| `country` | `accountBillingAddress.country` |
| `state` | `accountBillingAddress.state` |
| `annualRevenue` | `accountOrganization.annualRevenue.amount` |
| `sicCode` | `accountOrganization.SICCode` |
| `industry` | `accountOrganization.industry` |
| `logoUrl` | `accountOrganization.logoUrl` |
| `numberOfEmployees` | `accountOrganization.numberOfEmployees` |
| `name` | `accountName` |
| `parentAccountId` | `accountParentID` |
| `sourceType` | `accountSourceType` |

{style=&quot;table-layout:auto&quot;}

## Chancen {#opportunities}

| Quell-Datensatz | XDM-Zielgruppe | Anmerkungen |
| -------------- | ---------------- | ----- |
| `id` | `opportunityID` | Primär |
| `externalOpportunityId` | `extSourceSystemAudit.externalID` | Sekundär |
| `mktoCdpAccountOrgId` | `accountID` | Beziehung |
| `description` | `opportunityDescription` |
| `name` | `opportunityName` |
| `stage` | `opportunityStage` |
| `type` | `opportunityType` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `expectedRevenue` | `expectedRevenue.amount` |
| `amount` | `opportunityAmount.amount` |
| `closeDate` | `expectedCloseDate` |
| `fiscalQuarter` | `fiscalQuarter` |
| `fiscalYear` | `fiscalYear` |
| `forecastCategory` | `forecastCategory` |
| `forecastCategoryName` | `forecastCategoryName` |
| `isClosed` | `isClosed` |
| `isWon` | `isWon` |
| `quantity` | `opportunityQuantity` |
| `probability` | `probabilityPercentage` |
| `Campaign-ID` | `campaignID` | Wird nur empfohlen, wenn Sie die Salesforce-Integration verwenden. |
| `lastActivityDate` | `lastActivityDate` |
| `leadSource` | `leadSource` |
| `nextStep` | `nextStep` |

{style=&quot;table-layout:auto&quot;}

## Kontaktrollen {#opportunity-contact-roles}

| Quell-Datensatz | XDM-Zielgruppe | Anmerkungen |
| -------------- | ---------------- | ----- |
| `id` | `opportunityPersonID` | Primär |
| `mktoCdpSfdcId` | `extSourceSystemAudit.externalID` | Sekundär |
| `mktoCdpOpptyId` | `opportunityID` | Beziehung |
| `leadId` | `personID` | Beziehung |
| `role` | `personRole` |
| `isPrimary` | `isPrimary` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |

{style=&quot;table-layout:auto&quot;}

## Personen {#persons}

Wenn im [!DNL Profiles]-Dashboard der Plattform-Benutzeroberfläche der Wert der ID-Verknüpfung in der von Ihnen verwendeten Zusammenführungsrichtlinie auf `None` festgelegt ist, zeigt das Fenster &quot;Verknüpfte Identitäten&quot;nur das primäre Identitätsattribut an.

Als Problemumgehung können Sie das ID-Heftfeld von `None` auf `Private graph` aktualisieren, um alle verknüpften Identitäten mit einem [!DNL Profile] anzuzeigen. Alternativ können Sie entweder eine neue Richtlinie für die Zusammenführung erstellen oder eine andere Richtlinie für die Zusammenführung verwenden, die einen auf `Private graph` festgelegten ID-Heftungswert enthält. Wenn Sie eine neue Richtlinie für die Zusammenführung erstellen oder eine andere Richtlinie für die Zusammenführung verwenden, müssen Sie sicherstellen, dass die Richtlinie denselben Schema-Typ enthält, der für den Personensatz [!DNL Marketo] verwendet wird. Weitere Informationen finden Sie im Handbuch [Richtlinien in der Benutzeroberfläche zusammenführen](../../../../profile/ui/merge-policies.md).

| Quell-Datensatz | XDM-Zielgruppe | Anmerkungen |
| -------------- | ---------------- | ----- |
| `id` | `personID` | Primär |
| `emailSuspended` | `b2b.personOptInOut._channels.email` |
| `emailSuspendedAt` | `b2b.personOptInOut.optOutDetails.email.optOutDate` |
| `emailSuspendedCause` | `b2b.personOptInOut.optOutDetails.email.optOutReason` |
| `contactCompany` | `b2b.accountID` |
| `marketingSuspended` | `b2b.isMarketingSuspended` |
| `marketingSuspendedCause` | `b2b.marketingSuspendedCause` |
| `leadScore` | `b2b.personScore` |
| `leadSource` | `b2b.personSource` |
| `leadStatus` | `b2b.personStatus` |
| `personType` | `b2b.personType` |
| `leadPartitionId` | `b2b.personGroupID` |
| `mktoCdpCnvContactPersonId` | `b2b.convertedContactID` |
| `mktoCdpIsConverted` | `b2b.isConverted` |
| `mktoCdpConvertedDate` | `b2b.convertedDate` |
| `sfdcId` | `extSourceSystemAudit.externalID` | Sekundär |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `title` | `extendedWorkDetails.jobTitle` |
| `fax` | `faxPhone.number` |
| `mobilePhone` | `mobilePhone.number` |
| `firstName` | `person.name.firstName` |
| `lastName` | `person.name.lastName` |
| `middleName` | `person.name.middleName` |
| `salutation` | `person.name.courtesyTitle` |
| `dateOfBirth` | `person.birthDate` |
| `city` | `workAddress.city` |
| `country` | `workAddress.country` |
| `postalCode` | `workAddress.postalCode` |
| `state` | `workAddress.state` |
| `address` | `workAddress.street1` |
| `phone` | `workPhone.number` |
| `company` | `organizations` |
| `leadScore` | `personComponents.personScore` |
| `leadSource` | `personComponents.personSource` |
| `leadStatus` | `personComponents.personStatus` |
| `personType` | `personComponents.personType` |
| `leadPartitionId` | `personComponents.personGroupID` |
| `mktoCdpCnvContactPersonId` | `personComponents.sourceConvertedContactID` |
| `contactCompany` | `personComponents.sourceAccountID` |
| `sfdcContactId` | `personComponents.sourceExternalID` | Wird nur empfohlen, wenn Sie die Salesforce-Integration verwenden. |
| `id` | `personComponents.sourcePersonID` |
| `email` | `personComponents.workEmail.address` |
| `email` | `workEmail.address` |

{style=&quot;table-layout:auto&quot;}

## Nächste Schritte

Durch Lesen dieses Dokuments haben Sie Einblicke in die Zuordnungsbeziehung zwischen Ihren [!DNL Marketo]-Datensätzen und den zugehörigen XDM-Feldern erhalten. Sehen Sie sich das Lernprogramm unter [Erstellen einer  [!DNL Marketo] Quellverbindung](../../../tutorials/ui/create/adobe-applications/marketo.md) an, um Ihren [!DNL Marketo]-Datendurchlauf abzuschließen.
