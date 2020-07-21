---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Entwicklerhandbuch zu Adobe Experience Platform Batch Ingestion
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '2552'
ht-degree: 94%

---


# Entwicklerhandbuch zu Batch Ingestion

Dieses Dokument bietet Ihnen einen umfassenden Überblick über die Verwendung von [Batch Ingestion-APIs](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml).

Der Anhang zu diesem Dokument enthält Informationen zur [Formatierung von Daten, die zur Erfassung verwendet werden sollen](#data-transformation-for-batch-ingestion), einschließlich Beispiel-CSV- und JSON-Datendateien.

## Erste Schritte

Data Ingestion bietet eine RESTful-API, mit der Sie bei unterstützten Objekttypen grundlegende CRUD-Vorgänge durchführen können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um erfolgreiche Aufrufe an die Batch Ingestion-API durchführen zu können.

Dieses Handbuch setzt ein grundlegendes Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Batch Ingestion](./overview.md): Erlaubt Ihnen das Erfassen von Daten in Adobe Experience Platform in Form von Batch-Dateien.
- [!DNL Experience Data Model (XDM) System](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Experience Platform] organisiert werden.
- [!DNL Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

### Lesehilfe für Beispiel-API-Aufrufe

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dabei wird auf Pfade ebenso eingegangen wie auf die erforderlichen Kopfzeilen und die für Anfrage-Payloads zu verwendende Formatierung. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Die in der Dokumentation zu Beispielen für API-Aufrufe verwendeten Konventionen werden im Handbuch zur Fehlerbehebung für unter [Lesehilfe für Beispiel-API-Aufrufe](../../landing/troubleshooting.md#how-do-i-format-an-api-request) erläutert.[!DNL Experience Platform]

### Werte der zu verwendenden Kopfzeilen

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

Anfragen, die eine Payload enthalten (POST, PUT, PATCH), erfordern möglicherweise eine zusätzliche `Content-Type`-Kopfzeile. Die für einzelne Aufrufe zulässigen Werte werden in den Aufrufparametern angegeben. In diesem Handbuch werden die folgenden Inhaltstypen verwendet:

- Content-Type: application/json
- Content-Type: application/octet-stream

## Typen

When ingesting data, it is important to understand how [!DNL Experience Data Model] (XDM) schemas work. Weiterführende Informationen zur Zuordnung von XDM-Feldtypen zu verschiedenen Formaten finden Sie im [Entwicklerhandbuch zur Schemaregistrierung](../../xdm/api/getting-started.md).

Bei der Erfassung von Daten gibt es eine gewisse Flexibilität. Wenn ein Typ nicht mit dem Zielschema übereinstimmt, werden die Daten in den ausgedrückten Zieltyp konvertiert. Wenn das nicht möglich ist, schlägt der Batch mit einer `TypeCompatibilityException` fehl.

Beispielsweise verfügen weder JSON noch CSV über einen Datums- oder Datum/Uhrzeit-Typ. Daher werden diese Werte mit [ISO 8061-formatierten Zeichenfolgen](https://www.iso.org/iso-8601-date-and-time-format.html) („2018-07-10T15:05:59.000-08:00“) oder mit Unix-Zeit in Millisekunden ausgedrückt (1531263959000) und zum Erfassungszeitpunkt in den XDM-Zieltyp konvertiert.

Folgende Tabelle enthält die Konversionen, die beim Erfassen von Daten unterstützt werden.

| Eingehend (Zeile) vs. Ziel (Spalte) | Zeichenfolge | Byte | Kurz | Ganzzahl | Lang | Doppelt | Datum | Datum/Uhrzeit | Objekt | Zuordnung |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Zeichenfolge | X | X | X | X | X | X | X | X |  |  |
| Byte | X | X | X | X | X | X |  |  |  |  |
| Kurz | X | X | X | X | X | X |  |  |  |  |
| Ganzzahl | X | X | X | X | X | X |  |  |  |  |
| Lang | X | X | X | X | X | X | X | X |  |  |
| Doppelt | X | X | X | X | X | X |  |  |  |  |
| Datum |  |  |  |  |  |  | X |  |  |  |
| Datum/Uhrzeit |  |  |  |  |  |  |  | X |  |  |
| Objekt |  |  |  |  |  |  |  |  | X | X |
| Zuordnung |  |  |  |  |  |  |  |  | X | X |

>[!NOTE]
>
>Boolesche Werte und Arrays können nicht in andere Typen konvertiert werden.

## Einschränkungen bei der Erfassung

Die Erfassung von Batch-Daten unterliegt verschiedenen Einschränkungen:
- Maximale Anzahl von Dateien pro Batch: 1.500
- Maximale Batch-Größe: 100 GB
- Maximale Anzahl von Eigenschaften oder Feldern pro Zeile: 10.000
- Maximale Anzahl der Batches pro Minute und Anwender: 138

## JSON-Dateien erfassen

>[!NOTE]
>
>Die folgenden Schritte gelten für kleine Dateien (256 MB oder weniger). Wenn Sie einen Gateway-Timeout erreichen oder Fehler wegen der Größe des Anfragetexts erhalten, müssen Sie zum Upload großer Dateien wechseln.

### Batch erstellen

Zunächst müssen Sie einen Batch erstellen, wobei JSON als Eingabeformat dient. Beim Erstellen des Batches müssen Sie eine Datensatz-ID angeben. Außerdem müssen Sie sicherstellen, dass alle mit dem Batch hochgeladenen Dateien mit dem XDM-Schema übereinstimmen, das mit dem angegebenen Datensatz verknüpft ist.

>[!NOTE]
>
>Die folgenden Beispiele stehen für einzeilige JSON-Dateien. Um mehrzeilige JSON zu erfassen, muss die `isMultiLineJson`-Markierung gesetzt werden. Weiterführende Informationen finden Sie im [Handbuch zur Fehlerbehebung für Batch Ingestion](./troubleshooting.md).

**API-Format**

```http
POST /batches
```

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Die Kennung des neu erstellten Batches. |
| `{DATASET_ID}` | Die Kennung des referenzierten Datensatzes. |

### Dateien hochladen

Nach dem Erstellen eines Batches können Sie die `batchId` verwenden, um Dateien in den Batch hochzuladen. Sie haben die Möglichkeit, mehrere Dateien in den Batch hochzuladen.

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
| `{FILE_NAME}` | Der Name der Datei, die Sie hochladen möchten. |

**Anfrage**

>[!NOTE]
>
>Die API unterstützt das Hochladen einzelner Teile. Stellen Sie sicher, dass der Content-Type „application/octet-stream“ lautet.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Der vollständige Pfad und Name der Datei, die Sie hochladen möchten. |

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

```http
200 OK
```

## Parquet-Dateien erfassen

>[!NOTE]
>
>Die folgenden Schritte gelten für kleine Dateien (256 MB oder weniger). Wenn Sie einen Gateway-Timeout erreichen oder Fehler wegen der Größe des Anfragetexts erhalten, müssen Sie zum Upload großer Dateien wechseln.

### Batch erstellen

Zunächst müssen Sie einen Batch erstellen, bei dem Parquet als Eingabeformat dient. Beim Erstellen des Batches müssen Sie eine Datensatz-ID angeben. Außerdem müssen Sie sicherstellen, dass alle im Batch hochgeladenen Dateien mit dem XDM-Schema übereinstimmen, das mit dem bereitgestellten Datensatz verknüpft ist.

**Anfrage**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-api-key : {API_KEY}" \
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
| `{FILE_NAME}` | Der Name der Datei, die Sie hochladen möchten. |

**Anfrage**

>[!CAUTION]
>
>Diese API unterstützt das Hochladen einzelner Teile. Stellen Sie sicher, dass der Content-Type „application/octet-stream“ lautet.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Der vollständige Pfad und Name der Datei, die Sie hochladen möchten. |

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Antwort**

```http
200 OK
```

## Große Parquet-Dateien erfassen

>[!NOTE]
>
>In diesem Abschnitt wird beschrieben, wie Sie Dateien hochladen, die über 256 MB groß sind. Die großen Dateien werden in Blöcken hochgeladen und dann über ein API-Signal zusammengefügt.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `{FILE_NAME}` | Der Name der Datei, die Sie hochladen möchten. |

**Anfrage**

>[!CAUTION]
>
>Diese API unterstützt das Hochladen einzelner Teile. Stellen Sie sicher, dass der Content-Type „application/octet-stream“ lautet.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'Content-Range: bytes {CONTENT_RANGE}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{CONTENT_RANGE}` | In Ganzzahlen: Anfang und Ende des angeforderten Bereichs. |
| `{FILE_PATH_AND_NAME}` | Der vollständige Pfad und Name der Datei, die Sie hochladen möchten. |


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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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
>Die folgenden Schritte gelten für kleine Dateien (256 MB oder weniger). Wenn Sie einen Gateway-Timeout erreichen oder Fehler wegen der Größe des Anfragetexts erhalten, müssen Sie zum Upload großer Dateien wechseln.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "{DATASET_NAME}",
      "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed+json;version=1"
      },
      "fileDescription": {
          "format": "parquet",
          "delimiters": [","], 
          "quotes": ["\""],
          "escapes": ["\\"],
          "header": true,
          "charset": "UTF-8"
      }      
  }'
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{TENANT_ID}` | Diese Kennung stellt sicher, dass die von Ihnen erstellten Ressourcen einen richtigen Namespace aufweisen und in Ihrer IMS-Organisation enthalten sind. |
| `{SCHEMA_ID}` | Die Kennung des erstellten Schemas. |

Eine Erläuterung der verschiedenen Teile des Abschnitts „fileDescription“ des JSON-Haupttexts finden Sie im Folgenden:

```json
{
    "fileDescription": {
        "format": "parquet",
        "delimiters": [","],
        "quotes": ["\""],
        "escapes": ["\\"],
        "header": true,
        "charset": "UTF-8"
    }
}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `format` | Das Format der Mastered-Datei, nicht das Format der Eingabedatei. |
| `delimiters` | Das als Trennzeichen zu verwendende Zeichen. |
| `quotes` | Das als Anführungszeichen zu verwendende Zeichen. |
| `escapes` | Das als Escape-Zeichen zu verwendende Zeichen. |
| `header` | Die hochgeladene Datei **muss** Kopfzeilen enthalten. Da Schemavalidierung durchgeführt wird, muss dieser Wert auf „true“ gesetzt sein. Darüber hinaus dürfen Kopfzeilen **keine** Leerzeichen enthalten. Wenn Ihre Kopfzeile Leerzeichen aufweist, ersetzen Sie diese durch Unterstriche. |
| `charset` | Ein optionales Feld. Andere unterstützte Zeichensätze sind „US-ASCII“ und „ISO-8869-1“. Bei leer gelassenem Feld wird standardmäßig von UTF-8 ausgegangen. |

Der referenzierte Datensatz muss über den oben aufgeführten Dateibeschreibungsblock verfügen und in der Registrierung auf ein gültiges Schema verweisen. Andernfalls wird die Datei nicht in Parquet gemastert.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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
| `{FILE_NAME}` | Der Name der Datei, die Sie hochladen möchten. |

**Anfrage**

>[!CAUTION]
>
>Diese API unterstützt das Hochladen einzelner Teile. Stellen Sie sicher, dass der Content-Type „application/octet-stream“ lautet.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.csv \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.csv"
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Der vollständige Pfad und Name der Datei, die Sie hochladen möchten. |


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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Antwort**

```http
200 OK
```

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
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
| `{FILE_NAME}` | Der Name der Datei, die Sie hochladen möchten. |

**Anfrage**

>[!CAUTION]
>
>Diese API unterstützt das Hochladen einzelner Teile. Stellen Sie sicher, dass der Content-Type „application/octet-stream“ lautet. Verwenden Sie nicht die Option „curl -F“, da dabei standardmäßig eine mehrteilige Anfrage verwendet wird, die mit der API nicht kompatibel ist.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Der vollständige Pfad und Name der Datei, die Sie hochladen möchten. |

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

```http
200 OK
```

## Anhang

### Datenumwandlung für die Batch-Erfassung

In order to ingest a data file into [!DNL Experience Platform], the hierarchical structure of the file must comply with the [Experience Data Model (XDM)](../../xdm/home.md) schema associated with the dataset being uploaded to.

Informationen dazu, wie Sie eine CSV-Datei einem XDM-Schema konform zuordnen, finden Sie im Dokument mit [Beispielumwandlungen](../../etl/transformations.md). Hier finden Sie außerdem ein Beispiel für eine richtig formatierte JSON-Datendatei. Im Dokument bereitgestellte Beispieldateien finden Sie hier:

- [CRM_profiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)