---
title: Schemata in Real-time Customer Data Platform B2B Edition
description: Eine Übersicht über die Rolle von Experience-Datenmodell-Schemas (XDM) in Adobe Real-Time Customer Data Platform B2B edition.
feature: Get Started, Data Management, Schemas
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 24%

---

# Schemata in Real-time Customer Data Platform B2B Edition

Adobe Real-Time Customer Data Platform B2B edition bietet mehrere standardmäßige [Experience-Datenmodell (XDM)-Klassen](../../xdm/schema/composition.md#class) die Details zu wesentlichen B2B-Datenentitäten wie Konten, Opportunitys, Kampagnen und mehr erfassen. Darüber hinaus können Sie mit Real-Time CDP B2B edition zwischen diesen Schemata Viele-zu-Eins-Beziehungen definieren, damit diese für erweiterte Segmentierungs-Anwendungsfälle verwendet werden können.

>[!IMPORTANT]
>
>B2B-Schemata sind für die Verwendung in Experience Platform-Programmen verfügbar (z. B. in [Customer Journey Analytics B2B edition](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b/cja-b2b-edition)). <br/>Sie müssen jedoch Zugriff auf Real-Time CDP B2B edition haben, damit (Profile in) B2B-Schemata am [Echtzeit-Kundenprofil“ teilnehmen &#x200B;](../../profile/home.md).

Die folgenden Standardklassen werden in Real-Time CDP B2B edition bereitgestellt:

* [XDM Business Account](../../xdm/classes/b2b/business-account.md)
* [XDM Business Account Person Relation](../../xdm/classes/b2b/business-account-person-relation.md)
* [XDM Business Campaign](../../xdm/classes/b2b/business-campaign.md)
* [XDM Business Campaign Members](../../xdm/classes/b2b/business-campaign-members.md)
* [XDM Business Opportunity](../../xdm/classes/b2b/business-opportunity.md)
* [XDM Business Opportunity Person Relation](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [XDM Business Marketing List](../../xdm/classes/b2b/business-marketing-list.md)
* [XDM Business Marketing List Members](../../xdm/classes/b2b/business-marketing-list-members.md)

Informationen dazu, wie Schemata in Ihren B2B-Workflow passen, finden Sie im [End-to-End-Tutorial](../b2b-tutorial.md).

Anweisungen zum Erstellen einer n:1-Beziehung zwischen zwei Schemata finden Sie im Tutorial zum [Erstellen von B2B-Schemabeziehungen](../../xdm/tutorials/relationship-b2b.md).

Wenn Sie eine B2B-Quellverbindung nutzen, können Sie ein Tool verwenden, um automatisch die erforderlichen Schemata und die Beziehungen zwischen ihnen zu generieren. Weitere Informationen finden Sie im Handbuch [B2B-Namespaces](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) in der Quellen-Dokumentation.


Die folgende Tabelle enthält Informationen zur zugrunde liegenden Einrichtung von B2B-Schemata.

>[!NOTE]
>
>Bitte nach links/rechts scrollen, um den vollständigen Inhalt der Tabelle anzuzeigen.

| Schemaname | Basisklasse | Feldergruppen | In Schema [!DNL Profile] | Primäre Identität | Primärer Identity-Namespace | Sekundäre Identität | Sekundärer Identity-Namespace | Beziehung | Anmerkungen |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| B2B-Konto | [XDM Business-Konto](../../xdm/classes/b2b/business-account.md) | Details zum XDM Business-Konto | Aktiviert | `accountKey.sourceKey` der Basisklasse | B2B-Konto | `extSourceSystemAudit.externalKey.sourceKey` der Basisklasse | B2B-Konto | <ul><li>`accountParentKey.sourceKey` in der Feldergruppe XDM Business-Kontodetails .</li><li>Zieleigenschaft: `/accountKey/sourceKey`</li><li>Typ: Eins-zu-eins</li><li>Referenzschema: B2B-Konto</li><li>Namespace: B2B-Konto</li></ul> |  |
| B2B-Person | [Individuelles XDM-Profil](../../xdm/classes/individual-profile.md) | <ul><li>XDM-Geschäftspersonendetails</li><li>XDM-Geschäftspersonenkomponenten</li><li>IdentityMap</li><li>Details zu Einverständnis und Voreinstellungen</li></ul> | Aktiviert | `b2b.personKey.sourceKey` in der Feldergruppe „XDM-Geschäftspersonendetails“ | B2B-Person | <ol><li>`extSourceSystemAudit.externalKey.sourceKey` der Feldergruppe „XDM-Geschäftspersonendetails“</li><li>`workEmail.address` der Feldergruppe „XDM-Geschäftspersonendetails“</ol></li> | <ol><li>B2B-Person</li><li>E-Mail</li></ol> | <ul><li>`personComponents.sourceAccountKey.sourceKey` der Feldergruppe XDM-Geschäftspersonenkomponenten</li><li>Typ: Viele-zu-eins</li><li>Referenzschema: B2B-Konto</li><li>Namespace: B2B-Konto</li><li>Ziel-Eigenschaft: accountKey.sourceKey</li><li>Beziehungsname aus aktuellem Schema: Konto</li><li>Beziehungsname aus Referenzschema: Personen</li></ul> |  |
| B2B-Opportunity | [XDM Business-Opportunity](../../xdm/classes/b2b/business-opportunity.md) | XDM Business-Opportunity-Details | Aktiviert | `opportunityKey.sourceKey` der Basisklasse | B2B-Opportunity | `extSourceSystemAudit.externalKey.sourceKey` der Basisklasse | B2B-Opportunity | <ul><li>`accountKey.sourceKey` der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenzschema: B2B-Konto</li><li>Namespace: B2B-Konto</li><li>Zieleigenschaft: `accountKey.sourceKey`</li><li>Beziehungsname aus aktuellem Schema: Konto</li><li>Beziehungsname aus Referenzschema: Opportunities</li></ul> |  |
| B2B-Opportunity-Person-Beziehung | [XDM Business Opportunity Person Relation](../../xdm/classes/b2b/business-opportunity-person-relation.md) | Keine | Aktiviert | `opportunityPersonKey.sourceKey` der Basisklasse | B2B-Opportunity-Person-Beziehung | | | **Erste Beziehung**<ul><li>`personKey.sourceKey` der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenzschema: B2B-Person</li><li>Namespace: B2B-Person</li><li>Zieleigenschaft: b2b.personKey.sourceKey</li><li>Beziehungsname aus aktuellem Schema: Person</li><li>Beziehungsname aus Referenzschema: Opportunities</li></ul>**Zweite Beziehung**<ul><li>`opportunityKey.sourceKey` der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenzschema: B2B-Opportunity </li><li>Namespace: B2B-Opportunity </li><li>Zieleigenschaft: `opportunityKey.sourceKey`</li><li>Beziehungsname aus aktuellem Schema: Opportunity</li><li>Beziehungsname aus Referenzschema: Personen</li></ul> |  |
| B2B-Kampagne | [XDM Business Campaign](../../xdm/classes/b2b/business-campaign.md) | XDM Business Campaign-Details | Aktiviert | `campaignKey.sourceKey` der Basisklasse | B2B-Kampagne | | | | |
| B2B-Kampagnenmitglied | [XDM Business Campaign Members](../../xdm/classes/b2b/business-campaign-members.md) | Abonnentendetails zur XDM Business-Kampagne | Aktiviert | `ccampaignMemberKey.sourceKey` der Basisklasse | B2B-Kampagnenmitglied | | | **Erste Beziehung**<ul><li>`personKey.sourceKey` der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenzschema: B2B-Person</li><li>Namespace: B2B-Person</li><li>Zieleigenschaft: `b2b.personKey.sourceKey`</li><li>Beziehungsname aus aktuellem Schema: Person</li><li>Beziehungsname aus Referenzschema: Kampagnen</li></ul>**Zweite Beziehung**<ul><li>`campaignKey.sourceKey` der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenzschema: B2B-Kampagne</li><li>Namespace: B2B-Kampagne</li><li>Zieleigenschaft: `campaignKey.sourceKey`</li><li>Beziehungsname aus aktuellem Schema: Kampagne</li><li>Beziehungsname aus Referenzschema: Personen</li></ul> |  |
| B2B-Marketing-Liste | [XDM Business Marketing List](../../xdm/classes/b2b/business-marketing-list.md) | Keine | Aktiviert | `marketingListKey.sourceKey` der Basisklasse | B2B-Marketing-Liste | Keine | Keine | Keine | Statische Liste wird nicht mit [!DNL Salesforce] synchronisiert und hat daher keine sekundäre Identität. |
| B2B-Marketing-Listenmitglied | [XDM Business Marketing List Members](../../xdm/classes/b2b/business-marketing-list-members.md) | Keine | Aktiviert | `marketingListMemberKey.sourceKey` der Basisklasse | B2B-Marketing-Listenmitglied | Keine | Keine | **Erste Beziehung**<ul><li>`PersonKey.sourceKey` der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenzschema: B2B-Person</li><li>Namespace: B2B-Person</li><li>Zieleigenschaft: `b2b.personKey.sourceKey`</li><li>Beziehungsname aus aktuellem Schema: Person</li><li>Beziehungsname aus Referenzschema: Marketing-Listen</li></ul>**Zweite Beziehung**<ul><li>`marketingListKey.sourceKey` der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenzschema: B2B-Marketing-Liste</li><li>Namespace: B2B-Marketing-Liste</li><li>Zieleigenschaft: `marketingListKey.sourceKey`</li><li>Beziehungsname aus aktuellem Schema: Marketing-Liste</li><li>Beziehungsname aus Referenzschema: Personen</li></ul> | Statisches Listenelement wird nicht mit [!DNL Salesforce] synchronisiert und hat daher keine sekundäre Identität. |
| B2B-Konto-Personen-Beziehung | [Personenbeziehung für XDM Business-Konto](../../xdm/classes/b2b/business-account-person-relation.md) | Identitätszuordnung | Aktiviert | `accountPersonKey.sourceKey` der Basisklasse | B2B-Konto-Personen-Beziehung | Keine | Keine | **Erste Beziehung**<ul><li>`personKey.sourceKey` der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenzschema: B2B-Person</li><li>Namespace: B2B-Person</li><li>Zieleigenschaft: `b2b.personKey.SourceKey`</li><li>Beziehungsname aus aktuellem Schema: Personen</li><li>Beziehungsname aus Referenzschema: Konto</li></ul>**Zweite Beziehung**<ul><li>`accountKey.sourceKey` der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenzschema: B2B-Konto</li><li>Namespace: B2B-Konto</li><li>Zieleigenschaft: `accountKey.sourceKey`</li><li>Beziehungsname aus aktuellem Schema: Konto</li><li>Beziehungsname aus Referenzschema: Personen</li></ul> |  |

{style="table-layout:auto"}

