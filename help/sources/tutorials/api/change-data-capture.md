---
title: Aktivieren der Änderungsdatenerfassung für Quellverbindungen in der API
description: Erfahren Sie, wie Sie die Änderungsdatenerfassung für Quellverbindungen in der API aktivieren
source-git-commit: d8b4557424e1f29dfdd8893932aef914226dd60d
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 0%

---

# Aktivieren der Änderungsdatenerfassung für Quellverbindungen in der API

Die Funktion „Datenerfassung in Adobe Experience Platform ändern“ kann verwendet werden, um die Echtzeit-Datensynchronisation zwischen Ihren Quell- und Zielsystemen aufrechtzuerhalten.

Derzeit unterstützt Experience Platform **inkrementelle Datenkopie** wodurch sichergestellt wird, dass neu erstellte oder aktualisierte Datensätze im Quellsystem regelmäßig in die aufgenommenen Datensätze kopiert werden. Dieser Prozess beruht auf der Verwendung der **Zeitstempelspalte**, z. B. `LastModified`, um Änderungen zu verfolgen und zu erfassen **nur die neu eingefügten oder aktualisierten Daten**. Diese Methode berücksichtigt jedoch keine gelöschten Datensätze, was im Laufe der Zeit zu Dateninkonsistenzen führen kann.

Bei der Erfassung von Änderungsdaten erfasst und wendet ein gegebener Fluss alle Änderungen an, einschließlich Einfügungen, Aktualisierungen und Löschungen. Ebenso bleiben Experience Platform-Datensätze vollständig mit dem Quellsystem synchronisiert.

Sie können die Änderungsdatenerfassung für die folgenden Quellen verwenden:

## [!DNL Amazon S3]

Stellen Sie sicher, dass `_change_request_type` in der [!DNL Amazon S3] vorhanden ist, die Sie in Experience Platform aufnehmen möchten. Darüber hinaus müssen Sie sicherstellen, dass die folgenden gültigen Werte in der Datei enthalten sind:

* `u`: für Einfügungen und Aktualisierungen
* `d`: für Löschvorgänge.

Wenn `_change_request_type` nicht in der Datei vorhanden ist, wird der Standardwert `u` verwendet.

Lesen Sie die folgende Dokumentation, um zu erfahren, wie Sie die Änderungsdatenerfassung für Ihre [!DNL Amazon S3]-Quellverbindung aktivieren:

* [Erstellen  [!DNL Amazon S3]  Basisverbindung](../api/create/cloud-storage/s3.md).
* [Erstellen einer Quellverbindung für einen Cloud-Speicher](../api/collect/cloud-storage.md#create-a-source-connection).

## [!DNL Azure Blob]

Stellen Sie sicher, dass `_change_request_type` in der [!DNL Azure Blob] vorhanden ist, die Sie in Experience Platform aufnehmen möchten. Darüber hinaus müssen Sie sicherstellen, dass die folgenden gültigen Werte in der Datei enthalten sind:

* `u`: für Einfügungen und Aktualisierungen
* `d`: für Löschvorgänge.

Wenn `_change_request_type` nicht in der Datei vorhanden ist, wird der Standardwert `u` verwendet.

Lesen Sie die folgende Dokumentation, um zu erfahren, wie Sie die Änderungsdatenerfassung für Ihre [!DNL Azure Blob]-Quellverbindung aktivieren:

* [Erstellen  [!DNL Azure Blob]  Basisverbindung](../api/create/cloud-storage/blob.md).
* [Erstellen einer Quellverbindung für einen Cloud-Speicher](../api/collect/cloud-storage.md#create-a-source-connection).

## [!DNL Azure Databricks]

Sie müssen **Daten-Feed ändern** in Ihrer [!DNL Azure Databricks] aktivieren, um die Änderungsdatenerfassung in Ihrer Quellverbindung verwenden zu können.

Verwenden Sie die folgenden Befehle, um die Option Daten-Feed ändern in [!DNL Azure Databricks] explizit zu aktivieren

**Neue Tabelle**

Um den Änderungsdaten-Feed auf eine neue Tabelle anzuwenden, müssen Sie die Tabelleneigenschaft `delta.enableChangeDataFeed` im `TRUE`-Befehl auf `CREATE TABLE` setzen.

```sql
CREATE TABLE student (id INT, name STRING, age INT) TBLPROPERTIES (delta.enableChangeDataFeed = true)
```

**Vorhandene Tabelle**

Um den Änderungsdaten-Feed auf eine vorhandene Tabelle anzuwenden, müssen Sie die Tabelleneigenschaft `delta.enableChangeDataFeed` im `TRUE`-Befehl auf `ALTER TABLE` setzen.

```sql
ALTER TABLE myDeltaTable SET TBLPROPERTIES (delta.enableChangeDataFeed = true)
```

**Alle neuen Tabellen**

Um den Änderungsdaten-Feed auf alle neuen Tabellen anzuwenden, müssen Sie Ihre Standardeigenschaften auf `TRUE` festlegen.

```sql
set spark.databricks.delta.properties.defaults.enableChangeDataFeed = true;
```

Weitere Informationen finden Sie im [[!DNL Azure Databricks] Handbuch zum Aktivieren des Änderungsdaten-Feeds](https://docs.databricks.com/aws/en/delta/delta-change-data-feed#enable-change-data-feed).

Lesen Sie die folgende Dokumentation, um zu erfahren, wie Sie die Änderungsdatenerfassung für Ihre [!DNL Azure Databricks]-Quellverbindung aktivieren:

* [Erstellen  [!DNL Azure Databricks]  Basisverbindung](../api/create/databases/databricks.md).
* [Erstellen einer Quellverbindung für eine Datenbank](../api/collect/database-nosql.md#create-a-source-connection).

## [!DNL Data Landing Zone]

Sie müssen **Daten-Feed ändern** in Ihrer [!DNL Data Landing Zone] aktivieren, um die Änderungsdatenerfassung in Ihrer Quellverbindung verwenden zu können.

Verwenden Sie die folgenden Befehle, um die Option Daten-Feed ändern in [!DNL Data Landing Zone] explizit zu aktivieren.

Lesen Sie die folgende Dokumentation, um zu erfahren, wie Sie die Änderungsdatenerfassung für Ihre [!DNL Data Landing Zone]-Quellverbindung aktivieren:

* [Erstellen  [!DNL Data Landing Zone]  Basisverbindung](../api/create/cloud-storage/data-landing-zone.md).
* [Erstellen einer Quellverbindung für einen Cloud-Speicher](../api/collect/cloud-storage.md#create-a-source-connection).

## [!DNL Google BigQuery]

So verwenden Sie die Änderungsdatenerfassung in Ihrer [!DNL Google BigQuery]. Navigieren Sie in der [!DNL Google BigQuery]-Konsole zu Ihrer [!DNL Google Cloud] und legen Sie `enable_change_history` auf `TRUE` fest. Diese Eigenschaft aktiviert den Änderungsverlauf für Ihre Datentabelle.

Weitere Informationen finden Sie im Handbuch zu [Datendefinitionssprachanweisungen in [!DNL GoogleSQL]](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#table_option_list).

Lesen Sie die folgende Dokumentation, um zu erfahren, wie Sie die Änderungsdatenerfassung für Ihre [!DNL Google BigQuery]-Quellverbindung aktivieren:

* [Erstellen  [!DNL Google BigQuery]  Basisverbindung](../api/create/databases/bigquery.md).
* [Erstellen einer Quellverbindung für eine Datenbank](../api/collect/database-nosql.md#create-a-source-connection).

## [!DNL Google Cloud Storage]

Stellen Sie sicher, dass `_change_request_type` in der [!DNL Google Cloud Storage] vorhanden ist, die Sie in Experience Platform aufnehmen möchten. Darüber hinaus müssen Sie sicherstellen, dass die folgenden gültigen Werte in der Datei enthalten sind:

* `u`: für Einfügungen und Aktualisierungen
* `d`: für Löschvorgänge.

Wenn `_change_request_type` nicht in der Datei vorhanden ist, wird der Standardwert `u` verwendet.

Lesen Sie die folgende Dokumentation, um zu erfahren, wie Sie die Änderungsdatenerfassung für Ihre [!DNL Google Cloud Storage]-Quellverbindung aktivieren:

* [Erstellen  [!DNL Google Cloud Storage]  Basisverbindung](../api/create/cloud-storage/google.md).
* [Erstellen einer Quellverbindung für einen Cloud-Speicher](../api/collect/cloud-storage.md#create-a-source-connection).


## [!DNL SFTP]

Stellen Sie sicher, dass `_change_request_type` in der [!DNL SFTP] vorhanden ist, die Sie in Experience Platform aufnehmen möchten. Darüber hinaus müssen Sie sicherstellen, dass die folgenden gültigen Werte in der Datei enthalten sind:

* `u`: für Einfügungen und Aktualisierungen
* `d`: für Löschvorgänge.

Wenn `_change_request_type` nicht in der Datei vorhanden ist, wird der Standardwert `u` verwendet.

Lesen Sie die folgende Dokumentation, um zu erfahren, wie Sie die Änderungsdatenerfassung für Ihre [!DNL SFTP]-Quellverbindung aktivieren:

* [Erstellen  [!DNL SFTP]  Basisverbindung](../api/create/cloud-storage/sftp.md).
* [Erstellen einer Quellverbindung für einen Cloud-Speicher](../api/collect/cloud-storage.md#create-a-source-connection).


## [!DNL Snowflake]

Sie müssen **Änderungs-Tracking** in Ihren [!DNL Snowflake]-Tabellen aktivieren, um die Änderungsdatenerfassung in Ihren Quellverbindungen verwenden zu können.

Aktivieren Sie [!DNL Snowflake] die Änderungsverfolgung mithilfe der `ALTER TABLE` und legen Sie `CHANGE_TRACKING` auf `TRUE` fest.

```sql
ALTER TABLE mytable SET CHANGE_TRACKING = TRUE
```

Weitere Informationen finden Sie im [[!DNL Snowflake] Handbuch zur Verwendung der changes-Klausel](https://docs.snowflake.com/en/sql-reference/constructs/changes#usage-notes).

Lesen Sie die folgende Dokumentation, um zu erfahren, wie Sie die Änderungsdatenerfassung für Ihre [!DNL Snowflake]-Quellverbindung aktivieren:

* [Erstellen  [!DNL Snowflake]  Basisverbindung](../api/create/databases/snowflake.md).
* [Erstellen einer Quellverbindung für eine Datenbank](../api/collect/database-nosql.md#create-a-source-connection).

