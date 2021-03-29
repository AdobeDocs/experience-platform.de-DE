---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Metrik-API-Endpunkt
topic: Entwicklerhandbuch
description: Erfahren Sie, wie Sie mithilfe der Observability Insights API in Experience Platform beobachtbare Metriken abrufen.
translation-type: tm+mt
source-git-commit: 136c75f56c2ba4d61fef7981ff8a7889a0ade3d1
workflow-type: tm+mt
source-wordcount: '2056'
ht-degree: 40%

---


# Metrik-Endpunkt

Beobachtungsmetriken bieten Einblicke in Nutzungsstatistiken, historische Trends und Leistungsindikatoren für verschiedene Funktionen in Adobe Experience Platform. Mit dem `/metrics`-Endpunkt in [!DNL Observability Insights API] können Sie Metrikdaten für die Aktivität Ihres Unternehmens in [!DNL Platform] programmgesteuert abrufen.

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil der [[!DNL Observability Insights] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml). Bevor Sie fortfahren, lesen Sie bitte im Handbuch [Erste Schritte](./getting-started.md) nach Links zu entsprechenden Dokumentationen, einem Leitfaden zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtigen Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen einer [!DNL Experience Platform]-API erforderlich sind.

## Beobachtbarkeitsmetriken abrufen

Es gibt zwei unterstützte Methoden zum Abrufen von Metrikdaten mit der API:

* [Version 1](#v1): Geben Sie Metriken mithilfe von Abfragen-Parametern an.
* [Version 2](#v2): Geben Sie mithilfe einer JSON-Nutzlast Filter an und wenden Sie sie auf Metriken an.

### Version 1 {#v1}

Sie können Metrikdaten abrufen, indem Sie eine GET an den `/metrics`-Endpunkt senden und Metriken mithilfe von Abfragen-Parametern angeben.

**API-Format**

Mindestens eine Metrik muss im Parameter `metric` angegeben werden. Andere Abfrageparameter dienen optional zum Filtern von Ergebnissen.

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
| `{ID}` | Der Bezeichner für eine bestimmte [!DNL Platform]-Ressource, deren Metriken Sie bereitstellen möchten. Diese Kennung kann je nach verwendeter Metrik optional, erforderlich oder nicht anwendbar sein. Eine Liste der verfügbaren Metriken, einschließlich der unterstützten IDs (sowohl erforderlich als auch optional) für jede Metrik finden Sie im Anhang [.](#available-metrics) |
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

Eine erfolgreiche Antwort gibt eine Liste von Objekten zurück, jeweils mit einem Zeitstempel innerhalb des angegebenen `dateRange` und den entsprechenden Werten für die im Anfragepfad angegebenen Metriken. Wenn `id` einer [!DNL Platform]-Ressource im Anforderungspfad enthalten ist, gelten die Ergebnisse nur für diese bestimmte Ressource. Wenn die `id` weggelassen wird, gelten die Ergebnisse für alle anwendbaren Ressourcen in Ihrer IMS-Organisation.

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

### Version 2 {#v2}

Sie können Metrikdaten abrufen, indem Sie eine POST an den `/metrics`-Endpunkt anfordern und die Metriken angeben, die Sie in der Nutzlast abrufen möchten.

**API-Format**

```http
POST /metrics
```

**Anfrage**

```sh
curl -X POST \
  https://platform.adobe.io/data/infrastructure/observability/insights/metrics \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "start": "2020-07-14T00:00:00.000Z",
        "end": "2020-07-22T00:00:00.000Z",
        "granularity": "day",
        "metrics": [
          {
            "name": "timeseries.ingestion.dataset.recordsuccess.count",
            "filters": [
              {
                "name": "dataSetId",
                "value": "5edcfb2fbb642119194c7d94|5eddb21420f516191b7a8dad",
                "groupBy": true
              }
            ],
            "aggregator": "sum",
            "downsample": "sum"
          },
          {
            "name": "timeseries.ingestion.dataset.dailysize",
            "filters": [
              {
                "name": "dataSetId",
                "value": "5eddb21420f516191b7a8dad",
                "groupBy": false
              }
            ],
            "aggregator": "sum",
            "downsample": "sum"
          }
        ]
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `start` | Das früheste Datum/die früheste Uhrzeit, ab der Metrikdaten abgerufen werden. |
| `end` | Das aktuelle Datum/die Uhrzeit, ab dem Metrikdaten abgerufen werden. |
| `granularity` | Ein optionales Feld, das das Zeitintervall angibt, nach dem die Metrikdaten dividiert werden sollen. Beispielsweise gibt der Wert `DAY` Metriken für jeden Tag zwischen dem `start`- und dem `end`-Datum zurück, während bei einem Wert von `MONTH` die Metrikergebnisse stattdessen nach Monat gruppiert werden. Bei Verwendung dieses Felds muss auch eine entsprechende `downsample`-Eigenschaft angegeben werden, mit welcher Aggregationsfunktion Daten gruppiert werden. |
| `metrics` | Ein Array von Objekten, eines für jede abzurufende Metrik. |
| `name` | Der Name einer Metrik, die von Observability Insights erkannt wird. Eine vollständige Liste der zulässigen Metriknamen finden Sie im Anhang [.](#available-metrics) |
| `filters` | Ein optionales Feld, mit dem Sie Metriken nach bestimmten Datensätzen filtern können. Das Feld ist ein Array von Objekten (eines für jeden Filter), wobei jedes Objekt die folgenden Eigenschaften enthält: <ul><li>`name`: Der Typ der Entität, nach der Metriken gefiltert werden sollen. Derzeit wird nur `dataSets` unterstützt.</li><li>`value`: Die ID eines oder mehrerer Datensätze. Es können mehrere Datenset-IDs als einzelne Zeichenfolge angegeben werden, wobei jede ID durch vertikale Balkenzeichen (`|`) getrennt wird.</li><li>`groupBy`: Wenn &quot;true&quot;festgelegt ist, gibt dies an, dass die entsprechenden Datensätze mehrere Datensätze  `value` darstellen, deren Metrikergebnisse separat zurückgegeben werden sollten. Bei der Einstellung false werden die Metrikergebnisse für diese Datensätze gruppiert.</li></ul> |
| `aggregator` | Gibt die Aggregationsfunktion an, die zum Gruppieren von Datensätzen mit mehreren Serien zu einzelnen Ergebnissen verwendet werden soll. Ausführliche Informationen zu verfügbaren Aggregatoren finden Sie in der [OpenTSDB-Dokumentation](http://opentsdb.net/docs/build/html/user_guide/query/aggregators.html). |
| `downsample` | Ein optionales Feld, mit dem Sie eine Aggregationsfunktion angeben können, um die Abtastrate von Metrikdaten zu reduzieren, indem Sie Felder in Intervalle (oder &quot;Behälter&quot;) sortieren. Das Intervall für die Neuberechnung wird durch die `granularity`-Eigenschaft bestimmt. Ausführliche Informationen zum Downsampling finden Sie in der [OpenTSDB-Dokumentation](http://opentsdb.net/docs/build/html/user_guide/query/downsampling.html). |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die resultierenden Datenpunkte für die in der Anforderung angegebenen Metriken und Filter zurück.

```json
{
  "metricResponses": [
    {
      "metric": "timeseries.ingestion.dataset.recordsuccess.count",
      "filters": [
        {
          "name": "dataSetId",
          "value": "5edcfb2fbb642119194c7d94|5eddb21420f516191b7a8dad",
          "groupBy": true
        }
      ],
      "datapoints": [
        {
          "groupBy": {
            "dataSetId": "5edcfb2fbb642119194c7d94"
          },
          "dps": {
            "2020-07-14T00:00:00Z": 44.0,
            "2020-07-15T00:00:00Z": 46.0,
            "2020-07-16T00:00:00Z": 36.0,
            "2020-07-17T00:00:00Z": 50.0,
            "2020-07-18T00:00:00Z": 38.0,
            "2020-07-19T00:00:00Z": 40.0,
            "2020-07-20T00:00:00Z": 42.0,
            "2020-07-21T00:00:00Z": 42.0,
            "2020-07-22T00:00:00Z": 50.0
          }
        },
        {
          "groupBy": {
            "dataSetId": "5eddb21420f516191b7a8dad"
          },
          "dps": {
            "2020-07-14T00:00:00Z": 44.0,
            "2020-07-15T00:00:00Z": 46.0,
            "2020-07-16T00:00:00Z": 36.0,
            "2020-07-17T00:00:00Z": 50.0,
            "2020-07-18T00:00:00Z": 38.0,
            "2020-07-19T00:00:00Z": 40.0,
            "2020-07-20T00:00:00Z": 42.0,
            "2020-07-21T00:00:00Z": 42.0,
            "2020-07-22T00:00:00Z": 50.0
          }
        }
      ],
      "granularity": "DAY"
    },
    {
      "metric": "timeseries.ingestion.dataset.dailysize",
      "filters": [
        {
          "name": "dataSetId",
          "value": "5eddb21420f516191b7a8dad",
          "groupBy": false
        }
      ],
      "datapoints": [
        {
          "groupBy": {},
          "dps": {
            "2020-07-14T00:00:00Z": 38455.0,
            "2020-07-15T00:00:00Z": 40213.0,
            "2020-07-16T00:00:00Z": 31476.0,
            "2020-07-17T00:00:00Z": 43705.0,
            "2020-07-18T00:00:00Z": 33227.0,
            "2020-07-19T00:00:00Z": 34977.0,
            "2020-07-20T00:00:00Z": 36735.0,
            "2020-07-21T00:00:00Z": 36737.0,
            "2020-07-22T00:00:00Z": 43715.0
          }
        }
      ],
      "granularity": "DAY"
    }
  ]
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `metricResponses` | Ein Array, dessen Objekte jede der in der Anforderung angegebenen Metriken darstellen. Jedes Objekt enthält Informationen zur Filterkonfiguration und zurückgegebene Metrikdaten. |
| `metric` | Der Name einer der in der Anforderung bereitgestellten Metriken. |
| `filters` | Die Filterkonfiguration für die angegebene Metrik. |
| `datapoints` | Ein Array, dessen Objekte die Ergebnisse der angegebenen Metrik und der angegebenen Filter darstellen. Die Anzahl der Objekte im Array hängt von den Filteroptionen ab, die in der Anforderung bereitgestellt werden. Wenn keine Filter angegeben wurden, enthält das Array nur ein einzelnes Objekt, das alle Datensätze darstellt. |
| `groupBy` | Wenn mehrere Datensätze in der `filter`-Eigenschaft für eine Metrik angegeben wurden und die `groupBy`-Option in der Anforderung auf &quot;true&quot;gesetzt wurde, enthält dieses Objekt die ID des Datensatzes, für das die entsprechende `dps`-Eigenschaft gilt.<br><br>Wenn dieses Objekt in der Antwort leer angezeigt wird, gilt die entsprechende  `dps` Eigenschaft für alle im  `filters` Array bereitgestellten Datensätze (bzw. für alle Datensätze, in denen  [!DNL Platform] keine Filter angegeben wurden). |
| `dps` | Die zurückgegebenen Daten für die angegebene Metrik, den Filter und den Zeitraum. Jeder Schlüssel in diesem Objekt stellt einen Zeitstempel mit einem entsprechenden Wert für die angegebene Metrik dar. Der Zeitraum zwischen den einzelnen Datenpunkten hängt vom `granularity`-Wert ab, der in der Anforderung angegeben ist. |

{style=&quot;table-layout:auto&quot;}

## Anhang

Der folgende Abschnitt enthält weitere Informationen zum Arbeiten mit dem `/metrics`-Endpunkt.

### Verfügbare Metriken {#available-metrics}

In den folgenden Tabellen werden alle Metriken Liste, die von [!DNL Observability Insights] bereitgestellt werden, aufgeschlüsselt nach [!DNL Platform]-Dienst. Jede Metrik enthält eine Beschreibung und einen akzeptierten ID-Abfrageparameter.

>[!NOTE]
>
>Alle aufgelisteten ID-Abfragen sind optional, sofern nicht anders angegeben.

#### [!DNL Data Ingestion] {#ingestion}

In der folgenden Tabelle sind die Metriken für Adobe Experience Platform [!DNL Data Ingestion] aufgeführt. Metriken in **Fettdruck** sind Streaming-Erfassungsmetriken.

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

{style=&quot;table-layout:auto&quot;}

#### [!DNL Identity Service] {#identity}

In der folgenden Tabelle sind die Metriken für Adobe Experience Platform [!DNL Identity Service] aufgeführt.

| Insight-Metrik | Beschreibung | ID-Abfrageparameter |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | Anzahl der Datensätze, die von [!DNL Identity Service] für einen Datensatz oder alle Datensätze in ihre Datenquelle geschrieben wurden. | Datensatz-ID |
| timeseries.identity.dataset.recordfailed.count | Anzahl der Datensätze fehlgeschlagen von [!DNL Identity Service], für einen Datensatz oder für alle Datensätze. | Datensatz-ID |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | Anzahl der Identitätseinträge, die für einen Namespace erfolgreich erfasst wurden. | Namespace-ID (**erforderlich**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | Anzahl der Identitätseinträge, die aufgrund eines Namespace fehlgeschlagen sind. | Namespace-ID (**erforderlich**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Anzahl der Identitätseinträge, die von einem Namespace übersprungen wurden. | Namespace-ID (**erforderlich**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Anzahl der eindeutigen Identitäten, die im Identitätsdiagramm für Ihre IMS-Organisation gespeichert sind. | K. A. |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Anzahl der eindeutigen Identitäten, die im Identitätsdiagramm für einen Namespace gespeichert sind. | Namespace-ID (**erforderlich**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | Anzahl der eindeutigen Diagrammidentitäten, die im Identitätsdiagramm für Ihre IMS-Organisation gespeichert sind. | K. A. |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Anzahl der eindeutigen Identitäten, die im Identitätsdiagramm für Ihre IMS-Organisation für eine bestimmte Diagrammstärke („unbekannt“, „schwach oder „stark“) gespeichert sind. | Diagrammstärke (**erforderlich**) |

{style=&quot;table-layout:auto&quot;}

#### [!DNL Privacy Service] {#privacy}

In der folgenden Tabelle sind die Metriken für Adobe Experience Platform [!DNL Privacy Service] aufgeführt.

| Insight-Metrik | Beschreibung | ID-Abfrageparameter |
| ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | Gesamtzahl der erstellten Aufträge von DSGVO. | ENV (**erforderlich**) |
| timeseries.gdpr.jobs.completedjobs.count | Gesamtzahl der abgeschlossenen Aufträge von DSGVO. | ENV (**erforderlich**) |
| timeseries.gdpr.jobs.errorjobs.count | Gesamtanzahl der Fehleraufträge von DSGVO. | ENV (**erforderlich**) |

{style=&quot;table-layout:auto&quot;}

#### [!DNL Query Service] {#query}

In der folgenden Tabelle sind die Metriken für Adobe Experience Platform [!DNL Query Service] aufgeführt.

| Insight-Metrik | Beschreibung | ID-Abfrageparameter |
| ---- | ---- | ---- |
| timeseries.queryservice.query.scheduleonce.count | Gesamtanzahl der einmaligen geplanten Abfragen. | K. A. |
| timeseries.queryservice.query.scheduledrecurring.count | Gesamtanzahl der wiederkehrenden geplanten Abfragen. | K. A. |
| timeseries.queryservice.query.batchquery.count | Gesamtzahl der ausgeführten Batch-Abfragen. | K. A. |
| timeseries.queryservice.query.scheduledquery.count | Gesamtzahl der ausgeführten geplanten Abfragen. | K. A. |
| timeseries.queryservice.query.interactivequery.count | Gesamtanzahl der ausgeführten interaktiven Abfragen. | K. A. |
| timeseries.queryservice.query.batchfrompsqlquery.count | Gesamtzahl der ausgeführten Batch-Abfragen von PSQL. | K. A. |

{style=&quot;table-layout:auto&quot;}

#### [!DNL Real-time Customer Profile] {#profile}

In der folgenden Tabelle sind die Metriken für [!DNL Real-time Customer Profile] aufgeführt.

| Insight-Metrik | Beschreibung | ID-Abfrageparameter |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | Anzahl der Datensätze, die von [!DNL Data Lake] von [!DNL Profile], für einen Datensatz oder für alle Datensätze gelesen werden. | Datensatz-ID |
| timeseries.profiles.dataset.recordsuccess.count | Anzahl der Datensätze, die von [!DNL Profile], für einen Datensatz oder für alle Datensätze in ihre Datenquelle geschrieben wurden. | Datensatz-ID |
| timeseries.profiles.dataset.recordfailed.count | Anzahl der Datensätze fehlgeschlagen von [!DNL Profile], für einen Datensatz oder für alle Datensätze. | Datensatz-ID |
| timeseries.profiles.dataset.batchsuccess.count | Anzahl der für einen Datensatz oder für alle Datensätze erfassten [!DNL Profile]-Stapel. | Datensatz-ID |
| timeseries.profiles.dataset.batchfailed.count | Anzahl der [!DNL Profile]-Stapel bei einem Datensatz oder bei allen Datensätzen fehlgeschlagen. | Datensatz-ID |
| platform.ups.ingest.streaming.request.m1_rate | Rate eingehender Anfragen. | IMS-Organisation (**Erforderlich**) |
| platform.ups.ingest.streaming.access.put.success.m1_rate | Erfolgsrate der Aufnahme. | IMS-Organisation (**Erforderlich**) |
| platform.ups.ingest.streaming.records.created.m15_rate | Rate der neuen Einträge, die für einen Datensatz erfasst werden. | Datensatz-ID (**Erforderlich**) |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | Rate von mit Zeitstempel versehenen und sich nicht in der Reihenfolge befindlichen Einträgen für die Erstellungsanfrage für einen Datensatz. | Datensatz-ID (**Erforderlich**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | Zeitstempel für die letzte Anfrage zur Eintragserstellung für einen Datensatz. | Datensatz-ID (**Erforderlich**) |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | Rate von mit Zeitstempel versehenen und sich nicht in der Reihenfolge befindlichen Einträgen für die Aktualisierungsanfrage für einen Datensatz. | Datensatz-ID (**Erforderlich**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | Zeitstempel für die letzte Anfrage zur Eintragsaktualisierung für einen Datensatz. | Datensatz-ID (**Erforderlich**) |
| platform.ups.ingest.streaming.record.size.m1_rate | Durchschnittliche Eintragsgröße. | IMS-Organisation (**Erforderlich**) |
| platform.ups.ingest.streaming.records.updated.m15_rate | Rate von Aktualisierungsanfragen für Einträge, die für einen Datensatz erfasst werden. | Datensatz-ID (**Erforderlich**) |

{style=&quot;table-layout:auto&quot;}

### Fehlermeldungen

Antworten vom `/metrics`-Endpunkt können unter bestimmten Bedingungen Fehlermeldungen zurückgeben. Diese Fehlermeldungen werden im folgenden Format zurückgegeben:

```json
{
    "type": "http://ns.adobe.com/aep/errors/INSGHT-1000-400",
    "title": "Bad Request - Start date cannot be after end date.",
    "status": 400,
    "report": {
        "tenantInfo": {
            "sandboxName": "prod",
            "sandboxId": "49f58060-5d47-34rd-aawf-a5384333ff12",
            "imsOrgId": "{IMS_ORG}"
        },
        "additionalContext": null
    },
    "error-chain": [
        {
            "serviceId": "INSGHT",
            "errorCode": "INSGHT-1000-400",
            "invokingServiceId": "INSGHT",
            "unixTimeStampMs": 1602095177129
        }
    ]
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `title` | Eine Zeichenfolge, die die Fehlermeldung und den potenziellen Grund für den Fehler enthält. |
| `report` | Enthält Kontextinformationen zum Fehler, einschließlich der Sandbox und des IMS-Orgs, die bei dem Vorgang verwendet werden, der ihn ausgelöst hat. |

{style=&quot;table-layout:auto&quot;}

In der folgenden Tabelle werden die verschiedenen Fehlercodes Liste, die von der API zurückgegeben werden können:

| Fehler-Code | Titel | Beschreibung |
| --- | --- | --- |
| `INSGHT-1000-400` | Fehlerhafte Anforderungs-Nutzlast | Irgendetwas stimmt nicht mit der Anforderungs-Nutzlast. Stellen Sie sicher, dass Sie die Payload-Formatierung genau wie [über](#v2) einhalten. Dieser Fehler kann auf eine der folgenden Ursachen Trigger haben:<ul><li>Fehlende erforderliche Felder wie `aggregator`</li><li>Ungültige Metriken</li><li>Die Anforderung enthält einen ungültigen Aggregator</li><li>Ein Beginn-Datum findet nach einem Enddatum statt</li></ul> |
| `INSGHT-1001-400` | Abfrage von Metriken fehlgeschlagen | Beim Versuch, die Metrikendatenbank Abfrage, ist ein Fehler aufgetreten, da eine fehlerhafte Anforderung oder die Abfrage selbst nicht zu partikelbar war. Vergewissern Sie sich, dass Ihre Anforderung korrekt formatiert ist, bevor Sie es erneut versuchen. |
| `INSGHT-1001-500` | Abfrage von Metriken fehlgeschlagen | Beim Versuch, die Metrikdatenbank Abfrage, ist aufgrund eines Serverfehlers ein Fehler aufgetreten. Versuchen Sie es erneut, und wenn das Problem weiterhin besteht, wenden Sie sich an den Support der Adobe. |
| `INSGHT-1002-500` | Dienstfehler | Die Anforderung konnte aufgrund eines internen Fehlers nicht verarbeitet werden. Versuchen Sie es erneut, und wenn das Problem weiterhin besteht, wenden Sie sich an den Support der Adobe. |
| `INSGHT-1003-401` | Sandbox-Überprüfungsfehler | Die Anforderung konnte aufgrund eines Sandbox-Validierungsfehlers nicht verarbeitet werden. Stellen Sie sicher, dass der im Header `x-sandbox-name` angegebene Sandbox-Name eine gültige, aktivierte Sandbox für Ihre IMS-Organisation darstellt, bevor Sie die Anforderung erneut versuchen. |

{style=&quot;table-layout:auto&quot;}
