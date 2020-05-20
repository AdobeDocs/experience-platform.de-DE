---
keywords: Experience Platform;Score a model;Data Science Workspace;popular topics
solution: Experience Platform
title: Modellbewertung (API)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 1%

---


# Modellbewertung (API)

In diesem Lernprogramm erfahren Sie, wie Sie die APIs nutzen, um ein Experiment und einen Experimentlauf zu erstellen. Eine detaillierte Liste der API-Dokumentation finden Sie in [diesem Dokument](https://www.adobe.io/apis/cloudplatform/dataservices/api-reference.html).

## Planes Experiment zur Bewertung erstellen

Ähnlich wie bei geplanten Experimenten für Schulungen erfolgt die Erstellung eines geplanten Experiments für die Bewertung auch durch Einbeziehung eines `template` Abschnitts in den Body-Parameter. Zusätzlich wird das `name` Feld unter `tasks` dem Körper als `score`.

Im Folgenden finden Sie ein Beispiel zum Erstellen eines Experiments, das alle 20 Minuten beginnt `startTime` und bis zum `endTime`.

**Anfrage**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{IMS_ORG}`: Ihre IMS-Organisationsberechtigungen finden Sie in Ihrer einzigartigen Adobe Experience Platform-Integration.\
`{ACCESS_TOKEN}`: Ihr spezifischer Inhabertoken-Wert wird nach der Authentifizierung bereitgestellt.\
`{API_KEY}`: Ihr spezifischer API-Schlüsselwert in Ihrer einzigartigen Adobe Experience Platform-Integration.\
`{JSON_PAYLOAD}`: Experimentlaufobjekt, das gesendet werden soll. Das Beispiel, das wir in unserem Tutorial verwenden, ist hier dargestellt:

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

`{INSTANCE_ID}`: Die ID, die die MLInstanz darstellt.\
`{MODEL_ID}`: Die ID, die das trainierte Modell darstellt.

Im Folgenden finden Sie die Antwort nach dem Erstellen des geplanten Experiments.

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
`{INSTANCE_ID}`: Die ID, die die MLInstanz darstellt.


### Experimentlauf zur Bewertung erstellen

Mit dem geschulten Modell können wir einen Experimentlauf zur Bewertung erstellen. Der Wert des `modelId` Parameters ist der `id` Parameter, der in der oben stehenden GET-Modell-Anforderung zurückgegeben wird.

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

`{IMS_ORG}`: Ihre IMS-Organisationsberechtigungen finden Sie in Ihrer einzigartigen Adobe Experience Platform-Integration.\
`{ACCESS_TOKEN}`: Ihr spezifischer Inhabertoken-Wert wird nach der Authentifizierung bereitgestellt.\
`{API_KEY}`: Ihr spezifischer API-Schlüsselwert in Ihrer einzigartigen Adobe Experience Platform-Integration.\
`{EXPERIMENT_ID}`: Die ID für das zu Zielgruppe Experiment. Dies finden Sie in der Antwort beim Erstellen Ihres Experiments.\
`{JSON_PAYLOAD}`: Zu veröffentlichende Daten. Das Beispiel, das wir in unserem Tutorial verwenden, ist hier:

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

`{MODEL_ID}`: Die dem Modell entsprechende ID.

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

`{EXPERIMENT_ID}`:  Die ID, die dem Experiment entspricht, unter dem die Ausführung läuft.\
`{EXPERIMENT_RUN_ID}`: Die ID, die dem soeben erstellten Experimentlauf entspricht.


### Abrufen des Status &quot;Experimentausführung&quot;für die geplante Experimentausführung

Um Experimentabläufe für geplante Experimente abzurufen, wird die Abfrage unten angezeigt:

**Anfrage**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_ID}`:  Die ID, die dem Experiment entspricht, unter dem die Ausführung läuft.\
`{ACCESS_TOKEN}`: Ihr spezifischer Inhabertoken-Wert wird nach der Authentifizierung bereitgestellt.\
`{IMS_ORG}`: Ihre IMS-Organisationsberechtigungen finden Sie in Ihrer einzigartigen Adobe Experience Platform-Integration.

Da es mehrere Experiment-ausgeführt werden, verfügt die zurückgegebene Antwort über ein Array von Ausführen-IDs.

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

`{EXPERIMENT_RUN_ID}`: Die ID, die dem Experimentlauf entspricht.\
`{EXPERIMENT_ID}`:  Die ID, die dem Experiment entspricht, unter dem die Ausführung läuft.

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
