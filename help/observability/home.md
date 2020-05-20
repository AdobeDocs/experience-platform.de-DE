---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Einblicke in die Adobe Experience Platform-Überwachung
topic: overview
translation-type: tm+mt
source-git-commit: d349ffab7c0de72d38b5195585c14a4a8f80e37c
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 2%

---


# Übersicht über die Beobachtbarkeit von Adobe Experience Platform

Observability Insights ist eine RESTful-API, mit der Sie wichtige Metriken zur Observability in Adobe Experience Platform bereitstellen können. Diese Metriken bieten Einblicke in die Statistiken zur Plattformnutzung, Gesundheitskontrollen für Plattformdienste, historische Trends und Leistungsindikatoren für verschiedene Plattformfunktionalitäten.

Dieses Dokument zeigt einen Beispielaufruf der Observability Insights-API. Eine vollständige Liste der Beobachtungs-Endpunkte finden Sie in der [Observability Insights-API-Referenz](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml).

## Erste Schritte

Um Aufrufe an Plattform-APIs durchzuführen, müssen Sie zunächst das [Authentifizierungstraining](../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungstreutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform API-Aufrufen bereit, wie unten dargestellt:

* Genehmigung: Träger `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in Experience Platform werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an Plattform-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird. Weitere Informationen zu Sandboxes in Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../sandboxes/home.md).

* x-sandbox-name: `{SANDBOX_NAME}`

## Abrufen von Beobachtungsmetriken

Sie können die Beobachtungsmetriken abrufen, indem Sie eine GET-Anforderung an den `/metrics` Endpunkt in der Observability Insights-API stellen.

**API-Format**

Bei Verwendung des `/metrics` Endpunkts muss mindestens ein Metrikanforderungsparameter angegeben werden. Andere Parameter für die Abfrage sind optional für Filterergebnisse.

```http
GET /metrics?metric={METRIC}
GET /metrics?metric={METRIC}&metric={METRIC_2}
GET /metrics?metric={METRIC}&id={ID}
GET /metrics?metric={METRIC}&dateRange={DATE_RANGE}
GET /metrics?metric={METRIC}&metric={METRIC_2}&id={ID}&dateRange={DATE_RANGE}
```

| Parameter | Beschreibung |
| --- | --- |
| `{METRIC}` | Die Metrik, die Sie bereitstellen möchten. Wenn Sie mehrere Metriken in einem einzelnen Aufruf kombinieren, müssen Sie ein kaufmännisches Und (`&`) verwenden, um einzelne Metriken zu trennen. Beispiel: `metric={METRIC_1}&metric={METRIC_2}`. |
| `{ID}` | Der Bezeichner für eine bestimmte Plattform-Ressource, deren Metriken Sie bereitstellen möchten. Diese ID kann optional, erforderlich oder je nach verwendeter Metrik nicht anwendbar sein. Eine Liste der verfügbaren Metriken sowie der unterstützten IDs (sowohl erforderlich als auch optional) für jede Metrik finden Sie im Referenz-Dokument zu den [verfügbaren Metriken](metrics.md). |
| `{DATE_RANGE}` | Der Datumsbereich für die Metriken, die Sie bereitstellen möchten, im ISO 8601-Format (z. B. `2018-10-01T07:00:00.000Z/2018-10-09T07:00:00.000Z`). |

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

Eine erfolgreiche Antwort gibt eine Liste von Objekten zurück, von denen jedes einen Zeitstempel innerhalb der angegebenen Werte `dateRange` und die entsprechenden Werte für die im Anforderungspfad angegebenen Metriken enthält. Wenn der Wert `id` einer Plattformressource im Anforderungspfad enthalten ist, gelten die Ergebnisse nur für diese bestimmte Ressource. Wenn der `id` Wert weggelassen wird, gelten die Ergebnisse für alle in Ihrer IMS-Organisation anwendbaren Ressourcen.

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

Dieses Dokument bietet einen Überblick über die Beobachtbarkeitseinblicke-API. Eine vollständige Liste der Metriken, die in der API verwendet werden können, finden Sie im Dokument zu [verfügbaren Metriken](metrics.md) .