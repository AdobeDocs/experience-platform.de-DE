---
audience: user
user-guide-title: Hilfe zur Datenerfassung in Adobe Experience Platform
breadcrumb-title: Anleitung zur Datenaufnahme
user-guide-description: Implementieren Sie Ihre Daten in Experience Platform durch die Batch- oder Streaming-Aufnahme.
feature: Data Ingestion
source-git-commit: 6110bf51cbd0005428e7dab4552944c5c9b54d03
workflow-type: ht
source-wordcount: '156'
ht-degree: 100%

---


# Datenerfassung in Adobe Experience Platform {#ingestion}

- [Datenerfassung – Übersicht](home.md)
- Streaming-Erfassung {#streaming}
   - [Übersicht](streaming-ingestion/overview.md)
   - [Kafka-Connector](streaming-ingestion/kafka.md)
   - [Fehlerbehebung](streaming-ingestion/troubleshooting.md)
- Batch-Erfassung {#batch}
   - [Erste Schritte mit APIs zur Batch-Aufnahme](batch-ingestion/getting-started.md)
   - [API-Übersicht](batch-ingestion/overview.md)
   - [API-Entwicklerhandbuch](batch-ingestion/api-overview.md)
   - [Partielle Batch-Erfassung](batch-ingestion/partial.md)
   - [Fehlerbehebung](batch-ingestion/troubleshooting.md)
- Tutorials {#tutorials}
   - Zuordnen einer CSV-Datei zu XDM {#map-csv}
      - [Übersicht](./tutorials/map-csv/overview.md)
      - [Zuordnen einer CSV-Datei zu einem vorhandenen Schema](./tutorials/map-csv/existing-schema.md)
      - [Zuordnen einer CSV-Datei unter Verwendung von KI-generierten Empfehlungen](./tutorials/map-csv/recommendations.md)
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
- [Schutzmaßnahmen bei der Datenaufnahme](guardrails.md)
- [Quell-Connectoren](source-connectors.md)
- [Referenz zur Batch-Aufnahme-API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)
- [Referenz zur Streaming-Aufnahme-API](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/)
- [Platform – Versionshinweise](https://docs.adobe.com/content/help/de-DE/experience-platform/release-notes/latest.html)
