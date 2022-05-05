---
keywords: Experience Platform; Homepage; beliebte Themen; Salesforce Marketing Cloud; Salesforce-Marketing Cloud; Marketing-Automatisierung
solution: Experience Platform
title: Salesforce Marketing Cloud Source - Überblick
topic-legacy: overview
description: Erfahren Sie, wie Sie Salesforce Marketing Cloud über APIs oder die Benutzeroberfläche mit Adobe Experience Platform verbinden.
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
source-git-commit: fa861e9740e05b4fcc4e8039bb288301d42b8357
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 28%

---

# (Beta) [!DNL Salesforce Marketing Cloud]

>[!NOTE]
>
>Die [!DNL Salesforce Marketing Cloud] -Quelle befindet sich in der Beta-Phase. Siehe [Quellen - Übersicht](../../home.md#terms-and-conditions) für weitere Informationen zur Verwendung von Beta-beschrifteten Quellen.

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

[!DNL Experience Platform] unterstützt die Erfassung von Daten aus Marketingautomatisierungssystemen von Drittanbietern. Unterstützung für Anbieter von Marketing-Automatisierungslösungen: [!DNL Salesforce Marketing Cloud].

## Voraussetzungen

Bevor Sie Ihre [!DNL Salesforce Marketing Cloud] -Quelle an Platform übermitteln, müssen Sie sicherstellen, dass Folgendes **Berechtigungsbereiche** für Ihre [!DNL Salesforce Marketing Cloud] Client-ID und Client-geheime Kombination:

* `campaign_read`
* `list_and_subscribers_read`

Sie können Scopes anfordern, indem Sie einen Aufruf an die `v2/userinfo` Ressource [!DNL Salesforce Marketing Cloud] API. Siehe [[!DNL Salesforce Marketing Cloud] Dokument zu Berechtigungsbereichen für API-Integration](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html) für Anleitungen zum Anfordern und Vergleichen von Bereichen.

Weitere Informationen zu Bereichen, einschließlich einer Liste der zugehörigen Berechtigungen und Verhaltensweisen, finden Sie in diesem [[!DNL Salesforce Marketing Cloud] REST-API-Dokument](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html).

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

## Verbinden [!DNL Salesforce Marketing Cloud] zur Plattform mithilfe von APIs

Die folgende Dokumentation enthält Informationen zur Verbindung [!DNL Salesforce Marketing Cloud] zur Plattform mithilfe von APIs:

* [Erstellen einer Salesforce-Marketing Cloud-Basisverbindung mithilfe der Flow Service-API](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [Datentabellen mithilfe der Flow Service-API durchsuchen](../../tutorials/api/explore/tabular.md)
* [Erstellen eines Datenflusses für eine Marketing-Automatisierungsquelle mithilfe der Flow Service-API](../../tutorials/api/collect/marketing-automation.md)

## Verbinden [!DNL Salesforce Marketing Cloud] zur Plattform mithilfe der Benutzeroberfläche

Die folgende Dokumentation enthält Informationen zur Verbindung [!DNL Salesforce Marketing Cloud] zur Plattform mithilfe der Benutzeroberfläche:

* [Erstellen einer Salesforce-Marketing Cloud-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [Erstellen eines Datenflusses für eine Verbindung zur Marketing-Automatisierungsquelle in der Benutzeroberfläche](../../tutorials/ui/dataflow/marketing-automation.md)
