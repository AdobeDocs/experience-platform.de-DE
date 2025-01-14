---
keywords: Experience Platform;Modell veröffentlichen;Data Science Workspace;beliebte Themen;Sensei Machine Learning-API
solution: Experience Platform
title: Publish as a Cloud Service-Modell unter Verwendung der Sensei-API für maschinelles Lernen
type: Tutorial
description: In diesem Tutorial wird der Prozess zum Veröffentlichen eines Modells als Service mithilfe der Sensei-API für maschinelles Lernen beschrieben.
exl-id: f78b1220-0595-492d-9f8b-c3a312f17253
source-git-commit: 863889984e5e77770638eb984e129e720b3d4458
workflow-type: tm+mt
source-wordcount: '1541'
ht-degree: 44%

---

# Publish as a -Modell als Service unter Verwendung des [!DNL Sensei Machine Learning API]

>[!NOTE]
>
>Data Science Workspace ist nicht mehr erhältlich.
>
>Diese Dokumentation richtet sich an Bestandskunden mit vorherigen Berechtigungen für Data Science Workspace.

In diesem Tutorial wird der Prozess zum Veröffentlichen eines Modells als Service mithilfe der [[!DNL Sensei Machine Learning API]](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/) beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis von Adobe Experience Platform Data Science Workspace voraus. Workspace Bevor Sie mit diesem Tutorial beginnen, lesen Sie [Übersicht über Data Science ](../home.md)), um eine allgemeine Einführung in den Service zu erhalten.

Um diesem Tutorial folgen zu können, müssen Sie über eine vorhandene ML-Engine, ML-Instanz und ein vorhandenes Experiment verfügen. Anweisungen zum Erstellen dieser Rezepte in der API finden Sie im Tutorial [Importieren eines gepackten Rezepts](./import-packaged-recipe-api.md).

Bevor Sie mit diesem Tutorial beginnen, lesen Sie abschließend den Abschnitt [Erste Schritte](../api/getting-started.md) des Entwicklerhandbuchs , um wichtige Informationen zu erhalten, die Sie für die erfolgreiche Durchführung von Aufrufen an die [!DNL Sensei Machine Learning]-API benötigen, einschließlich der erforderlichen Kopfzeilen, die in diesem Tutorial verwendet werden:

- `{ACCESS_TOKEN}`
- `{ORG_ID}`
- `{API_KEY}`

Für alle POST-, PUT- und PATCH-Anfragen ist eine zusätzliche -Kopfzeile erforderlich:

- Content-Type: application/json

### Schlüsselbegriffe

In der folgenden Tabelle sind einige der in diesem Tutorial häufig verwendeten Begriffe aufgeführt:

| Begriff | Definition |
| --- | --- |
| **Machine Learning Instance (MLInstance)** | Eine Instanz einer [!DNL Sensei] Engine für einen bestimmten Mandanten, die bestimmte Daten, Parameter und [!DNL Sensei] enthält. |
| **Experiment** | Eine Dachentität für Schulungs-Experimentabläufe, Auswertungs-Experimentabläufe, oder beides. |
| **Geplantes Experiment** | Ein Begriff, der die Automatisierung von Schulungen oder Auswertungen von Experimentabläufen beschreibt und von einem benutzerdefinierten Zeitplan bestimmt wird. |
| **Experimentablauf** | Eine bestimmte Instanz von Experimenten-Schulungen oder -Auswertungen. Mehrere Experimentabläufe eines bestimmten Experiments können sich von den für die Schulung oder Auswertung verwendeten Datensatzwerten unterscheiden. |
| **Schulungsmodell** | Ein Machine Learning-Modell, das durch Experimentierungs- und Funktionstechnik erstellt wurde, bevor ein validiertes, ausgewertetes und abgeschlossenes Modell erreicht wird. |
| **Veröffentlichtes Modell** | Nach Schulung, Validierung und Auswertung ist ein fertig definiertes und versioniertes Modell entstanden. |
| **Machine Learning Service (ML-Dienst)** | Eine als Service bereitgestellte XML-Instanz zur Unterstützung von On-Demand-Anforderungen für Schulung und Bewertung mithilfe eines API-Endpunkts. Ein ML-Service kann auch mit vorhandenen trainierten Experimentausführungen erstellt werden. |

## Erstellen eines ML-Service mit einem vorhandenen Trainings-Experiment und geplanter Bewertung

Wenn Sie ein Trainings-Experiment veröffentlichen, das als ML-Service ausgeführt wird, können Sie die Bewertung planen, indem Sie Details zum Scoring-Experiment angeben und die Payload einer POST-Anfrage ausführen. Dies führt zur Erstellung einer Entität für das geplante Experiment zur Bewertung.

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
| `mlInstanceId` | Identifizieren Sie die vorhandene ML-Instanz. Der zum Erstellen des ML-Service verwendete Trainings-Experimentlauf sollte dieser bestimmten ML-Instanz entsprechen. |
| `trainingExperimentId` | Experimentidentifizierung, die der ML-Instanzidentifizierung entspricht. |
| `trainingExperimentRunId` | Ein bestimmtes Trainings-Experiment, das für die Veröffentlichung des ML-Service verwendet werden soll. |
| `scoringDataSetId` | Identifizierung, die sich auf den spezifischen Datensatz bezieht, der für geplante Auswertungs-Experimentabläufe verwendet werden soll. |
| `scoringTimeframe` | Ein ganzzahliger Wert, der Minuten für das Filtern von Daten darstellt, die für die Auswertungs-Experimentabläufen verwendet werden sollen. Beispielsweise wird für jeden geplanten Auswertungs-Experimentablauf ein Wert von `10080` verwendet, was Daten aus den letzten 10080 Minuten oder 168 Stunden bedeutet. Beachten Sie, dass mit dem Wert von `0` keine Daten gefiltert werden. Alle Daten im Datensatz werden für die Auswertung verwendet. |
| `scoringSchedule` | Enthält Details zu geplanten Auswertungs-Experimentabläufen. |
| `scoringSchedule.startTime` | Datum/Uhrzeit, das angibt, wann die Bewertung beginnen soll. |
| `scoringSchedule.endTime` | Datum/Uhrzeit, das angibt, wann die Bewertung beginnen soll. |
| `scoringSchedule.cron` | Cron-Wert, der das Intervall angibt, in dem die Experimentdurchgänge bewertet werden sollen. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details des neu erstellten ML-Service zurück, einschließlich der eindeutigen `id` und der `scoringExperimentId` für das entsprechende Scoring-Experiment.


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

## Erstellen eines ML-Service aus einer vorhandenen ML-Instanz

Je nach Ihrem spezifischen Anwendungsfall und Ihren Anforderungen ist die Erstellung eines ML-Service mit einer ML-Instanz in Bezug auf die Planung von Schulungs- und Scoring-Experimentausführungen flexibel. In diesem Tutorial werden die spezifischen Fälle behandelt, in denen:

- [Sie benötigen kein geplantes Training, sondern ein geplantes Scoring.](#ml-service-with-scheduled-experiment-for-scoring)
- [Sowohl für das Training als auch für die Bewertung sind geplante Experimentdurchgänge erforderlich.](#ml-service-with-scheduled-experiments-for-training-and-scoring)

Beachten Sie, dass ein ML-Service mit einer ML-Instanz erstellt werden kann, ohne Schulungs- oder Bewertungsexperimente zu planen. Solche ML-Services erstellen normale Experimententitäten und einen einzigen Experimentdurchgang für das Training und die Bewertung.

### ML-Dienst mit geplantem Experiment für die Auswertung {#ml-service-with-scheduled-experiment-for-scoring}

Sie können einen ML-Service erstellen, indem Sie eine ML-Instanz mit geplanten Experimentausführungen zur Bewertung veröffentlichen, wodurch eine normale Experimententität für das Training erstellt wird. Ein Trainings-Experimentdurchgang wird generiert und für alle geplanten Scoring-Experimentdurchgänge verwendet. Vergewissern Sie sich, dass Sie über `mlInstanceId`, `trainingDataSetId` und `scoringDataSetId` verfügen, die für das Erstellen des ML-Dienstes erforderlich sind und dass diese vorliegen und gültige Werte sind.

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
| `scoringSchedule.startTime` | Datum/Uhrzeit, das angibt, wann die Bewertung beginnen soll. |
| `scoringSchedule.endTime` | Datum/Uhrzeit, das angibt, wann die Bewertung beginnen soll. |
| `scoringSchedule.cron` | Cron-Wert, der das Intervall angibt, in dem die Experimentdurchgänge bewertet werden sollen. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details des neu erstellten ML-Service zurück. Dazu gehören die eindeutige `id` des Service sowie die `trainingExperimentId` und `scoringExperimentId` für die entsprechenden Schulungs- bzw. Bewertungsexperimente.

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

Um eine vorhandene ML-Instanz als ML-Service mit geplanten Trainings- und Scoring-Experimentausführungen zu veröffentlichen, müssen Sie sowohl Trainings- als auch Scoring-Zeitpläne bereitstellen. Wenn ein ML-Service dieser Konfiguration erstellt wird, werden auch geplante Experimententitäten für Training und Bewertung erstellt. Beachten Sie, dass Schulungs- und Auswertungszeitpläne nicht identisch sein müssen. Während der Ausführung eines Auswertungsauftrags wird das neueste geschulte Modell, das von geplanten Schulungs-Experimentabläufen produziert wird, abgerufen und für den geplanten Auswertungsablauf verwendet.

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
| `scoringSchedule.startTime` | Datum/Uhrzeit, das angibt, wann die Bewertung beginnen soll. |
| `scoringSchedule.endTime` | Datum/Uhrzeit, das angibt, wann die Bewertung beginnen soll. |
| `scoringSchedule.cron` | Cron-Wert, der das Intervall angibt, in dem die Experimentdurchgänge bewertet werden sollen. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details des neu erstellten ML-Service zurück. Dazu gehören die eindeutige `id` des Service sowie die `trainingExperimentId` und `scoringExperimentId` der entsprechenden Schulungs- bzw. Bewertungsexperimente. In der folgenden Beispielantwort legt das Vorhandensein von `trainingSchedule` und `scoringSchedule` nahe, dass die Experimententitäten für das Training und die Bewertung geplante Experimente sind.

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

## Suchen eines ML-Service {#retrieving-ml-services}

Sie können einen vorhandenen ML-Service suchen, indem Sie eine `GET`-Anfrage an `/mlServices` stellen und die eindeutige `id` des ML-Service im Pfad angeben.

**API-Format**

```http
GET /mlServices/{SERVICE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SERVICE_ID}` | Die eindeutige `id` des ML-Services, den Sie suchen. |

**Anfrage**

```SHELL
curl -X GET 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des ML-Service zurück.

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
>Das Abrufen verschiedener ML-Services kann eine Antwort mit mehr oder weniger Schlüssel-Wert-Paaren zurückgeben. Die obige Antwort ist eine Darstellung eines [ML-Dienstes mit geplanten Schulungs- und Auswertungs-Experimentabläufen](#ml-service-with-scheduled-experiments-for-training-and-scoring).


## Planen von Schulungen oder Auswertungen

Wenn Sie die Bewertung und Schulung für einen bereits veröffentlichten ML-Service planen möchten, können Sie dies tun, indem Sie den vorhandenen ML-Service mit einer `PUT` auf `/mlServices` aktualisieren.

**API-Format**

```http
PUT /mlServices/{SERVICE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SERVICE_ID}` | Die eindeutige `id` des ML-Services, den Sie aktualisieren. |

**Anfrage**

Mit der folgenden Anfrage wird ein Zeitplan für das Training und die Bewertung für einen vorhandenen ML-Service erstellt, indem die `trainingSchedule`- und `scoringSchedule`-Schlüssel mit den entsprechenden `startTime`-, `endTime`- und `cron`-Schlüsseln hinzugefügt werden.

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
>Versuchen Sie nicht, die `startTime` für bestehende geplante Schulungs- und Scoring-Aufträge zu ändern. Wenn die `startTime` geändert werden muss, sollten Sie erwägen, dasselbe Modell zu veröffentlichen und die Schulungs- und Auswertungsaufträge umzuplanen.

**Antwort**

Eine erfolgreiche Antwort gibt die Details des aktualisierten ML-Service zurück.

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
