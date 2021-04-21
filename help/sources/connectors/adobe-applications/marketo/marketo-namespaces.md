---
keywords: Experience Platform;Home;beliebte Themen;Marketo-Quellanschluss;Namensräume;Schemas
solution: Experience Platform
title: 'Marketo Namensräume '
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über benutzerdefinierte Namensraum, die beim Erstellen eines Marketo Engage-Quell-Connectors erforderlich sind.
translation-type: tm+mt
source-git-commit: bea6b35627b0e913c894c38ba9553085ba0aa26f
workflow-type: tm+mt
source-wordcount: '1215'
ht-degree: 13%

---


# (Beta) [!DNL Marketo Engage] Namensraum und Schema

>[!IMPORTANT]
>
>Die [!DNL Marketo Engage]-Quelle befindet sich derzeit in der Betaphase. Die Funktion und Dokumentation werden geändert.

Dieses Dokument enthält Informationen über die zugrunde liegende Einrichtung für die B2B-Namensraum und -Schema, die mit [!DNL Marketo Engage] (im Folgenden als &quot;[!DNL Marketo]&quot;bezeichnet) verwendet werden. In diesem Dokument finden Sie auch Informationen zum Einrichten des Postman-Automatisierungsdienstprogramms, das zum Generieren von [!DNL Marketo] B2B-Namensräumen und -Schemas erforderlich ist.

## Voraussetzungen

Bevor Sie Ihre B2B-Namensraum und -Schema generieren können, müssen Sie zunächst Ihre Plattform-Entwicklerkonsole und [!DNL Postman]-Umgebung einrichten. Weitere Informationen finden Sie im Tutorial zum Einrichten der Entwicklerkonsole und [. [!DNL Postman]](../../../../landing/postman.md)

Wenden Sie bei Einrichtung einer Plattform-Entwicklerkonsole und eines [!DNL Postman]-Setups die folgenden Variablen auf Ihre [!DNL Marketo]-Umgebung an:

| Umgebung | Beispielwert | Anmerkungen |
| --- | --- | --- |
| `PRIVATE_KEY` | `{PRIVATE_KEY}` |
| `SANDBOX_NAME` | `prod` |
| `TENANT_ID` | `b2bcdpproductiontest` |
| `munchkinId` | `123-ABC-456 ` | Weitere Informationen finden Sie im Tutorial [zum Authentifizieren Ihrer [!DNL Marketo] Instanz](./marketo-auth.md). |
| `sfdc_org_id` | `00D4W000000FgYJUA0` | Weitere Informationen zum Erwerb der Organisations-ID finden Sie in der folgenden [[!DNL Salesforce] Anleitung](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1). |
| `msd_org_id` | `f6438fab-67e8-4814-a6b5-8c8dcdf7a98f` | Weitere Informationen zum Erwerb der Organisations-ID finden Sie in der folgenden [[!DNL Microsoft Dynamics] Anleitung](https://docs.microsoft.com/en-us/power-platform/admin/determine-org-id-name). |
| `has_abm` | `false` | Dieser Wert wird auf `true` gesetzt, wenn Sie ein Abonnement für kontobasiertes Marketing haben. |
| `has_msi` | `false` | Dieser Wert wird auf `true` gesetzt, wenn Sie [!DNL Marketo Sales Insight] abonniert haben. |

{style=&quot;table-layout:auto&quot;}

## [!DNL Marketo] Namensraum

Identitäts-Namespaces sind eine Komponente des [[!DNL Identity Service]](../../../../identity-service/home.md), die als Indikatoren für den Kontext dient, auf den sich eine Identität bezieht.

Eine vollqualifizierte Identität umfasst einen ID-Wert und einen Namespace. Für jede neue [!DNL Marketo]-Instanz und Dataset-Kombination ist ein neuer benutzerdefinierter Namensraum erforderlich. Ein [!DNL Marketo]-Quellanschluss, der das `programs`-Dataset enthält, erfordert beispielsweise einen eigenen benutzerdefinierten Namensraum, und ein anderer Marketo-Quellanschluss, der dasselbe Dataset enthält, erfordert auch einen eigenen neuen benutzerdefinierten Namensraum. Weitere Informationen finden Sie unter [Übersicht über Namensraum](../../../../identity-service/namespaces.md).

Der [!DNL Marketo]-Namensraum wird in der primären Identität der Entität verwendet.

Die folgende Tabelle enthält Informationen zum zugrunde liegenden Setup für [!DNL Marketo]-Namensraum.

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Anzeigename | Identitätssymbol | Identitätstyp | Ausstellertyp | Entitätstyp des Emittenten | Munchkin-ID-Beispiel |
| --- | --- | --- | --- | --- | --- |
| `marketo_person_{MUNCHKIN_ID}` | automatisch generiert | `CROSS_DEVICE` | [!DNL Marketo] | `person` | `123-ABC-789` |
| `marketo_company_{MUNCHKIN_ID}` | automatisch generiert | `B2B_ACCOUNT` | [!DNL Marketo] | `company` | `123-ABC-789` |
| `marketo_opportunity_{MUNCHKIN_ID}` | automatisch generiert | `B2B_OPPORTUNITY` | [!DNL Marketo] | `opportunity` | `123-ABC-789` |
| `marketo_opportunity_contact_role_{MUNCHKIN_ID}` | automatisch generiert | `B2B_OPPORTUNITY_PERSON` | [!DNL Marketo] | `opportunity contact role` | `123-ABC-789` |
| `marketo_program_{MUNCHKIN_ID}` | automatisch generiert | `B2B_CAMPAIGN` | [!DNL Marketo] | `program` | `123-ABC-789` |
| `marketo_program_member_{MUNCHKIN_ID}` | automatisch generiert | `B2B_CAMPAIGN_MEMBER` | [!DNL Marketo] | `program member` | `123-ABC-789` |
| `marketo_static_list_{MUNCHKIN_ID}` | automatisch generiert | `B2B_MARKETING_LIST` | [!DNL Marketo] | `static list` | `123-ABC-789` |
| `marketo_static_list_member_{MUNCHKIN_ID}` | automatisch generiert | `B2B_MARKETING_LIST_MEMBER` | [!DNL Marketo] | `static list member` | `123-ABC-789` |
| `marketo_named_account_{MUNCHKIN_ID}` | automatisch generiert | `B2B_ACCOUNT` | [!DNL Marketo] | `named account` | `123-ABC-789` |

{style=&quot;table-layout:auto&quot;}

### [!DNL Salesforce] Namensraum

Wenn Sie die [!DNL Salesforce]-Integration abonniert haben, wird der [!DNL Salesforce]-Namensraum in der sekundären Identität der Entität verwendet.

Die folgende Tabelle enthält Informationen zum zugrunde liegenden Setup für [!DNL Salesforce]-Namensraum.

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Anzeigename | Identitätssymbol | Identitätstyp | Ausstellertyp | Entitätstyp des Emittenten | [!DNL Salesforce] Beispiel für eine Organisations-ID eines Abonnements |
| --- | --- | --- | --- | --- | --- |
| `salesforce_person_{SALESFORCE_ORGANIZATION_ID}` | automatisch generiert | `CROSS_DEVICE` | [!DNL Salesforce] | `person` | `00DA0000000Hz79` |
| `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | automatisch generiert | `B2B_ACCOUNT` | [!DNL Salesforce] | `account` | `00DA0000000Hz79` |
| `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | automatisch generiert | `B2B_OPPORTUNITY` | [!DNL Salesforce] | `opportunity` | `00DA0000000Hz79` |
| `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | automatisch generiert | `B2B_OPPORTUNITY_PERSON` | [!DNL Salesforce] | `opportunity contact role` | `00DA0000000Hz79` |
| `salesforce_campaign_{SALESFORCE_ORGANIZATION_ID}` | automatisch generiert | `B2B_CAMPAIGN` | [!DNL Salesforce] | `campaign` | `00DA0000000Hz79` |
| `salesforce_campaign_member_{SALESFORCE_ORGANIZATION_ID}` | automatisch generiert | `B2B_CAMPAIGN_MEMBER` | [!DNL Salesforce] | `campaign member` | `00DA0000000Hz79` |

{style=&quot;table-layout:auto&quot;}

### [!DNL Microsoft Dynamics] Namensraum

Wenn Sie die [!DNL Dynamics]-Integration abonniert haben, wird der [!DNL Dynamics]-Namensraum als sekundäre Identität der Entität verwendet.

Die folgende Tabelle enthält Informationen zum zugrunde liegenden Setup für [!DNL Dynamics]-Namensraum.

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Anzeigename | Identitätssymbol | Identitätstyp | Ausstellertyp | Entitätstyp des Emittenten | [!DNL Salesforce] Beispiel für eine Organisations-ID eines Abonnements |
| --- | --- | --- | --- | --- | --- |
| `microsoft_person_{DYNAMICS_ID}` | automatisch generiert | `CROSS_DEVICE` | [!DNL Microsoft] | `person` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_account_{DYNAMICS_ID}` | automatisch generiert | `B2B_ACCOUNT` | [!DNL Microsoft] | `account` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_{DYNAMICS_ID}` | automatisch generiert | `B2B_OPPORTUNITY` | [!DNL Microsoft] | `opportunity` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_contact_connection_{DYNAMICS_ID}` | automatisch generiert | `B2B_OPPORTUNITY_PERSON` | [!DNL Microsoft] | `opportunity relationship` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_{DYNAMICS_ID}` | automatisch generiert | `B2B_CAMPAIGN` | [!DNL Microsoft] | `campaign` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_member_{DYNAMICS_ID}` | automatisch generiert | `B2B_CAMPAIGN_MEMBER` | [!DNL Microsoft] | `campaign member` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |

{style=&quot;table-layout:auto&quot;}

## [!DNL Marketo] Schemas

Schemas dienen in Experience Platform zur konsistenten und wiederverwendbaren Beschreibung der Struktur von Daten. Durch die systemübergreifende einheitliche Definition von Daten wird es einfacher, die Bedeutung beizubehalten und somit Wert aus Daten zu ziehen.

Bevor Daten in eine Plattform aufgenommen werden können, muss ein Schema zusammengestellt werden, das die Datenstruktur beschreibt und Einschränkungen für den Datentyp bereitstellt, der in den einzelnen Feldern enthalten sein kann. Schema bestehen aus einer Basisklasse und Null oder mehr Mixins.

Weitere Informationen zum Kompositionsmodell für Schemas, einschließlich Designprinzipien und Best Practices, finden Sie in den [Grundlagen der Schema-Komposition](../../../../xdm/schema/composition.md).

Die folgende Tabelle enthält Informationen zur zugrunde liegenden Einrichtung von [!DNL Marketo]-Schemas.

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Name des Schemas | Basisklasse | Mixins | Primär | Primär identitäts-Namensraum | Sekundär | Sekundär identitäts-Namensraum | Beziehung | Anmerkungen |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| [!DNL Marketo] Firma {MUNCHKIN_ID} | XDM-Geschäftskonto | XDM-Geschäftskontodetails | `accountID` in der Basisklasse | `marketo_company_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` in der Basisklasse | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` in XDM Business Account Details mixen</li><li>Typ: one-to-one</li><li>Referenz-Schema: Marketo-Firma {MUNCHKIN_ID}</li><li>Namespace: `marketo_company_{MUNCHKIN_ID}`</li></ul> |
| [!DNL Marketo] Person {MUNCHKIN_ID} | XDM Individuelles Profil | <ul><li>XDM-Geschäftspersonaldetails</li><li>XDM-Business-Personenkomponenten</li></ul> | `personID` in der Basisklasse | `marketo_person_{MUNCHKIN_ID}` | <ol><li>`extSourceSystemAudit.externalID` XDM Business Person Details mixen</li><li>`workEmail.address` XDM Business Person Details mixen</li><li>`identityMap` von Identity Map mixin</ol></li> | <ol><li>`salesforce_person_{SALESFORCE_ORGANIZATION_ID}`</li><li>E-Mail </li><li>ECID</li></ol> | <ul><li>`personComponents.sourceAccountID` von XDM Business Person Components mixen</li><li>Typ: Viele-zu-eins</li><li>Referenz-Schema: Marketo-Firma {MUNCHKIN_ID}</li><li>Namensraum: `marketo_company_{MUNCHKIN_ID}`</li><li>Zieleigenschaft: `accountID`</li><li>Beziehungsname aus aktuellem Schema: Konto</li><li>Beziehungsname aus dem Referenz-Schema: Personen</li></ul> |
| [!DNL Marketo] Gelegenheit {MUNCHKIN_ID} | XDM-Geschäftsgelegenheit | XDM-Geschäftsgelegenheiten - Details | `opportunityID` in der Basisklasse | `marketo_opportunity_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` in der Basisklasse | `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountID` in der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenz-Schema: Marketo-Firma {MUNCHKIN_ID}</li><li>Namensraum: `marketo_company_{MUNCHKIN_ID}`</li><li>Zieleigenschaft: `accountID`</li><li>Beziehungsname aus aktuellem Schema: Konto</li><li>Beziehungsname aus dem Referenz-Schema: Chancen</li></ul> |
| [!DNL Marketo] Opportunity-Kontaktrolle {MUNCHKIN_ID} | XDM Geschäftsgelegenheit Personenbeziehung | Keine | `opportunityPersonID` in der Basisklasse | `marketo_opportunity_contact_role_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` in der Basisklasse | `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | Erste Beziehung<ul><li>`personID` in der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenz-Schema: Marketo Person {MUNCHKIN_ID}</li><li>Namensraum: `marketo_person_{MUNCHKIN_ID}`</li><li>Zieleigenschaft: `personID`</li><li>Beziehungsname aus aktuellem Schema: Person</li><li>Beziehungsname aus dem Referenz-Schema: Chancen</li></ul>Zweite Beziehung<ul><li>`opportunityID` in der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenz-Schema: Marketo-Chancen {MUNCHKIN_ID}</li><li>Namensraum: `marketo_opportunity_{MUNCHKIN_ID}`</li><li>Zieleigenschaft: `opportunityID`</li><li>Beziehungsname aus aktuellem Schema: Chancen</li><li>Beziehungsname aus dem Referenz-Schema: Personen</li></ul> |
| [!DNL Marketo] Programm {MUNCHKIN_ID} | XDM Business Kampagne | XDM Business Kampagne Details | `campaignID` in der Basisklasse | `marketo_program_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` in der Basisklasse | `salesforce_campaign_SALESFORCE_ORGANIZATION_ID}` |
| [!DNL Marketo] Programm Member {MUNCHKIN_ID} | XDM Business Kampagne Member | XDM Business Kampagne Member Details | `campaignMemberID` in der Basisklasse | `marketo_program_member_{MUNCHKIN_ID}` | Keine | Keine | Erste Beziehung<ul><li>`personID` in der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenz-Schema: Marketo Person {MUNCHKIN_ID}</li><li>Namensraum: `marketo_person_{MUNCHKIN_ID}`</li><li>Zieleigenschaft: `personID`</li><li>Beziehungsname aus aktuellem Schema: Person</li><li>Beziehungsname aus dem Referenz-Schema: Programme</li></ul>Zweite Beziehung<ul><li>`campaignID` in der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenz-Schema: Marketo-Programm {MUNCHKIN_ID}</li><li>Namensraum: `marketo_program_{MUNCHKIN_ID}`</li><li>Zieleigenschaft: campaignID</li><li>Beziehungsname aus aktuellem Schema: Programm</li><li>Beziehungsname aus dem Referenz-Schema: Personen</li></ul> |
| [!DNL Marketo] Statische Liste {MUNCHKIN_ID} | XDM Business Marketing-Liste | Keine | `marketingListID` in der Basisklasse | `marketo_static_list_{MUNCHKIN_ID}` | Keine | Keine | Keine | Statische Liste wird nicht von [!DNL Salesforce] synchronisiert und hat daher keine sekundäre Identität. |
| [!DNL Marketo] Mitglied der statischen Liste {MUNCHKIN_ID} | XDM Business Marketing-Listen | Keine | `marketingListMemberID` in der Basisklasse | `marketo_static_list_member_{MUNCHKIN_ID}` | Keine | Keine | Erste Beziehung<ul><li>`personID` in der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenz-Schema: Marketo Person {MUNCHKIN_ID}</li><li>Namensraum: `marketo_person_{MUNCHKIN_ID}`</li><li>Zieleigenschaft: `personID`</li><li>Beziehungsname aus aktuellem Schema: Person</li><li>Beziehungsname aus dem Referenz-Schema: Listen</li></ul>Zweite Beziehung<ul><li>`marketingListID` in der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenz-Schema: Statische Marketo-Liste {MUNCHKIN_ID}</li><li>Namensraum: `marketo_static_list_{MUNCHKIN_ID}`</li><li>Zieleigenschaft: `marketingListID`</li><li>Beziehungsname aus aktuellem Schema: Liste</li><li>Beziehungsname aus dem Referenz-Schema: Personen</li></ul> |
| [!DNL Marketo] Benanntes Konto {MUNCHKIN_ID} | XDM-Geschäftskonto | XDM-Geschäftskontodetails | `accountID` in der Basisklasse | `marketo_named_account_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` in der Basisklasse | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` in XDM Business Account Details mixen</li><li>Typ: one-to-one</li><li>Referenz-Schema: Marketo-benanntes Konto {MUNCHKIN_ID}</li><li>Namensraum: `marketo_named_account_{MUNCHKIN_ID}` |
| [!DNL Marketo] Aktivität {MUNCHKIN-ID} | XDM Experience Ereignis | <ul><li>WebPage besuchen</li><li>Neuer Interessent</li><li>Interessenten konvertieren</li><li>hinzufügen in Liste</li><li>Aus Liste entfernen</li><li>hinzufügen zu Chancen</li><li>Aus Gelegenheit entfernen</li><li>Ausgefülltes Formular</li><li>Link-Klicks</li><li>Ausgelieferte E-Mail</li><li>E-Mail geöffnet</li><li>E-Mail angeklickt</li><li>E-Mail abgeschnitten</li><li>E-Mail-Absprung weich</li><li>E-Mail nicht abonniert</li><li>Ergebnis geändert</li><li>Chancen aktualisiert</li><li>Status in Kampagne Progression geändert</li><li>Person-ID</li><li>Marketo Web URL | `personID` des Personen-ID-Mixins | marketo_person_{MUNCHKIN_ID} | Keine | Keine | Erste Beziehung<ul><li>`listOperations.listID` field</li><li>Typ: one-to-one</li><li>Referenz-Schema: Statische Marketo-Liste {MUNCHKIN_ID}</li><li>Namensraum: `marketo_static_list_{MUNCHKIN_ID}`</li></ul>Zweite Beziehung<ul><li>`opportunityEvent.opportunityID` field</li><li>Typ: one-to-one</li><li>Referenz-Schema: Marketo-Chancen {MUNCHKIN_ID}</li><li>Namensraum: `marketo_opportunity_{MUNCHKIN_ID}`</li></ul>Dritte Beziehung<ul><li>`leadOperation.campaignProgression.campaignID` field</li><li>Typ: one-to-one</li><li>Referenz-Schema: Marketo-Programm {MUNCHKIN_ID}</li><li>Namensraum: `marketo_program_{MUNCHKIN_ID}`</li></ul> |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Alle Schema sind für [!DNL Real-time Customer Profile] aktiviert

## Nächste Schritte

Informationen zum Verbinden Ihrer [!DNL Marketo]-Daten mit der Plattform finden Sie im Lernprogramm [Erstellen eines Marketo-Quellconnectors in der Benutzeroberfläche](../../../tutorials/ui/create/adobe-applications/marketo.md).