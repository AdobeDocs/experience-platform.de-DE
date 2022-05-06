---
keywords: Experience Platform; Entwicklerhandbuch; Endpunkt; Data Science Workspace; beliebte Themen; Instanzen; Sensei Machine Learning API
solution: Experience Platform
title: MLInstances API Endpoint
topic-legacy: Developer guide
description: Eine MLInstance ist eine Kopplung einer vorhandenen Engine mit einem entsprechenden Satz von Konfigurationen, die Trainings-Parameter, Scoring-Parameter oder Hardware-Ressourcenkonfigurationen definieren.
exl-id: e78cda69-1ff9-47ce-b25d-915de4633e11
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 19%

---

# MLInstances-Endpunkt

Eine MLInstance ist eine Kopplung eines vorhandenen [Engine](./engines.md) mit einem geeigneten Satz von Konfigurationen, die Trainings-Parameter, Scoring-Parameter oder Hardware-Ressourcenkonfigurationen definieren.

## Erstellen einer MLInstance {#create-an-mlinstance}

Sie können eine MLInstance erstellen, indem Sie eine POST-Anfrage ausführen und dabei eine Anfrage-Payload angeben, die aus einer gültigen Engine-ID (`{ENGINE_ID}`) und einen entsprechenden Satz von Standardkonfigurationen.

Wenn die Engine-ID auf eine PySpark- oder Spark-Engine verweist, können Sie die Anzahl der Berechnungsressourcen konfigurieren, z. B. die Anzahl der Kerne oder die Speichermenge. Wenn auf eine Python-Engine verwiesen wird, können Sie entweder eine CPU oder eine GPU zu Trainings- und Scoring-Zwecken verwenden. Weitere Informationen finden Sie im Anhang unter [PySpark- und Spark-Ressourcenkonfigurationen](./appendix.md#resource-config) und [Python-CPU- und GPU-Konfigurationen](./appendix.md#cpu-gpu-config) für weitere Informationen.

**API-Format**

```http
POST /mlInstances
```

**Anfrage**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/mlInstances \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -d '{
        "name": "A name for this MLInstance",
        "description": "A description for this MLInstance",
        "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
        "tasks": [
            {
                "name": "train",
                "parameters": [
                    {
                        "key": "training parameter",
                        "value": "parameter value"
                    }
                ]
            },
            {
                "name": "score",
                "parameters": [
                    {
                        "key": "scoring parameter",
                        "value": "parameter value"
                    }
                ]
            },
            {
                "name": "fp",
                "parameters": [
                    {
                        "key": "feature pipeline parameter",
                        "value": "parameter value"
                    }
                ]
            }
        ],
    }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der gewünschte Name für die MLInstance. Das Modell, das dieser MLInstance entspricht, übernimmt diesen Wert, der in der Benutzeroberfläche als Modellname angezeigt werden soll. |
| `description` | Eine optionale Beschreibung für die MLInstance. Das Modell, das dieser MLInstance entspricht, übernimmt diesen Wert, der in der Benutzeroberfläche als Beschreibung des Modells angezeigt werden soll. Diese Eigenschaft ist erforderlich. Wenn Sie keine Beschreibung angeben möchten, legen Sie als Wert eine leere Zeichenfolge fest. |
| `engineId` | Die Kennung einer vorhandenen Engine. |
| `tasks` | Ein Satz von Konfigurationen für Trainings-, Scoring- oder Feature-Pipelines. |

**Antwort**

Eine erfolgreiche Antwort gibt eine Payload zurück, die die Details der neu erstellten MLInstance einschließlich ihrer eindeutigen Kennung (`id`).

```json
{
    "id": "46986c8f-7739-4376-8509-0178bdf32cda",
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "training parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "scoring parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "fp",
            "parameters": [
                {
                    "key": "feature pipeline parameter",
                    "value": "parameter value"
                }
            ]
        }
    ]
}
```

## Abrufen einer Liste von MLInstances

Sie können eine Liste von MLInstances abrufen, indem Sie eine einzige GET-Anfrage ausführen. Sie können die Ergebnisse filtern, indem Sie im Anfragepfad Abfrageparameter angeben. Eine Liste der verfügbaren Abfragen finden Sie im Anhang zu den [Abfrageparametern für den Asset-Abruf](./appendix.md#query).

**API-Format**

```http
GET /mlInstances
GET /mlInstances?{QUERY_PARAMETER}={VALUE}
GET /mlInstances?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parameter | Beschreibung |
| --- | --- |
| `{QUERY_PARAMETER}` | Eines der [Verfügbare Abfrageparameter](./appendix.md#query) verwendet, um Ergebnisse zu filtern. |
| `{VALUE}` | Der Wert für den vorangehenden Abfrageparameter. |

**Anfrage**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlInstances \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von MLInstances und deren Details zurück.

```json
{
    "children": [
        {
            "id": "46986c8f-7739-4376-8509-0178bdf32cda",
            "name": "A name for this MLInstance",
            "description": "A description for this MLInstance",
            "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        },
        {
            "id": "56986c8f-7739-4376-8509-0178bdf32cda",
            "name": "Retail Sales Model",
            "description": "A Model created with the Retail Sales Recipe",
            "engineId": "32f4166f-85ba-4130-a995-a2b8e1edde32",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        }
    ],
    "_page": {
        "property": "deleted==false",
        "totalCount": 2,
        "count": 2
    }
}
```

## Abrufen einer bestimmten MLInstance {#retrieve-specific}

Sie können die Details einer bestimmten MLInstance abrufen, indem Sie eine GET-Anfrage ausführen, die die ID der gewünschten MLInstance im Anfragepfad enthält.

**API-Format**

```http
GET /mlInstances/{MLINSTANCE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{MLINSTANCE_ID}` | Die ID der gewünschten MLInstance. |

**Anfrage**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der MLInstance zurück.

```json
{
    "id": "46986c8f-7739-4376-8509-0178bdf32cda",
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "training parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "scoring parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "featurePipeline",
            "parameters": [
                {
                    "key": "feature pipeline parameter",
                    "value": "parameter value"
                }
            ]
        }
    ]
}
```

## Aktualisieren einer MLInstance

Sie können eine vorhandene MLInstance aktualisieren, indem Sie ihre Eigenschaften über eine PUT-Anfrage überschreiben, die die ID der Ziel-MLInstance im Anfragepfad enthält, und eine JSON-Payload mit aktualisierten Eigenschaften bereitstellen.

>[!TIP]
>
>Um den Erfolg dieser PUT-Anfrage sicherzustellen, wird empfohlen, zunächst eine GET-Anfrage an [Abrufen der MLInstance nach ID](#retrieve-specific). Ändern und aktualisieren Sie dann das zurückgegebene JSON-Objekt und übernehmen Sie die Gesamtheit des geänderten JSON-Objekts als Payload für die PUT-Anfrage.

Mit dem folgenden Beispiel-API-Aufruf werden die Trainings- und Scoring-Parameter einer MLInstance aktualisiert, während sie zunächst über diese Eigenschaften verfügen:

```json
{
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "00000000-0000-0000-0000-000000000000",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "learning_rate",
                    "value": "0.3"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "output_dataset_id",
                    "value": "output-dataset-000"
                }
            ]
        }
    ]
}
```

**API-Format**

```http
PUT /mlInstances/{MLINSTANCE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{MLINSTANCE_ID}` | Eine gültige MLInstance-ID. |

**Anfrage**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -d '{
        "name": "A name for this MLInstance",
        "description": "A description for this MLInstance",
        "engineId": "00000000-0000-0000-0000-000000000000",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "displayName": "Jane Doe",
            "userId": "Jane_Doe@AdobeID"
        },
        "tasks": [
            {
                "name": "train",
                "parameters": [
                    {
                        "key": "learning_rate",
                        "value": "0.5"
                    }
                ]
            },
            {
                "name": "score",
                "parameters": [
                    {
                        "key": "output_dataset_id",
                        "value": "output-dataset-001"
                    }
                ]
            }
        ]
    }'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Payload zurück, die die aktualisierten Details der MLInstance enthält.

```json
{
    "id": "46986c8f-7739-4376-8509-0178bdf32cda",
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "00000000-0000-0000-0000-000000000000",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "learning_rate",
                    "value": "0.5"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "output_dataset_id",
                    "value": "output-data-set-001"
                }
            ]
        }
    ]
}
```

## Löschen von MLInstances nach Engine ID

Sie können alle MLInstances, die dieselbe Engine verwenden, löschen, indem Sie eine DELETE-Anfrage ausführen, die die Engine-ID als Abfrageparameter enthält.

**API-Format**

```http
DELETE /mlInstances?engineId={ENGINE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{ENGINE_ID}` | Eine gültige Engine-ID. |

**Anfrage**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlInstances?engineId=22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "MLInstances successfully deleted"
}
```

## Löschen einer MLInstance

Sie können eine einzelne MLInstance löschen, indem Sie eine DELETE-Anfrage ausführen, die die ID der Ziel-MLInstance im Anfragepfad enthält.

**API-Format**

```http
DELETE /mlInstances/{MLINSTANCE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{MLINSTANCE_ID}` | Eine gültige MLInstance-ID. |

**Anfrage**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "MLInstance deletion was successful"
}
```
