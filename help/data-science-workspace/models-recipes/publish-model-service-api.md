---
keywords: Experience Platform;publish a model;Data Science Workspace;popular topics
solution: Experience Platform
title: Veröffentlichen eines Modells als Dienst (API)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 4b0f0dda97f044590f55eaf75a220f631f3313ee
workflow-type: tm+mt
source-wordcount: '1478'
ht-degree: 1%

---


# Veröffentlichen eines Modells als Dienst (API)

Dieses Lernprogramm behandelt den Prozess der Veröffentlichung eines Modells als Dienst mit dem [!DNL Sensei Machine Learning API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml).

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der Adobe Experience Platform Data Science Workspace. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Übersicht über den [Data Science Workspace](../home.md) , um eine allgemeine Einführung in den Dienst zu erhalten.

Um mit diesem Lernprogramm fortzufahren, müssen Sie über eine vorhandene ML-Engine, ML-Instanz und ein Experiment verfügen. Anweisungen zum Erstellen dieser Skripten in der API finden Sie im Lernprogramm zum [Importieren eines zusammengestellten Skripts](./import-packaged-recipe-api.md).

Bevor Sie dieses Lernprogramm starten, lesen Sie abschließend den Abschnitt &quot; [Erste Schritte](../api/getting-started.md) &quot;im Entwicklerhandbuch nach wichtigen Informationen, die Sie für eine erfolgreiche Verwendung der [!DNL Sensei Machine Learning] API benötigen, einschließlich der erforderlichen Kopfzeilen, die in diesem Lernprogramm verwendet werden:

- `{ACCESS_TOKEN}`
- `{IMS_ORG}`
- `{API_KEY}`

Für alle POST-, PUT- und PATCH-Anforderungen ist ein zusätzlicher Header erforderlich:

- Content-Type: application/json

### Schlüsselbegriffe

In der folgenden Tabelle werden einige häufig verwendete Terminologie für dieses Lernprogramm aufgeführt:

| Begriff | Definition |
--- | ---
| **Instanz für maschinelles Lernen (ML-Instanz)** | Eine Instanz einer [!DNL Sensei] Engine für einen bestimmten Mandanten, die bestimmte Daten, Parameter und [!DNL Sensei] Code enthält. |
| **Experiment** | Eine Dacheinheit für die Durchführung von Experimentübungen, Scoring Experiment Runs oder beides. |
| **Geplantes Experiment** | Ein Begriff, der die Automatisierung von Trainings- oder Bewertungsexperimenten beschreibt und von einem benutzerdefinierten Zeitplan bestimmt wird. |
| **Experimentausführung** | Eine bestimmte Instanz von Trainings- oder Bewertungsexperimenten. Mehrere Experimentabläufe eines bestimmten Experiments können sich von den für die Schulung oder Auswertung verwendeten Datensatzwerten unterscheiden. |
| **Auszubildendes Modell** | Ein maschinelles Lernmodell, das durch Experimentierungs- und Funktionstechnik erstellt wurde, bevor ein validiertes, evaluiertes und abgeschlossenes Modell erreicht wird. |
| **Veröffentlichtes Modell** | Nach Schulung, Validierung und Auswertung ist ein fertig definiertes und versioniertes Modell entstanden. |
| **Machine Learning Service (ML-Dienst)** | Eine als Dienst bereitgestellte ML-Instanz, um On-Demand-Anforderungen für Schulungs- und Bewertungsaufgaben mithilfe eines API-Endpunkts zu unterstützen. Ein ML-Dienst kann auch mithilfe vorhandener, geschulter Experimentläufe erstellt werden. |

## Erstellen eines XML-Dienstes mit einem vorhandenen Schulungsexperiment Ausführen und geplanter Bewertung

Wenn Sie ein Schulungsexperiment mit Ausführung als ML-Dienst veröffentlichen, können Sie die Bewertung planen, indem Sie Details zum Bewertungsexperiment bereitstellen Führen Sie die Nutzlast einer POST-Anforderung aus. Dies führt zur Erstellung einer geplanten Experimententität für die Bewertung.

**API-Format**

```http
POST /mlServices
```

**Anfrage**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'Content-Type: application/json'
  -d '{
        "name": "Service name",
        "description": "Service description",
        "trainingExperimentId": "c4155146-b38f-4a8b-86d8-1de3838c8d87",
        "trainingExperimentRunId": "5c5af39c73fcec153117eed1",
        "scoringDataSetId": "5c5af39c73fcec153117eed1",
        "scoringTimeframe": "20000",
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        }
      }'
```

| Eigenschaft | Beschreibung |
--- | ---
| `mlInstanceId` | Bestehende ML-Instanzidentifizierung, der zum Erstellen des ML-Diensts verwendete Schulungsexperimentlauf sollte dieser bestimmten ML-Instanz entsprechen. |
| `trainingExperimentId` | Experimentkennung entsprechend der ML-Instanzkennung. |
| `trainingExperimentRunId` | Ein bestimmtes Schulungsexperiment Ausführen, das zum Veröffentlichen des ML-Dienstes verwendet wird. |
| `scoringDataSetId` | Identifikation, die sich auf den spezifischen Datensatz bezieht, der für geplante BewertungsexperimentLAUFEN verwendet werden soll. |
| `scoringTimeframe` | Ein ganzzahliger Wert, der Minuten für das Filtern von Daten darstellt, die für die Bewertung von Experimentläufen verwendet werden sollen. Beispielsweise wird für jeden geplanten Testlauf ein Wert von `10080` &quot;bedeutet&quot;-Daten aus den letzten 10080 Minuten oder 168 Stunden verwendet. Beachten Sie, dass mit dem Wert von `0` nicht Daten gefiltert werden. Alle Daten im Datensatz werden für die Bewertung verwendet. |
| `scoringSchedule` | Enthält Details zu geplanten Testläufen. |
| `scoringSchedule.startTime` | Zeitpunkt, der angibt, wann Beginn bewertet werden. |
| `scoringSchedule.endTime` | Zeitpunkt, der angibt, wann Beginn bewertet werden. |
| `scoringSchedule.cron` | Cron-Wert, der das Intervall angibt, in dem Experiment ausgeführt werden soll. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details des neu erstellten ML-Dienstes zurück, einschließlich seines eindeutigen Dienstes `id` und des zugehörigen `scoringExperimentId` Bewertungsexperiments.


```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingExperimentRunId": "string",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "scoringSchedule": {
    "startTime": "2019-03-13T00:00",
    "endTime": "2019-03-14T00:00",
    "cron": "30 * * * *"
  },
  "created": "2019-04-08T14:45:25.981Z",
  "updated": "2019-04-08T14:45:25.981Z"
}
```

## Erstellen eines ML-Dienstes aus einer vorhandenen ML-Instanz

Je nach Anwendungsfall und Anforderungen ist das Erstellen eines ML-Dienstes mit einer ML-Instanz hinsichtlich der Planung von Schulungs- und BewertungsexperimentLAUFEN flexibel. In diesem Lernprogramm werden die spezifischen Fälle behandelt, in denen:

- [Sie benötigen keine geplante Schulung, sondern eine geplante Bewertung.](#ml-service-with-scheduled-experiment-for-scoring)
- [Sie benötigen geplante Experimentabläufe sowohl für Schulungen als auch für Punktbewertungen.](#ml-service-with-scheduled-experiments-for-training-and-scoring)

Beachten Sie, dass ein ML-Dienst mit einer ML-Instanz erstellt werden kann, ohne Schulungs- oder Bewertungsexperimente zu planen. Solche ML-Dienste werden normale Experimententitäten und einen einzigen Experimentlauf zur Schulung und Bewertung erstellen.

### ML-Dienst mit geplantem Experiment für die Bewertung {#ml-service-with-scheduled-experiment-for-scoring}

Sie können einen ML-Dienst erstellen, indem Sie eine ML-Instanz mit geplanten Experimentabläufen für die Auswertung veröffentlichen, wodurch eine normale Experimententität für die Schulung erstellt wird. Ein Testlauf für Schulungen wird generiert und für alle geplanten Testläufe verwendet. Vergewissern Sie sich, dass Sie über die für die Erstellung des ML-Diensts erforderlichen Werte verfügen `mlInstanceId`, `trainingDataSetId`und diese `scoringDataSetId` benötigen und dass sie vorhanden sind und gültige Werte sind.

**API-Format**

```http
POST /mlServices
```

**Anfrage**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "name": "Service name",
        "description": "Service description",
        "mlInstanceId": "c4155146-b38f-4a8b-86d8-1de3838c8d87",
        "trainingDataSetId": "5c5af39c73fcec153117eed1",
        "trainingTimeframe": "10000",
        "scoringDataSetId": "5c5af39c73fcec153117eed1",
        "scoringTimeframe": "20000",
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        }
      }'
```

| JSON-Schlüssel | Beschreibung |
| --- | --- |
| `mlInstanceId` | Vorhandene ML-Instanz-ID, die die zur Erstellung des ML-Dienstes verwendete ML-Instanz darstellt. |
| `trainingDataSetId` | Identifikation, die sich auf den spezifischen Datensatz bezieht, der für das Schulungsexperiment verwendet werden soll. |
| `trainingTimeframe` | Ein ganzzahliger Wert, der Minuten zum Filtern von Daten darstellt, die für Schulungsexperimente verwendet werden sollen. Beispielsweise wird der Wert `"10080"` &quot;bedeutet&quot;Daten aus den letzten 10080 Minuten oder 168 Stunden für den Testlauf der Schulung verwendet. Beachten Sie, dass mit dem Wert von `"0"` nicht Daten gefiltert werden. Alle Daten im Datensatz werden für Schulungen verwendet. |
| `scoringDataSetId` | Identifikation, die sich auf den spezifischen Datensatz bezieht, der für geplante BewertungsexperimentLAUFEN verwendet werden soll. |
| `scoringTimeframe` | Ein ganzzahliger Wert, der Minuten für das Filtern von Daten darstellt, die für die Bewertung von Experimentläufen verwendet werden sollen. Beispielsweise wird für jeden geplanten Testlauf ein Wert von `"10080"` &quot;bedeutet&quot;-Daten aus den letzten 10080 Minuten oder 168 Stunden verwendet. Beachten Sie, dass mit dem Wert von `"0"` nicht Daten gefiltert werden. Alle Daten im Datensatz werden für die Bewertung verwendet. |
| `scoringSchedule` | Enthält Details zu geplanten Testläufen. |
| `scoringSchedule.startTime` | Zeitpunkt, der angibt, wann Beginn bewertet werden. |
| `scoringSchedule.endTime` | Zeitpunkt, der angibt, wann Beginn bewertet werden. |
| `scoringSchedule.cron` | Cron-Wert, der das Intervall angibt, in dem Experiment ausgeführt werden soll. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details des neu erstellten ML-Dienstes zurück. Dazu gehören die einzigartigen `id`und die entsprechenden Trainings- `trainingExperimentId` und `scoringExperimentId` Bewertungsexperimente.

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "created": "2019-04-09T08:58:10.956Z",
  "updated": "2019-04-09T08:58:10.956Z"
}
```

### ML-Dienst mit geplanten Experimenten für Schulung und Bewertung {#ml-service-with-scheduled-experiments-for-training-and-scoring}

Um eine vorhandene ML-Instanz als XML-Dienst mit geplanten Schulungs- und BewertungsexperimentLAUFEN zu veröffentlichen, müssen Sie Schulungs- und Bewertungszeitpläne bereitstellen. Wenn ein ML-Dienst dieser Konfiguration erstellt wird, werden auch geplante Experimententitäten für Schulung und Bewertung erstellt. Beachten Sie, dass Schulungs- und Bewertungszeitpläne nicht identisch sein müssen. Während der Ausführung eines Bewertungsauftrags wird das neueste geschulte Modell, das von geplanten Testlauf-Schulungen produziert wird, abgerufen und für die geplante Bewertungsausführung verwendet.

**API-Format**

```http
POST /mlServices
```

**Anfrage**

```SHELL
curl -X POST 'https://platform-int.adobe.io/data/sensei/mlServices' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "name": "string",
        "description": "string",
        "mlInstanceId": "string",
        "trainingDataSetId": "string",
        "trainingTimeframe": "string",
        "scoringDataSetId": "string",
        "scoringTimeframe": "string",
        "trainingSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        },
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        }
      }'
```

| JSON-Schlüssel | Beschreibung |
| --- | --- |
| `mlInstanceId` | Vorhandene ML-Instanz-ID, die die zur Erstellung des ML-Dienstes verwendete ML-Instanz darstellt. |
| `trainingDataSetId` | Identifikation, die sich auf den spezifischen Datensatz bezieht, der für das Schulungsexperiment verwendet werden soll. |
| `trainingTimeframe` | Ein ganzzahliger Wert, der Minuten zum Filtern von Daten darstellt, die für Schulungsexperimente verwendet werden sollen. Beispielsweise wird der Wert `"10080"` &quot;bedeutet&quot;Daten aus den letzten 10080 Minuten oder 168 Stunden für den Testlauf der Schulung verwendet. Beachten Sie, dass mit dem Wert von `"0"` nicht Daten gefiltert werden. Alle Daten im Datensatz werden für Schulungen verwendet. |
| `scoringDataSetId` | Identifikation, die sich auf den spezifischen Datensatz bezieht, der für geplante BewertungsexperimentLAUFEN verwendet werden soll. |
| `scoringTimeframe` | Ein ganzzahliger Wert, der Minuten für das Filtern von Daten darstellt, die für die Bewertung von Experimentläufen verwendet werden sollen. Beispielsweise wird für jeden geplanten Testlauf ein Wert von `"10080"` &quot;bedeutet&quot;-Daten aus den letzten 10080 Minuten oder 168 Stunden verwendet. Beachten Sie, dass mit dem Wert von `"0"` nicht Daten gefiltert werden. Alle Daten im Datensatz werden für die Bewertung verwendet. |
| `trainingSchedule` | Enthält Details zu geplanten Testläufen für Schulungen. |
| `scoringSchedule` | Enthält Details zu geplanten Testläufen. |
| `scoringSchedule.startTime` | Zeitpunkt, der angibt, wann Beginn bewertet werden. |
| `scoringSchedule.endTime` | Zeitpunkt, der angibt, wann Beginn bewertet werden. |
| `scoringSchedule.cron` | Cron-Wert, der das Intervall angibt, in dem Experiment ausgeführt werden soll. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details des neu erstellten ML-Dienstes zurück. Dazu gehören die einzigartigen `id`und die `trainingExperimentId` und `scoringExperimentId` die zugehörigen Trainings- bzw. Scoring-Experimente. In der unten stehenden Beispielantwort wird darauf hingewiesen, dass die Experimententitäten für Schulung und Bewertung geplante Experimente sind `trainingSchedule` und `scoringSchedule` darauf hindeuten.

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",,
  "scoringTimeframe": "integer",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "created": "2019-04-09T08:58:10.956Z",
  "updated": "2019-04-09T08:58:10.956Z"
}
```

## XML-Dienst suchen {#retrieving-ml-services}

Sie können einen vorhandenen ML-Dienst nachschlagen, indem Sie eine `GET` Anforderung an `/mlServices` und die eindeutige Angabe `id` des ML-Dienstes im Pfad ausführen.

**API-Format**

```http
GET /mlServices/{SERVICE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SERVICE_ID}` | Der einzigartige `id` von Ihnen gesuchte ML Service. |

**Anfrage**

```SHELL
curl -X GET 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des ML-Dienstes zurück.

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "created": "2019-05-13T23:46:03.478Z",
  "updated": "2019-05-13T23:46:03.478Z"
}
```

>[!NOTE] Beim Abrufen verschiedener ML-Dienste kann eine Antwort mit mehr oder weniger Schlüssel/Wert-Paaren zurückgegeben werden. Die obige Antwort ist eine Darstellung eines [ML-Dienstes mit geplanten Schulungs- und BewertungsexperimentLAUFEN](#ml-service-with-scheduled-experiments-for-training-and-scoring).


## Planen von Schulungen oder Bewertungen

Wenn Sie die Bewertung und Schulung für einen bereits veröffentlichten ML-Dienst planen möchten, können Sie dies tun, indem Sie den vorhandenen ML-Dienst mit einer `PUT` Anforderung am aktualisieren `/mlServices`.

**API-Format**

```http
PUT /mlServices/{SERVICE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SERVICE_ID}` | Der eindeutige `id` von Ihnen aktualisierte ML-Dienst. |

**Anfrage**

Mit der folgenden Anforderung werden Schulungen und Bewertungen für einen vorhandenen ML-Dienst geplant, indem die Schlüssel `trainingSchedule` und `scoringSchedule` Schlüssel mit ihren jeweiligen `startTime`, `endTime`und `cron` Schlüsseln hinzugefügt werden.

```SHELL
curl -X PUT 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "name": "string",
        "description": "string",
        "mlInstanceId": "string",
        "trainingExperimentId": "string",
        "trainingDataSetId": "string",
        "trainingTimeframe": "integer",
        "scoringExperimentId": "string",
        "scoringDataSetId": "string",
        "scoringTimeframe": "integer",
        "trainingSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-11T00:00",
          "cron": "20 * * * *"
        },
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-11T00:00",
          "cron": "20 * * * *"
        }
      }'
```

>[!WARNING] Versuchen Sie nicht, die `startTime` bei vorhandenen geplanten Schulungs- und Bewertungsaufträgen zu ändern. Wenn das Modell geändert werden `startTime` muss, sollten Sie dasselbe Modell veröffentlichen und Schulungs- und Bewertungsaufträge umplanen.

**Antwort**

Eine erfolgreiche Antwort gibt die Details des aktualisierten ML-Dienstes zurück.

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-11T00:00",
    "cron": "20 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-11T00:00",
    "cron": "20 * * * *"
  },
  "created": "2019-04-09T08:58:10.956Z",
  "updated": "2019-04-09T09:43:55.563Z"
}
```
