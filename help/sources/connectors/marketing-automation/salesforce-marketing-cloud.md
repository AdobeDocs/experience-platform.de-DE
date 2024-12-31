---
solution: Experience Platform
title: Salesforce Marketing Cloud Source - Überblick
description: Erfahren Sie, wie Sie Salesforce Marketing Cloud mithilfe von APIs oder der Benutzeroberfläche mit Adobe Experience Platform verbinden.
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
>Die [!DNL Salesforce Marketing Cloud] wird Ende Juni 2025 eingestellt.

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform unterstützt die Aufnahme von Daten aus Marketing-Automatisierungssystemen von Drittanbietern. Der Support für Anbieter von Marketing-Automatisierung umfasst [!DNL Salesforce Marketing Cloud].

## Voraussetzungen

Bevor Sie Ihre [!DNL Salesforce Marketing Cloud] mit Platform verbinden können, müssen Sie sicherstellen, dass die folgenden **Berechtigungsbereiche** für Ihre [!DNL Salesforce Marketing Cloud] Kombination aus Client-ID und Client-Geheimnis bereitgestellt werden:

* `campaign_read`
* `list_and_subscribers_read`

Sie können Bereiche anfordern, indem Sie die `v2/userinfo` Ressource der [!DNL Salesforce Marketing Cloud]-API aufrufen. Anleitungen zum Anfordern und Vergleichen von Bereichen finden [[!DNL Salesforce Marketing Cloud]  im Dokument ](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html>)API-Integrationsberechtigungsumfänge“.

Weitere Informationen zu Bereichen, einschließlich einer Liste der zugehörigen Berechtigungen und Verhaltensweisen, finden Sie in diesem [[!DNL Salesforce Marketing Cloud] REST-API-Dokument](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html>).

>[!IMPORTANT]
>
>Die Aufnahme benutzerdefinierter Objekte wird von der [!DNL Salesforce Marketing Cloud] derzeit nicht unterstützt.

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Performance-Einbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

## Verbinden von [!DNL Salesforce Marketing Cloud] mit Platform mithilfe von APIs

Die folgende Dokumentation enthält Informationen zum Verbinden von [!DNL Salesforce Marketing Cloud] mit Platform mithilfe von APIs:

* [Erstellen einer Salesforce-Marketing Cloud-Basisverbindung mithilfe der Flow Service-API](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [Erkunden von Datentabellen mithilfe der Flow Service-API](../../tutorials/api/explore/tabular.md)
* [Erstellen eines Datenflusses für eine Marketing-Automatisierungsquelle mithilfe der Flow Service-API](../../tutorials/api/collect/marketing-automation.md)

## Verbinden von [!DNL Salesforce Marketing Cloud] mit Platform über die Benutzeroberfläche

Die folgende Dokumentation enthält Informationen zum Verbinden von [!DNL Salesforce Marketing Cloud] mit Platform über die Benutzeroberfläche:

* [Erstellen einer Salesforce-Marketing Cloud-Quellverbindung über die Benutzeroberfläche](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [Erstellen eines Datenflusses für eine Marketing-Automatisierungs-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/marketing-automation.md)
