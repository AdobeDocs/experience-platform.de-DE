---
keywords: Experience Platform; Startseite; beliebte Themen; Marketo-Quell-Connector; Namespaces; Schemas; b2b; B2B
solution: Experience Platform
title: B2B-Namespaces und -Schemata
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über benutzerdefinierte Namespaces, die beim Erstellen eines B2B-Quell-Connectors erforderlich sind.
exl-id: f1592be5-987e-41b8-9844-9dea5bd452b9
source-git-commit: df48e813c9b4bafaad1547bd4053b3ed730cc6c9
workflow-type: tm+mt
source-wordcount: '1705'
ht-degree: 14%

---

# B2B-Namespaces und -Schemata

Dieses Dokument enthält Informationen über die zugrunde liegende Einrichtung für Namespaces und Schemas, die mit B2B-Quellen verwendet werden sollen. In diesem Dokument finden Sie außerdem Informationen zum Einrichten Ihres Automatisierungsdienstprogramms für Postman, das zum Generieren von B2B-Namespaces und -Schemas erforderlich ist.

>[!IMPORTANT]
>
>Sie müssen Zugriff auf [Real-time Customer Data Platform B2B Edition](../../../../rtcdp/b2b-overview.md) , damit B2B-Schemata [Echtzeit-Kundenprofil](../../../../profile/home.md).

## Einrichten von B2B-Namespaces und des Dienstprogramm zur automatischen Schemaerstellung

Der erste Schritt bei der Verwendung des Namespace B2B und des Dienstprogramms für die automatische Schemaerstellung besteht darin, Ihre Platform-Entwicklerkonsole einzurichten und [!DNL Postman] Umgebung.

- Sie können die Sammlung und Umgebung des Dienstprogramms für die automatische Generierung von Namespaces und Schemas von dieser [GitHub-Repository](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Informationen zur Verwendung von Platform-APIs, einschließlich Details zum Sammeln von Werten für erforderliche Kopfzeilen und zum Lesen von Beispiel-API-Aufrufen, finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../landing/api-guide.md).
- Informationen zum Generieren Ihrer Anmeldeinformationen für Platform-APIs finden Sie im Tutorial zu [Authentifizierung und Zugriff auf Experience Platform-APIs](../../../../landing/api-authentication.md).
- Informationen zur Einrichtung von [!DNL Postman] Informationen zu Platform-APIs finden Sie im Tutorial zu [Einrichten der Entwicklerkonsole und [!DNL Postman]](../../../../landing/postman.md).

Mit der Platform-Entwicklerkonsole und [!DNL Postman] eingerichtet haben, können Sie jetzt mit der Anwendung der entsprechenden Umgebungswerte auf Ihre [!DNL Postman] Umgebung.

Die folgende Tabelle enthält Beispielwerte sowie zusätzliche Informationen zum Ausfüllen Ihrer [!DNL Postman] Umgebung:

| Variable | Beschreibung | Beispiel |
| --- | --- | --- |
| `CLIENT_SECRET` | Eine eindeutige Kennung, mit der Ihre `{ACCESS_TOKEN}`. Siehe Tutorial zu [Authentifizierung und Zugriff auf Experience Platform-APIs](../../../../landing/api-authentication.md) Informationen zum Abrufen Ihrer `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | Das JSON-Web-Token (JWT) ist eine Authentifizierungsberechtigung, die zum Generieren Ihres {ACCESS_TOKEN} verwendet wird. Siehe Tutorial zu [Authentifizierung und Zugriff auf Experience Platform-APIs](../../../../landing/api-authentication.md) Informationen zur Generierung Ihrer `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | Eine eindeutige Kennung, die zum Authentifizieren von Aufrufen an Experience Platform-APIs verwendet wird. Siehe Tutorial zu [Authentifizierung und Zugriff auf Experience Platform-APIs](../../../../landing/api-authentication.md) Informationen zum Abrufen Ihrer `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Das Autorisierungstoken, das zum Abschließen von Aufrufen an Experience Platform-APIs erforderlich ist. Siehe Tutorial zu [Authentifizierung und Zugriff auf Experience Platform-APIs](../../../../landing/api-authentication.md) Informationen zum Abrufen Ihrer `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | Im Hinblick auf [!DNL Marketo]festgelegt ist, ist dieser Wert fest und immer auf Folgendes festgelegt: `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | Die `global` -Container enthält alle vom Standardpartner für Adoben und Experience Platformen bereitgestellten Klassen, Schemafeldgruppen, Datentypen und Schemas. Im Hinblick auf [!DNL Marketo]festgelegt ist, wird dieser Wert festgelegt und immer auf `global`. | `global` |
| `PRIVATE_KEY` | Eine Berechtigung zum Authentifizieren Ihrer [!DNL Postman] -Instanz zu Experience Platform-APIs. Siehe Tutorial zum Einrichten der Entwicklerkonsole und [Einrichten der Entwicklerkonsole und [!DNL Postman]](../../../../landing/postman.md) für Anweisungen zum Abrufen Ihres {PRIVATE_KEY}. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Eine Berechtigung zur Integration in Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Das Identity Management-System (IMS) bietet das Framework für die Authentifizierung bei Adobe-Diensten. Im Hinblick auf [!DNL Marketo]festgelegt ist, wird dieser Wert festgelegt und immer auf Folgendes festgelegt: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Eine Unternehmenseinheit, die Produkte und Dienste besitzen oder lizenzieren und Zugriff auf ihre Mitglieder gewähren kann. Siehe Tutorial zu [Einrichten der Entwicklerkonsole und [!DNL Postman]](../../../../landing/postman.md) Anweisungen zum Abrufen Ihrer `{ORG_ID}` Informationen. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | Der Name der von Ihnen verwendeten virtuellen Sandbox-Partition. | `prod` |
| `TENANT_ID` | Eine ID, mit der sichergestellt wird, dass die von Ihnen erstellten Ressourcen den richtigen Namespace aufweisen und in Ihrer IMS-Organisation enthalten sind. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | Der URL-Endpunkt, an den Sie API-Aufrufe durchführen. Dieser Wert ist fest festgelegt und immer auf Folgendes festgelegt: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |

{style=&quot;table-layout:auto&quot;}

### Scripts ausführen

Mit [!DNL Postman] Sammlung und Umgebung eingerichtet sind, können Sie das Skript jetzt über das [!DNL Postman] -Schnittstelle.

Im [!DNL Postman] -Benutzeroberfläche, wählen Sie den Stammordner des AutoGenerator-Dienstprogramms aus und klicken Sie dann auf **[!DNL Run]** aus der oberen Kopfzeile.

![root-folder](../images/marketo/root-folder.png)

Die [!DNL Runner] -Benutzeroberfläche angezeigt. Vergewissern Sie sich von hier aus, dass alle Kontrollkästchen aktiviert sind, und wählen Sie dann **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![run-generator](../images/marketo/run-generator.png)

Eine erfolgreiche Anfrage erstellt die für B2B erforderlichen Namespaces und Schemas.

## B2B-Namespaces

Identitäts-Namespaces sind eine Komponente von [[!DNL Identity Service]](../../../../identity-service/home.md) , die dazu dienen, den Kontext oder den Typ einer Identität zu unterscheiden. Eine vollqualifizierte Identität umfasst einen ID-Wert und einen Namespace. Siehe [Namespaces - Übersicht](../../../../identity-service/namespaces.md) für weitere Informationen.

B2B-Namespaces werden in der primären Identität der Entität verwendet.

Die folgende Tabelle enthält Informationen zum zugrunde liegenden Setup für B2B-Namespaces.

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Anzeigename | Identitätssymbol | Identitätstyp |
| --- | --- | --- |
| B2B Person | `b2b_person` | `CROSS_DEVICE` |
| B2B-Konto | `b2b_account` | `B2B_ACCOUNT` |
| B2B-Chancen | `b2b_opportunity` | `B2B_OPPORTUNITY` |
| B2B Opportunity-Personenbeziehung | `b2b_opportunity_person_relation` | `B2B_OPPORTUNITY_PERSON` |
| B2B-Kampagne | `b2b_campaign` | `B2B_CAMPAIGN` |
| B2B Campaign-Mitglied | `b2b_campaign_member` | `B2B_CAMPAIGN_MEMBER` |
| B2B-Marketingliste | `b2b_marketing_list` | `B2B_MARKETING_LIST` |
| B2B Marketing List Member | `b2b_marketing_list_member` | `B2B_MARKETING_LIST_MEMBER` |
| B2B-Konto-Personenbeziehung | `b2b_account_person_relation` | `B2B_ACCOUNT_PERSON` |

{style=&quot;table-layout:auto&quot;}

## B2B-Schemata

Schemas dienen in Experience Platform zur konsistenten und wiederverwendbaren Beschreibung der Struktur von Daten. Durch die systemübergreifende einheitliche Definition von Daten wird es einfacher, deren Bedeutung beizubehalten und somit Wert aus Daten zu ziehen.

Bevor Daten in Platform aufgenommen werden können, muss ein Schema erstellt werden, das die Datenstruktur beschreibt und den Datentyp entsprechend des jeweiligen Feldes einschränkt. Schemas bestehen aus einer Basisklasse und keiner oder mehreren Schema-Feldergruppen.

Weitere Informationen zum Schemaaufbaumodell, einschließlich Planungsgrundsätzen und Best Practices, finden Sie in den [Grundlagen des Schemaaufbaus](../../../../xdm/schema/composition.md).

Die folgende Tabelle enthält Informationen zur zugrunde liegenden Einrichtung von B2B-Schemas.

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Schemaname | Basisklasse | Feldergruppen | [!DNL Profile] in Schema | Primäre Identität | Primärer Identitäts-Namespace | Sekundäre Identität | Sekundärer Identitäts-Namespace | Beziehung | Anmerkungen |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| B2B-Konto | [XDM Business Account](../../../../xdm/classes/b2b/business-account.md) | XDM-Geschäftskontodetails | Aktiviert | `accountKey.sourceKey` in der Basisklasse | B2B-Konto | `extSourceSystemAudit.externalKey.sourceKey` in der Basisklasse | B2B-Konto | <ul><li>`accountParentKey.sourceKey` in der Feldergruppe &quot;XDM Business Account Details&quot;</li><li>Ziel-Eigenschaft: `/accountKey/sourceKey`</li><li>Typ: Eins-zu-eins</li><li>Referenzschema: B2B-Konto</li><li>Namespace: B2B-Konto</li></ul> |
| B2B Person | [XDM Individual Profile](../../../../xdm/classes/individual-profile.md) | <ul><li>XDM-Geschäftspersonendetails</li><li>XDM-Geschäftspersonenkomponenten</li><li>IdentityMap</li><li>Einverständnis und Präferenzdetails</li></ul> | Aktiviert | `b2b.personKey.sourceKey` in der Feldergruppe &quot;XDM Business Person Details&quot; | B2B Person | <ol><li>`extSourceSystemAudit.externalKey.sourceKey` Feldergruppe &quot;XDM Business Person Details&quot;</li><li>`workEmail.address` Feldergruppe &quot;XDM Business Person Details&quot;</ol></li> | <ol><li>B2B Person</li><li>E-Mail</li></ol> | <ul><li>`personComponents.sourceAccountKey.sourceKey` Feldergruppe &quot;XDM Business Person Components&quot;</li><li>Typ: Viele-zu-eins</li><li>Referenzschema: B2B-Konto</li><li>Namespace: B2B-Konto</li><li>Ziel-Eigenschaft: accountKey.sourceKey</li><li>Beziehungsname aus aktuellem Schema: Konto</li><li>Beziehungsname aus Referenzschema: Personen</li></ul> |
| B2B-Chancen | [XDM Business Opportunity](../../../../xdm/classes/b2b/business-opportunity.md) | XDM-Geschäftsangebotsdetails | Aktiviert | `opportunityKey.sourceKey` in der Basisklasse | B2B-Chancen | `extSourceSystemAudit.externalKey.sourceKey` in der Basisklasse | B2B-Chancen | <ul><li>`accountKey.sourceKey` in der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenzschema: B2B-Konto</li><li>Namespace: B2B-Konto</li><li>Ziel-Eigenschaft: `accountKey.sourceKey`</li><li>Beziehungsname aus aktuellem Schema: Konto</li><li>Beziehungsname aus Referenzschema: Chancen</li></ul> |
| B2B Opportunity-Personenbeziehung | [XDM Business Opportunity Person Relation](../../../../xdm/classes/b2b/business-opportunity-person-relation.md) | Keine | Aktiviert | `opportunityPersonKey.sourceKey` in der Basisklasse | B2B Opportunity-Personenbeziehung | `extSourceSystemAudit.externalKey.sourceKey` in der Basisklasse | B2B Opportunity-Personenbeziehung | **Erste Beziehung**<ul><li>`personKey.sourceKey` in der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenzschema: B2B Person</li><li>Namespace: B2B Person</li><li>Ziel-Eigenschaft: b2b.personKey.sourceKey</li><li>Beziehungsname aus aktuellem Schema: Person</li><li>Beziehungsname aus Referenzschema: Chancen</li></ul>**Zweite Beziehung**<ul><li>`opportunityKey.sourceKey` in der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenzschema: B2B-Chancen </li><li>Namespace: B2B-Chancen </li><li>Ziel-Eigenschaft: `opportunityKey.sourceKey`</li><li>Beziehungsname aus aktuellem Schema: Chancen</li><li>Beziehungsname aus Referenzschema: Personen</li></ul> |
| B2B-Kampagne | [XDM Business Campaign](../../../../xdm/classes/b2b/business-campaign.md) | XDM-Geschäftskampagnendetails | Aktiviert | `campaignKey.sourceKey` in der Basisklasse | B2B-Kampagne | `extSourceSystemAudit.externalKey.sourceKey` in der Basisklasse | B2B-Kampagne |
| B2B Campaign-Mitglied | [XDM Business Campaign Members](../../../../xdm/classes/b2b/business-campaign-members.md) | Details zu XDM-Business-Campaign-Mitgliedern | Aktiviert | `ccampaignMemberKey.sourceKey` in der Basisklasse | B2B Campaign-Mitglied | `extSourceSystemAudit.externalKey.sourceKey` in der Basisklasse | B2B Campaign-Mitglied | **Erste Beziehung**<ul><li>`personKey.sourceKey` in der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenzschema: B2B Person</li><li>Namespace: B2B Person</li><li>Ziel-Eigenschaft: `b2b.personKey.sourceKey`</li><li>Beziehungsname aus aktuellem Schema: Person</li><li>Beziehungsname aus Referenzschema: Kampagnen</li></ul>**Zweite Beziehung**<ul><li>`campaignKey.sourceKey` in der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenzschema: B2B-Kampagne</li><li>Namespace: B2B-Kampagne</li><li>Ziel-Eigenschaft: `campaignKey.sourceKey`</li><li>Beziehungsname aus aktuellem Schema: Kampagne</li><li>Beziehungsname aus Referenzschema: Personen</li></ul> |
| B2B-Marketingliste | [XDM Business Marketing List](../../../../xdm/classes/b2b/business-marketing-list.md) | Keine | Aktiviert | `marketingListKey.sourceKey` in der Basisklasse | B2B-Marketingliste | Keine | Keine | Keine | Statische Liste wird nicht synchronisiert aus [!DNL Salesforce] und hat daher keine sekundäre Identität. |
| B2B Marketing List Member | [XDM Business Marketing List Members](../../../../xdm/classes/b2b/business-marketing-list-members.md) | Keine | Aktiviert | `marketingListMemberKey.sourceKey` in der Basisklasse | B2B Marketing List Member | Keine | Keine | **Erste Beziehung**<ul><li>`PersonKey.sourceKey` in der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenzschema: B2B Person</li><li>Namespace: B2B Person</li><li>Ziel-Eigenschaft: `b2b.personKey.sourceKey`</li><li>Beziehungsname aus aktuellem Schema: Person</li><li>Beziehungsname aus Referenzschema: Marketinglisten</li></ul>**Zweite Beziehung**<ul><li>`marketingListKey.sourceKey` in der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenzschema: B2B-Marketingliste</li><li>Namespace: B2B-Marketingliste</li><li>Ziel-Eigenschaft: `marketingListKey.sourceKey`</li><li>Beziehungsname aus aktuellem Schema: Marketingliste</li><li>Beziehungsname aus Referenzschema: Personen</li></ul> | Statisches Listenelement wird nicht synchronisiert aus [!DNL Salesforce] und hat daher keine sekundäre Identität. |
| B2B-Aktivität | [XDM ExperienceEvent](../../../../xdm/classes/experienceevent.md) | <ul><li>Website besuchen</li><li>Neuer Lead</li><li>Blei konvertieren</li><li>Zu Liste hinzufügen</li><li>Aus Liste löschen</li><li>Zu Chancen hinzufügen</li><li>Aus Opportunity entfernen</li><li>Ausgefülltes Formular</li><li>Link-Klicks</li><li>Zugestellt E-Mail</li><li>E-Mail geöffnet</li><li>E-Mail angeklickt</li><li>E-Mail Bounce</li><li>E-Mail-Bounce Soft</li><li>E-Mail-Abmeldung</li><li>Score geändert</li><li>Chancen aktualisiert</li><li>Status in Kampagnenfortschritt geändert</li><li>Personen-ID</li><li>Marketo Web URL</li><li>Interessanter Moment</li><li>Webhook aufrufen</li><li>Ändern der Kampagnenkadenz</li><li>Umsatzstatus geändert</li><li>Zusammenführen von Leads</li><li>E-Mail gesendet</li><li>Kampagne ändern</li><li>Zu Campaign hinzufügen</li></ul> | Aktiviert | `personKey.sourceKey` Feldergruppe &quot;Person Identifier&quot; | B2B Person | Keine | Keine | **Erste Beziehung**<ul><li>`listOperations.listKey.sourceKey` field</li><li>Typ: Eins-zu-eins</li><li>Referenzschema: B2B-Marketingliste</li><li>Namespace: B2B-Marketingliste</li></ul>**Zweite Beziehung**<ul><li>`opportunityEvent.opportunityKey.sourceKey` field</li><li>Typ: Eins-zu-eins</li><li>Referenzschema: B2B-Chancen</li><li>Namespace: B2B-Chancen</li></ul>**Dritte Beziehung**<ul><li>`leadOperation.campaignProgression.campaignKey.sourceKey` field</li><li>Typ: Eins-zu-eins</li><li>Referenzschema: B2B-Kampagne</li><li>Namespace: B2B-Kampagne</li></ul> | `ExperienceEvent` unterscheidet sich von Entitäten. Die Identität des Erlebnisereignisses ist die Person, die die Aktivität durchgeführt hat. |
| B2B-Konto-Personenbeziehung | [XDM Business Account Person Relation](../../../../xdm/classes/b2b/business-account-person-relation.md) | Identitätszuordnung | Aktiviert | `accountPersonKey.sourceKey` in der Basisklasse | B2B-Konto-Personenbeziehung | Keine | Keine | **Erste Beziehung**<ul><li>`personKey.sourceKey` in der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenzschema: B2B Person</li><li>Namespace: B2B Person</li><li>Ziel-Eigenschaft: `b2b.personKey.SourceKey`</li><li>Beziehungsname aus aktuellem Schema: Personen</li><li>Beziehungsname aus Referenzschema: Konto</li></ul>**Zweite Beziehung**<ul><li>`accountKey.sourceKey` in der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenzschema: B2B-Konto</li><li>Namespace: B2B-Konto</li><li>Ziel-Eigenschaft: `accountKey.sourceKey`</li><li>Beziehungsname aus aktuellem Schema: Konto</li><li>Beziehungsname aus Referenzschema: Personen</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Nächste Schritte

Erfahren Sie, wie Sie Ihre [!DNL Marketo] Daten an Platform weiterleiten, siehe Tutorial zu [Erstellen eines Quell-Connectors für Marketo über die Benutzeroberfläche](../../../tutorials/ui/create/adobe-applications/marketo.md).
