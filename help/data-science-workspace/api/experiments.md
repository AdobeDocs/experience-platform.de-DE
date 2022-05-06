---
keywords: Experience Platform; Entwicklerhandbuch; Endpunkt; Data Science Workspace; beliebte Themen; Experimente; Sensei-API für maschinelles Lernen
solution: Experience Platform
title: Experiment-API-Endpunkt
topic-legacy: Developer guide
description: Modellentwicklung und -schulung finden auf Experimentebene statt, bei der ein Experiment aus einer MLInstance, Trainings-Läufen und Scoring-Läufen besteht.
exl-id: 6ca5106e-896d-4c03-aecc-344632d5307d
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 17%

---

# Experiment-Endpunkt

Modellentwicklung und -schulung finden auf Experimentebene statt, bei der ein Experiment aus einer MLInstance, Trainings-Läufen und Scoring-Läufen besteht.

## Erstellen eines Experiments {#create-an-experiment}

Sie können ein Experiment erstellen, indem Sie eine POST-Anfrage ausführen und in der Anfrage-Payload einen Namen und eine gültige MLInstance-ID angeben.

>[!NOTE]
>
>Im Gegensatz zur Modellschulung in der Benutzeroberfläche wird beim Erstellen eines Experiments über einen expliziten API-Aufruf nicht automatisch ein Trainings-Lauf erstellt und ausgeführt.

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
| `name` | Der gewünschte Name für das Experiment. Der diesem Experiment entsprechende Trainings-Lauf übernimmt diesen Wert, der in der Benutzeroberfläche als Trainings-Lauf-Name angezeigt werden soll. |
| `mlInstanceId` | Eine gültige MLInstance-ID. |

**Antwort**

Eine erfolgreiche Antwort gibt eine Payload zurück, die die Details des neu erstellten Experiments einschließlich der eindeutigen Kennung (`id`).

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

## Erstellen und Ausführen eines Trainings- oder Scoring-Laufs {#experiment-training-scoring}

Sie können Trainings- oder Scoring-Läufe erstellen, indem Sie eine POST-Anfrage ausführen, eine gültige Experiment-ID angeben und die Ausführungsaufgabe angeben. Scoring-Läufe können nur erstellt werden, wenn das Experiment über einen vorhandenen und erfolgreichen Trainings-Lauf verfügt. Wenn Sie einen Trainings-Lauf erfolgreich erstellen, wird das Trainings-Verfahren für das Modell initialisiert und nach erfolgreichem Abschluss wird ein trainiertes Modell generiert. Durch das Generieren trainierter Modelle werden alle bereits vorhandenen ersetzt, sodass ein Experiment immer nur ein trainiertes Modell verwenden kann.

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
| `{TASK}` | Gibt die Aufgabe der Ausführung an. Setzen Sie diesen Wert auf `train` für die Ausbildung, `score` für Scoring oder `featurePipeline` für die Funktions-Pipeline. |

**Antwort**

Eine erfolgreiche Antwort gibt eine Payload mit den Details der neu erstellten Ausführung zurück, einschließlich der geerbten standardmäßigen Trainings- oder Scoring-Parameter und der eindeutigen Kennung der Ausführung (`{RUN_ID}`).

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

## Liste von Experimenten abrufen

Sie können eine Liste von Experimenten abrufen, die zu einer bestimmten MLInstance gehören, indem Sie eine einzige GET-Anfrage ausführen und eine gültige MLInstance-ID als Abfrageparameter angeben. Eine Liste der verfügbaren Abfragen finden Sie im Anhang zu den [Abfrageparametern für den Asset-Abruf](./appendix.md#query).


**API-Format**

```http
GET /experiments
GET /experiments?property=mlInstanceId=={MLINSTANCE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{MLINSTANCE_ID}` | Stellen Sie eine gültige MLInstance-ID bereit, um eine Liste der Experimente abzurufen, die zu dieser bestimmten MLInstance gehören. |

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

Eine erfolgreiche Antwort gibt eine Liste von Experimenten zurück, die dieselbe MLInstance-ID (`{MLINSTANCE_ID}`).

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

Sie können die Details eines bestimmten Experiments abrufen, indem Sie eine GET-Anfrage ausführen, die die Kennung des gewünschten Experiments im Anfragepfad enthält.

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

## Abrufen einer Liste von Experimentabläufen

Sie können eine Liste von Trainings- oder Scoring-Läufen abrufen, die zu einem bestimmten Experiment gehören, indem Sie eine einzige GET-Anfrage ausführen und eine gültige Experiment-ID angeben. Sie können die Ergebnisse filtern, indem Sie im Anfragepfad Abfrageparameter angeben. Eine vollständige Liste der verfügbaren Abfrageparameter finden Sie im Anhang unter [Abfrageparameter für den Asset-Abruf](./appendix.md#query).

>[!NOTE]
>
>Wenn mehrere Abfrageparameter kombiniert werden, müssen diese durch das kaufmännische Und-Zeichen (&amp;) getrennt werden.

**API-Format**

```http
GET /experiments/{EXPERIMENT_ID}/runs
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER}={VALUE}
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parameter | Beschreibung |
| --- | --- |
| `{EXPERIMENT_ID}` | Eine gültige Experiment-ID. |
| `{QUERY_PARAMETER}` | Eines der [Verfügbare Abfrageparameter](./appendix.md#query) verwendet, um Ergebnisse zu filtern. |
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

Eine erfolgreiche Antwort gibt eine Payload zurück, die eine Liste der Ausführungen und deren Details einschließlich ihrer Experimentablauf-ID (`{RUN_ID}`).

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

## Experiment aktualisieren

Sie können ein vorhandenes Experiment aktualisieren, indem Sie seine Eigenschaften durch eine PUT-Anfrage überschreiben, die die Kennung des Zielexperiments im Anfragepfad enthält, und eine JSON-Payload mit aktualisierten Eigenschaften bereitstellen.

>[!TIP]
>
>Um den Erfolg dieser PUT-Anfrage sicherzustellen, wird empfohlen, zunächst eine GET-Anfrage an [Abrufen des Experiments nach ID](#retrieve-specific). Ändern und aktualisieren Sie dann das zurückgegebene JSON-Objekt und übernehmen Sie die Gesamtheit des geänderten JSON-Objekts als Payload für die PUT-Anfrage.

Der folgende Beispiel-API-Aufruf aktualisiert den Namen eines Experiments und weist zunächst diese Eigenschaften auf:

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

Sie können ein einzelnes Experiment löschen, indem Sie eine DELETE-Anfrage ausführen, die die Kennung des Zielexperiments im Anfragepfad enthält.

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
