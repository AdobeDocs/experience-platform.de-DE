---
audience: user
user-guide-title: Hilfe zur Datenerfassung in Adobe Experience Platform
breadcrumb-title: Anleitung zur Datenaufnahme
user-guide-description: Implementieren Sie Ihre Daten durch Batch- oder Streaming-Aufnahmen in Platform.
feature: Datenerfassung
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 100%

---


# Datenerfassung in Adobe Experience Platform {#ingestion}

- [Datenerfassung – Übersicht](home.md)
- Streaming-Erfassung {#streaming}
   - [Übersicht](streaming-ingestion/overview.md)
   - [Kafka-Connector](streaming-ingestion/kafka.md)
   - [Fehlerbehebung](streaming-ingestion/troubleshooting.md)
- Batch-Erfassung {#batch}
   - [Übersicht](batch-ingestion/overview.md)
   - [Batch Ingestion-API](batch-ingestion/api-overview.md)
   - [Partielle Batch-Erfassung](batch-ingestion/partial.md)
   - [Fehlerbehebung](batch-ingestion/troubleshooting.md)
- Tutorials {#tutorials}
   - [Zuordnen einer CSV-Datei zu XDM](tutorials/map-a-csv-file.md)
   - [Aufnahmen von Batch-Daten über die Benutzeroberfläche](tutorials/ingest-batch-data.md)
   - [Erstellen einer authentifizierten Streaming-Verbindung](tutorials/create-authenticated-streaming-connection.md)
   - [Aufbauen einer Streaming-Verbindung (API)](tutorials/create-streaming-connection.md)
   - [Aufbauen einer Streaming-Verbindung (Benutzeroberfläche)](tutorials/create-streaming-connection-ui.md)
   - [Streaming von Datensatzdaten](tutorials/streaming-record-data.md)
   - [Streamen von Zeitreihendaten](tutorials/streaming-time-series-data.md)
   - [Streaming mehrerer Nachrichten](tutorials/streaming-multiple-messages.md)
- Qualität und Überwachung der Daten {#quality}
   - [Übersicht](quality/overview.md)
   - [Überwachen der Datenerfassung](quality/monitor-data-ingestion.md)
   - [Abrufen von Fehlerdiagnosen](quality/error-diagnostics.md)
   - [Abrufen fehlgeschlagener Batches](quality/retrieve-failed-batches.md)
   - [Validieren der Streaming-Erfasssung](quality/streaming-validation.md)
   - [Benachrichtigungen zur Datenerfassung](quality/subscribe-events.md)
- [Quellen-Connectoren](source-connectors.md)
- [API-Referenz](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)
- [Platform – Versionshinweise](https://docs.adobe.com/content/help/de-DE/experience-platform/release-notes/latest.html)