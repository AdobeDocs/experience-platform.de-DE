---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Modelle
topic: Developer guide
translation-type: tm+mt
source-git-commit: 01cfbc86516a05df36714b8c91666983f7a1b0e8
workflow-type: tm+mt
source-wordcount: '472'
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
            "id": "{MODEL_ID}",
            "name": "A name for this Model",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
            "description": "A description for this Model",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "{MODEL_ID}",
            "name": "Model 2",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
            "description": "A description for Model2",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "{MODEL_ID}",
            "name": "Model 3",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
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
  https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID} \
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
            "id": "{MODEL_ID}",
            "name": "A name for this Model",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
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
        "property": "experimentRunId=={EXPERIMENT_RUN_ID},deleted==false",
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
  https://platform.adobe.io/data/sensei/models/{MODEL_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -d '{
        "id": "{MODEL_ID}",
        "name": "A name for this Model",
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
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
        "id": "{MODEL_ID}",
        "name": "A name for this Model",
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
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

Sie können ein einzelnes Modell löschen, indem Sie eine DELETE-Anforderung ausführen, die die ID des Zielgruppe-Modells im Anforderungspfad enthält.

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
  https://platform.adobe.io/data/sensei/models/{MODEL_ID} \
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
