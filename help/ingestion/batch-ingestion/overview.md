---
keywords: Experience Platform;Startseite;beliebte Themen;Datenaufnahme;Batch;Batch;Datensatz aktivieren;Übersicht zur Batch-Aufnahme;Übersicht;Übersicht zur Batch-Aufnahme;
solution: Experience Platform
title: Übersicht über die Batch-Aufnahme-API
description: Mit der Batch-Aufnahme-API von Adobe Experience Platform können Sie Daten als Batch-Dateien in Experience Platform aufnehmen. Bei den aufgenommenen Daten kann es sich um Profildaten aus einer flachen Datei in einem CRM-System (z. B. einer Parquet-Datei) oder um Daten handeln, die einem bekannten Schema in der Registrierung des Experience-Datenmodells (XDM) entsprechen.
exl-id: ffd1dc2d-eff8-4ef7-a26b-f78988f050ef
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1390'
ht-degree: 65%

---

# Übersicht über die Batch-Aufnahme-API

Mit der Batch-Aufnahme-API von Adobe Experience Platform können Sie Daten als Batch-Dateien in Experience Platform aufnehmen. Bei den aufgenommenen Daten kann es sich um Profildaten aus einer flachen Datei (z. B. einer Parquet-Datei) oder um Daten handeln, die einem bekannten Schema in der [!DNL Experience Data Model] (XDM)-Registrierung entsprechen.

Die [Referenz zur Batch](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)Aufnahme-API enthält zusätzliche Informationen zu diesen API-Aufrufen.

Das folgende Diagramm zeigt den Vorgang der Batch-Erfassung.

![](../images/batch-ingestion/overview/batch_ingestion.png)

## Erste Schritte

Die in diesem Handbuch verwendeten API-Endpunkte sind Teil der [Batch-Aufnahme-API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/). Bevor Sie fortfahren, lesen Sie das Handbuch [Erste Schritte](getting-started.md) mit Links zur zugehörigen Dokumentation, einer Anleitung zum Lesen der API-Beispielaufrufe in diesem Dokument und wichtigen Informationen zu den erforderlichen Kopfzeilen, die für die erfolgreiche Ausführung von Aufrufen an eine Experience Platform-API erforderlich sind.

### Voraussetzungen für [!DNL Data Ingestion]

- Die hochzuladenden Daten müssen im Parquet- oder JSON-Format vorliegen.
- Ein in der [[!DNL Catalog services]](../../catalog/home.md) erstellter Datensatz.
- Der Inhalt der Parquet-Datei muss mit einer Teilmenge des Schemas des Datensatzes übereinstimmen, in den hochgeladen wird.
- Lassen Sie sich nach der Authentifizierung Ihr eindeutiges Zugriffstoken anzeigen.

### Best Practices zur Batch-Erfassung

- Die empfohlene Batch-Größe liegt zwischen 256 MB und 100 GB.
- Jeder Batch sollte maximal 1500 Dateien enthalten.

### Einschränkungen bei der Batch-Aufnahme

Die Erfassung von Batch-Daten unterliegt verschiedenen Einschränkungen:

- Maximale Anzahl von Dateien pro Batch: 1.500
- Maximale Batch-Größe: 100 GB
- Maximale Anzahl von Eigenschaften oder Feldern pro Zeile: 10.000
- Maximale Anzahl von Batches auf dem Data Lake pro Minute und Benutzer: 2000

>[!NOTE]
>
>Um eine Datei hochzuladen, die größer als 512 MB ist, muss die Datei in kleinere Abschnitte unterteilt werden. Anweisungen zum Hochladen einer großen Datei finden Sie im Abschnitt [Hochladen großer Dateien dieses Dokuments](#large-file-upload---create-file).

### Typen

Bei der Datenaufnahme müssen Sie wissen, wie [!DNL Experience Data Model] (XDM)-Schemata funktionieren. Weiterführende Informationen zur Zuordnung von XDM-Feldtypen zu verschiedenen Formaten finden Sie im [Entwicklerhandbuch zur Schemaregistrierung](../../xdm/api/getting-started.md).

Es gibt eine gewisse Flexibilität bei der Aufnahme von Daten - wenn ein Typ nicht mit dem übereinstimmt, was im Zielschema ist, werden die Daten in den ausgedrückten Zieltyp konvertiert. Wenn das nicht möglich ist, schlägt der Batch mit einer `TypeCompatibilityException` fehl.

Beispielsweise haben weder JSON noch CSV den Typ `date` oder `date-time`. Daher werden diese Werte mit [ISO 8601-formatierten Zeichenfolgen](https://www.iso.org/iso-8601-date-and-time-format.html) („2018-07-10T15:05:59.000-08:00„) oder in Millisekunden (1531263959000) formatierter Unix-Zeit ausgedrückt und zur Aufnahmezeit in den Ziel-XDM-Typ konvertiert.

Folgende Tabelle enthält die Konversionen, die beim Erfassen von Daten unterstützt werden.

| Eingehend (Zeile) vs. Ziel (Spalte) | Zeichenfolge | Byte | Kurz | Ganzzahl | Lang | Double | Datum | Datum/Uhrzeit | Objekt | Zuordnung |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Zeichenfolge | X | X | X | X | X | X | X | X |   |   |
| Byte | X | X | X | X | X | X |   |   |   |   |
| Kurz | X | X | X | X | X | X |   |   |   |   |
| Ganzzahl | X | X | X | X | X | X |   |   |   |   |
| Lang | X | X | X | X | X | X | X | X |   |   |
| Double | X | X | X | X | X | X |   |   |   |   |
| Datum |   |   |   |   |   |   | X |   |   |   |
| Datum/Uhrzeit |   |   |   |   |   |   |   | X |   |   |
| Objekt |   |   |   |   |   |   |   |   | X | X |
| Zuordnung |   |   |   |   |   |   |   |   | X | X |

>[!NOTE]
>
>Boolesche Werte und Arrays können nicht in andere Typen konvertiert werden.

## Verwenden der API

Mit der [!DNL Data Ingestion]-API können Sie Daten als Batches (eine Dateneinheit, die aus einer oder mehreren Dateien besteht, die als einzelne Einheit aufgenommen werden sollen) in drei grundlegenden Schritten in [!DNL Experience Platform] aufnehmen:

1. Erstellen eines neuen Batches.
2. Hochladen von Dateien in einen angegebenen Datensatz, der dem XDM-Schema der Daten entspricht.
3. Signalisieren des Batch-Endes.

## Erstellen eines Batches

Bevor Daten zu einem Datensatz hinzugefügt werden können, müssen sie mit einem Batch verknüpft werden, der später in einen bestimmten Datensatz hochgeladen wird.

```http
POST /batches
```

**Anfrage**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
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

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `id` | Die ID des soeben erstellten Batches (in nachfolgenden Anfragen verwendet). |
| `relatedObjects.id` | Die ID des Datensatzes, in den die Dateien hochgeladen werden sollen. |

## Datei-Upload

Nachdem Sie erfolgreich einen neuen Batch zum Hochladen erstellt haben, können Dateien in einen bestimmten Datensatz hochgeladen werden.

Sie können Dateien mithilfe der Small File Upload-API hochladen. Wenn Ihre Dateien jedoch zu groß sind und das Gateway-Limit überschritten wird (z. B. verlängerte Zeitüberschreitungen, Anfragen nach Körpergröße überschritten und andere Einschränkungen), können Sie zur API für den Upload großer Dateien wechseln. Diese API lädt die Datei in Blöcken hoch und ordnet Daten mithilfe des API-Aufrufs zum Abschließen des Uploads großer Dateien zusammen.

>[!NOTE]
>
>Die Batch-Aufnahme kann verwendet werden, um Daten im Profilspeicher inkrementell zu aktualisieren. Weitere Informationen finden Sie im Abschnitt [Aktualisieren eines Batches](#patch-a-batch) im [Entwicklerhandbuch zur Batch-Aufnahme](api-overview.md).

>[!INFO]
>
>In den folgenden Beispielen wird das [Apache Parquet](https://parquet.apache.org/docs/)-Dateiformat verwendet. Ein Beispiel, das das JSON-Dateiformat verwendet, finden Sie im [Entwicklerhandbuch zur Batch-Erfassung](api-overview.md).

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
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
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
  -H "x-gw-ims-org-id: {ORG_ID}" \
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
  -H "x-gw-ims-org-id: {ORG_ID}" \
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

Nachdem alle Dateien in den Batch hochgeladen wurden, kann dieser als fertiggestellt gekennzeichnet werden. Dadurch werden die [!DNL Catalog] DataSetFile-Einträge für die abgeschlossenen Dateien erstellt und mit dem oben generierten Batch verknüpft. Der [!DNL Catalog]-Batch wird dann als erfolgreich markiert, wodurch bei nachgelagerten Flüssen die Aufnahme der verfügbaren Daten ausgelöst wird.

**Anfrage**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{BATCH_ID}` | Die ID des Batches, der in den Datensatz hochgeladen werden soll. |

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
-H "x-gw-ims-org-id: {ORG_ID}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key: {API_KEY}"
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
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

**Antwort**

```JSON
{
    "{BATCH_ID}": {
        "imsOrg": "{ORG_ID}",
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
| Abgebrochen | Für den angegebenen Stapel wurde **explizit** ein Unterbrechungsvorgang (über die Batch-Aufnahme-API) aufgerufen. Sobald sich der Batch im Status „Geladen“ befindet, kann er nicht mehr abgebrochen werden. |
| Aktiv | Der Batch wurde erfolgreich gefördert und steht für den nachgelagerten Verbrauch zur Verfügung. Dieser Status kann synonym mit „Erfolg“ verwendet werden. |
| Gelöscht | Die Daten für den Batch wurden vollständig entfernt. |
| Fehlgeschlagen | Ein Terminal-Status, der entweder auf eine fehlerhafte Konfiguration und/oder auf fehlerhafte Daten zurückzuführen ist. Daten für einen fehlgeschlagenen Batch werden **nicht** angezeigt. Dieser Status kann synonym mit „Failure“ verwendet werden. |
| Inaktiv | Der Batch wurde erfolgreich gefördert, wurde jedoch zurückgesetzt oder ist abgelaufen. Der Batch ist nicht mehr für den nachgelagerten Verbrauch verfügbar. |
| Geladen | Die Daten für den Batch sind abgeschlossen und der Stapel kann gefördert werden. |
| Wird geladen | Daten für diesen Batch werden hochgeladen und der Batch kann derzeit noch **nicht** gefördert werden. |
| Wird wiederholt | Die Daten für diesen Batch werden verarbeitet. Aufgrund eines System- oder vorübergehenden Fehlers ist der Batch jedoch fehlgeschlagen. Daher wird für diesen Batch ein erneuter Versuch unternommen. |
| Staging | Die Staging-Phase des Förderungsprozesses für einen Batch ist abgeschlossen und der Aufnahmeauftrag wurde ausgeführt. |
| Staging | Die Daten für den Batch werden verarbeitet. |
| Angehalten | Die Daten für den Batch werden verarbeitet. Die Batch-Förderung wurde jedoch nach einigen weiteren erneuten Versuchen angehalten. |
