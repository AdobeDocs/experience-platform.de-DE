---
keywords: Experience Platform; Entwicklerhandbuch; Endpunkt; Data Science Workspace; beliebte Themen; Experimente; Sensei Machine Learning-API
solution: Experience Platform
title: API-Endpunkt für Experimente
description: Die Modellentwicklung und das Training erfolgen auf Experimentebene, wo ein Experiment aus einer MLI-Instanz, Trainings-Läufen und Scoring-Läufen besteht.
role: Developer
exl-id: 6ca5106e-896d-4c03-aecc-344632d5307d
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 17%

---

# Experiments-Endpunkt

>[!NOTE]
>
>Data Science Workspace ist nicht mehr erhältlich.
>
>Diese Dokumentation richtet sich an Bestandskunden mit vorherigen Berechtigungen für Data Science Workspace.

Die Modellentwicklung und das Training erfolgen auf Experimentebene, wo ein Experiment aus einer MLI-Instanz, Trainings-Läufen und Scoring-Läufen besteht.

## Erstellen eines Experiments {#create-an-experiment}

Sie können ein Experiment erstellen, indem Sie eine POST-Anfrage ausführen und dabei einen Namen und eine gültige MLInstance-ID in der Anfrage-Payload angeben.

>[!NOTE]
>
>Im Gegensatz zum Modell-Training in der Benutzeroberfläche wird beim Erstellen eines Experiments über einen expliziten API-Aufruf nicht automatisch ein Trainings-Durchgang erstellt und ausgeführt.

**API-Format**

```http
POST /experiments
```

**Anfrage**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/experiments \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
    -d '{
        "name": "a name for this Experiment",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda"
    }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der gewünschte Name für das Experiment. Der Trainings-Lauf, der diesem Experiment entspricht, übernimmt diesen Wert, der in der Benutzeroberfläche als Name des Trainings-Laufs angezeigt wird. |
| `mlInstanceId` | Eine gültige MLInstance-ID. |

**Antwort**

Bei einer erfolgreichen Antwort wird eine Payload zurückgegeben, die die Details des neu erstellten Experiments einschließlich der eindeutigen Kennung (`id`) enthält.

```json
{
    "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "name": "A name for this Experiment",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## Erstellen und Ausführen eines Trainings- oder Scoring-Durchgangs {#experiment-training-scoring}

Sie können Trainings- oder Scoring-Durchgänge erstellen, indem Sie eine Experimentanforderung ausführen, eine gültige POST-ID angeben und die Ausführungsaufgabe angeben. Scoring-Durchgänge können nur erstellt werden, wenn das Experiment über einen vorhandenen und erfolgreichen Trainings-Durchgang verfügt. Wenn ein Trainings-Durchgang erfolgreich erstellt wurde, wird das Modell-Trainingsverfahren initialisiert, und nach erfolgreichem Abschluss wird ein trainiertes Modell generiert. Das Generieren trainierter Modelle ersetzt alle zuvor vorhandenen, sodass ein Experiment immer nur ein trainiertes Modell verwenden kann.

**API-Format**

```http
POST /experiments/{EXPERIMENT_ID}/runs
```

| Parameter | Beschreibung |
| --- | --- |
| `{EXPERIMENT_ID}` | Eine gültige Experiment-ID. |

**Anfrage**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b/runs \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
    -d '{
        "mode": "{TASK}"
    }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `{TASK}` | Gibt die Aufgabe der Ausführung an. Legen Sie diesen Wert entweder als `train` für das Training, als `score` für die Bewertung oder als `featurePipeline` für die Feature Pipeline fest. |

**Antwort**

Bei einer erfolgreichen Antwort wird eine Payload zurückgegeben, die die Details des neu erstellten Durchgangs enthält, einschließlich der geerbten Standard-Trainings- oder Bewertungsparameter und der eindeutigen ID des Durchgangs (`{RUN_ID}`).

```json
{
    "id": "33408593-2871-4198-a812-6d1b7d939cda",
    "mode": "{TASK}",
    "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdBySchedule": false,
    "tasks": [
        {
            "name": "{TASK}",
            "parameters": [
                {
                    "key": "parameter",
                    "value": "parameter value"
                }
            ]
        }
    ]
}
```

## Abrufen einer Liste von Experimenten

Sie können eine Liste von Experimenten abrufen, die zu einer bestimmten MLInstance gehören, indem Sie eine einzige GET-Anfrage ausführen und eine gültige MLInstance-ID als Abfrageparameter angeben. Eine Liste der verfügbaren Abfragen finden Sie im Anhang zu den [Abfrageparametern für den Asset-Abruf](./appendix.md#query).


**API-Format**

```http
GET /experiments
GET /experiments?property=mlInstanceId=={MLINSTANCE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{MLINSTANCE_ID}` | Geben Sie eine gültige MLInstance-ID an, um eine Liste der Experimente abzurufen, die zu dieser MLInstance gehören. |

**Anfrage**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Experimenten zurück, die dieselbe MLInstance-ID (`{MLINSTANCE_ID}`) haben.

```json
{
    "children": [
        {
            "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "name": "A name for this Experiment",
            "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "6cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "name": "Training Run 1",
            "mlInstanceId": "46986c8f-7839-4376-8509-0178bdf32cda",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "7cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "name": "Training Run 2",
            "mlInstanceId": "46986c8f-7939-4376-8509-0178bdf32cda",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        }
    ],
    "_page": {
        "property": "deleted==false",
        "count": 3
    }
}
```

## Abrufen eines bestimmten Experiments {#retrieve-specific}

Sie können die Details eines bestimmten Experiments abrufen, indem Sie eine GET-Anfrage ausführen, die die ID des gewünschten Experiments im Anfragepfad enthält.

**API-Format**

```http
GET /experiments/{EXPERIMENT_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{EXPERIMENT_ID}` | Eine gültige Experiment-ID. |

**Anfrage**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Payload zurück, die die Details des angeforderten Experiments enthält.

```json
{
    "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "name": "A name for this Experiment",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## Abrufen einer Liste von Experimentausführungen

Sie können eine Liste von Trainings- oder Scoring-Durchgängen abrufen, die zu einem bestimmten Experiment gehören, indem Sie eine einzige GET-Anfrage ausführen und eine gültige Experiment-ID angeben. Sie können die Ergebnisse filtern, indem Sie im Anfragepfad Abfrageparameter angeben. Eine vollständige Liste der verfügbaren Abfrageparameter finden Sie im Anhang unter [Abfrageparameter für den Asset-Abruf](./appendix.md#query).

>[!NOTE]
>
>Wenn mehrere Abfrageparameter kombiniert werden, müssen sie durch kaufmännische Und-Zeichen (&amp;) getrennt werden.

**API-Format**

```http
GET /experiments/{EXPERIMENT_ID}/runs
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER}={VALUE}
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parameter | Beschreibung |
| --- | --- |
| `{EXPERIMENT_ID}` | Eine gültige Experiment-ID. |
| `{QUERY_PARAMETER}` | Einer der [verfügbaren Abfrageparameter](./appendix.md#query) zum Filtern von Ergebnissen. |
| `{VALUE}` | Der Wert für den vorangehenden Abfrageparameter. |

**Anfrage**

Die folgende Anfrage enthält eine Abfrage und ruft eine Liste von Trainings-Läufen ab, die zu einem Experiment gehören.

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b/runs?property=mode==train \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort wird eine Payload zurückgegeben, die eine Liste der Ausführungen und jedes ihrer Details enthält, einschließlich der Experiment-Ausführungs-ID (`{RUN_ID}`).

```json
{
    "children": [
        {
            "id": "33408593-2871-4198-a812-6d1b7d939cda",
            "mode": "train",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "createdBySchedule": false
        }
    ],
    "_page": {
        "property": "mode==train,experimentId==5cb25a2d-2cbd-4c99-a619-8ddae5250a7b,deleted==false",
        "totalCount": 1,
        "count": 1
    }
}
```

## Aktualisieren eines Experiments

Sie können ein vorhandenes Experiment aktualisieren, indem Sie seine Eigenschaften über eine PUT-Anfrage überschreiben, die die ID des Zielexperiments im Anfragepfad enthält, und eine JSON-Payload mit aktualisierten Eigenschaften angeben.

>[!TIP]
>
>Um den Erfolg dieser PUT-Anfrage sicherzustellen, wird empfohlen, zunächst eine GET-Anfrage durchzuführen, um [das Experiment nach ID abzurufen](#retrieve-specific). Ändern und aktualisieren Sie dann das zurückgegebene JSON-Objekt und übernehmen Sie die Gesamtheit des geänderten JSON-Objekts als Payload für die PUT-Anfrage.

Der folgende Beispiel-API-Aufruf aktualisiert den Namen eines Experiments, während es anfänglich diese Eigenschaften hat:

```json
{
    "name": "A name for this Experiment",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "createdByService": false
}
```

**API-Format**

```http
PUT /experiments/{EXPERIMENT_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{EXPERIMENT_ID}` | Eine gültige Experiment-ID. |

**Anfrage**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiments.v1.json' \
    -d '{
        "name": "An upated name",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "createdByService": false
    }'
```

**Antwort**

Bei erfolgreicher Antwort wird eine Payload mit den aktualisierten Details des Experiments zurückgegeben.

```json
{
    "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "name": "An updated name",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "createdByService": false
}
```

## Löschen eines Experiments

Sie können ein einzelnes DELETE löschen, indem Sie eine Experimentanfrage ausführen, die die ID des Zielexperiments im Anfragepfad enthält.

**API-Format**

```http
DELETE /experiments/{EXPERIMENT_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{EXPERIMENT_ID}` | Eine gültige Experiment-ID. |

**Anfrage**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
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
    "detail": "Experiment successfully deleted"
}
```

## Löschen von Experimenten nach MLInstance-ID

Sie können alle Experimente löschen, die zu einer bestimmten MLInstance gehören, indem Sie eine DELETE-Anfrage ausführen, die die MLInstance-ID als Abfrageparameter enthält.

**API-Format**

```http
DELETE /experiments?mlInstanceId={MLINSTANCE_ID}
```

| Parameter | Beschreibung |
| --- | ---|
| `{MLINSTANCE_ID}` | Eine gültige MLInstance-ID. |

**Anfrage**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/experiments?mlInstanceId=46986c8f-7739-4376-8509-0178bdf32cda \
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
    "detail": "Experiments successfully deleted"
}
```
