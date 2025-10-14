---
title: B2B-Namespaces und -Schemata
description: Dieses Dokument bietet einen Überblick über die benutzerdefinierten Namespaces, die beim Erstellen eines B2B-Quell-Connectors erforderlich sind.
exl-id: f1592be5-987e-41b8-9844-9dea5bd452b9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1659'
ht-degree: 16%

---

# B2B-Namespaces und -Schemata

>[!AVAILABILITY]
>
>Sie müssen Zugriff auf [Adobe Real-Time Customer Data Platform B2B edition](../../../../rtcdp/b2b-overview.md) haben, damit Ihre B2B-Schemata im [Echtzeit-Kundenprofil) &#x200B;](../../../../profile/home.md) werden können.

>[!NOTE]
>
>Sie können Vorlagen in der Adobe Experience Platform-Benutzeroberfläche verwenden, um die Asset-Erstellung für B2B- und B2C-Daten zu beschleunigen. Weitere Informationen finden sich im Handbuch unter [Verwenden von Vorlagen in der Experience Platform-Benutzeroberfläche](../../../tutorials/ui/templates.md).

In diesem Dokument finden Sie Informationen zum zugrunde liegenden Setup für die Namespaces und Schemata, die mit B2B-Quellen verwendet werden sollen. In diesem Dokument finden Sie auch Informationen zum Einrichten Ihres Postman-Automatisierungsdienstprogramms, das zum Generieren von B2B-Namespaces und -Schemata erforderlich ist.

## Einrichten von B2B-Namespaces und des Dienstprogramms zur automatischen Schemaerstellung

>[!IMPORTANT]
>
>Anmeldedaten für Service-Konten (JWT) werden nicht mehr unterstützt. Sie müssen sicherstellen, dass Sie Ihre Anwendung oder Integration vor dem 27. Januar 2025 zu den neuen OAuth Server-zu-Server-Anmeldedaten migrieren. Lesen Sie die folgende Dokumentation für detaillierte Schritte [Migrieren Ihrer JWT-Anmeldedaten zu OAuth-Server-zu-Server-Anmeldedaten](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

In der folgenden Dokumentation finden Sie vorausgesetzte Informationen zum Einrichten Ihrer [!DNL Postman]-Umgebung zur Unterstützung des B2B-Namespace und des Dienstprogramms zur automatischen Schemaerstellung.

- Sie können den Namespace und die Dienstprogrammsammlung zur automatischen Schemaerstellung sowie die Umgebung aus diesem GitHub[Repository &#x200B;](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Informationen zur Verwendung von Experience Platform-APIs, einschließlich Details zum Erfassen von Werten für erforderliche Kopfzeilen und zum Lesen von Beispiel-API-Aufrufen, finden Sie im Handbuch [Erste Schritte mit Experience Platform-APIs](../../../../landing/api-guide.md).
- Informationen zum Generieren Ihrer Anmeldeinformationen für Experience Platform-APIs finden Sie im Tutorial zum [Authentifizieren und Zugreifen auf Experience Platform-APIs](../../../../landing/api-authentication.md).
- Informationen zum Einrichten von [!DNL Postman] für Experience Platform-APIs finden Sie im Tutorial zum [&#x200B; von Entwicklerkonsole und  [!DNL Postman]](../../../../landing/postman.md).

Wenn eine Experience Platform-Entwicklerkonsole und [!DNL Postman] eingerichtet sind, können Sie jetzt damit beginnen, die entsprechenden Umgebungswerte auf Ihre [!DNL Postman] anzuwenden.

Die folgende Tabelle enthält Beispielwerte sowie zusätzliche Informationen zum Ausfüllen Ihrer [!DNL Postman]:

| Variable | Beschreibung | Beispiel |
| --- | --- | --- |
| `CLIENT_SECRET` | Eine eindeutige Kennung, die zum Generieren Ihres `{ACCESS_TOKEN}` verwendet wird. Informationen zum Abrufen Ihrer `{CLIENT_SECRET}` finden [&#x200B; im Tutorial zum &#x200B;](../../../../landing/api-authentication.md) und Zugreifen auf Experience Platform-APIs . | `{CLIENT_SECRET}` |
| `API_KEY` | Eine eindeutige Kennung, die zum Authentifizieren von Aufrufen an Experience Platform-APIs verwendet wird. Informationen zum Abrufen Ihrer `{API_KEY}` finden [&#x200B; im Tutorial zum &#x200B;](../../../../landing/api-authentication.md) und Zugreifen auf Experience Platform-APIs . | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Das Autorisierungs-Token, das zum Abschließen von Aufrufen an Experience Platform-APIs erforderlich ist. Informationen zum Abrufen Ihrer `{ACCESS_TOKEN}` finden [&#x200B; im Tutorial zum &#x200B;](../../../../landing/api-authentication.md) und Zugreifen auf Experience Platform-APIs . | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | In Bezug auf [!DNL Marketo] ist dieser Wert fest und wird immer auf `ent_dataservices_sdk` festgelegt. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | Der `global`-Container enthält alle standardmäßigen von Adobe und Experience Platform bereitgestellten Partnerklassen, Schemafeldgruppen, Datentypen und Schemata. In Bezug auf [!DNL Marketo] ist dieser Wert fest und wird immer auf `global` festgelegt. | `global` |
| `TECHNICAL_ACCOUNT_ID` | Eine Berechtigung, die zur Integration mit Adobe I/O verwendet wird. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Das Identity Management-System (IMS) stellt das Framework für die Authentifizierung für Adobe-Services bereit. In Bezug auf [!DNL Marketo] ist dieser Wert fest und wird immer auf `ims-na1.adobelogin.com` festgelegt. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Eine Unternehmenseinheit, die Produkte und Dienstleistungen besitzen oder lizenzieren und ihren Mitgliedern Zugang gewähren kann. Anweisungen zum Abrufen Ihrer `{ORG_ID}` finden [&#x200B; im Tutorial zum Einrichten  [!DNL Postman]](../../../../landing/postman.md) Entwicklerkonsole und . | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | Der Name der virtuellen Sandbox-Partition, die Sie verwenden. | `prod` |
| `TENANT_ID` | Eine ID, mit der sichergestellt wird, dass die von Ihnen erstellten Ressourcen über den richtigen Namespace verfügen und in Ihrer Organisation enthalten sind. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | Der URL-Endpunkt, an den Sie API-Aufrufe durchführen. Dieser Wert ist fest und immer auf `http://platform.adobe.io/` festgelegt. | `http://platform.adobe.io/` |

{style="table-layout:auto"}

### Skripte ausführen

Nachdem Sie Ihre [!DNL Postman] und Umgebung eingerichtet haben, können Sie das Skript jetzt über die [!DNL Postman] ausführen.

Wählen Sie in der [!DNL Postman] den Stammordner des Dienstprogramms zur automatischen Generierung und dann **[!DNL Run]** aus der oberen Kopfzeile aus.

![Der Stammordner des Generators Namespaces und Schemata in der Postman-Benutzeroberfläche. „Ausführungen“ ist in der oberen Menüleiste hervorgehoben.](../images/marketo/root_folder.png)

Die [!DNL Runner] wird angezeigt. Stellen Sie von hier aus sicher, dass alle Kontrollkästchen aktiviert sind, und wählen Sie dann **[!DNL Run Namespaces and Schemas Autogeneration Utility]** aus.

![Die Runner-Oberfläche der Postman-Benutzeroberfläche mit mehreren Anforderungen in der Sammlung „Namespaces und Schemata“ aktiviert und die Schaltfläche „Namespaces und Schemata ausführen“ auf der rechten Seite hervorgehoben.](../images/marketo/run_generator.png)

Bei einer erfolgreichen Anfrage werden die für B2B erforderlichen Namespaces und Schemata erstellt.

## B2B-Namespaces

Identity-Namespaces sind eine Komponente von [[!DNL Identity Service]](../../../../identity-service/home.md), die dazu dienen, den Kontext einer Identität zu unterscheiden. Eine vollqualifizierte Identität enthält einen Identitätswert und einen Namespace. Weitere Informationen finden [&#x200B; in der &#x200B;](../../../../identity-service/features/namespaces.md) zu Namespaces .

B2B-Namespaces werden in der primären Identität der Entität verwendet.

Die folgende Tabelle enthält Informationen zur zugrunde liegenden Einrichtung für B2B-Namespaces.

>[!NOTE]
>
>Bitte nach links/rechts scrollen, um den vollständigen Inhalt der Tabelle anzuzeigen.

| Anzeigename | Identitätssymbol | Identitätstyp |
| --- | --- | --- |
| B2B-Person | `b2b_person` | `CROSS_DEVICE` |
| B2B-Konto | `b2b_account` | `B2B_ACCOUNT` |
| B2B-Opportunity | `b2b_opportunity` | `B2B_OPPORTUNITY` |
| B2B-Opportunity-Person-Beziehung | `b2b_opportunity_person_relation` | `B2B_OPPORTUNITY_PERSON` |
| B2B-Kampagne | `b2b_campaign` | `B2B_CAMPAIGN` |
| B2B-Kampagnenmitglied | `b2b_campaign_member` | `B2B_CAMPAIGN_MEMBER` |
| B2B-Marketing-Liste | `b2b_marketing_list` | `B2B_MARKETING_LIST` |
| B2B-Marketing-Listenmitglied | `b2b_marketing_list_member` | `B2B_MARKETING_LIST_MEMBER` |
| B2B-Konto-Personen-Beziehung | `b2b_account_person_relation` | `B2B_ACCOUNT_PERSON` |

{style="table-layout:auto"}

## B2B-Schemata

Schemata dienen in Experience Platform zur konsistenten und wiederverwendbaren Beschreibung der Struktur von Daten. Durch die systemübergreifende einheitliche Definition von Daten wird es einfacher, deren Bedeutung beizubehalten und somit Wert aus Daten zu ziehen.

Bevor Daten in Experience Platform aufgenommen werden können, muss ein Schema erstellt werden, das die Datenstruktur beschreibt und den Datentyp einschränkt, der in den einzelnen Feldern enthalten sein kann. Schemata bestehen aus einer Basisklasse und keiner oder mehreren Schema-Feldergruppen.

Weitere Informationen zum Schemaaufbaumodell, einschließlich Planungsgrundsätzen und Best Practices, finden Sie in den [Grundlagen des Schemaaufbaus](../../../../xdm/schema/composition.md).

Die folgende Tabelle enthält Informationen zur zugrunde liegenden Einrichtung von B2B-Schemata.

>[!NOTE]
>
>Bitte nach links/rechts scrollen, um den vollständigen Inhalt der Tabelle anzuzeigen.

| Schemaname | Basisklasse | Feldergruppen | In Schema [!DNL Profile] | Primäre Identität | Primärer Identity-Namespace | Sekundäre Identität | Sekundärer Identity-Namespace | Beziehung | Anmerkungen |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| B2B-Konto | [XDM Business-Konto](../../../../xdm/classes/b2b/business-account.md) | Details zum XDM Business-Konto | Aktiviert | `accountKey.sourceKey` der Basisklasse | B2B-Konto | `extSourceSystemAudit.externalKey.sourceKey` der Basisklasse | B2B-Konto | <ul><li>`accountParentKey.sourceKey` in der Feldergruppe XDM Business-Kontodetails .</li><li>Zieleigenschaft: `/accountKey/sourceKey`</li><li>Typ: Eins-zu-eins</li><li>Referenzschema: B2B-Konto</li><li>Namespace: B2B-Konto</li></ul> |
| B2B-Person | [Individuelles XDM-Profil](../../../../xdm/classes/individual-profile.md) | <ul><li>XDM-Geschäftspersonendetails</li><li>XDM-Geschäftspersonenkomponenten</li><li>IdentityMap</li><li>Details zu Einverständnis und Voreinstellungen</li></ul> | Aktiviert | `b2b.personKey.sourceKey` in der Feldergruppe „XDM-Geschäftspersonendetails“ | B2B-Person | <ol><li>`extSourceSystemAudit.externalKey.sourceKey` der Feldergruppe „XDM-Geschäftspersonendetails“</li><li>`workEmail.address` der Feldergruppe „XDM-Geschäftspersonendetails“</ol></li> | <ol><li>B2B-Person</li><li>E-Mail</li></ol> | <ul><li>`personComponents.sourceAccountKey.sourceKey` der Feldergruppe XDM-Geschäftspersonenkomponenten</li><li>Typ: Viele-zu-eins</li><li>Referenzschema: B2B-Konto</li><li>Namespace: B2B-Konto</li><li>Ziel-Eigenschaft: accountKey.sourceKey</li><li>Beziehungsname aus aktuellem Schema: Konto</li><li>Beziehungsname aus Referenzschema: Personen</li></ul> |
| B2B-Opportunity | [XDM Business-Opportunity](../../../../xdm/classes/b2b/business-opportunity.md) | XDM Business-Opportunity-Details | Aktiviert | `opportunityKey.sourceKey` der Basisklasse | B2B-Opportunity | `extSourceSystemAudit.externalKey.sourceKey` der Basisklasse | B2B-Opportunity | <ul><li>`accountKey.sourceKey` der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenzschema: B2B-Konto</li><li>Namespace: B2B-Konto</li><li>Zieleigenschaft: `accountKey.sourceKey`</li><li>Beziehungsname aus aktuellem Schema: Konto</li><li>Beziehungsname aus Referenzschema: Opportunities</li></ul> |
| B2B-Opportunity-Person-Beziehung | [XDM Business Opportunity Person Relation](../../../../xdm/classes/b2b/business-opportunity-person-relation.md) | Keine | Aktiviert | `opportunityPersonKey.sourceKey` der Basisklasse | B2B-Opportunity-Person-Beziehung | `extSourceSystemAudit.externalKey.sourceKey` der Basisklasse | B2B-Opportunity-Person-Beziehung | **Erste Beziehung**<ul><li>`personKey.sourceKey` der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenzschema: B2B-Person</li><li>Namespace: B2B-Person</li><li>Zieleigenschaft: b2b.personKey.sourceKey</li><li>Beziehungsname aus aktuellem Schema: Person</li><li>Beziehungsname aus Referenzschema: Opportunities</li></ul>**Zweite Beziehung**<ul><li>`opportunityKey.sourceKey` der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenzschema: B2B-Opportunity </li><li>Namespace: B2B-Opportunity </li><li>Zieleigenschaft: `opportunityKey.sourceKey`</li><li>Beziehungsname aus aktuellem Schema: Opportunity</li><li>Beziehungsname aus Referenzschema: Personen</li></ul> |
| B2B-Kampagne | [XDM Business Campaign](../../../../xdm/classes/b2b/business-campaign.md) | XDM Business Campaign-Details | Aktiviert | `campaignKey.sourceKey` der Basisklasse | B2B-Kampagne | `extSourceSystemAudit.externalKey.sourceKey` der Basisklasse | B2B-Kampagne |
| B2B-Kampagnenmitglied | [XDM Business Campaign Members](../../../../xdm/classes/b2b/business-campaign-members.md) | Abonnentendetails zur XDM Business-Kampagne | Aktiviert | `ccampaignMemberKey.sourceKey` der Basisklasse | B2B-Kampagnenmitglied | `extSourceSystemAudit.externalKey.sourceKey` der Basisklasse | B2B-Kampagnenmitglied | **Erste Beziehung**<ul><li>`personKey.sourceKey` der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenzschema: B2B-Person</li><li>Namespace: B2B-Person</li><li>Zieleigenschaft: `b2b.personKey.sourceKey`</li><li>Beziehungsname aus aktuellem Schema: Person</li><li>Beziehungsname aus Referenzschema: Kampagnen</li></ul>**Zweite Beziehung**<ul><li>`campaignKey.sourceKey` der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenzschema: B2B-Kampagne</li><li>Namespace: B2B-Kampagne</li><li>Zieleigenschaft: `campaignKey.sourceKey`</li><li>Beziehungsname aus aktuellem Schema: Kampagne</li><li>Beziehungsname aus Referenzschema: Personen</li></ul> |
| B2B-Marketing-Liste | [XDM Business Marketing List](../../../../xdm/classes/b2b/business-marketing-list.md) | Keine | Aktiviert | `marketingListKey.sourceKey` der Basisklasse | B2B-Marketing-Liste | Keine | Keine | Keine | Statische Liste wird nicht mit [!DNL Salesforce] synchronisiert und hat daher keine sekundäre Identität. |
| B2B-Marketing-Listenmitglied | [XDM Business Marketing List Members](../../../../xdm/classes/b2b/business-marketing-list-members.md) | Keine | Aktiviert | `marketingListMemberKey.sourceKey` der Basisklasse | B2B-Marketing-Listenmitglied | Keine | Keine | **Erste Beziehung**<ul><li>`PersonKey.sourceKey` der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenzschema: B2B-Person</li><li>Namespace: B2B-Person</li><li>Zieleigenschaft: `b2b.personKey.sourceKey`</li><li>Beziehungsname aus aktuellem Schema: Person</li><li>Beziehungsname aus Referenzschema: Marketing-Listen</li></ul>**Zweite Beziehung**<ul><li>`marketingListKey.sourceKey` der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenzschema: B2B-Marketing-Liste</li><li>Namespace: B2B-Marketing-Liste</li><li>Zieleigenschaft: `marketingListKey.sourceKey`</li><li>Beziehungsname aus aktuellem Schema: Marketing-Liste</li><li>Beziehungsname aus Referenzschema: Personen</li></ul> | Statisches Listenelement wird nicht mit [!DNL Salesforce] synchronisiert und hat daher keine sekundäre Identität. |
| B2B-Aktivität | [XDM ExperienceEvent](../../../../xdm/classes/experienceevent.md) | <ul><li>Web-Seite besuchen</li><li>Neuer Lead</li><li>Lead konvertieren</li><li>Zur Liste hinzufügen</li><li>Von Liste entfernen</li><li>Zur Opportunity hinzufügen</li><li>Aus der Opportunity entfernen</li><li>Formular ausgefüllt</li><li>Link-Klicks</li><li>E-Mail zugestellt</li><li>E-Mail geöffnet</li><li>E-Mail angeklickt</li><li>E-Mail gebounct</li><li>E-Mail nicht zugestellt (Soft-Bounce)</li><li>E-Mail abbestellt</li><li>Bewertung wurde geändert</li><li>Opportunity aktualisiert</li><li>Status im Kampagnenfortschritt geändert</li><li>Personenkennung</li><li>Marketo Web-URL</li><li>Interessanter Moment</li><li>Webhook aufrufen</li><li>Kampagnenkadenz ändern</li><li>Umsatzschritt geändert</li><li>Leads zusammenführen</li><li>E-Mail gesendet</li><li>Kampagnen-Stream ändern</li><li>Zu Kampagne hinzufügen</li></ul> | Aktiviert | `personKey.sourceKey` der Feldergruppe „Personenkennung“ | B2B-Person | Keine | Keine | **Erste Beziehung**<ul><li>`listOperations.listKey.sourceKey`</li><li>Typ: Eins-zu-eins</li><li>Referenzschema: B2B-Marketing-Liste</li><li>Namespace: B2B-Marketing-Liste</li></ul>**Zweite Beziehung**<ul><li>`opportunityEvent.opportunityKey.sourceKey`</li><li>Typ: Eins-zu-eins</li><li>Referenzschema: B2B-Opportunity</li><li>Namespace: B2B-Opportunity</li></ul>**Dritte Beziehung**<ul><li>`leadOperation.campaignProgression.campaignKey.sourceKey`</li><li>Typ: Eins-zu-eins</li><li>Referenzschema: B2B-Kampagne</li><li>Namespace: B2B-Kampagne</li></ul> | `ExperienceEvent` unterscheidet sich von Entitäten. Die Identität des Erlebnisereignisses ist die Person, die die Aktivität durchgeführt hat. |
| B2B-Konto-Personen-Beziehung | [Personenbeziehung für XDM Business-Konto](../../../../xdm/classes/b2b/business-account-person-relation.md) | Identitätszuordnung | Aktiviert | `accountPersonKey.sourceKey` der Basisklasse | B2B-Konto-Personen-Beziehung | Keine | Keine | **Erste Beziehung**<ul><li>`personKey.sourceKey` der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenzschema: B2B-Person</li><li>Namespace: B2B-Person</li><li>Zieleigenschaft: `b2b.personKey.SourceKey`</li><li>Beziehungsname aus aktuellem Schema: Personen</li><li>Beziehungsname aus Referenzschema: Konto</li></ul>**Zweite Beziehung**<ul><li>`accountKey.sourceKey` der Basisklasse</li><li>Typ: Viele-zu-eins</li><li>Referenzschema: B2B-Konto</li><li>Namespace: B2B-Konto</li><li>Zieleigenschaft: `accountKey.sourceKey`</li><li>Beziehungsname aus aktuellem Schema: Konto</li><li>Beziehungsname aus Referenzschema: Personen</li></ul> |

{style="table-layout:auto"}

## Nächste Schritte

Informationen zum Verbinden Ihrer [!DNL Marketo] mit Experience Platform finden Sie im Tutorial zum [&#x200B; eines Marketo-Quell-Connectors in der Benutzeroberfläche](../../../tutorials/ui/create/adobe-applications/marketo.md).
