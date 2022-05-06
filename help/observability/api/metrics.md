---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Metrik-API-Endpunkt
topic-legacy: developer guide
description: Erfahren Sie, wie Sie Beobachtbarkeitsmetriken in Experience Platform mithilfe der Observability Insights-API abrufen.
exl-id: 08d416f0-305a-44e2-a2b7-d563b2bdd2d2
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1864'
ht-degree: 42%

---

# Endpunkt &quot;Metriken&quot;

Beobachtbarkeitsmetriken bieten Einblicke in Nutzungsstatistiken, historische Trends und Leistungsindikatoren für verschiedene Funktionen in Adobe Experience Platform. Die `/metrics` -Endpunkt im [!DNL Observability Insights API] ermöglicht Ihnen das programmgesteuerte Abrufen von Metrikdaten für die Aktivität Ihres Unternehmens in [!DNL Platform].

>[!NOTE]
>
>Die vorherige Version des Metrik-Endpunkts (V1) wird nicht mehr unterstützt. Dieses Dokument konzentriert sich ausschließlich auf die aktuelle Version (V2). Weitere Informationen zum V1-Endpunkt für ältere Implementierungen finden Sie im Abschnitt [API-Referenz](https://www.adobe.io/experience-platform-apis/references/observability-insights/#operation/retrieveMetricsV1).

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil der [[!DNL Observability Insights] API](https://www.adobe.io/experience-platform-apis/references/observability-insights/). Bevor Sie fortfahren, lesen Sie im Handbuch [Erste Schritte](./getting-started.md) die Links zu entsprechenden Dokumentationen, den Leitfaden zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtige Informationen zu Kopfzeilen, die für das erfolgreiche Aufrufen einer [!DNL Experience Platform]-API erforderlich sind.

## Beobachtbarkeitsmetriken abrufen

Sie können Metrikdaten abrufen, indem Sie eine POST-Anfrage an die `/metrics` -Endpunkt, der die Metriken angibt, die Sie in der Payload abrufen möchten.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `start` | Das früheste Datum/die früheste Uhrzeit, ab dem/der Metrikdaten abgerufen werden sollen. |
| `end` | Das aktuelle Datum/die aktuelle Uhrzeit, ab dem/der Metrikdaten abgerufen werden sollen. |
| `granularity` | Ein optionales Feld, das das Zeitintervall angibt, nach dem die Metrikdaten geteilt werden sollen. Beispielsweise wird der Wert `DAY` gibt Metriken für jeden Tag zwischen `start` und `end` Datum, während der Wert `MONTH` würde die Metrikergebnisse stattdessen nach Monat gruppieren. Bei Verwendung dieses Felds muss die `downsample` -Eigenschaft muss auch angegeben werden, mit welcher Aggregationsfunktion Daten gruppiert werden sollen. |
| `metrics` | Ein Array von Objekten, eines für jede Metrik, die Sie abrufen möchten. |
| `name` | Der Name einer Metrik, die von Observability Insights erkannt wird. Siehe [Anhang](#available-metrics) für eine vollständige Liste der akzeptierten Metriknamen. |
| `filters` | Ein optionales Feld, mit dem Sie Metriken nach bestimmten Datensätzen filtern können. Das Feld ist ein Array von Objekten (eines für jeden Filter), wobei jedes Objekt die folgenden Eigenschaften enthält: <ul><li>`name`: Der Typ der Entität, nach der Metriken gefiltert werden sollen. Derzeit wird nur `dataSets` unterstützt.</li><li>`value`: Die ID eines oder mehrerer Datensätze. Mehrere Datensatz-IDs können als einzelne Zeichenfolge angegeben werden, wobei jede ID durch vertikale Balkenzeichen (`\|`).</li><li>`groupBy`: Wenn auf &quot;true&quot;gesetzt, zeigt an, dass die entsprechende `value` stellt mehrere Datensätze dar, deren Metrikergebnisse separat zurückgegeben werden sollten. Wenn der Wert auf &quot;false&quot;gesetzt ist, werden die Metrikergebnisse für diese Datensätze gruppiert.</li></ul> |
| `aggregator` | Gibt die Aggregationsfunktion an, die zum Gruppieren mehrerer Datensätze aus Zeitreihen zu einzelnen Ergebnissen verwendet werden soll. Detaillierte Informationen zu den verfügbaren Aggregatoren finden Sie im Abschnitt [OpenTSDB-Dokumentation](https://docs.w3cub.com/opentsdb/user_guide/query/aggregators). |
| `downsample` | Ein optionales Feld, mit dem Sie eine Aggregationsfunktion angeben können, um die Sampling-Rate von Metrikdaten zu reduzieren, indem Sie Felder in Intervalle (oder &quot;Behälter&quot;) sortieren. Das Intervall für die Neuberechnung wird durch die `granularity` -Eigenschaft. Ausführliche Informationen zum Downsampling finden Sie im Abschnitt [OpenTSDB-Dokumentation](https://docs.w3cub.com/opentsdb/user_guide/query/aggregators). |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die resultierenden Datenpunkte für die in der Anfrage angegebenen Metriken und Filter zurück.

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
| `metricResponses` | Ein Array, dessen Objekte jede der in der Anfrage angegebenen Metriken darstellen. Jedes Objekt enthält Informationen zur Filterkonfiguration und die zurückgegebenen Metrikdaten. |
| `metric` | Der Name einer der in der Anfrage angegebenen Metriken. |
| `filters` | Die Filterkonfiguration für die angegebene Metrik. |
| `datapoints` | Ein Array, dessen Objekte die Ergebnisse der angegebenen Metrik und Filter darstellen. Die Anzahl der Objekte im Array hängt von den in der Anfrage angegebenen Filteroptionen ab. Wenn keine Filter angegeben wurden, enthält das Array nur ein einzelnes Objekt, das alle Datensätze darstellt. |
| `groupBy` | Wenn mehrere Datensätze im `filter` -Eigenschaft für eine Metrik und die `groupBy` in der Anfrage auf true festgelegt wurde, enthält dieses Objekt die Kennung des Datensatzes, zu dem die entsprechende `dps` -Eigenschaft gilt für .<br><br>Wenn dieses Objekt in der Antwort leer erscheint, wird die entsprechende `dps` -Eigenschaft gilt für alle Datensätze, die im `filters` Array (oder alle Datensätze in [!DNL Platform] , wenn keine Filter angegeben wurden). |
| `dps` | Die zurückgegebenen Daten für die angegebene Metrik, den Filter und den Zeitraum. Jeder Schlüssel in diesem Objekt stellt einen Zeitstempel mit einem entsprechenden Wert für die angegebene Metrik dar. Der Zeitraum zwischen den einzelnen Datenpunkten hängt von der `granularity` -Wert, der in der Anfrage angegeben ist. |

{style=&quot;table-layout:auto&quot;}

## Anhang

Im folgenden Abschnitt finden Sie weitere Informationen zum Arbeiten mit der `/metrics` -Endpunkt.

### Verfügbare Metriken {#available-metrics}

In den folgenden Tabellen sind alle Metriken aufgeführt, die durch [!DNL Observability Insights], aufgeschlüsselt nach [!DNL Platform] Dienst. Jede Metrik enthält eine Beschreibung und einen akzeptierten ID-Abfrageparameter.

>[!NOTE]
>
>Alle aufgelisteten ID-Abfrageparameter sind optional, sofern nicht anders angegeben.

#### [!DNL Data Ingestion] {#ingestion}

In der folgenden Tabelle sind die Metriken für Adobe Experience Platform aufgeführt [!DNL Data Ingestion]. Metriken in **Fettdruck** sind Streaming-Erfassungsmetriken.

| Insights-Metrik | Beschreibung | ID-Abfrageparameter |
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

In der folgenden Tabelle sind die Metriken für Adobe Experience Platform aufgeführt [!DNL Identity Service].

| Insights-Metrik | Beschreibung | ID-Abfrageparameter |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | Anzahl der in ihre Datenquelle geschriebenen Datensätze nach [!DNL Identity Service], für einen Datensatz oder alle Datensätze. | Datensatz-ID |
| timeseries.identity.dataset.recordfailed.count | Anzahl fehlgeschlagener Datensätze nach [!DNL Identity Service], für einen Datensatz oder für alle Datensätze. | Datensatz-ID |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | Anzahl der Identitätseinträge, die für einen Namespace erfolgreich erfasst wurden. | Namespace-ID (**erforderlich**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | Anzahl der Identitätseinträge, die aufgrund eines Namespace fehlgeschlagen sind. | Namespace-ID (**erforderlich**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Anzahl der Identitätseinträge, die von einem Namespace übersprungen wurden. | Namespace-ID (**erforderlich**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Anzahl der eindeutigen Identitäten, die im Identitätsdiagramm für Ihre IMS-Organisation gespeichert sind. | K. A. |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Anzahl der eindeutigen Identitäten, die im Identitätsdiagramm für einen Namespace gespeichert sind. | Namespace-ID (**erforderlich**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | Anzahl der eindeutigen Diagrammidentitäten, die im Identitätsdiagramm für Ihre IMS-Organisation gespeichert sind. | K. A. |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Anzahl der eindeutigen Identitäten, die im Identitätsdiagramm für Ihre IMS-Organisation für eine bestimmte Diagrammstärke („unbekannt“, „schwach oder „stark“) gespeichert sind. | Diagrammstärke (**erforderlich**) |

{style=&quot;table-layout:auto&quot;}

#### [!DNL Privacy Service] {#privacy}

In der folgenden Tabelle sind die Metriken für Adobe Experience Platform aufgeführt [!DNL Privacy Service].

| Insights-Metrik | Beschreibung | ID-Abfrageparameter |
| ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | Gesamtzahl der erstellten Aufträge von DSGVO. | ENV (**erforderlich**) |
| timeseries.gdpr.jobs.completedjobs.count | Gesamtzahl der abgeschlossenen Aufträge von DSGVO. | ENV (**erforderlich**) |
| timeseries.gdpr.jobs.errorjobs.count | Gesamtanzahl der Fehleraufträge von DSGVO. | ENV (**erforderlich**) |

{style=&quot;table-layout:auto&quot;}

#### [!DNL Query Service] {#query}

In der folgenden Tabelle sind die Metriken für Adobe Experience Platform aufgeführt [!DNL Query Service].

| Insights-Metrik | Beschreibung | ID-Abfrageparameter |
| ---- | ---- | ---- |
| timeseries.queryservice.query.scheduleonce.count | Gesamtanzahl der einmaligen geplanten Abfragen. | K. A. |
| timeseries.queryservice.query.scheduledrecurring.count | Gesamtanzahl der wiederkehrenden geplanten Abfragen. | K. A. |
| timeseries.queryservice.query.batchquery.count | Gesamtzahl der ausgeführten Batch-Abfragen. | K. A. |
| timeseries.queryservice.query.scheduledquery.count | Gesamtzahl der ausgeführten geplanten Abfragen. | K. A. |
| timeseries.queryservice.query.interactivequery.count | Gesamtanzahl der ausgeführten interaktiven Abfragen. | K. A. |
| timeseries.queryservice.query.batchfrompsqlquery.count | Gesamtzahl der ausgeführten Batch-Abfragen von PSQL. | K. A. |

{style=&quot;table-layout:auto&quot;}

#### [!DNL Real-time Customer Profile] {#profile}

In der folgenden Tabelle sind die Metriken für [!DNL Real-time Customer Profile].

| Insights-Metrik | Beschreibung | ID-Abfrageparameter |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | Anzahl der aus der Variablen [!DNL Data Lake] von [!DNL Profile], für einen Datensatz oder für alle Datensätze. | Datensatz-ID |
| timeseries.profiles.dataset.recordsuccess.count | Anzahl der in ihre Datenquelle geschriebenen Datensätze nach [!DNL Profile], für einen Datensatz oder für alle Datensätze. | Datensatz-ID |
| timeseries.profiles.dataset.recordfailed.count | Anzahl fehlgeschlagener Datensätze nach [!DNL Profile], für einen Datensatz oder für alle Datensätze. | Datensatz-ID |
| timeseries.profiles.dataset.batchsuccess.count | Anzahl der [!DNL Profile] Batches, die für einen Datensatz oder für alle Datensätze erfasst werden. | Datensatz-ID |
| timeseries.profiles.dataset.batchfailed.count | Anzahl der [!DNL Profile] Batches schlugen für einen Datensatz oder für alle Datensätze fehl. | Datensatz-ID |
| platform.ups.ingest.streaming.request.m1_rate | Rate eingehender Anfragen. | IMS-Organisation (**Erforderlich**) |
| aep.core.unified-profile.psi.platform.ups.ingest.streaming.access.put.success.meter.m1_rate | Erfolgsrate der Aufnahme. | IMS-Organisation (**Erforderlich**) |
| platform.ups.ingest.streaming.records.created.m15_rate | Rate der neuen Einträge, die für einen Datensatz erfasst werden. | Datensatz-ID (**Erforderlich**) |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | Rate von mit Zeitstempel versehenen und sich nicht in der Reihenfolge befindlichen Einträgen für die Erstellungsanfrage für einen Datensatz. | Datensatz-ID (**Erforderlich**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | Zeitstempel für die letzte Anfrage zur Eintragserstellung für einen Datensatz. | Datensatz-ID (**Erforderlich**) |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | Rate von mit Zeitstempel versehenen und sich nicht in der Reihenfolge befindlichen Einträgen für die Aktualisierungsanfrage für einen Datensatz. | Datensatz-ID (**Erforderlich**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | Zeitstempel für die letzte Anfrage zur Eintragsaktualisierung für einen Datensatz. | Datensatz-ID (**Erforderlich**) |
| platform.ups.ingest.streaming.record.size.m1_rate | Durchschnittliche Eintragsgröße. | IMS-Organisation (**Erforderlich**) |
| platform.ups.ingest.streaming.records.updated.m15_rate | Rate von Aktualisierungsanfragen für Einträge, die für einen Datensatz erfasst werden. | Datensatz-ID (**Erforderlich**) |

{style=&quot;table-layout:auto&quot;}

### Fehlermeldungen

Antworten von `/metrics` Endpunkt kann unter bestimmten Bedingungen Fehlermeldungen zurückgeben. Diese Fehlermeldungen werden im folgenden Format zurückgegeben:

```json
{
    "type": "http://ns.adobe.com/aep/errors/INSGHT-1000-400",
    "title": "Bad Request - Start date cannot be after end date.",
    "status": 400,
    "report": {
        "tenantInfo": {
            "sandboxName": "prod",
            "sandboxId": "49f58060-5d47-34rd-aawf-a5384333ff12",
            "imsOrgId": "{ORG_ID}"
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
| `title` | Eine Zeichenfolge, die die Fehlermeldung und den möglichen Grund für den Fehler enthält. |
| `report` | Enthält Kontextdaten zum Fehler, einschließlich der Sandbox und der IMS-Organisation, die in dem Vorgang verwendet werden, der den Fehler ausgelöst hat. |

{style=&quot;table-layout:auto&quot;}

In der folgenden Tabelle sind die verschiedenen Fehlercodes aufgeführt, die von der API zurückgegeben werden können:

| Fehler-Code | Titel | Beschreibung |
| --- | --- | --- |
| `INSGHT-1000-400` | Schlechte Anfrage-Payload | Mit der Anfrage-Payload ist etwas nicht in Ordnung. Stellen Sie sicher, dass Sie die Payload-Formatierung genau wie folgt einhalten [above](#v2). Dieser Fehler kann aus allen möglichen Gründen Trigger werden:<ul><li>Erforderliche Felder fehlen, z. B. `aggregator`</li><li>Ungültige Metriken</li><li>Die Anfrage enthält einen ungültigen Aggregator</li><li>Ein Startdatum liegt nach dem Enddatum</li></ul> |
| `INSGHT-1001-400` | Metrikabfrage fehlgeschlagen | Beim Versuch, die Metrikdatenbank abzufragen, trat ein Fehler auf, da eine ungültige Anforderung oder die Abfrage selbst nicht analysierbar war. Stellen Sie sicher, dass Ihre Anforderung korrekt formatiert ist, bevor Sie es erneut versuchen. |
| `INSGHT-1001-500` | Metrikabfrage fehlgeschlagen | Beim Versuch, die Metrikdatenbank abzufragen, trat aufgrund eines Serverfehlers ein Fehler auf. Versuchen Sie es erneut. Wenn das Problem weiterhin auftritt, wenden Sie sich an den Support von Adobe. |
| `INSGHT-1002-500` | Dienstfehler | Die Anfrage konnte aufgrund eines internen Fehlers nicht verarbeitet werden. Versuchen Sie es erneut. Wenn das Problem weiterhin auftritt, wenden Sie sich an den Support von Adobe. |
| `INSGHT-1003-401` | Sandbox-Validierungsfehler | Die Anfrage konnte aufgrund eines Sandbox-Validierungsfehlers nicht verarbeitet werden. Stellen Sie sicher, dass der Sandbox-Name, den Sie im `x-sandbox-name` -Kopfzeile stellt eine gültige, aktivierte Sandbox für Ihre IMS-Organisation dar, bevor Sie die Anfrage erneut ausführen. |

{style=&quot;table-layout:auto&quot;}
