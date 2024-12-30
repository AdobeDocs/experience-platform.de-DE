---
title: Exportieren von Daten in externe ML-Umgebungen
description: Erfahren Sie, wie Sie einen mit Data Distiller erstellten vorbereiteten Trainings-Datensatz an einem Cloud-Speicherort freigeben, den Ihre ML-Umgebung zum Trainieren und Bewerten Ihres Modells lesen kann.
exl-id: 75022acf-fafd-41d6-8dfa-ff3fd4c4fa7e
source-git-commit: 7cde32f841497edca7de0c995cc4c14501206b1a
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 6%

---

# Exportieren von Daten in externe ML-Umgebungen

In diesem Dokument wird gezeigt, wie ein mit Data Distiller erstellter vorbereiteter Schulungsdatensatz an einem Cloud-Speicherort freigegeben wird, den Ihre ML-Umgebung zum Trainieren und Bewerten Ihres Modells lesen kann. Das folgende Beispiel exportiert den Trainings-Datensatz in die [Data Landing Zone (DLZ)](../../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md). Sie können das -Speicherziel nach Bedarf ändern, um mit Ihrer maschinellen Lernumgebung zu arbeiten.

Der [Flow Service für Ziele](https://developer.adobe.com/experience-platform-apis/references/destinations/) wird verwendet, um die Funktions-Pipeline abzuschließen, indem ein Datensatz mit berechneten Funktionen an einem entsprechenden Cloud-Speicherort abgelegt wird.

## Erstellen der Quellverbindung {#create-source-connection}

Die Quellverbindung ist für die Konfiguration der Verbindung zu Ihrem Adobe Experience Platform-Datensatz verantwortlich, sodass der resultierende Fluss genau weiß, wo nach den Daten gesucht werden soll und in welchem Format.

```python
from aepp import flowservice
flow_conn = flowservice.FlowService()

training_dataset_id = <YOUR_TRAINING_DATASET_ID>

source_res = flow_conn.createSourceConnectionDataLake(
    name=f"[CMLE] Featurized Dataset source connection created by {username}",
    dataset_ids=[training_dataset_id],
    format="parquet"
)
source_connection_id = source_res["id"]
```

## Erstellen der Zielverbindung {#create-target-connection}

Die Zielverbindung ist für die Verbindung mit dem Zieldateisystem verantwortlich. Dazu muss zunächst eine Basisverbindung zum Cloud-Speicherkonto (in diesem Beispiel die Data Landing Zone) und dann eine Zielverbindung zu einem bestimmten Dateipfad mit angegebenen Komprimierungs- und Formatoptionen erstellt werden.

Die verfügbaren Cloud-Speicher-Ziele werden jeweils durch eine Verbindungsspezifikations-ID identifiziert:

| Cloud-Speichertyp | Verbindungsspezifikations-ID |
|-----------------------|--------------------------------------|
| Amazon S3 | 4FCE964D-3F37-408F-9778-E597338A21EE |
| Azur Blob-Speicherung | 6d6b59bf-fb58-4107-9064-4d246c0e5bb2 |
| Azure Data Lake | be2c3209-53bc-47e7-ab25-145db8b873e1 |
| Data Landing Zone | 10440537-2a7b-4583-ac39-ed38d4b848e8 |
| Google Cloud Storage | c5d93acb-ea8b-4b14-8f53-02138444ae99 |
| SFTP | 36965A81-B1C6-401B-99F8-22508F1E6A26 |

```python
connection_spec_id = "10440537-2a7b-4583-ac39-ed38d4b848e8"
base_connection_res = flow_conn.createConnection(data={
    "name": "Base Connection to DLZ created by",
    "auth": None,
    "connectionSpec": {
        "id": connection_spec_id,
        "version": "1.0"
    }
})
base_connection_id = base_connection_res["id"]

target_res = flow_conn.createTargetConnection(
    data={
        "name": "Data Landing Zone target connection",
        "baseConnectionId": base_connection_id,
        "params": {
            "mode": "Server-to-server",
            "compression": config.get("Cloud", "compression_type"),
            "datasetFileType": config.get("Cloud", "data_format"),
            "path": config.get("Cloud", "export_path")
        },
        "connectionSpec": {
            "id": connection_spec_id,
            "version": "1.0"
        }
    }
)
target_connection_id = target_res["id"]
```

## Datenfluss erstellen {#create-data-flow}

Der letzte Schritt besteht darin, einen Datenfluss zwischen dem in der Quellverbindung angegebenen Datensatz und dem in der Zielverbindung angegebenen Zieldateipfad zu erstellen.

Jeder verfügbare Cloud-Speichertyp wird durch eine Flussspezifikations-ID identifiziert:

| Cloud-Speichertyp | Flussspezifikations-ID |
|-----------------------|--------------------------------------|
| Amazon S3 | 269BA276-16FC-47DB-92B0-C1049A3C131F |
| Azur Blob-Speicherung | 95bd8965-fc8a-4119-b9c3-944c2c2df6d2 |
| Azure Data Lake | 17be2013-2549-41ce-96e7-a70363bec293 |
| Data Landing Zone | cd2fc47e-e838-4f38-a581-8fff2f99b63a |
| Google Cloud Storage | 585c15c4-6cbf-4126-8f87-e26bff78b657 |
| SFTP | 354d6aad-4754-46e4-a576-1b384561c440 |

Der folgende Code erstellt einen Datenfluss mit einem Zeitplan, der weit in der Zukunft beginnen soll. Auf diese Weise können Sie Ad-hoc-Flüsse während der Modellentwicklung mit Triggern versehen. Sobald Sie über ein trainiertes Modell verfügen, können Sie den Zeitplan des Datenflusses aktualisieren, um den Funktionsdatensatz nach dem gewünschten Zeitplan freizugeben.

```python
import time

on_schedule = False
if on_schedule:
    schedule_params = {
        "interval": 3,
        "timeUnit": "hour",
        "startTime": int(time.time())
    }
else:
    schedule_params = {
        "interval": 1,
        "timeUnit": "day",
        "startTime": int(time.time() + 60*60*24*365) # Start the schedule far in the future
    }

flow_spec_id = "cd2fc47e-e838-4f38-a581-8fff2f99b63a"
flow_obj = {
    "name": "Flow for Feature Dataset to DLZ",
    "flowSpec": {
        "id": flow_spec_id,
        "version": "1.0"
    },
    "sourceConnectionIds": [
        source_connection_id
    ],
    "targetConnectionIds": [
        target_connection_id
    ],
    "transformations": [],
    "scheduleParams": schedule_params
}
flow_res = flow_conn.createFlow(
    obj = flow_obj,
    flow_spec_id = flow_spec_id
)
dataflow_id = flow_res["id"]
```

Nachdem der Datenfluss erstellt wurde, können Sie jetzt einen Trigger für eine Ad-hoc-Flussausführung erstellen, um den Funktionsdatensatz bei Bedarf freizugeben:

```python
from aepp import connector

connector = connector.AdobeRequest(
  config_object=aepp.config.config_object,
  header=aepp.config.header,
  loggingEnabled=False,
  logger=None,
)

endpoint = aepp.config.endpoints["global"] + "/data/core/activation/disflowprovider/adhocrun"

payload = {
    "activationInfo": {
        "destinations": [
            {
                "flowId": dataflow_id, 
                "datasets": [
                    {"id": created_dataset_id}
                ]
            }
        ]
    }
}

connector.header.update({"Accept":"application/vnd.adobe.adhoc.dataset.activation+json; version=1"})
activation_res = connector.postData(endpoint=endpoint, data=payload)
activation_res
```

## Optimierte Freigabe für Data Landing Zone

Um die Freigabe eines Datensatzes für die Data Landing Zone zu erleichtern, stellt die `aepp`-Bibliothek eine `exportDatasetToDataLandingZone` Funktion bereit, die die oben genannten Schritte in einem einzigen Funktionsaufruf ausführt:

```python
from aepp import exportDatasetToDataLandingZone

export = exportDatasetToDataLandingZone.ExportDatasetToDataLandingZone()

dataflow_id = export.createDataFlowRunIfNotExists(
    dataset_id = created_dataset_id,
    data_format = data_format, 
    export_path= export_path, 
    compression_type = compression_type, 
    on_schedule = False, 
    config_path = config_path, 
    entity_name = "Flow for Featurized Dataset to DLZ"
)
```

Dieser Code erstellt die Quellverbindung, die Zielverbindung und den Datenfluss basierend auf den bereitgestellten Parametern und führt in einem einzigen Schritt eine Ad-hoc-Ausführung des Datenflusses aus.
