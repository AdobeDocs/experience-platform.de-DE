---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Übersicht zur partiellen Batch-Erfassung in Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: ac75b1858b6a731915bbc698107f0be6043267d8
workflow-type: tm+mt
source-wordcount: '1446'
ht-degree: 40%

---



# Partielle Batch-Erfassung

Partielle Batch-Erfassung ist die Fähigkeit, Daten mit Fehlern bis zu einem bestimmten Schwellenwert zu erfassen. Mit dieser Funktion können Benutzer alle korrekten Daten erfolgreich in Adobe Experience Platform erfassen, während alle fehlerhaften Daten in Batches separat verarbeitet werden (zusammen mit Details dazu, warum sie ungültig sind).

Dieses Dokument enthält eine Anleitung zum Verwalten der partiellen Batch-Erfassung.

Darüber hinaus beinhaltet der [Anhang](#appendix) zu dieser Anleitung eine Referenz zu Fehlertypen bei der partiellen Batch-Erfassung.

## Erste Schritte

Diese Anleitung setzt grundlegende Kenntnisse zu den verschiedenen Adobe Experience Platform-Diensten voraus, die mit der partiellen Batch-Erfassung verbunden sind. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [Batch-Erfassung](./overview.md)[!DNL Platform]: Die Methode, mit der Daten aus Datendateien wie CSV und Parquet erfasst und speichert.
- [[!DNL Experience Data Model] (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Platform] organisiert werden.

The following sections provide additional information that you will need to know in order to successfully make calls to [!DNL Platform] APIs.

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

## Enable a batch for partial batch ingestion in the API {#enable-api}

>[!NOTE]
>
>In diesem Abschnitt wird die Aktivierung eines Stapels für die teilweise Stapelverarbeitung mithilfe der API beschrieben. For instructions on using the UI, please read the [enable a batch for partial batch ingestion in the UI](#enable-ui) step.

Sie können einen neuen Stapel mit aktivierter teilweiser Erfassung erstellen.

Um einen neuen Stapel zu erstellen, führen Sie die Schritte im Entwicklerhandbuch für die [Stapelverarbeitung](./api-overview.md)aus. Once you reach the **[!UICONTROL Create batch]** step, add the following field within the request body:

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercentage": 5
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `enableErrorDiagnostics` | Ein Flag, mit dem detaillierte Fehlermeldungen zum Stapel generiert [!DNL Platform] werden können. |
| `partialIngestionPercentage` | Der Prozentsatz der akzeptablen Fehler, bevor der gesamte Batch fehlschlägt. In diesem Beispiel können also maximal 5 % des Stapels Fehler sein, bevor er fehlschlägt. |


## Enable a batch for partial batch ingestion in the UI {#enable-ui}

>[!NOTE]
>
>In diesem Abschnitt wird beschrieben, wie Sie einen Stapel für die teilweise Stapelverarbeitung mithilfe der Benutzeroberfläche aktivieren. Wenn Sie bereits einen Stapel für die teilweise Stapelverarbeitung mithilfe der API aktiviert haben, können Sie mit dem nächsten Abschnitt fortfahren.

Um einen Stapel für die teilweise Erfassung über die [!DNL Platform] Benutzeroberfläche zu aktivieren, können Sie einen neuen Stapel über Quellverbindungen erstellen, einen neuen Stapel in einem vorhandenen Datensatz erstellen oder einen neuen Stapel über den Fluss[!UICONTROL &quot;CSV zu XDM zuordnen&quot;erstellen].

### Neue Quellverbindung erstellen {#new-source}

Um eine neue Quellverbindung zu erstellen, führen Sie die in der Übersicht über die [Quellen](../../sources/home.md)aufgeführten Schritte aus. Once you reach the **[!UICONTROL Dataflow detail]** step, take note of the **[!UICONTROL Partial ingestion]** and **[!UICONTROL Error diagnostics]** fields.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

Mit dem Umschalter **[!UICONTROL Partielle Erfassung]** können Sie die Verwendung der partiellen Batch-Erfassung aktivieren oder deaktivieren.

The **[!UICONTROL Error diagnostics]** toggle only appears when the **[!UICONTROL Partial ingestion]** toggle is off. This feature allows [!DNL Platform] to generate detailed error messages about your ingested batches. If the *[!UICONTROL Partial ingestion]* toggle is turned on, enhanced error diagnostics are automatically enforced.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

Mit dem **[!UICONTROL Fehlerschwellenwert]** können Sie den Prozentsatz der zulässigen Fehler festlegen, bevor der gesamte Batch fehlschlägt. Standardmäßig ist dieser Wert auf 5 % eingestellt.

### Vorhandenen Datensatz verwenden {#existing-dataset}

Um einen vorhandenen Datensatz zu verwenden, wählen Sie einen Beginn aus, indem Sie einen Datensatz auswählen. Die Seitenleiste rechts enthält Informationen zum Datensatz.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

Mit dem Umschalter **[!UICONTROL Partielle Erfassung]** können Sie die Verwendung der partiellen Batch-Erfassung aktivieren oder deaktivieren.

The **[!UICONTROL Error diagnostics]** toggle only appears when the **[!UICONTROL Partial ingestion]** toggle is off. This feature allows [!DNL Platform] to generate detailed error messages about your ingested batches. If the **[!UICONTROL Partial ingestion]** toggle is turned on, enhanced error diagnostics are automatically enforced.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

Mit dem **[!UICONTROL Fehlerschwellenwert]** können Sie den Prozentsatz der zulässigen Fehler festlegen, bevor der gesamte Batch fehlschlägt. Standardmäßig ist dieser Wert auf 5 % eingestellt.

Jetzt können Sie Daten mit der Schaltfläche **Hinzufügen Daten** hochladen, die dann mit einer teilweisen Erfassung erfasst werden.

### Verwenden Sie den Fluss &quot;CSV[!UICONTROL zu XDM-Schema]zuordnen&quot; {#map-flow}

Um den Fluss &quot;CSV[!UICONTROL zu XDM-Schema]zuordnen&quot;zu verwenden, führen Sie die im Lernprogramm [CSV-Datei](../tutorials/map-a-csv-file.md)zuordnen aufgeführten Schritte aus. Once you reach the **[!UICONTROL Add data]** step, take note of the **[!UICONTROL Partial ingestion]** and **[!UICONTROL Error diagnostics]** fields.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

Mit dem Umschalter **[!UICONTROL Partielle Erfassung]** können Sie die Verwendung der partiellen Batch-Erfassung aktivieren oder deaktivieren.

The **[!UICONTROL Error diagnostics]** toggle only appears when the **[!UICONTROL Partial ingestion]** toggle is off. This feature allows [!DNL Platform] to generate detailed error messages about your ingested batches. If the **[!UICONTROL Partial ingestion]** toggle is turned on, enhanced error diagnostics are automatically enforced.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

Mit dem **[!UICONTROL Fehlerschwellenwert]** können Sie den Prozentsatz der zulässigen Fehler festlegen, bevor der gesamte Batch fehlschlägt. Standardmäßig ist dieser Wert auf 5 % eingestellt.

## Herunterladen von Metadaten auf Dateiebene {#download-metadata}

Adobe Experience Platform ermöglicht es Benutzern, die Metadaten der Eingabedateien herunterzuladen. Die Metadaten werden innerhalb von [!DNL Platform] bis zu 30 Tagen gespeichert.

### Liste-Eingabedateien {#list-files}

Die folgende Anforderung ermöglicht die Ansicht einer Liste aller in einem finalisierten Stapel bereitgestellten Dateien.

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 zurückgegeben, wobei JSON-Objekte Pfadobjekte enthalten, die detailliert angeben, wo die Metadaten gespeichert wurden.

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
                    "href": "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files/fileMetaData1.json"
                }
            },
            "length": "1337",
            "name": "fileMetaData1.json"
        },
                {
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files/fileMetaData2.json"
                }
            },
            "length": "1042",
            "name": "fileMetaData2.json"
        }
    ]
}
```

### Abrufen von Metadaten für Eingabedateien {#retrieve-metadata}

Nachdem Sie eine Liste aller Eingabedateien abgerufen haben, können Sie die Metadaten der einzelnen Datei mit dem folgenden Endpunkt abrufen.

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=input_files/fileMetaData1.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 zurückgegeben, wobei JSON-Objekte Pfadobjekte enthalten, die detailliert angeben, wo die Metadaten gespeichert wurden.

```json
{"path": "F1.json"}
{"path": "etc/F2.json"}
```

## Fehlern bei der partiellen Batch-Erfassung abrufen {#retrieve-errors}

Wenn Batches Fehler enthalten, müssen Sie Fehlerinformationen zu diesen Fehlern abrufen, um die Daten erneut erfassen zu können.

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
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort ohne Fehler**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit detaillierten Informationen zum Batch-Status zurück.

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

Wenn der Stapel einen oder mehrere Fehler enthält und die Fehlerdiagnose aktiviert ist, enthält der Status weitere Informationen zu den Fehlern, die sowohl in der Antwort als auch in einer herunterladbaren Fehlerdatei bereitgestellt werden. `success`

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
> {
>         "errors": [{
>                 "code": "INGEST-1211-400",
>                 "description": "Encountered errors while parsing, converting or otherwise validating the data. Please resend the data with error diagnostics enabled to collect additional information on failure types"
>         }]
> }
> ```

## Nächste Schritte {#next-steps}

In dieser Anleitung wurde beschrieben, wie Sie einen Datensatz erstellen oder ändern, um die partielle Batch-Erfassung zu aktivieren. Weiterführende Informationen zur Batch-Erfassung finden Sie im [Entwicklerhandbuch zur Batch-Erfassung](./api-overview.md).

## Fehlertypen bei der partiellen Batch-Erfassung {#appendix}

Bei der Partiellen Stapelverarbeitung gibt es beim Erfassen von Daten drei verschiedene Fehlertypen.

- [Unlesbare Dateien](#unreadable)
- [Ungültige Schemas oder Kopfzeilen](#schemas-headers)
- [Nicht analysierbare Zeilen](#unparsable)

### Unlesbare Dateien {#unreadable}

Wenn der erfasste Batch unlesbare Dateien enthält, werden die Fehler des Batch an den Batch selbst angehängt. Weiterführende Informationen zum Abrufen des fehlgeschlagenen Batch finden Sie im Handbuch zum [Abrufen fehlgeschlagener Batches](../quality/retrieve-failed-batches.md).

### Ungültige Schemas oder Kopfzeilen {#schemas-headers}

Wenn der erfasste Batch ein ungültiges Schema oder ungültige Kopfzeilen enthält, werden die Fehler des Batch an den Batch selbst angehängt. Weiterführende Informationen zum Abrufen des fehlgeschlagenen Batch finden Sie im Handbuch zum [Abrufen fehlgeschlagener Batches](../quality/retrieve-failed-batches.md).

### Nicht analysierbare Zeilen {#unparsable}

Wenn der von Ihnen erfasste Stapel über nicht trennbare Zeilen verfügt, können Sie den folgenden Endpunkt verwenden, um eine Liste von Dateien mit Fehlermeldungen Ansicht.

**API-Format**

```http
GET /export/batches/{BATCH_ID}/meta?path=row_errors
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BATCH_ID}` | Der `id`-Wert des Batch, aus dem Sie Fehlerdaten abrufen. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/meta?path=row_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit einer Liste der Dateien zurück, die Fehler aufweisen.

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

Mithilfe des [Metadaten-Abrufendpunkts](#retrieve-metadata)können Sie dann detaillierte Informationen zu den Fehlern abrufen.

Nachstehend finden Sie eine Beispielantwort zum Abrufen der Fehlerdatei:

```json
{
    "_corrupt_record": "{missingQuotes: "v1"}",
    "_errors": [{
        "code": "1401",
        "message": "Row is corrupted and cannot be read, please fix and resend."
    }],
    "_filename": "parsing_errors_0.json"
}
```
