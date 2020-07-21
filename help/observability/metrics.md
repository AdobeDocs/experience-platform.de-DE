---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Verfügbare Metriken
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 82%

---


# Liste der verfügbaren Metriken

The following tables list all of the metrics that are exposed by Observability Insights, broken down by [!DNL Platform] service. Jede Metrik enthält eine Beschreibung und einen akzeptierten ID-Abfrageparameter.

## [!DNL Data Ingestion]

The following table outlines metrics for Adobe Experience Platform [!DNL Data Ingestion]. Metriken in **Fettdruck** sind Streaming-Erfassungsmetriken.

| Insights-Metrik  | Beschreibung | ID-Abfrageparameter |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | Gesamtzahl der erstellten Datensätze. | K. A. |
| timeseries.ingestion.dataset.size | Kumulative Größe aller Daten, die für einen Datensatz oder für alle Datensätze erfasst werden. | Datensatz-ID (optional) |
| timeseries.ingestion.dataset.dailysize | Größe der Daten, die täglich für einen Datensatz oder für alle Datensätze erfasst werden. | Datensatz-ID (optional) |
| timeseries.ingestion.dataset.batchfailed.count | Anzahl der fehlgeschlagenen Batches für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| timeseries.ingestion.dataset.batchsuccess.count | Anzahl der erfassten Batches für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| timeseries.ingestion.dataset.recordsuccess.count | Anzahl der erfassten Einträge für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| **timeseries.data.collection.validation.total.messages.rate** | Gesamtanzahl der Meldungen für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| **timeseries.data.collection.validation.valid.messages.rate** | Gesamtanzahl der gültigen Meldungen für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| **timeseries.data.collection.validation.invalid.messages.rate** | Gesamtzahl ungültiger Meldungen für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| **timeseries.data.collection.validation.category.type.count** | Gesamtanzahl ungültiger Meldungen vom Typ „Typ“ für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| **timeseries.data.collection.validation.category.range.count** | Gesamtanzahl ungültiger Meldungen vom Typ „Bereich“ für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| **timeseries.data.collection.validation.category.format.count** | Gesamtanzahl ungültiger Meldungen vom Typ „Format“ für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| **timeseries.data.collection.validation.category.pattern.count** | Gesamtanzahl ungültiger Meldungen vom Typ „Muster“ für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| **timeseries.data.collection.validation.category.presence.count** | Gesamtanzahl ungültiger Meldungen vom Typ „Präsenz“ für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| **timeseries.data.collection.validation.category.enum.count** | Gesamtanzahl ungültiger Meldungen vom Typ „Aufzählung“ für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| **timeseries.data.collection.validation.category.unclassified.count** | Gesamtanzahl ungültiger Meldungen vom Typ „Nicht klassifiziert“ für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| **timeseries.data.collection.validation.category.unknown.count** | Gesamtanzahl ungültiger Meldungen vom Typ „Unbekannt“ für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| **timeseries.data.collection.inlet.total.messages.received** | Gesamtzahl der Meldungen, die für einen Daten-Inlet oder für alle Daten-Inlets empfangen wurden. | Inlet-ID (optional) |
| **timeseries.data.collection.inlet.total.messages.size.received** | Gesamtgröße der Daten, die für einen Daten-Inlet oder für alle Daten-Inlets empfangen wurden. | Inlet-ID (optional) |
| **timeseries.data.collection.inlet.success** | Gesamtzahl erfolgreicher HTTP-Aufrufe an einen Daten-Inlet oder an alle Daten-Inlets. | Inlet-ID (optional) |
| **timeseries.data.collection.inlet.failure** | Gesamtzahl fehlgeschlagener HTTP-Aufrufe an einen Daten-Inlet oder an alle Daten-Inlets. | Inlet-ID (optional) |

## [!DNL Identity Service]

The following table outlines metrics for Adobe Experience Platform [!DNL Identity Service].

| Insights-Metrik  | Beschreibung | ID-Abfrageparameter |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | Number of records written to their data source by [!DNL Identity Service], for one dataset or all datasets. | Datensatz-ID (optional) |
| timeseries.identity.dataset.recordfailed.count | Number of records failed by [!DNL Identity Service], for one dataset or for all datasets. | Datensatz-ID (optional) |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | Anzahl der Identitätseinträge, die für einen Namespace erfolgreich erfasst wurden. | Namespace-ID (**erforderlich**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | Anzahl der Identitätseinträge, die aufgrund eines Namespace fehlgeschlagen sind. | Namespace-ID (**erforderlich**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Anzahl der Identitätseinträge, die von einem Namespace übersprungen wurden. | Namespace-ID (**erforderlich**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Anzahl der eindeutigen Identitäten, die im Identitätsdiagramm für Ihre IMS-Organisation gespeichert sind. | K. A. |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Anzahl der eindeutigen Identitäten, die im Identitätsdiagramm für einen Namespace gespeichert sind. | Namespace-ID (**erforderlich**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | Anzahl der eindeutigen Diagrammidentitäten, die im Identitätsdiagramm für Ihre IMS-Organisation gespeichert sind. | K. A. |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Anzahl der eindeutigen Identitäten, die im Identitätsdiagramm für Ihre IMS-Organisation für eine bestimmte Diagrammstärke („unbekannt“, „schwach oder „stark“) gespeichert sind. | Diagrammstärke (**erforderlich**) |

## [!DNL Privacy Service]

The following table outlines metrics for Adobe Experience Platform [!DNL Privacy Service].

| Insights-Metrik  | Beschreibung | ID-Abfrageparameter |
| ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | Gesamtzahl der erstellten Aufträge von DSGVO. | ENV (**erforderlich**) |
| timeseries.gdpr.jobs.completedjobs.count | Gesamtzahl der abgeschlossenen Aufträge von DSGVO. | ENV (**erforderlich**) |
| timeseries.gdpr.jobs.errorjobs.count | Gesamtanzahl der Fehleraufträge von DSGVO. | ENV (**erforderlich**) |

## [!DNL Query Service]

The following table outlines metrics for Adobe Experience Platform [!DNL Query Service].

| Insights-Metrik  | Beschreibung | ID-Abfrageparameter |
| ---- | ---- | ---- |
| timeseries.queryservice.query.scheduleonce.count | Gesamtanzahl der einmaligen geplanten Abfragen. | K. A. |
| timeseries.queryservice.query.scheduledrecurring.count | Gesamtanzahl der wiederkehrenden geplanten Abfragen. | K. A. |
| timeseries.queryservice.query.batchquery.count | Gesamtzahl der ausgeführten Batch-Abfragen. | K. A. |
| timeseries.queryservice.query.scheduledquery.count | Gesamtzahl der ausgeführten geplanten Abfragen. | K. A. |
| timeseries.queryservice.query.interactivequery.count | Gesamtanzahl der ausgeführten interaktiven Abfragen. | K. A. |
| timeseries.queryservice.query.batchfrompsqlquery.count | Gesamtzahl der ausgeführten Batch-Abfragen von PSQL. | K. A. |

## [!DNL Real-time Customer Profile]

The following table outlines metrics for [!DNL Real-time Customer Profile].

| Insights-Metrik  | Beschreibung | ID-Abfrageparameter |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | Number of records read from the [!DNL Data Lake] by [!DNL Profile], for one dataset or for all datasets. | Datensatz-ID (optional) |
| timeseries.profiles.dataset.recordsuccess.count | Number of records written to their data source by [!DNL Profile], for one dataset or for all datasets. | Datensatz-ID (optional) |
| timeseries.profiles.dataset.recordfailed.count | Number of records failed by [!DNL Profile], for one dataset or for all datasets. | Datensatz-ID (optional) |
| timeseries.profiles.dataset.batchsuccess.count | Number of [!DNL Profile] batches ingested for a dataset or for all datasets. | Datensatz-ID (optional) |
| timeseries.profiles.dataset.batchfailed.count | Number of [!DNL Profile] batches failed for one dataset or for all datasets. | Datensatz-ID (optional) |
| platform.ups.ingest.streaming.request.m1_rate | Rate eingehender Anfragen. | IMS-Organisation |
| platform.ups.ingest.streaming.access.put.success.m1_rate | Erfolgsrate der Aufnahme. | IMS-Organisation |
| platform.ups.ingest.streaming.records.created.m15_rate | Rate der neuen Einträge, die für einen Datensatz erfasst werden. | Datensatz-ID |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | Rate von mit Zeitstempel versehenen und sich nicht in der Reihenfolge befindlichen Einträgen für die Erstellungsanfrage für einen Datensatz. | Datensatz-ID |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | Zeitstempel für die letzte Anfrage zur Eintragserstellung für einen Datensatz. | Datensatz-ID |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | Rate von mit Zeitstempel versehenen und sich nicht in der Reihenfolge befindlichen Einträgen für die Aktualisierungsanfrage für einen Datensatz. | Datensatz-ID |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | Zeitstempel für die letzte Anfrage zur Eintragsaktualisierung für einen Datensatz. | Datensatz-ID |
| platform.ups.ingest.streaming.record.size.m1_rate | Durchschnittliche Eintragsgröße. | IMS-Organisation |
| platform.ups.ingest.streaming.records.updated.m15_rate | Rate von Aktualisierungsanfragen für Einträge, die für einen Datensatz erfasst werden. | Datensatz-ID |
