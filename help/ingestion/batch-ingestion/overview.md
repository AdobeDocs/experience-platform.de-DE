---
keywords: Experience Platform;home;popular topics;data ingestion;batch;Batch;enable dataset;Batch ingestion overview;overview;batch ingestion overview;
solution: Experience Platform
title: Batch-Erfassung in Adobe Experience Platform – Übersicht
topic: overview
description: Mit der Batch Ingestion-API können Sie Daten als Batch-Dateien in Adobe Experience Platform aufnehmen. Daten, die aufgenommen werden, können Profildaten aus einer reduzierten Datei in einem CRM-System (z. B. eine Parquet-Datei) oder Daten sein, die einem bekannten Schema in der Experience-Datenmodell (XDM)-Registry entsprechen.
translation-type: tm+mt
source-git-commit: c04fb056d4564e53f192e0734a700a13820f5ba7
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 83%

---


# [!DNL Batch Ingestion]Übersicht

The [!DNL Batch Ingestion] API allows you to ingest data into Adobe Experience Platform as batch files. Data being ingested can be the profile data from a flat file in a CRM system (such as a parquet file), or data that conforms to a known schema in the [!DNL Experience Data Model] (XDM) registry.

Der [Datenaufnahme-API-Verweis](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) enthält weitere Informationen zu diesen API-Aufrufen.

Das folgende Diagramm zeigt den Vorgang der Batch-Erfassung.

![](../images/batch-ingestion/overview/batch_ingestion.png)

## Verwenden der API

The [!DNL Data Ingestion] API allows you to ingest data as batches (a unit of data that consists of one or more files to be ingested as a single unit) into [!DNL Experience Platform] in three basic steps:

1. Erstellen eines neuen Batches.
2. Hochladen von Dateien in einen angegebenen Datensatz, der dem XDM-Schema der Daten entspricht.
3. Signalisieren des Batch-Endes.


### [!DNL Data Ingestion] Voraussetzungen

- Die hochzuladenden Daten müssen im Parquet- oder JSON-Format vorliegen.
- A dataset created in the [[!DNL Catalog services]](../../catalog/home.md).
- Der Inhalt der Parquet-Datei muss mit einer Untergruppe des Schemas des hochgeladenen Datensatzes übereinstimmen.
- Lassen Sie sich nach der Authentifizierung Ihr eindeutiges Zugriffstoken anzeigen.

### Best Practices zur Batch-Erfassung

- Die empfohlene Batch-Größe liegt zwischen 256 MB und 100 GB.
- Jeder Batch sollte maximal 1500 Dateien enthalten.

Um eine Datei hochzuladen, die größer als 512 MB ist, muss die Datei in kleinere Abschnitte unterteilt werden. Anweisungen zum Hochladen einer großen Datei finden Sie [hier](#large-file-upload---create-file).

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

- Content-Type: application/json

### Erstellen eines Batches

Bevor Daten zu einem Datensatz hinzugefügt werden können, müssen sie mit einem Batch verknüpft werden, der später in einen bestimmten Datensatz hochgeladen wird.

```http
POST /batches
```

**Anfrage**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
  -d '{ 
          "datasetId": "{DATASET_ID}" 
      }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `datasetId` | Die ID des Datensatzes, in den die Dateien hochgeladen werden sollen. |

**Antwort**

```JSON
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `id` | Die ID des soeben erstellten Batches (in nachfolgenden Anfragen verwendet). |
| `relatedObjects.id` | Die ID des Datensatzes, in den die Dateien hochgeladen werden sollen. |

## Datei-Upload

Nachdem Sie erfolgreich einen neuen Batch zum Hochladen erstellt haben, können Dateien in einen bestimmten Datensatz hochgeladen werden.

Sie können Dateien mit der **Small File Upload-API** hochladen. Wenn Ihre Dateien jedoch zu groß sind und das Gateway-Limit überschritten wird (z. B. längere Timeouts, Anfragen für überschrittene Dateigröße und andere Einschränkungen), können Sie zur **Large File Upload-API** wechseln. Diese API lädt die Datei in Teilen hoch und fügt die Daten mithilfe des Aufrufs **Large File Upload Complete-API** wieder zusammen.

>[!NOTE]
>
> Die folgenden Beispiele verwenden das [Parquet](https://parquet.apache.org/documentation/latest/)-Dateiformat. Ein Beispiel, das das JSON-Dateiformat verwendet, finden Sie im [Entwicklerhandbuch zur Batch-Erfassung](./api-overview.md).

### Hochladen von kleinen Dateien

Nachdem ein Batch erstellt wurde, können Daten in einen bereits vorhandenen Datensatz hochgeladen werden.  Die hochgeladene Datei muss mit dem referenzierten XDM-Schema übereinstimmen.

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{BATCH_ID}` | Die Batch-ID. |
| `{DATASET_ID}` | Die Datensatz-ID, in den Dateien hochgeladen werden sollen. |
| `{FILE_NAME}` | Der Dateiname, wie er im Datensatz angezeigt wird. |

**Anfrage**

```SHELL
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Pfad und Dateiname der Datei, die in den Datensatz hochgeladen werden soll. |

**Antwort**

```JSON
#Status 200 OK, with empty response body
```

### Hochladen großer Dateien – Datei erstellen

Um eine große Datei hochzuladen, muss die Datei in kleinere Abschnitte aufgeteilt und diese Abschnitte müssen einzeln hochgeladen werden.

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}?action=initialize
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{BATCH_ID}` | Die Batch-ID. |
| `{DATASET_ID}` | Die ID des Datensatzes, in den die Dateien aufgenommen werden. |
| `{FILE_NAME}` | Der Dateiname, wie er im Datensatz angezeigt wird. |

**Anfrage**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet?action=initialize" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Antwort**

```JSON
#Status 201 CREATED, with empty response body
```

### Hochladen großer Dateien – nachfolgende Teile hochladen

Nachdem die Datei erstellt wurde, können alle nachfolgenden Teile durch wiederholte PATCH-Anfragen hochgeladen werden, jeweils einen für jeden Abschnitt der Datei.

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{BATCH_ID}` | Die Batch-ID. |
| `{DATASET_ID}` | Die ID des Datensatzes, in den die Dateien hochgeladen werden sollen. |
| `{FILE_NAME}` | Dateiname, wie er im Datensatz angezeigt wird. |

**Anfrage**

```SHELL
curl -X PATCH "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "Content-Range: bytes {CONTENT_RANGE}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Pfad und Dateiname der Datei, die in den Datensatz hochgeladen werden soll. |

**Antwort**

```JSON
#Status 200 OK, with empty response
```

## Kennzeichnen der Fertigstellung eines Batches

Nachdem alle Dateien in den Batch hochgeladen wurden, kann dieser als fertiggestellt gekennzeichnet werden. By doing this, the [!DNL Catalog] **DataSetFile** entries are created for the completed files and associated with the batch generated above. The [!DNL Catalog] batch is then marked as successful, which triggers downstream flows to ingest the available data.

**Anfrage**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{BATCH_ID}` | Die ID des Batches, der in den Datensatz hochgeladen werden soll. |

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
-H "x-gw-ims-org-id: {IMS_ORG}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key : {API_KEY}"
```

**Antwort**

```JSON
#Status 200 OK, with empty response
```

## Prüfen des Batch-Status

Während darauf gewartet wird, dass die Dateien in den Batch hochgeladen werden, kann der Status des Stapels überprüft werden, um den Fortschritt zu sehen.

**API-Format**

```http
GET /batch/{BATCH_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{BATCH_ID}` | Die ID des geprüften Batches. |

**Anfrage**

```shell
curl GET "https://platform.adobe.io/data/foundation/catalog/batch/{BATCH_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

**Antwort**

```JSON
{
    "{BATCH_ID}": {
        "imsOrg": "{IMS_ORG}",
        "created": 1494349962314,
        "createdClient": "MCDPCatalogService",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1494349963467,
        "externalId": "{EXTERNAL_ID}",
        "status": "success",
        "errors": [
            {
                "code": "err-1494349963436"
            }
        ],
        "version": "1.0.3",
        "availableDates": {
            "startDate": 1337,
            "endDate": 4000
        },
        "relatedObjects": [
            {
                "type": "batch",
                "id": "foo_batch"
            },
            {
                "type": "connection",
                "id": "foo_connection"
            },
            {
                "type": "connector",
                "id": "foo_connector"
            },
            {
                "type": "dataSet",
                "id": "foo_dataSet"
            },
            {
                "type": "dataSetView",
                "id": "foo_dataSetView"
            },
            {
                "type": "dataSetFile",
                "id": "foo_dataSetFile"
            },
            {
                "type": "expressionBlock",
                "id": "foo_expressionBlock"
            },
            {
                "type": "service",
                "id": "foo_service"
            },
            {
                "type": "serviceDefinition",
                "id": "foo_serviceDefinition"
            }
        ],
        "metrics": {
            "foo": 1337
        },
        "tags": {
            "foo_bar": [
                "stuff"
            ],
            "bar_foo": [
                "woo",
                "baz"
            ],
            "foo/bar/foo-bar": [
                "weehaw",
                "wee:haw"
            ]
        },
        "inputFormat": {
            "format": "parquet",
            "delimiter": ".",
            "quote": "`",
            "escape": "\\",
            "nullMarker": "",
            "header": "true",
            "charset": "UTF-8"
        }
    }
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{USER_ID}` | Die ID des Benutzers, der den Batch erstellt oder aktualisiert hat. |

Das `"status"`-Feld zeigt den aktuellen Status des angeforderten Batches an. Die Batches können einen der folgenden Status haben:

## Batch-Erfassungstatus

| Status | Beschreibung |
| ------ | ----------- |
| Vorzeitig beendet | Der Batch wurde nicht im erwarteten Zeitrahmen fertiggestellt. |
| Abgebrochen | Für den angegebenen Stapel wurde **explizit** ein Unterbrechungsvorgang (über die Batch-Aufnahme-API) aufgerufen. Sobald sich ein Batch im Status **Geladen** befindet, kann der Batch nicht mehr abgebrochen werden. |
| Aktiv | Der Batch wurde erfolgreich gefördert und steht für den nachgelagerten Verbrauch zur Verfügung. Dieser Status kann synonym mit **Erfolg** verwendet werden. |
| Gelöscht | Die Daten für den Batch wurden vollständig entfernt. |
| Fehlgeschlagen | Ein Terminal-Status, der entweder auf eine fehlerhafte Konfiguration und/oder auf fehlerhafte Daten zurückzuführen ist. Daten für einen fehlgeschlagenen Batch werden **nicht** angezeigt. Dieser Status kann synonym mit **Fehler** verwendet werden. |
| Inaktiv | Der Batch wurde erfolgreich gefördert, wurde jedoch zurückgesetzt oder ist abgelaufen. Der Batch ist nicht mehr für den nachgelagerten Verbrauch verfügbar. |
| Geladen | Die Daten für den Batch sind abgeschlossen und der Stapel kann gefördert werden. |
| Wird geladen | Daten für diesen Batch werden hochgeladen und der Batch kann derzeit noch **nicht** gefördert werden. |
| Wird wiederholt | Die Daten für diesen Batch werden verarbeitet. Aufgrund eines System- oder vorübergehenden Fehlers ist der Batch jedoch fehlgeschlagen. Daher wird für diesen Batch ein erneuter Versuch unternommen. |
| Staging | Die Staging-Phase des Förderungsprozesses für einen Batch ist abgeschlossen und der Aufnahmeauftrag wurde ausgeführt. |
| Staging | Die Daten für den Batch werden verarbeitet. |
| Angehalten | Die Daten für den Batch werden verarbeitet. Die Batch-Förderung wurde jedoch nach einigen weiteren erneuten Versuchen angehalten. |