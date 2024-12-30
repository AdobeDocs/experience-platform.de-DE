---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Metrics-API-Endpunkt
description: Erfahren Sie, wie Sie Observability-Metriken in Experience Platform mithilfe der Observability Insights-API abrufen.
exl-id: 08d416f0-305a-44e2-a2b7-d563b2bdd2d2
source-git-commit: bd5018a2d867d0483f3f2f0c45e356ea69a01801
workflow-type: tm+mt
source-wordcount: '1278'
ht-degree: 25%

---

# Metrik-Endpunkt

Observability-Metriken bieten Einblicke in Nutzungsstatistiken, historische Trends und Leistungsindikatoren für verschiedene Funktionen in Adobe Experience Platform. Mit dem `/metrics`-Endpunkt in der [!DNL Observability Insights API] können Sie programmgesteuert Metrikdaten für die Aktivität Ihrer Organisation in [!DNL Platform] abrufen.

>[!NOTE]
>
>Die vorherige Version des Metrik-Endpunkts (V1) wird nicht mehr unterstützt. Dieses Dokument bezieht sich ausschließlich auf die aktuelle Version (V2). Weitere Informationen zum V1-Endpunkt für ältere Implementierungen finden Sie in der [API-Referenz](https://www.adobe.io/experience-platform-apis/references/observability-insights/#operation/retrieveMetricsV1).

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil der [[!DNL Observability Insights] API](https://www.adobe.io/experience-platform-apis/references/observability-insights/). Bevor Sie fortfahren, lesen Sie im Handbuch [Erste Schritte](./getting-started.md) die Links zu entsprechenden Dokumentationen, den Leitfaden zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtige Informationen zu Kopfzeilen, die für das erfolgreiche Aufrufen einer [!DNL Experience Platform]-API erforderlich sind.

## Beobachtbarkeitsmetriken abrufen

Sie können Metrikdaten abrufen, indem Sie eine POST-Anfrage an den `/metrics`-Endpunkt stellen und dabei die Metriken angeben, die Sie in der Payload abrufen möchten.

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
  -H 'x-sandbox-id: {SANDBOX_ID}'
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
            "aggregator": "sum"
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
          }
        ]
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `start` | Das früheste Datum/die früheste Uhrzeit, ab dem/der die Metrikdaten abgerufen werden. |
| `end` | Das letzte Datum/die letzte Uhrzeit, ab dem/der die Metrikdaten abgerufen werden. |
| `granularity` | Ein optionales Feld, das das Zeitintervall angibt, nach dem Metrikdaten geteilt werden. Beispielsweise werden bei einem Wert von `DAY` Metriken für jeden Tag zwischen dem `start`- und `end` zurückgegeben, während bei einem Wert von `MONTH` die Metrikergebnisse stattdessen nach Monat gruppiert würden. |
| `metrics` | Ein Array von Objekten, eines für jede Metrik, die Sie abrufen möchten. |
| `name` | Der Name einer Metrik, die von Observability Insights erkannt wird. Eine vollständige Liste der ](#available-metrics) Metriknamen finden Sie im [Anhang“. |
| `filters` | Ein optionales Feld, mit dem Sie Metriken nach bestimmten Datensätzen filtern können. Das Feld ist ein Array von Objekten (eines für jeden Filter), wobei jedes Objekt die folgenden Eigenschaften enthält: <ul><li>`name`: Der Typ der Entität, nach der die Metriken gefiltert werden sollen. Derzeit wird nur `dataSets` unterstützt.</li><li>`value`: Die ID eines oder mehrerer Datensätze. Mehrere Datensatz-IDs können als einzelne Zeichenfolge bereitgestellt werden, wobei jede ID durch vertikale Balkenzeichen (`\|`) getrennt ist.</li><li>`groupBy`: Wenn auf „true“ gesetzt, bedeutet dies, dass die entsprechende `value` mehrere Datensätze darstellt, deren Metrikergebnisse separat zurückgegeben werden sollen. Wenn dies auf „false“ gesetzt ist, werden die Metrikergebnisse für diese Datensätze gruppiert.</li></ul> |
| `aggregator` | Gibt die Aggregationsfunktion an, die zum Gruppieren von Datensätzen mit mehreren Zeitreihen in einzelne Ergebnisse verwendet werden soll. Die aktuell unterstützten Aggregatoren sind Min., Max., Summe und Durchschnitt , je nach Definition der Metrik. |

{style="table-layout:auto"}

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
| `metricResponses` | Ein Array, dessen Objekte jede der in der Anfrage angegebenen Metriken darstellen. Jedes -Objekt enthält Informationen zur Filterkonfiguration und die zurückgegebenen Metrikdaten. |
| `metric` | Der Name einer der in der Anfrage angegebenen Metriken. |
| `filters` | Die Filterkonfiguration für die angegebene Metrik. |
| `datapoints` | Ein Array, dessen Objekte die Ergebnisse der angegebenen Metrik und Filter darstellen. Die Anzahl der Objekte im Array hängt von den in der Anfrage bereitgestellten Filteroptionen ab. Wenn keine Filter bereitgestellt wurden, enthält das -Array nur ein einzelnes -Objekt, das alle Datensätze darstellt. |
| `groupBy` | Wenn mehrere Datensätze in der `filter`-Eigenschaft für eine Metrik angegeben wurden und die `groupBy`-Option in der Anfrage auf „true“ gesetzt wurde, enthält dieses Objekt die ID des Datensatzes, für den die entsprechende `dps`-Eigenschaft gilt.<br><br>Wenn dieses Objekt in der Antwort leer erscheint, gilt die entsprechende `dps`-Eigenschaft für alle Datensätze, die im `filters`-Array bereitgestellt werden (oder für alle Datensätze in [!DNL Platform], wenn keine Filter bereitgestellt wurden). |
| `dps` | Die zurückgegebenen Daten für die angegebene Metrik, den angegebenen Filter und den angegebenen Zeitbereich. Jeder Schlüssel in diesem Objekt stellt einen Zeitstempel mit einem entsprechenden Wert für die angegebene Metrik dar. Der Zeitraum zwischen den einzelnen Datenpunkten hängt vom in der Anfrage angegebenen `granularity` ab. |

{style="table-layout:auto"}

## Anhang

Der folgende Abschnitt enthält zusätzliche Informationen zum Arbeiten mit dem `/metrics`-Endpunkt.

### Verfügbare Metriken {#available-metrics}

In der folgenden Tabelle sind alle Metriken aufgelistet, die nach [!DNL Observability Insights] verfügbar gemacht werden, aufgeschlüsselt nach [!DNL Platform] Service. Jede Metrik enthält eine Beschreibung und einen akzeptierten ID-Abfrageparameter.

>[!NOTE]
>
>Alle aufgelisteten ID-Abfrageparameter sind optional, sofern nicht anders angegeben.

#### [!DNL Data Ingestion] {#ingestion}

In der folgenden Tabelle sind Metriken für Adobe Experience Platform [!DNL Data Ingestion] aufgeführt. Metriken in **Fettdruck** sind Streaming-Erfassungsmetriken.

| Insights-Metrik | Beschreibung | ID-Abfrageparameter |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.size | Kumulative Größe aller Daten, die für einen Datensatz oder für alle Datensätze erfasst werden. | Datensatz-ID |
| timeseries.ingestion.dataset.dailysize | Größe der Daten, die täglich für einen Datensatz oder für alle Datensätze erfasst werden. | Datensatz-ID |
| timeseries.ingestion.dataset.batchfailed.count | Anzahl der fehlgeschlagenen Batches für einen Datensatz oder für alle Datensätze. | Datensatz-ID |
| timeseries.ingestion.dataset.batchsuccess.count | Anzahl der erfassten Batches für einen Datensatz oder für alle Datensätze. | Datensatz-ID |
| timeseries.ingestion.dataset.recordsuccess.count | Anzahl der erfassten Einträge für einen Datensatz oder für alle Datensätze. | Datensatz-ID |
| **timeseries.data.collection.validation.category.presence.count** | Gesamtanzahl ungültiger Meldungen vom Typ „Präsenz“ für einen Datensatz oder für alle Datensätze. | Datensatz-ID |
| **timeseries.data.collection.inlet.total.messages.received** | Gesamtzahl der Meldungen, die für einen Daten-Inlet oder für alle Daten-Inlets empfangen wurden. | Eintritts-ID |
| **timeseries.data.collection.inlet.total.messages.size.received** | Gesamtgröße der Daten, die für einen Daten-Inlet oder für alle Daten-Inlets empfangen wurden. | Eintritts-ID |
| **timeseries.data.collection.inlet.success** | Gesamtzahl erfolgreicher HTTP-Aufrufe an einen Daten-Inlet oder an alle Daten-Inlets. | Eintritts-ID |
| **timeseries.data.collection.inlet.failure** | Gesamtzahl fehlgeschlagener HTTP-Aufrufe an einen Daten-Inlet oder an alle Daten-Inlets. | Eintritts-ID |

{style="table-layout:auto"}

#### [!DNL Identity Service] {#identity}

In der folgenden Tabelle sind Metriken für Adobe Experience Platform [!DNL Identity Service] aufgeführt.

| Insights-Metrik | Beschreibung | ID-Abfrageparameter |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | Anzahl der Datensätze, die von [!DNL Identity Service] in ihre Datenquelle geschrieben wurden, für einen Datensatz oder alle Datensätze. | Datensatz-ID |
| timeseries.identity.dataset.recordfailed.count | Anzahl von fehlgeschlagenen Datensätzen nach [!DNL Identity Service], für einen Datensatz oder für alle Datensätze. | Datensatz-ID |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Anzahl übersprungener Identitätseinträge. | Organisations-ID |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Anzahl der eindeutigen Identitäten, die im Identitätsdiagramm für Ihre Organisation gespeichert sind. | K. A. |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Anzahl der eindeutigen Identitäten, die im Identitätsdiagramm für einen Namespace gespeichert sind. | Namespace-ID (**erforderlich**) |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Anzahl der eindeutigen Identitäten, die im Identitätsdiagramm für Ihre Organisation für eine bestimmte Diagrammstärke gespeichert sind („unbekannt“, „schwach“ oder „stark„). | Diagrammstärke (**erforderlich**) |

{style="table-layout:auto"}

#### [!DNL Real-Time Customer Profile] {#profile}

In der folgenden Tabelle sind Metriken für [!DNL Real-Time Customer Profile] aufgeführt.

| Insights-Metrik | Beschreibung | ID-Abfrageparameter |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | Anzahl der von [!DNL Profile] aus dem [!DNL Data Lake] gelesenen Datensätze für einen Datensatz oder für alle Datensätze. | Datensatz-ID |
| timeseries.profiles.dataset.recordsuccess.count | Anzahl der Datensätze, die für einen Datensatz oder für alle Datensätze [!DNL Profile] in die Datenquelle geschrieben wurden. | Datensatz-ID |
| timeseries.profiles.dataset.batchsuccess.count | Anzahl der [!DNL Profile] Batches, die für einen Datensatz oder für alle Datensätze aufgenommen wurden. | Datensatz-ID |

{style="table-layout:auto"}

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
| `title` | Eine Zeichenfolge, die die Fehlermeldung und den möglichen Grund für das Auftreten enthält. |
| `report` | Enthält kontextuelle Informationen zum Fehler, einschließlich der Sandbox und der Organisation, die in dem Vorgang verwendet werden, der ihn ausgelöst hat. |

{style="table-layout:auto"}

In der folgenden Tabelle sind die verschiedenen Fehler-Codes aufgeführt, die von der API zurückgegeben werden können:

| Fehler-Code | Titel | Beschreibung |
| --- | --- | --- |
| `INSGHT-1000-400` | Fehlerhafte Anfrage - Payload | Bei der Anfrage-Payload ist ein Fehler aufgetreten. Stellen Sie sicher, dass Sie die Payload-Formatierung genau wie [oben) ](#v2). Jeder der möglichen Gründe kann diesen Trigger verursachen:<ul><li>Erforderliche Felder wie `aggregator` fehlen</li><li>Invalid metrics</li><li>Die Anfrage enthält einen ungültigen Aggregator</li><li>Ein Startdatum liegt hinter einem Enddatum</li></ul> |
| `INSGHT-1001-400` | Metrikabfrage fehlgeschlagen | Beim Versuch, die Metrikdatenbank abzufragen, ist ein Fehler aufgetreten, da eine fehlerhafte Anfrage vorliegt oder die Abfrage selbst nicht parsierbar ist. Vergewissern Sie sich, dass Ihre Anfrage ordnungsgemäß formatiert ist, bevor Sie es erneut versuchen. |
| `INSGHT-1001-500` | Metrikabfrage fehlgeschlagen | Beim Versuch, die Metrikdatenbank abzufragen, ist aufgrund eines Server-Fehlers ein Fehler aufgetreten. Wiederholen Sie die Anfrage. Wenn das Problem weiterhin besteht, wenden Sie sich an den Adobe-Support. |
| `INSGHT-1002-500` | Service-Fehler | Die Anfrage konnte aufgrund eines internen Fehlers nicht verarbeitet werden. Wiederholen Sie die Anfrage. Wenn das Problem weiterhin besteht, wenden Sie sich an den Adobe-Support. |
| `INSGHT-1003-401` | Sandbox-Validierungsfehler | Die Anfrage konnte aufgrund eines Sandbox-Validierungsfehlers nicht verarbeitet werden. Stellen Sie sicher, dass der in der `x-sandbox-name`-Kopfzeile angegebene Sandbox-Name eine gültige, aktivierte Sandbox für Ihre Organisation darstellt, bevor Sie die Anfrage erneut versuchen. |

{style="table-layout:auto"}
