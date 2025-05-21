---
title: Übersicht über den MySQL Source Connector
description: Erfahren Sie, wie Sie MySQL mithilfe von APIs oder der Benutzeroberfläche mit Adobe Experience Platform verbinden.
last-substantial-update: 2025-05-20T00:00:00Z
exl-id: a18e8e69-880f-4bee-b339-726091d6f858
source-git-commit: b73ced639100c95f6c62be92d4796a206a688958
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 5%

---

# [!DNL MySQL]

[!DNL MySQL] ist ein relationales Open-Source-Datenbankverwaltungssystem, das zum Speichern und Verwalten strukturierter Daten verwendet wird. Es organisiert Daten in Tabellen und verwendet SQL (Structured Query Language) zum Abfragen und Aktualisieren von Informationen. [!DNL MySQL] wird häufig in Web-Anwendungen verwendet, unterstützt mehrere Plattformen und ist für seine Geschwindigkeit, Zuverlässigkeit und Benutzerfreundlichkeit bekannt.

Sie können die [!DNL MySQL] verwenden, um Ihr -Konto zu verbinden und Daten aus Ihrer [!DNL MySQL]-Datenbank in Adobe Experience Platform aufzunehmen.

## Voraussetzungen {#prerequisites}

Lesen Sie die folgenden Abschnitte, um die erforderliche Einrichtung abzuschließen, bevor Sie Ihr [!DNL MySQl]-Konto mit Experience Platform verbinden.

### Zulassungsliste von IP-Adressen

Sie müssen Ihrer Zulassungsliste regionsspezifische IP-Adressen hinzufügen, bevor Sie Ihre Quellen mit Experience Platform über Azure oder Amazon Web Services (AWS) verbinden. Weitere Informationen finden Sie im Handbuch unter [Zulassungsauflistung von IP-Adressen für die Verbindung mit Experience Platform auf Azure und AWS](../../ip-address-allow-list.md) .

### Bei Experience Platform auf Azure authentifizieren {#azure}

Sie können entweder die Kontoschlüsselauthentifizierung oder die Standardauthentifizierung verwenden, um Ihre [!DNL MySQL] mit Experience Platform auf Azure zu verbinden.

>[!BEGINTABS]

>[!TAB Authentifizierung mit Kontoschlüssel]

Geben Sie Werte für die folgenden Anmeldeinformationen an, um Ihre [!DNL MySQL] mithilfe der Kontoschlüsselauthentifizierung mit Experience Platform zu verbinden.

| Anmeldedaten | Beschreibung |
| --- | --- |
| `connectionString` | Die Ihrem Konto zugeordnete [!DNL MySQL]-Verbindungszeichenfolge. Das [!DNL MySQL]-Verbindungszeichenfolgenmuster ist: `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL MySQL] ist `26d738e0-8963-47ea-aadf-c60de735468a`. |

Weitere Informationen finden Sie in der [[!DNL MySQL] Dokumentation zu Verbindungszeichenfolgen](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html).

>[!TAB Einfache Authentifizierung]

Geben Sie Werte für die folgenden Anmeldeinformationen an, um Ihre [!DNL MySQL]-Datenbank mithilfe der Standardauthentifizierung mit Experience Platform zu verbinden.

| Anmeldedaten | Beschreibung |
| --- | --- |
| `server` | Der Name oder die IP-Adresse Ihrer [!DNL MySQL]. |
| `username` | Der Benutzername, der Ihrer [!DNL MySQL]-Datenbankauthentifizierung zugeordnet ist. |
| `password` | Das Passwort, das mit Ihrer [!DNL MySQL]-Datenbankauthentifizierung verknüpft ist. |
| `database` | Der Name der [!DNL MySQL] Datenbank, mit der Sie eine Verbindung herstellen möchten. |
| `sslMode` | Die [!DNL Secure Sockets Layer] (SSL)-Methode, die auf Ihre Verbindung angewendet werden soll. Folgende Werte sind verfügbar: <ul><li>`DISABLED`: Verwenden Sie diese Option, um SSL zu deaktivieren. Wenn Ihr Server eine SSL-Konfiguration erfordert, schlägt die Verbindung fehl</li><li>`PREFERRED`: Verwenden Sie diese Option, um SSL-Verbindungen zu bevorzugen, da der Server sie unterstützt. Diese Option ermöglicht auch Nicht-SSL-Verbindungen.</li><li>`REQUIRED`: Verwenden Sie diese Option, um SSL-Verbindungen als obligatorisch festzulegen. Wenn der Server SSL nicht unterstützt, schlagen die Verbindungen fehl.</li><li>`Verify-Ca`: Verwenden Sie diese Option, um Serverzertifikate zu überprüfen, während Verbindungen fehlschlagen, wenn der Server SSL nicht unterstützt.</li><li>`Verify Identity`: Verwenden Sie diese Option, um Serverzertifikate mit dem Host-Namen zu überprüfen, während Verbindungen fehlschlagen, wenn der Server SSL nicht unterstützt.</li></ul> |

>[!ENDTABS]

### Authentifizierung bei Experience Platform auf Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Dieser Abschnitt gilt für Implementierungen von Experience Platform, die auf Amazon Web Services (AWS) ausgeführt werden. Experience Platform, das auf AWS ausgeführt wird, steht derzeit einer begrenzten Anzahl von Kunden zur Verfügung. Weitere Informationen zur unterstützten Experience Platform-Infrastruktur finden Sie in der Übersicht zur [Experience Platform Multi-Cloud](../../../landing/multi-cloud.md).

Sie müssen Werte für die folgenden Anmeldeinformationen angeben, um [!DNL MySQL] mit Experience Platform auf AWS zu verbinden.

| Anmeldedaten | Beschreibung |
| --- | --- |
| `server` | Der Name oder die IP der [!DNL MySQL]. |
| `username` | Der Name Ihrer Datenbank. |
| `password` | Der Benutzername, der Ihrer Datenbank entspricht. |
| `database` | Das Passwort, das Ihrer Datenbank entspricht. |
| `sslMode` | Ein boolescher Wert, der steuert, ob SSL je nach Server-Unterstützung erzwungen wird oder nicht. Die Standardeinstellung für diese Konfiguration ist `false`. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL MySQL] ist `26d738e0-8963-47ea-aadf-c60de735468a`. **Hinweis**: Diese Berechtigung ist nur erforderlich, wenn eine Verbindung über die [!DNL Flow Service]-API hergestellt wird. |

## Verbinden von [!DNL MySQL] mit Experience Platform mithilfe von APIs

- [Verbinden  [!DNL MySQL]  Datenbank mithilfe der Flow Service-API](../../tutorials/api/create/databases/mysql.md)
- [Erkunden von Datentabellen mithilfe der Flow Service-API](../../tutorials/api/explore/tabular.md)
- [Erstellen eines Datenflusses für eine Datenbankquelle mithilfe der Flow Service-API](../../tutorials/api/collect/database-nosql.md)

## Verbinden von MySQL mit Experience Platform über die Benutzeroberfläche

- [Verbinden Ihrer  [!DNL MySQL]  mit Experience Platform über die Benutzeroberfläche](../../tutorials/ui/create/databases/mysql.md)
- [Erstellen eines Datenflusses für eine Datenbank-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/databases.md)
