---
title: Adobe Experience Platform – Versionshinweise, September 2021
description: Versionshinweise September 2021 zu Adobe Experience Platform.
exl-id: 96375409-803f-45af-805e-900207d972e4
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 95%

---

# Adobe Experience Platform – Versionshinweise

**Release-Datum: 29. September 2021**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Datenaufnahme](#ingestion)
- [[!DNL Data Prep]](#data-prep)
- [Quellen](#sources)

## Datenaufnahme {#ingestion}

Datenerfassung in Adobe Experience Platform stellt die verschiedenen Methoden dar, mit denen Platform Daten aus den Quellen aufnimmt, sowie die Art und Weise, wie die Daten im Data Lake zur Verwendung durch nachgelagerte Platform-Services persistiert werden.

**Neue Funktionen**

| Funktion | Beschreibung |
|------- | -----------|
| Aktualisieren oder Patchen von Profildatensätzen mithilfe der Batch-Aufnahme | Das Echtzeit-Kundenprofil ermöglicht nun über die Batch-Erfassung Aktualisierungen an Profilattributen in individuellen Profildatensatzdaten. Weitere Informationen finden Sie im [Entwicklerhandbuch zur Batch-Aufnahme](../../ingestion/batch-ingestion/api-overview.md). |

Weitere Informationen zur Erfassung von Daten in Platform finden Sie in der [Datenerfassungsdokumentation](../../ingestion/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] ermöglicht es Dateningenieuren, Daten mit dem Experience-Datenmodell (XDM) zu mappen sowie sie umzuformen und zu validieren.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für Streaming-Datenflüsse | Sie können jetzt Datenvorbereitungsfunktionen beim Erstellen eines Streaming-Datenflusses für [!DNL Amazon Kinesis], [!DNL Azure Event Hubs] und [!DNL Google PubSub] verwenden. Weitere Informationen finden Sie im Tutorial zum [Erstellen eines Streaming-Datenflusses für Cloud-Speicherquellen](../../sources/tutorials/ui/dataflow/streaming/cloud-storage-streaming.md). |

Weitere Informationen zu [!DNL Data Prep] finden Sie in der [[!DNL Data Prep] Übersicht](../../data-prep/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

| Funktion | Beschreibung |
| --- | --- |
| [!DNL Data Landing Zone] | Sie können jetzt eine [!DNL Data Landing Zone]-Quellverbindung mithilfe der [[!DNL Flow Service] API](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) oder der [Benutzeroberfläche](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md) erstellen. [!DNL Data Landing Zone] ist eine von Platform bereitgestellte [!DNL Azure Blob]-Speicherschnittstelle, über die Sie auf eine sichere, Cloud-basierte Dateispeichereinrichtung zugreifen können, um Dateien in Platform zu laden. Weitere Informationen finden Sie in der [[!DNL Data Landing Zone] Übersicht über](../../sources/connectors/cloud-storage/data-landing-zone.md). |
| [!DNL Snowflake] | Sie können jetzt eine [!DNL Snowflake]-Quellverbindung mithilfe der [[!DNL Flow Service] API](../../sources/tutorials/api/create/databases/snowflake.md) oder der [Benutzeroberfläche](../../sources/tutorials/ui/create/databases/snowflake.md) erstellen, um Daten aus Ihrer [!DNL Snowflake]-Datenbank in Platform zu übertragen. Weitere Informationen finden Sie in der [[!DNL Snowflake] Übersicht über](../../sources/connectors/databases/snowflake.md). |
| [!DNL SFTP]-Quellverbesserungen | Sie können beim Erstellen einer [!DNL SFTP]-Quellverbindung manuell eine benutzerdefinierte Port-Nummer festlegen. Weitere Informationen finden Sie in der [[!DNL SFTP] Übersicht über](../../sources/connectors/cloud-storage/sftp.md). |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
