---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Metrik-API-Endpunkt
description: Erfahren Sie, wie Sie mithilfe der Observability Insights-API Beobachtbarkeitsmetriken in Experience Platform abrufen.
exl-id: 08d416f0-305a-44e2-a2b7-d563b2bdd2d2
source-git-commit: bd5018a2d867d0483f3f2f0c45e356ea69a01801
workflow-type: tm+mt
source-wordcount: '1278'
ht-degree: 25%

---

# Endpunkt &quot;Metriken&quot;

Beobachtbarkeitsmetriken bieten Einblicke in Nutzungsstatistiken, historische Trends und Leistungsindikatoren für verschiedene Funktionen in Adobe Experience Platform. Mit dem `/metrics` -Endpunkt im [!DNL Observability Insights API] können Sie Metrikdaten für die Aktivität Ihres Unternehmens in [!DNL Platform] programmgesteuert abrufen.

>[!NOTE]
>
>Die vorherige Version des Metrik-Endpunkts (V1) wird nicht mehr unterstützt. Dieses Dokument konzentriert sich ausschließlich auf die aktuelle Version (V2). Weitere Informationen zum V1-Endpunkt für ältere Implementierungen finden Sie in der [API-Referenz](https://www.adobe.io/experience-platform-apis/references/observability-insights/#operation/retrieveMetricsV1).

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil der [[!DNL Observability Insights] API](https://www.adobe.io/experience-platform-apis/references/observability-insights/). Bevor Sie fortfahren, lesen Sie im Handbuch [Erste Schritte](./getting-started.md) die Links zu entsprechenden Dokumentationen, den Leitfaden zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtige Informationen zu Kopfzeilen, die für das erfolgreiche Aufrufen einer [!DNL Experience Platform]-API erforderlich sind.

## Beobachtbarkeitsmetriken abrufen

Sie können Metrikdaten abrufen, indem Sie eine POST-Anfrage an den `/metrics` -Endpunkt senden und die Metriken angeben, die Sie in der Payload abrufen möchten.

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
| `start` | Das früheste Datum/die früheste Uhrzeit, ab dem/der Metrikdaten abgerufen werden sollen. |
| `end` | Das aktuelle Datum/die aktuelle Uhrzeit, ab dem/der Metrikdaten abgerufen werden sollen. |
| `granularity` | Ein optionales Feld, das das Zeitintervall angibt, nach dem die Metrikdaten geteilt werden sollen. Beispielsweise gibt der Wert `DAY` Metriken für jeden Tag zwischen dem Datum `start` und dem Datum `end` zurück, während der Wert `MONTH` die Metrikergebnisse stattdessen nach Monat gruppiert. |
| `metrics` | Ein Array von Objekten, eines für jede Metrik, die Sie abrufen möchten. |
| `name` | Der Name einer Metrik, die von Observability Insights erkannt wird. Eine vollständige Liste der akzeptierten Metriknamen finden Sie im [Anhang](#available-metrics) . |
| `filters` | Ein optionales Feld, mit dem Sie Metriken nach bestimmten Datensätzen filtern können. Das Feld ist ein Array von Objekten (eines für jeden Filter), wobei jedes Objekt die folgenden Eigenschaften enthält: <ul><li>`name`: Der Typ der Entität, nach der Metriken gefiltert werden sollen. Derzeit wird nur `dataSets` unterstützt.</li><li>`value`: Die ID eines oder mehrerer Datensätze. Es können mehrere Datensatz-IDs als einzelne Zeichenfolge angegeben werden, wobei jede ID durch vertikale Balkenzeichen (`\|`) getrennt ist.</li><li>`groupBy`: Gibt bei Festlegung auf &quot;true&quot;an, dass der entsprechende `value` mehrere Datensätze darstellt, deren Metrikergebnisse separat zurückgegeben werden sollen. Wenn der Wert auf &quot;false&quot;gesetzt ist, werden die Metrikergebnisse für diese Datensätze gruppiert.</li></ul> |
| `aggregator` | Gibt die Aggregationsfunktion an, die zum Gruppieren mehrerer Datensätze aus Zeitreihen zu einzelnen Ergebnissen verwendet werden soll. Die derzeit unterstützten Aggregatoren sind &quot;min&quot;, &quot;max&quot;, &quot;sum&quot;und &quot;avg&quot;, je nach Definition der Metrik. |

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
| `metricResponses` | Ein Array, dessen Objekte jede der in der Anfrage angegebenen Metriken darstellen. Jedes Objekt enthält Informationen zur Filterkonfiguration und die zurückgegebenen Metrikdaten. |
| `metric` | Der Name einer der in der Anfrage angegebenen Metriken. |
| `filters` | Die Filterkonfiguration für die angegebene Metrik. |
| `datapoints` | Ein Array, dessen Objekte die Ergebnisse der angegebenen Metrik und Filter darstellen. Die Anzahl der Objekte im Array hängt von den in der Anfrage angegebenen Filteroptionen ab. Wenn keine Filter angegeben wurden, enthält das Array nur ein einzelnes Objekt, das alle Datensätze darstellt. |
| `groupBy` | Wenn mehrere Datensätze in der Eigenschaft `filter` für eine Metrik angegeben wurden und die Option `groupBy` in der Anfrage auf &quot;true&quot;gesetzt wurde, enthält dieses Objekt die ID des Datensatzes, für den die entsprechende Eigenschaft `dps` gilt.<br><br>Wenn dieses Objekt in der Antwort leer angezeigt wird, gilt die entsprechende `dps` -Eigenschaft für alle im `filters` -Array bereitgestellten Datensätze (oder für alle Datensätze in [!DNL Platform] , wenn keine Filter bereitgestellt wurden). |
| `dps` | Die zurückgegebenen Daten für die angegebene Metrik, den Filter und den Zeitraum. Jeder Schlüssel in diesem Objekt stellt einen Zeitstempel mit einem entsprechenden Wert für die angegebene Metrik dar. Der Zeitraum zwischen den einzelnen Datenpunkten hängt vom in der Anfrage angegebenen `granularity` -Wert ab. |

{style="table-layout:auto"}

## Anhang

Der folgende Abschnitt enthält zusätzliche Informationen zum Arbeiten mit dem `/metrics` -Endpunkt.

### Verfügbare Metriken {#available-metrics}

In den folgenden Tabellen sind alle Metriken aufgeführt, die durch den Dienst [!DNL Observability Insights] bereitgestellt werden, aufgeschlüsselt nach dem Dienst [!DNL Platform]. Jede Metrik enthält eine Beschreibung und einen akzeptierten ID-Abfrageparameter.

>[!NOTE]
>
>Alle aufgelisteten ID-Abfrageparameter sind optional, sofern nicht anders angegeben.

#### [!DNL Data Ingestion] {#ingestion}

In der folgenden Tabelle sind die Metriken für Adobe Experience Platform [!DNL Data Ingestion] aufgeführt. Metriken in **Fettdruck** sind Streaming-Erfassungsmetriken.

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

In der folgenden Tabelle sind die Metriken für Adobe Experience Platform [!DNL Identity Service] aufgeführt.

| Insights-Metrik | Beschreibung | ID-Abfrageparameter |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | Anzahl der Einträge, die für einen Datensatz oder alle Datensätze von [!DNL Identity Service] in ihre Datenquelle geschrieben wurden. | Datensatz-ID |
| timeseries.identity.dataset.recordfailed.count | Anzahl der fehlgeschlagenen Einträge von [!DNL Identity Service], für einen Datensatz oder für alle Datensätze. | Datensatz-ID |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Anzahl der übersprungenen Identitätsdatensätze. | Organisations-ID |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Anzahl der eindeutigen Identitäten, die im Identitätsdiagramm für Ihre Organisation gespeichert sind. | K. A. |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Anzahl der eindeutigen Identitäten, die im Identitätsdiagramm für einen Namespace gespeichert sind. | Namespace-ID (**erforderlich**) |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Anzahl der eindeutigen Identitäten, die im Identitätsdiagramm für Ihre Organisation für eine bestimmte Diagrammstärke (&quot;unbekannt&quot;, &quot;schwach&quot;oder &quot;stark&quot;) gespeichert sind. | Diagrammstärke (**erforderlich**) |

{style="table-layout:auto"}

#### [!DNL Real-Time Customer Profile] {#profile}

In der folgenden Tabelle sind die Metriken für [!DNL Real-Time Customer Profile] aufgeführt.

| Insights-Metrik | Beschreibung | ID-Abfrageparameter |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | Anzahl der Einträge, die für einen Datensatz oder für alle Datensätze aus dem [!DNL Data Lake] von [!DNL Profile] gelesen wurden. | Datensatz-ID |
| timeseries.profiles.dataset.recordsuccess.count | Anzahl der Einträge, die von [!DNL Profile] für einen Datensatz oder für alle Datensätze in ihre Datenquelle geschrieben wurden. | Datensatz-ID |
| timeseries.profiles.dataset.batchsuccess.count | Anzahl der [!DNL Profile] Batches, die für einen Datensatz oder für alle Datensätze erfasst werden. | Datensatz-ID |

{style="table-layout:auto"}

### Fehlermeldungen

Antworten vom `/metrics` -Endpunkt können unter bestimmten Bedingungen Fehlermeldungen zurückgeben. Diese Fehlermeldungen werden im folgenden Format zurückgegeben:

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
| `report` | Enthält Kontextdaten zum Fehler, einschließlich der Sandbox und der Organisation, die in dem Vorgang verwendet werden, der den Fehler ausgelöst hat. |

{style="table-layout:auto"}

In der folgenden Tabelle sind die verschiedenen Fehlercodes aufgeführt, die von der API zurückgegeben werden können:

| Fehler-Code | Titel | Beschreibung |
| --- | --- | --- |
| `INSGHT-1000-400` | Schlechte Anfrage-Payload | Mit der Anfrage-Payload ist etwas nicht in Ordnung. Stellen Sie sicher, dass Sie die Payload-Formatierung genau wie in [über](#v2) angezeigt haben. Dieser Fehler kann aus allen möglichen Gründen Trigger werden:<ul><li>Fehlende erforderliche Felder wie `aggregator`</li><li>Ungültige Metriken</li><li>Die Anfrage enthält einen ungültigen Aggregator</li><li>Ein Startdatum liegt nach dem Enddatum</li></ul> |
| `INSGHT-1001-400` | Metrikabfrage fehlgeschlagen | Beim Versuch, die Metrikdatenbank abzufragen, trat ein Fehler auf, da eine ungültige Anforderung oder die Abfrage selbst nicht analysierbar war. Stellen Sie sicher, dass Ihre Anforderung korrekt formatiert ist, bevor Sie es erneut versuchen. |
| `INSGHT-1001-500` | Metrikabfrage fehlgeschlagen | Beim Versuch, die Metrikdatenbank abzufragen, trat aufgrund eines Serverfehlers ein Fehler auf. Versuchen Sie die Anfrage erneut. Wenn das Problem weiterhin besteht, wenden Sie sich an den Adobe-Support. |
| `INSGHT-1002-500` | Service-Fehler | Die Anfrage konnte aufgrund eines internen Fehlers nicht verarbeitet werden. Versuchen Sie die Anfrage erneut. Wenn das Problem weiterhin besteht, wenden Sie sich an den Adobe-Support. |
| `INSGHT-1003-401` | Sandbox-Validierungsfehler | Die Anfrage konnte aufgrund eines Sandbox-Validierungsfehlers nicht verarbeitet werden. Stellen Sie sicher, dass der Sandbox-Name, den Sie in der Kopfzeile `x-sandbox-name` angegeben haben, eine gültige, aktivierte Sandbox für Ihre Organisation darstellt, bevor Sie die Anfrage erneut ausführen. |

{style="table-layout:auto"}
