---
keywords: Experience Platform;Fehlerbehebung;Leitlinien;Richtlinien;
title: Leitlinien für die Datenaufnahme
description: Dieses Dokument enthält Anleitungen zu Leitlinien für die Datenaufnahme in Adobe Experience Platform
exl-id: f07751cb-f9d3-49ab-bda6-8e6fec59c337
source-git-commit: 4fd26078017ae13e22ebb02f98335094c8e0581b
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 92%

---

# Leitlinien für die Datenaufnahme

Leitlinien sind Schwellenwerte, die Anhaltspunkte für die Daten- und Systemnutzung, die Leistungsoptimierung und die Vermeidung von Fehlern oder unerwarteten Ergebnissen in Adobe Experience Platform bieten. Leitlinien können sich auf Ihre Nutzung oder Verwendung von Daten und Verarbeitung im Zusammenhang mit Ihren Lizenzierungsberechtigungen beziehen.

Dieses Dokument enthält Anleitungen zu Leitlinien für die Datenaufnahme in Adobe Experience Platform.

## Leitlinien für die Batch-Aufnahme

In der folgenden Tabelle sind Leitlinien aufgeführt, die bei der Verwendung der [Batch-Aufnahme-API](./batch-ingestion/overview.md) oder von Quellen zu beachten sind:

| Art der Aufnahme | Leitlinien | Anmerkungen |
| --- | --- | --- |
| Data-Lake-Aufnahme mithilfe der Batch-Aufnahme-API | <ul><li>Mit der Batch-Aufnahme-API können Sie bis zu 20 GB Daten pro Stunde in den Data Lake aufnehmen.</li><li>Die maximale Anzahl von Dateien pro Batch beträgt 1.500.</li><li>Die maximale Batch-Größe beträgt 100 GB.</li><li>Die maximale Anzahl von Eigenschaften oder Feldern pro Zeile beträgt 10.000.</li><li>Die maximale Anzahl der Batches pro Minute und anwendender Person beträgt 138.</li></ul> |
| Data-Lake-Aufnahme mithilfe von Batch-Quellen | <ul><li>Sie können mit Batch-Aufnahme-Quellen wie [!DNL Azure Blob], [!DNL Amazon S3] und [!DNL SFTP] bis zu 200 GB Daten pro Stunde in den Data Lake aufnehmen.</li><li>Die Größe eines Batches sollte zwischen 256 MB und 100 GB liegen.</li><li>Die maximale Anzahl von Dateien pro Batch beträgt 1.500.</li></ul> | In der [Quellenübersicht](../sources/home.md) finden Sie einen Katalog der Quellen, die Sie für die Datenaufnahme verwenden können. |
| Batch-Aufnahme in Profil | <ul><li>Sie können bis zu 120 GB Daten pro Stunde aufnehmen.</li><li>Die maximale Größe einer Datensatzklasse beträgt 100 KB (Soft).</li><li>Die maximale Größe einer ExperienceEvent-Klasse beträgt 10 KB (Soft).</li><li>Die maximale Größe eines einzelnen Datensatzes beträgt 1 MB.</li></ul> |

## Leitlinien für die Streaming-Aufnahme

In der folgenden Tabelle sind Leitlinien aufgeführt, die bei der Verwendung der [Streaming-Aufnahme-API](./streaming-ingestion/overview.md) oder von Streaming-Quellen zu beachten sind:

| Art der Aufnahme | Leitlinien | Anmerkungen |
| --- | --- | --- |
| Streaming-Aufnahme | <ul><li>Die maximale Datensatzgröße beträgt 1 MB, wobei die empfohlene Größe bei 10 KB liegt.</li><li>Sie können 20.000 Anfragen pro Sekunde an das Profil in weniger als einer Minute verarbeiten.</li><li>Sie können bis zu 20.000 Anfragen pro Sekunde an den Data Lake in weniger als 15 Minuten verarbeiten.</li></ul> | Verwenden Sie die Batch-Aufnahme-API, wenn Sie einen höheren Datendurchsatz benötigen. |
| Streaming-Quellen | <ul><li>Die maximale Datensatzgröße beträgt 1 MB, wobei die empfohlene Größe bei 10 KB liegt.</li><li>Streaming-Quellen unterstützen bei Erstellung einer neuen Quellverbindung zwischen 4.000 und 5.000 Anfragen pro Sekunde. **Hinweis**: Es kann bis zu 30 Minuten dauern, bis Streaming-Daten vollständig in Data Lake verarbeitet werden.</li><li>Sie können zwischen 4.000 und 5.000 Anfragen pro Sekunde an den Data Lake verarbeiten. **Hinweis**: Es kann bis zu 30 Minuten dauern, bis Streaming-Daten vollständig in Data Lake verarbeitet werden.</li></ul> | Streaming-Quellen wie [!DNL Kafka], [!DNL Azure Event Hubs] und [!DNL Amazon Kinesis] verwenden nicht die Route des [!DNL Data Collection Core Service] (DCCS) und können unterschiedliche Durchsatzbeschränkungen aufweisen. In der [Quellenübersicht](../sources/home.md) finden Sie einen Katalog der Quellen, die Sie für die Datenaufnahme verwenden können. |

## Nächste Schritte

In der folgenden Dokumentation finden Sie weitere Informationen zu Leitlinien für Daten und Verarbeitung in Experience Platform:

* [Leitlinien für Echtzeit-Kundenprofil-Daten](../profile/guardrails.md)
* [Leitlinien für Identity Service-Daten](../identity-service/guardrails.md)
