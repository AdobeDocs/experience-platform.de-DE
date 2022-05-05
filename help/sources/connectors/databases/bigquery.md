---
keywords: Experience Platform;home;popular topics;BigQuery;bigquery;Google BigQuery;Google bigquery
solution: Experience Platform
title: Google BigQuery Source Connector - Überblick
topic-legacy: overview
description: Erfahren Sie, wie Sie Google BigQuery über APIs oder die Benutzeroberfläche mit Adobe Experience Platform verbinden.
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: fa861e9740e05b4fcc4e8039bb288301d42b8357
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 34%

---

# (Beta) [!DNL Google BigQuery] Connector

>[!NOTE]
>
>Die [!DNL Google BigQuery] ist in der Beta-Phase. Siehe [Quellen - Übersicht](../../home.md#terms-and-conditions) Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectoren.

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

Detaillierte Anweisungen zum Generieren von OAuth 2.0-Anmeldeinformationen finden Sie unter [!DNL Google] APIs, siehe die folgenden [[!DNL Google] OAuth 2.0-Authentifizierungshandbuch](https://developers.google.com/identity/protocols/oauth2).

## Verbinden von [!DNL Google BigQuery] mit Platform

Die folgende Dokumentation enthält Informationen dazu, wie Sie [!DNL Google BigQuery] mithilfe von APIs oder der Benutzeroberfläche mit Platform verbinden können:

### Verwenden von APIs

- [Erstellen einer Google BigQuery-Basisverbindung mithilfe der Flow Service-API](../../tutorials/api/create/databases/bigquery.md)
- [Datentabellen mithilfe der Flow Service-API durchsuchen](../../tutorials/api/explore/tabular.md)
- [Erstellen eines Datenflusses für eine Datenbankquelle mithilfe der Flow Service-API](../../tutorials/api/collect/database-nosql.md)

### Verwenden der Benutzeroberfläche

- [Erstellen einer Google BigQuery-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/databases/bigquery.md)
- [Erstellen eines Datenflusses für eine Datenbankquellenverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/databases.md)
