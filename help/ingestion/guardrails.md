---
keywords: Experience Platform; Fehlerbehebung; Limits; Richtlinien;
title: Limits für die Datenerfassung
description: Dieses Dokument enthält Anleitungen zu Limits für die Datenerfassung in Adobe Experience Platform
exl-id: f07751cb-f9d3-49ab-bda6-8e6fec59c337
source-git-commit: 4fd26078017ae13e22ebb02f98335094c8e0581b
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---

# Limits für die Datenerfassung

Limits sind Schwellenwerte, die die Datennutzung und Systemnutzung, Leistungsoptimierung und Vermeidung von Fehlern oder unerwarteten Ergebnissen in Adobe Experience Platform unterstützen. Limits können sich auf Ihre Nutzung oder Nutzung von Daten und Verarbeitung im Zusammenhang mit Ihren Lizenzberechtigungen beziehen.

Dieses Dokument enthält Anleitungen zu Limits für die Datenerfassung in Adobe Experience Platform.

## Schutzmechanismen für die Batch-Erfassung

In der folgenden Tabelle sind die bei Verwendung der Variablen [Batch-Aufnahme-API](./batch-ingestion/overview.md) oder Quellen:

| Art der Aufnahme | Leitlinien | Anmerkungen |
| --- | --- | --- |
| Data Lake-Erfassung mithilfe der Batch-Aufnahme-API | <ul><li>Mit der Batch-Aufnahme-API können Sie bis zu 20 GB Daten pro Stunde in Data Lake erfassen.</li><li>Die maximale Anzahl von Dateien pro Batch beträgt 1500.</li><li>Die maximale Batch-Größe beträgt 100 GB.</li><li>Die maximale Anzahl von Eigenschaften oder Feldern pro Zeile beträgt 10.000.</li><li>Die maximale Anzahl von Batches pro Minute und Benutzer beträgt 138.</li></ul> |
| Data Lake-Erfassung mithilfe von Batch-Quellen | <ul><li>Mit Batch-Erfassungsquellen wie beispielsweise [!DNL Azure Blob], [!DNL Amazon S3]und [!DNL SFTP].</li><li>Die Batch-Größe sollte zwischen 256 MB und 100 GB liegen.</li><li>Die maximale Anzahl von Dateien pro Batch beträgt 1500.</li></ul> | Siehe [Quellen - Übersicht](../sources/home.md) für einen Katalog von Quellen, die Sie für die Datenerfassung verwenden können. |
| Batch-Erfassung in Profil | <ul><li>Sie können bis zu 120 GB Daten pro Stunde erfassen.</li><li>Die maximale Größe einer Datensatzklasse beträgt 100 KB (Soft).</li><li>Die maximale Größe einer ExperienceEvent-Klasse beträgt 10 KB (weich).</li><li>Die maximale Größe eines einzelnen Datensatzes beträgt 1 MB.</li></ul> |

## Limits für die Streaming-Erfassung

In der folgenden Tabelle sind die bei Verwendung der Variablen [Streaming-Aufnahme-API](./streaming-ingestion/overview.md) oder Streaming-Quellen:

| Art der Aufnahme | Leitlinien | Anmerkungen |
| --- | --- | --- |
| Streaming-Erfassung | <ul><li>Die maximale Datensatzgröße beträgt 1 MB, die empfohlene Größe beträgt 10 KB.</li><li>Sie können 20000 Anfragen pro Sekunde an Profile in weniger als einer Minute verarbeiten.</li><li>Sie können bis zu 20000 Anfragen pro Sekunde an Data Lake in weniger als 15 Minuten verarbeiten.</li></ul> | Verwenden Sie die Batch-Aufnahme-API , wenn Sie einen höheren Datendurchsatz benötigen. |
| Streaming-Quellen | <ul><li>Die maximale Datensatzgröße beträgt 1 MB, die empfohlene Größe beträgt 10 KB.</li><li>Streaming-Quellen unterstützen bei Erstellung einer neuen Quellverbindung zwischen 4000 und 5000 Anfragen pro Sekunde. **Hinweis**: Es kann bis zu 30 Minuten dauern, bis Streaming-Daten vollständig in Data Lake verarbeitet werden.</li><li>Sie können zwischen 4000 und 5000 Anfragen pro Sekunde an Data Lake verarbeiten. **Hinweis**: Es kann bis zu 30 Minuten dauern, bis Streaming-Daten vollständig in Data Lake verarbeitet werden.</li></ul> | Streaming-Quellen wie [!DNL Kafka], [!DNL Azure Event Hubs]und [!DNL Amazon Kinesis] Verwenden Sie nicht die [!DNL Data Collection Core Service] (DCCS) und unterschiedliche Durchsatzbeschränkungen aufweisen. Siehe [Quellen - Übersicht](../sources/home.md) für einen Katalog von Quellen, die Sie für die Datenerfassung verwenden können. |

## Nächste Schritte

Weitere Informationen zu Data- und Processing-Limits in Experience Platform finden Sie in der folgenden Dokumentation:

* [Limits für Echtzeit-Kundenprofil-Daten](../profile/guardrails.md)
* [Limits für Identity Service-Daten](../identity-service/guardrails.md)
