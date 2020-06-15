---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Experimente
topic: Developer guide
translation-type: tm+mt
source-git-commit: 63a128202826ec39911e70d34dda9dfb2bc585b2
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 4%

---


# Experimente

Modellentwicklung und Schulung erfolgen auf Experimentebene, bei denen ein Experiment aus einer MLInstanz, Trainingsläufen und Scoring-Läufen besteht.

## Experiment erstellen {#create-an-experiment}

Sie können ein Experiment erstellen, indem Sie eine POST-Anforderung ausführen und gleichzeitig einen Namen und eine gültige MLInstance-ID in der Anforderungs-Nutzlast angeben.

>[!NOTE] Im Gegensatz zur Modellschulung in der Benutzeroberfläche wird beim Erstellen eines Experiments durch einen expliziten API-Aufruf nicht automatisch ein Schulungslauf erstellt und ausgeführt.

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
        "mlInstanceId": "{MLINSTANCE_ID}"
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
    "id": "{EXPERIMENT_ID}",
    "name": "A name for this Experiment",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## Erstellen und Ausführen eines Schulungs- oder Bewertungslaufs {#experiment-training-scoring}

Sie können Schulungs- oder Bewertungsabläufe erstellen, indem Sie eine POST-Anforderung ausführen, eine gültige Experiment-ID bereitstellen und die ausgeführte Aufgabe angeben. Bewertungsläufe können nur erstellt werden, wenn das Experiment über einen vorhandenen und erfolgreichen Schulungslauf verfügt. Durch die erfolgreiche Erstellung eines Schulungslaufs wird der Modellschulungsvorgang initialisiert, und der erfolgreiche Abschluss führt zu einem geschulten Modell. Das Generieren geschulter Modelle ersetzt alle bereits vorhandenen Modelle, sodass ein Experiment zu jeder Zeit nur ein einziges trainiertes Modell verwenden kann.

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
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs \
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
| `{TASK}` | Gibt die Aufgabe des Vorgangs an. Legen Sie diesen Wert entweder `train` für Schulungen, `score` Bewertungen oder `featurePipeline` für Feature-Pipeline fest. |

**Antwort**

Eine erfolgreiche Antwort gibt eine Nutzlast zurück, die die Details der neu erstellten Ausführung einschließlich der geerbten Standard-Schulungs- oder Bewertungsparameter und der eindeutigen ID (`{RUN_ID}`) der Ausführung enthält.

```json
{
    "id": "{RUN_ID}",
    "mode": "{TASK}",
    "experimentId": "{EXPERIMENT_ID}",
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

Sie können eine Liste von Experimenten abrufen, die zu einer bestimmten MLInstanz gehören, indem Sie eine GET-Anforderung ausführen und eine gültige MLInstance-ID als Parameter für die Abfrage angeben. Eine Liste der verfügbaren Abfragen finden Sie im Anhang zu den [Abfrage-Parametern für den Asset-Abruf](./appendix.md#query).


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
    https://platform.adobe.io/data/sensei/experiments?property=mlInstanceId=={MLINSTANCE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort wird eine Liste von Experimenten mit derselben MLInstance-ID (`{MLINSTANCE_ID}`) zurückgegeben.

```json
{
    "children": [
        {
            "id": "{EXPERIMENT_ID}",
            "name": "A name for this Experiment",
            "mlInstanceId": "{MLINSTANCE_ID}",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "{EXPERIMENT_ID}",
            "name": "Training Run 1",
            "mlInstanceId": "{MLINSTANCE_ID}",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "{EXPERIMENT_ID}",
            "name": "Training Run 2",
            "mlInstanceId": "{MLINSTANCE_ID}",
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

Sie können die Details eines bestimmten Experiments abrufen, indem Sie eine GET-Anforderung ausführen, die die ID des gewünschten Experiments im Anforderungspfad enthält.

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
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Nutzlast mit den Details des angeforderten Experiments zurück.

```json
{
    "id": "{EXPERIMENT_ID}",
    "name": "A name for this Experiment",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## Abrufen einer Liste von Experimentabläufen

Sie können eine Liste von Schulungs- oder Bewertungsabläufen abrufen, die zu einem bestimmten Experiment gehören, indem Sie eine GET-Anforderung ausführen und eine gültige Experiment-ID angeben. Um die Ergebnisse zu filtern, können Sie die Parameter für die Abfrage im Anforderungspfad angeben. Eine vollständige Liste der verfügbaren Parameter für die Abfrage finden Sie im Anhang zu den [Abfrage-Parametern für den Asset-Abruf](./appendix.md#query).

>[!NOTE] Beim Kombinieren mehrerer Abfragen-Parameter müssen diese durch das kaufmännische Und (&amp;) getrennt werden.

**API-Format**

```http
GET /experiments/{EXPERIMENT_ID}/runs
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER}={VALUE}
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parameter | Beschreibung |
| --- | --- |
| `{EXPERIMENT_ID}` | Eine gültige Experiment-ID. |
| `{QUERY_PARAMETER}` | Einer der [verfügbaren Parameter](./appendix.md#query) für die Abfrage zum Filtern der Ergebnisse. |
| `{VALUE}` | Der Wert für den Parameter der vorherigen Abfrage. |

**Anfrage**

Die folgende Anforderung enthält eine Abfrage und ruft eine Liste von Schulungsabläufen ab, die zu einem Experiment gehören.

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs?property=mode==train \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Nutzlast zurück, die eine Liste der ausgeführten Vorgänge und deren Details einschließlich der Experiment-Ausführen-ID (`{RUN_ID}`) enthält.

```json
{
    "children": [
        {
            "id": "{RUN_ID}",
            "mode": "train",
            "experimentId": "{EXPERIMENT_ID}",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "createdBySchedule": false
        }
    ],
    "_page": {
        "property": "mode==train,experimentId=={EXPERIMENT_ID},deleted==false",
        "totalCount": 1,
        "count": 1
    }
}
```

## Experiment aktualisieren

Sie können ein vorhandenes Experiment aktualisieren, indem Sie seine Eigenschaften durch eine PUT-Anforderung überschreiben, die die ID des Experiments &quot;Zielgruppe&quot;im Anforderungspfad enthält und eine JSON-Nutzlast mit aktualisierten Eigenschaften bereitstellt.

>[!TIP] Um den Erfolg dieser PUT-Anforderung sicherzustellen, wird empfohlen, zuerst eine GET-Anforderung zum [Abrufen des Experiments nach ID](#retrieve-specific)auszuführen. Ändern Sie dann das zurückgegebene JSON-Objekt und aktualisieren Sie es und wenden Sie die gesamte Eigenschaft des geänderten JSON-Objekts als Nutzlast für die PUT-Anforderung an.

Der folgende Beispiel-API-Aufruf aktualisiert den Namen eines Experiments, während diese Eigenschaften zunächst verwendet werden:

```json
{
    "name": "A name for this Experiment",
    "mlInstanceId": "{MLINSTANCE_ID}",
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
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiments.v1.json' \
    -d '{
        "name": "An upated name",
        "mlInstanceId": "{MLINSTANCE_ID}",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "createdByService": false
    }'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Nutzlast mit den aktualisierten Details des Experiments zurück.

```json
{
    "id": "{EXPERIMENT_ID}",
    "name": "An updated name",
    "mlInstanceId": "{MLINSTANCE_ID}",
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
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID} \
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
    https://platform.adobe.io/data/sensei/experiments?mlInstanceId={MLINSTANCE_ID} \
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
