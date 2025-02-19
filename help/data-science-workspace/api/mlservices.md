---
keywords: Experience Platform;Entwicklerhandbuch;Endpunkt;Data Science Workspace;beliebte Themen;mlservices;Sensei Machine Learning-API
solution: Experience Platform
title: MLServices-API-Endpunkt
description: Ein MLService ist ein veröffentlichtes trainiertes Modell, das Ihrem Unternehmen die Möglichkeit bietet, auf zuvor entwickelte Modelle zuzugreifen und sie wiederzuverwenden. Ein wesentliches Merkmal von MLServices ist die Möglichkeit, Trainings- und Scoring-Vorgänge auf geplanter Basis zu automatisieren. Geplante Trainings-Läufe können dazu beitragen, die Effizienz und Genauigkeit eines Modells aufrechtzuerhalten, während geplante Scoring-Läufe sicherstellen können, dass neue Einblicke konsistent generiert werden.
role: Developer
exl-id: cd236e0b-3bfc-4d37-83eb-432f6ad5c5b6
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 9%

---

# MLServices-Endpunkt

>[!NOTE]
>
>Data Science Workspace ist nicht mehr erhältlich.
>
>Diese Dokumentation richtet sich an Bestandskunden mit vorherigen Berechtigungen für Data Science Workspace.

Ein MLService ist ein veröffentlichtes trainiertes Modell, das Ihrem Unternehmen die Möglichkeit bietet, auf zuvor entwickelte Modelle zuzugreifen und sie wiederzuverwenden. Ein wesentliches Merkmal von MLServices ist die Möglichkeit, Trainings- und Scoring-Vorgänge auf geplanter Basis zu automatisieren. Geplante Trainings-Läufe können dazu beitragen, die Effizienz und Genauigkeit eines Modells aufrechtzuerhalten, während geplante Scoring-Läufe sicherstellen können, dass neue Einblicke konsistent generiert werden.

Automatische Trainings- und Scoring-Zeitpläne sind mit einem Start- und Endzeitstempel sowie einer Häufigkeit definiert, die als „Cron[Ausdruck“ dargestellt ](https://en.wikipedia.org/wiki/Cron). Zeitpläne können beim Erstellen [ MLService definiert ](#create-an-mlservice) durch [Aktualisieren eines vorhandenen MLService) ](#update-an-mlservice).

## Erstellen eines MLService {#create-an-mlservice}

Sie können einen MLService erstellen, indem Sie eine POST-Anfrage und eine Payload ausführen, die einen Namen für den Service und eine gültige MLInstance-ID angeben. Die MLInstance, die zum Erstellen eines MLService verwendet wird, muss nicht über vorhandene Trainings-Experimente verfügen. Sie können jedoch den MLService mit einem vorhandenen trainierten Modell erstellen, indem Sie die entsprechende Experiment-ID und Trainings-Durchgangs-ID angeben.

**API-Format**

```http
POST /mlServices
```

**Anfrage**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/mlServices \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json; profile=mlService.v1.json' \
    -d '{
        "name": "A name for this MLService",
        "description": "A description for this MLService",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
        "trainingDataSetId": "5ee3cd7f2d34011913c56941",
        "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
        "trainingExperimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "trainingSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        },
        "scoringSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        }
    }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der gewünschte Name für den MLService. Der Service, der diesem MLService entspricht, übernimmt diesen Wert, der in der Service Gallery-Benutzeroberfläche als Name des Services angezeigt wird. |
| `description` | Eine optionale Beschreibung für den MLService. Der Service, der diesem MLService entspricht, übernimmt diesen Wert, der in der Service Gallery-Benutzeroberfläche als Beschreibung des Services angezeigt wird. |
| `mlInstanceId` | Eine gültige MLInstance-ID. |
| `trainingDataSetId` | Eine Trainings-Datensatz-ID, die, falls angegeben, die standardmäßige Datensatz-ID der MLInstance überschreibt. Wenn die MLInstance, die zum Erstellen des MLService verwendet wird, keinen Trainings-Datensatz definiert, müssen Sie eine entsprechende Trainings-Datensatz-ID angeben. |
| `trainingExperimentId` | Eine Experiment-ID, die Sie optional angeben können. Wenn dieser Wert nicht angegeben wird, wird beim Erstellen des MLService auch ein neues Experiment unter Verwendung der Standardkonfigurationen der MLInstance erstellt. |
| `trainingExperimentRunId` | Eine ID für den Trainings-Durchgang, die Sie optional angeben können. Wenn dieser Wert nicht angegeben wird, wird beim Erstellen des MLService auch ein Trainings-Durchgang unter Verwendung der standardmäßigen Trainings-Parameter der MLInstance erstellt und ausgeführt. |
| `trainingSchedule` | Ein Zeitplan für automatisierte Trainings-Läufe. Wenn diese Eigenschaft definiert ist, führt der MLService automatisch geplante Schulungsdurchgänge durch. |
| `trainingSchedule.startTime` | Ein Zeitstempel, für den geplante Trainings-Läufe beginnen. |
| `trainingSchedule.endTime` | Ein Zeitstempel, für den geplante Schulungsdurchgänge beendet werden. |
| `trainingSchedule.cron` | Ein Cron-Ausdruck, der die Häufigkeit automatisierter Trainings-Läufe definiert. |
| `scoringSchedule` | Ein Zeitplan für automatische Scoring-Durchgänge. Wenn diese Eigenschaft definiert ist, führt MLService automatisch geplante Bewertungsdurchgänge durch. |
| `scoringSchedule.startTime` | Ein Zeitstempel, für den geplante Scoring-Durchgänge beginnen. |
| `scoringSchedule.endTime` | Ein Zeitstempel, für den geplante Scoring-Durchgänge enden. |
| `scoringSchedule.cron` | Ein Cron-Ausdruck, der die Häufigkeit automatisierter Scoring-Durchgänge definiert. |

**Antwort**

Bei einer erfolgreichen Antwort wird eine Payload zurückgegeben, die die Details des neu erstellten MLService enthält, einschließlich der eindeutigen Kennung (`id`), der Experiment-ID für das Training (`trainingExperimentId`), der Experiment-ID für die Bewertung (`scoringExperimentId`) und der Eingabe-Datensatz-ID für das Training (`trainingDataSetId`).

```json
{
    "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
    "trainingDataSetId": "5ee3cd7f2d34011913c56941",
    "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "trainingSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "scoringSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "updated": "2019-01-01T00:00:00.000Z"
}
```

## Abrufen einer Liste von MLServices {#retrieve-a-list-of-mlservices}

Sie können eine Liste von MLServices abrufen, indem Sie eine einzelne GET-Anfrage ausführen. Sie können die Ergebnisse filtern, indem Sie im Anfragepfad Abfrageparameter angeben. Eine Liste der verfügbaren Abfragen finden Sie im Anhang zu den [Abfrageparametern für den Asset-Abruf](./appendix.md#query).

**API-Format**

```http
GET /mlServices
GET /mlServices?{QUERY_PARAMETER}={VALUE}
GET /mlServices?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parameter | Beschreibung |
| --- | --- |
| `{QUERY_PARAMETER}` | Einer der [verfügbaren Abfrageparameter](./appendix.md#query) zum Filtern von Ergebnissen. |
| `{VALUE}` | Der Wert für den vorangehenden Abfrageparameter. |

**Anfrage**

Die folgende Anfrage enthält eine Abfrage und ruft eine Liste von MLServices ab, die dieselbe MLInstance-ID haben (`{MLINSTANCE_ID}`).

```shell
curl -X GET \
    'https://platform.adobe.io/data/sensei/mlServices?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort wird eine Liste von MLServices und deren Details zurückgegeben, einschließlich der MLService-ID (`{MLSERVICE_ID}`), der Experiment-ID für das Training (`{TRAINING_ID}`), der Experiment-ID für die Bewertung (`{SCORING_ID}`) und der Eingabe-Trainings-Datensatz-ID (`{DATASET_ID}`).

```json
{
    "children": [
        {
            "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
            "name": "A service created in UI",
            "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
            "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
            "trainingDataSetId": "5ee3cd7f2d34011913c56941",
            "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        }
    ],
    "_page": {
        "property": "mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda,deleted==false",
        "count": 1
    }
}
```

## Abrufen eines bestimmten MLService {#retrieve-a-specific-mlservice}

Sie können die Details eines bestimmten Experiments abrufen, indem Sie eine GET-Anfrage ausführen, die die ID des gewünschten MLService im Anfragepfad enthält.

**API-Format**

```http
GET /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`: Eine gültige MLService-ID.

**Anfrage**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Payload zurück, die die Details des angeforderten MLService enthält.

```json
{
    "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
    "trainingDataSetId": "5ee3cd7f2d34011913c56941",
    "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z"
}
```

## Aktualisieren eines MLService {#update-an-mlservice}

Sie können einen vorhandenen MLService aktualisieren, indem Sie seine Eigenschaften durch eine PUT-Anfrage überschreiben, die die ID des Ziel-MLService im Anfragepfad enthält, und eine JSON-Payload mit aktualisierten Eigenschaften angeben.

>[!TIP]
>
>Um den Erfolg dieser PUT-Anfrage sicherzustellen, wird empfohlen, zunächst eine GET-Anfrage durchzuführen, um (den MLService nach ID [) ](#retrieve-a-specific-mlservice). Ändern und aktualisieren Sie dann das zurückgegebene JSON-Objekt und übernehmen Sie die Gesamtheit des geänderten JSON-Objekts als Payload für die PUT-Anfrage.

**API-Format**

```http
PUT /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`: Eine gültige MLService-ID.

**Anfrage**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json; profile=mlService.v1.json' \
    -d '{
        "name": "A name for this MLService",
        "description": "A description for this MLService",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
        "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
        "trainingDataSetId": "5ee3cd7f2d34011913c56941",
        "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
        "trainingSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        },
        "scoringSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        }
    }'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Payload zurück, die die aktualisierten Details des MLService enthält.

```json
{
    "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
    "trainingDataSetId": "5ee3cd7f2d34011913c56941",
    "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "trainingSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "scoringSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "updated": "2019-01-02T00:00:00.000Z"
}
```

## Löschen eines MLService

Sie können einen einzelnen MLService löschen, indem Sie eine DELETE-Anfrage ausführen, die die ID des Ziel-MLService im Anfragepfad enthält.

**API-Format**

```http
DELETE /mlServices/{MLSERVICE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{MLSERVICE_ID}` | Eine gültige MLService-ID. |

**Anfrage**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
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
    "detail": "MLService deletion was successful"
}
```

## Löschen von MLServices nach MLInstance-ID

Sie können alle MLServices löschen, die zu einer bestimmten MLInstance gehören, indem Sie eine DELETE-Anfrage ausführen, die eine MLInstance-ID als Abfrageparameter angibt.

**API-Format**

```http
DELETE /mlServices?mlInstanceId={MLINSTANCE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{MLINSTANCE_ID}` | Eine gültige MLInstance-ID. |

**Anfrage**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlServices?mlInstanceId=46986c8f-7739-4376-8509-0178bdf32cda \
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
    "detail": "MLServices deletion was successful"
}
```
