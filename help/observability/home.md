---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Observability Insights
topic: overview
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 68%

---


# Übersicht über Adobe Experience Platform Observability Insights

Observability Insights ist eine RESTful-API, mit der Sie wichtige Beobachtbarkeitsmetriken in Adobe Experience Platform bereitstellen können. These metrics provide insights into [!DNL Platform] usage statistics, health-checks for [!DNL Platform] services, historical trends, and performance indicators for various [!DNL Platform] functionalities.

Dieses Dokument demonstriert einen Beispielaufruf an die Observability Insights-API. Eine vollständige Liste der Observability-Endpunkte finden Sie in der [Referenz zur Observability Insights-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml).

## Erste Schritte

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in. For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../sandboxes/home.md).

* x-sandbox-name: `{SANDBOX_NAME}`

## Beobachtbarkeitsmetriken abrufen

Sie können Beobachtbarkeitsmetriken abrufen, indem Sie in der Observability Insights-API eine GET-Anfrage an den `/metrics`-Endpunkt richten.

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
| `{ID}` | The identifier for a particular [!DNL Platform] resource whose metrics you want to expose. Diese Kennung kann je nach verwendeter Metrik optional, erforderlich oder nicht anwendbar sein. Eine Liste der verfügbaren Metriken sowie der unterstützten Kennungen für jede Metrik (sowohl erforderlich als auch optional) finden Sie im Referenzdokument zu [verfügbaren Metriken](metrics.md). |
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

## Nächste Schritte

Dieses Dokument bietet einen Überblick über die Observability Insights-API. Eine vollständige Liste der Metriken, die in der API verwendet werden können, finden Sie im Dokument zu [verfügbaren Metriken](metrics.md).