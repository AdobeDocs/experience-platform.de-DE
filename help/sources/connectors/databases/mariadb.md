---
title: Übersicht über MariaDB Source Connector
description: Erfahren Sie, wie Sie MariaDB mithilfe von APIs oder der Benutzeroberfläche mit Adobe Experience Platform verbinden.
exl-id: 37b8f991-dca9-4f85-9bdd-4927a015e4c0
source-git-commit: 0bf31c76f86b4515688d3aa60deb8744e38b4cd5
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 21%

---

# [!DNL MariaDB]

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Experience Platform]-Services zu strukturieren, zu kennzeichnen und zu verbessern. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform ermöglicht die Aufnahme von Daten aus Datenbanken von Drittanbietern. [!DNL Experience Platform] können eine Verbindung zu verschiedenen Datenbanktypen herstellen, z. B. relationale Datenbanken, NoSQL oder Data Warehouses. Die Unterstützung für Datenbankanbieter umfasst [!DNL MariaDB].

## Voraussetzungen {#prerequisites}

Lesen Sie die folgenden Abschnitte, um die erforderliche Einrichtung abzuschließen, bevor Sie Ihr [!DNL MariaDB]-Konto mit Experience Platform verbinden.

### Zulassungsliste von IP-Adressen

Sie müssen Ihrer Zulassungsliste regionsspezifische IP-Adressen hinzufügen, bevor Sie Ihre Quellen mit Experience Platform über Azure oder Amazon Web Services (AWS) verbinden. Weitere Informationen finden Sie im Handbuch unter [Zulassungsauflistung von IP-Adressen für die Verbindung mit Experience Platform auf Azure und AWS](../../ip-address-allow-list.md) .

### Bei Experience Platform auf Azure authentifizieren {#azure}

Sie müssen Werte für die folgenden Anmeldeinformationen angeben, um [!DNL MariaDB] mit Experience Platform auf Azure zu verbinden.

>[!BEGINTABS]

>[!TAB Authentifizierung mit Kontoschlüssel]

Um die Kontoschlüsselauthentifizierung zu verwenden, geben Sie die entsprechenden Werte für die folgenden Anmeldeinformationen an.

| Anmeldedaten | Beschreibung |
| --- | --- |
| `connectionString` | Die mit Ihrer [!DNL MariaDB] verknüpfte Verbindungszeichenfolge. Das [!DNL MariaDB]-Verbindungszeichenfolgenmuster ist: `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL MariaDB] ist `3000eb99-cd47-43f3-827c-43caf170f015`. **Hinweis**: Diese Berechtigung ist nur erforderlich, wenn eine Verbindung über die [!DNL Flow Service]-API hergestellt wird. |

Weiterführende Informationen zum Abrufen einer Verbindungszeichenfolge finden Sie in diesem [[!DNL MariaDB] Dokument](https://mariadb.com/kb/en/about-mariadb-connector-odbc/).

>[!TAB Einfache Authentifizierung]

Um die Standardauthentifizierung zu verwenden, geben Sie die entsprechenden Werte für die folgenden Anmeldeinformationen an.

| Anmeldedaten | Beschreibung |
| --- | --- |
| `server` | Der Name oder die IP der [!DNL MariaDB]. |
| `username` | Der Name Ihrer Datenbank. |
| `port` | Die Port-Nummer des Kommunikationsendpunkts, mit dem Sie eine Verbindung herstellen. |
| `password` | Der Benutzername, der Ihrer Datenbank entspricht. |
| `database` | Das Passwort, das Ihrer Datenbank entspricht. |
| `sslMode` | Die Methode, mit der Daten während der Datenübertragung verschlüsselt werden. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL MariaDB] ist `3000eb99-cd47-43f3-827c-43caf170f015`. **Hinweis**: Diese Berechtigung ist nur erforderlich, wenn eine Verbindung über die [!DNL Flow Service]-API hergestellt wird. |

Weiterführende Informationen zum Abrufen einer Verbindungszeichenfolge finden Sie in diesem [[!DNL MariaDB] Dokument](https://mariadb.com/kb/en/about-mariadb-connector-odbc/).

>[!ENDTABS]

### Authentifizierung bei Experience Platform auf Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Dieser Abschnitt gilt für Implementierungen von Experience Platform, die auf Amazon Web Services (AWS) ausgeführt werden. Experience Platform, das auf AWS ausgeführt wird, steht derzeit einer begrenzten Anzahl von Kunden zur Verfügung. Weitere Informationen zur unterstützten Experience Platform-Infrastruktur finden Sie in der Übersicht zur [Experience Platform Multi-Cloud](../../../landing/multi-cloud.md).

Sie müssen Werte für die folgenden Anmeldeinformationen angeben, um [!DNL MariaDB] mit Experience Platform auf AWS zu verbinden.

| Anmeldedaten | Beschreibung |
| --- | --- |
| `server` | Der Name oder die IP der [!DNL MariaDB]. |
| `username` | Der Name Ihrer Datenbank. |
| `port` | Die Port-Nummer des Kommunikationsendpunkts, mit dem Sie eine Verbindung herstellen. |
| `password` | Der Benutzername, der Ihrer Datenbank entspricht. |
| `database` | Das Passwort, das Ihrer Datenbank entspricht. |
| `sslMode` | Die Methode, mit der Daten während der Datenübertragung verschlüsselt werden. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL MariaDB] ist `3000eb99-cd47-43f3-827c-43caf170f015`. **Hinweis**: Diese Berechtigung ist nur erforderlich, wenn eine Verbindung über die [!DNL Flow Service]-API hergestellt wird. |

Weiterführende Informationen zum Abrufen einer Verbindungszeichenfolge finden Sie in diesem [[!DNL MariaDB] Dokument](https://mariadb.com/kb/en/about-mariadb-connector-odbc/).

## Verbinden von [!DNL MariaDB] mit Experience Platform mithilfe von APIs

- [Erstellen einer MariaDB-Basisverbindung mithilfe der Flow Service-API](../../tutorials/api/create/databases/mariadb.md)
- [Erkunden von Datentabellen mithilfe der Flow Service-API](../../tutorials/api/explore/tabular.md)
- [Erstellen eines Datenflusses für eine Datenbankquelle mithilfe der Flow Service-API](../../tutorials/api/collect/database-nosql.md)

## Verbinden von [!DNL MariaDB] mit Experience Platform über die Benutzeroberfläche

- [Erstellen einer MariaDB-Quellverbindung über die Benutzeroberfläche](../../tutorials/ui/create/databases/mariadb.md)
- [Erstellen eines Datenflusses für eine Datenbank-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/databases.md)
