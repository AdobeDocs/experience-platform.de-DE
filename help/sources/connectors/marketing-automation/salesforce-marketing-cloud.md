---
keywords: Experience Platform; Homepage; beliebte Themen; Salesforce Marketing Cloud; Salesforce-Marketing Cloud; Marketing-Automatisierung
solution: Experience Platform
title: Salesforce Marketing Cloud Source - Überblick
description: Erfahren Sie, wie Sie Salesforce Marketing Cloud über APIs oder die Benutzeroberfläche mit Adobe Experience Platform verbinden.
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 45%

---

# (Beta) [!DNL Salesforce Marketing Cloud]

>[!NOTE]
>
>Die [!DNL Salesforce Marketing Cloud]-Quelle befindet sich in der Beta-Phase. Siehe [Quellen – Übersicht](../../home.md#terms-and-conditions) für weitere Informationen zur Verwendung von Beta-gekennzeichneten Quellen.

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

## Verbinden von [!DNL Salesforce Marketing Cloud] mit Platform mithilfe von APIs

Die folgende Dokumentation enthält Informationen zur Verbindung [!DNL Salesforce Marketing Cloud] zur Plattform mithilfe von APIs:

* [Erstellen einer Salesforce-Marketing Cloud-Basisverbindung mithilfe der Flow Service-API](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [Erkunden von Datentabellen mithilfe der Flow Service-API](../../tutorials/api/explore/tabular.md)
* [Erstellen eines Datenflusses für eine Marketing-Automatisierungsquelle mithilfe der Flow Service-API](../../tutorials/api/collect/marketing-automation.md)

## Verbinden von [!DNL Salesforce Marketing Cloud] mit Platform über die Benutzeroberfläche

Die folgende Dokumentation enthält Informationen zur Verbindung [!DNL Salesforce Marketing Cloud] zur Plattform mithilfe der Benutzeroberfläche:

* [Erstellen einer Salesforce-Marketing Cloud-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [Erstellen eines Datenflusses für eine Marketing-Automatisierungs-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/marketing-automation.md)
