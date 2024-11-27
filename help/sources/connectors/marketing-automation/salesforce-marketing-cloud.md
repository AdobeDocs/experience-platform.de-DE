---
solution: Experience Platform
title: Überblick über Salesforce Marketing Cloud Source
description: Erfahren Sie, wie Sie Salesforce Marketing Cloud mit Adobe Experience Platform über APIs oder die Benutzeroberfläche verbinden.
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
last-substantial-update: 2023-05-25T00:00:00Z
source-git-commit: 9ca4f19f7b59f075250bce7035303e11d3f3710f
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 42%

---

# [!DNL Salesforce Marketing Cloud]

>[!WARNING]
>
>Die Quelle [!DNL Salesforce Marketing Cloud] wird Ende Juni 2025 eingestellt.

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform unterstützt die Erfassung von Daten aus Marketingautomatisierungssystemen von Drittanbietern. Unterstützung für Anbieter von Marketing-Automatisierung umfasst [!DNL Salesforce Marketing Cloud].

## Voraussetzungen

Bevor Sie Ihre [!DNL Salesforce Marketing Cloud]-Quelle mit Platform verbinden können, müssen Sie sicherstellen, dass die folgenden **Berechtigungsbereiche** für Ihre [!DNL Salesforce Marketing Cloud]-Client-ID und die Client-Geheimkombination bereitgestellt werden:

* `campaign_read`
* `list_and_subscribers_read`

Sie können Perimeter anfordern, indem Sie die `v2/userinfo` -Ressource der [!DNL Salesforce Marketing Cloud]-API aufrufen. Eine Anleitung zum Anfordern und Vergleichen von Bereichen finden Sie im Dokument [[!DNL Salesforce Marketing Cloud] API-Integrationsberechtigungsbereiche](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html>) .

Weitere Informationen zu Bereichen, einschließlich einer Liste der zugehörigen Berechtigungen und Verhaltensweisen, finden Sie in diesem [[!DNL Salesforce Marketing Cloud] REST API-Dokument](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html>) .

>[!IMPORTANT]
>
>Die Erfassung benutzerdefinierter Objekte wird von der Quellintegration für [!DNL Salesforce Marketing Cloud] derzeit nicht unterstützt.

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Performance-Einbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

## Verbinden von [!DNL Salesforce Marketing Cloud] mit Platform mithilfe von APIs

Die folgende Dokumentation enthält Informationen dazu, wie Sie mithilfe von APIs [!DNL Salesforce Marketing Cloud] mit Platform verbinden:

* [Erstellen einer Basisverbindung mit dem Salesforce-Marketing Cloud mithilfe der Flow Service-API](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [Erkunden von Datentabellen mithilfe der Flow Service-API](../../tutorials/api/explore/tabular.md)
* [Erstellen eines Datenflusses für eine Marketing-Automatisierungsquelle mithilfe der Flow Service-API](../../tutorials/api/collect/marketing-automation.md)

## Verbinden von [!DNL Salesforce Marketing Cloud] mit Platform über die Benutzeroberfläche

Die folgende Dokumentation enthält Informationen dazu, wie Sie mithilfe der Benutzeroberfläche [!DNL Salesforce Marketing Cloud] mit Platform verbinden:

* [Erstellen einer Salesforce-Marketing Cloud-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [Erstellen eines Datenflusses für eine Marketing-Automatisierungs-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/marketing-automation.md)
