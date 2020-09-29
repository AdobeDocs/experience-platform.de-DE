---
keywords: Experience Platform;home;popular topics;batch ingestion;Batch ingestion;partial ingestion;Partial ingestion;Retrieve error;retrieve error;Partial batch ingestion;partial batch ingestion;partial;ingestion;Ingestion;error diagnostics;retrieve error diagnostics;get error diagnostics;get error;get errors;retrieve errors;
solution: Experience Platform
title: Übersicht zur partiellen Batch-Erfassung in Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 4652722b17a290c9ef53244498257eb4cb97ac6d
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 33%

---


# Fehlerdiagnose abrufen

Adobe Experience Platform bietet für den Upload und die Aufnahme von Daten zwei Methoden. You can either use batch ingestion, which allows you to insert data using various file types (such as CSVs), or streaming ingestion, which allows you to insert their data to [!DNL Platform] using streaming endpoints in real time.

Dieses Dokument enthält Informationen zur Überwachung der Stapelverarbeitung, zur Verwaltung von Fehlern bei der Partiellen Stapelverarbeitung sowie eine Referenz für Stapelverarbeitungsarten.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Experience Platform] organisiert werden.
- [[!DNL Adobe Experience Platform Data Ingestion]](../home.md): Die Methoden, mit denen Daten gesendet werden können [!DNL Experience Platform].

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to the [!DNL Schema Registry], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

## Herunterladen der Fehlerdiagnose {#download-diagnostics}

Mit Adobe Experience Platform können Benutzer die Fehlerdiagnose der Eingabedateien herunterladen. Die Diagnose wird innerhalb von [!DNL Platform] bis zu 30 Tagen aufbewahrt.

### Liste-Eingabedateien {#list-files}

Mit der folgenden Anforderung wird eine Liste aller in einem finalisierten Stapel bereitgestellten Dateien abgerufen.

**API-Format**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{BATCH_ID}` | Die ID des Batches, den Sie nachschlagen. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort werden JSON-Objekte zurückgegeben, die detailliert angeben, wo die Diagnose gespeichert wurde.

```json
{
    "_page": {
        "count": 1,
        "limit": 100
    },
    "data": [
        {
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files/fileMetaData1.json"
                }
            },
            "length": "1337",
            "name": "fileMetaData1.json"
        },
                {
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2}/meta?path=input_files/fileMetaData2.json"
                }
            },
            "length": "1042",
            "name": "fileMetaData2.json"
        }
    ]
}
```

### Diagnose der Eingabedatei abrufen {#retrieve-diagnostics}

Nachdem Sie eine Liste der verschiedenen Eingabedateien abgerufen haben, können Sie die Diagnose der einzelnen Datei mithilfe der folgenden Anforderung abrufen.

**API-Format**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files/{FILE}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{BATCH_ID}` | Die ID des Batches, den Sie nachschlagen. |
| `{FILE}` | Der Name der Datei, auf die Sie zugreifen. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files/fileMetaData1.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt JSON-Objekte zurück, die `path` Objekte enthalten, die detailliert angeben, wo die Diagnose gespeichert wurde. Die Antwort gibt die `path` Objekte im [JSON-Zeilen](https://jsonlines.org/) -Format zurück.

```json
{"path": "F1.json"}
{"path": "etc/F2.json"}
```

## Retrieve batch ingestion errors {#retrieve-errors}

Wenn Stapel Fehler enthalten, sollten Sie Fehlerinformationen zu diesen Fehlern abrufen, damit Sie die Daten erneut erfassen können.

### Status prüfen {#check-status}

Um den Status des erfassten Batch zu überprüfen, müssen Sie im Pfad einer GET-Anfrage die Kennung des Batch angeben.

**API-Format**

```http
GET /catalog/batches/{BATCH_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Der `id`-Wert des Batch, dessen Status Sie überprüfen möchten. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/af838510-2233-11ea-acf0-f3edfcded2d2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort ohne Fehler**

Eine erfolgreiche Antwort mit detaillierten Informationen zum Status des Stapels wird zurückgegeben.

```json
{
    "af838510-2233-11ea-acf0-f3edfcded2d2": {
        "status": "success",
        "tags": {
            "acp_enableErrorDiagnostics": true,
            "acp_partialIngestionPercent": 5
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5deac2648a19d218a888d2b1"
            }
        ],
        "id": "af838510-2233-11ea-acf0-f3edfcded2d2",
        "externalId": "af838510-2233-11ea-acf0-f3edfcded2d2",
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "{IMS_ORG}",
        "started": 1576741718543,
        "metrics": {
            "inputByteSize": 568,
            "inputFileCount": 4,
            "inputRecordCount": 519,
            "outputRecordCount": 497,
            "failedRecordCount": 0
        },
        "completed": 1576741722026,
        "created": 1576741597205,
        "createdClient": "{API_KEY}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1576741722644,
        "version": "1.0.5"
    }    
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `metrics.failedRecordCount` | Die Anzahl der Zeilen, die aufgrund der Analyse, Konvertierung oder Validierung nicht verarbeitet werden konnten. Dieser Wert kann durch Subtraktion des Werts `inputRecordCount` vom Wert `outputRecordCount`abgeleitet werden. Dieser Wert wird für alle Stapel generiert, unabhängig davon, ob er aktiviert `errorDiagnostics` ist. |

**Antwort mit Fehlern**

Wenn der Stapel einen oder mehrere Fehler enthält und die Fehlerdiagnose aktiviert ist, gibt die Antwort weitere Informationen zu den Fehlern zurück, sowohl innerhalb der Payload selbst als auch in einer herunterladbaren Fehlerdatei. Beachten Sie, dass der Status eines Stapels, der Fehler enthält, immer noch den Status Erfolg hat.

```json
{
    "01E8043CY305K2MTV5ANH9G1GC": {
        "status": "success",
        "tags": {
            "acp_enableErrorDiagnostics": true,
            "acp_partialIngestionPercent": 5
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5deac2648a19d218a888d2b1"
            }
        ],
        "id": "01E8043CY305K2MTV5ANH9G1GC",
        "externalId": "01E8043CY305K2MTV5ANH9G1GC",
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "{IMS_ORG}",
        "started": 1576741718543,
        "metrics": {
            "inputByteSize": 568,
            "inputFileCount": 4,
            "inputRecordCount": 519,
            "outputRecordCount": 514,
            "failedRecordCount": 5
        },
        "completed": 1576741722026,
        "created": 1576741597205,
        "createdClient": "{API_KEY}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1576741722644,
        "version": "1.0.5",
        "errors": [
           {
             "code": "INGEST-1212-400",
             "description": "Encountered 5 errors in the data. Successfully ingested 514 rows. Please review the associated diagnostic files for more details."
           },
           {
             "code": "INGEST-1401-400",
             "description": "The row has corrupted data and cannot be read or parsed. Fix the corrupted data and try again.",
             "recordCount": 2
           },
           {
             "code": "INGEST-1555-400",
             "description": "A required field is either missing or has a value of null. Add the required field to the input row and try again.",
             "recordCount": 3
           }
        ]
    }
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `metrics.failedRecordCount` | Die Anzahl der Zeilen, die aufgrund der Analyse, Konvertierung oder Validierung nicht verarbeitet werden konnten. Dieser Wert kann durch Subtraktion des Werts `inputRecordCount` vom Wert `outputRecordCount`abgeleitet werden. Dieser Wert wird für alle Stapel generiert, unabhängig davon, ob er aktiviert `errorDiagnostics` ist. |
| `errors.recordCount` | Die Anzahl der Zeilen, die für den angegebenen Fehlercode fehlgeschlagen sind. Dieser Wert wird **nur** generiert, wenn er aktiviert `errorDiagnostics` ist. |

>[!NOTE]
>
>Wenn keine Fehlerdiagnose verfügbar ist, wird stattdessen die folgende Fehlermeldung angezeigt:
>
```json
>{
>       "errors": [{
>               "code": "INGEST-1211-400",
>               "description": "Encountered errors while parsing, converting or otherwise validating the data. Please resend the data with error diagnostics enabled to collect additional information on failure types"
>       }]
>}
>```

## Nächste Schritte {#next-steps}

In diesem Lernprogramm wurde beschrieben, wie Sie Fehler bei der Partiellen Stapelverarbeitung überwachen. Weiterführende Informationen zur Batch-Erfassung finden Sie im [Entwicklerhandbuch zur Batch-Erfassung](../batch-ingestion/api-overview.md).

## Anhang {#appendix}

Dieser Abschnitt enthält zusätzliche Informationen zu den Fehlertypen bei der Aufnahme.

### Fehlertypen bei der partiellen Batch-Erfassung {#partial-ingestion-types}

Bei der Partiellen Stapelverarbeitung gibt es beim Erfassen von Daten drei verschiedene Fehlertypen:

- [Unlesbare Dateien](#unreadable)
- [Ungültige Schemas oder Kopfzeilen](#schemas-headers)
- [Nicht analysierbare Zeilen](#unparsable)

### Unlesbare Dateien {#unreadable}

Wenn der erfasste Batch unlesbare Dateien enthält, werden die Fehler des Batch an den Batch selbst angehängt. Weiterführende Informationen zum Abrufen des fehlgeschlagenen Batch finden Sie im Handbuch zum [Abrufen fehlgeschlagener Batches](../quality/retrieve-failed-batches.md).

### Ungültige Schemas oder Kopfzeilen {#schemas-headers}

Wenn der erfasste Batch ein ungültiges Schema oder ungültige Kopfzeilen enthält, werden die Fehler des Batch an den Batch selbst angehängt. Weiterführende Informationen zum Abrufen des fehlgeschlagenen Batch finden Sie im Handbuch zum [Abrufen fehlgeschlagener Batches](../quality/retrieve-failed-batches.md).

### Nicht analysierbare Zeilen {#unparsable}

Wenn der von Ihnen erfasste Stapel über nicht trennbare Zeilen verfügt, können Sie die folgende Anforderung verwenden, um eine Liste von Dateien mit Fehlermeldungen Ansicht.

**API-Format**

```http
GET /export/batches/{BATCH_ID}/meta?path=row_errors
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Der `id`-Wert des Batch, aus dem Sie Fehlerdaten abrufen. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste der Dateien mit Fehlern zurück.

```json
{
    "data": [
        {
            "name": "conversion_errors_0.json",
            "length": "1162",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors%2Fconversion_errors_0.json"
                }
            }
        },
        {
            "name": "parsing_errors_0.json",
            "length": "153",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors%2Fparsing_errors_0.json"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 2
    }
}
```

Mithilfe des [Diagnoseabfrageendpunkts](#retrieve-diagnostics)können Sie dann detaillierte Informationen zu den Fehlern abrufen.

Nachstehend finden Sie eine Beispielantwort zum Abrufen der Fehlerdatei:

```json
{
    "_corrupt_record": "{missingQuotes: 'v1'}",
    "_errors": [{
        "code": "1401",
        "message": "Row is corrupted and cannot be read, please fix and resend."
    }],
    "_filename": "parsing_errors_0.json"
}
```
