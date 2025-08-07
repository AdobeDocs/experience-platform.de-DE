---
title: Übersicht über den Oracle DB Source Connector
description: Erfahren Sie, wie Sie Oracle mithilfe von APIs oder der Benutzeroberfläche mit Adobe Experience Platform verbinden.
last-substantial-update: 2025-08-06T00:00:00Z
exl-id: be422cf8-fb24-48c7-8369-34f0f2ec95fc
source-git-commit: aa5496be968ee6f117649a6fff2c9e83a4ed7681
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 8%

---

# [!DNL Oracle DB]

[!DNL Oracle DB] ist ein leistungsstarkes relationales Datenbankmanagementsystem, das von [!DNL Oracle Corporation] entwickelt wurde. Mit [!DNL Oracle DB] können Sie große Mengen strukturierter Daten effizient und sicher speichern, verwalten und abrufen.

Verwenden Sie die [!DNL Oracle DB] im Adobe Experience Platform-Quellkatalog, um Ihre Datenbank zu verbinden und Daten in Experience Platform aufzunehmen.

## Voraussetzungen {#prerequisites}

Lesen Sie die folgenden Abschnitte, um die erforderliche Einrichtung abzuschließen, bevor Sie Ihr [!DNL Oracle DB]-Konto mit Experience Platform verbinden.

### Zulassungsliste von IP-Adressen

Sie müssen Ihrer Zulassungsliste regionsspezifische IP-Adressen hinzufügen, bevor Sie Ihre Quellen mit Experience Platform über Azure oder Amazon Web Services (AWS) verbinden. Weitere Informationen finden Sie im Handbuch unter [Zulassungsauflistung von IP-Adressen für die Verbindung mit Experience Platform auf Azure und AWS](../../ip-address-allow-list.md) .

### Bei Experience Platform auf Azure authentifizieren {#azure}

Geben Sie eine Verbindungszeichenfolge zur Authentifizierung und zum Verbinden Ihres [!DNL Oracle DB]-Kontos mit Experience Platform auf Azure an.

| Anmeldedaten | Beschreibung |
| --- | --- |
| Verbindungszeichenfolge | Eine Verbindungszeichenfolge ist eine Textzeichenfolge, die von Anwendungen zum Herstellen einer Verbindung mit einer Datenbank verwendet wird. Das [!DNL Oracle DB]-Verbindungszeichenfolgenmuster ist: `Host={HOST};Port={PORT};Sid={SID};User Id={USERNAME};Password={PASSWORD}`. |
| Verbindungsspezifikations-ID | Die Verbindungsspezifikations-ID gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Oracle] ist `d6b52d86-f0f8-475f-89d4-ce54c8527328`. **Hinweis**: Diese Berechtigung ist nur erforderlich, wenn eine Verbindung über die [!DNL Flow Service]-API hergestellt wird. |

### Authentifizierung bei Experience Platform auf Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Dieser Abschnitt gilt für Implementierungen von Experience Platform, die auf Amazon Web Services (AWS) ausgeführt werden. Experience Platform, das auf AWS ausgeführt wird, steht derzeit einer begrenzten Anzahl von Kunden zur Verfügung. Weitere Informationen zur unterstützten Experience Platform-Infrastruktur finden Sie in der Übersicht zur [Experience Platform Multi-Cloud](../../../landing/multi-cloud.md).

Geben Sie Werte für die folgenden Anmeldeinformationen an, um sich zu authentifizieren und Ihr [!DNL Oracle DB]-Konto mit Experience Platform auf AWS zu verbinden.

| Anmeldedaten | Beschreibung |
| --- | --- |
| Server | Die IP-Adresse oder der Hostname Ihres [!DNL Oracle DB]. |
| Port | Die Port-Nummer des Datenbank-Servers. Die Standard-Portnummer lautet `1521`. |
| Benutzername | Das für die Authentifizierung und den Zugriff auf die Datenbank verwendete [!DNL Oracle DB]-Benutzerkonto. |
| Passwort | Der Ihrem Benutzernamen zugeordnete geheime Schlüssel, der für die Authentifizierung verwendet wird. |
| Datenbank | Die spezifische [!DNL Oracle]-Datenbankinstanz, mit der Sie eine Verbindung herstellen möchten. |
| Schema | Der Container für Datenbankobjekte wie Tabellen, Ansichten oder Prozeduren. |
| SSL-Modus | Ein boolescher Wert, der steuert, ob SSL erzwungen wird oder nicht. Diese Konfiguration hängt von Ihrer Server-Unterstützung ab und standardmäßig von `false`. |
| Verbindungsspezifikations-ID | Die Verbindungsspezifikations-ID gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Oracle] ist `d6b52d86-f0f8-475f-89d4-ce54c8527328`. **Hinweis**: Diese Berechtigung ist nur erforderlich, wenn eine Verbindung über die [!DNL Flow Service]-API hergestellt wird. |


## Verbinden von [!DNL Oracle] mit [!DNL Experience Platform] mithilfe von APIs

- [Verbinden von Oracle DB mithilfe der Flow Service-API](../../tutorials/api/create/databases/oracle.md)
- [Erkunden von Datentabellen mithilfe der Flow Service-API](../../tutorials/api/explore/tabular.md)
- [Erstellen eines Datenflusses für eine Datenbankquelle mithilfe der Flow Service-API](../../tutorials/api/collect/database-nosql.md)

## Verbinden von [!DNL Oracle] mit [!DNL Experience Platform] über die Benutzeroberfläche

- [Verbinden von Oracle DB mithilfe des Arbeitsbereichs der Experience Platform-Benutzeroberfläche.](../../tutorials/ui/create/databases/oracle.md)
- [Erstellen eines Datenflusses für eine Datenbank-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/databases.md)
