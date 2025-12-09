---
title: Aktivieren der Änderungsdatenerfassung für Quellverbindungen in der API
description: Erfahren Sie, wie Sie die Änderungsdatenerfassung für Quellverbindungen in der API aktivieren
exl-id: 362f3811-7d1e-4f16-b45f-ce04f03798aa
source-git-commit: 491588dab1388755176b5e00f9d8ae3e49b7f856
workflow-type: tm+mt
source-wordcount: '1234'
ht-degree: 0%

---

# Aktivieren der Änderungsdatenerfassung für Quellverbindungen in der API

Verwenden Sie die Änderungsdatenerfassung in Adobe Experience Platform-Quellen, um Ihre Quell- und Zielsysteme nahezu in Echtzeit synchronisiert zu halten.

Experience Platform unterstützt derzeit **inkrementelle Datenkopie** mit der regelmäßig neu erstellte oder aktualisierte Datensätze aus dem Quellsystem an die aufgenommenen Datensätze übertragen werden. Bei dieser Methode werden Änderungen mithilfe einer **Zeitstempelspalte** verfolgt, es werden jedoch keine Löschungen erkannt, was im Laufe der Zeit zu Dateninkonsistenzen führen kann.

Im Gegensatz dazu erfasst und wendet Change Data Capture Einfügungen, Aktualisierungen und Löschungen nahezu in Echtzeit an. Diese umfassende Änderungsverfolgung stellt sicher, dass Datensätze vollständig mit dem Quellsystem abgestimmt bleiben, und bietet einen vollständigen Änderungsverlauf, der über die Unterstützung inkrementeller Kopien hinausgeht. Löschvorgänge müssen jedoch besonders berücksichtigt werden, da sie sich auf alle Anwendungen auswirken, die die Zieldatensätze verwenden.

Für das Ändern der Datenerfassung in Experience Platform ist **[Data Mirror](../../../xdm/data-mirror/overview.md)** mit [relationalen Schemata](../../../xdm/schema/relational.md) erforderlich. Sie können Änderungsdaten auf zwei Arten für Data Mirror bereitstellen:

* **[Manuelles Änderungs-Tracking](#file-based-sources)**: Fügen Sie eine `_change_request_type` Spalte in Ihren Datensatz für Quellen ein, die nativ keine Änderungsdatensätze generieren
* **[Exporte der nativen Änderungsdatenerfassung](#database-sources)**: Verwenden Sie Änderungsdatenerfassungsdatensätze, die direkt aus Ihrem Quellsystem exportiert wurden

Bei beiden Ansätzen ist Data Mirror mit relationalen Schemata erforderlich, um Beziehungen beizubehalten und Eindeutigkeit zu erzwingen.

## Data Mirror mit relationalen Schemata

>[!AVAILABILITY]
>
>Data Mirror und relationale Schemata stehen Adobe Journey Optimizer-Lizenzinhabern **Orchestrierte Kampagnen** zur Verfügung. Sie sind auch als **eingeschränkte Version** für Customer Journey Analytics-Benutzer verfügbar, je nach Ihrer Lizenz und der Aktivierung von Funktionen. Wenden Sie sich an den Adobe-Support, um Zugang zu erhalten.

>[!NOTE]
>
>**Benutzende mit orchestrierten Kampagnen**: Verwenden Sie die in diesem Dokument beschriebenen Data Mirror-Funktionen, um mit Kundendaten zu arbeiten, die die referenzielle Integrität wahren. Auch wenn Ihre Quelle die Datenerfassungsformatierung für Änderungen nicht verwendet, unterstützt Data Mirror relationale Funktionen wie die Durchsetzung von Primärschlüsseln, Upserts auf Datensatzebene und Schemabeziehungen. Diese Funktionen gewährleisten eine konsistente und zuverlässige Datenmodellierung über verbundene Datensätze hinweg.

Data Mirror verwendet relationale Schemata, um die Änderungsdatenerfassung zu erweitern und erweiterte Datenbanksynchronisierungsfunktionen zu ermöglichen. Einen Überblick über Data Mirror finden Sie unter [Übersicht über Data Mirror](../../../xdm/data-mirror/overview.md).

Relationale Schemata erweitern Experience Platform, um die Eindeutigkeit von Primärschlüsseln zu erzwingen, Änderungen auf Zeilenebene zu verfolgen und Beziehungen auf Schemaebene zu definieren. Bei der Datenerfassung für Änderungen wenden sie Einfügungen, Aktualisierungen und Löschungen direkt im Data Lake an, wodurch die Notwendigkeit von Extract, Transform, Load (ETL) oder manueller Abstimmung reduziert wird.

Weitere [&#x200B; finden Sie unter &#x200B;](../../../xdm/schema/relational.md) zu relationalen Schemata .

### Anforderungen an relationale Schemata zur Änderungsdatenerfassung

Bevor Sie ein relationales Schema mit Änderungsdatenerfassung verwenden, konfigurieren Sie die folgenden Kennungen:

* Jeden Datensatz mit einem Primärschlüssel eindeutig identifizieren.
* Wenden Sie Aktualisierungen nacheinander mithilfe einer Versionskennung an.
* Fügen Sie für Zeitreihenschemas eine Zeitstempelkennung hinzu.

### Umgang mit Kontrollspalten {#control-column-handling}

Verwenden Sie die Spalte `_change_request_type` , um anzugeben, wie jede Zeile verarbeitet werden soll:

* `u` — upsert (Standard, wenn die Spalte fehlt)
* `d` — Löschen

Diese Spalte wird nur während der Aufnahme ausgewertet und nicht gespeichert oder XDM-Feldern zugeordnet.

### Workflow {#workflow}

So aktivieren Sie die Änderungsdatenerfassung mit einem relationalen Schema:

1. Erstellen Sie ein relationales Schema.
2. Fügen Sie die erforderlichen Deskriptoren hinzu:
   * [Primärer Schlüsseldeskriptor](../../../xdm/api/descriptors.md#primary-key-descriptor)
   * [Versionsdeskriptor](../../../xdm/api/descriptors.md#version-descriptor)
   * [Zeitstempeldeskriptor](../../../xdm/api/descriptors.md#timestamp-descriptor) (nur Zeitreihen)
3. Erstellen Sie einen Datensatz aus dem Schema und aktivieren Sie die Änderungsdatenerfassung.
4. Nur für die dateibasierte Aufnahme: Fügen Sie die Spalte `_change_request_type` zu Ihren Quelldateien hinzu, wenn Sie Löschvorgänge explizit angeben müssen. CDC-Exportkonfigurationen behandeln dies automatisch für Datenbankquellen.
5. Schließen Sie die Einrichtung der Quellverbindung ab, um die Aufnahme zu aktivieren.

>[!NOTE]
>
>Die Spalte `_change_request_type` ist nur für dateibasierte Quellen (Amazon S3, Azure Blob, Google Cloud Storage, SFTP) erforderlich, wenn Sie das Änderungsverhalten auf Zeilenebene explizit steuern möchten. Bei Datenbankquellen mit nativen CDC-Funktionen werden Änderungsvorgänge automatisch über CDC-Exportkonfigurationen verarbeitet. Die dateibasierte Aufnahme setzt standardmäßig Upsert-Vorgänge voraus. Sie müssen diese Spalte nur hinzufügen, wenn Sie Löschvorgänge in Ihren Datei-Uploads angeben möchten.

>[!IMPORTANT]
>
>**Planung des Löschens von Daten ist erforderlich**. Alle Programme, die relationale Schemata verwenden, müssen die Auswirkungen von Löschungen verstehen, bevor sie die Änderungsdatenerfassung implementieren. Planen Sie, wie sich Löschungen auf zugehörige Datensätze, Compliance-Anforderungen und nachgelagerte Prozesse auswirken. Siehe [Überlegungen zur Datenhygiene](../../../hygiene/ui/record-delete.md#relational-record-delete) für Anleitungen.

## Bereitstellung von Änderungsdaten für dateibasierte Quellen {#file-based-sources}

>[!IMPORTANT]
>
>Die dateibasierte Änderungsdatenerfassung erfordert Data Mirror mit relationalen Schemata. Bevor Sie die folgenden Dateiformatierungsschritte ausführen, stellen Sie sicher, dass Sie den Data Mirror-Setup-Workflow [&#128279;](#workflow) abgeschlossen haben, der zuvor in diesem Dokument beschrieben wurde. In den folgenden Schritten wird beschrieben, wie Sie Ihre Datendateien formatieren, um Änderungsnachverfolgungsinformationen einzuschließen, die von Data Mirror verarbeitet werden.

Fügen Sie bei dateibasierten Quellen ([!DNL Amazon S3], [!DNL Azure Blob], [!DNL Google Cloud Storage] und [!DNL SFTP]) eine `_change_request_type` Spalte in Ihre Dateien ein.

Verwenden Sie die `_change_request_type` Werte, die im Abschnitt [Umgang mit Kontrollspalten](#control-column-handling) oben definiert wurden.

>[!IMPORTANT]
>
>Für **nur dateibasierte Quellen** benötigen bestimmte Anwendungen möglicherweise eine `_change_request_type` Spalte mit entweder `u` (upsert) oder `d` (delete), um die Funktionen zum Nachverfolgen von Änderungen zu validieren. Die Adobe Journey Optimizer-Funktion **Orchestrierte Kampagnen** erfordert diese Spalte beispielsweise, um den Umschalter „Orchestrierte Kampagnen“ zu aktivieren und die Datensatzauswahl für die Zielgruppenbestimmung zuzulassen. Anwendungsspezifische Validierungsanforderungen können variieren.

Führen Sie die folgenden quellspezifischen Schritte aus.

### Cloud-Speicherquellen {#cloud-storage-sources}

Aktivieren Sie die Änderungsdatenerfassung für Cloud-Speicherquellen, indem Sie die folgenden Schritte ausführen:

1. Erstellen Sie eine Basisverbindung für Ihre Quelle:

   | Quelle | Basisverbindungshandbuch |
   |---|---|
   | [!DNL Amazon S3] | [Erstellen einer  [!DNL Amazon S3] -Basisverbindung](../api/create/cloud-storage/s3.md) |
   | [!DNL Azure Blob] | [Erstellen einer  [!DNL Azure Blob] -Basisverbindung](../api/create/cloud-storage/blob.md) |
   | [!DNL Google Cloud Storage] | [Erstellen einer  [!DNL Google Cloud Storage] -Basisverbindung](../api/create/cloud-storage/google.md) |
   | [!DNL SFTP] | [Erstellen einer  [!DNL SFTP] -Basisverbindung](../api/create/cloud-storage/sftp.md) |

2. [Erstellen einer Quellverbindung für einen Cloud-Speicher](../api/collect/cloud-storage.md#create-a-source-connection).

Alle Cloud-Speicherquellen verwenden dasselbe `_change_request_type` Spaltenformat, das im Abschnitt [Dateibasierte Quellen](#file-based-sources) oben beschrieben wird.

## Datenbankquellen {#database-sources}

### [!DNL Azure Databricks]

Um die Änderungsdatenerfassung mit [!DNL Azure Databricks] zu verwenden, müssen Sie sowohl **Datenfeed ändern** in Ihren Quelltabellen aktivieren als auch Data Mirror mit relationalen Schemata in Experience Platform konfigurieren.

Verwenden Sie die folgenden Befehle, um den Änderungsdaten-Feed in Ihren Tabellen zu aktivieren:

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

### [!DNL Data Landing Zone]

Um die Änderungsdatenerfassung mit [!DNL Data Landing Zone] zu verwenden, müssen Sie sowohl **Datenfeed ändern** in Ihren Quelltabellen aktivieren als auch Data Mirror mit relationalen Schemata in Experience Platform konfigurieren.

Lesen Sie die folgende Dokumentation, um zu erfahren, wie Sie die Änderungsdatenerfassung für Ihre [!DNL Data Landing Zone]-Quellverbindung aktivieren:

* [Erstellen  [!DNL Data Landing Zone]  Basisverbindung](../api/create/cloud-storage/data-landing-zone.md).
* [Erstellen einer Quellverbindung für einen Cloud-Speicher](../api/collect/cloud-storage.md#create-a-source-connection).

### [!DNL Google BigQuery]

Um die Änderungsdatenerfassung mit [!DNL Google BigQuery] verwenden zu können, müssen Sie sowohl den Änderungsverlauf in Ihren Quelltabellen aktivieren als auch Data Mirror mit relationalen Schemata in Experience Platform konfigurieren.

Um den Änderungsverlauf in Ihrer [!DNL Google BigQuery]-Quellverbindung zu aktivieren, navigieren Sie in der [!DNL Google BigQuery]-Konsole zu Ihrer [!DNL Google Cloud]-Seite und setzen `enable_change_history` auf `TRUE`. Diese Eigenschaft aktiviert den Änderungsverlauf für Ihre Datentabelle.

Weitere Informationen finden Sie im Handbuch zu [Datendefinitionssprachanweisungen in [!DNL GoogleSQL]](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#table_option_list).

Lesen Sie die folgende Dokumentation, um zu erfahren, wie Sie die Änderungsdatenerfassung für Ihre [!DNL Google BigQuery]-Quellverbindung aktivieren:

* [Erstellen  [!DNL Google BigQuery]  Basisverbindung](../api/create/databases/bigquery.md).
* [Erstellen einer Quellverbindung für eine Datenbank](../api/collect/database-nosql.md#create-a-source-connection).

### [!DNL Snowflake]

Um die Änderungsdatenerfassung mit [!DNL Snowflake] verwenden zu können, müssen Sie sowohl **Änderungsverfolgung“** Ihren Quelltabellen aktivieren als auch Data Mirror mit relationalen Schemata in Experience Platform konfigurieren.

Aktivieren Sie [!DNL Snowflake] die Änderungsverfolgung mithilfe der `ALTER TABLE` und legen Sie `CHANGE_TRACKING` auf `TRUE` fest.

```sql
ALTER TABLE mytable SET CHANGE_TRACKING = TRUE
```

Weitere Informationen finden Sie im [[!DNL Snowflake] Handbuch zur Verwendung der changes-Klausel](https://docs.snowflake.com/en/sql-reference/constructs/changes#usage-notes).

Lesen Sie die folgende Dokumentation, um zu erfahren, wie Sie die Änderungsdatenerfassung für Ihre [!DNL Snowflake]-Quellverbindung aktivieren:

* [Erstellen  [!DNL Snowflake]  Basisverbindung](../api/create/databases/snowflake.md).
* [Erstellen einer Quellverbindung für eine Datenbank](../api/collect/database-nosql.md#create-a-source-connection).
