---
title: SugarCRM-Quelle - Überblick
description: Erfahren Sie, wie Sie SugarCRM über APIs oder die Benutzeroberfläche mit Adobe Experience Platform verbinden.
last-substantial-update: 2023-08-23T00:00:00Z
exl-id: 03fbc4e9-974d-494e-8463-756c96665fd5
source-git-commit: 68c14d7b187075b4af6b019a8bd1ca2625beabde
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 41%

---

# [!DNL SugarCRM]

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform unterstützt die Aufnahme von Daten aus einer Drittanbieter-CRM-Anwendung. Unterstützung für CRM-Anbieter umfasst [!DNL SugarCRM].

[[!DNL SugarCRM]](https://www.sugarcrm.com/) ist ein CRM-System (Customer Relationship Management). [!DNL SugarCRM]Zu den Funktionen gehören Automatisierung von Verkaufsaktivitäten, Marketing-Kampagnen, Kundensupport, Zusammenarbeit, Mobile CRM, Social CRM und Reporting.

Die [!DNL SugarCRM] -Quelle können Sie Konten-, Kontakt- und Ereignisdaten aus den folgenden API-Endpunkten erfassen:

* [Konten](https://market.apidocs.sugarcrm.com/#b0aeb0cd-80ea-4688-8474-54e4873f32f3)
* [Kontakte](https://market.apidocs.sugarcrm.com/#308c5025-9478-4de3-8a41-1fc3cff1d8d1)
* [Ereignisse](https://market.apidocs.sugarcrm.com/#516ec3b1-8e70-43d4-8bf2-38a2ae74c0a5)

[!DNL SugarCRM] verwendet Trägertoken als Authentifizierungsmechanismus für die Kommunikation mit dem [!DNL SugarCRM] Konto- und Kontakt-APIs und die [!DNL SugarCRM] Events-API.

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

## Voraussetzungen

Bevor Sie eine [!DNL SugarCRM] -Quellverbindung verwenden, müssen Sie zunächst Folgendes sicherstellen:

* A [!DNL SugarMarket] -Konto. Sie müssen Ihre [!DNL SugarCRM] Kundenbetreuer zum Abrufen eines gültigen [!DNL SugarMarket] , wenn Sie noch keinen haben.

* Ein eindeutiger API-Benutzername und -Konto, die von einem Benutzerkonto getrennt sind, das mit dem Marketing- oder Verkaufsprozess verknüpft ist. Diese eindeutige Kombination von Benutzername und Konto muss über API-Zugriffsberechtigungen verfügen. Weitere Informationen zum Einrichten eines Kontos finden Sie unter [[!DNL SugarMarket RESTFUL API]](https://market.apidocs.sugarcrm.com/#intro) Dokumentation.

## Verbinden von [!DNL SugarCRM Accounts & Contacts] mit Platform

* [Erstellen Sie eine Quellverbindung, um [!DNL SugarCRM Accounts & Contacts] -Daten durch Verwenden von APIs in Platform zu importieren](../../tutorials/api/create/crm/sugarcrm-accounts-contacts.md).
* [Erstellen Sie eine Quellverbindung, um sie zu bringen [!DNL SugarCRM Accounts & Contacts] Daten an Platform mithilfe der Benutzeroberfläche](../../tutorials/ui/create/crm/sugarcrm-accounts-contacts.md).
* [Erstellen eines Datenflusses für eine CRM-Quelle mithilfe der Flow Service-API](../../tutorials/api/collect/crm.md)


## Verbinden von [!DNL SugarCRM Events] mit Platform

* [Erstellen Sie eine Quellverbindung, um [!DNL SugarCRM Events] -Daten durch Verwenden von APIs in Platform zu importieren](../../tutorials/ui/create/crm/sugarcrm-events.md).
* [Erstellen Sie eine Quellverbindung, um sie zu bringen [!DNL SugarCRM Events] Daten an Platform mithilfe der Benutzeroberfläche](../../tutorials/ui/create/crm/sugarcrm-events.md).
* [Erstellen eines Datenflusses für eine CRM-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/crm.md)
