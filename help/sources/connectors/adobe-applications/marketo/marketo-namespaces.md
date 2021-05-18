---
keywords: Experience Platform;Home;beliebte Themen;Marketo-Quellanschluss;Namensräume;Schemas
solution: Experience Platform
title: Marketo Namensräume
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über benutzerdefinierte Namensraum, die beim Erstellen eines Marketo Engage-Quell-Connectors erforderlich sind.
exl-id: f1592be5-987e-41b8-9844-9dea5bd452b9
source-git-commit: 609b951cbde880a9f354b343adb1796def0a812c
workflow-type: tm+mt
source-wordcount: '1677'
ht-degree: 10%

---

# (Beta) [!DNL Marketo Engage] Namensraum und Schema

>[!IMPORTANT]
>
>Die [!DNL Marketo Engage]-Quelle befindet sich derzeit in der Betaphase. Die Funktion und Dokumentation werden geändert.

Dieses Dokument enthält Informationen über die zugrunde liegende Einrichtung für die B2B-Namensraum und -Schema, die mit [!DNL Marketo Engage] (im Folgenden als &quot;[!DNL Marketo]&quot;bezeichnet) verwendet werden. In diesem Dokument finden Sie auch Informationen zum Einrichten des Postman-Automatisierungsdienstprogramms, das zum Generieren von [!DNL Marketo] B2B-Namensräumen und -Schemas erforderlich ist.

## Einrichten des Dienstprogramms für die automatische Generierung von Namensräumen und Schemas[!DNL Marketo]

Der erste Schritt bei der Verwendung des Dienstprogramms für die automatische Erzeugung von Namensraum und Schema besteht darin, Ihre Plattform-Entwicklerkonsole und [!DNL Postman]-Umgebung einzurichten.[!DNL Marketo]

- Sie können die Sammlung und Umgebung des Dienstprogramms zur automatischen Generierung von Namensraum und Schema von diesem [GitHub-Repository](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility) herunterladen.
- Informationen zur Verwendung von Plattform-APIs, einschließlich Informationen zum Sammeln von Werten für erforderliche Header und zum Lesen von Beispiel-API-Aufrufen, finden Sie im Handbuch [Erste Schritte mit Plattform-APIs](../../../../landing/api-guide.md).
- Informationen zum Generieren Ihrer Anmeldeinformationen für Plattform-APIs finden Sie im Lernprogramm [Authentifizierung und Zugriff auf Experience Platform-APIs](../../../../landing/api-authentication.md).
- Weitere Informationen zum Einrichten von [!DNL Postman] für Plattform-APIs finden Sie im Lernprogramm zum Einrichten der Entwicklerkonsole und [!DNL Postman]](../../../../landing/postman.md).[

Bei der Einrichtung einer Plattform-Entwicklerkonsole und [!DNL Postman] können Sie jetzt Beginn beim Anwenden der entsprechenden Umgebung auf Ihre [!DNL Postman]-Umgebung verwenden.

Die folgende Tabelle enthält Beispielwerte sowie weitere Informationen zum Ausfüllen der [!DNL Postman]-Umgebung:

| Variable | Beschreibung | Beispiel |
| --- | --- | --- |
| `CLIENT_SECRET` | Ein eindeutiger Bezeichner, mit dem Ihr `{ACCESS_TOKEN}` generiert wird. Informationen zum Abrufen Ihrer `{CLIENT_SECRET}`-APIs für die Authentifizierung und den Zugriff auf die Experience Platform finden Sie im Lernprogramm [.](../../../../landing/api-authentication.md) | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | Das JSON-Web-Token (JWT) ist eine Authentifizierungsberechtigung, mit der Ihr {ACCESS_TOKEN} generiert wird. Informationen zum Generieren Ihrer `{JWT_TOKEN}`-APIs für die Authentifizierung und den Zugriff auf die Experience Platform finden Sie im Tutorial [.](../../../../landing/api-authentication.md) | `{JWT_TOKEN}` |
| `API_KEY` | Eine eindeutige ID, die zum Authentifizieren von Aufrufen von Experience Platform-APIs verwendet wird. Informationen zum Abrufen Ihrer `{API_KEY}`-APIs für die Authentifizierung und den Zugriff auf die Experience Platform finden Sie im Lernprogramm [.](../../../../landing/api-authentication.md) | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Das Autorisierungstoken, das zum Durchführen von Aufrufen von Experience Platform-APIs erforderlich ist. Informationen zum Abrufen Ihrer `{ACCESS_TOKEN}`-APIs für die Authentifizierung und den Zugriff auf die Experience Platform finden Sie im Lernprogramm [.](../../../../landing/api-authentication.md) | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | In Bezug auf [!DNL Marketo] ist dieser Wert fixiert und immer auf: `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | Der `global`-Container enthält alle vom Standardpartner für Adobe und Experience Platform bereitgestellten Klassen, Schema-Feldgruppen, Datentypen und Schema. In Bezug auf [!DNL Marketo] ist dieser Wert fest und immer auf `global` eingestellt. | `global` |
| `PRIVATE_KEY` | Eine Berechtigung zum Authentifizieren der [!DNL Postman]-Instanz für Experience Platform-APIs. Anweisungen zum Abrufen von {PRIVATE_KEY} finden Sie im Lernprogramm zum Einrichten der Entwicklerkonsole und [Einrichten der Entwicklerkonsole und [!DNL Postman]](../../../../landing/postman.md). | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Eine Berechtigung zur Integration in die Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Das Identity Management-System (IMS) bietet den Rahmen für die Authentifizierung von Adoben-Diensten. In Bezug auf [!DNL Marketo] ist dieser Wert fixiert und immer auf: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Eine Unternehmenseinheit, die Produkte und Dienstleistungen besitzen oder lizenzieren und Zugriff auf ihre Mitglieder gewähren kann. Anweisungen zum Abrufen Ihrer `{IMS_ORG}`-Informationen finden Sie im Lernprogramm unter [Einrichten der Entwicklerkonsole und [!DNL Postman]](../../../../landing/postman.md). | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | Der Name der verwendeten virtuellen Sandbox-Partition. | `prod` |
| `TENANT_ID` | Eine ID, mit der sichergestellt wird, dass die von Ihnen erstellten Ressourcen korrekt benannt werden und in Ihrer IMS-Organisation enthalten sind. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | Der URL-Endpunkt, an den Sie API-Aufrufe durchführen. Dieser Wert ist festgelegt und immer auf Folgendes eingestellt: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |
| `munchkinId` | Die eindeutige ID für Ihr [!DNL Marketo]-Konto. Informationen zum Abrufen Ihrer `munchkinId`-Instanz finden Sie im Tutorial [zum Authentifizieren Ihrer [!DNL Marketo] Instanz](./marketo-auth.md). | `123-ABC-456` |
| `sfdc_org_id` | Die Organisations-ID für Ihr [!DNL Salesforce]-Konto. Weitere Informationen zum Erwerb der [!DNL Salesforce]-Organisations-ID finden Sie im folgenden [[!DNL Salesforce] Handbuch](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1). | `00D4W000000FgYJUA0` |
| `msd_org_id` | Die Organisations-ID für Ihr [!DNL Dynamics]-Konto. Weitere Informationen zum Erwerb der [!DNL Dynamics]-Organisations-ID finden Sie im folgenden [[!DNL Microsoft Dynamics] Handbuch](https://docs.microsoft.com/en-us/power-platform/admin/determine-org-id-name). | `f6438fab-67e8-4814-a6b5-8c8dcdf7a98f` |
| `has_abm` | Ein boolescher Wert, der angibt, ob Sie [!DNL Marketo Account-Based Marketing] abonniert haben. | `false` |
| `has_msi` | Ein boolescher Wert, der angibt, ob Sie bei [!DNL Marketo Sales Insight] angemeldet sind. | `false` |

{style=&quot;table-layout:auto&quot;}

### Ausführen der Skripten

Nachdem die Sammlung und Umgebung für [!DNL Postman] eingerichtet wurde, können Sie das Skript jetzt über die [!DNL Postman]-Schnittstelle ausführen.

Wählen Sie in der Oberfläche [!DNL Postman] den Stammordner des Autogenerator-Dienstprogramms aus und wählen Sie dann **[!DNL Run]** aus der oberen Kopfzeile.

![root-folder](../images/marketo/root-folder.png)

Die [!DNL Runner]-Schnittstelle wird angezeigt. Stellen Sie von hier aus sicher, dass alle Kontrollkästchen aktiviert sind, und wählen Sie **[!DNL Run Adobe I/O Access Token Generation + Automate Namespace creation]**.

![Generator](../images/marketo/run-generator.png)

Bei einer erfolgreichen Anforderung werden die B2B-Namensraum und -Schema gemäß den Beta-Spezifikationen erstellt.

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
| `salesforce_lead_{SALESFORCE_ORGANIZATION_ID}` | automatisch generiert | `CROSS_DEVICE` | [!DNL Salesforce] | `lead` | `00DA0000000Hz79` |
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

| Anzeigename | Identitätssymbol | Identitätstyp | Ausstellertyp | Entitätstyp des Emittenten | [!DNL Dynamics] Beispiel für eine Organisations-ID eines Abonnements |
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

Bevor Daten in eine Plattform aufgenommen werden können, muss ein Schema zusammengestellt werden, das die Datenstruktur beschreibt und Einschränkungen für den Datentyp bereitstellt, der in den einzelnen Feldern enthalten sein kann. Schema bestehen aus einer Basisklasse und einer Schema- oder Feldgruppe.

Weitere Informationen zum Kompositionsmodell für Schemas, einschließlich Designprinzipien und Best Practices, finden Sie in den [Grundlagen der Schema-Komposition](../../../../xdm/schema/composition.md).

Die folgende Tabelle enthält Informationen zur zugrunde liegenden Einrichtung von [!DNL Marketo]-Schemas.

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Name des Schemas | Basisklasse | Feldergruppen | [!DNL Profile] in Schema | Primär | Primär identitäts-Namensraum | Sekundär | Sekundär identitäts-Namensraum | Beziehung | Anmerkungen |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `[!DNL Marketo] Company {MUNCHKIN_ID}` | XDM-Geschäftskonto | XDM-Geschäftskontodetails | Aktiviert | `accountID` in der Basisklasse | `marketo_company_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` in der Basisklasse | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` in der XDM-Feldgruppe &quot;Geschäftskontodetails&quot;</li><li>Typ: one-to-one</li><li>Referenz-Schema: `[!DNL Marketo] Company {MUNCHKIN_ID}`</li><li>Namespace: `marketo_company_{MUNCHKIN_ID}`</li></ul> |
| `[!DNL Marketo] Person {MUNCHKIN_ID}` | XDM Individuelles Profil | <ul><li>XDM-Geschäftspersonaldetails</li><li>XDM-Business-Personenkomponenten</li><li>IdentityMap</li></ul> | Aktiviert | `personID` in der Basisklasse | `marketo_person_{MUNCHKIN_ID}` | <ol><li>`extSourceSystemAudit.externalID` XDM-Feldgruppe &quot;Geschäftspersonendetails&quot;</li><li>`workEmail.address` XDM-Feldgruppe &quot;Geschäftspersonendetails&quot;</li><li>`identityMap` der Identitätszuordnungsfeldgruppe</ol></li> | <ol><li>`salesforce_lead_{SALESFORCE_ORGANIZATION_ID}`</li><li>E-Mail </li><li>ECID</li></ol> | <ul><li>`personComponents.sourceAccountID` XDM Business Person Components field group</li><li>Typ: Viele-zu-eins</li><li>Referenz-Schema: `[!DNL Marketo] Company {MUNCHKIN_ID}`</li><li>Namensraum: `marketo_company_{MUNCHKIN_ID}`</li><li>Zieleigenschaft: `accountID`</li><li>Beziehungsname aus aktuellem Schema: Konto</li><li>Beziehungsname aus dem Referenz-Schema: Personen</li></ul> |
| `[!DNL Marketo] Opportunity {MUNCHKIN_ID}` | XDM-Geschäftsgelegenheit | XDM-Geschäftsgelegenheiten - Details | Aktiviert | `opportunityID` in der Basisklasse | `marketo_opportunity_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` in der Basisklasse | `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountID` in der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenz-Schema: `[!DNL Marketo] Company {MUNCHKIN_ID}`</li><li>Namensraum: `marketo_company_{MUNCHKIN_ID}`</li><li>Zieleigenschaft: `accountID`</li><li>Beziehungsname aus aktuellem Schema: Konto</li><li>Beziehungsname aus dem Referenz-Schema: Chancen</li></ul> |
| `[!DNL Marketo] Opportunity Contact Role {MUNCHKIN_ID}` | XDM Geschäftsgelegenheit Personenbeziehung | Keine | Aktiviert | `opportunityPersonID` in der Basisklasse | `marketo_opportunity_contact_role_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` in der Basisklasse | `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | Erste Beziehung<ul><li>`personID` in der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenz-Schema: `[!DNL Marketo] Person {MUNCHKIN_ID}`</li><li>Namensraum: `marketo_person_{MUNCHKIN_ID}`</li><li>Zieleigenschaft: `personID`</li><li>Beziehungsname aus aktuellem Schema: Person</li><li>Beziehungsname aus dem Referenz-Schema: Chancen</li></ul>Zweite Beziehung<ul><li>`opportunityID` in der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenz-Schema: `[!DNL Marketo] Opportunity {MUNCHKIN_ID}`</li><li>Namensraum: `marketo_opportunity_{MUNCHKIN_ID}`</li><li>Zieleigenschaft: `opportunityID`</li><li>Beziehungsname aus aktuellem Schema: Chancen</li><li>Beziehungsname aus dem Referenz-Schema: Personen</li></ul> |
| `[!DNL Marketo] Program {MUNCHKIN_ID}` | XDM Business Kampagne | XDM Business Kampagne Details | Aktiviert | `campaignID` in der Basisklasse | `marketo_program_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` in der Basisklasse | `salesforce_campaign_{SALESFORCE_ORGANIZATION_ID}` |
| `[!DNL Marketo] Program Member {MUNCHKIN_ID}` | XDM Business Kampagne Member | XDM Business Kampagne Member Details | Aktiviert | `campaignMemberID` in der Basisklasse | `marketo_program_member_{MUNCHKIN_ID}` | Keine | Keine | Erste Beziehung<ul><li>`personID` in der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenz-Schema: Marketo Person {MUNCHKIN_ID}</li><li>Namensraum: `marketo_person_{MUNCHKIN_ID}`</li><li>Zieleigenschaft: `personID`</li><li>Beziehungsname aus aktuellem Schema: Person</li><li>Beziehungsname aus dem Referenz-Schema: Programme</li></ul>Zweite Beziehung<ul><li>`campaignID` in der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenz-Schema: `[!DNL Marketo] Program {MUNCHKIN_ID}`</li><li>Namensraum: `marketo_program_{MUNCHKIN_ID}`</li><li>Zieleigenschaft: `campaignID`</li><li>Beziehungsname aus aktuellem Schema: Programm</li><li>Beziehungsname aus dem Referenz-Schema: Personen</li></ul> |
| `[!DNL Marketo] Static List {MUNCHKIN_ID}` | XDM Business Marketing-Liste | Keine | Aktiviert | `marketingListID` in der Basisklasse | `marketo_static_list_{MUNCHKIN_ID}` | Keine | Keine | Keine | Statische Liste wird nicht von [!DNL Salesforce] synchronisiert und hat daher keine sekundäre Identität. |
| `[!DNL Marketo] Static List Member {MUNCHKIN_ID}` | XDM Business Marketing-Listen | Keine | Aktiviert | `marketingListMemberID` in der Basisklasse | `marketo_static_list_member_{MUNCHKIN_ID}` | Keine | Keine | Erste Beziehung<ul><li>`personID` in der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenz-Schema: `[!DNL Marketo] Person {MUNCHKIN_ID}`</li><li>Namensraum: `marketo_person_{MUNCHKIN_ID}`</li><li>Zieleigenschaft: `personID`</li><li>Beziehungsname aus aktuellem Schema: Person</li><li>Beziehungsname aus dem Referenz-Schema: Listen</li></ul>Zweite Beziehung<ul><li>`marketingListID` in der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenz-Schema: `[!DNL Marketo] Static List {MUNCHKIN_ID}`</li><li>Namensraum: `marketo_static_list_{MUNCHKIN_ID}`</li><li>Zieleigenschaft: `marketingListID`</li><li>Beziehungsname aus aktuellem Schema: Liste</li><li>Beziehungsname aus dem Referenz-Schema: Personen</li></ul> | Statisches Liste-Mitglied wird nicht von [!DNL Salesforce] synchronisiert und hat daher keine sekundäre Identität. |
| `[!DNL Marketo] Named Account {MUNCHKIN_ID}` | XDM-Geschäftskonto | XDM-Geschäftskontodetails | Aktiviert | `accountID` in der Basisklasse | `marketo_named_account_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` in der Basisklasse | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` in der XDM-Feldgruppe &quot;Geschäftskontodetails&quot;</li><li>Typ: one-to-one</li><li>Referenz-Schema: `[!DNL Marketo] Named Account {MUNCHKIN_ID}`</li><li>Namensraum: `marketo_named_account_{MUNCHKIN_ID}` |
| [!DNL Marketo] Aktivität `{MUNCHKIN ID}` | XDM ExperienceEvent | <ul><li>WebPage besuchen</li><li>Neuer Interessent</li><li>Interessenten konvertieren</li><li>hinzufügen in Liste</li><li>Aus Liste entfernen</li><li>hinzufügen zu Chancen</li><li>Aus Gelegenheit entfernen</li><li>Ausgefülltes Formular</li><li>Link-Klicks</li><li>Ausgelieferte E-Mail</li><li>E-Mail geöffnet</li><li>E-Mail angeklickt</li><li>E-Mail abgeschnitten</li><li>E-Mail-Absprung weich</li><li>E-Mail nicht abonniert</li><li>Ergebnis geändert</li><li>Chancen aktualisiert</li><li>Status in Kampagne Progression geändert</li><li>Person-ID</li><li>Marketo Web URL | Aktiviert | `personID` der Personennummer-Feldgruppe | `marketo_person_{MUNCHKIN_ID}` | Keine | Keine | Erste Beziehung<ul><li>`listOperations.listID` field</li><li>Typ: one-to-one</li><li>Referenz-Schema: `[!DNL Marketo] Static List {MUNCHKIN_ID}`</li><li>Namensraum: `marketo_static_list_{MUNCHKIN_ID}`</li></ul>Zweite Beziehung<ul><li>`opportunityEvent.opportunityID` field</li><li>Typ: one-to-one</li><li>Referenz-Schema: `[!DNL Marketo] Opportunity {MUNCHKIN_ID}`</li><li>Namensraum: `marketo_opportunity_{MUNCHKIN_ID}`</li></ul>Dritte Beziehung<ul><li>`leadOperation.campaignProgression.campaignID` field</li><li>Typ: one-to-one</li><li>Referenz-Schema: `[!DNL Marketo] Program {MUNCHKIN_ID}`</li><li>Namensraum: `marketo_program_{MUNCHKIN_ID}`</li></ul> | Die primäre Identität von `[!DNL Marketo] Activity {MUNCHKIN_ID}`-Schema ist `personID`, was der primären Identität von `[!DNL Marketo] Person {MUNCHKIN_ID}`-Schema entspricht. |

{style=&quot;table-layout:auto&quot;}

## Nächste Schritte

Informationen zum Verbinden Ihrer [!DNL Marketo]-Daten mit der Plattform finden Sie im Lernprogramm [Erstellen eines Marketo-Quellconnectors in der Benutzeroberfläche](../../../tutorials/ui/create/adobe-applications/marketo.md).
