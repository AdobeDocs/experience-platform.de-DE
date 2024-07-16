---
title: Salesforce Source Connector - Überblick
description: Erfahren Sie, wie Sie Salesforce über APIs oder die Benutzeroberfläche mit Adobe Experience Platform verbinden.
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: 5d28db34edd377269e8710b1741098a08616ae5f
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 20%

---

# [!DNL Salesforce]

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform bietet Unterstützung für die Aufnahme von Daten aus einem CRM-System eines Drittanbieters. Unterstützung für CRM-Anbieter umfasst [!DNL Salesforce].

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Performance-Einbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

## Feldzuordnung von [!DNL Salesforce] zu XDM

Um eine Quellverbindung zwischen [!DNL Salesforce] und Platform herzustellen, müssen die [!DNL Salesforce]-Quelldatenfelder den entsprechenden Ziel-XDM-Feldern zugeordnet werden, bevor sie in Platform erfasst werden.

Im Folgenden finden Sie detaillierte Informationen zu den Feldzuordnungsregeln zwischen [!DNL Salesforce] Datensätzen und Platform:

- [Kontakte](../adobe-applications/mapping/salesforce.md#contact)
- [Leads](../adobe-applications/mapping/salesforce.md#lead)
- [Konten](../adobe-applications/mapping/salesforce.md#account)
- [Opportunities](../adobe-applications/mapping/salesforce.md#opportunity)
- [Rollen von Kontakten bei Opportunities](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [Kampagnen](../adobe-applications/mapping/salesforce.md#campaign)
- [Kampagnenmitglieder](../adobe-applications/mapping/salesforce.md#campaign-member)
- [Account-Kontaktbeziehung](../adobe-applications/mapping/salesforce.md#account-contact-relation)

## Einrichten des Namespace- und Schemadienstprogramms für die automatische Schemaerstellung[!DNL Salesforce]

Um die [!DNL Salesforce]-Quelle als Teil von [!DNL B2B-CDP] zu verwenden, müssen Sie zunächst ein [!DNL Postman]-Dienstprogramm einrichten, um Ihre [!DNL Salesforce]-Namespaces und -Schemas automatisch zu generieren. Die folgende Dokumentation enthält zusätzliche Informationen zum Einrichten des Dienstprogramms [!DNL Postman] :

- Sie können die Sammlung und Umgebung des Dienstprogramms für die automatische Generierung von Namespace- und Schemas von diesem [GitHub-Repository](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility) herunterladen.
- Informationen zur Verwendung von Platform-APIs, einschließlich Details zum Sammeln von Werten für erforderliche Kopfzeilen und zum Lesen von Beispiel-API-Aufrufen, finden Sie im Leitfaden zu den ersten Schritten mit Platform-APIs ](../../../landing/api-guide.md).[
- Informationen zum Generieren Ihrer Anmeldeinformationen für Platform-APIs finden Sie im Tutorial zum [Authentifizieren und Zugreifen auf Experience Platform-APIs](../../../landing/api-authentication.md).
- Informationen zum Einrichten von [!DNL Postman] für Platform-APIs finden Sie im Tutorial zum [Einrichten der Entwicklerkonsole und  [!DNL Postman]](../../../landing/postman.md).

Mit der Einrichtung einer Platform-Entwicklerkonsole und [!DNL Postman] können Sie jetzt mit der Anwendung der entsprechenden Umgebungswerte auf Ihre [!DNL Postman] -Umgebung beginnen.

Die folgende Tabelle enthält Beispielwerte sowie zusätzliche Informationen zum Ausfüllen Ihrer [!DNL Postman] -Umgebung:

| Variable | Beschreibung | Beispiel |
| --- | --- | --- |
| `CLIENT_SECRET` | Eine eindeutige Kennung, mit der Ihr `{ACCESS_TOKEN}` generiert wird. Informationen zum Abrufen Ihrer `{CLIENT_SECRET}` finden Sie im Tutorial zum [Authentifizieren und Zugreifen auf Experience Platform-APIs](../../../landing/api-authentication.md) . | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | Das JSON-Web-Token (JWT) ist eine Authentifizierungsberechtigung, die zum Generieren Ihres {ACCESS_TOKEN} verwendet wird. Informationen zum Generieren Ihrer `{JWT_TOKEN}` finden Sie im Tutorial zum [Authentifizieren und Zugreifen auf Experience Platform-APIs](../../../landing/api-authentication.md) . | `{JWT_TOKEN}` |
| `API_KEY` | Eine eindeutige Kennung, mit der Aufrufe an Experience Platform-APIs authentifiziert werden. Informationen zum Abrufen Ihrer `{API_KEY}` finden Sie im Tutorial zum [Authentifizieren und Zugreifen auf Experience Platform-APIs](../../../landing/api-authentication.md) . | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Das Autorisierungstoken, das zum Abschließen von Aufrufen an Experience Platform-APIs erforderlich ist. Informationen zum Abrufen Ihrer `{ACCESS_TOKEN}` finden Sie im Tutorial zum [Authentifizieren und Zugreifen auf Experience Platform-APIs](../../../landing/api-authentication.md) . | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | In Bezug auf [!DNL Marketo] ist dieser Wert fest festgelegt und immer auf: `ent_dataservices_sdk` festgelegt. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | Der `global` -Container enthält alle vom Experience Platform-Partner bereitgestellten Standardklassen, Schemafeldgruppen, Datentypen und Schemata. In Bezug auf [!DNL Marketo] ist dieser Wert festgelegt und immer auf `global` gesetzt. | `global` |
| `PRIVATE_KEY` | Eine Berechtigung zum Authentifizieren Ihrer [!DNL Postman] -Instanz bei Experience Platform-APIs. Anweisungen zum Abrufen Ihrer {PRIVATE_KEY} finden Sie im Tutorial zum Einrichten der Entwicklerkonsole und [Einrichten der Entwicklerkonsole und  [!DNL Postman]](../../../landing/postman.md) . | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Eine Berechtigung zur Integration in Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Das Identity Management-System (IMS) stellt das Framework für die Authentifizierung bei Adobe-Diensten bereit. In Bezug auf [!DNL Marketo] ist dieser Wert festgelegt und immer auf: `ims-na1.adobelogin.com` festgelegt. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Eine Unternehmenseinheit, die Produkte und Dienste besitzen oder lizenzieren und Zugriff auf ihre Mitglieder gewähren kann. Anweisungen zum Abrufen Ihrer `{ORG_ID}` -Informationen finden Sie im Tutorial zum Einrichten der Entwicklerkonsole mit [und  [!DNL Postman]](../../../landing/postman.md) . | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | Der Name der verwendeten virtuellen Sandbox-Partition. | `prod` |
| `TENANT_ID` | Eine ID, mit der sichergestellt wird, dass die von Ihnen erstellten Ressourcen den richtigen Namespace aufweisen und in Ihrem Unternehmen enthalten sind. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | Der URL-Endpunkt, an den Sie API-Aufrufe durchführen. Dieser Wert ist fest und immer auf `http://platform.adobe.io/` festgelegt. | `http://platform.adobe.io/` |
| `munchkinId` | Die eindeutige ID für Ihr [!DNL Marketo]-Konto. Informationen zum Abrufen Ihrer `munchkinId` finden Sie im Tutorial zum [Authentifizieren Ihrer [!DNL Marketo] Instanz](../adobe-applications/marketo/marketo-auth.md) . | `123-ABC-456` |
| `sfdc_org_id` | Die Organisations-ID für Ihr [!DNL Salesforce]-Konto. Weitere Informationen zum Erwerb Ihrer [!DNL Salesforce] Organisations-ID finden Sie im folgenden [[!DNL Salesforce] Handbuch](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) . | `00D4W000000FgYJUA0` |
| `has_abm` | Ein boolean -Wert, der anzeigt, ob Sie [!DNL Marketo Account-Based Marketing] abonniert haben. | `false` |
| `has_msi` | Ein boolean -Wert, der anzeigt, ob Sie bei [!DNL Marketo Sales Insight] angemeldet sind. | `false` |

{style="table-layout:auto"}

### Scripts ausführen

Nachdem Sie die [!DNL Postman] -Sammlung und -Umgebung eingerichtet haben, können Sie das Skript jetzt über die [!DNL Postman] -Oberfläche ausführen.

Wählen Sie in der Benutzeroberfläche von [!DNL Postman] den Stammordner des Autogenerator-Dienstprogramms aus und wählen Sie dann **[!DNL Run]** aus der oberen Kopfzeile aus.

![root-folder](../../images/tutorials/create/salesforce/root-folder.png)

Die Oberfläche [!DNL Runner] wird angezeigt. Stellen Sie von hier aus sicher, dass alle Kontrollkästchen aktiviert sind, und wählen Sie dann **[!DNL Run Namespaces and Schemas Autogeneration Utility]** aus.

![run-generator](../../images/tutorials/create/salesforce/run-generator.png)

Eine erfolgreiche Anfrage erstellt die B2B-Namespaces und -Schemas gemäß den Beta-Spezifikationen.

## Verbinden von [!DNL Salesforce] mit Platform mithilfe von APIs

Die folgende Dokumentation enthält Informationen zur Verbindung von [!DNL Salesforce] mit Platform mithilfe von APIs oder der Benutzeroberfläche:

- [Salesforce-Basisverbindung mithilfe der Flow Service-API erstellen](../../tutorials/api/create/crm/salesforce.md)
- [Erkunden von Datentabellen mithilfe der Flow Service-API](../../tutorials/api/explore/tabular.md)
- [Erstellen eines Datenflusses für eine CRM-Quelle mithilfe der Flow Service-API](../../tutorials/api/collect/crm.md)

## Verbinden von [!DNL Salesforce] mit Platform über die Benutzeroberfläche

- [Erstellen einer Salesforce-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/crm/salesforce.md)
- [Erstellen eines Datenflusses für eine CRM-Verbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/crm.md)
