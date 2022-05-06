---
keywords: Experience Platform; Startseite; beliebte Themen; crm-Schema; crm; CRM; Salesforce; Salesforce
solution: Experience Platform
title: Salesforce Source Connector - Überblick
topic-legacy: overview
description: Erfahren Sie, wie Sie Salesforce über APIs oder die Benutzeroberfläche mit Adobe Experience Platform verbinden.
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: 93061c84639ca1fdd3f7abb1bbd050eb6eebbdd6
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 17%

---

# [!DNL Salesforce]-Connector

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform bietet Unterstützung für die Aufnahme von Daten aus einem CRM-System eines Drittanbieters. Unterstützung für CRM-Anbieter umfasst [!DNL Salesforce].

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

## Feldzuordnung aus [!DNL Salesforce] in XDM

So richten Sie eine Quellverbindung zwischen [!DNL Salesforce] und Platform, die [!DNL Salesforce] Quelldatenfelder müssen ihren entsprechenden Ziel-XDM-Feldern zugeordnet werden, bevor sie in Platform erfasst werden.

Detaillierte Informationen zu den Feldzuordnungsregeln zwischen [!DNL Salesforce] Datensätze und Plattform:

- [Kontakte](../adobe-applications/mapping/salesforce.md#contact)
- [Leads](../adobe-applications/mapping/salesforce.md#lead)
- [Konten](../adobe-applications/mapping/salesforce.md#account)
- [Opportunities](../adobe-applications/mapping/salesforce.md#opportunity)
- [Rollen von Kontakten bei Opportunities](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [Kampagnen](../adobe-applications/mapping/salesforce.md#campaign)
- [Kampagnenmitglieder](../adobe-applications/mapping/salesforce.md#campaign-member)

## Richten Sie die [!DNL Salesforce] Dienstprogramm zur automatischen Namespace- und Schemaerstellung

So verwenden Sie die [!DNL Salesforce] als Teil von [!DNL B2B-CDP]müssen Sie zunächst eine [!DNL Postman] -Dienstprogramm zum automatischen Generieren Ihrer [!DNL Salesforce] Namespaces und Schemas. Die folgende Dokumentation enthält zusätzliche Informationen zum Einrichten der [!DNL Postman] Dienstprogramm:

- Sie können die Sammlung und Umgebung des Dienstprogramms für die automatische Generierung von Namespaces und Schemas von dieser [GitHub-Repository](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Informationen zur Verwendung von Platform-APIs, einschließlich Details zum Sammeln von Werten für erforderliche Kopfzeilen und zum Lesen von Beispiel-API-Aufrufen, finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../landing/api-guide.md).
- Informationen zum Generieren Ihrer Anmeldeinformationen für Platform-APIs finden Sie im Tutorial zu [Authentifizierung und Zugriff auf Experience Platform-APIs](../../../landing/api-authentication.md).
- Informationen zur Einrichtung von [!DNL Postman] Informationen zu Platform-APIs finden Sie im Tutorial zu [Einrichten der Entwicklerkonsole und [!DNL Postman]](../../../landing/postman.md).

Mit der Platform-Entwicklerkonsole und [!DNL Postman] eingerichtet haben, können Sie jetzt mit der Anwendung der entsprechenden Umgebungswerte auf Ihre [!DNL Postman] Umgebung.

Die folgende Tabelle enthält Beispielwerte sowie zusätzliche Informationen zum Ausfüllen Ihrer [!DNL Postman] Umgebung:

| Variable | Beschreibung | Beispiel |
| --- | --- | --- |
| `CLIENT_SECRET` | Eine eindeutige Kennung, mit der Ihre `{ACCESS_TOKEN}`. Siehe Tutorial zu [Authentifizierung und Zugriff auf Experience Platform-APIs](../../../landing/api-authentication.md) Informationen zum Abrufen Ihrer `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | Das JSON-Web-Token (JWT) ist eine Authentifizierungsberechtigung, die zum Generieren Ihres {ACCESS_TOKEN} verwendet wird. Siehe Tutorial zu [Authentifizierung und Zugriff auf Experience Platform-APIs](../../../landing/api-authentication.md) Informationen zur Generierung Ihrer `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | Eine eindeutige Kennung, die zum Authentifizieren von Aufrufen an Experience Platform-APIs verwendet wird. Siehe Tutorial zu [Authentifizierung und Zugriff auf Experience Platform-APIs](../../../landing/api-authentication.md) Informationen zum Abrufen Ihrer `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Das Autorisierungstoken, das zum Abschließen von Aufrufen an Experience Platform-APIs erforderlich ist. Siehe Tutorial zu [Authentifizierung und Zugriff auf Experience Platform-APIs](../../../landing/api-authentication.md) Informationen zum Abrufen Ihrer `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | Im Hinblick auf [!DNL Marketo]festgelegt ist, ist dieser Wert fest und immer auf Folgendes festgelegt: `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | Die `global` -Container enthält alle vom Standardpartner für Adoben und Experience Platformen bereitgestellten Klassen, Schemafeldgruppen, Datentypen und Schemas. Im Hinblick auf [!DNL Marketo]festgelegt ist, wird dieser Wert festgelegt und immer auf `global`. | `global` |
| `PRIVATE_KEY` | Eine Berechtigung zum Authentifizieren Ihrer [!DNL Postman] -Instanz zu Experience Platform-APIs. Siehe Tutorial zum Einrichten der Entwicklerkonsole und [Einrichten der Entwicklerkonsole und [!DNL Postman]](../../../landing/postman.md) für Anweisungen zum Abrufen Ihres {PRIVATE_KEY}. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Eine Berechtigung zur Integration in Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Das Identity Management-System (IMS) bietet das Framework für die Authentifizierung bei Adobe-Diensten. Im Hinblick auf [!DNL Marketo]festgelegt ist, wird dieser Wert festgelegt und immer auf Folgendes festgelegt: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Eine Unternehmenseinheit, die Produkte und Dienste besitzen oder lizenzieren und Zugriff auf ihre Mitglieder gewähren kann. Siehe Tutorial zu [Einrichten der Entwicklerkonsole und [!DNL Postman]](../../../landing/postman.md) Anweisungen zum Abrufen Ihrer `{ORG_ID}` Informationen. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | Der Name der von Ihnen verwendeten virtuellen Sandbox-Partition. | `prod` |
| `TENANT_ID` | Eine ID, mit der sichergestellt wird, dass die von Ihnen erstellten Ressourcen den richtigen Namespace aufweisen und in Ihrer IMS-Organisation enthalten sind. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | Der URL-Endpunkt, an den Sie API-Aufrufe durchführen. Dieser Wert ist fest festgelegt und immer auf Folgendes festgelegt: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |
| `munchkinId` | Die eindeutige ID für Ihre [!DNL Marketo] -Konto. Siehe Tutorial zu [Ihre [!DNL Marketo] instance](../adobe-applications/marketo/marketo-auth.md) Informationen zum Abrufen Ihrer `munchkinId`. | `123-ABC-456` |
| `sfdc_org_id` | Die Organisations-ID für Ihre [!DNL Salesforce] -Konto. Siehe Folgendes [[!DNL Salesforce] Handbuch](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) Weitere Informationen zum Erwerb Ihrer [!DNL Salesforce] Organisations-ID. | `00D4W000000FgYJUA0` |
| `has_abm` | Ein boolean -Wert, der anzeigt, ob Sie ein Abonnement für [!DNL Marketo Account-Based Marketing]. | `false` |
| `has_msi` | Ein boolean -Wert, der anzeigt, ob Sie sich bei [!DNL Marketo Sales Insight]. | `false` |

{style=&quot;table-layout:auto&quot;}

### Scripts ausführen

Mit [!DNL Postman] Sammlung und Umgebung eingerichtet sind, können Sie das Skript jetzt über das [!DNL Postman] -Schnittstelle.

Im [!DNL Postman] -Benutzeroberfläche, wählen Sie den Stammordner des AutoGenerator-Dienstprogramms aus und klicken Sie dann auf **[!DNL Run]** aus der oberen Kopfzeile.

![root-folder](../../images/tutorials/create/salesforce/root-folder.png)

Die [!DNL Runner] -Benutzeroberfläche angezeigt. Vergewissern Sie sich von hier aus, dass alle Kontrollkästchen aktiviert sind, und wählen Sie dann **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![run-generator](../../images/tutorials/create/salesforce/run-generator.png)

Eine erfolgreiche Anfrage erstellt die B2B-Namespaces und -Schemas gemäß den Beta-Spezifikationen.

## Verbinden [!DNL Salesforce] zur Plattform mithilfe von APIs

Die folgende Dokumentation enthält Informationen zur Verbindung von [!DNL Salesforce] mit Platform mithilfe von APIs oder der Benutzeroberfläche:

- [Salesforce-Basisverbindung mithilfe der Flow Service-API erstellen](../../tutorials/api/create/crm/salesforce.md)
- [Datentabellen mithilfe der Flow Service-API durchsuchen](../../tutorials/api/explore/tabular.md)
- [Erstellen eines Datenflusses für eine CRM-Quelle mithilfe der Flow Service-API](../../tutorials/api/collect/crm.md)

## Verbinden [!DNL Salesforce] zur Plattform mithilfe der Benutzeroberfläche

- [Erstellen einer Salesforce-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/crm/salesforce.md)
- [Erstellen eines Datenflusses für eine CRM-Verbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/crm.md)
