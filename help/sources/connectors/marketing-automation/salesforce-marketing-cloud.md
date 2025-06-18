---
title: Übersicht über Salesforce Marketing Cloud Source
description: Erfahren Sie, wie Sie Salesforce Marketing Cloud mithilfe von APIs oder der Benutzeroberfläche mit Adobe Experience Platform verbinden.
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
last-substantial-update: 2025-05-17T00:00:00Z
source-git-commit: 0c0a58df4beae499008e52c118b40bed86ff0596
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 8%

---

# [!DNL Salesforce Marketing Cloud]

>[!WARNING]
>
>Die [!DNL Salesforce Marketing Cloud] wird im Januar 2026 eingestellt. Eine neue Quelle wird noch in diesem Jahr als Alternative veröffentlicht. Nach der Veröffentlichung der neuen Quelle müssen Sie die Migration zur neuen Quelle planen, indem Sie neue Kontoverbindungen und Datenflüsse vor Ende Januar 2026 erstellen.

[!DNL Salesforce Marketing Cloud] ermöglicht Ihnen die Verwaltung und Automatisierung der Kundeninteraktion über E-Mail, Mobilgeräte, soziale Medien und Werbung hinweg - und das alles auf einer Plattform. Mit Tools wie Email Studio, Journey Builder und Audience Builder können Sie personalisierte Kampagnen und Kunden-Journey erstellen, die auf Ihre Audience zugeschnitten sind.

Sie können die [!DNL Salesforce Marketing Cloud] verwenden, um Ihr Konto zu verbinden und Ihre Daten an Adobe Experience Platform zu übertragen.

## Voraussetzungen

Bevor Sie Ihre [!DNL Salesforce Marketing Cloud] mit Experience Platform verbinden können, müssen Sie sicherstellen, dass die folgenden **Berechtigungsbereiche** für Ihre [!DNL Salesforce Marketing Cloud] Kombination aus Client-ID und Client-Geheimnis bereitgestellt werden:

* `campaign_read`
* `list_and_subscribers_read`

Sie können Bereiche anfordern, indem Sie die `v2/userinfo` Ressource der [!DNL Salesforce Marketing Cloud]-API aufrufen. Anleitungen zum Anfordern und Vergleichen von Bereichen finden [[!DNL Salesforce Marketing Cloud]  im Dokument ](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html>)API-Integrationsberechtigungsumfänge“.

Weitere Informationen zu Bereichen, einschließlich einer Liste der zugehörigen Berechtigungen und Verhaltensweisen, finden Sie in diesem [[!DNL Salesforce Marketing Cloud] REST-API-Dokument](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html>).

>[!IMPORTANT]
>
>Die Aufnahme benutzerdefinierter Objekte wird von der [!DNL Salesforce Marketing Cloud] derzeit nicht unterstützt.

### Zulassungsliste von IP-Adressen

Sie müssen Ihrer Zulassungsliste regionsspezifische IP-Adressen hinzufügen, bevor Sie Ihre Quellen mit Experience Platform verbinden. Weitere Informationen finden Sie im Handbuch unter [Zulassungsauflistung von IP-Adressen für die Verbindung mit Experience Platform](../../ip-address-allow-list.md) .

>[!WARNING]
>
>Wenn Sie die erforderlichen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, stellt Ihr [!DNL Salesforce Marketing Cloud] keine Verbindung zu Experience Platform her.

### Bei Experience Platform auf Azure authentifizieren {#azure}

Sie müssen Werte für die folgenden Anmeldeinformationen angeben, um [!DNL Salesforce Marketing Cloud] mit Experience Platform on [!DNL Azure] zu verbinden.

| Anmeldedaten | Beschreibung |
| --- | --- |
| Host | Der Hostserver der Anwendung. Dies ist häufig Ihre Subdomain. **Hinweis:** Bei der Eingabe Ihres `host` müssen Sie den `{subdomain}.rest.marketingcloudapis.com` angeben. Wenn Ihre Host-URL beispielsweise `https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/` ist, müssen Sie `acme-ab12c3d4e5fg6hijk7lmnop8qrst.rest.marketingcloudapis.com/` als Host-Wert eingeben. |
| Client-ID | Die mit Ihrem [!DNL Salesforce Marketing Cloud] Programm verknüpfte Client-ID. |
| Client-Geheimnis | Das mit Ihrer [!DNL Salesforce Marketing Cloud]-Anwendung verknüpfte Client-Geheimnis. |
| Verbindungsspezifikations-ID | Die **Verbindungsspezifikation** stellt die Connector-Eigenschaften einer Datenquelle bereit. Dazu gehören Details wie Authentifizierungsspezifikationen und Anforderungen für die Erstellung von **Basis**- und **Quelle**-Verbindungen. [!DNL Salesforce Marketing Cloud] lautet die Verbindungsspezifikations-ID: `ea1c2a08-b722-11eb-8529-0242ac130003`. **Hinweis:** Diese Anmeldedaten sind nur bei der Verbindung über APIs erforderlich. |

### Authentifizierung bei Experience Platform auf Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Dieser Abschnitt gilt für Implementierungen von Experience Platform, die auf Amazon Web Services (AWS) ausgeführt werden. Experience Platform, das auf AWS ausgeführt wird, steht derzeit einer begrenzten Anzahl von Kunden zur Verfügung. Weitere Informationen zur unterstützten Experience Platform-Infrastruktur finden Sie in der Übersicht zur [Experience Platform Multi-Cloud](../../../landing/multi-cloud.md).

Sie müssen Werte für die folgenden Anmeldeinformationen angeben, um [!DNL Salesforce Marketing Cloud] mit Experience Platform auf AWS zu verbinden.

| Anmeldedaten | Beschreibung |
| --- | --- |
| Subdomain | Der eindeutige Teil der URL Ihrer [!DNL Salesforce Marketing Cloud], der zum Erstellen von API-Endpunkten verwendet wird. |
| Client-ID | Eine öffentliche Kennung für Ihre Anwendung, die erzeugt wird, wenn Sie ein installiertes Paket in [!DNL Salesforce Marketing Cloud] erstellen |
| Client-Geheimnis | Ein vertraulicher Schlüssel, der mit Ihrer Client-ID verknüpft ist und auch im installierten Paket generiert wird. |
| Verbindungsspezifikations-ID | Die **Verbindungsspezifikation** stellt die Connector-Eigenschaften einer Datenquelle bereit. Dazu gehören Details wie Authentifizierungsspezifikationen und Anforderungen für die Erstellung von **Basis**- und **Quelle**-Verbindungen. [!DNL Salesforce Marketing Cloud] lautet die Verbindungsspezifikations-ID: `ea1c2a08-b722-11eb-8529-0242ac130003`. **Hinweis:** Diese Anmeldedaten sind nur bei der Verbindung über APIs erforderlich. |

Weitere Informationen finden Sie in der [[!DNL Salesforce] Dokumentation zu Zugriffstoken für Server-zu-Server-Integrationen](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html).

## Verbinden von [!DNL Salesforce Marketing Cloud] mit Experience Platform mithilfe von APIs

Die folgende Dokumentation enthält Informationen zum Verbinden von [!DNL Salesforce Marketing Cloud] mit Experience Platform mithilfe von APIs:

* [Verbinden  [!DNL Salesforce Marketing Cloud]  Experience Platform mithilfe der Flow Service-API](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [Erkunden von Datentabellen mithilfe der Flow Service-API](../../tutorials/api/explore/tabular.md)
* [Erstellen eines Datenflusses für eine Marketing-Automatisierungsquelle mithilfe der Flow Service-API](../../tutorials/api/collect/marketing-automation.md)

## Verbinden von [!DNL Salesforce Marketing Cloud] mit Experience Platform über die Benutzeroberfläche

Die folgende Dokumentation enthält Informationen zum Verbinden von [!DNL Salesforce Marketing Cloud] mit Experience Platform über die Benutzeroberfläche:

* [Verbinden  [!DNL Salesforce Marketing Cloud]  Experience Platform über die Benutzeroberfläche](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [Erstellen eines Datenflusses für eine Marketing-Automatisierungs-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/marketing-automation.md)
