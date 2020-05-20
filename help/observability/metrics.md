---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Verfügbare Metriken
topic: developer guide
translation-type: tm+mt
source-git-commit: ff299a69a81f00cad3e90a83f7411e4b15d4f850
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 3%

---


# Liste der verfügbaren Metriken

In den folgenden Tabellen werden alle Metriken, die von Observability Insights bereitgestellt werden, nach Plattformdienst aufgeschlüsselt Liste. Jede Metrik enthält eine Beschreibung und einen akzeptierten ID-Abfrage-Parameter.

## Dateneinbindung

In der folgenden Tabelle sind die Metriken für die Dateneinbettung in Adobe Experience Platform aufgeführt. Metriken in **Fettdruck** sind Streaming-Erfassungsmetriken.

| Insight-Metrik  | Beschreibung | ID-Abfrage-Parameter |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | Gesamtzahl der erstellten Datensätze. | K. A. |
| timeseries.ingestion.dataset.size | Kumulative Größe aller Daten, die für einen Datensatz für oder alle Datensätze erfasst werden. | Datensatz-ID (optional) |
| timeseries.ingestion.dataset.dailysize | Die Menge der Daten, die auf der Grundlage der täglichen Nutzung für einen Datensatz oder für alle Datensätze erfasst werden. | Datensatz-ID (optional) |
| timeseries.ingestion.dataset.batchfailed.count | Anzahl der Stapel für einen Datensatz oder für alle Datensätze fehlgeschlagen. | Datensatz-ID (optional) |
| timeseries.ingestion.dataset.batchsuccess.count | Anzahl der für einen Datensatz oder für alle Datensätze erfassten Stapel. | Datensatz-ID (optional) |
| timeseries.ingestion.dataset.recordsuccess.count | Anzahl der Datensätze, die für einen Datensatz oder für alle Datensätze erfasst werden. | Datensatz-ID (optional) |
| **timeseries.data.collection.validation.total.messages.rate** | Gesamtanzahl der Meldungen für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| **timeseries.data.collection.validation.valid.messages.rate** | Gesamtanzahl der gültigen Meldungen für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| **timeseries.data.collection.validation.Invalid.messages.rate** | Gesamtzahl ungültiger Meldungen für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| **timeseries.data.collection.validation.Kategorie.type.count** | Gesamtanzahl ungültiger Meldungen vom Typ &quot;Typ&quot;für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| **timeseries.data.collection.validation.Kategorie.range.count** | Gesamtzahl ungültiger &quot;Bereichsmeldungen&quot;für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| **timeseries.data.collection.validation.Kategorie.format.count** | Gesamtzahl ungültiger &quot;Formatmeldungen&quot;für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| **timeseries.data.collection.validation.Kategorie.pattern.count** | Gesamtanzahl ungültiger &quot;Muster&quot;-Meldungen für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| **timeseries.data.collection.validation.Kategorie.presence.count** | Gesamtzahl ungültiger &quot;Präsenzmeldungen&quot;für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| **timeseries.data.collection.validation.Kategorie.enum.count** | Gesamtzahl ungültiger &quot;Enum&quot;-Meldungen für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| **timeseries.data.collection.validation.Kategorie.unclassi.count** | Gesamtzahl ungültiger &quot;nicht klassifizierter&quot;Nachrichten für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| **timeseries.data.collection.validation.Kategorie.unknown.count** | Gesamtzahl ungültiger &quot;unbekannter&quot;Meldungen für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| **timeseries.data.collection.delivery.total.messages.receive** | Gesamtzahl der Nachrichten, die für einen Dateneinlass oder für alle Dateneingänge empfangen wurden. | Inlet-ID (optional) |
| **timeseries.data.collection.delivery.total.messages.size.receive** | Gesamtgröße der empfangenen Daten für einen Dateneinlass oder für alle Dateneingänge. | Inlet-ID (optional) |
| **timeseries.data.collection.delivery.success** | Gesamtzahl erfolgreicher HTTP-Aufrufe an einen Dateneinlass oder an alle Dateneingänge. | Inlet-ID (optional) |
| **timeseries.data.collection.delivery.failure** | Gesamtzahl der fehlgeschlagenen HTTP-Aufrufe an einen Dateneinlass oder an alle Dateneingänge. | Inlet-ID (optional) |

## Identitätsdienst

In der folgenden Tabelle sind die Metriken für den Identitätsdienst für Adobe Experience Platform aufgeführt.

| Insight-Metrik  | Beschreibung | ID-Abfrage-Parameter |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | Anzahl der Datensätze, die vom Identitätsdienst in ihre Datenquelle geschrieben wurden, für einen Datensatz oder alle Datensätze. | Datensatz-ID (optional) |
| timeseries.identity.dataset.recordfailed.count | Anzahl der Datensätze, die vom Identitätsdienst, für einen Datensatz oder für alle Datensätze fehlgeschlagen sind. | Datensatz-ID (optional) |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | Anzahl der Identitätsdatensätze, die für einen Namensraum erfolgreich erfasst wurden. | Namensraum-ID (**erforderlich**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | Anzahl der Identitätsdatensätze durch einen Namensraum fehlgeschlagen. | Namensraum-ID (**erforderlich**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Anzahl der Identitätsdatensätze, die von einem Namensraum übersprungen wurden. | Namensraum-ID (**erforderlich**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Anzahl der eindeutigen Identitäten, die im Identitätsdiagramm für Ihre IMS-Organisation gespeichert sind. | K. A. |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Anzahl der eindeutigen Identitäten, die im Identitätsdiagramm für einen Namensraum gespeichert werden. | Namensraum-ID (**erforderlich**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | Anzahl der eindeutigen Diagrammkennungen, die im Identitätsdiagramm für Ihre IMS-Organisation gespeichert sind. | K. A. |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Anzahl der eindeutigen Identitäten, die im Identitätsdiagramm für Ihre IMS-Organisation für eine bestimmte Diagrammstärke (&quot;unbekannt&quot;, &quot;schwach&quot;oder &quot;stark&quot;) gespeichert werden. | Diagrammstärke (**erforderlich**) |

## Privacy Service

In der folgenden Tabelle sind die Metriken für den Adobe Experience Platform-Datenschutzdienst aufgeführt.

| Insight-Metrik  | Beschreibung | ID-Abfrage-Parameter |
| ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | Gesamtzahl der durch das GDPR geschaffenen Arbeitsplätze. | ENV (**erforderlich**) |
| timeseries.gdpr.jobs.completedjobs.count | Gesamtzahl der abgeschlossenen Aufträge aus dem GDPR. | ENV (**erforderlich**) |
| timeseries.gdpr.jobs.errorjobs.count | Gesamtanzahl der Fehleraufträge aus GDPR. | ENV (**erforderlich**) |

## Abfrage

In der folgenden Tabelle sind die Metriken für den Adobe Experience Platform Abfrage Service aufgeführt.

| Insight-Metrik  | Beschreibung | ID-Abfrage-Parameter |
| ---- | ---- | ---- |
| timeseries.queryservice.query.scheduleonce.count | Gesamtanzahl der nicht wiederkehrenden geplanten Abfragen. | K. A. |
| timeseries.queryservice.query.scheduledrecurring.count | Gesamtanzahl der wiederkehrenden geplanten Abfragen. | K. A. |
| timeseries.queryservice.query.batchquery.count | Gesamtzahl der ausgeführten Batch-Abfragen. | K. A. |
| timeseries.queryservice.query.scheduledquery.count | Gesamtzahl der ausgeführten geplanten Abfragen | K. A. |
| timeseries.queryservice.query.interactivequery.count | Gesamtanzahl der ausgeführten interaktiven Abfragen. | K. A. |
| timeseries.queryservice.query.batchfrompsqlquery.count | Gesamtzahl der ausgeführten Batch-Abfragen von PSQL. | K. A. |

## Echtzeit-Kundenprofil

In der folgenden Tabelle sind die Metriken für das Echtzeit-Profil von Kunden aufgeführt.

| Insight-Metrik  | Beschreibung | ID-Abfrage-Parameter |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | Anzahl der Datensätze, die aus dem Datensee nach Profil, für einen Datensatz oder für alle Datensätze gelesen werden. | Datensatz-ID (optional) |
| timeseries.profiles.dataset.recordsuccess.count | Anzahl der Datensätze, die in ihre Datenquelle geschrieben wurden, nach Profil, für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| timeseries.profiles.dataset.recordfailed.count | Anzahl der Datensätze fehlgeschlagen nach Profil, für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| timeseries.profiles.dataset.batchsuccess.count | Anzahl der Profil-Stapel, die für einen Datensatz oder für alle Datensätze erfasst werden. | Datensatz-ID (optional) |
| timeseries.profiles.dataset.batchfailed.count | Anzahl der Profil-Stapel für einen Datensatz oder für alle Datensätze fehlgeschlagen. | Datensatz-ID (optional) |
| platform.ups.ingest.streaming.request.m1_rate | Eingangsanforderungsrate. | IMS-Org |
| platform.ups.ingest.streaming.access.put.success.m1_rate | Erfolgsrate der Ingestion. | IMS-Org |
| platform.ups.ingest.streaming.records.created.m15_rate | Rate der neuen Datensätze, die für einen Datensatz erfasst werden. | Datenbestand-ID |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | Rate von nicht in der Reihenfolge befindlichen Datensätzen zum Erstellen einer Anforderung für einen Datensatz. | Datenbestand-ID |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | Zeitstempel für die letzte Datensatzanforderung für einen Datensatz. | Datenbestand-ID |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | Rate von nicht in der Reihenfolge befindlichen Datensätzen mit Zeitstempel für die Aktualisierungsanforderung eines Datensatzes. | Datenbestand-ID |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | Zeitstempel für die Anforderung des letzten Aktualisierungsdatensatzes für einen Datensatz. | Datenbestand-ID |
| platform.ups.ingest.streaming.record.size.m1_rate | Durchschnittliche Datensatzgröße. | IMS-Org |
| platform.ups.ingest.streaming.records.updated.m15_rate | Rate der Aktualisierungsanforderungen für Datensätze, die für einen Datensatz erfasst werden. | Datenbestand-ID |
