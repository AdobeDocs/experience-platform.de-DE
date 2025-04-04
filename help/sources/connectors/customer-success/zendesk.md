---
title: Übersicht über den Zendesk Source Connector
description: Erfahren Sie, wie Sie Zendesk mithilfe von APIs oder der Benutzeroberfläche mit Adobe Experience Platform verbinden.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 9f245783-949d-4f40-9cf3-8991b4b6d780
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 27%

---

# [!DNL Zendesk]

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform ermöglicht die Aufnahme von Daten aus Drittanbieter-Anwendungen für das Customer Success Management. Zu den Anbietern, die Customer Success unterstützen, gehören [!DNL Zendesk].

Diese Adobe Experience Platform [Quellen](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=de) nutzt die [Zendesk-Such-API > Suchergebnisse exportieren](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) die Benutzerinformationen von Zendesk zur weiteren Verarbeitung an Experience Platform zurückgibt.

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Performance-Einbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

## [!DNL Zendesk] authentifizieren

[!DNL Zendesk] verwendet Träger-Token als Authentifizierungsmechanismus für die Kommunikation mit der [!DNL Zendesk]-API.

In diesem Abschnitt werden die Schritte beschrieben, die zur Authentifizierung Ihres [!DNL Zendesk]-Kontos erforderlich sind.

* Der erste Schritt bei der Authentifizierung Ihres [!DNL Zendesk]-Kontos besteht darin, sicherzustellen, dass Sie über [!DNL Zendesk] Support-Konto verfügen. Wenn Sie noch keines haben, sehen Sie die [[!DNL Zendesk] Anmeldeseite](https://www.zendesk.de/register/) um sich zu registrieren und Ihr Zendesk-Konto zu erstellen.
* Navigieren Sie nach der erfolgreichen Registrierung zur [[!DNL Zendesk] Website](https://www.zendesk.com/login/) und geben Sie Ihre **Subdomain** an.
* Wählen Sie als Nächstes **[!DNL Settings]** > **[!DNL Apps and Integrations]** > **[!DNL Zendesk API]** aus.
* Rufen Sie abschließend Ihr API-Token aus dem Abschnitt **[!DNL API token]** ab.

![Zendesk-API-Token](../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

Informationen zum Abrufen Ihrer Subdomain finden Sie im [[!DNL Zendesk documentation on subdomains]](<https://support.zendesk.com/hc/en-us/articles/4409381383578-Where-can-I-find-my-Zendesk-subdomain->) . Informationen zum Generieren Ihres API-Tokens finden Sie im [[!DNL Zendesk] Handbuch zum Generieren eines neuen API-Tokens](<https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token>).

Die folgende Dokumentation enthält Informationen zum Verbinden von [!DNL Zendesk] mit Experience Platform mithilfe von APIs oder der Benutzeroberfläche:

## Verbinden von [!DNL Zendesk] mit Experience Platform mithilfe von APIs

* [Erstellen einer Quellverbindung und eines Datenflusses für  [!DNL Zendesk]  mithilfe der Flow Service-API](../../tutorials/api/create/customer-success/zendesk.md)

## Verbinden von [!DNL Zendesk] mit Experience Platform über die Benutzeroberfläche

* [Erstellen einer  [!DNL Zendesk ]-Quellverbindung über die Benutzeroberfläche](../../tutorials/ui/create/customer-success/zendesk.md)
* [Erstellen eines Datenflusses für eine Customer-Success-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/customer-success.md)
