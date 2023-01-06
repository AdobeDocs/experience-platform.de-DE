---
keywords: Experience Platform; Entwicklerhandbuch; Endpunkt; Data Science Workspace; beliebte Themen; Einblicke; Sensei Machine Learning API
solution: Experience Platform
title: Insights-API-Endpunkt
description: Insights bieten Metriken, mit denen Datenwissenschaftler durch Anzeige relevanter Bewertungsmetriken optimale ML-Modelle ermitteln und auswählen können.
exl-id: 603546d6-5686-4b59-99a7-90ecc0db8de3
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 96%

---

# Insights-Endpunkt

Insights bieten Metriken, mit denen Datenwissenschaftler durch Anzeige relevanter Bewertungsmetriken optimale ML-Modelle ermitteln und auswählen können.

## Liste mit Insights abrufen

Sie können eine Liste mit Insights abrufen, indem Sie eine GET-Anfrage an den Insights-Endpunkt richten.  Sie können die Ergebnisse filtern, indem Sie im Anfragepfad Abfrageparameter angeben. Eine Liste der verfügbaren Abfragen finden Sie im Anhang zu den [Abfrageparametern für den Asset-Abruf](./appendix.md#query).

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Payload zurück, die eine Liste mit Insights enthält, wobei jeder Insight eine eindeutige Kennung (`id`) aufweist. Darüber hinaus erhalten Sie `context` (Kontext), der die eindeutigen Kennungen enthält, die mit diesem bestimmten Insight verknüpft sind, gefolgt von den Insights-Ereignissen und Metrikdaten.

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
| `id` | Die Kennung, die dem Insight entspricht. |
| `experimentId` | Eine gültige Experiment-ID. |
| `experimentRunId` | Eine gültige Experimentablauf-ID. |
| `modelId` | Eine gültige Modellkennung. |

## Bestimmten Insight abrufen

Um einen bestimmten Insight nachzuschlagen, stellen Sie eine GET-Anfrage und geben Sie im Anfragepfad eine gültige `{INSIGHT_ID}` an. Sie können die Ergebnisse filtern, indem Sie im Anfragepfad Abfrageparameter angeben. Eine Liste der verfügbaren Abfragen finden Sie im Anhang zu den [Abfrageparametern für den Asset-Abruf](./appendix.md#query).

**API-Format**

```http
GET /insights/{INSIGHT_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{INSIGHT_ID}` | Die eindeutige Kennung eines Sensei-Insight. |

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/insights/08b8d174-6b0d-4d7e-acd8-1c4c908e14b2 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Payload zurück, die die eindeutige Kennung (`id`) des Insight umfasst. Darüber hinaus erhalten Sie `context` (Kontext), der die eindeutigen Kennungen enthält, die mit diesem bestimmten Insight verknüpft sind, gefolgt von den Insights-Ereignissen und Metrikdaten.

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
| `id` | Die Kennung, die dem Insight entspricht. |
| `experimentId` | Eine gültige Experiment-ID. |
| `experimentRunId` | Eine gültige Experimentablauf-ID. |
| `modelId` | Eine gültige Modellkennung. |

## Neuen Modell-Insight hinzufügen

Sie können einen neuen Modell-Insight erstellen, indem Sie eine POST-Anfrage und eine Payload ausführen, die Kontext, Ereignisse und Metriken für den neuen Modell-Insight bereitstellt. Das zum Erstellen eines neuen Modell-Insight verwendete Kontextfeld muss nicht mit vorhandenen Diensten verknüpft sein. Sie können den neuen Modell-Insight jedoch mit vorhandenen Diensten erstellen, indem Sie eine oder mehrere der entsprechenden Kennungen angeben:

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Eine erfolgreiche Antwort gibt eine Payload zurück, die über eine `{INSIGHT_ID}` und alle Parameter verfügt, die Sie in der ursprünglichen Anfrage angegeben haben.

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
| `insightId` | Die eindeutige Kennung, die für diesen speziellen Insight erstellt wird, wenn eine erfolgreiche POST-Anfrage ausgeführt wird. |

## Liste mit Standardmetriken für Algorithmen abrufen

Sie können eine Liste mit allen Ihren Algorithmen und Standardmetriken abrufen, indem Sie eine GET-Anfrage an den Metrikendpunkt richten. Zur Abfrage einer bestimmten Metrik stellen Sie eine GET-Anfrage und geben im Anfragepfad einen gültigen `{ALGORITHM}` an.

**API-Format**

```http
GET /insights/metrics
GET /insights/metrics?algorithm={ALGORITHM}
```

| Parameter | Beschreibung |
| --- | --- |
| `{ALGORITHM}` | Die Kennung des Algorithmustyps. |

**Anfrage**

Die folgende Anfrage enthält eine Abfrage und ruft mithilfe der Algorithmuskennung `{ALGORITHM}` eine spezifische Metrik ab.

```shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/insights/metrics?algorithm={ALGORITHM}' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Payload zurück, die die eindeutige Kennung des `algorithm` und eine Gruppe von Standardmetriken enthält.

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
