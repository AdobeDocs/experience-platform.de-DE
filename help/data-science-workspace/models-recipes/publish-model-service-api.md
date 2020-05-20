---
keywords: Experience Platform;publish a model;Data Science Workspace;popular topics
solution: Experience Platform
title: Veröffentlichen eines Modells als Dienst (API)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c
workflow-type: tm+mt
source-wordcount: '1762'
ht-degree: 0%

---


# Veröffentlichen eines Modells als Dienst (API)

## Voraussetzungen

- Befolgen Sie diese [Übung](../../tutorials/authentication.md) zur Autorisierung von Beginn, die API-Aufrufe ausführen.
In der Übung sollten Sie nun über die folgenden Informationen verfügen:
   - `{ACCESS_TOKEN}`: Ihr spezifischer Inhabertoken-Wert wird nach der Authentifizierung bereitgestellt.
   - `{IMS_ORG}`: Ihre IMS-Organisationsberechtigungen finden Sie in Ihrer einzigartigen Adobe Experience Platform-Integration.
   - `{API_KEY}`: Ihr spezifischer API-Schlüsselwert in Ihrer einzigartigen Adobe Experience Platform-Integration.
- Dieses Lernprogramm erfordert vorhandene ML-Engine-, ML-Instanz- und Experimententitäten. Informationen zum Erstellen von ML-Engine-, ML-Instanz- oder -Experimententitäten finden Sie in diesem [Lernprogramm](./import-packaged-recipe-api.md) .
- Informationen zu den in diesem Lernprogramm erwähnten API-Endpunkten und -Anforderungen finden Sie in der vollständigen [Sensei Machine Learning API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml).

## Schlüsselbegriffe

In diesem Lernprogramm werden einige häufig verwendete Terminologie verwendet:

| Begriff | Definition |
--- | ---
| **Instanz für maschinelles Lernen (ML-Instanz)** | Die konzeptionelle Einheit, die eine Instanz einer Sensei Engine für einen bestimmten Mieter ist, bestehend aus bestimmten Daten, Parametern und Sensei-Code. |
| **Experiment** | Eine Dacheinheit für die Durchführung von Experimentübungen, Scoring Experiment Runs oder beides. |
| **Geplantes Experiment** | Ein Begriff, der die Automatisierung von Trainings- oder Bewertungsexperimenten beschreibt und von einem benutzerdefinierten Zeitplan bestimmt wird. |
| **Experimentausführung** | Eine bestimmte Instanz von Trainings- oder Bewertungsexperimenten. Mehrere Experimentabläufe eines bestimmten Experiments können sich von den für die Schulung oder Auswertung verwendeten Datensatzwerten unterscheiden. |
| **Auszubildendes Modell** | Ein maschinelles Lernmodell, das durch Experimentierungs- und Funktionstechnik erstellt wurde, bevor ein validiertes, evaluiertes und abgeschlossenes Modell erreicht wird. |
| **Veröffentlichtes Modell** | Nach Schulung, Validierung und Auswertung ist ein fertig definiertes und versioniertes Modell entstanden. |
| **Machine Learning Service (ML-Dienst)** | Eine als Dienst bereitgestellte ML-Instanz zur Unterstützung von On-Demand-Schulungs- und Bewertungsanfragen über einen Endpunkt. Beachten Sie, dass ein ML-Dienst auch mit vorhandenen, geschulten Experimentabläufen erstellt werden kann. |


## API-Workflow

In diesem Lernprogramm werden das Erstellen, Abrufen und Aktualisieren eines ML-Diensts erläutert.

## Erstellen eines ML-Diensts mit einem vorhandenen Schulungsexperiment Ausführen und planmäßiger Bewertung

Wenn Sie ein Schulungsexperiment als ML-Dienst veröffentlichen, können Sie die Bewertung planen, indem Sie Details zum Testlauf in `scoringSchedule` Ihrem {JSON_PAYLOAD} angeben. Dies führt zur Erstellung einer geplanten Experimententität für die Bewertung. Vergewissern Sie sich, dass die Werte `mlInstanceId`, `trainingExperimentId`, `trainingExperimentRunId`, `scoringDataSetId`und vorhanden sind und gültige Werte sind.

Um Beginn zu erhalten, stellen Sie eine `POST` Anforderung an `/mlServices`. Nachfolgend finden Sie ein Beispiel für einen Befehl zum Aufrollen:

**Anfrage**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -d '{JSON_PAYLOAD}'
```

- `{API_KEY}` : Ihr spezifischer API-Schlüsselwert in Ihrer einzigartigen Adobe Experience Platform-Integration.
- `{IMS_ORG}` :  Ihre IMS-Organisations-ID finden Sie unter den Integrationsdetails in der Adobe I/O-Konsole.
- `{ACCESS_TOKEN}` : Ihr spezifischer Inhabertoken-Wert wird nach der Authentifizierung bereitgestellt.
- `{JSON_PAYLOAD}` : Nachstehend finden Sie ein Beispiel für ein JSON-Nutzdatenformat:

```JSON
{
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingExperimentRunId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "scoringSchedule": {
    "startTime": "2019-03-13T00:00",
    "endTime": "2019-03-14T00:00",
    "cron": "30 * * * *"
  }
}
```

- `mlInstanceId` : Bestehende ML-Instanzidentifizierung, der zum Erstellen des ML-Diensts verwendete Schulungsexperimentlauf sollte dieser bestimmten ML-Instanz entsprechen.
- `trainingExperimentId` : Experimentkennung entsprechend der ML-Instanzkennung.
- `trainingExperimentRunId` : Ein bestimmtes Schulungsexperiment Ausführen, das zum Veröffentlichen des ML-Dienstes verwendet wird.
- `scoringDataSetId` : Identifikation, die sich auf den spezifischen Datensatz bezieht, der für geplante BewertungsexperimentLAUFEN verwendet werden soll.
- `scoringTimeframe` : Ein ganzzahliger Wert, der Minuten für das Filtern von Daten darstellt, die für die Bewertung von Experimentläufen verwendet werden sollen. Beispielsweise wird für jeden geplanten Testlauf ein Wert von `"10080"` &quot;bedeutet&quot;-Daten aus den letzten 10080 Minuten oder 168 Stunden verwendet. Beachten Sie, dass mit dem Wert von `"0"` nicht Daten gefiltert werden. Alle Daten im Datensatz werden für die Bewertung verwendet.
- `scoringSchedule` : Enthält Details zu geplanten Testläufen.
- `startTime` : definiert.
- `endTime` : definiert.
- `cron` : definiert.

**Antwort**

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

Aus der JSON-Antwort geht hervor, dass der Schlüssel `scoringExperimentId` mit dem zugehörigen Wert zusammen mit dem Experimentplan, den Sie in der `POST` Anforderung angegeben haben, ein neues Bewertungsexperiment erstellt wurde. Der `id` Schlüssel in der Antwort identifiziert eindeutig den erstellten ML-Dienst.

## Erstellen eines ML-Dienstes aus einer vorhandenen ML-Instanz

Je nach Anwendungsfall und Anforderungen ist das Erstellen eines ML-Dienstes mit einer ML-Instanz hinsichtlich der Planung von Schulungs- und BewertungsexperimentLAUFEN flexibel. In diesem Lernprogramm werden die spezifischen Fälle behandelt, in denen:

- [Sie benötigen keine geplante Schulung, sondern eine geplante Bewertung.](#ml-service-with-scheduled-experiment-for-scoring)
- [Sie benötigen geplante Experimentabläufe sowohl für Schulungen als auch für Punktbewertungen.](#ml-service-with-scheduled-experiments-for-training-and-scoring)

Beachten Sie, dass ein ML-Dienst mit einer ML-Instanz erstellt werden kann, ohne Schulungs- oder Bewertungsexperimente zu planen. Ein solcher ML-Dienst erstellt normale Experimententitäten und einen einzigen Experimentlauf für Schulung und Bewertung.

### ML-Dienst mit geplantem Experiment für die Bewertung {#ml-service-with-scheduled-experiment-for-scoring}

Das Erstellen eines ML-Diensts durch Veröffentlichen einer ML-Instanz mit geplanten Experimentabläufen für die Auswertung führt zur Erstellung einer normalen Experimententität für die Schulung. Der erstellte Schulungsexperimentlauf wird für alle geplanten Testläufe verwendet. Vergewissern Sie sich, dass Sie über die für die Erstellung des ML-Diensts erforderlichen Werte verfügen `mlInstanceId`, `trainingDataSetId`und diese `scoringDataSetId` benötigen und dass sie vorhanden sind und gültige Werte sind.

Um Beginn zu erhalten, stellen Sie eine `POST` Anforderung an `/mlServices`. Nachfolgend finden Sie ein Beispiel für einen Befehl zum Aufrollen:

**Anfrage**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -d '{JSON_PAYLOAD}'
```

- `{API_KEY}` : Ihr spezifischer API-Schlüsselwert in Ihrer einzigartigen Adobe Experience Platform-Integration.
- `{IMS_ORG}` :  Ihre IMS-Organisations-ID finden Sie unter den Integrationsdetails in der Adobe I/O-Konsole.
- `{ACCESS_TOKEN}` : Ihr spezifischer Inhabertoken-Wert wird nach der Authentifizierung bereitgestellt.
- `{JSON_PAYLOAD}` : Nachstehend finden Sie ein Beispiel für ein JSON-Nutzdatenformat:

```JSON
{
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
}
```

| JSON-Schlüssel | Beschreibung |
| --- | --- |
| **`mlInstanceId`** | Vorhandene ML-Instanz-ID, die die zur Erstellung des ML-Dienstes verwendete ML-Instanz darstellt. |
| **`trainingDataSetId`** | Identifikation, die sich auf den spezifischen Datensatz bezieht, der für das Schulungsexperiment verwendet werden soll. |
| **`trainingTimeframe`** | Ein ganzzahliger Wert, der Minuten zum Filtern von Daten darstellt, die für Schulungsexperimente verwendet werden sollen. Beispielsweise wird der Wert `"10080"` &quot;bedeutet&quot;Daten aus den letzten 10080 Minuten oder 168 Stunden für den Testlauf der Schulung verwendet. Beachten Sie, dass mit dem Wert von `"0"` nicht Daten gefiltert werden. Alle Daten im Datensatz werden für Schulungen verwendet. |
| **`scoringDataSetId`** | Identifikation, die sich auf den spezifischen Datensatz bezieht, der für geplante BewertungsexperimentLAUFEN verwendet werden soll. |
| **`scoringTimeframe`** | Ein ganzzahliger Wert, der Minuten für das Filtern von Daten darstellt, die für die Bewertung von Experimentläufen verwendet werden sollen. Beispielsweise wird für jeden geplanten Testlauf ein Wert von `"10080"` &quot;bedeutet&quot;-Daten aus den letzten 10080 Minuten oder 168 Stunden verwendet. Beachten Sie, dass mit dem Wert von `"0"` nicht Daten gefiltert werden. Alle Daten im Datensatz werden für die Bewertung verwendet. |
| **`scoringSchedule`** | Enthält Details zu geplanten Testläufen. |

**Antwort**

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

Aus der `JSON` Antwort geht hervor, dass die Schlüssel `trainingExperimentId` und der `scoringExperimentId` Vorschlag, dass für diesen ML-Dienst eine neue Entität für Training und Scoring Experiment erstellt wurde. Das Vorhandensein des `scoringSchedule` Objekts bezieht sich auf Details zum Zeitplan für die Auswertung von Experimenten. Der `id` Schlüssel in der Antwort bezieht sich auf den soeben erstellten ML-Dienst.

### ML-Dienst mit geplanten Experimenten für Schulung und Bewertung {#ml-service-with-scheduled-experiments-for-training-and-scoring}

Um eine vorhandene ML-Instanz als XML-Dienst mit geplanten Schulungs- und BewertungsexperimentLAUFEN zu veröffentlichen, müssen Sie Schulungs- und Bewertungszeitpläne bereitstellen. Wenn ein ML-Dienst dieser Konfiguration erstellt wird, werden auch geplante Experimententitäten für Schulung und Bewertung erstellt. Beachten Sie, dass Schulungs- und Bewertungszeitpläne nicht identisch sein müssen. Während der Ausführung eines Bewertungsauftrags wird das neueste geschulte Modell, das von geplanten Testlauf-Schulungen produziert wird, abgerufen und für die geplante Bewertungsausführung verwendet.

Um den ML-Dienst zu erstellen, stellen Sie eine `POST` Anforderung an `/mlServices` die `{JSON_PAYLOAD}` Darstellung des hinzuzufügenden ML-Dienstobjekts. Stellen Sie sicher, dass die Werte `mlInstanceId`, `trainingDataSetId`und `scoringDataSetId` vorhanden sind und gültige Werte sind.

**Anfrage**

```SHELL
curl -X POST "https://platform-int.adobe.io/data/sensei/mlServices" 
  -H "Authorization: Bearer {ACCESS_TOKEN}" 
  -H "x-api-key: {API_KEY}" 
  -H "x-gw-ims-org-id: {IMS_ORG}" 
  -d "{JSON_PAYLOAD}"
```

- `{API_KEY}` : Ihr spezifischer API-Schlüsselwert in Ihrer einzigartigen Adobe Experience Platform-Integration.
- `{IMS_ORG}` :  Ihre IMS-Organisations-ID finden Sie unter den Integrationsdetails in der Adobe I/O-Konsole.
- `{ACCESS_TOKEN}` : Ihr spezifischer Inhabertoken-Wert wird nach der Authentifizierung bereitgestellt.
- `{JSON_PAYLOAD}` : Nachstehend finden Sie ein Beispiel für ein JSON-Nutzdatenformat:

```JSON
{
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
}
```

| JSON-Schlüssel | Beschreibung |
| --- | --- |
| **`mlInstanceId`** | Vorhandene ML-Instanz-ID, die die zur Erstellung des ML-Dienstes verwendete ML-Instanz darstellt. |
| **`trainingDataSetId`** | Identifikation, die sich auf den spezifischen Datensatz bezieht, der für das Schulungsexperiment verwendet werden soll. |
| **`trainingTimeframe`** | Ein ganzzahliger Wert, der Minuten zum Filtern von Daten darstellt, die für Schulungsexperimente verwendet werden sollen. Beispielsweise wird der Wert `"10080"` &quot;bedeutet&quot;Daten aus den letzten 10080 Minuten oder 168 Stunden für den Testlauf der Schulung verwendet. Beachten Sie, dass mit dem Wert von `"0"` nicht Daten gefiltert werden. Alle Daten im Datensatz werden für Schulungen verwendet. |
| **`scoringDataSetId`** | Identifikation, die sich auf den spezifischen Datensatz bezieht, der für geplante BewertungsexperimentLAUFEN verwendet werden soll. |
| **`scoringTimeframe`** | Ein ganzzahliger Wert, der Minuten für das Filtern von Daten darstellt, die für die Bewertung von Experimentläufen verwendet werden sollen. Beispielsweise wird für jeden geplanten Testlauf ein Wert von `"10080"` &quot;bedeutet&quot;-Daten aus den letzten 10080 Minuten oder 168 Stunden verwendet. Beachten Sie, dass mit dem Wert von `"0"` nicht Daten gefiltert werden. Alle Daten im Datensatz werden für die Bewertung verwendet. |
| **`trainingSchedule`** | Enthält Details zu geplanten Testläufen für Schulungen. |
| **`scoringSchedule`** | Enthält Details zu geplanten Testläufen. |

**Antwort**

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

Die Hinzufügung von und `trainingExperimentId` `scoringExperimentId` im Reaktionsgremium deutet auf die Schaffung von Experimententitäten sowohl für die Ausbildung als auch für die Bewertung hin. Die Anwesenheit `trainingSchedule` und `scoringSchedule` der Hinweis, dass die oben genannten Experimententitäten für Schulung und Bewertung Experimente sind geplant. Der `id` Schlüssel in der Antwort bezieht sich auf den soeben erstellten ML-Dienst.

## Abrufen von ML-Diensten {#retrieving-ml-services}

Ein vorhandener ML-Dienst abzurufen ist so einfach, wie eine `GET` Anforderung an den `/mlServices` Endpunkt zu stellen. Stellen Sie sicher, dass die ML-Dienst-ID für den spezifischen ML-Dienst, den Sie abrufen möchten, vorhanden ist.

**Anfrage**

```SHELL
curl -X GET "https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}" 
  -H "Authorization: Bearer {ACCESS_TOKEN}" 
  -H "x-api-key: {API_KEY}" 
  -H "x-gw-ims-org-id: {IMS_ORG}" 
```

- `{API_KEY}` : Ihr spezifischer API-Schlüsselwert in Ihrer einzigartigen Adobe Experience Platform-Integration.
- `{IMS_ORG}` :  Ihre IMS-Organisations-ID finden Sie unter den Integrationsdetails in der Adobe I/O-Konsole.
- `{ACCESS_TOKEN}` : Ihr spezifischer Inhabertoken-Wert wird nach der Authentifizierung bereitgestellt.

**Antwort**

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

Die JSON-Antwort stellt das ML-Dienstobjekt dar. Dieses Objekt entspricht der Antwort für den Zeitpunkt, zu dem der ML-Dienst erstellt wird. Beachten Sie, dass beim Abrufen verschiedener ML-Dienste möglicherweise eine Antwort mit mehr oder weniger Schlüssel/Wert-Paaren zurückgegeben wird. Die obige Antwort ist eine Darstellung eines [ML-Dienstes mit geplanten Schulungs- und BewertungsexperimentLAUFEN](#ml-service-with-scheduled-experiments-for-training-and-scoring).


## Planen von Schulungen oder Bewertungen

Angenommen, Sie möchten die Bewertung und Schulung für einen bereits veröffentlichten ML-Dienst planen, indem Sie den vorhandenen ML-Dienst mit einer `PUT` Anforderung am aktualisieren `/mlServices`. Stellen Sie sicher, dass Sie die ML-Dienst-ID haben, die Sie aktualisieren möchten. Für Ihre Referenz ist das [Abrufen des zu aktualisierenden ML-Dienstes](#retrieving-ml-services) ein nützlicher erster Schritt.

**Anfrage**

```SHELL
curl -X PUT "https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}" 
  -H "Authorization: {ACCESS_TOKEN}" 
  -H "x-api-key: {API_KEY}" 
  -H "x-gw-ims-org-id: {IMS_ORG}" 
  -d "{JSON_PAYLOAD}"
```

- `{SERVICE_ID}` : Eindeutige Kennung, die sich auf den zu aktualisierenden ML-Dienst bezieht.
- `{API_KEY}` : Ihr spezifischer API-Schlüsselwert in Ihrer einzigartigen Adobe Experience Platform-Integration.
- `{IMS_ORG}` :  Ihre IMS-Organisations-ID finden Sie unter den Integrationsdetails in der Adobe I/O-Konsole.
- `{ACCESS_TOKEN}` : Ihr spezifischer Inhabertoken-Wert wird nach der Authentifizierung bereitgestellt.
- `{JSON_PAYLOAD}` : Nachstehend finden Sie ein Beispiel für ein JSON-Nutzdatenformat:

```JSON
{
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
}
```

Das Planen von Schulungen und Bewertungen kann durch Hinzufügen des `trainingSchedule` und `scoringSchedule` -Schlüssels mit den entsprechenden `startTime`, `endTime`und `cron` Schlüsseln durchgeführt werden.

>[!NOTE] die `PUT` Anforderungen an `mlServices` ermöglichen, Dienste mit bereits durchgeführten geplanten Experimenten zu ändern. Bitte **versuchen Sie nicht** , die Einstellung für bestehende geplante `startTime` Schulungen und Bewertungsarbeiten zu ändern. Wenn das Modell geändert werden `startTime` muss, sollten Sie dasselbe Modell veröffentlichen und Schulungs- und Bewertungsaufträge umplanen.

**Antwort**

Die Antwort ist die `{JSON_PAYLOAD}` aber mit zusätzlichen `id`, `created`und `updated` Tasten im Objekt.

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
