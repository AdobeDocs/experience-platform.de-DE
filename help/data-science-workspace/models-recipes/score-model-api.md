---
keywords: Experience Platform;Modell bewerten;Data Science Workspace;beliebte Themen;Sensei-API für maschinelles Lernen
solution: Experience Platform
title: Modellbewertung mit der Sensei Machine Learning API
topic-legacy: tutorial
type: Tutorial
description: In diesem Tutorial erfahren Sie, wie Sie die Sensei Machine Learning-APIs nutzen können, um ein Experiment und einen Experimentablauf zu erstellen.
exl-id: 202c63b0-86d8-4a82-8ec8-d144a8911d08
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 87%

---

# Score a model using [!DNL Sensei Machine Learning API]

In diesem Tutorial erfahren Sie, wie Sie die APIs nutzen können, um ein Experiment und einen Experimentlauf zu erstellen. Eine Liste aller Endpunkte der Sensei Machine Learning-API finden Sie unter [dieses Dokuments](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/).

## Geplantes Experiment für Scoring erstellen

Ähnlich wie bei geplanten Experimenten für das Training erfolgt die Erstellung eines geplanten Experiments für das Scoring ebenfalls durch Einbeziehung eines `template`-Abschnitts in den Textparameter. Außerdem wird das `name`-Feld unter `tasks` im Text auf `score` gesetzt.

Im Folgenden finden Sie ein Beispiel zum Erstellen eines Experiments, das ab `startTime` (Anfangszeit) alle 20 Minuten und bis `endTime` (Endzeit) ausgeführt.

**Anfrage**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{ORG_ID}`: Ihre IMS-Organisationsberechtigungen in Ihrer eindeutigen Adobe Experience Platform-Integration.\
`{ACCESS_TOKEN}`: Ihr spezifischer Inhaber-Token-Wert, der nach der Authentifizierung bereitgestellt wird.\
`{API_KEY}`: Ihr spezifischer API-Schlüsselwert in Ihrer eindeutigen Adobe Experience Platform-Integration.\
`{JSON_PAYLOAD}`: Das Objekt für den Experimentlauf, das gesendet werden soll. Das Beispiel, das wir in unserem Tutorial verwenden, ist hier dargestellt:

```JSON
{
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "template": {
        "tasks": [{
            "name": "score",
            "parameters": [
                {
                    "key": "modelId",
                    "value": "{MODEL_ID}"
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
            "startTime": "2018-07-04",
            "endTime": "2018-07-06"
        }
    }
}
```

`{INSTANCE_ID}`: Die ID, die die MLInstance darstellt.\
`{MODEL_ID}`: Die Kennung, die das trainierte Modell darstellt.

Im Folgenden sehen Sie die Antwort nach dem Erstellen des geplanten Experiments.

**Antwort**

```JSON
{
  "id": "{EXPERIMENT_ID}",
  "name": "Experiment for Retail",
  "mlInstanceId": "{INSTANCE_ID}",
  "created": "2018-11-11T11:11:11.111Z",
  "updated": "2018-11-11T11:11:11.111Z",
  "template": {
    "tasks": [
      {
        "name": "score",
        "parameters": [...],
        "specification": {
          "type": "SparkTaskSpec",
          "executorCores": 5,
          "numExecutors": 5
        }
      }
    ],
    "schedule": {
      "cron": "*\/20 * * * *",
      "startTime": "2018-07-04",
      "endTime": "2018-07-06"
    }
  }
}
```

`{EXPERIMENT_ID}`: Die ID, die das Experiment darstellt.\
`{INSTANCE_ID}`: Die ID, die die MLInstance darstellt.


### Experimentlauf zum Scoring erstellen

Mit dem trainierten Modell können wir nun einen Experimentlauf für das Scoring erstellen. Der Wert des `modelId`-Parameters ist der `id`-Parameter, der in der oben stehenden GET Model-Anfrage zurückgegeben wird.

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

`{ORG_ID}`: Ihre IMS-Organisationsberechtigungen in Ihrer eindeutigen Adobe Experience Platform-Integration.\
`{ACCESS_TOKEN}`: Ihr spezifischer Inhaber-Token-Wert, der nach der Authentifizierung bereitgestellt wird.\
`{API_KEY}`: Ihr spezifischer API-Schlüsselwert in Ihrer eindeutigen Adobe Experience Platform-Integration.\
`{EXPERIMENT_ID}`: Die dem Zielexperiment entsprechende Kennung. Diese finden Sie in der Antwort beim Erstellen Ihres Experiments.\
`{JSON_PAYLOAD}`: Zu veröffentlichende Daten. Das Beispiel, das wir in unserem Tutorial verwenden, lautet hier:

```JSON
{
   "mode":"score",
    "tasks": [
        {
            "name": "score",
            "parameters": [
                {
                    "key": "modelId",
                    "value": "{MODEL_ID}"
                }
            ]
        }
    ]
}
```

`{MODEL_ID}`: Die dem Modell entsprechende Kennung.

Die Antwort aus der Erstellung des Experimentlaufs ist unten dargestellt:

**Antwort**

```JSON
{
    "id": "{EXPERIMENT_RUN_ID}",
    "mode": "score",
    "experimentId": "{EXPERIMENT_ID}",
    "created": "2018-01-01T11:11:11.011Z",
    "updated": "2018-01-01T11:11:11.011Z",
    "deleted": false,
    "tasks": [
        {
            "name": "score",
            "parameters": [...]
        }
    ]
}
```

`{EXPERIMENT_ID}`: Die Kennung, die dem Experiment entspricht, unter dem der Lauf ausgeführt wird.\
`{EXPERIMENT_RUN_ID}`: Die Kennung, die dem soeben erstellten Experimentablauf entspricht.


### Experimentlaufstatus für geplanten Experimentlauf abrufen

Die Abfrage zum Abrufen von Experimentläufen für geplante Experimente wird im Folgenden dargestellt:

**Anfrage**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}`: Die Kennung, die dem Experiment entspricht, unter dem der Lauf ausgeführt wird.\
`{ACCESS_TOKEN}`: Ihr spezifischer Bearer-Token-Wert, der nach der Authentifizierung bereitgestellt wird.\
`{ORG_ID}`: Die Anmeldeinformationen für Ihre IMS-Organisation in Ihrer eindeutigen Adobe Experience Platform-Integration.

Da es mehrere Experimentläufe für ein spezifisches Experiment gibt, verfügt die zurückgegebene Antwort über verschiedene Ausführungskennungen.

**Antwort**

```JSON
{
    "children": [
        {
            "id": "{EXPERIMENT_RUN_ID}",
            "experimentId": "{EXPERIMENT_ID}",
            "created": "2018-01-01T11:11:11.011Z",
            "updated": "2018-01-01T11:11:11.011Z"
        },
        {
            "id": "{EXPERIMENT_RUN_ID}",
            "experimentId": "{EXPERIMENT_ID}",
            "created": "2018-01-01T11:11:11.011Z",
            "updated": "2018-01-01T11:11:11.011Z"
        }
    ]
}
```

`{EXPERIMENT_RUN_ID}`: Die Kennung, die dem Experimentablauf entspricht.\
`{EXPERIMENT_ID}`: Die Kennung, die dem Experiment entspricht, unter dem der Lauf ausgeführt wird.

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
