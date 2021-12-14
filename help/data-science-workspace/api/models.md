---
keywords: Experience Platform; Entwicklerhandbuch; Endpunkt; Data Science Workspace; beliebte Themen; Modelle; Sensei Machine Learning API
solution: Experience Platform
title: API-Endpunkt der Modelle
topic-legacy: Developer guide
description: Ein Modell ist eine Instanz eines Rezepts für maschinelles Lernen, das mithilfe von historischen Daten und Konfigurationen dazu trainiert wird, eine geschäftliche Fragestellung zu lösen.
exl-id: e66119a9-9552-497c-9b3a-b64eb3b51fcf
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 65%

---

# Modelle-Endpunkt

Ein Modell ist eine Instanz eines Rezepts für maschinelles Lernen, das mithilfe von historischen Daten und Konfigurationen dazu trainiert wird, eine geschäftliche Fragestellung zu lösen.

## Abrufen einer Liste von Modellen

Sie können eine Liste mit Details zu den verfügbaren Modellen mittels GET-Anfrage an „/models“ abrufen. Standardmäßig wird diese Liste beginnend beim ältesten erstellten Modell sortiert und ist auf 25 Ergebnisse beschränkt. Sie können die Ergebnisse durch Angabe von Abfrageparametern filtern. Eine Liste der verfügbaren Abfragen finden Sie im Anhang zu den [Abfrageparametern für den Asset-Abruf](./appendix.md#query).

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

Bei erfolgreicher Antwort wird eine Payload mit Details zu Ihren Modellen einschließlich der eindeutigen Kennung (`id`) jedes einzelnen Modells zurückgegeben.

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
| `id` | Die dem Modell zugehörige ID. |
| `modelArtifactUri` | Ein URI, der angibt, wo das Modell gespeichert ist. Der URI endet mit dem Wert für `name` des Modells. |
| `experimentId` | Eine gültige Experiment-ID. |
| `experimentRunId` | Eine gültige Experimentablauf-ID. |

## Abrufen eines einzelnen Modells

Sie können eine Liste mit Details zu einem einzelnen Modell Modelldetails abrufen, indem Sie eine GET-Anfrage unter Angabe einer gültigen Modell-ID im Anfragepfad ausführen. Sie können die Ergebnisse filtern, indem Sie im Anfragepfad Abfrageparameter angeben. Eine Liste der verfügbaren Abfragen finden Sie im Anhang zu den [Abfrageparametern für den Asset-Abruf](./appendix.md#query).

**API-Format**

```http
GET /models/{MODEL_ID}
GET /models/?property=experimentRunID=={EXPERIMENT_RUN_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{MODEL_ID}` | Die Kennung des trainierten oder veröffentlichten Modells. |
| `{EXPERIMENT_RUN_ID}` | Die Kennung des Experiment-Laufs. |

**Anfrage**

Die nachfolgende Anfrage enthält eine Abfrage und ruft eine Liste trainierter Modelle ab, die dieselbe experimentRunID ({EXPERIMENT_RUN_ID}) verwenden.

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/?property=experimentRunId==33408593-2871-4198-a812-6d1b7d939cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei erfolgreicher Antwort wird eine Payload mit Details zu Ihrem Modell einschließlich der eindeutigen Kennung (`id`) des Modells zurückgegeben.

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
| `id` | Die dem Modell zugehörige ID. |
| `modelArtifactUri` | Ein URI, der angibt, wo das Modell gespeichert ist. Der URI endet mit dem Wert für `name` des Modells. |
| `experimentId` | Eine gültige Experiment-ID. |
| `experimentRunId` | Eine gültige Experimentablauf-ID. |

## Vorgeneriertes Modell registrieren {#register-a-model}

Sie können ein vorgeneriertes Modell registrieren, indem Sie eine POST-Anfrage an die `/models` -Endpunkt. Um Ihr Modell zu registrieren, muss die `modelArtifact` Datei und `model` -Eigenschaftswerte müssen im Hauptteil der Anfrage enthalten sein.

**API-Format**

```http
POST /models
```

**Anfrage**

Die folgende POST enthält die `modelArtifact` Datei und `model` benötigte Eigenschaftswerte. Weitere Informationen zu diesen Werten finden Sie in der Tabelle unten.

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
| `modelArtifact` | Der Speicherort des vollständigen Modellartefakts, das Sie einbeziehen möchten. |
| `model` | Die Formulardaten des Modellobjekts, das erstellt werden muss. |

**Antwort**

Bei erfolgreicher Antwort wird eine Payload mit Details zu Ihrem Modell einschließlich der eindeutigen Kennung (`id`) des Modells zurückgegeben.

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
| `id` | Die dem Modell zugehörige ID. |
| `modelArtifactUri` | Ein URI, der angibt, wo das Modell gespeichert ist. Der URI endet mit der `id` -Wert für Ihr Modell. |

## Aktualisieren des Modells nach ID

Sie können ein vorhandenes Modell aktualisieren, indem Sie seine Eigenschaften anhand einer PUT-Anfrage überschreiben, in der Sie die ID des entsprechenden Modells im Anfragepfad sowie eine JSON-Payload mit aktualisierten Eigenschaften angeben.

>[!TIP]
>
> Um sicherzustellen, dass diese PUT-Anfrage erfolgreich ausgeführt wird, wird empfohlen, das Modell zunächst mittels GET-Anfrage über seine ID abzurufen. Ändern und aktualisieren Sie dann das zurückgegebene JSON-Objekt und übernehmen Sie die Gesamtheit des geänderten JSON-Objekts als Payload für die PUT-Anfrage.

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

Bei erfolgreicher Antwort wird eine Payload mit den aktualisierten Details des Experiments zurückgegeben.

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

## Löschen des Modells nach ID

Sie können ein einzelnes Modell löschen, indem Sie eine DELETE-Anfrage ausführen, in der Sie die ID des entsprechenden Modells im Anfragepfad angeben.

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

Bei erfolgreicher Antwort wird eine Payload mit Status-Code 200 zurückgegeben, der das Löschen des Modells bestätigt.

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Model deletion was successful"
}
```

## Neue Transkodierung für ein Modell erstellen {#create-transcoded-model}

Transcodierung ist die direkte digitale Konvertierung einer Kodierung in eine andere. Sie erstellen eine neue Transkodierung für ein Modell, indem Sie die Variable `{MODEL_ID}` und `targetFormat` Sie möchten, dass sich die neue Ausgabe befindet.

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
 "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
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

Eine erfolgreiche Antwort gibt eine Payload zurück, die ein JSON-Objekt mit den Informationen Ihrer Transkodierung enthält. Dazu gehört die eindeutige Kennung der Transkodierungen (`id`) verwendet in [Abrufen eines bestimmten transkodierten Modells](#retrieve-transcoded-model).

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

## Liste von Transkodierungen für ein Modell abrufen {#retrieve-transcoded-model-list}

Sie können eine Liste von Transkodierungen abrufen, die für ein Modell durchgeführt wurden, indem Sie eine GET-Anfrage mit Ihrer `{MODEL_ID}`.

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

Eine erfolgreiche Antwort gibt eine Payload zurück, die ein JSON-Objekt mit einer Liste jeder auf dem Modell durchgeführten Transkodierung enthält. Jedes transkodierte Modell erhält eine eindeutige Kennung (`id`).

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

Sie können ein bestimmtes transkodiertes Modell abrufen, indem Sie eine GET-Anfrage mit Ihrer `{MODEL_ID}` und die ID eines transkodierten Modells.

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

Eine erfolgreiche Antwort gibt eine Payload zurück, die ein JSON-Objekt mit den Daten des transkodierten Modells enthält.

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
