---
keywords: Experience Platform;train and evaluate;Data Science Workspace;popular topics
solution: Experience Platform
title: Erstellen und Auswerten eines Modells (API)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a
workflow-type: tm+mt
source-wordcount: '1191'
ht-degree: 1%

---


# Erstellen und Auswerten eines Modells (API)


In diesem Lernprogramm erfahren Sie, wie Sie ein Modell mithilfe von API-Aufrufen erstellen, ausbilden und bewerten. Eine detaillierte Liste der API-Dokumentation finden Sie in [diesem Dokument](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) .

## Voraussetzungen

Folgen Sie dem [Importieren eines gepackten Rezepts mit der API](./import-packaged-recipe-api.md) zum Erstellen einer Engine, die zum Training und zum Auswerten eines Modells mit der API erforderlich ist.

Befolgen Sie diese [Übung](../../tutorials/authentication.md) zur Autorisierung von Beginn, die API-Aufrufe ausführen.

In der Übung sollten Sie nun die folgenden Werte haben:

- `{ACCESS_TOKEN}`: Ihr spezifischer Inhabertoken-Wert wird nach der Authentifizierung bereitgestellt.
- `{IMS_ORG}`: Ihre IMS-Organisationsberechtigungen finden Sie in Ihrer einzigartigen Adobe Experience Platform-Integration.
- `{API_KEY}`: Ihr spezifischer API-Schlüsselwert in Ihrer einzigartigen Adobe Experience Platform-Integration.

- Link zu einem Dockerbild eines intelligenten Dienstes

## API-Workflow

Wir werden die APIs verwenden, um einen Experimentlauf zur Schulung zu erstellen. Für dieses Tutorial konzentrieren wir uns auf die Endpunkte **Engines**, **MLInstances** und **Experiments** . Das folgende Diagramm zeigt die Beziehung zwischen den drei und stellt auch die Idee eines Run und eines Model vor.

![](../images/models-recipes/train-evaluate-api/engine_hierarchy_api.png)

>[!NOTE] Die Begriffe &quot;Engine&quot;, &quot;MLInstance&quot;, &quot;MLService&quot;, &quot;Experiment&quot;und &quot;Modell&quot;werden in der Benutzeroberfläche als unterschiedliche Begriffe bezeichnet. Wenn Sie von der Benutzeroberfläche kommen, werden die Unterschiede in der folgenden Tabelle zugeordnet.
> 
> | Begriff der Benutzeroberfläche | API-Begriff |
> --- | ---
> | Rezept | Engine |
> | Modell | MLInstance |
> | Schulungen | Experiment |
> | Service | MLService |



### Erstellen einer MLInstanz

Das Erstellen einer MLInstanz kann mit der folgenden Anforderung durchgeführt werden. Sie verwenden das `{ENGINE_ID}` , das beim Erstellen einer Engine aus dem [Importieren eines gepackten Rezepts mithilfe des API](./import-packaged-recipe-ui.md) -Lernprogramms zurückgegeben wurde.

**Anfrage**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/mlInstances \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d `{JSON_PAYLOAD}`
```

`{ACCESS_TOKEN}`: Ihr spezifischer Inhabertoken-Wert wird nach der Authentifizierung bereitgestellt.\
`{IMS_ORG}`: Ihre IMS-Organisationsberechtigungen finden Sie in Ihrer einzigartigen Adobe Experience Platform-Integration.\
`{API_KEY}`: Ihr spezifischer API-Schlüsselwert in Ihrer einzigartigen Adobe Experience Platform-Integration.\
`{JSON_PAYLOAD}`: Die Konfiguration unserer MLInstance. Das Beispiel, das wir in unserem Tutorial verwenden, ist hier dargestellt:

```JSON
{
    "name": "Retail - Instance",
    "description": "Instance for ML Instance",
    "engineId": "{ENGINE_ID}",
    "createdBy": {
        "displayName": "John Doe",
        "userId": "johnd"
    },
    "tags": {
        "purpose": "tutorial"
    },
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "numFeatures",
                    "value": "10"
                },
                {
                    "key": "maxIter",
                    "value": "2"
                },
                {
                    "key": "regParam",
                    "value": "0.15"
                },
                {
                    "key": "trainingDataLocation",
                    "value": "sample_training_data.csv"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "scoringDataLocation",
                    "value": "sample_scoring_data.csv"
                },
                {
                    "key": "scoringResultsLocation",
                    "value": "scoring_results.net"
                }
            ]
        }
    ]
}
```

>[!NOTE] Im `{JSON_PAYLOAD}`Array definieren wir Parameter, die für Schulungen und Scoring im `tasks` Array verwendet werden. Die `{ENGINE_ID}` ID der Engine, die Sie verwenden möchten, und das `tag` Feld ist ein optionaler Parameter, der zur Identifizierung der Instanz verwendet wird.

Die Antwort enthält die `{INSTANCE_ID}` , die die erstellte MLInstanz darstellt. Es können mehrere MLInstances mit verschiedenen Konfigurationen erstellt werden.

**Antwort**

```JSON
{
    "id": "{INSTANCE_ID}",
    "name": "Retail - Instance",
    "description": "Instance for ML Instance",
    "engineId": "{ENGINE_ID}",
    "created": "2018-21-21T11:11:11.111Z",
    "createdBy": {
        "displayName": "John Doe",
        "userId": "johnd"
    },
    "updated": "2018-21-01T11:11:11.111Z",
    "deleted": false,
    "tags": {
        "purpose": "tutorial"
    },
    "tasks": [
        {
            "name": "train",
            "parameters": [...]
        },
        {
            "name": "score",
            "parameters": [...]
        }
    ]
}
```

`{ENGINE_ID}`: Diese ID, die die Engine darstellt, unter der die MLInstanz erstellt wird.\
`{INSTANCE_ID}`: Die ID, die die MLInstanz darstellt.

### Experiment erstellen

Ein Experiment wird von einem Datenwissenschaftler verwendet, um während der Ausbildung ein leistungsfähiges Modell zu erreichen. Zu den verschiedenen Experimenten gehören das Ändern von Datensätzen, Funktionen, Lernparametern und Hardware. Im Folgenden finden Sie ein Beispiel zum Erstellen eines Experiments.

**Anfrage**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY' \
  -d `{JSON PAYLOAD}`
```

`{IMS_ORG}`: Ihre IMS-Organisationsberechtigungen finden Sie in Ihrer einzigartigen Adobe Experience Platform-Integration.\
`{ACCESS_TOKEN}`: Ihr spezifischer Inhabertoken-Wert wird nach der Authentifizierung bereitgestellt.\
`{API_KEY}`: Ihr spezifischer API-Schlüsselwert in Ihrer einzigartigen Adobe Experience Platform-Integration.\
`{JSON_PAYLOAD}`: Erstelltes Experimentobjekt. Das Beispiel, das wir in unserem Tutorial verwenden, ist hier dargestellt:

```JSON
{
    "name": "Experiment for Retail ",
    "mlInstanceId": "{INSTANCE_ID}",
    "tags": {
        "test": "guide"
    }
}
```

`{INSTANCE_ID}`: Die ID, die die MLInstanz darstellt.

Die Antwort aus der Experimenterstellung sieht wie folgt aus.

**Antwort**

```JSON
{
    "id": "{EXPERIMENT_ID}",
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "created": "2018-01-01T11:11:11.111Z",
    "updated": "2018-01-01T11:11:11.111Z",
    "deleted": false,
    "tags": {
        "test": "guide"
    }
}
```

`{EXPERIMENT_ID}`: Die ID, die das soeben erstellte Experiment darstellt.
`{INSTANCE_ID}`: Die ID, die die MLInstanz darstellt.

### Planes Experiment für eine Schulung erstellen

Geplante Experimente werden verwendet, damit nicht jede einzelne Experimentausführung über einen API-Aufruf erstellt werden muss. Stattdessen stellen wir alle notwendigen Parameter während der Experimenterstellung bereit und jeder Run wird regelmäßig erstellt.

Um die Erstellung eines geplanten Experiments anzuzeigen, müssen wir einen `template` Abschnitt im Hauptteil der Anforderung hinzufügen. In `template`der Tabelle sind alle erforderlichen Parameter für die Planung der Ausführung enthalten, z. B. `tasks`, die angeben, welche Aktion ausgeführt werden soll, und `schedule`die den Zeitpunkt der geplanten Ausführung angeben.

**Anfrage**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}`
```

`{IMS_ORG}`: Ihre IMS-Organisationsberechtigungen finden Sie in Ihrer einzigartigen Adobe Experience Platform-Integration.\
`{ACCESS_TOKEN}`: Ihr spezifischer Inhabertoken-Wert wird nach der Authentifizierung bereitgestellt.\
`{API_KEY}`: Ihr spezifischer API-Schlüsselwert in Ihrer einzigartigen Adobe Experience Platform-Integration.\
`{JSON_PAYLOAD}`: Zu veröffentlichender Datensatz. Das Beispiel, das wir in unserem Tutorial verwenden, ist hier dargestellt:

```JSON
{
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "template": {
        "tasks": [{
            "name": "train",
            "parameters": [
                   {
                        "value": "1000",
                        "key": "numFeatures"
                    }
            ],
            "specification": {
                "type": "SparkTaskSpec",
                "executorCores": 5,
                "numExecutors": 5
            }
        }],
        "schedule": {
            "cron": "*/20 * * * *",
            "startTime": "2018-11-11",
            "endTime": "2019-11-11"
        }
    }
}
```

Wenn wir ein Experiment erstellen, sollte der Körper entweder den `{JSON_PAYLOAD}`oder den `mlInstanceId` `mlInstanceQuery` Parameter enthalten. In diesem Beispiel ruft ein geplantes Experiment alle 20 Minuten eine Ausführung auf, die im `cron` Parameter festgelegt wird, beginnend mit dem `startTime` bis zum `endTime`.

**Antwort**

```JSON
{
    "id": "{EXPERIMENT_ID}",
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "created": "2018-11-11T11:11:11.111Z",
    "updated": "2018-11-11T11:11:11.111Z",
    "deleted": false,
    "workflowId": "endid123_0379bc0b_8f7e_4706_bcd9_1a2s3d4f5g_abcdf",
    "template": {
        "tasks": [
            {
                "name": "train",
                "parameters": [...],
                "specification": {
                    "type": "SparkTaskSpec",
                    "executorCores": 5,
                    "numExecutors": 5
                }
            }
        ],
        "schedule": {
            "cron": "*/20 * * * *",
            "startTime": "2018-07-04",
            "endTime": "2018-07-06"
        }
    }
}
```

`{EXPERIMENT_ID}`: Die ID, die das Experiment darstellt.\
`{INSTANCE_ID}`: Die ID, die die MLInstanz darstellt.


### Experimentlauf zur Schulung erstellen

Wenn eine Experimententität erstellt wurde, kann ein Schulungslauf mithilfe des nachfolgenden Aufrufs erstellt und ausgeführt werden. Sie benötigen den `{EXPERIMENT_ID}` und geben an, was `mode` Sie im Anforderungstext auslösen möchten.

**Anfrage**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{EXPERIMENT_ID}`: Die ID für das zu Zielgruppe Experiment. Dies finden Sie in der Antwort beim Erstellen Ihres Experiments.\
`{IMS_ORG}`: Ihre IMS-Organisationsberechtigungen finden Sie in Ihrer einzigartigen Adobe Experience Platform-Integration.\
`{ACCESS_TOKEN}`: Ihr spezifischer Inhabertoken-Wert wird nach der Authentifizierung bereitgestellt.\
`{API_KEY}`: Ihr spezifischer API-Schlüsselwert in Ihrer einzigartigen Adobe Experience Platform-Integration.\
`{JSON_PAYLOAD}`: Um einen Schulungslauf zu erstellen, müssen Sie Folgendes in den Text einschließen:

```JSON
{
    "mode":"Train"
}
```

Sie können die Konfigurationsparameter auch außer Kraft setzen, indem Sie ein `tasks` Array einfügen:

```JSON
{
   "mode":"Train",
   "tasks": [
        {
           "name": "train",
           "parameters": [
                {
                   "key": "numFeatures",
                   "value": "2"
                }
            ]
        }
    ]
}
```

Sie erhalten die folgende Antwort, die Sie über die Konfiguration `{EXPERIMENT_RUN_ID}` und die unter `tasks`.

**Antwort**

```JSON
{
    "id": "{EXPERIMENT_RUN_ID}",
    "mode": "train",
    "experimentId": "{EXPERIMENT_ID}",
    "created": "2018-01-01T11:11:11.903Z",
    "updated": "2018-01-01T11:11:11.903Z",
    "deleted": false,
    "tasks": [
        {
            "name": "Train",
            "parameters": [...]
        }
    ]
}
```

`{EXPERIMENT_RUN_ID}`:  Die ID, die den Experimentlauf darstellt.\
`{EXPERIMENT_ID}`: Die ID, die das Experiment darstellt, unter dem sich der Experimentlauf befindet.

### Abrufen des Status &quot;Experimentausführung&quot;

Der Status des Experimentlaufs kann mit dem `{EXPERIMENT_RUN_ID}`abgefragt werden.

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs/{EXPERIMENT_RUN_ID}/status \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}'
```

`{EXPERIMENT_ID}`: Die ID, die das Experiment darstellt.\
`{EXPERIMENT_RUN_ID}`: Die ID, die den Experimentlauf darstellt.\
`{ACCESS_TOKEN}`: Ihr spezifischer Inhabertoken-Wert wird nach der Authentifizierung bereitgestellt.\
`{IMS_ORG}`: Ihre IMS-Organisationsberechtigungen finden Sie in Ihrer einzigartigen Adobe Experience Platform-Integration.\
`{API_KEY}`: Ihr spezifischer API-Schlüsselwert in Ihrer einzigartigen Adobe Experience Platform-Integration.

**Antwort**

Der GET-Aufruf stellt den Status im `state` Parameter wie folgt bereit:

```JSON
{
    "id": "{EXPERIMENT_ID}",
    "name": "RunStatus for experimentRunId {EXPERIMENT_RUN_ID}",
    "experimentRunId": "{EXPERIMENT_RUN_ID}",
    "deleted": false,
    "status": {
        "tasks": [
            {
                "id": "{MODEL_ID}",
                "state": "DONE",
                "tasklogs": [
                    {
                        "name": "execution",
                        "url": "https://mlbaprod1sapwd7jzid.file.core.windows.net/..."
                    },
                    {
                        "name": "stderr",
                        "url": "https://mlbaprod1sapwd7jzid.file.core.windows.net/..."
                    },
                    {
                        "name": "stdout",
                        "url": "https://mlbaprod1sapwd7jzid.file.core.windows.net/..."
                    }
                ]
            }
        ]
    }
}
```

`{EXPERIMENT_RUN_ID}`:  Die ID, die den Experimentlauf darstellt.\
`{EXPERIMENT_ID}`: Die ID, die das Experiment darstellt, unter dem sich der Experimentlauf befindet.

Neben dem `DONE` Status gibt es auch folgende Status:
- `PENDING`
- `RUNNING`
- `FAILED`

Um weitere Informationen zu erhalten, finden Sie die detaillierten Protokolle unter dem `tasklogs` Parameter.

### Das geschulte Modell abrufen

Um das oben erstellte trainierte Modell während der Schulung zu erhalten, stellen wir folgende Anforderung an:

**Anfrage**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_RUN_ID}`: Die ID, die dem Experimentlauf entspricht, der Zielgruppe werden soll. Dies finden Sie in der Antwort beim Erstellen des Experimentlaufs.\
`{ACCESS_TOKEN}`: Ihr spezifischer Inhabertoken-Wert wird nach der Authentifizierung bereitgestellt.\
`{IMS_ORG}`: Ihre IMS-Organisationsberechtigungen finden Sie in Ihrer einzigartigen Adobe Experience Platform-Integration.

Die Antwort stellt das geschulte Modell dar, das erstellt wurde.

**Antwort**

```JSON
{
    "children": [
        {
            "id": "{MODEL_ID}",
            "name": "Tutorial trained Model",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
            "description": "trained model for ID",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/{MODEL_ID}",
            "created": "2018-01-01T11:11:11.011Z",
            "updated": "2018-01-01T11:11:11.011Z",
            "deleted": false
        }
    ],
    "_page": {
        "property": "ExperimentRunId=={EXPERIMENT_RUN_ID},deleted!=true",
        "count": 1
    }
}
```

`{MODEL_ID}`: Die dem Modell entsprechende ID.\
`{EXPERIMENT_ID}`:  Die ID, die dem Experiment entspricht, das der Experimentlauf durchführt, befindet sich unter.\
`{EXPERIMENT_RUN_ID}`: Die ID, die dem Experimentlauf entspricht.

### Beenden und Löschen eines geplanten Experiments

Wenn Sie die Ausführung eines geplanten Experiments vor dessen Ausführung beenden möchten, `endTime`können Sie eine DELETE-Anforderung an die `{EXPERIMENT_ID}`

**Anfrage**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_ID}`:  Die ID, die dem Experiment entspricht.\
`{ACCESS_TOKEN}`: Ihr spezifischer Inhabertoken-Wert wird nach der Authentifizierung bereitgestellt.\
`{IMS_ORG}`: Ihre IMS-Organisationsberechtigungen finden Sie in Ihrer einzigartigen Adobe Experience Platform-Integration.

>[!NOTE] Der API-Aufruf deaktiviert die Erstellung neuer Experimentausführungen. Die Ausführung bereits ausgeführter Experimentläufe wird jedoch nicht beendet.

Im Folgenden finden Sie die Antwort, die darauf hinweist, dass das Experiment erfolgreich gelöscht wurde.

**Antwort**

```JSON
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```

## Nächste Schritte

In diesem Lernprogramm wurde erläutert, wie die APIs genutzt werden können, um eine Engine, ein Experiment, geplante Experimentabläufe und trainierte Modelle zu erstellen. In der [nächsten Übung](./score-model-api.md)werden Sie Prognosen erstellen, indem Sie einen neuen Datensatz mit dem leistungsfähigsten geschulten Modell bewerten.