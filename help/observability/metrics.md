---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Verfügbare Metriken
topic: developer guide
translation-type: tm+mt
source-git-commit: 947955403a270914437d9172bca458f9c49ccd8f

---


# Liste der verfügbaren Metriken

Im Folgenden finden Sie eine Liste von Metriken, die von Observability Insights bereitgestellt werden, jeweils mit dem zugehörigen Plattformdienst, der zugehörigen Beschreibung und dem akzeptierten Parameter für die ID-Abfrage.

| Insight-Metrik | Plattformdienst | Beschreibung | ID-Abfrage-Parameter |
| ---- | ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | Dateneinbindung | Gesamtzahl der erstellten Datensätze. | K. A. |
| timeseries.ingestion.dataset.size | Dateneinbindung | Kumulative Größe aller Daten, die für einen Datensatz für oder alle Datensätze erfasst werden. | Datensatz-ID (optional) |
| timeseries.ingestion.dataset.dailysize | Dateneinbindung | Die Menge der Daten, die auf der Grundlage der täglichen Nutzung für einen Datensatz oder für alle Datensätze erfasst werden. | Datensatz-ID (optional) |
| timeseries.ingestion.dataset.batchfailed.count | Dateneinbindung | Anzahl der Stapel für einen Datensatz oder für alle Datensätze fehlgeschlagen. | Datensatz-ID (optional) |
| timeseries.ingestion.dataset.batchsuccess.count | Dateneinbindung | Anzahl der für einen Datensatz oder für alle Datensätze erfassten Stapel. | Datensatz-ID (optional) |
| timeseries.ingestion.dataset.records.count | Dateneinbindung | Anzahl der Datensätze, die für einen Datensatz oder für alle Datensätze erfasst werden. | Datensatz-ID (optional) |
| timeseries.data.collection.validation.total.messages.rate | Dateneinbettung (Streaming) | Gesamtanzahl der Meldungen für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| timeseries.data.collection.validation.valid.messages.rate | Dateneinbettung (Streaming) | Gesamtanzahl der gültigen Meldungen für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| timeseries.data.collection.validation.Invalid.messages.rate | Dateneinbettung (Streaming) | Gesamtzahl ungültiger Meldungen für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| timeseries.data.collection.validation.Kategorie.type.count | Dateneinbettung (Streaming) | Gesamtanzahl ungültiger Meldungen vom Typ &quot;Typ&quot;für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| timeseries.data.collection.validation.Kategorie.range.count | Dateneinbettung (Streaming) | Gesamtzahl ungültiger &quot;Bereichsmeldungen&quot;für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| timeseries.data.collection.validation.Kategorie.format.count | Dateneinbettung (Streaming) | Gesamtzahl ungültiger &quot;Formatmeldungen&quot;für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| timeseries.data.collection.validation.Kategorie.pattern.count | Dateneinbettung (Streaming) | Gesamtanzahl ungültiger &quot;Muster&quot;-Meldungen für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| timeseries.data.collection.validation.Kategorie.presence.count | Dateneinbettung (Streaming) | Gesamtzahl ungültiger &quot;Präsenzmeldungen&quot;für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| timeseries.data.collection.validation.Kategorie.enum.count | Dateneinbettung (Streaming) | Gesamtzahl ungültiger &quot;Enum&quot;-Meldungen für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| timeseries.data.collection.validation.Kategorie.unclassi.count | Dateneinbettung (Streaming) | Gesamtzahl ungültiger &quot;nicht klassifizierter&quot;Nachrichten für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| timeseries.data.collection.validation.Kategorie.unknown.count | Dateneinbettung (Streaming) | Gesamtzahl ungültiger &quot;unbekannter&quot;Meldungen für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| timeseries.data.collection.delivery.total.messages.receive | Dateneinbettung (Streaming) | Gesamtzahl der Nachrichten, die für einen Dateneinlass oder für alle Dateneingänge empfangen wurden. | Inlet-ID (optional) |
| timeseries.data.collection.delivery.total.messages.size.receive | Dateneinbettung (Streaming) | Gesamtgröße der empfangenen Daten für einen Dateneinlass oder für alle Dateneingänge. | Inlet-ID (optional) |
| timeseries.data.collection.delivery.success | Dateneinbettung (Streaming) | Gesamtzahl erfolgreicher HTTP-Aufrufe an einen Dateneinlass oder an alle Dateneingänge. | Inlet-ID (optional) |
| timeseries.data.collection.delivery.failure | Dateneinbettung (Streaming) | Gesamtzahl der fehlgeschlagenen HTTP-Aufrufe an einen Dateneinlass oder an alle Dateneingänge. | Inlet-ID (optional) |
| timeseries.Profils.dataset.records.count | Echtzeit-Kundenprofil | Anzahl der Datensätze, die aus dem Datensee nach Profil, für einen Datensatz oder für alle Datensätze gelesen werden. | Datensatz-ID (optional) |
| timeseries.Profils.dataset.records.count | Echtzeit-Kundenprofil | Anzahl der Datensätze, die in ihre Datenquelle geschrieben wurden, nach Profil, für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| timeseries.Profils.dataset.records.failed.count | Echtzeit-Kundenprofil | Anzahl der Datensätze fehlgeschlagen nach Profil, für einen Datensatz oder für alle Datensätze. | Datensatz-ID (optional) |
| timeseries.Profils.dataset.batchsuccess.count | Echtzeit-Kundenprofil | Anzahl der Profil-Stapel, die für einen Datensatz oder für alle Datensätze erfasst werden. | Datensatz-ID (optional) |
| timeseries.Profils.dataset.batchfailed.count | Echtzeit-Kundenprofil | Anzahl der Profil-Stapel für einen Datensatz oder für alle Datensätze fehlgeschlagen. | Datensatz-ID (optional) |
| timeseries.identity.dataset.recordSucc.count | Identitätsdienst | Anzahl der Datensätze, die vom Identitätsdienst in ihre Datenquelle geschrieben wurden, für einen Datensatz oder alle Datensätze. | Datensatz-ID (optional) |
| timeseries.identity.dataset.records.failed.count | Identitätsdienst | Anzahl der Datensätze, die vom Identitätsdienst, für einen Datensatz oder für alle Datensätze fehlgeschlagen sind. | Datensatz-ID (optional) |
| timeseries.identity.dataset.namespacecode.records.count | Identitätsdienst | Anzahl der Identitätsdatensätze, die für einen Namensraum erfolgreich erfasst wurden. | Namensraum-ID (**erforderlich**) |
| timeseries.identity.dataset.namespacecode.records.failure | Identitätsdienst | Anzahl der Identitätsdatensätze durch einen Namensraum fehlgeschlagen. | Namensraum-ID (**erforderlich**) |
| timeseries.identity.dataset.namespacecode.records.count | Identitätsdienst | Anzahl der Identitätsdatensätze, die von einem Namensraum übersprungen wurden. | Namensraum-ID (**erforderlich**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Identitätsdienst | Anzahl der eindeutigen Identitäten, die im Identitätsdiagramm für Ihre IMS-Organisation gespeichert sind. | K. A. |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Identitätsdienst | Anzahl der eindeutigen Identitäten, die im Identitätsdiagramm für einen Namensraum gespeichert werden. | Namensraum-ID (**erforderlich**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | Identitätsdienst | Anzahl der eindeutigen Diagrammkennungen, die im Identitätsdiagramm für Ihre IMS-Organisation gespeichert sind. | K. A. |
| timeseries.identity.graph.imsorg.graphstrong.uniqueidentities.count | Identitätsdienst | Anzahl der eindeutigen Identitäten, die im Identitätsdiagramm für Ihre IMS-Organisation für eine bestimmte Diagrammstärke (&quot;unbekannt&quot;, &quot;schwach&quot;oder &quot;stark&quot;) gespeichert werden. | Diagrammstärke (**erforderlich**) |
| timeseries.gdpr.jobs.totaljobs.count | DSGVO | Gesamtzahl der durch das GDPR geschaffenen Arbeitsplätze. | ENV (**erforderlich**) |
| timeseries.gdpr.jobs.completedjobs.count | DSGVO | Gesamtzahl der abgeschlossenen Aufträge aus dem GDPR. | ENV (**erforderlich**) |
| timeseries.gdpr.jobs.errorjobs.count | DSGVO | Gesamtanzahl der Fehleraufträge aus GDPR. | ENV (**erforderlich**) |
| timeseries.queryservice.Abfrage.Scheduleonce.count | Abfrage | Gesamtanzahl der nicht wiederkehrenden geplanten Abfragen. | K. A. |
| timeseries.queryservice.Abfrage.scheduleRecurring.count | Abfrage | Gesamtanzahl der wiederkehrenden geplanten Abfragen. | K. A. |
| timeseries.queryservice.Abfrage.batchquery.count | Abfrage | Gesamtzahl der ausgeführten Batch-Abfragen. | K. A. |
| timeseries.queryservice.Abfrage.Scheduledquery.count | Abfrage | Gesamtzahl der ausgeführten geplanten Abfragen | K. A. |
| timeseries.queryservice.Abfrage.interactivequery.count | Abfrage | Gesamtanzahl der ausgeführten interaktiven Abfragen. | K. A. |
| timeseries.queryservice.Abfrage.batchfrompsqlquery.count | Abfrage | Gesamtzahl der ausgeführten Batch-Abfragen von PSQL. | K. A. |