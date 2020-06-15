---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Insights
topic: Developer guide
translation-type: tm+mt
source-git-commit: 7bd6807e620febe134f8c75e67c0f723850e49c1
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 4%

---


# Insights

Statistiken enthalten Metriken, mit denen ein Datenwissenschaftler in die Lage versetzt wird, optimale ML-Modelle durch Anzeige relevanter Bewertungsmetriken zu bewerten und auszuwählen.

## Abrufen einer Liste von Insight

Sie können eine Insight-Liste abrufen, indem Sie eine GET-Anforderung an den Insight-Endpunkt ausführen.  Um die Ergebnisse zu filtern, können Sie die Parameter für die Abfrage im Anforderungspfad angeben. Eine Liste der verfügbaren Abfragen finden Sie im Anhang zu den [Abfrage-Parametern für den Asset-Abruf](./appendix.md#query).

**API-Format**

```http
GET /insights
```

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/insights \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Nutzlast zurück, die eine Liste von Erkenntnissen enthält und jeder Einblick einen eindeutigen Bezeichner enthält ( `id` ). Darüber hinaus erhalten Sie `context` die eindeutigen Bezeichner, die nach den Daten zu Insight-Ereignissen und -Metriken mit dieser speziellen Erkenntnis verknüpft sind.

```json
{
    "children": [
        {
            "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
            "context": {
                "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
                "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
                "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
            },
            "events": {
                "name": "fit",
                "eventValues": {
                    "algorithm": null,
                    "ratio": "0.8"
                }
            },
            "metrics": [
                {
                    "name": "MAPE",
                    "value": "0.0111111111111",
                    "valueType": "double"
                }
            ],
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-02T00:00:00.000Z"
        },
        {
            "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
            "context": {
                "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
                "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
                "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
            },
            "events": {
                "name": "fit",
                "eventValues": {
                    "algorithm": null,
                    "ratio": "0.8"
                }
            },
            "metrics": [
                {
                    "name": "MAPE",
                    "value": "0.0111111111111",
                    "valueType": "double"
                }
            ],
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-02T00:00:00.000Z"
            }
        ],
    "_page": {
        "count": 2
    }
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `id` | Die ID, die dem Insight entspricht. |
| `experimentId` | Eine gültige Experiment-ID. |
| `experimentRunId` | Eine gültige Experimentausführung-ID. |
| `modelId` | Eine gültige Modell-ID. |

## Abrufen eines bestimmten Insight

Um einen bestimmten Einblick nachzuschlagen, stellen Sie eine GET-Anforderung und geben Sie eine gültige Angabe `{INSIGHT_ID}` im Anforderungspfad ein. Um die Ergebnisse zu filtern, können Sie die Parameter für die Abfrage im Anforderungspfad angeben. Eine Liste der verfügbaren Abfragen finden Sie im Anhang zu den [Abfrage-Parametern für den Asset-Abruf](./appendix.md#query).

**API-Format**

```http
GET /insights/{INSIGHT_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{INSIGHT_ID}` | Die eindeutige Kennung eines Sensei Insight. |

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/insights/08b8d174-6b0d-4d7e-acd8-1c4c908e14b2 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Nutzlast zurück, die die eindeutige Erkennungskennung (`id`) enthält. Zusätzlich erhalten Sie `context` die eindeutigen Bezeichner, die mit den Insight-Ereignissen und Metrikdaten verknüpft sind.

```json
{
    "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
    "context": {
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
    },
    "events": {
        "name": "fit",
        "eventValues": {
            "algorithm": null,
            "ratio": "0.8"
        }
    },
    "metrics": [
        {
            "name": "MAPE",
            "value": "0.0111111111111",
            "valueType": "double"
        }
    ],
    "created": "2019-01-01T00:00:00.000Z",
    "updated": "2019-01-02T00:00:00.000Z"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `id` | Die ID, die dem Insight entspricht. |
| `experimentId` | Eine gültige Experiment-ID. |
| `experimentRunId` | Eine gültige Experimentausführung-ID. |
| `modelId` | Eine gültige Modell-ID. |

## Hinzufügen eines neuen Model Insight

Sie können einen neuen Modellinsight erstellen, indem Sie eine POST-Anforderung und eine Nutzlast ausführen, die Kontext, Ereignis und Metriken für den neuen Modellinsight bereitstellt. Das zum Erstellen eines neuen Modellinsight verwendete Kontextfeld muss nicht mit vorhandenen Diensten verknüpft sein. Sie können jedoch den neuen Modellinsight mit vorhandenen Diensten erstellen, indem Sie eine oder mehrere der entsprechenden IDs bereitstellen:

```json
"context": {
    "clientId": "f1ab3164-e688-433d-99ef-077b2be84731",
    "notebookId": "T4ab3164-e658-443d-97ef-022b2be84999",
    "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
    "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
    "dataSetId": "5ee3cd7f2d34011913c56941"
  }
```

**API-Format**

```http
POST /insights
```

**Anfrage**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/insights \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H `Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json`
    -d {
    "context": {
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
    },
    "events": {
        "name": "fit2",
        "eventValues": {
            "algorithm": null,
            "ratio": "0.99"
        }
    },
    "metrics": [
        {
            "name": "MAPE2",
            "value": "0.11111111111",
            "valueType": "double"
        }
    ],
    "created": "2019-01-01T00:00:00.000Z",
    "updated": "2019-01-02T00:00:00.000Z"
}
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Nutzlast zurück, die über einen Parameter `{INSIGHT_ID}` und alle Parameter verfügt, die Sie in der ursprünglichen Anforderung angegeben haben.

```json
{
    "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
    "context": {
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
    },
    "events": {
        "name": "fit2",
        "eventValues": {
            "algorithm": null,
            "ratio": "0.99"
        }
    },
    "metrics": [
        {
            "name": "MAPE2",
            "value": "0.11111111111",
            "valueType": "double"
        }
    ],
    "created": "2019-01-01T00:00:00.000Z",
    "updated": "2019-01-02T00:00:00.000Z"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `insightId` | Die eindeutige ID, die für diese spezielle Erkenntnis erstellt wird, wenn eine erfolgreiche POST-Anforderung ausgeführt wird. |

## Abrufen einer Liste von Standardmetriken für Algorithmen

Sie können eine Liste aller Algorithmus- und Standardmetriken abrufen, indem Sie eine GET-Anforderung an den Metrikendpunkt ausführen. Zur Abfrage einer bestimmten Metrik stellen Sie eine GET-Anforderung und geben Sie eine gültige `{ALGORITHM}` im Anforderungspfad an.

**API-Format**

```http
GET /insights/metrics
GET /insights/metrics?algorithm={ALGORITHM}
```

| Parameter | Beschreibung |
| --- | --- |
| `{ALGORITHM}` | Der Bezeichner des Algorithmustyps. |

**Anfrage**

Die folgende Anforderung enthält eine Abfrage und ruft mithilfe der Algorithmuskennung eine spezifische Metrik ab `{ALGORITHM}`

```shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/insights/metrics?algorithm={ALGORITHM}' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Nutzlast zurück, die den `algorithm` eindeutigen Bezeichner und ein Array von Standardmetriken enthält.

```json
{
    "children": [
        {
            "algorithm": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "defaultMetrics": [
                "f-score",
                "auroc",
                "roc",
                "precision",
                "recall",
                "accuracy",
                "confusion matrix"
            ]
        }
    ]
}
```
