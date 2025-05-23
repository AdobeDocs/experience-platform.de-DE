---
solution: Experience Platform
title: Übersicht über Salesforce Marketing Cloud Source
description: Erfahren Sie, wie Sie Salesforce Marketing Cloud mithilfe von APIs oder der Benutzeroberfläche mit Adobe Experience Platform verbinden.
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
last-substantial-update: 2025-04-29T00:00:00Z
source-git-commit: ce96dbc64845fddb40ebee709828c56d51a6c6ba
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 14%

---

# [!DNL Salesforce Marketing Cloud]

>[!WARNING]
>
>Die [!DNL Salesforce Marketing Cloud] wird im Januar 2026 eingestellt. Eine neue Quelle wird noch in diesem Jahr als Alternative veröffentlicht. Nach der Veröffentlichung der neuen Quelle müssen Sie die Migration zur neuen Quelle planen, indem Sie neue Kontoverbindungen und Datenflüsse vor Ende Januar 2026 erstellen.

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform unterstützt die Aufnahme von Daten aus Marketing-Automatisierungssystemen von Drittanbietern. Der Support für Anbieter von Marketing-Automatisierung umfasst [!DNL Salesforce Marketing Cloud].

## Voraussetzungen

Bevor Sie Ihre [!DNL Salesforce Marketing Cloud] mit Experience Platform verbinden können, müssen Sie sicherstellen, dass die folgenden **Berechtigungsbereiche** für Ihre [!DNL Salesforce Marketing Cloud] Kombination aus Client-ID und Client-Geheimnis bereitgestellt werden:

* `campaign_read`
* `list_and_subscribers_read`

Sie können Bereiche anfordern, indem Sie die `v2/userinfo` Ressource der [!DNL Salesforce Marketing Cloud]-API aufrufen. Anleitungen zum Anfordern und Vergleichen von Bereichen finden [[!DNL Salesforce Marketing Cloud]  im Dokument ](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html>)API-Integrationsberechtigungsumfänge“.

Weitere Informationen zu Bereichen, einschließlich einer Liste der zugehörigen Berechtigungen und Verhaltensweisen, finden Sie in diesem [[!DNL Salesforce Marketing Cloud] REST-API-Dokument](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html>).

>[!IMPORTANT]
>
>Die Aufnahme benutzerdefinierter Objekte wird von der [!DNL Salesforce Marketing Cloud] derzeit nicht unterstützt.

## Zulassungsliste von IP-Adressen

Sie müssen Ihrer Zulassungsliste regionsspezifische IP-Adressen hinzufügen, bevor Sie Ihre Quellen mit Experience Platform verbinden. Weitere Informationen finden Sie im Handbuch unter [Zulassungsauflistung von IP-Adressen für die Verbindung mit Experience Platform](../../ip-address-allow-list.md) .

>[!WARNING]
>
>Wenn Sie die erforderlichen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, stellt Ihr [!DNL Salesforce Marketing Cloud] keine Verbindung zu Experience Platform her.

## Verbinden von [!DNL Salesforce Marketing Cloud] mit Experience Platform mithilfe von APIs

Die folgende Dokumentation enthält Informationen zum Verbinden von [!DNL Salesforce Marketing Cloud] mit Experience Platform mithilfe von APIs:

* [Erstellen einer Salesforce Marketing Cloud-Basisverbindung mithilfe der Flow Service-API](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [Erkunden von Datentabellen mithilfe der Flow Service-API](../../tutorials/api/explore/tabular.md)
* [Erstellen eines Datenflusses für eine Marketing-Automatisierungsquelle mithilfe der Flow Service-API](../../tutorials/api/collect/marketing-automation.md)

## Verbinden von [!DNL Salesforce Marketing Cloud] mit Experience Platform über die Benutzeroberfläche

Die folgende Dokumentation enthält Informationen zum Verbinden von [!DNL Salesforce Marketing Cloud] mit Experience Platform über die Benutzeroberfläche:

* [Erstellen einer Salesforce Marketing Cloud-Quellverbindung über die Benutzeroberfläche](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [Erstellen eines Datenflusses für eine Marketing-Automatisierungs-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/marketing-automation.md)
