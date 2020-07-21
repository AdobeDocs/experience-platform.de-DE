---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Übersicht über den Katalog-Service
topic: overview
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 43%

---


# [!DNL Catalog Service]Übersicht

[!DNL Catalog Service] ist ein Aufzeichnungssystem für Speicherort und Herkunft von Daten in Experience Platform. While all data that is ingested into [!DNL Experience Platform] is stored in the [!DNL Data Lake] as files and directories, [!DNL Catalog] holds the metadata and description of those files and directories for lookup and monitoring purposes.

Simply put, [!DNL Catalog] acts as a metadata store or &quot;[!UICONTROL catalog]&quot; where you can find information about your data within [!DNL Experience Platform]. You can use [!DNL Catalog] to answer the following questions:

* Wo befinden sich meine Daten?
* Auf welcher Stufe der Verarbeitung befinden sich diese Daten?
* Welche Systeme oder Prozesse haben Aktionen auf meine Daten ausgeführt?
* Wie viele Daten wurden erfolgreich verarbeitet?
* Welche Fehler sind bei der Verarbeitung aufgetreten?

[!DNL Catalog] stellt eine RESTful-API bereit, mit der Sie [!DNL Platform] Metadaten programmgesteuert mithilfe einfacher CRUD-Vorgänge verwalten können. Weitere Informationen finden Sie im [Katalog-Service-Entwicklerhandbuch](api/getting-started.md).

## [!DNL Catalog] und [!DNL Experience Platform] Dienstleistungen

Die [!DNL Catalog Service] nachverfolgten Ressourcen werden von mehreren [!DNL Experience Platform] Diensten verwendet. In order to make the most of [!DNL Catalog's] capabilities, it is recommended that you become familiar with these services and how they interact with [!DNL Catalog].

### [!DNL Experience Data Model] (XDM) System

[!DNL Experience Data Model] (XDM) System ist das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Platform] organisiert werden. [!DNL Experience Platform]XDM-Schemas dienen in zur konsistenten und wiederverwendbaren Beschreibung der Struktur von Daten.

When data is ingested into [!DNL Platform], the structure of that data is mapped to an XDM schema and stored within the [!DNL Data Lake] as part of a **dataset**. The metadata for each dataset is tracked by [!DNL Catalog Service], which includes a reference to the XDM schema that the dataset conforms to.

Informationen zum XDM-System im Allgemeinen finden Sie in der [Übersicht über das XDM-System](../xdm/home.md).

### [!DNL Data Ingestion]

[!DNL Experience Platform] erfasst Daten aus mehreren Quellen und speichert Datensätze als Datensätze innerhalb der [!DNL Data Lake]. [!DNL Catalog] verfolgt die Metadaten für diese Datensätze, unabhängig von ihrer Quelle oder Methode der Erfassung.

When using the batch ingestion method, [!DNL Catalog] also tracks additional metadata for **batch** files. Batches sind Dateneinheiten aus einer oder mehreren Dateien, die als Ganzes aufgenommen werden. [!DNL Catalog] verfolgt die Metadaten für diese Stapeldateien sowie die Datensätze, in denen sie nach der Erfassung beibehalten werden. Batch-Metadaten umfassen Informationen zur Anzahl der erfolgreich aufgenommenen Datensätze sowie zu fehlgeschlagenen Datensätzen und zugehörige Fehlermeldungen.

Weitere Informationen finden Sie in der [Übersicht über die Datenaufnahme](../ingestion/home.md).

## [!DNL Catalog] Objekte

As outlined in the previous section, [!DNL Catalog] tracks metadata for several kinds of resources and operations that are used by other [!DNL Platform] services. [!DNL Catalog] verwaltet einen eigenen Speicher von &quot;Objekten&quot;, die diese Metadaten kapseln. [!DNL Catalog] Objekte sind abfragliche Darstellungen von [!DNL Platform] Daten, mit denen Sie Ihre Daten suchen, überwachen und beschriften können, ohne selbst auf die Daten zugreifen zu müssen.

The following table outlines the different object types supported by [!DNL Catalog]:

| Objekt | API-Endpunkt | Definition |
|---|---|---|
| Konto | `/accounts` | Beim Erstellen von Quellverbindungen müssen Authentifizierungsberechtigungen angegeben werden. Ein Konto ist eine Sammlung von Anmeldeinformationen, die zur Authentifizierung für das Herstellen einer Verbindung bestimmten Typs verwendet wurden. Each connection has a set of unique parameters that are persisted by [!DNL Catalog] and secured in an [!DNL Azure Key Vault]. |
| Batch | `/batches` | Batches sind Dateneinheiten aus einer oder mehreren Dateien, die als Ganzes aufgenommen werden. A batch object in [!DNL Catalog] outlines the batch&#39;s ingestion metrics (such as the number of records processed or size on disk) and may also include links to datasets, views, and other resources that were affected by the batch operation. |
| Verbindung | `/connections` | Eine Verbindung ist eine einzelne Instanz eines Quell-Connectors, die für Ihr Unternehmen eindeutig ist und unter Verwendung der entsprechenden Anmeldeinformationen zur Authentifizierung für den Connector-Typ konfiguriert wurde. |
| Connector | `/connectors` | Connectors define how source connections are to gather data from other Adobe applications (such as Adobe Analytics and Adobe Audience Manager), third-party cloud storage sources (such as [!DNL Azure Blob], [!DNL Amazon S3], FTP servers, and SFTP servers), and third-party CRM systems (such as [!DNL Microsoft Dynamics] and [!DNL Salesforce]). |
| Datensatz | `/dataSets` | Ein Datensatz ist ein Konstrukt zur Datenspeicherung und -verwaltung, in dem Daten (in der Regel) in einer Tabelle erfasst werden, die ein Schema (Spalten) und Felder (Zeilen) beinhaltet. See the [datasets overview](./datasets/overview.md) for more information. |
| Datensatzdatei | `/datasetFiles` | Dataset files represent blocks of data that has been saved on [!DNL Platform]. Sie stellen Aufzeichnungen von Literaldateien und liefern als solches Informationen zur Dateigröße, zur Anzahl der darin enthaltenen Datensätze und einen Verweis auf den Batch, in dem die Datei aufgenommen wurde. |

## Nächste Schritte

This document provided an introduction to [!DNL Catalog Service] and how it functions within the greater scope of [!DNL Experience Platform]. Die einzelnen Schritte für die Interaktion mit den verschiedenen Endpunkten der zugehörigen Service API finden Sie im [Katalog-Service-Entwicklerhandbuch](api/getting-started.md). [!DNL Catalog] Es wird empfohlen, auch das Handbuch zum Thema [Filtern von Katalogdaten](api/filter-data.md) durchzugehen, da darin Best Practices für die Beschränkung der in API-Antworten zurückgegebenen Daten erläutert werden.