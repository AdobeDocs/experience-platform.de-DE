---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Entwicklerhandbuch zur Adobe Experience Platform Batch Ingestion
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '2577'
ht-degree: 6%

---


# Entwicklerhandbuch zur Stapelverarbeitung

Dieses Dokument bietet einen umfassenden Überblick über die Verwendung von [Stapelverarbeitungs-APIs](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml).

Der Anhang zu diesem Dokument enthält Informationen zur [Formatierung von Daten, die zur Erfassung](#data-transformation-for-batch-ingestion)verwendet werden sollen, einschließlich Beispiel-CSV- und JSON-Datendateien.

## Erste Schritte

Die Datenerfassung bietet eine RESTful-API, mit der Sie grundlegende CRUD-Vorgänge für die unterstützten Objekttypen durchführen können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um erfolgreich Aufrufe an die Batch Ingestion API durchführen zu können.

Dieses Handbuch erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

- [Stapelverarbeitung](./overview.md): Ermöglicht Ihnen das Erfassen von Daten in die Adobe Experience Platform als Stapeldateien.
- [Erlebnis-Datenmodell (XDM)-System](../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
- [Sandboxen](../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxen, die eine Instanz einer Platform in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt [zum Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung bei Experience Platformen.

### Werte für erforderliche Kopfzeilen sammeln

Um Platformen-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungslehrgang](../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungtutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform API-Aufrufen bereit, wie unten dargestellt:

- Genehmigung: Träger `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in der Experience Platform werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an Platform-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxen in der Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Anforderungen, die eine Nutzlast enthalten (POST, PUT, PATCH), erfordern möglicherweise einen zusätzlichen `Content-Type` Header. Die für jeden Aufruf akzeptierten Werte werden in den Aufrufparametern bereitgestellt. Die folgenden Inhaltstypen werden in diesem Handbuch verwendet:

- Content-Type: application/json
- Content-Type: application/octet-stream

## Typen

Beim Erfassen von Daten ist es wichtig, zu verstehen, wie Experience Data Model (XDM)-Schema funktionieren. Weitere Informationen zur Zuordnung von XDM-Feldtypen zu verschiedenen Formaten finden Sie im [Schema Registry Developer Guide](../../xdm/api/getting-started.md).

Beim Eingeben von Daten gibt es eine gewisse Flexibilität. Wenn ein Typ nicht mit dem Schema Zielgruppe übereinstimmt, werden die Daten in den Typ der ausgedrückten Zielgruppe konvertiert. Wenn dies nicht möglich ist, schlägt der Stapel mit einem `TypeCompatibilityException`Fehler fehl.

Beispielsweise haben weder JSON noch CSV einen Datums- oder Uhrzeittyp. Daher werden diese Werte mit [ISO 8061 formatierten Zeichenfolgen](https://www.iso.org/iso-8601-date-and-time-format.html) (&quot;2018-07-10T15:05:59.000-08:00&quot;) oder Unix Time in Millisekunden formatiert (153126395999 000) und werden zur Erfassungszeit in den XDM-Typ der Zielgruppe konvertiert.

Die folgende Tabelle zeigt die Konvertierungen, die beim Erfassen von Daten unterstützt werden.

| Inbound (row) vs. Target (col) | Zeichenfolge | Byte | Short | Ganzzahl | lang | Doppelt | Datum | Date-Time | Objekt | Landkarte |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Zeichenfolge | X | X | X | X | X | X | X | X |  |  |
| Byte | X | X | X | X | X | X |  |  |  |  |
| Short | X | X | X | X | X | X |  |  |  |  |
| Ganzzahl | X | X | X | X | X | X |  |  |  |  |
| lang | X | X | X | X | X | X | X | X |  |  |
| Doppelt | X | X | X | X | X | X |  |  |  |  |
| Datum |  |  |  |  |  |  | X |  |  |  |
| Date-Time |  |  |  |  |  |  |  | X |  |  |
| Objekt |  |  |  |  |  |  |  |  | X | X |
| Landkarte |  |  |  |  |  |  |  |  | X | X |

>[!NOTE]
>
>Booleans und Arrays können nicht in andere Typen konvertiert werden.

## Engpasseinschränkungen

Die Stapeldatenerfassung unterliegt einigen Einschränkungen:
- Maximale Anzahl von Dateien pro Stapel: 1500
- Maximale Stapelgröße: 100 GB
- Maximale Anzahl von Eigenschaften oder Feldern pro Zeile: 10000
- Maximale Anzahl der Stapel pro Minute pro Benutzer: 138

## JSON-Dateien aufnehmen

>[!NOTE]
>
>Die folgenden Schritte gelten für kleine Dateien (256 MB oder weniger). Wenn Sie einen Gateway-Timeout-Wert erreichen oder Fehler in der Körpergröße anfordern, müssen Sie zum Hochladen großer Dateien wechseln.

### Stapel erstellen

Zunächst müssen Sie einen Stapel erstellen, wobei JSON als Eingabeformat dient. Beim Erstellen des Stapels müssen Sie eine DataSet-ID angeben. Sie müssen außerdem sicherstellen, dass alle im Batch hochgeladenen Dateien mit dem XDM-Schema übereinstimmen, das mit dem bereitgestellten Datensatz verknüpft ist.

>[!NOTE]
>
>Die folgenden Beispiele beziehen sich auf einzeilige JSON-Dateien. Um mehrzeiliges JSON zu erfassen, muss das `isMultiLineJson` Flag eingestellt werden. Weitere Informationen finden Sie im Handbuch zur Fehlerbehebung bei der [Stapelverarbeitung](./troubleshooting.md).

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
| `{DATASET_ID}` | Die ID des Referenzdatasets. |

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
| `{BATCH_ID}` | Die ID des neu erstellten Stapels. |
| `{DATASET_ID}` | Die ID des referenzierten Datensatzes. |

### Hochladen von Dateien

Nachdem Sie einen Stapel erstellt haben, können Sie die Datei `batchId` von vor verwenden, um Dateien in den Stapel hochzuladen. Sie können mehrere Dateien in den Stapel hochladen.

>[!NOTE]
>
>Im Anhang finden Sie ein [Beispiel für eine ordnungsgemäß formatierte JSON-Datendatei](#data-transformation-for-batch-ingestion).

**API-Format**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Die ID des Stapels, in den Sie hochladen möchten. |
| `{DATASET_ID}` | Die ID des Referenzdatasets des Stapels. |
| `{FILE_NAME}` | Der Name der Datei, die Sie hochladen möchten. |

**Anfrage**

>[!NOTE]
>
>Die API unterstützt das Hochladen von Einzelteilen. Stellen Sie sicher, dass der Content-Typ application/octet-stream ist.

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
| `{FILE_PATH_AND_NAME}` | Der vollständige Pfad und der Name der Datei, die Sie hochladen möchten. |

**Antwort**

```http
200 OK
```

### Stapel abschließen

Nachdem Sie alle verschiedenen Teile der Datei hochgeladen haben, müssen Sie signalisieren, dass die Daten vollständig hochgeladen wurden und dass der Stapel zur Promotion bereit ist.

**API-Format**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Die ID des Stapels, in den Sie hochladen möchten. |

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

## Parquet-Dateien einbeziehen

>[!NOTE]
>
>Die folgenden Schritte gelten für kleine Dateien (256 MB oder weniger). Wenn Sie einen Gateway-Timeout-Wert erreichen oder Fehler in der Körpergröße anfordern, müssen Sie zum Hochladen großer Dateien wechseln.

### Stapel erstellen

Zunächst müssen Sie einen Stapel erstellen, bei dem Parquet als Eingabeformat dient. Beim Erstellen des Stapels müssen Sie eine DataSet-ID angeben. Sie müssen außerdem sicherstellen, dass alle im Batch hochgeladenen Dateien mit dem XDM-Schema übereinstimmen, das mit dem bereitgestellten Datensatz verknüpft ist.

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
| `{DATASET_ID}` | Die ID des Referenzdatasets. |

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
| `{BATCH_ID}` | Die ID des neu erstellten Stapels. |
| `{DATASET_ID}` | Die ID des referenzierten Datensatzes. |
| `{USER_ID}` | Die ID des Benutzers, der den Stapel erstellt hat. |

### Hochladen von Dateien

Nachdem Sie einen Stapel erstellt haben, können Sie die Datei `batchId` von vor verwenden, um Dateien in den Stapel hochzuladen. Sie können mehrere Dateien in den Stapel hochladen.

**API-Format**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Die ID des Stapels, in den Sie hochladen möchten. |
| `{DATASET_ID}` | Die ID des Referenzdatasets des Stapels. |
| `{FILE_NAME}` | Der Name der Datei, die Sie hochladen möchten. |

**Anfrage**

>[!CAUTION]
>
>Diese API unterstützt das Hochladen von Einzelteilen. Stellen Sie sicher, dass der Content-Typ application/octet-stream ist.

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
| `{FILE_PATH_AND_NAME}` | Der vollständige Pfad und der Name der Datei, die Sie hochladen möchten. |

**Antwort**

```http
200 OK
```

### Stapel abschließen

Nachdem Sie alle verschiedenen Teile der Datei hochgeladen haben, müssen Sie signalisieren, dass die Daten vollständig hochgeladen wurden und dass der Stapel zur Promotion bereit ist.

**API-Format**

```http
POST /batches/{BATCH_ID}?action=complete
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Die ID des Stapels, der signalisiert werden soll, kann abgeschlossen werden. |

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

## Große Parkettdateien aufnehmen

>[!NOTE]
>
>In diesem Abschnitt wird beschrieben, wie Sie Dateien hochladen, die größer als 256 MB sind. Die großen Dateien werden in Textbausteinen hochgeladen und dann über ein API-Signal verbunden.

### Stapel erstellen

Zunächst müssen Sie einen Stapel erstellen, bei dem Parquet als Eingabeformat dient. Beim Erstellen des Stapels müssen Sie eine DataSet-ID angeben. Sie müssen außerdem sicherstellen, dass alle im Batch hochgeladenen Dateien mit dem XDM-Schema übereinstimmen, das mit dem bereitgestellten Datensatz verknüpft ist.

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
| `{DATASET_ID}` | Die ID des Referenzdatasets. |

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
| `{BATCH_ID}` | Die ID des neu erstellten Stapels. |
| `{DATASET_ID}` | Die ID des referenzierten Datensatzes. |
| `{USER_ID}` | Die ID des Benutzers, der den Stapel erstellt hat. |

### Große Datei initialisieren

Nachdem Sie den Stapel erstellt haben, müssen Sie die große Datei initialisieren, bevor Sie Abschnitte in den Stapel hochladen können.

**API-Format**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Die ID des neu erstellten Stapels. |
| `{DATASET_ID}` | Die ID des referenzierten Datensatzes. |
| `{FILE_NAME}` | Der Name der Datei, die demnächst initialisiert werden soll. |

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

### Hochladen großer Dateibausteine

Nachdem die Datei erstellt wurde, können alle nachfolgenden Abschnitte durch wiederholte PATCH-Anfragen hochgeladen werden, jeweils einen für jeden Abschnitt der Datei.

**API-Format**

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Die ID des Stapels, in den Sie hochladen möchten. |
| `{DATASET_ID}` | Die ID des Referenzdatasets des Stapels. |
| `{FILE_NAME}` | Der Name der Datei, die Sie hochladen möchten. |

**Anfrage**

>[!CAUTION]
>
>Diese API unterstützt das Hochladen von Einzelteilen. Stellen Sie sicher, dass der Content-Typ application/octet-stream ist.

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
| `{FILE_PATH_AND_NAME}` | Der vollständige Pfad und der Name der Datei, die Sie hochladen möchten. |


**Antwort**

```http
200 OK
```

### Eine große Datei abschließen

Nachdem Sie einen Stapel erstellt haben, können Sie die Datei `batchId` von vor verwenden, um Dateien in den Stapel hochzuladen. Sie können mehrere Dateien in den Stapel hochladen.

**API-Format**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Die ID des Stapels, für den die Beendigung signalisiert werden soll. |
| `{DATASET_ID}` | Die ID des Referenzdatasets des Stapels. |
| `{FILE_NAME}` | Der Name der Datei, von der das Ausfüllen signalisiert werden soll. |

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

### Stapel abschließen

Nachdem Sie alle verschiedenen Teile der Datei hochgeladen haben, müssen Sie signalisieren, dass die Daten vollständig hochgeladen wurden und dass der Stapel zur Promotion bereit ist.

**API-Format**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Die ID des Stapels, der signalisiert werden soll, ist abgeschlossen. |


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

## CSV-Dateien aufnehmen

Um CSV-Dateien zu erfassen, müssen Sie eine Klasse, ein Schema und einen Datensatz erstellen, der CSV unterstützt. Detaillierte Informationen zum Erstellen der erforderlichen Klasse und des erforderlichen Schemas finden Sie in den Anweisungen im Lernprogramm zur Erstellung von [Ad-hoc-Schemas](../../xdm/api/ad-hoc.md).

>[!NOTE]
>
>Die folgenden Schritte gelten für kleine Dateien (256 MB oder weniger). Wenn Sie einen Gateway-Timeout-Wert erreichen oder Fehler in der Körpergröße anfordern, müssen Sie zum Hochladen großer Dateien wechseln.

### Datensatz erstellen

Nachdem Sie die oben stehenden Anweisungen befolgt haben, um die erforderliche Klasse und das erforderliche Schema zu erstellen, müssen Sie ein Dataset erstellen, das CSV unterstützen kann.

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
| `{TENANT_ID}` | Diese ID wird verwendet, um sicherzustellen, dass die von Ihnen erstellten Ressourcen korrekt benannt und in Ihrer IMS-Organisation enthalten sind. |
| `{SCHEMA_ID}` | Die ID des erstellten Schemas. |

Eine Erläuterung der verschiedenen Teile des Abschnitts &quot;fileDescription&quot;des JSON-Textkörpers finden Sie unten:

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
| `format` | Das Format der Masterdatei, nicht das Format der Eingabedatei. |
| `delimiters` | Das als Trennzeichen zu verwendende Zeichen. |
| `quotes` | Das für Anführungszeichen zu verwendende Zeichen. |
| `escapes` | Das als Escape-Zeichen zu verwendende Zeichen. |
| `header` | Die hochgeladene Datei **muss** Kopfzeilen enthalten. Da die Validierung des Schemas abgeschlossen ist, muss dies auf &quot;true&quot;gesetzt werden. Darüber hinaus dürfen Kopfzeilen **keine** Leerzeichen enthalten. Wenn Sie Leerzeichen in Ihrer Kopfzeile haben, ersetzen Sie diese stattdessen durch Unterstriche. |
| `charset` | Ein optionales Feld. Andere unterstützte Zeichensätze sind &quot;US-ASCII&quot;und &quot;ISO-8869-1&quot;. Wenn das Feld leer gelassen wird, wird UTF-8 standardmäßig angenommen. |

Der referenzierte Datensatz muss über den oben aufgeführten Dateinamenblock verfügen und auf ein gültiges Schema in der Registrierung verweisen. Andernfalls wird die Datei nicht in Parkett gemeistert.

### Stapel erstellen

Als Nächstes müssen Sie einen Stapel mit CSV als Eingabeformat erstellen. Beim Erstellen des Stapels müssen Sie eine DataSet-ID angeben. Sie müssen außerdem sicherstellen, dass alle im Rahmen des Stapels hochgeladenen Dateien mit dem Schema übereinstimmen, das mit dem bereitgestellten Datensatz verknüpft ist.

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
| `{DATASET_ID}` | Die ID des Referenzdatasets. |

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
| `{BATCH_ID}` | Die ID des neu erstellten Stapels. |
| `{DATASET_ID}` | Die ID des referenzierten Datensatzes. |
| `{USER_ID}` | Die ID des Benutzers, der den Stapel erstellt hat. |

### Hochladen von Dateien

Nachdem Sie einen Stapel erstellt haben, können Sie die Datei `batchId` von vor verwenden, um Dateien in den Stapel hochzuladen. Sie können mehrere Dateien in den Stapel hochladen.

>[!NOTE]
>
>Im Anhang finden Sie ein [Beispiel für eine ordnungsgemäß formatierte CSV-Datendatei](#data-transformation-for-batch-ingestion).

**API-Format**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Die ID des Stapels, in den Sie hochladen möchten. |
| `{DATASET_ID}` | Die ID des Referenzdatasets des Stapels. |
| `{FILE_NAME}` | Der Name der Datei, die Sie hochladen möchten. |

**Anfrage**

>[!CAUTION]
>
>Diese API unterstützt das Hochladen von Einzelteilen. Stellen Sie sicher, dass der Content-Typ application/octet-stream ist.

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
| `{FILE_PATH_AND_NAME}` | Der vollständige Pfad und der Name der Datei, die Sie hochladen möchten. |


**Antwort**

```http
200 OK
```

### Stapel abschließen

Nachdem Sie alle verschiedenen Teile der Datei hochgeladen haben, müssen Sie signalisieren, dass die Daten vollständig hochgeladen wurden und dass der Stapel für die Promotion bereit ist.

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

## Stapel abbrechen

Während der Stapel verarbeitet wird, kann er dennoch abgebrochen werden. Sobald ein Stapel fertig gestellt ist (z. B. ein Erfolgs- oder ein Fehler-Status), kann der Stapel jedoch nicht abgebrochen werden.

**API-Format**

```http
POST /batches/{BATCH_ID}?action=ABORT
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Die ID des Stapels, den Sie abbrechen möchten. |

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

## Stapel löschen {#delete-a-batch}

Ein Stapel kann gelöscht werden, indem die folgende POST-Anforderung mit dem Parameter `action=REVERT` Abfrage zur ID des Stapels ausgeführt wird, den Sie löschen möchten. Der Stapel ist als &quot;inaktiv&quot;markiert, sodass er für die Müllabfuhr zugelassen wird. Der Stapel wird asynchron erfasst und zu diesem Zeitpunkt als &quot;gelöscht&quot;gekennzeichnet.

**API-Format**

```http
POST /batches/{BATCH_ID}?action=REVERT
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Die ID des Stapels, den Sie löschen möchten. |

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

## Stapel erneut abspielen

Wenn Sie einen bereits erfassten Stapel ersetzen möchten, können Sie dies mit &quot;Batch-Wiederholung&quot;tun. Diese Aktion entspricht dem Löschen des alten Stapels und dem Einfügen eines neuen Stapels.

### Stapel erstellen

Zunächst müssen Sie einen Stapel erstellen, wobei JSON als Eingabeformat dient. Beim Erstellen des Stapels müssen Sie eine DataSet-ID angeben. Sie müssen außerdem sicherstellen, dass alle im Batch hochgeladenen Dateien mit dem XDM-Schema übereinstimmen, das mit dem bereitgestellten Datensatz verknüpft ist. Außerdem müssen Sie die alten Stapel als Referenz im Abschnitt &quot;Wiederholung&quot;angeben. Im folgenden Beispiel werden Stapel mit IDs `batchIdA` und `batchIdB`wiedergegeben.

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
| `{DATASET_ID}` | Die ID des Referenzdatasets. |

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
| `{BATCH_ID}` | Die ID des neu erstellten Stapels. |
| `{DATASET_ID}` | Die ID des referenzierten Datensatzes. |
| `{USER_ID}` | Die ID des Benutzers, der den Stapel erstellt hat. |


### Hochladen von Dateien

Nachdem Sie einen Stapel erstellt haben, können Sie die Datei `batchId` von vor verwenden, um Dateien in den Stapel hochzuladen. Sie können mehrere Dateien in den Stapel hochladen.

**API-Format**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Die ID des Stapels, in den Sie hochladen möchten. |
| `{DATASET_ID}` | Die ID des Referenzdatasets des Stapels. |
| `{FILE_NAME}` | Der Name der Datei, die Sie hochladen möchten. |

**Anfrage**

>[!CAUTION]
>
>Diese API unterstützt das Hochladen von Einzelteilen. Stellen Sie sicher, dass der Content-Typ application/octet-stream ist. Verwenden Sie nicht die Option curl -F, da standardmäßig eine mehrteilige Anforderung verwendet wird, die mit der API nicht kompatibel ist.

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
| `{FILE_PATH_AND_NAME}` | Der vollständige Pfad und der Name der Datei, die Sie hochladen möchten. |

**Antwort**

```http
200 OK
```

### Stapel abschließen

Nachdem Sie alle verschiedenen Teile der Datei hochgeladen haben, müssen Sie signalisieren, dass die Daten vollständig hochgeladen wurden und dass der Stapel zur Promotion bereit ist.

**API-Format**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Die ID des Stapels, den Sie abschließen möchten. |

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

### Datenumwandlung für die Stapelverarbeitung

Um eine Datendatei in Experience Platform zu erfassen, muss die hierarchische Dateistruktur dem XDM-Schema ( [Experience Data Model)](../../xdm/home.md) entsprechen, das mit dem hochgeladenen Datensatz verknüpft ist.

Informationen dazu, wie eine CSV-Datei einem XDM-Schema zugeordnet werden kann, finden Sie im Dokument für [Beispieltransformationen](../../etl/transformations.md) sowie im Beispiel einer ordnungsgemäß formatierten JSON-Datendatei. Beispieldateien im Dokument finden Sie hier:

- [CRM_Profils.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_Profils.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)