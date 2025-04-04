---
title: Adobe Experience Platform – Versionshinweise, September 2021
description: Versionshinweise September 2021 zu Adobe Experience Platform.
exl-id: 96375409-803f-45af-805e-900207d972e4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 64%

---

# Adobe Experience Platform – Versionshinweise

**Release-Datum: 29. September 2021**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Datenaufnahme](#ingestion)
- [[!DNL Data Prep]](#data-prep)
- [Quellen](#sources)

## Datenaufnahme {#ingestion}

Die Datenaufnahme in Adobe Experience Platform stellt die verschiedenen Methoden dar, mit denen Experience Platform Daten aus verschiedenen Quellen aufnimmt, sowie die Art und Weise, wie diese Daten im Data Lake zur Verwendung durch nachgelagerte Experience Platform-Services persistiert werden.

**Neue Funktionen**

| Funktion | Beschreibung |
|------- | -----------|
| Aktualisieren oder Patchen von Profildatensätzen mithilfe der Batch-Aufnahme | Das Echtzeit-Kundenprofil ermöglicht jetzt über die Batch-Aufnahme Aktualisierungen an Profilattributen in individuellen Profildatensatzdaten. Weitere Informationen finden Sie im [Entwicklerhandbuch zur Batch-Aufnahme](../../ingestion/batch-ingestion/api-overview.md). |

Weitere Informationen zur Aufnahme von Daten in Experience Platform finden Sie in der [Datenerfassungsdokumentation](../../ingestion/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] ermöglicht es Dateningenieuren, Daten mit dem Experience-Datenmodell (XDM) zu mappen sowie sie umzuformen und zu validieren.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für Streaming-Datenflüsse | Sie können jetzt Datenvorbereitungsfunktionen beim Erstellen eines Streaming-Datenflusses für [!DNL Amazon Kinesis], [!DNL Azure Event Hubs] und [!DNL Google PubSub] verwenden. Weitere Informationen finden Sie im Tutorial zum [Erstellen eines Streaming-Datenflusses für Cloud-Speicherquellen](../../sources/tutorials/ui/dataflow/streaming/cloud-storage-streaming.md). |

Weitere Informationen zu [!DNL Data Prep] finden Sie in der [[!DNL Data Prep] Übersicht](../../data-prep/home.md).

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen aufnehmen und ermöglicht es Ihnen gleichzeitig, diese Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

| Funktion | Beschreibung |
| --- | --- |
| [!DNL Data Landing Zone] | Sie können jetzt eine [!DNL Data Landing Zone]-Quellverbindung mithilfe der [[!DNL Flow Service] API](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) oder der [Benutzeroberfläche](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md) erstellen. [!DNL Data Landing Zone] ist eine von Experience Platform bereitgestellte [!DNL Azure Blob]-Speicherschnittstelle, über die Sie auf eine sichere, Cloud-basierte Dateispeichereinrichtung zugreifen können, um Dateien in Experience Platform zu laden. Weitere Informationen finden Sie in der [[!DNL Data Landing Zone] Übersicht](../../sources/connectors/cloud-storage/data-landing-zone.md). |
| [!DNL Snowflake] | Sie können jetzt eine [!DNL Snowflake]-Quellverbindung mithilfe der [[!DNL Flow Service] API](../../sources/tutorials/api/create/databases/snowflake.md) oder der [Benutzeroberfläche) ](../../sources/tutorials/ui/create/databases/snowflake.md), um Daten aus Ihrer [!DNL Snowflake] in Experience Platform zu übertragen. Weitere Informationen finden Sie in der [[!DNL Snowflake] Übersicht über](../../sources/connectors/databases/snowflake.md). |
| [!DNL SFTP]-Quellverbesserungen | Sie können beim Erstellen einer [!DNL SFTP]-Quellverbindung manuell eine benutzerdefinierte Port-Nummer festlegen. Weitere Informationen finden Sie in der [[!DNL SFTP] Übersicht über](../../sources/connectors/cloud-storage/sftp.md). |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
