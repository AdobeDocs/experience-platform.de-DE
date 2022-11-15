---
keywords: Experience Platform; Startseite; beliebte Themen; Batch-Erfassung; Batch-Erfassung; Erfassung; Entwicklerhandbuch; API-Handbuch; Hochladen; Parquet erfassen; JSON erfassen erfassen;
solution: Experience Platform
title: Handbuch zur Batch Ingestion-API
description: Dieses Dokument enthält eine umfassende Anleitung für Entwickler, die mit Batch-Aufnahme-APIs für Adobe Experience Platform arbeiten.
exl-id: 4ca9d18d-1b65-4aa7-b608-1624bca19097
source-git-commit: 49281d6ef959c84c3da964f0a9e19859fd8901a5
workflow-type: tm+mt
source-wordcount: '2413'
ht-degree: 77%

---

# Entwicklerhandbuch zur Batch-Erfassung

Dieses Dokument enthält eine umfassende Anleitung zur Verwendung von [API-Endpunkte für die Batch-Erfassung](https://www.adobe.io/experience-platform-apis/references/data-ingestion/#tag/Batch-Ingestion) in Adobe Experience Platform. Einen Überblick über Batch-Aufnahme-APIs, einschließlich Voraussetzungen und Best Practices, erhalten Sie im Abschnitt [Batch-Aufnahme-API - Übersicht](overview.md).

Der Anhang zu diesem Dokument enthält Informationen zur [Formatierung von Daten, die zur Erfassung verwendet werden sollen](#data-transformation-for-batch-ingestion), einschließlich Beispiel-CSV- und JSON-Datendateien.

## Erste Schritte

Die in diesem Handbuch verwendeten API-Endpunkte sind Teil der [Datenerfassungs-API](https://www.adobe.io/experience-platform-apis/references/data-ingestion/). Data Ingestion bietet eine RESTful-API, mit der Sie bei unterstützten Objekttypen grundlegende CRUD-Vorgänge durchführen können.

Bevor Sie fortfahren, lesen Sie bitte die [Batch-Aufnahme-API - Übersicht](overview.md) und [Erste Schritte](getting-started.md).

## JSON-Dateien erfassen

>[!NOTE]
>
> Die folgenden Schritte gelten für kleine Dateien (256 MB oder weniger). Wenn Sie einen Gateway-Timeout erreichen oder Fehler wegen der Größe des Anfragetexts erhalten, müssen Sie zum Upload großer Dateien wechseln.

### Batch erstellen

Zunächst müssen Sie einen Batch erstellen, wobei JSON als Eingabeformat dient. Beim Erstellen des Batches müssen Sie eine Datensatz-ID angeben. Außerdem müssen Sie sicherstellen, dass alle im Batch hochgeladenen Dateien mit dem XDM-Schema übereinstimmen, das mit dem bereitgestellten Datensatz verknüpft ist.

>[!NOTE]
>
> Die folgenden Beispiele stehen für einzeilige JSON-Dateien. Um mehrzeilige JSON zu erfassen, muss die `isMultiLineJson`-Markierung gesetzt werden. Weiterführende Informationen finden Sie im [Handbuch zur Fehlerbehebung bei der Batch-Erfassung](./troubleshooting.md).

**API-Format**

```http
POST /batches
```

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
      }'
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{DATASET_ID}` | Die Kennung des Referenzdatensatzes. |

**Antwort**

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
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

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Die Kennung des neu erstellten Batches. |
| `{DATASET_ID}` | Die Kennung des referenzierten Datensatzes. |

### Dateien hochladen

Nachdem Sie einen Batch erstellt haben, können Sie die Batch-Kennung aus der Batch-Erstellungsantwort verwenden, um Dateien in den Batch hochzuladen. Sie haben die Möglichkeit, mehrere Dateien in den Batch hochzuladen.

>[!NOTE]
>
>Im Anhang finden Sie ein [Beispiel für eine ordnungsgemäß formatierte JSON-Datendatei](#data-transformation-for-batch-ingestion).

**API-Format**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Die Kennung des Batches, in den Sie hochladen möchten. |
| `{DATASET_ID}` | Die Kennung des Referenzdatensatzes des Batches. |
| `{FILE_NAME}` | Der Name der Datei, die Sie hochladen möchten. Stellen Sie sicher, dass Sie einen eindeutigen Dateinamen verwenden, damit er nicht mit einer anderen Datei für den Batch der gesendeten Dateien kollidiert. |

**Anfrage**

>[!NOTE]
>
> Die API unterstützt das Hochladen einzelner Teile. Stellen Sie sicher, dass der Content-Type „application/octet-stream“ lautet.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Der vollständige Pfad und Name der Datei, die Sie hochladen möchten. Dieser Dateipfad ist der lokale Dateipfad, z. B. `acme/customers/campaigns/summer.json`. |

**Antwort**

```http
200 OK
```

### Batch abschließen

Nachdem Sie alle Teile der Datei hochgeladen haben, müssen Sie signalisieren, dass die Daten vollständig hochgeladen worden sind und dass der Batch bereit zur Promotion ist.

**API-Format**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Die Kennung des Batches, in den Sie hochladen möchten. |

**Anfrage**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

```http
200 OK
```

## Parquet-Dateien erfassen {#ingest-parquet-files}

>[!NOTE]
>
> Die folgenden Schritte gelten für kleine Dateien (256 MB oder weniger). Wenn Sie einen Gateway-Timeout erreichen oder Fehler wegen der Größe des Anfragetexts erhalten, müssen Sie zum Upload großer Dateien wechseln.

### Batch erstellen

Zunächst müssen Sie einen Batch erstellen, bei dem Parquet als Eingabeformat dient. Beim Erstellen des Batches müssen Sie eine Datensatz-ID angeben. Außerdem müssen Sie sicherstellen, dass alle im Batch hochgeladenen Dateien mit dem XDM-Schema übereinstimmen, das mit dem bereitgestellten Datensatz verknüpft ist.

**Anfrage**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" 
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "parquet"
           }
      }'
```

| Parameter | Beschreibung |
| --------- | ------------ |
| `{DATASET_ID}` | Die Kennung des Referenzdatensatzes. |

**Antwort**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
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

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Die Kennung des neu erstellten Batches. |
| `{DATASET_ID}` | Die Kennung des referenzierten Datensatzes. |
| `{USER_ID}` | Die Kennung des Anwenders, der den Batch erstellt hat. |

### Dateien hochladen

Nach dem Erstellen eines Batches können Sie die `batchId` verwenden, um Dateien in den Batch hochzuladen. Sie haben die Möglichkeit, mehrere Dateien in den Batch hochzuladen.

**API-Format**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Die Kennung des Batches, in den Sie hochladen möchten. |
| `{DATASET_ID}` | Die Kennung des Referenzdatensatzes des Batches. |
| `{FILE_NAME}` | Der Name der Datei, die Sie hochladen möchten. Stellen Sie sicher, dass Sie einen eindeutigen Dateinamen verwenden, damit er nicht mit einer anderen Datei für den Batch der gesendeten Dateien kollidiert. |

**Anfrage**

>[!CAUTION]
>
> Diese API unterstützt das Hochladen einzelner Teile. Stellen Sie sicher, dass der Content-Type „application/octet-stream“ lautet.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Der vollständige Pfad und Name der Datei, die Sie hochladen möchten. Dieser Dateipfad ist der lokale Dateipfad, z. B. `acme/customers/campaigns/summer.parquet`. |

**Antwort**

```http
200 OK
```

### Batch abschließen

Nachdem Sie alle Teile der Datei hochgeladen haben, müssen Sie signalisieren, dass die Daten vollständig hochgeladen worden sind und dass der Batch bereit zur Promotion ist.

**API-Format**

```http
POST /batches/{BATCH_ID}?action=complete
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Die Kennung des Batches, den Sie als abschlussbereit signalisieren möchten. |

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Antwort**

```http
200 OK
```

## Große Parquet-Dateien erfassen

>[!NOTE]
>
> In diesem Abschnitt wird beschrieben, wie Sie Dateien hochladen, die über 256 MB groß sind. Die großen Dateien werden in Blöcken hochgeladen und dann über ein API-Signal zusammengefügt.

### Batch erstellen

Zunächst müssen Sie einen Batch erstellen, bei dem Parquet als Eingabeformat dient. Beim Erstellen des Batches müssen Sie eine Datensatz-ID angeben. Außerdem müssen Sie sicherstellen, dass alle im Batch hochgeladenen Dateien mit dem XDM-Schema übereinstimmen, das mit dem bereitgestellten Datensatz verknüpft ist.

**API-Format**

```http
POST /batches
```

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
             "format": "parquet"
           }
      }'
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{DATASET_ID}` | Die Kennung des Referenzdatensatzes. |

**Antwort**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
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

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Die Kennung des neu erstellten Batches. |
| `{DATASET_ID}` | Die Kennung des referenzierten Datensatzes. |
| `{USER_ID}` | Die Kennung des Anwenders, der den Batch erstellt hat. |

### Große Datei initialisieren

Nachdem Sie den Batch erstellt haben, müssen Sie die große Datei initialisieren, bevor Sie Blöcke in den Batch hochladen können.

**API-Format**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Die Kennung des neu erstellten Batches. |
| `{DATASET_ID}` | Die Kennung des referenzierten Datensatzes. |
| `{FILE_NAME}` | Der Name der Datei, die initialisiert werden soll. |

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=INITIALIZE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Antwort**

```http
201 Created
```

### Blöcke der großen Datei hochladen

Nachdem die Datei erstellt wurde, können durch wiederholte PATCH-Anfragen alle nachfolgenden Blöcke hochgeladen werden, jeweils einer für jeden Abschnitt der Datei.

**API-Format**

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Die Kennung des Batches, in den Sie hochladen möchten. |
| `{DATASET_ID}` | Die Kennung des Referenzdatensatzes des Batches. |
| `{FILE_NAME}` | Der Name der Datei, die Sie hochladen möchten. Stellen Sie sicher, dass Sie einen eindeutigen Dateinamen verwenden, damit er nicht mit einer anderen Datei für den Batch der gesendeten Dateien kollidiert. |

**Anfrage**

>[!CAUTION]
>
> Diese API unterstützt das Hochladen einzelner Teile. Stellen Sie sicher, dass der Content-Type „application/octet-stream“ lautet.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'Content-Range: bytes {CONTENT_RANGE}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{CONTENT_RANGE}` | In Ganzzahlen: Anfang und Ende des angeforderten Bereichs. |
| `{FILE_PATH_AND_NAME}` | Der vollständige Pfad und Name der Datei, die Sie hochladen möchten. Dieser Dateipfad ist der lokale Dateipfad, z. B. `acme/customers/campaigns/summer.json`. |


**Antwort**

```http
200 OK
```

### Große Datei abschließen

Nach dem Erstellen eines Batches können Sie die `batchId` verwenden, um Dateien in den Batch hochzuladen. Sie haben die Möglichkeit, mehrere Dateien in den Batch hochzuladen.

**API-Format**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Die Kennung des Batches, für den der Abschluss signalisiert werden soll. |
| `{DATASET_ID}` | Die Kennung des Referenzdatensatzes des Batches. |
| `{FILE_NAME}` | Der Name der Datei, für die der Abschluss signalisiert werden soll. |

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Antwort**

```http
201 Created
```

### Batch abschließen

Nachdem Sie alle Teile der Datei hochgeladen haben, müssen Sie signalisieren, dass die Daten vollständig hochgeladen worden sind und dass der Batch bereit zur Promotion ist.

**API-Format**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Die Kennung des Batches, für den der Abschluss signalisiert werden soll. |


**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Antwort**

```http
200 OK
```

## CSV-Dateien erfassen

Um CSV-Dateien zu erfassen, müssen Sie eine Klasse, ein Schema und einen Datensatz erstellen, die CSV unterstützen. Genaue Informationen zum Erstellen der erforderlichen Klasse und des erforderlichen Schemas finden Sie in den Anweisungen im [Tutorial zur Erstellung von Ad-hoc-Schemas](../../xdm/api/ad-hoc.md).

>[!NOTE]
>
> Die folgenden Schritte gelten für kleine Dateien (256 MB oder weniger). Wenn Sie einen Gateway-Timeout erreichen oder Fehler wegen der Größe des Anfragetexts erhalten, müssen Sie zum Upload großer Dateien wechseln.

### Datensatz erstellen

Nachdem Sie die oben stehenden Anweisungen zum Erstellen der erforderlichen Klasse und des erforderlichen Schemas befolgt haben, müssen Sie einen Datensatz erzeugen, der CSV unterstützen kann.

**API-Format**

```http
POST /catalog/dataSets
```

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "{DATASET_NAME}",
      "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed+json;version=1"
      }
  }'
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{TENANT_ID}` | Diese Kennung stellt sicher, dass die von Ihnen erstellten Ressourcen den richtigen Namespace aufweisen und in Ihrer IMS-Organisation enthalten sind. |
| `{SCHEMA_ID}` | Die Kennung des erstellten Schemas. |

### Batch erstellen

Als Nächstes müssen Sie einen Batch mit CSV als Eingabeformat erstellen. Beim Erstellen des Batches müssen Sie eine Datensatz-ID angeben. Außerdem müssen Sie sicherstellen, dass alle im Batch hochgeladenen Dateien mit dem Schema übereinstimmen, das mit dem bereitgestellten Datensatz verknüpft ist.

**API-Format**

```http
POST /batches
```

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
            "datasetId": "{DATASET_ID}",
            "inputFormat": {
                "format": "csv"
            }
      }'
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{DATASET_ID}` | Die Kennung des Referenzdatensatzes. |

**Antwort**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
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

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Die Kennung des neu erstellten Batches. |
| `{DATASET_ID}` | Die Kennung des referenzierten Datensatzes. |
| `{USER_ID}` | Die Kennung des Anwenders, der den Batch erstellt hat. |

### Dateien hochladen

Nach dem Erstellen eines Batches können Sie die `batchId` verwenden, um Dateien in den Batch hochzuladen. Sie haben die Möglichkeit, mehrere Dateien in den Batch hochzuladen.

>[!NOTE]
>
>Im Anhang finden Sie ein [Beispiel für eine ordnungsgemäß formatierte CSV-Datendatei](#data-transformation-for-batch-ingestion).

**API-Format**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Die Kennung des Batches, in den Sie hochladen möchten. |
| `{DATASET_ID}` | Die Kennung des Referenzdatensatzes des Batches. |
| `{FILE_NAME}` | Der Name der Datei, die Sie hochladen möchten. Stellen Sie sicher, dass Sie einen eindeutigen Dateinamen verwenden, damit er nicht mit einer anderen Datei für den Batch der gesendeten Dateien kollidiert. |

**Anfrage**

>[!CAUTION]
>
> Diese API unterstützt das Hochladen einzelner Teile. Stellen Sie sicher, dass der Content-Type „application/octet-stream“ lautet.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.csv \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.csv"
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Der vollständige Pfad und Name der Datei, die Sie hochladen möchten. Dieser Dateipfad ist der lokale Dateipfad, z. B. `acme/customers/campaigns/summer.csv`. |


**Antwort**

```http
200 OK
```

### Batch abschließen

Nachdem Sie alle Teile der Datei hochgeladen haben, müssen Sie signalisieren, dass die Daten vollständig hochgeladen worden sind und dass der Batch bereit zur Promotion ist.

**API-Format**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

```http
200 OK
```

## Batch abbrechen

Solange der Batch verarbeitet wird, kann er abgebrochen werden. Sobald ein Batch jedoch finalisiert wurde (z. B. Status „Erfolg“ oder „Fehlgeschlagen“), kann er nicht mehr abgebrochen werden.

**API-Format**

```http
POST /batches/{BATCH_ID}?action=ABORT
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Die Kennung des Batches, den Sie abbrechen möchten. |

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=ABORT \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Antwort**

```http
200 OK
```

## Batch löschen {#delete-a-batch}

Ein Batch kann gelöscht werden, indem Sie folgende POST-Anfrage mit dem `action=REVERT`-Abfrageparameter an die Kennung des Batches, den Sie löschen möchten, richten. Der Batch ist als „inaktiv“ markiert, sodass er für die Speicherbereinigung qualifiziert ist. Der Batch wird asynchron gesammelt und zu diesem Zeitpunkt als „gelöscht“ gekennzeichnet.

**API-Format**

```http
POST /batches/{BATCH_ID}?action=REVERT
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Die Kennung des Batches, den Sie löschen möchten. |

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=REVERT \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Antwort**

```http
200 OK
```

## Batch Patch

Gelegentlich kann es erforderlich sein, Daten im Profilspeicher Ihrer Organisation zu aktualisieren. Vielleicht müssen Sie zum Beispiel Datensätze korrigieren oder einen Attributwert ändern. Adobe Experience Platform unterstützt die Aktualisierung oder den Patch von Profilspeicherdaten durch eine Upstream-Aktion oder &quot;Patchen eines Batches&quot;.

>[!NOTE]
>
>Diese Aktualisierungen sind nur für Profildatensätze zulässig, nicht für Erlebnisereignisse.

Folgendes ist erforderlich, um einen Batch zu patchen:

- **Ein für Profil- und Attributaktualisierungen aktivierter Datensatz.** Dies erfolgt über Datensatz-Tags und erfordert eine bestimmte `isUpsert:true` -Tag dem `unifiedProfile` Array. Ausführliche Anweisungen zum Erstellen eines Datensatzes oder Konfigurieren eines vorhandenen Datensatzes für die Aktualisierung finden Sie im Tutorial für [Aktivieren eines Datensatzes für Profil-Updates](../../catalog/datasets/enable-upsert.md).
- **Eine Parquet-Datei mit den zu patchierenden Feldern und Identitätsfeldern für das Profil.** Das Datenformat für das Patchen eines Batches ähnelt dem normalen Batch-Erfassungsvorgang. Die erforderliche Eingabe ist eine Parquet-Datei. Zusätzlich zu den zu aktualisierenden Feldern müssen die hochgeladenen Daten die Identitätsfelder enthalten, damit sie mit den Daten im Profilspeicher übereinstimmen.

Nachdem Sie einen Datensatz für Profil und Upload aktiviert haben und eine Parquet-Datei mit den Feldern, die Sie patchen möchten, sowie den erforderlichen Identitätsfeldern, können Sie die Schritte für [Erfassen von Parquet-Dateien](#ingest-parquet-files) um den Patch über die Batch-Erfassung abzuschließen.

## Batch ersetzen

Wenn Sie einen bereits erfassten Batch ersetzen möchten, können Sie dies mit „batch replace“ tun. Diese Aktion entspricht einem Löschen des alten Batches und dem Erfassen eines neuen Batches.

### Batch erstellen

Zunächst müssen Sie einen Batch erstellen, wobei JSON als Eingabeformat dient. Beim Erstellen des Batches müssen Sie eine Datensatz-ID angeben. Außerdem müssen Sie sicherstellen, dass alle im Batch hochgeladenen Dateien mit dem XDM-Schema übereinstimmen, das mit dem bereitgestellten Datensatz verknüpft ist. Außerdem müssen Sie die alten Batches im Abschnitt „replace“ als Referenz angeben. Im folgenden Beispiel werden Batches mit den Kennungen `batchIdA` und `batchIdB` wiederholt.

**API-Format**

```http
POST /batches
```

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
             "format": "json"
           },
            "replay": {
                "predecessors": ["${batchIdA}","${batchIdB}"],
                "reason": "replace"
             }
      }'
```

| Parameter | Beschreibung |
| --------- | ----------- | 
| `{DATASET_ID}` | Die Kennung des Referenzdatensatzes. |

**Antwort**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "replay": {
        "predecessors": [
            "batchIdA", "batchIdB"
        ],
        "reason": "replace"
    },
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Die Kennung des neu erstellten Batches. |
| `{DATASET_ID}` | Die Kennung des referenzierten Datensatzes. |
| `{USER_ID}` | Die Kennung des Anwenders, der den Batch erstellt hat. |


### Dateien hochladen

Nach dem Erstellen eines Batches können Sie die `batchId` verwenden, um Dateien in den Batch hochzuladen. Sie haben die Möglichkeit, mehrere Dateien in den Batch hochzuladen.

**API-Format**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Die Kennung des Batches, in den Sie hochladen möchten. |
| `{DATASET_ID}` | Die Kennung des Referenzdatensatzes des Batches. |
| `{FILE_NAME}` | Der Name der Datei, die Sie hochladen möchten. Stellen Sie sicher, dass Sie einen eindeutigen Dateinamen verwenden, damit er nicht mit einer anderen Datei für den Batch der gesendeten Dateien kollidiert. |

**Anfrage**

>[!CAUTION]
>
> Diese API unterstützt das Hochladen einzelner Teile. Stellen Sie sicher, dass der Content-Type „application/octet-stream“ lautet. Verwenden Sie nicht die Option „curl -F“, da dabei standardmäßig eine mehrteilige Anfrage verwendet wird, die mit der API nicht kompatibel ist.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Der vollständige Pfad und Name der Datei, die Sie hochladen möchten. Dieser Dateipfad ist der lokale Dateipfad, z. B. `acme/customers/campaigns/summer.json`. |

**Antwort**

```http
200 OK
```

### Batch abschließen

Nachdem Sie alle Teile der Datei hochgeladen haben, müssen Sie signalisieren, dass die Daten vollständig hochgeladen worden sind und dass der Batch bereit zur Promotion ist.

**API-Format**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Die Kennung des Batches, den Sie abschließen möchten. |

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

```http
200 OK
```

## Anhang

Der folgende Abschnitt enthält zusätzliche Informationen zur Aufnahme von Daten in Experience Platform mithilfe der Batch-Erfassung.

### Datenumwandlung für die Batch-Erfassung

So erfassen Sie eine Datendatei in [!DNL Experience Platform]muss die hierarchische Struktur der Datei mit dem [Experience-Datenmodell (XDM)](../../xdm/home.md) Schema, das mit dem hochgeladenen Datensatz verknüpft ist.

Informationen dazu, wie Sie eine CSV-Datei einem XDM-Schema konform zuordnen, finden Sie im Dokument mit [Beispielumwandlungen](../../etl/transformations.md). Hier finden Sie außerdem ein Beispiel für eine richtig formatierte JSON-Datendatei. Im Dokument bereitgestellte Beispieldateien finden Sie hier:

- [CRM_profiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)
