---
title: SugarCRM Source - Übersicht
description: Erfahren Sie, wie Sie SugarCRM mithilfe von APIs oder der Benutzeroberfläche mit Adobe Experience Platform verbinden.
last-substantial-update: 2023-08-23T00:00:00Z
exl-id: 03fbc4e9-974d-494e-8463-756c96665fd5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 28%

---

# [!DNL SugarCRM]

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform unterstützt die Aufnahme von Daten aus einem CRM-Programm eines Drittanbieters. Unterstützung für CRM-Anbieter umfasst [!DNL SugarCRM].

[[!DNL SugarCRM]](https://www.sugarcrm.com/) ist ein CRM-System (Customer Relationship Management). Zu den Funktionen von [!DNL SugarCRM] gehören Sales-Force-Automatisierung, Marketing-Kampagnen, Kunden-Support, Zusammenarbeit, mobiles CRM, Social CRM und Reporting.

Mit der [!DNL SugarCRM] können Sie Konto-, Kontakt- und Ereignisdaten aus den folgenden API-Endpunkten aufnehmen:

* [Konten](https://market.apidocs.sugarcrm.com/#b0aeb0cd-80ea-4688-8474-54e4873f32f3)
* [Kontakte](https://market.apidocs.sugarcrm.com/#308c5025-9478-4de3-8a41-1fc3cff1d8d1)
* [Ereignisse](https://market.apidocs.sugarcrm.com/#516ec3b1-8e70-43d4-8bf2-38a2ae74c0a5)

[!DNL SugarCRM] verwendet Träger-Token als Authentifizierungsmechanismus für die Kommunikation mit den APIs für [!DNL SugarCRM]-Konten und Kontakte und der API für [!DNL SugarCRM].

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Performance-Einbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

## Voraussetzungen

Bevor Sie eine [!DNL SugarCRM]-Quellverbindung erstellen können, müssen Sie zunächst sicherstellen, dass Folgendes vorhanden ist:

* Ein [!DNL SugarMarket]. Sie müssen sich an Ihren [!DNL SugarCRM] Account Manager wenden, um ein gültiges [!DNL SugarMarket]-Konto zu erhalten, falls Sie noch keines haben.

* Ein eindeutiger API-Benutzername und ein eindeutiges Konto, getrennt von jedem Benutzerkonto, das mit dem Marketing- oder Verkaufsprozess verknüpft ist. Diese eindeutige Kombination aus Benutzername und Konto muss über API-Zugriffsberechtigungen verfügen. Weitere Informationen zum Einrichten eines Kontos finden Sie in der [[!DNL SugarMarket RESTFUL API]](https://market.apidocs.sugarcrm.com/#intro).

## Verbinden von [!DNL SugarCRM Accounts & Contacts] mit Experience Platform

* [Erstellen Sie eine Quellverbindung, um - [!DNL SugarCRM Accounts & Contacts]  mithilfe von APIs in Experience Platform zu ](../../tutorials/api/create/crm/sugarcrm-accounts-contacts.md).
* [Erstellen Sie eine Quellverbindung, um - [!DNL SugarCRM Accounts & Contacts]  über die Benutzeroberfläche in Experience Platform zu importieren](../../tutorials/ui/create/crm/sugarcrm-accounts-contacts.md).
* [Erstellen eines Datenflusses für eine CRM-Quelle mithilfe der Flow Service-API](../../tutorials/api/collect/crm.md)


## Verbinden von [!DNL SugarCRM Events] mit Experience Platform

* [Erstellen Sie eine Quellverbindung, um - [!DNL SugarCRM Events]  mithilfe von APIs in Experience Platform zu ](../../tutorials/ui/create/crm/sugarcrm-events.md).
* [Erstellen Sie eine Quellverbindung, um - [!DNL SugarCRM Events]  über die Benutzeroberfläche in Experience Platform zu importieren](../../tutorials/ui/create/crm/sugarcrm-events.md).
* [Erstellen eines Datenflusses für eine CRM-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/crm.md)
