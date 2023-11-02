---
title: Zendesk Source Connector - Überblick
description: Erfahren Sie, wie Sie Zendesk über APIs oder die Benutzeroberfläche mit Adobe Experience Platform verbinden.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 9f245783-949d-4f40-9cf3-8991b4b6d780
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 44%

---

# [!DNL Zendesk]

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform ermöglicht die Aufnahme von Daten aus Drittanbieter-Anwendungen für das Customer Success Management. Zu den Support-Anbietern für den Kundenerfolg zählen: [!DNL Zendesk].

Diese Adobe Experience Platform [sources](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=de) nutzt die [Zendesk Search API > Suchergebnisse exportieren](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) , das Benutzerinformationen zur weiteren Verarbeitung an Experience Platform von Zendesk zurückgibt.

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

## Authentifizieren Ihrer [!DNL Zendesk] account

[!DNL Zendesk] verwendet Trägertoken als Authentifizierungsmechanismus für die Kommunikation mit dem [!DNL Zendesk] API.

In diesem Abschnitt werden die erforderlichen Schritte beschrieben, die zum Authentifizieren Ihrer [!DNL Zendesk] -Konto.

* Der erste Schritt bei der Authentifizierung Ihrer [!DNL Zendesk] dient dazu, sicherzustellen, dass Sie [!DNL Zendesk] Support-Konto. Wenn Sie noch keine haben, sehen Sie die [[!DNL Zendesk] Registrierungsseite](https://www.zendesk.de/register/) , um sich zu registrieren und Ihr Zendesk-Konto zu erstellen.
* Nachdem Sie sich erfolgreich registriert haben, navigieren Sie zum [[!DNL Zendesk] website](https://www.zendesk.com/login/) und stellen Sie **Subdomain**.
* Wählen Sie als Nächstes **[!DNL Settings]** > **[!DNL Apps and Integrations]** > **[!DNL Zendesk API]**.
* Rufen Sie abschließend Ihr API-Token aus der **[!DNL API token]** Abschnitt.

![Zendesk-API-Token](../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

Siehe [[!DNL Zendesk documentation on subdomains]](<https://support.zendesk.com/hc/en-us/articles/4409381383578-Where-can-I-find-my-Zendesk-subdomain->) für Informationen zum Abrufen Ihrer Subdomain. Informationen zum Generieren Ihres API-Tokens finden Sie in der [[!DNL Zendesk] Handbuch zum Generieren eines neuen API-Tokens](<https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token>).

Die folgende Dokumentation enthält Informationen zur Verbindung von [!DNL Zendesk] mit Platform mithilfe von APIs oder der Benutzeroberfläche:

## Verbinden von [!DNL Zendesk] mit Platform mithilfe von APIs

* [Erstellen Sie eine Quellverbindung und einen Datenfluss für [!DNL Zendesk] Verwenden der Flow Service-API](../../tutorials/api/create/customer-success/zendesk.md)

## Verbinden von [!DNL Zendesk] mit Platform über die Benutzeroberfläche

* [Erstellen einer  [!DNL Zendesk ]-Quellverbindung über die Benutzeroberfläche](../../tutorials/ui/create/customer-success/zendesk.md)
* [Erstellen eines Datenflusses für eine Kundenerfolgsquellenverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/customer-success.md)
