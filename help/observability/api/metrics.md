---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Verfügbare Metriken
topic: developer guide
translation-type: tm+mt
source-git-commit: c5455dc0812b251483170ac19506d7c60ad4ecaa
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 70%

---


# Metrik-Endpunkt

Beobachtungsmetriken bieten Einblicke in Nutzungsstatistiken, historische Trends und Leistungsindikatoren für verschiedene Funktionen in Adobe Experience Platform. Mit dem `/metrics` Endpunkt im [!DNL Observability Insights API] können Sie Metrikdaten für die Aktivität Ihres Unternehmens in [!DNL Platform]programmgesteuert abrufen.

## Erste Schritte

The API endpoint used in this guide is part of the [[!DNL Observability Insights] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml). Bevor Sie fortfahren, lesen Sie bitte die [Anleitung](./getting-started.md) zu den ersten Schritten für Links zur zugehörigen Dokumentation, eine Anleitung zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtige Informationen zu den erforderlichen Kopfzeilen, die zum erfolgreichen Aufrufen einer beliebigen [!DNL Experience Platform] API erforderlich sind.

## Beobachtbarkeitsmetriken abrufen

You can retrieve observability metrics by making a GET request to the `/metrics` endpoint in the [!DNL Observability Insights] API.

**API-Format**

Bei Verwendung des `/metrics`-Endpunkts muss mindestens ein Metrikanfrageparameter angegeben werden. Andere Abfrageparameter dienen optional zum Filtern von Ergebnissen.

```http
GET /metrics?metric={METRIC}
GET /metrics?metric={METRIC}&metric={METRIC_2}
GET /metrics?metric={METRIC}&id={ID}
GET /metrics?metric={METRIC}&dateRange={DATE_RANGE}
GET /metrics?metric={METRIC}&metric={METRIC_2}&id={ID}&dateRange={DATE_RANGE}
```

| Parameter | Beschreibung |
| --- | --- |
| `{METRIC}` | Die Metrik, die Sie verfügbar machen möchten. Wenn Sie mehrere Metriken in einem einzelnen Aufruf kombinieren, müssen Sie kaufmännische Und-Zeichen (`&`) verwenden, um einzelne Metriken voneinander zu trennen. Beispiel: `metric={METRIC_1}&metric={METRIC_2}`. |
| `{ID}` | The identifier for a particular [!DNL Platform] resource whose metrics you want to expose. Diese Kennung kann je nach verwendeter Metrik optional, erforderlich oder nicht anwendbar sein. Eine Liste der verfügbaren Metriken sowie der unterstützten IDs (sowohl erforderlich als auch optional) für jede Metrik finden Sie im [Anhang](#available-metrics) . |
| `{DATE_RANGE}` | Der Datumsbereich für die Metriken, die Sie verfügbar machen möchten, im ISO 8601-Format (z. B. `2018-10-01T07:00:00.000Z/2018-10-09T07:00:00.000Z`). |

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/observability/insights/metrics?metric=timeseries.ingestion.dataset.size&metric=timeseries.ingestion.dataset.recordsuccess.count&id=5cf8ab4ec48aba145214abeb&dateRange=2018-10-01T07:00:00.000Z/2019-06-06T07:00:00.000Z \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Objekten zurück, jeweils mit einem Zeitstempel innerhalb des angegebenen `dateRange` und den entsprechenden Werten für die im Anfragepfad angegebenen Metriken. If the `id` of a [!DNL Platform] resource is included in the request path, the results will apply only to that particular resource. Wenn die `id` weggelassen wird, gelten die Ergebnisse für alle anwendbaren Ressourcen in Ihrer IMS-Organisation.

```json
{
    "id": "5cf8ab4ec48aba145214abeb",
    "imsOrgId": "{IMS_ORG}",
    "timeseries": {
        "granularity": "MONTH",
        "items": [
            {
                "timestamp": "2019-06-01T00:00:00Z",
                "metrics": {
                    "timeseries.ingestion.dataset.recordsuccess.count": 1125,
                    "timeseries.ingestion.dataset.size": 32320
                }
            },
            {
                "timestamp": "2019-05-01T00:00:00Z",
                "metrics": {
                    "timeseries.ingestion.dataset.recordsuccess.count": 1003,
                    "timeseries.ingestion.dataset.size": 31409
                }
            },
            {
                "timestamp": "2019-04-01T00:00:00Z",
                "metrics": {
                    "timeseries.ingestion.dataset.recordsuccess.count": 740,
                    "timeseries.ingestion.dataset.size": 25809
                }
            },
            {
                "timestamp": "2019-03-01T00:00:00Z",
                "metrics": {
                    "timeseries.ingestion.dataset.recordsuccess.count": 740,
                    "timeseries.ingestion.dataset.size": 25809
                }
            },
            {
                "timestamp": "2019-02-01T00:00:00Z",
                "metrics": {
                    "timeseries.ingestion.dataset.recordsuccess.count": 390,
                    "timeseries.ingestion.dataset.size": 16801
                }
            }
        ],
        "_page": null,
        "_links": null
    },
    "stats": {}
}
```

## Anhang

Der folgende Abschnitt enthält weitere Informationen zum Arbeiten mit dem `/metrics` Endpunkt.

### Verfügbare Metriken {#available-metrics}

The following tables list all of the metrics that are exposed by [!DNL Observability Insights], broken down by [!DNL Platform] service. Jede Metrik enthält eine Beschreibung und einen akzeptierten ID-Abfrageparameter.

>[!NOTE]
>
>Alle aufgelisteten ID-Abfragen sind optional, sofern nicht anders angegeben.

#### [!DNL Data Ingestion] {#ingestion}

The following table outlines metrics for Adobe Experience Platform [!DNL Data Ingestion]. Metriken in **Fettdruck** sind Streaming-Erfassungsmetriken.

| Insight-Metrik | Beschreibung | ID-Abfrageparameter |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | Gesamtzahl der erstellten Datensätze. | K. A. |
| timeseries.ingestion.dataset.size | Kumulative Größe aller Daten, die für einen Datensatz oder für alle Datensätze erfasst werden. | Datensatz-ID |
| timeseries.ingestion.dataset.dailysize | Größe der Daten, die täglich für einen Datensatz oder für alle Datensätze erfasst werden. | Datensatz-ID |
| timeseries.ingestion.dataset.batchfailed.count | Anzahl der fehlgeschlagenen Batches für einen Datensatz oder für alle Datensätze. | Datensatz-ID |
| timeseries.ingestion.dataset.batchsuccess.count | Anzahl der erfassten Batches für einen Datensatz oder für alle Datensätze. | Datensatz-ID |
| timeseries.ingestion.dataset.recordsuccess.count | Anzahl der erfassten Einträge für einen Datensatz oder für alle Datensätze. | Datensatz-ID |
| **timeseries.data.collection.validation.total.messages.rate** | Gesamtanzahl der Meldungen für einen Datensatz oder für alle Datensätze. | Datensatz-ID |
| **timeseries.data.collection.validation.valid.messages.rate** | Gesamtanzahl der gültigen Meldungen für einen Datensatz oder für alle Datensätze. | Datensatz-ID |
| **timeseries.data.collection.validation.invalid.messages.rate** | Gesamtzahl ungültiger Meldungen für einen Datensatz oder für alle Datensätze. | Datensatz-ID |
| **timeseries.data.collection.validation.category.type.count** | Gesamtanzahl ungültiger Meldungen vom Typ „Typ“ für einen Datensatz oder für alle Datensätze. | Datensatz-ID |
| **timeseries.data.collection.validation.category.range.count** | Gesamtanzahl ungültiger Meldungen vom Typ „Bereich“ für einen Datensatz oder für alle Datensätze. | Datensatz-ID |
| **timeseries.data.collection.validation.category.format.count** | Gesamtanzahl ungültiger Meldungen vom Typ „Format“ für einen Datensatz oder für alle Datensätze. | Datensatz-ID |
| **timeseries.data.collection.validation.category.pattern.count** | Gesamtanzahl ungültiger Meldungen vom Typ „Muster“ für einen Datensatz oder für alle Datensätze. | Datensatz-ID |
| **timeseries.data.collection.validation.category.presence.count** | Gesamtanzahl ungültiger Meldungen vom Typ „Präsenz“ für einen Datensatz oder für alle Datensätze. | Datensatz-ID |
| **timeseries.data.collection.validation.category.enum.count** | Gesamtanzahl ungültiger Meldungen vom Typ „Aufzählung“ für einen Datensatz oder für alle Datensätze. | Datensatz-ID |
| **timeseries.data.collection.validation.category.unclassified.count** | Gesamtanzahl ungültiger Meldungen vom Typ „Nicht klassifiziert“ für einen Datensatz oder für alle Datensätze. | Datensatz-ID |
| **timeseries.data.collection.validation.category.unknown.count** | Gesamtanzahl ungültiger Meldungen vom Typ „Unbekannt“ für einen Datensatz oder für alle Datensätze. | Datensatz-ID |
| **timeseries.data.collection.inlet.total.messages.received** | Gesamtzahl der Meldungen, die für einen Daten-Inlet oder für alle Daten-Inlets empfangen wurden. | Inlet-ID |
| **timeseries.data.collection.inlet.total.messages.size.received** | Gesamtgröße der Daten, die für einen Daten-Inlet oder für alle Daten-Inlets empfangen wurden. | Inlet-ID |
| **timeseries.data.collection.inlet.success** | Gesamtzahl erfolgreicher HTTP-Aufrufe an einen Daten-Inlet oder an alle Daten-Inlets. | Inlet-ID |
| **timeseries.data.collection.inlet.failure** | Gesamtzahl fehlgeschlagener HTTP-Aufrufe an einen Daten-Inlet oder an alle Daten-Inlets. | Inlet-ID |

#### [!DNL Identity Service] {#identity}

The following table outlines metrics for Adobe Experience Platform [!DNL Identity Service].

| Insight-Metrik | Beschreibung | ID-Abfrageparameter |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | Number of records written to their data source by [!DNL Identity Service], for one dataset or all datasets. | Datensatz-ID |
| timeseries.identity.dataset.recordfailed.count | Number of records failed by [!DNL Identity Service], for one dataset or for all datasets. | Datensatz-ID |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | Anzahl der Identitätseinträge, die für einen Namespace erfolgreich erfasst wurden. | Namespace-ID (**erforderlich**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | Anzahl der Identitätseinträge, die aufgrund eines Namespace fehlgeschlagen sind. | Namespace-ID (**erforderlich**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Anzahl der Identitätseinträge, die von einem Namespace übersprungen wurden. | Namespace-ID (**erforderlich**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Anzahl der eindeutigen Identitäten, die im Identitätsdiagramm für Ihre IMS-Organisation gespeichert sind. | K. A. |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Anzahl der eindeutigen Identitäten, die im Identitätsdiagramm für einen Namespace gespeichert sind. | Namespace-ID (**erforderlich**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | Anzahl der eindeutigen Diagrammidentitäten, die im Identitätsdiagramm für Ihre IMS-Organisation gespeichert sind. | K. A. |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Anzahl der eindeutigen Identitäten, die im Identitätsdiagramm für Ihre IMS-Organisation für eine bestimmte Diagrammstärke („unbekannt“, „schwach oder „stark“) gespeichert sind. | Diagrammstärke (**erforderlich**) |

#### [!DNL Privacy Service] {#privacy}

The following table outlines metrics for Adobe Experience Platform [!DNL Privacy Service].

| Insight-Metrik | Beschreibung | ID-Abfrageparameter |
| ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | Gesamtzahl der erstellten Aufträge von DSGVO. | ENV (**erforderlich**) |
| timeseries.gdpr.jobs.completedjobs.count | Gesamtzahl der abgeschlossenen Aufträge von DSGVO. | ENV (**erforderlich**) |
| timeseries.gdpr.jobs.errorjobs.count | Gesamtanzahl der Fehleraufträge von DSGVO. | ENV (**erforderlich**) |

#### [!DNL Query Service] {#query}

The following table outlines metrics for Adobe Experience Platform [!DNL Query Service].

| Insight-Metrik | Beschreibung | ID-Abfrageparameter |
| ---- | ---- | ---- |
| timeseries.queryservice.query.scheduleonce.count | Gesamtanzahl der einmaligen geplanten Abfragen. | K. A. |
| timeseries.queryservice.query.scheduledrecurring.count | Gesamtanzahl der wiederkehrenden geplanten Abfragen. | K. A. |
| timeseries.queryservice.query.batchquery.count | Gesamtzahl der ausgeführten Batch-Abfragen. | K. A. |
| timeseries.queryservice.query.scheduledquery.count | Gesamtzahl der ausgeführten geplanten Abfragen. | K. A. |
| timeseries.queryservice.query.interactivequery.count | Gesamtanzahl der ausgeführten interaktiven Abfragen. | K. A. |
| timeseries.queryservice.query.batchfrompsqlquery.count | Gesamtzahl der ausgeführten Batch-Abfragen von PSQL. | K. A. |

#### [!DNL Real-time Customer Profile] {#profile}

The following table outlines metrics for [!DNL Real-time Customer Profile].

| Insight-Metrik | Beschreibung | ID-Abfrageparameter |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | Number of records read from the [!DNL Data Lake] by [!DNL Profile], for one dataset or for all datasets. | Datensatz-ID |
| timeseries.profiles.dataset.recordsuccess.count | Number of records written to their data source by [!DNL Profile], for one dataset or for all datasets. | Datensatz-ID |
| timeseries.profiles.dataset.recordfailed.count | Number of records failed by [!DNL Profile], for one dataset or for all datasets. | Datensatz-ID |
| timeseries.profiles.dataset.batchsuccess.count | Number of [!DNL Profile] batches ingested for a dataset or for all datasets. | Datensatz-ID |
| timeseries.profiles.dataset.batchfailed.count | Number of [!DNL Profile] batches failed for one dataset or for all datasets. | Datensatz-ID |
| platform.ups.ingest.streaming.request.m1_rate | Rate eingehender Anfragen. | IMS-Organisation (**Erforderlich**) |
| platform.ups.ingest.streaming.access.put.success.m1_rate | Erfolgsrate der Aufnahme. | IMS-Organisation (**Erforderlich**) |
| platform.ups.ingest.streaming.records.created.m15_rate | Rate der neuen Einträge, die für einen Datensatz erfasst werden. | Datensatz-ID (**Erforderlich**) |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | Rate von mit Zeitstempel versehenen und sich nicht in der Reihenfolge befindlichen Einträgen für die Erstellungsanfrage für einen Datensatz. | Datensatz-ID (**Erforderlich**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | Zeitstempel für die letzte Anfrage zur Eintragserstellung für einen Datensatz. | Datensatz-ID (**Erforderlich**) |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | Rate von mit Zeitstempel versehenen und sich nicht in der Reihenfolge befindlichen Einträgen für die Aktualisierungsanfrage für einen Datensatz. | Datensatz-ID (**Erforderlich**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | Zeitstempel für die letzte Anfrage zur Eintragsaktualisierung für einen Datensatz. | Datensatz-ID (**Erforderlich**) |
| platform.ups.ingest.streaming.record.size.m1_rate | Durchschnittliche Eintragsgröße. | IMS-Organisation (**Erforderlich**) |
| platform.ups.ingest.streaming.records.updated.m15_rate | Rate von Aktualisierungsanfragen für Einträge, die für einen Datensatz erfasst werden. | Datensatz-ID (**Erforderlich**) |