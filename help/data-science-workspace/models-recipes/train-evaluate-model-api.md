---
keywords: Experience Platform; Schulung und Auswertung; Data Science Workspace; beliebte Themen; Sensei Machine Learning API
solution: Experience Platform
title: Modell mithilfe der Sensei Machine Learning API trainieren und bewerten
topic-legacy: tutorial
type: Tutorial
description: In diesem Tutorial erfahren Sie, wie Sie ein Modell mit Sensei Machine Learning-API-Aufrufen erstellen, trainieren und bewerten.
exl-id: 8107221f-184c-426c-a33e-0ef55ed7796e
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 92%

---

# Trainieren und Auswerten eines Modells mithilfe des [!DNL Sensei Machine Learning] API


In diesem Tutorial erfahren Sie, wie Sie ein Modell mithilfe von API-Aufrufen erstellen, dazu schulen und auswerten. Eine detaillierte Liste der API-Dokumentation finden Sie in [diesem Dokument](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml).

## Voraussetzungen

Folgen Sie dem [Importieren eines verpackten Rezepts mit der API](./import-packaged-recipe-api.md) zum Erstellen einer Engine, die zur Schulung und Auswertung für ein Modell mit der API erforderlich ist.

Befolgen Sie die [Tutorial zur Authentifizierung der Experience Platform-API](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) , um API-Aufrufe zu starten.

Sie sollten nun die folgenden Werte aus dem Tutorial haben:

- `{ACCESS_TOKEN}`: Ihr spezifischer Inhaber-Token-Wert, der nach der Authentifizierung bereitgestellt wird.
- `{ORG_ID}`: Ihre IMS-Organisationsberechtigungen in Ihrer eindeutigen Adobe Experience Platform-Integration.
- `{API_KEY}`: Ihr spezifischer API-Schlüsselwert in Ihrer eindeutigen Adobe Experience Platform-Integration.

- Link zu einem Docker-Bild eines intelligenten Dienstes

## API-Workflow

Wir verbrauchen die APIs, um einen Experimentablauf zu Schulungszwecken zu erstellen. Für dieses Tutorial konzentrieren wir uns auf die Endpunkte Engines, MLInstances und Experiments. Das folgende Diagramm zeigt die Beziehung zwischen diesen drei Punkten und stellt auch die Idee eines Ablaufs und eines Modells vor.

![](../images/models-recipes/train-evaluate-api/engine_hierarchy_api.png)

>[!NOTE]
>
> Die Begriffe „Engine“, „MLInstance“, „MLService“, „Experiment“ und „Modell“ werden in der Benutzeroberfläche als unterschiedliche Begriffe bezeichnet. Wenn Sie von der Benutzeroberfläche kommen, werden die Unterschiede in der folgenden Tabelle zugeordnet.

| UI-Begriff | API-Begriff |
| --- | --- |
| Rezept | Engine |
| Modell | MLInstance |
| Schulungsabläufe | Experiment |
| Service | MLService |

### Erstellen einer MLInstance

Das Erstellen einer MLInstance kann mit der folgenden Anfrage durchgeführt werden. Sie verwenden die `{ENGINE_ID}`, die beim Erstellen einer Engine aus dem [Importieren eines verpackten Rezepts mithilfe des API](./import-packaged-recipe-ui.md)-Tutorial zurückgegeben wurde.

**Anfrage**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/mlInstances \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d `{JSON_PAYLOAD}`
```

`{ACCESS_TOKEN}`: Ihr spezifischer Inhaber-Token-Wert, der nach der Authentifizierung bereitgestellt wird.\
`{ORG_ID}`: Ihre IMS-Organisationsberechtigungen in Ihrer eindeutigen Adobe Experience Platform-Integration.\
`{API_KEY}`: Ihr spezifischer API-Schlüsselwert in Ihrer eindeutigen Adobe Experience Platform-Integration.\
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

>[!NOTE]
>
> Im `{JSON_PAYLOAD}` definieren wir Parameter, die für Schulungen und Auswertungen im `tasks` Array verwendet werden. Die `{ENGINE_ID}` ist die ID der Engine, die Sie verwenden möchten, und das `tag`-Feld ist ein optionaler Parameter, der zur Identifizierung der Instanz verwendet wird.

Die Antwort enthält die `{INSTANCE_ID}` , die die erstellte MLInstance darstellt. Es können mehrere MLInstances mit verschiedenen Konfigurationen erstellt werden.

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

`{ENGINE_ID}`: Diese ID, die die Engine darstellt, unter der die MLInstance erstellt wird.\
`{INSTANCE_ID}`: Die ID, die die MLInstance darstellt.

### Erstellen eines Experiments

Ein Experiment wird von einem Datenwissenschaftler verwendet, um während der Schulung ein leistungsfähiges Modell zu erreichen. Zu den verschiedenen Experimenten gehören das Ändern von Datensätzen, Funktionen, Lernparametern und Hardware. Im Folgenden finden Sie ein Beispiel zum Erstellen eines Experiments.

**Anfrage**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY' \
  -d `{JSON PAYLOAD}`
```

`{ORG_ID}`: Ihre IMS-Organisationsberechtigungen in Ihrer eindeutigen Adobe Experience Platform-Integration.\
`{ACCESS_TOKEN}`: Ihr spezifischer Inhaber-Token-Wert, der nach der Authentifizierung bereitgestellt wird.\
`{API_KEY}`: Ihr spezifischer API-Schlüsselwert in Ihrer eindeutigen Adobe Experience Platform-Integration.\
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

`{INSTANCE_ID}`: Die ID, die die MLInstance darstellt.

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
`{INSTANCE_ID}`: Die ID, die die MLInstance darstellt.

### Erstellen eines geplanten Experiments zu Schulungszwecken

Geplante Experimente werden verwendet, damit nicht jeder einzelne Experimentablauf über einen API-Aufruf erstellt werden muss. Stattdessen stellen wir alle notwendigen Parameter während der Experimenterstellung bereit und jeder Ablauf wird regelmäßig erstellt.

Um die Erstellung eines geplanten Experiments anzuzeigen, müssen wir einen `template`-Abschnitt im Text der Anfrage hinzufügen. In der `template` sind alle erforderlichen Parameter für die Planung von Abläufen enthalten, z. B. `tasks`, die angeben, welche Aktion ausgeführt werden soll, und ein `schedule`, der den Zeitpunkt der geplanten Abläufe angibt.

**Anfrage**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}`
```

`{ORG_ID}`: Ihre IMS-Organisationsberechtigungen in Ihrer eindeutigen Adobe Experience Platform-Integration.\
`{ACCESS_TOKEN}`: Ihr spezifischer Inhaber-Token-Wert, der nach der Authentifizierung bereitgestellt wird.\
`{API_KEY}`: Ihr spezifischer API-Schlüsselwert in Ihrer eindeutigen Adobe Experience Platform-Integration.\
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

Wenn wir ein Experiment erstellen, sollte der Text, `{JSON_PAYLOAD}`, entweder den `mlInstanceId`- oder den `mlInstanceQuery`-Parameter enthalten. In diesem Beispiel ruft ein geplantes Experiment alle 20 Minuten einen Ablauf auf, der im `cron`-Parameter festgelegt wird, beginnend mit der `startTime` bis zur `endTime`.

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
`{INSTANCE_ID}`: Die ID, die die MLInstance darstellt.


### Erstellen eines Experimentablaufs für Schulungszwecke

Wenn eine Experiment-Entität erstellt wurde, kann ein Schulungsablauf mithilfe des nachfolgenden Aufrufs erstellt und ausgeführt werden. Sie benötigen die `{EXPERIMENT_ID}` und geben an, welchen `mode` Sie im Anfragetext auslösen möchten.

**Anfrage**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{EXPERIMENT_ID}`: Die dem Zielexperiment entsprechende Kennung. Diese finden Sie in der Antwort beim Erstellen Ihres Experiments.\
`{ORG_ID}`: Ihre IMS-Organisationsberechtigungen in Ihrer eindeutigen Adobe Experience Platform-Integration.\
`{ACCESS_TOKEN}`: Ihr spezifischer Inhaber-Token-Wert, der nach der Authentifizierung bereitgestellt wird.\
`{API_KEY}`: Ihr spezifischer API-Schlüsselwert in Ihrer eindeutigen Adobe Experience Platform-Integration.\
`{JSON_PAYLOAD}`: Um einen Schulungsablauf zu erstellen, müssen Sie Folgendes in den Text einschließen:

```JSON
{
    "mode":"Train"
}
```

Sie können die Konfigurationsparameter auch außer Kraft setzen, indem Sie ein `tasks`-Array einfügen:

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

Sie erhalten die folgende Antwort, die Sie über die `{EXPERIMENT_RUN_ID}` und die Konfiguration unter `tasks` informiert.

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

`{EXPERIMENT_RUN_ID}`:  Die ID, die den Experimentablauf darstellt.\
`{EXPERIMENT_ID}`: Die ID, die das Experiment darstellt, unter dem sich der Experimentablauf befindet.

### Abrufen eines Experimentablauf-Status

Der Status des Experimentablaufs kann mit der `{EXPERIMENT_RUN_ID}` abgefragt werden.

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs/{EXPERIMENT_RUN_ID}/status \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}'
```

`{EXPERIMENT_ID}`: Die ID, die das Experiment darstellt.\
`{EXPERIMENT_RUN_ID}`: Die ID, die den Experimentablauf darstellt.\
`{ACCESS_TOKEN}`: Ihr spezifischer Bearer-Tokenwert, der nach der Authentifizierung bereitgestellt wird.\
`{ORG_ID}`: Ihre IMS-Organisationsberechtigungen in Ihrer eindeutigen Adobe Experience Platform-Integration.\
`{API_KEY}`: Ihr spezifischer API-Schlüsselwert in Ihrer eindeutigen Adobe Experience Platform-Integration.

**Antwort**

Der GET-Aufruf stellt den Status im `state`-Parameter wie folgt bereit:

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

`{EXPERIMENT_RUN_ID}`:  Die ID, die den Experimentablauf darstellt.\
`{EXPERIMENT_ID}`: Die ID, die das Experiment darstellt, unter dem sich der Experimentablauf befindet.

Neben dem Status `DONE` gibt es auch folgende Status:
- `PENDING`
- `RUNNING`
- `FAILED`

Um weitere Informationen zu erhalten, finden Sie die detaillierten Protokolle unter dem Parameter `tasklogs`.

### Abrufen des Schulungsmodells

Um das oben erstellte Schulungsmodell während der Schulung zu erhalten, stellen wir folgende Anfrage:

**Anfrage**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_RUN_ID}`: Die dem Zielexperimentablauf entsprechende Kennung. Diese finden Sie in der Antwort beim Erstellen des Experimentablaufs.\
`{ACCESS_TOKEN}`: Ihr spezifischer Bearer-Tokenwert, der nach der Authentifizierung bereitgestellt wird.\
`{ORG_ID}`: Ihre IMS-Organisationsberechtigungen in Ihrer eindeutigen Adobe Experience Platform-Integration.

Die Antwort stellt das Schulungsmodell dar, das erstellt wurde.

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
`{EXPERIMENT_ID}`: Die Kennung, die dem Experiment entspricht, unter dem sich der Experimentablauf befindet.\
`{EXPERIMENT_RUN_ID}`: Die Kennung, die dem Experimentablauf entspricht.

### Beenden und Löschen eines geplanten Experiments

Wenn Sie die Ausführung eines geplanten Experiments vor dessen `endTime` abbrechen möchten, können Sie eine DELETE-Anfrage an die `{EXPERIMENT_ID}` senden

**Anfrage**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}`: Die Kennung, die dem Experiment entspricht.\
`{ACCESS_TOKEN}`: Ihr spezifischer Bearer-Tokenwert, der nach der Authentifizierung bereitgestellt wird.\
`{ORG_ID}`: Ihre IMS-Organisationsberechtigungen in Ihrer eindeutigen Adobe Experience Platform-Integration.

>[!NOTE]
>
> Der API-Aufruf deaktiviert die Erstellung neuer Experimentabläufe. Die Ausführung bereits ausgeführter Experimentabläufe wird jedoch nicht beendet.

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

In diesem Tutorial wurde erläutert, wie die APIs genutzt werden können, um eine Engine, ein Experiment, geplante Experimentabläufe und Schulungsmodelle zu erstellen. In der [nächsten Übung](./score-model-api.md) werden Sie Prognosen erstellen, indem Sie einen neuen Datensatz mit dem leistungsfähigsten Schulungsmodell auswerten.
