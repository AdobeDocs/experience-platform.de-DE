---
title: Übersicht über den Salesforce Source Connector
description: Erfahren Sie, wie Sie Salesforce mithilfe von APIs oder der Benutzeroberfläche mit Adobe Experience Platform verbinden.
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

Um eine Quellverbindung zwischen [!DNL Salesforce] und Platform herzustellen, müssen die [!DNL Salesforce] Quelldatenfelder den entsprechenden XDM-Zielfeldern zugeordnet werden, bevor sie in Platform aufgenommen werden.

Siehe die folgenden Informationen zu den Feldzuordnungsregeln zwischen [!DNL Salesforce] Datensätzen und Platform:

- [Kontakte](../adobe-applications/mapping/salesforce.md#contact)
- [Leads](../adobe-applications/mapping/salesforce.md#lead)
- [Konten](../adobe-applications/mapping/salesforce.md#account)
- [Opportunities](../adobe-applications/mapping/salesforce.md#opportunity)
- [Rollen von Kontakten bei Opportunities](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [Kampagnen](../adobe-applications/mapping/salesforce.md#campaign)
- [Kampagnenmitglieder](../adobe-applications/mapping/salesforce.md#campaign-member)
- [Account-Kontaktbeziehung](../adobe-applications/mapping/salesforce.md#account-contact-relation)

## Einrichten des [!DNL Salesforce] Namespace und des Dienstprogramms zur automatischen Schemaerstellung

Um die [!DNL Salesforce] als Teil von [!DNL B2B-CDP] zu verwenden, müssen Sie zunächst ein [!DNL Postman]-Dienstprogramm einrichten, um Ihre [!DNL Salesforce] Namespaces und Schemata automatisch zu generieren. Die folgende Dokumentation enthält zusätzliche Informationen zum Einrichten des [!DNL Postman]:

- Sie können den Namespace und die Dienstprogrammsammlung zur automatischen Schemaerstellung sowie die Umgebung aus diesem GitHub[Repository ](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Informationen zur Verwendung von Platform-APIs, einschließlich Details zum Erfassen von Werten für erforderliche Kopfzeilen und zum Lesen von Beispiel-API-Aufrufen, finden Sie im Handbuch [Erste Schritte mit Platform-APIs](../../../landing/api-guide.md).
- Informationen zum Generieren Ihrer Anmeldeinformationen für Platform-APIs finden Sie im Tutorial zum [Authentifizieren und Zugreifen auf Experience Platform-APIs](../../../landing/api-authentication.md).
- Informationen zum Einrichten von [!DNL Postman] für Platform-APIs finden Sie im Tutorial zum Einrichten [ Entwicklerkonsole und  [!DNL Postman]](../../../landing/postman.md).

Wenn eine Platform-Entwicklerkonsole und [!DNL Postman] eingerichtet sind, können Sie jetzt damit beginnen, die entsprechenden Umgebungswerte auf Ihre [!DNL Postman] anzuwenden.

Die folgende Tabelle enthält Beispielwerte sowie zusätzliche Informationen zum Ausfüllen Ihrer [!DNL Postman]:

| Variable | Beschreibung | Beispiel |
| --- | --- | --- |
| `CLIENT_SECRET` | Eine eindeutige Kennung, die zum Generieren Ihres `{ACCESS_TOKEN}` verwendet wird. Weitere Informationen zum Abrufen [ Experience Platform-APIs finden Sie im Tutorial ](../../../landing/api-authentication.md)Authentifizieren und Zugreifen auf `{CLIENT_SECRET}`&quot;. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | Das JSON Web Token (JWT) ist eine Authentifizierungsberechtigung, die zum Generieren Ihres {ACCESS_TOKEN} verwendet wird. Informationen zum Generieren [ Experience Platform-APIs finden Sie im Tutorial ](../../../landing/api-authentication.md)Authentifizieren und Zugreifen auf `{JWT_TOKEN}`-APIs“ . | `{JWT_TOKEN}` |
| `API_KEY` | Eine eindeutige Kennung, die zum Authentifizieren von Aufrufen an Experience Platform-APIs verwendet wird. Weitere Informationen zum Abrufen [ Experience Platform-APIs finden Sie im Tutorial ](../../../landing/api-authentication.md)Authentifizieren und Zugreifen auf `{API_KEY}`&quot;. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Das zum Abschließen von Aufrufen an Experience Platform-APIs erforderliche Autorisierungs-Token. Weitere Informationen zum Abrufen [ Experience Platform-APIs finden Sie im Tutorial ](../../../landing/api-authentication.md)Authentifizieren und Zugreifen auf `{ACCESS_TOKEN}`&quot;. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | In Bezug auf [!DNL Marketo] ist dieser Wert fest und wird immer auf `ent_dataservices_sdk` festgelegt. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | Der `global`-Container enthält alle von standardmäßigen Adobe- und Experience Platform-Partnern bereitgestellten Klassen, Schemafeldgruppen, Datentypen und Schemata. In Bezug auf [!DNL Marketo] ist dieser Wert fest und wird immer auf `global` festgelegt. | `global` |
| `PRIVATE_KEY` | Eine Berechtigung, die zum Authentifizieren Ihrer [!DNL Postman] bei Experience Platform-APIs verwendet wird. Anweisungen zum Abrufen Ihrer {PRIVATE_KEY} finden Sie im Tutorial zum Einrichten [ Entwicklerkonsole und  [!DNL Postman]](../../../landing/postman.md)Einrichten der Entwicklerkonsole und . | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Eine Berechtigung für die Integration mit Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Das Identity Management-System (IMS) stellt das Framework für die Authentifizierung für Adobe-Services bereit. In Bezug auf [!DNL Marketo] ist dieser Wert fest und wird immer auf `ims-na1.adobelogin.com` festgelegt. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Eine Unternehmenseinheit, die Produkte und Dienstleistungen besitzen oder lizenzieren und ihren Mitgliedern Zugang gewähren kann. Anweisungen zum Abrufen Ihrer `{ORG_ID}` finden [ im Tutorial zum Einrichten  [!DNL Postman]](../../../landing/postman.md) Entwicklerkonsole und . | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | Der Name der virtuellen Sandbox-Partition, die Sie verwenden. | `prod` |
| `TENANT_ID` | Eine ID, mit der sichergestellt wird, dass die von Ihnen erstellten Ressourcen über den richtigen Namespace verfügen und in Ihrer Organisation enthalten sind. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | Der URL-Endpunkt, an den Sie API-Aufrufe durchführen. Dieser Wert ist fest und immer auf `http://platform.adobe.io/` festgelegt. | `http://platform.adobe.io/` |
| `munchkinId` | Die eindeutige ID für Ihr [!DNL Marketo]. Informationen zum Abrufen Ihrer `munchkinId` finden [ im Tutorial  [!DNL Marketo] Authentifizieren ](../adobe-applications/marketo/marketo-auth.md)Instanz) . | `123-ABC-456` |
| `sfdc_org_id` | Die Organisations-ID für Ihr [!DNL Salesforce]. Weiterführende Informationen dazu, [[!DNL Salesforce]  Sie Ihre [!DNL Salesforce]-Organisations-ID erhalten, finden Sie im folgenden Handbuch](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) . | `00D4W000000FgYJUA0` |
| `has_abm` | Ein boolescher Wert, der angibt, ob Sie [!DNL Marketo Account-Based Marketing] abonniert haben. | `false` |
| `has_msi` | Ein boolescher Wert, der angibt, ob Sie [!DNL Marketo Sales Insight] abonniert haben. | `false` |

{style="table-layout:auto"}

### Skripte ausführen

Nachdem Sie Ihre [!DNL Postman] und Umgebung eingerichtet haben, können Sie das Skript jetzt über die [!DNL Postman] ausführen.

Wählen Sie in der [!DNL Postman] den Stammordner des Dienstprogramms zur automatischen Generierung und dann **[!DNL Run]** aus der oberen Kopfzeile aus.

![root-folder](../../images/tutorials/create/salesforce/root-folder.png)

Die [!DNL Runner] wird angezeigt. Stellen Sie von hier aus sicher, dass alle Kontrollkästchen aktiviert sind, und wählen Sie dann **[!DNL Run Namespaces and Schemas Autogeneration Utility]** aus.

![run-generator](../../images/tutorials/create/salesforce/run-generator.png)

Bei einer erfolgreichen Anfrage werden die B2B-Namespaces und -Schemas gemäß den Beta-Spezifikationen erstellt.

## Verbinden von [!DNL Salesforce] mit Platform mithilfe von APIs

Die folgende Dokumentation enthält Informationen zur Verbindung von [!DNL Salesforce] mit Platform mithilfe von APIs oder der Benutzeroberfläche:

- [Erstellen einer Salesforce-Basisverbindung mithilfe der Flow Service-API](../../tutorials/api/create/crm/salesforce.md)
- [Erkunden von Datentabellen mithilfe der Flow Service-API](../../tutorials/api/explore/tabular.md)
- [Erstellen eines Datenflusses für eine CRM-Quelle mithilfe der Flow Service-API](../../tutorials/api/collect/crm.md)

## Verbinden von [!DNL Salesforce] mit Platform über die Benutzeroberfläche

- [Erstellen einer Salesforce-Quellverbindung über die Benutzeroberfläche](../../tutorials/ui/create/crm/salesforce.md)
- [Erstellen eines Datenflusses für eine CRM-Verbindung über die Benutzeroberfläche](../../tutorials/ui/dataflow/crm.md)
