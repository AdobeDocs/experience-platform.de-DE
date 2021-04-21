---
keywords: Experience Platform;Entwicklerhandbuch;Endpunkt;Data Science Workspace;beliebte Themen;mlservices;sensei-maschinelles Lernen
solution: Experience Platform
title: MLServices API-Endpunkt
topic-legacy: Developer guide
description: Ein MLService ist ein veröffentlichtes, geschultes Modell, das Ihrem Unternehmen die Möglichkeit gibt, auf bereits entwickelte Modelle zuzugreifen und sie wiederzuverwenden. Eine wichtige Funktion von MLServices ist die Möglichkeit, Schulungen und Bewertungen planmäßig zu automatisieren. Terminierte Schulungen können dazu beitragen, die Effizienz und Genauigkeit eines Modells zu erhalten, während geplante Bewertungsläufe sicherstellen können, dass stets neue Erkenntnisse generiert werden.
exl-id: cd236e0b-3bfc-4d37-83eb-432f6ad5c5b6
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 9%

---

# MLServices-Endpunkt

Ein MLService ist ein veröffentlichtes, geschultes Modell, das Ihrem Unternehmen die Möglichkeit gibt, auf bereits entwickelte Modelle zuzugreifen und sie wiederzuverwenden. Eine wichtige Funktion von MLServices ist die Möglichkeit, Schulungen und Bewertungen planmäßig zu automatisieren. Terminierte Schulungen können dazu beitragen, die Effizienz und Genauigkeit eines Modells zu erhalten, während geplante Bewertungsläufe sicherstellen können, dass stets neue Erkenntnisse generiert werden.

Automatisierte Schulungs- und Bewertungszeitpläne werden mit einem Startzeitstempel, einem Endzeitstempel und einer Häufigkeit definiert, die als [cron-Ausdruck](https://en.wikipedia.org/wiki/Cron) dargestellt wird. Zeitpläne können definiert werden, wenn [ein MLService](#create-an-mlservice) erstellt wird oder [ein vorhandener MLService](#update-an-mlservice) aktualisiert wird.

## Erstellen eines MLService {#create-an-mlservice}

Sie können einen MLService erstellen, indem Sie eine Anforderung zur POST und eine Payload ausführen, die einen Dienstnamen und eine gültige MLInstance-ID bereitstellt. Die zum Erstellen eines MLService verwendete MLService-Instanz benötigt keine vorhandenen Schulungsexperimente, Sie können jedoch den MLService mit einem vorhandenen geschulten Modell erstellen, indem Sie die entsprechende Experiment-ID und die Schulungslaufs-ID angeben.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | Der gewünschte Name für den MLService. Der diesem MLService entsprechende Dienst erbt diesen Wert, der in der Dienstgalerie-Benutzeroberfläche als Dienstname angezeigt wird. |
| `description` | Eine optionale Beschreibung für den MLService. Der Dienst, der diesem MLService entspricht, übernimmt diesen Wert, der in der Dienstgalerie-Benutzeroberfläche als Dienstbeschreibung angezeigt wird. |
| `mlInstanceId` | Eine gültige MLInstance-ID. |
| `trainingDataSetId` | Eine Schulungsdataset-ID, die bei Bereitstellung die Standard-Dataset-ID der MLInstanz außer Kraft setzt. Wenn die zum Erstellen des MLService verwendete MLInstanz kein Schulungsdatensatz definiert, müssen Sie eine entsprechende Schulungsdatensatz-ID bereitstellen. |
| `trainingExperimentId` | Eine Experiment-ID, die Sie optional bereitstellen können. Wenn dieser Wert nicht angegeben ist, erstellt der MLService auch ein neues Experiment mit den Standardkonfigurationen der MLInstanz. |
| `trainingExperimentRunId` | Eine Schulungslaufs-ID, die Sie optional bereitstellen können. Wenn dieser Wert nicht angegeben ist, wird beim Erstellen des MLService auch ein Schulungslauf mit den Standard-Schulungsparametern der MLInstanz erstellt und ausgeführt. |
| `trainingSchedule` | Ein Zeitplan für automatisierte Schulungen wird ausgeführt. Wenn diese Eigenschaft definiert ist, führt der MLService automatisch Schulungen planmäßig durch. |
| `trainingSchedule.startTime` | Ein Zeitstempel, für den geplante Schulungen beginnen. |
| `trainingSchedule.endTime` | Ein Zeitstempel, für den geplante Schulungen beendet werden. |
| `trainingSchedule.cron` | Ein Cron-Ausdruck, der die Häufigkeit automatisierter Schulungen definiert. |
| `scoringSchedule` | Ein Zeitplan für die automatisierte Bewertung wird ausgeführt. Wenn diese Eigenschaft definiert ist, führt der MLService automatisch eine geplante Auswertung durch. |
| `scoringSchedule.startTime` | Ein Zeitstempel, für den geplante Scoring-Vorgänge beginnen. |
| `scoringSchedule.endTime` | Ein Zeitstempel, für den geplante Scoring-Vorgänge beendet werden. |
| `scoringSchedule.cron` | Ein Cron-Ausdruck, der die Häufigkeit automatisierter Scoring-Vorgänge definiert. |

**Antwort**

Eine erfolgreiche Antwort gibt eine Nutzlast zurück, die die Details des neu erstellten MLService einschließlich seiner eindeutigen Kennung (`id`), Experiment-ID für die Schulung (`trainingExperimentId`), Experiment-ID für die Auswertung (`scoringExperimentId`) und der Eingabe-Schulungsdatensatz-ID (`trainingDataSetId`) enthält.

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

Sie können eine Liste von MLServices abrufen, indem Sie eine einzige GET anfordern. Sie können die Ergebnisse filtern, indem Sie im Anfragepfad Abfrageparameter angeben. Eine Liste der verfügbaren Abfragen finden Sie im Anhang zu den [Abfrageparametern für den Asset-Abruf](./appendix.md#query).

**API-Format**

```http
GET /mlServices
GET /mlServices?{QUERY_PARAMETER}={VALUE}
GET /mlServices?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parameter | Beschreibung |
| --- | --- |
| `{QUERY_PARAMETER}` | Einer der [verfügbaren Abfrage-Parameter](./appendix.md#query), der zum Filtern der Ergebnisse verwendet wird. |
| `{VALUE}` | Der Wert für den Parameter der vorherigen Abfrage. |

**Anfrage**

Die folgende Anforderung enthält eine Abfrage und ruft eine Liste von MLServices mit derselben MLInstance-ID (`{MLINSTANCE_ID}`) ab.

```shell
curl -X GET \
    'https://platform.adobe.io/data/sensei/mlServices?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von MLServices und deren Details zurück, einschließlich ihrer MLService-ID (`{MLSERVICE_ID}`), Experiment-ID für die Schulung (`{TRAINING_ID}`), Experiment-ID für die Auswertung (`{SCORING_ID}`) und der Eingabe-Schulungsdatensatz-ID (`{DATASET_ID}`).

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

Sie können die Details eines bestimmten Experiments abrufen, indem Sie eine GET durchführen, die die gewünschte MLService-ID im Anforderungspfad enthält.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Payload mit den Details des angeforderten MLService zurück.

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

Sie können einen vorhandenen MLService aktualisieren, indem Sie seine Eigenschaften durch eine PUT-Anforderung überschreiben, die die Zielgruppe-MLService-ID im Anforderungspfad enthält und eine JSON-Nutzlast mit aktualisierten Eigenschaften bereitstellt.

>[!TIP]
>
>Um den Erfolg dieser PUT-Anforderung sicherzustellen, wird empfohlen, zunächst eine GET an [den MLService nach ID](#retrieve-a-specific-mlservice) abzurufen. Ändern und aktualisieren Sie dann das zurückgegebene JSON-Objekt und übernehmen Sie die Gesamtheit des geänderten JSON-Objekts als Payload für die PUT-Anfrage.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Eine erfolgreiche Antwort gibt eine Payload mit den aktualisierten Details des MLService zurück.

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

Sie können einen einzelnen MLService löschen, indem Sie eine DELETE-Anforderung ausführen, die die Zielgruppe-MLService-ID im Anforderungspfad enthält.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

## MLServices nach MLInstance-ID löschen

Sie können alle zu einer bestimmten MLServices gehörenden MLServices löschen, indem Sie eine DELETE-Anforderung ausführen, die eine MLInstance-ID als Abfrage-Parameter angibt.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
