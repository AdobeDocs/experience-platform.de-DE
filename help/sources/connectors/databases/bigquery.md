---
title: Google BigQuery Source Connector - Überblick
description: Erfahren Sie, wie Sie Google BigQuery über APIs oder die Benutzeroberfläche mit Adobe Experience Platform verbinden.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 1fa79b31b5a257ebb3cbd60246b757d8a4a63d7c
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 25%

---

# [!DNL Google BigQuery] source

>[!IMPORTANT]
>
>Die Quelle &quot;[!DNL Google BigQuery]&quot; steht Benutzern, die Real-time Customer Data Platform Ultimate erworben haben, im Quellkatalog zur Verfügung.

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Lesen Sie dieses Dokument für die erforderlichen Schritte, die Sie ausführen müssen, um Ihr [!DNL Google BigQuery]-Konto erfolgreich mit Experience Platform zu verbinden.

## Voraussetzungen {#prerequisites}

Im folgenden Abschnitt finden Sie weitere Informationen zur erforderlichen Einrichtung, bevor Sie eine [!DNL Google BigQuery]-Quellverbindung erstellen können.

### IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Performance-Einbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

### Generieren Sie Ihre [!DNL Google BigQuery]-Anmeldedaten {#credentials}

Um [!DNL Google BigQuery] mit Experience Platform zu verbinden, müssen Sie Werte für die folgenden Anmeldedaten generieren:

>[!BEGINTABS]

>[!TAB Grundlegende Authentifizierung]

Um sich mit einer Kombination aus OAuth 2.0 und einfacher Authentifizierung zu authentifizieren, geben Sie die entsprechenden Werte für die folgenden Anmeldeinformationen ein.

| Anmeldedaten | Beschreibung |
| --- | --- |
| `project` | Das Projekt ist die Organisationseinheit auf Basisebene für Ihre [!DNL Google Cloud] -Ressourcen, einschließlich [!DNL Google BigQuery]. |
| `clientID` | Die Client-ID entspricht der Hälfte Ihrer [!DNL Google BigQuery] OAuth 2.0-Anmeldedaten. |
| `clientSecret` | Das Client-Geheimnis ist die andere Hälfte Ihrer [!DNL Google BigQuery] OAuth 2.0-Anmeldedaten. |
| `refreshToken` | Mit dem Aktualisierungstoken können Sie neue Zugriffstoken für Ihre API abrufen. Zugriffstoken haben eine begrenzte Lebensdauer und können im Laufe Ihres Projekts ablaufen. Sie können das Aktualisierungstoken verwenden, um sich bei Bedarf zu authentifizieren und nachfolgende Zugriffstoken für Ihr Projekt anzufordern. |
| `largeResultsDataSetId` | (Optional) Die vorab erstellte Datensatz-ID [!DNL Google BigQuery] , die erforderlich ist, um die Unterstützung für große Ergebnismengen zu ermöglichen. |

Ausführliche Anweisungen zum Generieren von OAuth 2.0-Anmeldeinformationen für [!DNL Google] -APIs finden Sie im folgenden [[!DNL Google] OAuth 2.0-Authentifizierungshandbuch](https://developers.google.com/identity/protocols/oauth2).

>[!TAB Dienstauthentifizierung]

Um sich mithilfe der Dienstauthentifizierung zu authentifizieren, geben Sie die entsprechenden Werte für die folgenden Anmeldeinformationen ein.

**Hinweis**: Ihr Dienstkonto muss über ausreichende Berechtigungen verfügen, z. B.: **[!DNL BigQuery Job User]**, **[!DNL BigQuery Data Viewer]**, **[!DNL BigQuery Read Session User]** und **[!DNL BigQuery Data Owner]**, um sich erfolgreich bei der Dienstauthentifizierung authentifizieren zu können.

| Anmeldedaten | Beschreibung |
| --- | --- |
| `projectId` | Die Kennung des [!DNL Google BigQuery] , mit dem Sie eine Abfrage durchführen möchten. |
| `keyFileContent` | Die Schlüsseldatei, die zum Authentifizieren des Dienstkontos verwendet wird. Sie können diesen Wert aus dem [[!DNL Google Cloud service accounts] Dashboard](https://console.cloud.google.com) abrufen. Der Inhalt der Schlüsseldatei liegt im JSON-Format vor. Sie müssen dies bei der Authentifizierung bei Experience Platform in [!DNL Base64] verschlüsseln. |
| `largeResultsDataSetId` | (Optional) Die vorab erstellte Datensatz-ID [!DNL Google BigQuery] , die erforderlich ist, um die Unterstützung für große Ergebnismengen zu ermöglichen. |

Weitere Informationen zur Verwendung von Dienstkonten in [!DNL Google BigQuery] finden Sie im Handbuch zu [Verwendung von Dienstkonten in  [!DNL Google BigQuery]](https://cloud.google.com/bigquery/docs/use-service-accounts).

>[!ENDTABS]

## Verbinden von [!DNL Google BigQuery] mit Platform

Die folgende Dokumentation enthält Informationen dazu, wie Sie [!DNL Google BigQuery] mithilfe von APIs oder der Benutzeroberfläche mit Platform verbinden können:

### Verwenden von APIs

- [Erstellen einer Google BigQuery-Basisverbindung mithilfe der Flow Service-API](../../tutorials/api/create/databases/bigquery.md)
- [Erkunden von Datentabellen mithilfe der Flow Service-API](../../tutorials/api/explore/tabular.md)
- [Erstellen eines Datenflusses für eine Datenbankquelle mithilfe der Flow Service-API](../../tutorials/api/collect/database-nosql.md)

### Verwenden der Benutzeroberfläche

- [Erstellen einer Google BigQuery-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/databases/bigquery.md)
- [Erstellen eines Datenflusses für eine Datenbankquellenverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/databases.md)
