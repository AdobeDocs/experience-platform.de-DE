---
title: Google BigQuery Source Connector - Überblick
description: Erfahren Sie, wie Sie Google BigQuery über APIs oder die Benutzeroberfläche mit Adobe Experience Platform verbinden.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 36%

---

# [!DNL Google BigQuery] source

>[!IMPORTANT]
>
>Die [!DNL Google BigQuery] -Quelle ist im Quellkatalog für Benutzer verfügbar, die Real-time Customer Data Platform Ultimate erworben haben.

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

[!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus Datenbanken von Drittanbietern. Platform kann eine Verbindung zu verschiedenen Arten von Datenbanken wie z. B. relationalen, NoSQL- oder Data Warehouse-Datenbanken herstellen. Unterstützung für Datenbankanbieter umfasst [!DNL Google BigQuery].

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

## Voraussetzungen

Im folgenden Abschnitt finden Sie weitere Informationen zur erforderlichen Einrichtung, bevor Sie eine [!DNL Google BigQuery] Quellverbindung.

### Generieren Sie Ihre [!DNL Google BigQuery] Anmeldeinformationen

Verbindung herstellen [!DNL Google BigQuery] in Platform verwenden, müssen Sie Werte für die folgenden Anmeldeinformationen generieren:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `project` | Das Projekt ist die Organisationseinheit auf der Basisebene für Ihre [!DNL Google Cloud] Ressourcen, einschließlich [!DNL Google BigQuery]. |
| `clientID` | Die Client-ID beträgt die Hälfte Ihrer [!DNL Google BigQuery] OAuth 2.0-Anmeldeinformationen. |
| `clientSecret` | Das Client-Geheimnis ist die andere Hälfte Ihrer [!DNL Google BigQuery] OAuth 2.0-Anmeldeinformationen. |
| `refreshToken` | Mit dem Aktualisierungstoken können Sie neue Zugriffstoken für Ihre API abrufen. Zugriffstoken haben eine begrenzte Lebensdauer und können im Laufe Ihres Projekts ablaufen. Sie können das Aktualisierungstoken verwenden, um sich bei Bedarf zu authentifizieren und nachfolgende Zugriffstoken für Ihr Projekt anzufordern. |
| `largeResultsDataSetId` | Die vorab erstellten  [!DNL Google BigQuery] Datensatz-ID, die erforderlich ist, um die Unterstützung für große Ergebnismengen zu ermöglichen. |

Detaillierte Anweisungen zum Generieren von OAuth 2.0-Anmeldeinformationen finden Sie unter [!DNL Google] APIs, siehe die folgenden [[!DNL Google] OAuth 2.0-Authentifizierungshandbuch](https://developers.google.com/identity/protocols/oauth2).

## Verbinden von [!DNL Google BigQuery] mit Platform

Die folgende Dokumentation enthält Informationen dazu, wie Sie [!DNL Google BigQuery] mithilfe von APIs oder der Benutzeroberfläche mit Platform verbinden können:

### Verwenden von APIs

- [Erstellen einer Google BigQuery-Basisverbindung mithilfe der Flow Service-API](../../tutorials/api/create/databases/bigquery.md)
- [Erkunden von Datentabellen mithilfe der Flow Service-API](../../tutorials/api/explore/tabular.md)
- [Erstellen eines Datenflusses für eine Datenbankquelle mithilfe der Flow Service-API](../../tutorials/api/collect/database-nosql.md)

### Verwenden der Benutzeroberfläche

- [Erstellen einer Google BigQuery-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/databases/bigquery.md)
- [Erstellen eines Datenflusses für eine Datenbankquellenverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/databases.md)
