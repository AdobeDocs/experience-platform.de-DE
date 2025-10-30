---
title: Microsoft Dynamics-Zuordnungsfelder
description: Die folgenden Tabellen enthalten die Zuordnungen zwischen Microsoft Dynamics-Quellfeldern und den zugehörigen XDM-Feldern.
exl-id: 32f51761-5de3-4192-8f23-c1412ca12c08
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 40%

---

# [!DNL Microsoft Dynamics]-Feldzuordnungen

Die folgenden Tabellen enthalten die Zuordnungen zwischen [!DNL Microsoft Dynamics]-Quellfeldern und den entsprechenden Feldern des Experience-Datenmodells (XDM).

## Kontakte {#contacts}

| Quellfeld | XDM-Zielfeld | Anmerkungen |
| --- | --- | --- |
| `address1_addressid` | `workAddress._id` |  |
| `address1_city` | `workAddress.city` |  |
| `address1_country` | `workAddress.country` |  |
| `address1_county` | `workAddress.stateProvince` |  |
| `address1_latitude` | `workAddress._schema.latitude` |  |
| `address1_line1` | `workAddress.street1` |  |
| `address1_line2` | `workAddress.street2` |  |
| `address1_line3` | `workAddress.street3` |  |
| `address1_longitude` | `workAddress._schema.longitude` |  |
| `address1_postalcode` | `workAddress.postalCode` |  |
| `address1_postofficebox` | `workAddress.postOfficeBox` |  |
| `address1_stateorprovince` | `workAddress.state` |  |
| `assistantname` | `extendedWorkDetails.assistantDetails.name.fullName` |  |
| `assistantphone` | `extendedWorkDetails.assistantDetails.phone.number` |  |
| `birthdate` | `person.birthDate` |  |
| `"Dynamics"` | `b2b.personKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `b2b.personKey.sourceInstanceID` | Der Wert für `"${CRM_ORG_ID}"` wird automatisch ersetzt. |
| `contactid` | `b2b.personKey.sourceID` |  |
| `concat(contactid,"@${CRM_ORG_ID}.Dynamics")` | `b2b.personKey.sourceKey` | Primäre Identität. Der Wert für `"${CRM_ORG_ID}"` wird automatisch ersetzt. |
| `iif(contactid != null && contactid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", contactid, "sourceKey", concat(contactid,"@${CRM_ORG_ID}.Dynamics")), null)` | `personComponents.sourcePersonKey` |  |
| `department` | `extendedWorkDetails.departments` |  |
| `fullname` | `person.name.fullName` |  |
| `suffix` | `person.name.suffix` |  |
| `iif(parentcustomerid != null && parentcustomerid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", parentcustomerid, "sourceKey", concat(parentcustomerid,"@${CRM_ORG_ID}.Dynamics")), null)` | `personComponents.sourceAccountKey` |  |
| `iif(parentcustomerid != null && parentcustomerid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", parentcustomerid, "sourceKey",  concat(parentcustomerid, "@${CRM_ORG_ID}.Dynamics")), null)` | `b2b.accountKey` |  |
| `createdon` | `extSourceSystemAudit.createdDate` |  |
| `emailaddress1` | `workEmail.address` | Sekundäre Kennung. |
| `emailaddress2` | `personalEmail.address` |  |
| `emailaddress1` | `personComponents.workEmail.address` |  |
| `firstname` | `person.name.firstName` |  |
| `fullname` | `person.name.fullName` |  |
| `lastname` | `person.name.lastName` |  |
| `jobtitle` | `extendedWorkDetails.jobTitle` |  |
| `middlename` | `person.name.middleName` |  |
| `mobilephone` | `mobilePhone.number` |  |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `salutation` | `person.name.courtesyTitle` |  |
| `telephone1` | `workPhone.number` |  |

{style="table-layout:auto"}

## Leads {#leads}

| Quellfeld | XDM-Zielfeld | Anmerkungen |
| --- | --- | --- |
| `address1_addressid` | `workAddress._id` |
| `address1_city` | `workAddress.city` |
| `address1_country` | `workAddress.country` |
| `address1_county` | `workAddress.stateProvince` |
| `address1_latitude` | `workAddress._schema.latitude` |
| `address1_line1` | `workAddress.street1` |
| `address1_line2` | `workAddress.street2` |
| `address1_line3` | `workAddress.street3` |
| `address1_longitude` | `workAddress._schema.longitude` |
| `address1_postalcode` | `workAddress.postalCode` |
| `address1_postofficebox` | `workAddress.postOfficeBox` |
| `address1_stateorprovince` | `workAddress.state` |
| `telephone1` | `workPhone.number` |
| `mobilephone` | `mobilePhone.number` |
| `createdon` | `extSourceSystemAudit.createdDate` |
| `emailaddress1` | `workEmail.address` | Sekundäre Kennung |
| `emailaddress2` | `personalEmail.address` |
| `emailaddress1` | `personComponents.workEmail.address` |
| `fax` | `faxPhone.number` |
| `firstname` | `person.name.firstName` |
| `fullname` | `person.name.fullName` |
| `jobtitle` | `extendedWorkDetails.jobTitle` |
| `lastname` | `person.name.lastName` |
| `"Dynamics"` | `b2b.personKey.sourceType` |
| `"${CRM_ORG_ID}"` | `b2b.personKey.sourceInstanceID` | Der Wert für `"${CRM_ORG_ID}"` wird automatisch ersetzt. |
| `leadid` | `b2b.personKey.sourceID` |
| `concat(leadid,"@${CRM_ORG_ID}.Dynamics")` | `b2b.personKey.sourceKey` | Primäre Identität. Der Wert für `"${CRM_ORG_ID}"` wird automatisch ersetzt. |
| `iif(leadid != null && leadid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", leadid, "sourceKey", concat(leadid,"@${CRM_ORG_ID}.Dynamics")), null)` | `personComponents.sourcePersonKey` |
| `middlename` | `person.name.middleName` |
| `mobilephone` | `mobilePhone.number` |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `salutation` | `person.name.courtesyTitle` |

{style="table-layout:auto"}

## Konten {#accounts}

| Quellfeld | XDM-Zielfeld | Anmerkungen |
| --- | --- | --- |
| `"Dynamics"` | `accountKey.sourceType` |
| `"${CRM_ORG_ID}"` | `accountKey.sourceInstanceID` | Der Wert für `"${CRM_ORG_ID}"` wird automatisch ersetzt. |
| `accountid` | `accountKey.sourceID` | Primäre Identität. Der Wert für `"${CRM_ORG_ID}"` wird automatisch ersetzt. |
| `accountnumber` | `accountNumber` |
| `accountratingcode` | `accountOrganization.rating` |
| `address1_addressid` | `accountPhysicalAddress._id` |
| `address1_city` | `accountPhysicalAddress.city` |
| `address1_country` | `accountPhysicalAddress.country` |
| `address1_county` | `accountPhysicalAddress.region` |
| `address1_latitude` | `accountPhysicalAddress._schema.latitude` |
| `address1_line1` | `accountPhysicalAddress.street1` |
| `address1_line2` | `accountPhysicalAddress.street2` |
| `address1_line3` | `accountPhysicalAddress.street3` |
| `address1_longitude` | `accountPhysicalAddress._schema.longitude` |
| `address1_name` | `accountPhysicalAddress.label` |
| `address1_postalcode` | `accountPhysicalAddress.postalCode` |
| `address1_postofficebox` | `accountPhysicalAddress.postOfficeBox` |
| `address1_stateorprovince` | `accountPhysicalAddress.state` |
| `createdon` | `extSourceSystemAudit.createdDate` |
| `description` | `accountDescription` |
| `fax` | `accountFax.number` |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `name` | `accountName` |
| `numberofemployees` | `accountOrganization.numberOfEmployees` |
| `revenue` | `accountOrganization.annualRevenue.amount` |
| `sic` | `accountOrganization.SICCode` |
| `telephone1` | `accountPhone.number` |
| `tickersymbol` | `accountOrganization.tickerSymbol` |
| `websiteurl` | `accountOrganization.website` |
| `concat(accountid,"@${CRM_ORG_ID}.Dynamics")` | `accountKey.sourceKey` |

{style="table-layout:auto"}

## Opportunities {#opportunities}

| Quellfeld | XDM-Zielfeld | Anmerkungen |
| --- | --- | --- |
| `name` | `opportunityName` |
| `"Dynamics"` | `opportunityKey.sourceType` |
| `"${CRM_ORG_ID}"` | `opportunityKey.sourceInstanceID` | Der Wert für `"${CRM_ORG_ID}"` wird automatisch ersetzt. |
| `iif(parentaccountid != null && parentaccountid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", parentaccountid, "sourceKey", concat(parentaccountid, "@${CRM_ORG_ID}.Dynamics")), null)` | `accountKey` |
| `actualclosedate` | `actualCloseDate` |
| `actualvalue` | `opportunityAmount.amount` |
| `iif(campaignid != null && campaignid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", campaignid, "sourceKey", concat(campaignid,"@${CRM_ORG_ID}.Dynamics")), null)` | `campaignKey` |
| `closeprobability` | `probabilityPercentage` |
| `createdon` | `extSourceSystemAudit.createdDate` |
| `description` | `opportunityDescription` |
| `estimatedclosedate` | `expectedCloseDate` |
| `estimatedvalue` | `expectedRevenue.amount` |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `opportunityid` | `opportunityKey.sourceID` |
| `concat(opportunityid,"@${CRM_ORG_ID}.Dynamics")` | `opportunityKey.sourceKey` | Primäre Identität. Der Wert für `"${CRM_ORG_ID}"` wird automatisch ersetzt. |
| `salesstage` | `opportunityStage` |
| `stepname` | `nextStep` |

{style="table-layout:auto"}

## Rollen von Kontakten bei Opportunitys {#opportunity-contact-roles}

| Quellfeld | XDM-Zielfeld | Anmerkungen |
| --- | --- | --- |
| `"Dynamics"` | `opportunityPersonKey.sourceType` |
| `"${CRM_ORG_ID}"` | `opportunityPersonKey.sourceInstanceID` | Der Wert für `"${CRM_ORG_ID}"` wird automatisch ersetzt. |
| `connectionid` | `opportunityPersonKey.sourceID` |
| `concat(connectionid,"@${CRM_ORG_ID}.Dynamics")` | `opportunityPersonKey.sourceKey` | Primäre Identität. Der Wert für `"${CRM_ORG_ID}"` wird automatisch ersetzt. |
| `createdon` | `extSourceSystemAudit.createdDate` |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `iif(record1id != null && record1id != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", record1id, "sourceKey", concat(record1id,"@${CRM_ORG_ID}.Dynamics")), null)` | `opportunityKey` |
| `iif(record2id != null && record2id != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", record2id, "sourceKey", concat(record2id,"@${CRM_ORG_ID}.Dynamics")), null)` | `personKey` |
| `connectionrole1.name` | `personRole` |
| `record1objecttypecode` | *Eine benutzerdefinierte Feldergruppe muss als Zielschema definiert werden.* Weitere Informationen finden Sie im Anhang mit [ Schritten zum Zuordnen eines Quellfelds vom Typ Auswahlliste zu ](#picklist-type-fields) XDM-Zielschema . | Eine Liste der möglichen Werte und Beschriftungen für das `record1objecttypecode`-Quellfeld finden Sie in diesem [[!DNL Microsoft Dynamics] Referenzdokument für Verbindungsentitäten](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/connection?view=op-9-1#record1objecttypecode-options). |
| `record2objecttypecode` | *Eine benutzerdefinierte Feldergruppe muss als Zielschema definiert werden.* Weitere Informationen finden Sie im Anhang mit [ Schritten zum Zuordnen eines Quellfelds vom Typ Auswahlliste zu ](#picklist-type-fields) XDM-Zielschema . | Eine Liste der möglichen Werte und Beschriftungen für das `record2objecttypecode`-Quellfeld finden Sie in diesem [[!DNL Microsoft Dynamics] Referenzdokument für Verbindungsentitäten](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/connection?view=op-9-1#record2objecttypecode-options). |

{style="table-layout:auto"}

## Kampagnen {#campaigns}

| Quellfeld | XDM-Zielfeld | Anmerkungen |
| --- | --- | --- |
| `campaignid` | `campaignKey.sourceID` |
| `"${CRM_ORG_ID}"` | `campaignKey.sourceInstanceID` | Der Wert für `"${CRM_ORG_ID}"` wird automatisch ersetzt. |
| `concat(campaignid,"@${CRM_ORG_ID}.Dynamics")` | `campaignKey.sourceKey` | Primäre Identität. Der Wert für `"${CRM_ORG_ID}"` wird automatisch ersetzt. |
| `"Dynamics"` | `campaignKey.sourceType` |
| `iif(campaignid != null && campaignid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", campaignid, "sourceKey", concat(campaignid,"@${CRM_ORG_ID}.Dynamics")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey` ist die sekundäre Identität. Der Wert für `"${CRM_ORG_ID}"` wird automatisch ersetzt. |
| `createdon` | `extSourceSystemAudit.createdDate` |
| `modifiedby` | `extSourceSystemAudit.lastUpdatedBy` |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `description` | `campaignDescription` |
| `name` | `campaignName` |
| `totalactualcost` | `actualCost.amount` |
| `budgetedcost` | `budgetedCost.amount` |
| `expectedrevenue` | `expectedRevenue.amount` |
| `actualend` | `campaignEndDate` |
| `actualstart` | `campaignStartDate` |
| `expectedresponse` | `expectedResponse` |
| `utcconversiontimezonecode` | `timeZone` |
| `utcconversiontimezonecode` | `timezoneName` |

{style="table-layout:auto"}

## Marketing-Liste {#marketing-list}

| Quellfeld | XDM-Zielfeld | Anmerkungen |
| --- | --- | --- |
| `"Dynamics"` | `marketingListKey.sourceType` |
| `"${CRM_ORG_ID}"` | `marketingListKey.sourceInstanceID` | Der Wert für `"${CRM_ORG_ID}"` wird automatisch ersetzt. |
| `description` | `marketingListDescription` |
| `listname` | `marketingListName` |
| `listid` | `marketingListKey.sourceID` |
| `concat(listid,"@${CRM_ORG_ID}.Dynamics")` | `marketingListKey.sourceKey` | Primäre Identität. Der Wert für `"${CRM_ORG_ID}"` wird automatisch ersetzt. |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `createdon` | `extSourceSystemAudit.createdDate` |

{style="table-layout:auto"}

## Marketing-Listenmitglieder {#marketing-list-members}

| Quellfeld | XDM-Zielfeld | Anmerkungen |
| --- | --- | --- |
| `"Dynamics"` | `marketingListMemberKey.sourceType` |
| `"${CRM_ORG_ID}"` | `marketingListMemberKey.sourceInstanceID` | Der Wert für `"${CRM_ORG_ID}"` wird automatisch ersetzt. |
| `iif(entityid != null && entityid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", entityid, "sourceKey", concat(entityid,"@${CRM_ORG_ID}.Dynamics")), null)` | `personKey` |
| `listmemberid` | `marketingListMemberKey.sourceID` |
| `concat(listmemberid,"@${CRM_ORG_ID}.Dynamics")` | `marketingListMemberKey.sourceKey` | Primäre Identität. Der Wert für `"${CRM_ORG_ID}"` wird automatisch ersetzt. |
| `iif(listid != null && listid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", listid, "sourceKey", concat(listid,"@${CRM_ORG_ID}.Dynamics")), null)` | `marketingListKey` |
| `createdon` | `extSourceSystemAudit.createdDate` |

{style="table-layout:auto"}

## Anhang

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie beim Konfigurieren von B2B-Zuordnungen für Ihre [!DNL Microsoft] Dynamics-Quelle verwenden können.

### Felder vom Typ Auswahlliste {#picklist-type-fields}

Sie können [berechnete Felder](../../../../data-prep/ui/mapping.md#calculated-fields) verwenden, um ein Quellfeld vom Typ Auswahlliste von [!DNL Microsoft Dynamics] einem XDM-Zielfeld zuzuordnen.

Das Feld `genderCode` enthält beispielsweise zwei Optionen:

| Wert | Label |
| --- | --- |
| 1 | `male` |
| 2 | `female` |

Sie können die folgenden Optionen verwenden, um das `genderCode` Quellfeld `person.gender` Zielfeld zuzuordnen:

#### Logischen Operator verwenden

| Quellfeld | XDM-Zielfeld |
| --- | --- |
| `decode(genderCode, "1", "male", "2", "female", "default")` | `person.gender` |

In diesem Szenario entspricht der Wert dem Schlüssel, wenn der Schlüssel in Optionen gefunden wird, oder `default`, wenn `default` vorhanden und der Schlüssel nicht gefunden wird. Der Wert entspricht &quot;`null`&quot;, wenn die Optionen `null` oder keine `default` vorhanden sind und der Schlüssel nicht gefunden wurde.

#### Berechnetes Feld verwenden

| Quellfeld | XDM-Zielfeld |
| --- | --- |
| `iif(gendercode.equals("1"),"male",iif(gendercode.equals("2"),"female",null))` | `person.gender` |

>[!TIP]
>
>Eine verschachtelte Iteration des obigen Vorgangs ähnelt: `iif(condition, iif(cond1, tv1, fv1), iif(cond2, tv2, fv2))`.

Weitere Informationen finden Sie im [Dokument zu logischen Operatoren in [!DNL Data Prep]](../../../../data-prep/functions.md##logical-operators)
