---
keywords: Experience Platform; Veröffentlichen eines Modells; Data Science Workspace; beliebte Themen; Sensei-API für maschinelles Lernen
solution: Experience Platform
title: Veröffentlichen eines Modells als Dienst mithilfe der Sensei Machine Learning API
type: Tutorial
description: In diesem Tutorial wird der Prozess der Veröffentlichung eines Modells als Dienst mit der Sensei Machine Learning-API behandelt.
exl-id: f78b1220-0595-492d-9f8b-c3a312f17253
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 49%

---

# Veröffentlichen eines Modells als Dienst mithilfe der [!DNL Sensei Machine Learning API]

In diesem Tutorial wird der Prozess zum Veröffentlichen eines Modells als Dienst mit dem [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml).

## Erste Schritte

Dieses Tutorial setzt ein grundlegendes Verständnis von Adobe Experience Platform Data Science Workspace voraus. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die [Data Science Workspace - Übersicht](../home.md) für eine allgemeine Einführung in den Dienst.

Um diesem Tutorial zu folgen, müssen Sie über eine vorhandene ML-Engine, MLInstance und ein vorhandenes Experiment verfügen. Anweisungen zum Erstellen dieser Komponenten in der API finden Sie im Tutorial zu [Importieren eines gepackten Rezepts](./import-packaged-recipe-api.md).

Bevor Sie mit diesem Tutorial beginnen, lesen Sie abschließend die [Erste Schritte](../api/getting-started.md) im Entwicklerhandbuch wichtige Informationen erhalten, die Sie benötigen, um erfolgreich Aufrufe an die [!DNL Sensei Machine Learning] API, einschließlich der erforderlichen Kopfzeilen, die in diesem Tutorial verwendet werden:

- `{ACCESS_TOKEN}`
- `{ORG_ID}`
- `{API_KEY}`

Für alle POST-, PUT- und PATCH-Anfragen ist eine zusätzliche Kopfzeile erforderlich:

- Content-Type: application/json

### Schlüsselbegriffe

In der folgenden Tabelle sind einige häufig verwendete Begriffe in diesem Tutorial aufgeführt:

| Begriff | Definition |
| --- | --- |
| **Machine Learning Instance (MLInstance)** | Eine Instanz eines [!DNL Sensei] Engine für einen bestimmten Mandanten, die bestimmte Daten, Parameter und [!DNL Sensei] Code. |
| **Experiment** | Eine Dachentität für Schulungs-Experimentabläufe, Auswertungs-Experimentabläufe, oder beides. |
| **Geplantes Experiment** | Ein Begriff, der die Automatisierung von Schulungen oder Auswertungen von Experimentabläufen beschreibt und von einem benutzerdefinierten Zeitplan bestimmt wird. |
| **Experimentablauf** | Eine bestimmte Instanz von Experimenten-Schulungen oder -Auswertungen. Mehrere Experimentabläufe eines bestimmten Experiments können sich von den für die Schulung oder Auswertung verwendeten Datensatzwerten unterscheiden. |
| **Schulungsmodell** | Ein Machine Learning-Modell, das durch Experimentierungs- und Funktionstechnik erstellt wurde, bevor ein validiertes, ausgewertetes und abgeschlossenes Modell erreicht wird. |
| **Veröffentlichtes Modell** | Nach Schulung, Validierung und Auswertung ist ein fertig definiertes und versioniertes Modell entstanden. |
| **Machine Learning Service (ML-Dienst)** | Eine als Dienst bereitgestellte MLInstance zur Unterstützung von On-Demand-Anfragen für Training und Scoring mithilfe eines API-Endpunkts. Ein ML-Dienst kann auch mithilfe vorhandener trainierter Experimentabläufe erstellt werden. |

## Erstellen eines ML-Dienstes mit einem vorhandenen Schulungs-Experimentablauf und geplanter Auswertung

Wenn Sie einen Schulungs-Experimentablauf als ML-Dienst veröffentlichen, können Sie die Auswertung planen, indem Sie Details für den Auswertungs-Experimentablauf angeben, um die Payload einer POST-Anfrage auszuführen. Dies führt zur Erstellung einer geplanten Experiment-Entität für die Auswertung.

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
  -H 'x-gw-ims-org-id: {ORG_ID}'
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
| --- | --- |
| `mlInstanceId` | Bestehende MLInstance-Identifizierung, der zum Erstellen des ML-Dienstes verwendete Schulungs-Experimentablauf sollte dieser bestimmten MLInstance entsprechen. |
| `trainingExperimentId` | Experimentidentifizierung entsprechend der MLInstance-Identifizierung. |
| `trainingExperimentRunId` | Ein bestimmter Schulungs-Experimentablauf, der zum Veröffentlichen des ML-Dienstes verwendet wird. |
| `scoringDataSetId` | Identifizierung, die sich auf den spezifischen Datensatz bezieht, der für geplante Auswertungs-Experimentabläufe verwendet werden soll. |
| `scoringTimeframe` | Ein ganzzahliger Wert, der Minuten für das Filtern von Daten darstellt, die für die Auswertungs-Experimentabläufen verwendet werden sollen. Beispielsweise wird für jeden geplanten Auswertungs-Experimentablauf ein Wert von `10080` verwendet, was Daten aus den letzten 10080 Minuten oder 168 Stunden bedeutet. Beachten Sie, dass mit dem Wert von `0` keine Daten gefiltert werden. Alle Daten im Datensatz werden für die Auswertung verwendet. |
| `scoringSchedule` | Enthält Details zu geplanten Auswertungs-Experimentabläufen. |
| `scoringSchedule.startTime` | Datum/Uhrzeit, der angibt, wann mit der Auswertung begonnen werden soll. |
| `scoringSchedule.endTime` | Datum/Uhrzeit, der angibt, wann mit der Auswertung begonnen werden soll. |
| `scoringSchedule.cron` | Cron-Wert, der angibt, nach welchem Intervall Experimentabläufe bewertet werden sollen. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details des neu erstellten ML-Dienstes zurück, einschließlich der eindeutigen `id` und `scoringExperimentId` für das entsprechende Scoring-Experiment.


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

## Erstellen eines ML-Dienstes aus einer vorhandenen MLInstance

Je nach Anwendungsfall und Anforderungen ist das Erstellen eines ML-Dienstes mit einer MLInstance hinsichtlich der Planung von Schulungs- und Auswertungs-Experimentabläufen flexibel. In diesem Tutorial werden die spezifischen Fälle behandelt, in denen:

- [Sie keine geplante Schulung benötigen, sondern eine geplante Auswertung.](#ml-service-with-scheduled-experiment-for-scoring)
- [Sie geplante Experimentabläufe sowohl für Schulungen als auch für Auswertungen benötigen.](#ml-service-with-scheduled-experiments-for-training-and-scoring)

Beachten Sie, dass ein ML-Dienst mit einer MLInstance erstellt werden kann, ohne Schulungs- oder Auswertungs-Experimente zu planen. Solche ML-Dienste erstellen normale Experiment-Entitäten und einen einzelnen Experimentablauf für Schulung und Auswertung.

### ML-Dienst mit geplantem Experiment für die Auswertung {#ml-service-with-scheduled-experiment-for-scoring}

Sie können einen ML-Dienst erstellen, indem Sie eine MLInstance mit geplanten Experimentabläufen für die Auswertung veröffentlichen, wodurch eine normale Experiment-Entität für die Schulung erstellt wird. Ein Schulungs-Experimentablauf wird generiert und für alle geplanten Auswertungs-Experimentabläufe verwendet. Vergewissern Sie sich, dass Sie über `mlInstanceId`, `trainingDataSetId` und `scoringDataSetId` verfügen, die für das Erstellen des ML-Dienstes erforderlich sind und dass diese vorliegen und gültige Werte sind.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' 
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
| `mlInstanceId` | Vorhandene MLInstance-Identifizierung, die die zur Erstellung des ML-Dienstes verwendete MLInstance darstellt. |
| `trainingDataSetId` | Identifizierung, die sich auf den spezifischen Datensatz bezieht, der für das Schulungsexperiment verwendet werden soll. |
| `trainingTimeframe` | Ein ganzzahliger Wert, der Minuten zum Filtern von Daten darstellt, die für Schulungsexperimente verwendet werden sollen. Beispielsweise wird für den Schulungs-Experimentablauf ein Wert von `"10080"` verwendet, was Daten aus den letzten 10080 Minuten oder 168 Stunden bedeutet. Beachten Sie, dass mit dem Wert von `"0"` keine Daten gefiltert werden. Alle Daten im Datensatz werden für die Schulung verwendet. |
| `scoringDataSetId` | Identifizierung, die sich auf den spezifischen Datensatz bezieht, der für geplante Auswertungs-Experimentabläufe verwendet werden soll. |
| `scoringTimeframe` | Ein ganzzahliger Wert, der Minuten für das Filtern von Daten darstellt, die für die Auswertungs-Experimentabläufen verwendet werden sollen. Beispielsweise wird für jeden geplanten Auswertungs-Experimentablauf ein Wert von `"10080"` verwendet, was Daten aus den letzten 10080 Minuten oder 168 Stunden bedeutet. Beachten Sie, dass mit dem Wert von `"0"` keine Daten gefiltert werden. Alle Daten im Datensatz werden für die Auswertung verwendet. |
| `scoringSchedule` | Enthält Details zu geplanten Auswertungs-Experimentabläufen. |
| `scoringSchedule.startTime` | Datum/Uhrzeit, der angibt, wann mit der Auswertung begonnen werden soll. |
| `scoringSchedule.endTime` | Datum/Uhrzeit, der angibt, wann mit der Auswertung begonnen werden soll. |
| `scoringSchedule.cron` | Cron-Wert, der angibt, nach welchem Intervall Experimentabläufe bewertet werden sollen. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details des neu erstellten ML-Dienstes zurück. Dies umfasst die eindeutige `id`sowie `trainingExperimentId` und `scoringExperimentId` für die entsprechenden Schulungs- bzw. Auswertungs-Experimente.

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

### ML-Dienst mit geplanten Experimenten für Schulung und Auswertung {#ml-service-with-scheduled-experiments-for-training-and-scoring}

Um eine vorhandene MLInstance als ML-Dienst mit geplanten Schulungs- und Auswertungs-Experimentabläufen zu veröffentlichen, müssen Sie Schulungs- und Auswertungszeitpläne bereitstellen. Wenn ein ML-Dienst dieser Konfiguration erstellt wird, werden auch geplante Experiment-Entitäten für Schulung und Auswertung erstellt. Beachten Sie, dass Schulungs- und Auswertungszeitpläne nicht identisch sein müssen. Während der Ausführung eines Auswertungsauftrags wird das neueste geschulte Modell, das von geplanten Schulungs-Experimentabläufen produziert wird, abgerufen und für den geplanten Auswertungsablauf verwendet.

**API-Format**

```http
POST /mlServices
```

**Anfrage**

```SHELL
curl -X POST 'https://platform.adobe.io/data/sensei/mlServices' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
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
| `mlInstanceId` | Vorhandene MLInstance-Identifizierung, die die zur Erstellung des ML-Dienstes verwendete MLInstance darstellt. |
| `trainingDataSetId` | Identifizierung, die sich auf den spezifischen Datensatz bezieht, der für das Schulungsexperiment verwendet werden soll. |
| `trainingTimeframe` | Ein ganzzahliger Wert, der Minuten zum Filtern von Daten darstellt, die für Schulungsexperimente verwendet werden sollen. Beispielsweise wird für den Schulungs-Experimentablauf ein Wert von `"10080"` verwendet, was Daten aus den letzten 10080 Minuten oder 168 Stunden bedeutet. Beachten Sie, dass mit dem Wert von `"0"` keine Daten gefiltert werden. Alle Daten im Datensatz werden für die Schulung verwendet. |
| `scoringDataSetId` | Identifizierung, die sich auf den spezifischen Datensatz bezieht, der für geplante Auswertungs-Experimentabläufe verwendet werden soll. |
| `scoringTimeframe` | Ein ganzzahliger Wert, der Minuten für das Filtern von Daten darstellt, die für die Auswertungs-Experimentabläufen verwendet werden sollen. Beispielsweise wird für jeden geplanten Auswertungs-Experimentablauf ein Wert von `"10080"` verwendet, was Daten aus den letzten 10080 Minuten oder 168 Stunden bedeutet. Beachten Sie, dass mit dem Wert von `"0"` keine Daten gefiltert werden. Alle Daten im Datensatz werden für die Auswertung verwendet. |
| `trainingSchedule` | Enthält Details zu geplanten Schulungs-Experimentabläufen. |
| `scoringSchedule` | Enthält Details zu geplanten Auswertungs-Experimentabläufen. |
| `scoringSchedule.startTime` | Datum/Uhrzeit, der angibt, wann mit der Auswertung begonnen werden soll. |
| `scoringSchedule.endTime` | Datum/Uhrzeit, der angibt, wann mit der Auswertung begonnen werden soll. |
| `scoringSchedule.cron` | Cron-Wert, der angibt, nach welchem Intervall Experimentabläufe bewertet werden sollen. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details des neu erstellten ML-Dienstes zurück. Dies umfasst die eindeutige `id`sowie `trainingExperimentId` und `scoringExperimentId` der entsprechenden Schulungs- und Auswertungsexperimente. In der folgenden Beispielantwort wird das Vorhandensein von `trainingSchedule` und `scoringSchedule` legt nahe, dass die Experiment-Entitäten für Schulung und Auswertung geplante Experimente sind.

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

## Suchen nach einem ML-Dienst {#retrieving-ml-services}

Sie können einen vorhandenen ML-Dienst nachschlagen, indem Sie einen `GET` Anfrage an `/mlServices` und die eindeutige `id` des ML-Dienstes im Pfad.

**API-Format**

```http
GET /mlServices/{SERVICE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SERVICE_ID}` | Die eindeutige `id` des ML-Dienstes, den Sie nachschlagen. |

**Anfrage**

```SHELL
curl -X GET 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
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

>[!NOTE]
>
>Beim Abrufen verschiedener ML-Dienste kann eine Antwort mit mehr oder weniger Schlüssel-Wert-Paaren zurückgegeben werden. Die obige Antwort ist eine Darstellung eines [ML-Dienstes mit geplanten Schulungs- und Auswertungs-Experimentabläufen](#ml-service-with-scheduled-experiments-for-training-and-scoring).


## Planen von Schulungen oder Auswertungen

Wenn Sie die Auswertung und Schulung für einen bereits veröffentlichten ML-Dienst planen möchten, können Sie dies tun, indem Sie den vorhandenen ML-Dienst mit einer `PUT` Anfrage an `/mlServices`.

**API-Format**

```http
PUT /mlServices/{SERVICE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SERVICE_ID}` | Die eindeutige `id` des ML-Dienstes, den Sie aktualisieren. |

**Anfrage**

Die folgende Anfrage plant das Training und Scoring für einen vorhandenen ML-Dienst, indem die `trainingSchedule` und `scoringSchedule` Schlüssel mit den entsprechenden `startTime`, `endTime`und `cron` Schlüssel.

```SHELL
curl -X PUT 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
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

>[!WARNING]
>
>Versuchen Sie nicht, die `startTime` für bestehende geplante Trainings- und Scoring-Aufträge. Wenn die `startTime` geändert werden muss, sollten Sie erwägen, dasselbe Modell zu veröffentlichen und die Schulungs- und Auswertungsaufträge umzuplanen.

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
