---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Modelle
topic: Developer guide
translation-type: tm+mt
source-git-commit: 33f8c424c208bb61319b49e7ecb30e3144ef108a
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 4%

---


# Modelle

Ein Modell ist ein Beispiel für ein maschinelles Lernrezept, das mithilfe von historischen Daten und Konfigurationen für die Lösung eines Geschäftsfalls trainiert wird.

## Eine Liste von Modellen abrufen

Sie können eine Liste von Modelldetails abrufen, die zu allen Modellen gehören, indem Sie eine GET-Anforderung an /models durchführen. Standardmäßig bestellt sich diese Liste vom ältesten erstellten Modell und beschränkt die Ergebnisse auf 25. Sie können die Abfragen filtern, indem Sie einige Parameter angeben. Eine Liste der verfügbaren Abfragen finden Sie im Anhang zu den [Abfrage-Parametern für den Asset-Abruf](./appendix.md#query).

**API-Format**

```http
GET /models
```

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/ \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Nutzlast zurück, die die Details Ihrer Modelle einschließlich der einzelnen eindeutigen Modellkennung (`id`) enthält.

```json
{
    "children": [
        {
            "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "name": "A name for this Model",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for this Model",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "27c53796-bd6b-4u59-b51d-7296aa20er23",
            "name": "Model 2",
            "experimentId": "3cb25a2d-2cbd-4d34-a619-8ddae5259a5t",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for Model2",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "name": "Model 3",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for Model3",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
    ],
    "_page": {
        "property": "deleted==false",
        "count": 3
    }
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `id` | Die dem Modell entsprechende ID. |
| `modelArtifactUri` | Ein URI, der angibt, wo das Modell gespeichert ist. Der URI endet mit dem `name` Wert für das Modell. |
| `experimentId` | Eine gültige Experiment-ID. |
| `experimentRunId` | Eine gültige Experimentausführung-ID. |

## Abrufen eines bestimmten Modells

Sie können eine Liste von Modelldetails abrufen, die zu einem bestimmten Modell gehören, indem Sie eine GET-Anforderung ausführen und eine gültige Modell-ID im Anforderungspfad angeben. Um die Ergebnisse zu filtern, können Sie die Parameter für die Abfrage im Anforderungspfad angeben. Eine Liste der verfügbaren Abfragen finden Sie im Anhang zu den [Abfrage-Parametern für den Asset-Abruf](./appendix.md#query).

**API-Format**

```http
GET /models/{MODEL_ID}
GET /models/?property=experimentRunID=={EXPERIMENT_RUN_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{MODEL_ID}` | Die Kennung des trainierten oder veröffentlichten Modells. |
| `{EXPERIMENT_RUN_ID}` | Der Bezeichner des Experiments, das ausgeführt wird. |

**Anfrage**

Die folgende Anforderung enthält eine Abfrage und ruft eine Liste geschulter Modelle ab, die dieselbe experimentRunID ({EXPERIMENT_RUN_ID}) gemeinsam verwenden.

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/?property=experimentRunId==33408593-2871-4198-a812-6d1b7d939cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Nutzlast zurück, die die Details Ihres Modells einschließlich der eindeutigen Modellkennung (`id`) enthält.

```json
{
    "children": [
        {
            "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "name": "A name for this Model",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for this Model",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       }
    ],
    "_page": {
        "property": "experimentRunId==33408593-2871-4198-a812-6d1b7d939cda,deleted==false",
        "count": 1
    }
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `id` | Die dem Modell entsprechende ID. |
| `modelArtifactUri` | Ein URI, der angibt, wo das Modell gespeichert ist. Der URI endet mit dem `name` Wert für das Modell. |
| `experimentId` | Eine gültige Experiment-ID. |
| `experimentRunId` | Eine gültige Experimentausführung-ID. |

## Vorab generiertes Modell registrieren {#register-a-model}

Sie können ein vorab erstelltes Modell registrieren, indem Sie eine POST-Anforderung an den `/models` Endpunkt senden. Um Ihr Modell registrieren zu können, müssen die `modelArtifact` Datei- und `model` Eigenschaftswerte im Hauptteil der Anforderung enthalten sein.

**API-Format**

```http
POST /models
```

**Anfrage**

Der folgende POST-Test enthält die erforderlichen `modelArtifact` Datei- und `model` Eigenschaftenwerte. Weitere Informationen zu diesen Werten finden Sie in der unten stehenden Tabelle.

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/models \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -F 'modelArtifact=@/Users/yourname/Desktop/model.onnx' \
    -F 'model={
            "name": "Your Model - 0615-1342-45",
            "originType": "offline"
    }'
```

| Parameter | Beschreibung |
| --- | --- |
| `modelArtifact` | Die Position des vollständigen Modellartefakts, das Sie einbeziehen möchten. |
| `model` | Die Formulardaten des Modellobjekts, das erstellt werden muss. |

**Antwort**

Eine erfolgreiche Antwort gibt eine Nutzlast zurück, die die Details Ihres Modells einschließlich der eindeutigen Modellkennung (`id`) enthält.

```json
{
  "id": "a28f151a-597a-4a7e-87e9-1c1dbc9c2af7",
  "name": "Your Model - 0615-1342-45",
  "originType": "offline",
  "modelArtifactUri": "http://storageblobml.blob.core.windows.net/prod-models/a28f151a-597a-4a7e-87e9-1c1dbc9c2af7",
  "created": "2020-06-15T20:55:41.520Z",
  "updated": "2020-06-15T20:55:41.520Z",
  "deprecated": false
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `id` | Die dem Modell entsprechende ID. |
| `modelArtifactUri` | Ein URI, der angibt, wo das Modell gespeichert ist. Der URI endet mit dem `id` Wert für Ihr Modell. |

## Modell nach ID aktualisieren

Sie können ein vorhandenes Modell aktualisieren, indem Sie seine Eigenschaften durch eine PUT-Anforderung überschreiben, die die ID des Zielgruppe-Modells im Anforderungspfad enthält und eine JSON-Nutzlast mit aktualisierten Eigenschaften bereitstellt.

>[!TIP] Um den Erfolg dieser PUT-Anforderung sicherzustellen, wird empfohlen, zuerst eine GET-Anforderung zum Abrufen des Modells nach ID auszuführen. Ändern Sie dann das zurückgegebene JSON-Objekt und aktualisieren Sie es und wenden Sie die gesamte Eigenschaft des geänderten JSON-Objekts als Nutzlast für die PUT-Anforderung an.

**API-Format**

```http
PUT /models/{MODEL_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{MODEL_ID}` | Die Kennung des trainierten oder veröffentlichten Modells. |

**Anfrage**

```shell
curl -X PUT \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -d '{
        "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
        "name": "A name for this Model",
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "description": "An updated description for this Model",
        "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "updated": "2019-01-02T00:00:00.000Z"
    }'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Nutzlast mit den aktualisierten Details des Experiments zurück.

```json
{
        "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
        "name": "A name for this Model",
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "description": "An updated description for this Model",
        "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "updated": "2019-01-02T00:00:00.000Z"
    }
```

## Modell nach ID löschen

Sie können ein einzelnes DELETE löschen, indem Sie eine Anforderung ausführen, die die ID des Zielgruppe-Modells im Anforderungspfad enthält.

**API-Format**

```http
DELETE /models/{MODEL_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{MODEL_ID}` | Die Kennung des trainierten oder veröffentlichten Modells. |

**Anfrage**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Nutzlast mit dem Status 200 zurück, die das Löschen des Modells bestätigt.

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Model deletion was successful"
}
```

## Neue Transkodierung für ein Modell erstellen {#create-transcoded-model}

Transcodierung ist die direkte digitale Konvertierung einer Kodierung in eine andere. Sie erstellen eine neue Transkodierung für ein Modell, indem Sie die `{MODEL_ID}` und die `targetFormat` gewünschte neue Ausgabe angeben.

**API-Format**

```http
POST /models/{MODEL_ID}/transcodings
```

| Parameter | Beschreibung |
| --- | --- |
| `{MODEL_ID}` | Die Kennung des trainierten oder veröffentlichten Modells. |

**Anfrage**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: text/plain' \
    -D '{
 "id": "491a3be5-1d32-4541-94d5-cd1cd07affb5",
 "modelId" : "15c53796-bd6b-4e09-b51d-7296aa20af71",
 "targetFormat": "CoreML",
 "created": "2019-12-16T19:59:08.360Z",
 "createdBy": {
    "userId": "FDD760CD5CD467380A495FE2@AdobeID"
 },
 "updated": "2019-12-19T18:37:43.696Z",
 "deleted": false,
}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Nutzlast zurück, die ein JSON-Objekt mit den Informationen zur Transkodierung enthält. Dazu gehört die eindeutige Kennung der Transkodierung (`id`), die beim [Abrufen eines bestimmten transkodierten Modells](#retrieve-transcoded-model)verwendet wird.

```json
{
  "id": "491a3be5-1d32-4541-94d5-cd1cd07affb5",
  "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
  "targetFormat": "CoreML",
  "created": "2020-06-12T22:01:55.886Z",
  "createdBy": {
    "userId": "FDD760CD5CD467380A495FE2@AdobeID"
  },
  "updated": "2020-06-12T22:01:55.886Z",
  "deleted": false
}
```

## Abrufen einer Liste von Transkodierungen für ein Modell {#retrieve-transcoded-model-list}

Sie können eine Liste von Transkodierungen abrufen, die an einem Modell durchgeführt wurden, indem Sie eine GET-Anforderung mit Ihrem `{MODEL_ID}`Modell durchführen.

**API-Format**

```http
GET /models/{MODEL_ID}/transcodings
```

| Parameter | Beschreibung |
| --- | --- |
| `{MODEL_ID}` | Die Kennung des trainierten oder veröffentlichten Modells. |

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Nutzlast zurück, die ein JSON-Objekt mit einer Liste jeder im Modell durchgeführten Transkodierung enthält. Jedes transkodierte Modell erhält einen eindeutigen Bezeichner (`id`).

```json
{
    "children": [
        {
            "id": "460aa5a1-e972-455d-b8dc-4bc6cd91edb6",
            "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "created": "2019-12-20T01:07:50.978Z",
            "createdBy": {
                "userId": "FDD760CD5CD467380A495FE2@AdobeID"
            },
            "updated": "2019-12-20T01:07:50.978Z",
            "deprecated": false
        },
        {
            "id": "bdb3e4c2-4702-4045-86b4-17ee40df91cc",
            "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "created": "2019-12-20T17:48:26.473Z",
            "createdBy": {
                "userId": "FDD760CD5CD467380A495FE2@AdobeID"
            },
            "updated": "2019-12-20T17:48:26.473Z",
            "deprecated": false
        }
    ],
    "_page": {
        "property": "modelId==15c53796-bd6b-4e09-b51d-7296aa20af71,deleted==false,deprecated==false",
        "count": 2
    }
}
```

## Abrufen eines bestimmten transkodierten Modells {#retrieve-transcoded-model}

Sie können ein bestimmtes transkodiertes Modell abrufen, indem Sie eine GET-Anforderung mit Ihrer ID `{MODEL_ID}` und der ID eines transkodierten Modells ausführen.

**API-Format**

```http
GET /models/{MODEL_ID}/transcodings/{TRANSCODING_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{MODEL_ID}` | Die eindeutige Kennung eines trainierten oder veröffentlichten Modells. |
| `{TRANSCODING_ID}` | Die eindeutige Kennung eines transkodierten Modells. |

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings/460aa5a1-e972-455d-b8dc-4bc6cd91edb6 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Nutzlast zurück, die ein JSON-Objekt mit den Daten des transkodierten Modells enthält.

```json
{
    "id": "460aa5a1-e972-455d-b8dc-4bc6cd91edb6",
    "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
    "created": "2019-12-20T01:07:50.978Z",
    "createdBy": {
        "userId": "FDD760CD5CD467380A495FE2@AdobeID"
    },
    "updated": "2019-12-20T01:07:50.978Z",
    "deprecated": false
}
```


