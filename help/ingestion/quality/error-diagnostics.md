---
keywords: Experience Platform;Startseite;beliebte Themen;Batch-Aufnahme;Batch-Aufnahme;partielle Aufnahme;partielle Aufnahme;Fehler abrufen;Fehler abrufen;partielle Batch-Aufnahme;partielle Batch-Aufnahme;partielle Aufnahme;Aufnahme;Fehlerdiagnose;Fehlerdiagnose abrufen;Fehlerdiagnose abrufen;Fehler abrufen;Fehler abrufen;Fehler abrufen;
solution: Experience Platform
title: Abrufen der Fehlerdiagnose für die Datenaufnahme
description: Dieses Dokument enthält Informationen zur Überwachung der Batch-Aufnahme, zur Verwaltung von Fehlern bei der partiellen Batch-Aufnahme sowie eine Referenz für Typen der partiellen Batch-Aufnahme.
exl-id: b885fb00-b66d-453b-80b7-8821117c2041
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 36%

---

# Abrufen der Fehlerdiagnose für die Datenaufnahme

Adobe Experience Platform bietet für den Upload und die Aufnahme von Daten zwei Methoden. Sie können entweder die Batch-Aufnahme verwenden, mit der Sie Daten mithilfe verschiedener Dateitypen (z. B. CSVs) einfügen können, oder die Streaming-Aufnahme, mit der Sie ihre Daten mithilfe von Streaming-Endpunkten in Echtzeit in [!DNL Experience Platform] einfügen können.

Dieses Dokument enthält Informationen zur Überwachung der Batch-Aufnahme, zur Verwaltung von Fehlern bei der partiellen Batch-Aufnahme sowie eine Referenz für Typen der partiellen Batch-Aufnahme.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von [!DNL Experience Platform] organisiert werden.
- [[!DNL Adobe Experience Platform Data Ingestion]](../home.md): Die Methoden, mit denen Daten an [!DNL Experience Platform] gesendet werden können.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Experience Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform], einschließlich der Ressourcen, die zum [!DNL Schema Registry] gehören, sind in bestimmten virtuellen Sandboxes isoliert. Bei allen Anfragen an [!DNL Experience Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in [!DNL Experience Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

## Herunterladen der Fehlerdiagnose {#download-diagnostics}

Mit Adobe Experience Platform können Benutzer die Fehlerdiagnose der Eingabedateien herunterladen. Die Diagnose wird innerhalb von [!DNL Experience Platform] bis zu 30 Tage aufbewahrt.

### Auflisten von Eingabedateien {#list-files}

Die folgende Anfrage ruft eine Liste aller Dateien ab, die in einem fertigen Batch bereitgestellt werden.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort werden JSON-Objekte zurückgegeben, die detailliert beschreiben, wo die Diagnose gespeichert wurde.

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

### Abrufen von Eingabedateidiagnosen {#retrieve-diagnostics}

Nachdem Sie eine Liste aller verschiedenen Eingabedateien abgerufen haben, können Sie die Diagnose der einzelnen Datei mithilfe der folgenden Anfrage abrufen.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort werden JSON-Objekte mit `path` Objekten zurückgegeben, die detailliert beschreiben, wo die Diagnose gespeichert wurde. Die Antwort gibt die `path` Objekte im Format [JSON-Zeilen](https://jsonlines.readthedocs.io/en/latest/) zurück.

```json
{"path": "F1.json"}
{"path": "etc/F2.json"}
```

## Abrufen von Batch-Erfassungsfehlern {#retrieve-errors}

Wenn Batches Fehler enthalten, sollten Sie Fehlerinformationen zu diesen Fehlern abrufen, damit Sie die Daten erneut aufnehmen können.

### Status prüfen {#check-status}

Um den Status des erfassten Batches zu überprüfen, müssen Sie die ID des Batches im Pfad einer GET-Anfrage angeben. Weitere Informationen zur Verwendung dieses API-Aufrufs finden Sie im [Handbuch für Catalog-Endpunkte](../../catalog/api/list-objects.md).

**API-Format**

```http
GET /catalog/batches/{BATCH_ID}
GET /catalog/batches/{BATCH_ID}?{FILTER}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Der `id`-Wert des Batch, dessen Status Sie überprüfen möchten. |
| `{FILTER}` | Ein Abfrageparameter, mit dem die in der Antwort zurückgegebenen Ergebnisse gefiltert werden. Mehrere Parameter werden durch das kaufmännische Und-Zeichen (`&`) getrennt. Weitere Informationen finden Sie im Handbuch unter [Filtern von Katalogdaten](../../catalog/api/filter-data.md). |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/af838510-2233-11ea-acf0-f3edfcded2d2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Fehlerfreie Antwort**

Eine erfolgreiche Antwort gibt mit detaillierten Informationen zum Status des Batches zurück.

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
        "imsOrg": "{ORG_ID}",
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
| `metrics.failedRecordCount` | Die Anzahl der Zeilen, die aufgrund von Parsing, Konversion oder Validierung nicht verarbeitet werden konnten. Dieser Wert kann durch Subtrahieren der `inputRecordCount` von der `outputRecordCount` abgeleitet werden. Dieser Wert wird für alle Batches generiert, unabhängig davon, ob `errorDiagnostics` aktiviert ist. |

**Fehlerbehebung**

Wenn für den Batch mindestens ein Fehler vorhanden und die Fehlerdiagnose aktiviert ist, gibt die Antwort weitere Informationen zu den Fehlern zurück, sowohl innerhalb der Payload selbst als auch in einer herunterladbaren Fehlerdatei. Beachten Sie, dass der Status eines Stapels mit Fehlern immer noch den Status Erfolg haben kann.

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
        "imsOrg": "{ORG_ID}",
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
| `metrics.failedRecordCount` | Die Anzahl der Zeilen, die aufgrund von Parsing, Konversion oder Validierung nicht verarbeitet werden konnten. Dieser Wert kann durch Subtrahieren der `inputRecordCount` von der `outputRecordCount` abgeleitet werden. Dieser Wert wird für alle Batches generiert, unabhängig davon, ob `errorDiagnostics` aktiviert ist. |
| `errors.recordCount` | Die Anzahl der Zeilen, die für den angegebenen Fehlercode fehlgeschlagen sind. Dieser Wert wird **nur** generiert, wenn `errorDiagnostics` aktiviert ist. |

>[!NOTE]
>
>Wenn keine Fehlerdiagnose verfügbar ist, wird stattdessen die folgende Fehlermeldung angezeigt:
>
>```json
>{
>       "errors": [{
>               "code": "INGEST-1211-400",
>               "description": "Encountered errors while parsing, converting or otherwise validating the data. Please resend the data with error diagnostics enabled to collect additional information on failure types"
>       }]
>}
>```

## Nächste Schritte {#next-steps}

In diesem Tutorial wurde beschrieben, wie Sie Fehler bei der partiellen Batch-Aufnahme überwachen. Weiterführende Informationen zur Batch-Erfassung finden Sie im [Entwicklerhandbuch zur Batch-Erfassung](../batch-ingestion/api-overview.md).

## Anhang {#appendix}

Dieser Abschnitt enthält zusätzliche Informationen zu Fehlertypen bei der Aufnahme.

### Fehlertypen bei der partiellen Batch-Erfassung {#partial-ingestion-types}

Die partielle Batch-Aufnahme hat drei verschiedene Fehlertypen bei der Datenaufnahme:

- [Unlesbare Dateien](#unreadable)
- [Ungültige Schemata oder Kopfzeilen](#schemas-headers)
- [Nicht analysierbare Zeilen](#unparsable)

### Unlesbare Dateien {#unreadable}

Wenn der erfasste Batch unlesbare Dateien enthält, werden die Fehler des Batch an den Batch selbst angehängt. Weiterführende Informationen zum Abrufen des fehlgeschlagenen Batch finden Sie im Handbuch zum [Abrufen fehlgeschlagener Batches](../quality/retrieve-failed-batches.md).

### Ungültige Schemata oder Kopfzeilen {#schemas-headers}

Wenn der erfasste Batch ein ungültiges Schema oder ungültige Kopfzeilen enthält, werden die Fehler des Batch an den Batch selbst angehängt. Weiterführende Informationen zum Abrufen des fehlgeschlagenen Batch finden Sie im Handbuch zum [Abrufen fehlgeschlagener Batches](../quality/retrieve-failed-batches.md).

### Nicht analysierbare Zeilen {#unparsable}

Wenn der aufgenommene Batch unparable Zeilen enthält, können Sie die folgende Anfrage verwenden, um eine Liste von Dateien mit Fehlern anzuzeigen.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste der Dateien zurück, die Fehler aufweisen.

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

Sie können dann detaillierte Informationen zu den Fehlern über den Endpunkt [Diagnoseabruf“ ](#retrieve-diagnostics).

Nachfolgend finden Sie eine Beispielantwort zum Abrufen der Fehlerdatei:

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
