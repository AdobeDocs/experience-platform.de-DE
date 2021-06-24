---
keywords: Experience Platform;home;popular topics;BigQuery;bigquery;Google BigQuery;Google BigQuery;Google bigquery
solution: Experience Platform
title: Überblick über Google BigQuery Source Connector
topic-legacy: overview
description: Erfahren Sie, wie Sie mit APIs oder der Benutzeroberfläche Google BigQuery mit Adobe Experience Platform verbinden.
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 9d68e54baa894ebeff4603c7df01a1fe42aa217f
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 16%

---

# (Beta) [!DNL Google BigQuery] Connector

>[!NOTE]
>
>[!DNL Google BigQuery] befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectoren finden Sie unter [Quellen - Übersicht](../../home.md#terms-and-conditions) .

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen erfasst werden, darunter etwa Adobe-Anwendungen, Cloud-basierte Datenspeicher und Datenbanken.

[!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus Datenbanken von Drittanbietern. Platform kann eine Verbindung zu verschiedenen Arten von Datenbanken wie z. B. relationalen, NoSQL- oder Data Warehouse-Datenbanken herstellen. Unterstützung für Datenbankanbieter: [!DNL Google BigQuery].

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Weitere Informationen finden Sie auf der Seite [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md) .

## Voraussetzungen   

Im folgenden Abschnitt finden Sie weitere Informationen zur erforderlichen Einrichtung, bevor Sie eine [!DNL Google BigQuery]-Quellverbindung erstellen können.

### Generieren Sie Ihre [!DNL Google BigQuery]-Anmeldedaten

Um [!DNL Google BigQuery] mit Platform zu verbinden, müssen Sie Werte für die folgenden Anmeldedaten generieren:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `project` | Das Projekt ist die Organisationseinheit auf Basisebene für Ihre [!DNL Google Cloud]-Ressourcen, einschließlich [!DNL Google BigQuery]. |
| `clientID` | Die Client-ID entspricht der Hälfte Ihrer [!DNL Google BigQuery] OAuth 2.0-Anmeldedaten. |
| `clientSecret` | Das Client-Geheimnis ist die andere Hälfte Ihrer [!DNL Google BigQuery] OAuth 2.0-Anmeldedaten. |
| `refreshToken` | Mit dem Aktualisierungstoken können Sie neue Zugriffstoken für Ihre API abrufen. Zugriffstoken haben eine begrenzte Lebensdauer und können im Laufe Ihres Projekts ablaufen. Sie können das Aktualisierungstoken verwenden, um sich bei Bedarf zu authentifizieren und nachfolgende Zugriffstoken für Ihr Projekt anzufordern. |

Ausführliche Anweisungen zum Generieren von OAuth 2.0-Anmeldeinformationen für [!DNL Google]-APIs finden Sie im folgenden [[!DNL Google] OAuth 2.0-Authentifizierungshandbuch](https://developers.google.com/identity/protocols/oauth2).

## Verbinden von [!DNL Google BigQuery] mit Platform

Die folgende Dokumentation enthält Informationen dazu, wie Sie mithilfe von APIs oder der Benutzeroberfläche eine Verbindung von [!DNL Google BigQuery] mit Platform herstellen:

### Verwenden von APIs

- [Erstellen einer Google BigQuery-Quellverbindung mithilfe der Flow Service-API](../../tutorials/api/create/databases/bigquery.md)
- [Durchsuchen eines Datenbanksystems mithilfe der Flow Service-API](../../tutorials/api/explore/database-nosql.md)
- [Erfassen von Daten aus einer Datenbank mithilfe der Flow Service-API](../../tutorials/api/collect/database-nosql.md)

### Verwenden der UI

- [Erstellen einer Google BigQuery-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/databases/bigquery.md)
- [Konfigurieren eines Datenflusses für eine Datenbankverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/databases.md)
