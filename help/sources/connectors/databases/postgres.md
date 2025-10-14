---
title: Übersicht über den PostgreSQL Source-Connector
description: Erfahren Sie mehr über die PostgreSQL-Quelle in Adobe Experience Platform.
last-substantial-update: 2025-05-20T00:00:00Z
exl-id: 27b891c5-5fc5-4539-8f98-e3a53e2eefe3
source-git-commit: f4200ca71479126e585ac76dd399af4092fdf683
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 13%

---

# [!DNL PostgreSQL]

Lesen Sie dieses Dokument, um mehr über die erforderlichen Schritte zu erfahren, die Sie durchführen müssen, bevor Sie Ihre [!DNL PostgreSQL] mit Adobe Experience Platform verbinden können.

## Voraussetzungen {#prerequisites}

Lesen Sie die folgenden Abschnitte, um die erforderliche Einrichtung abzuschließen, bevor Sie Ihre [!DNL PostgreSQL]-Datenbank mit Experience Platform verbinden.

### Zulassungsliste von IP-Adressen

Sie müssen Ihrer Zulassungsliste regionsspezifische IP-Adressen hinzufügen, bevor Sie Ihre Quellen mit Experience Platform über Azure oder Amazon Web Services (AWS) verbinden. Weitere Informationen finden Sie im Handbuch unter [Zulassungsauflistung von IP-Adressen für die Verbindung mit Experience Platform auf Azure und AWS](../../ip-address-allow-list.md) .

### Bei Experience Platform auf Azure authentifizieren {#azure}

Sie müssen Werte für die folgenden Authentifizierungsdaten angeben, um [!DNL PostgreSQL] mit Experience Platform auf Azure zu verbinden.

>[!BEGINTABS]

>[!TAB Authentifizierung mit Kontoschlüssel]

Geben Sie Werte für die folgenden Anmeldeinformationen an, um Ihre [!DNL PostgreSQL]-Datenbank mithilfe der Kontoschlüsselauthentifizierung mit Experience Platform auf Azure zu verbinden.

| Anmeldedaten | Beschreibung |
| --- | --- |
| `connectionString` | Die mit Ihrem [!DNL PostgreSQL]-Konto verknüpfte Verbindungszeichenfolge. Das [!DNL PostgreSQL]-Verbindungszeichenfolgenmuster ist: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL PostgreSQL] ist `74a1c565-4e59-48d7-9d67-7c03b8a13137`. Diese Berechtigung ist nur erforderlich, wenn eine Verbindung über die [!DNL Flow Service]-API hergestellt wird. |

Weitere Informationen finden [[!DNL PostgreSQL]  in der &#x200B;](https://www.postgresql.org/docs/current/).

>[!TAB Einfache Authentifizierung]

Geben Sie Werte für die folgenden Anmeldeinformationen an, um Ihre [!DNL PostgreSQL]-Datenbank mithilfe der Standardauthentifizierung mit Experience Platform auf Azure zu verbinden.

| Anmeldedaten | Beschreibung |
| --- | --- |
| `server` | Der Name oder die IP-Adresse Ihrer [!DNL PostgreSQL]. |
| `port` | Der TCP-Port Ihres [!DNL PostgreSQL]. |
| `username` | Der Benutzername, der Ihrer [!DNL PostgreSQL]-Datenbankauthentifizierung zugeordnet ist. |
| `password` | Das Passwort, das mit Ihrer [!DNL PostgreSQL]-Datenbankauthentifizierung verknüpft ist. |
| `database` | Der Name der [!DNL PostgreSQL] Datenbank, mit der Sie eine Verbindung herstellen möchten. |
| `sslMode` | Die [!DNL Secure Sockets Layer] (SSL)-Methode, die auf Ihre Verbindung angewendet werden soll. Folgende Werte sind verfügbar: <ul><li>`Disable`: Verwenden Sie diese Option, um SSL zu deaktivieren. Wenn Ihr Server eine SSL-Konfiguration erfordert, schlägt die Verbindung fehl.</li><li>`Allow`: Verwenden Sie diese Option, um SSL-Verbindungen zuzulassen. Nicht-SSL-Verbindungen können weiterhin verwendet werden, wenn der Server sie unterstützt.</li><li>`Prefer`: Verwenden Sie diese Option, um SSL-Verbindungen zu bevorzugen, da der Server sie unterstützt. Diese Option ermöglicht auch Nicht-SSL-Verbindungen.</li><li>`Require`: Verwenden Sie diese Option, um SSL-Verbindungen als obligatorisch festzulegen. Wenn der Server SSL nicht unterstützt, schlagen die Verbindungen fehl.</li><li>`Verify-Ca`: Verwenden Sie diese Option, um Serverzertifikate zu überprüfen, während Verbindungen fehlschlagen, wenn der Server SSL nicht unterstützt.</li><li>`Verify-Full`: Verwenden Sie diese Option, um Serverzertifikate mit dem Host-Namen zu überprüfen, während Verbindungen fehlschlagen, wenn der Server SSL nicht unterstützt.</li></ul> |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL PostgreSQL] ist `74a1c565-4e59-48d7-9d67-7c03b8a13137`. Diese Berechtigung ist nur erforderlich, wenn eine Verbindung über die [!DNL Flow Service]-API hergestellt wird. |

Weitere Informationen finden [[!DNL PostgreSQL]  in der &#x200B;](https://www.postgresql.org/docs/current/).

>[!ENDTABS]

### Authentifizierung bei Experience Platform auf Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Dieser Abschnitt gilt für Implementierungen von Experience Platform, die auf Amazon Web Services (AWS) ausgeführt werden. Experience Platform, das auf AWS ausgeführt wird, steht derzeit einer begrenzten Anzahl von Kunden zur Verfügung. Weitere Informationen zur unterstützten Experience Platform-Infrastruktur finden Sie in der Übersicht zur [Experience Platform Multi-Cloud](../../../landing/multi-cloud.md).

Geben Sie Werte für die folgenden Anmeldeinformationen an, um Ihre [!DNL PostgreSQL]-Datenbank mithilfe der Standardauthentifizierung mit Experience Platform auf AWS zu verbinden.

| Anmeldedaten | Beschreibung |
| --- | --- |
| `server` | Der Name oder die IP-Adresse Ihrer [!DNL PostgreSQL]. |
| `port` | Der TCP-Port Ihres [!DNL PostgreSQL]. |
| `username` | Der Benutzername, der Ihrer [!DNL PostgreSQL]-Datenbankauthentifizierung zugeordnet ist. |
| `password` | Das Passwort, das mit Ihrer [!DNL PostgreSQL]-Datenbankauthentifizierung verknüpft ist. |
| `database` | Der Name der [!DNL PostgreSQL] Datenbank, mit der Sie eine Verbindung herstellen möchten. |
| `sslMode` | Ein boolescher Wert, der steuert, ob SSL je nach Server-Unterstützung erzwungen wird oder nicht. Die Standardeinstellung für diese Konfiguration ist `false`. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL PostgreSQL] ist `74a1c565-4e59-48d7-9d67-7c03b8a13137`. Diese Berechtigung ist nur erforderlich, wenn eine Verbindung über die [!DNL Flow Service]-API hergestellt wird. |

Weitere Informationen finden [[!DNL PostgreSQL]  in der &#x200B;](https://www.postgresql.org/docs/current/).

## Verbinden von [!DNL PostgreSQL] mit Experience Platform mithilfe von APIs

* [Erstellen einer  [!DNL PostgreSQL] -Basisverbindung mit der Flow Service-API](../../tutorials/api/create/databases/postgres.md)
* [Erkunden von Datentabellen mithilfe der Flow Service-API](../../tutorials/api/explore/tabular.md)
* [Erstellen eines Datenflusses für eine Datenbankquelle mithilfe der Flow Service-API](../../tutorials/api/collect/database-nosql.md)

## Verbinden von [!DNL PostgreSQL] mit Experience Platform über die Benutzeroberfläche

* [Erstellen einer  [!DNL PostgreSQL] -Quellverbindung über die Benutzeroberfläche](../../tutorials/ui/create/databases/postgres.md)
* [Erstellen eines Datenflusses für eine Datenbank-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/databases.md)
