---
keywords: Experience Platform;Entwicklerhandbuch;Endpunkt;Data Science Workspace;beliebte Themen;Experimente;sensei-maschinelles Lernen API
solution: Experience Platform
title: Experiment-API-Endpunkt
topic-legacy: Developer guide
description: Modellentwicklung und Schulung erfolgen auf Experimentebene, bei denen ein Experiment aus einer MLInstanz, Trainingsläufen und Scoring-Läufen besteht.
exl-id: 6ca5106e-896d-4c03-aecc-344632d5307d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 17%

---

# Experimentendpunkt

Modellentwicklung und Schulung erfolgen auf Experimentebene, bei denen ein Experiment aus einer MLInstanz, Trainingsläufen und Scoring-Läufen besteht.

## Erstellen eines Experiments {#create-an-experiment}

Sie können ein Experiment erstellen, indem Sie eine Anforderung zur POST ausführen und gleichzeitig einen Namen und eine gültige MLInstance-ID in der Anforderungs-Nutzlast angeben.

>[!NOTE]
>
>Im Gegensatz zur Modellschulung in der Benutzeroberfläche wird beim Erstellen eines Experiments durch einen expliziten API-Aufruf nicht automatisch ein Schulungslauf erstellt und ausgeführt.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
    -d '{
        "name": "a name for this Experiment",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda"
    }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der gewünschte Name für das Experiment. Der diesem Experiment entsprechende Schulungslauf erbt diesen Wert, der in der Benutzeroberfläche als Name der Schulungsausführung angezeigt wird. |
| `mlInstanceId` | Eine gültige MLInstance-ID. |

**Antwort**

Eine erfolgreiche Antwort gibt eine Nutzlast zurück, die die Details des neu erstellten Experiments einschließlich der eindeutigen Kennung (`id`) enthält.

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

## Erstellen und Ausführen einer Schulung oder einer Bewertungsausführung {#experiment-training-scoring}

Sie können Schulungs- oder Bewertungsabläufe erstellen, indem Sie eine POST anfordern, eine gültige Experiment-ID bereitstellen und die ausgeführte Aufgabe angeben. Bewertungsläufe können nur erstellt werden, wenn das Experiment über einen vorhandenen und erfolgreichen Schulungslauf verfügt. Durch die erfolgreiche Erstellung eines Schulungslaufs wird der Modellschulungsvorgang initialisiert, und der erfolgreiche Abschluss führt zu einem geschulten Modell. Das Generieren geschulter Modelle ersetzt alle bereits vorhandenen Modelle, sodass ein Experiment zu jeder Zeit nur ein einziges trainiertes Modell verwenden kann.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
    -d '{
        "mode": "{TASK}"
    }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `{TASK}` | Gibt die Aufgabe des Vorgangs an. Legen Sie für diesen Wert entweder `train` für die Schulung, `score` für die Bewertung oder `featurePipeline` für die Feature-Pipeline fest. |

**Antwort**

Eine erfolgreiche Antwort gibt eine Nutzlast zurück, die die Details der neu erstellten Ausführung einschließlich der geerbten Standard-Schulungs- oder Bewertungsparameter und der eindeutigen ID der Ausführung (`{RUN_ID}`) enthält.

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

Sie können eine Liste von Experimenten abrufen, die zu einer bestimmten MLInstanz gehören, indem Sie eine einzige GET anfordern und eine gültige MLInstance-ID als Parameter für die Abfrage angeben. Eine Liste der verfügbaren Abfragen finden Sie im Anhang zu den [Abfrageparametern für den Asset-Abruf](./appendix.md#query).


**API-Format**

```http
GET /experiments
GET /experiments?property=mlInstanceId=={MLINSTANCE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{MLINSTANCE_ID}` | Geben Sie eine gültige MLInstance-ID an, um eine Liste von Experimenten abzurufen, die zu dieser bestimmten MLInstanz gehören. |

**Anfrage**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Experimenten mit derselben MLInstance-ID (`{MLINSTANCE_ID}`) zurück.

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

Sie können die Details eines bestimmten Experiments abrufen, indem Sie eine GET anfordern, die die ID des gewünschten Experiments im Anforderungspfad enthält.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Nutzlast mit den Details des angeforderten Experiments zurück.

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

Sie können eine Liste von Schulungs- oder Bewertungsabläufen abrufen, die zu einem bestimmten Experiment gehören, indem Sie eine einzige GET anfordern und eine gültige Experiment-ID angeben. Sie können die Ergebnisse filtern, indem Sie im Anfragepfad Abfrageparameter angeben. Eine vollständige Liste der verfügbaren Abfrage-Parameter finden Sie im Anhang zu [Abfrage-Parametern für das Abrufen von Assets](./appendix.md#query).

>[!NOTE]
>
>Beim Kombinieren mehrerer Abfragen-Parameter müssen diese durch das kaufmännische Und (&amp;) getrennt werden.

**API-Format**

```http
GET /experiments/{EXPERIMENT_ID}/runs
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER}={VALUE}
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parameter | Beschreibung |
| --- | --- |
| `{EXPERIMENT_ID}` | Eine gültige Experiment-ID. |
| `{QUERY_PARAMETER}` | Einer der [verfügbaren Abfrage-Parameter](./appendix.md#query), der zum Filtern der Ergebnisse verwendet wird. |
| `{VALUE}` | Der Wert für den Parameter der vorherigen Abfrage. |

**Anfrage**

Die folgende Anforderung enthält eine Abfrage und ruft eine Liste von Schulungsabläufen ab, die zu einem Experiment gehören.

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b/runs?property=mode==train \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Nutzlast zurück, die eine Liste der Ausführung und deren Details einschließlich der Experiment-Ausführen-ID (`{RUN_ID}`) enthält.

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

Sie können ein vorhandenes Experiment aktualisieren, indem Sie seine Eigenschaften durch eine PUT-Anforderung überschreiben, die die ID des Zielgruppen-Experiments im Anforderungspfad enthält und eine JSON-Nutzlast mit aktualisierten Eigenschaften bereitstellt.

>[!TIP]
>
>Um den Erfolg dieser PUT-Anforderung sicherzustellen, wird empfohlen, zunächst eine GET an [das Experiment nach ID](#retrieve-specific) abzurufen. Ändern und aktualisieren Sie dann das zurückgegebene JSON-Objekt und übernehmen Sie die Gesamtheit des geänderten JSON-Objekts als Payload für die PUT-Anfrage.

Der folgende Beispiel-API-Aufruf aktualisiert den Namen eines Experiments, während diese Eigenschaften zunächst verwendet werden:

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

## Experimente löschen

Sie können ein einzelnes Experiment löschen, indem Sie eine DELETE-Anforderung ausführen, die die ID des Zielgruppen-Experiments im Anforderungspfad enthält.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

## Experimente nach MLInstance-ID löschen

Sie können alle Experimente, die zu einer bestimmten MLInstanz gehören, löschen, indem Sie eine DELETE-Anforderung ausführen, die die MLInstance-ID als Abfrage-Parameter enthält.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
