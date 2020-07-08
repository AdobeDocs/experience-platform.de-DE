---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Übersicht über die Adobe Experience Platform Batch Ingestion
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 2%

---


# Batch Ingestion - Übersicht

Mit der Stapeleinbetungs-API können Sie Daten als Batch-Dateien in die Adobe Experience Platform aufnehmen. Daten, die erfasst werden, können Profil-Daten aus einer reduzierten Datei in einem CRM-System (z. B. eine Parkettdatei) oder Daten sein, die einem bekannten Schema in der XDM-Registrierung (Experience Data Model) entsprechen.

Der [Data Ingestion API-Verweis](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) enthält weitere Informationen zu diesen API-Aufrufen.

Das folgende Diagramm zeigt den Vorgang der Stapelverarbeitung:

![](../images/batch-ingestion/overview/batch_ingestion.png)

## Verwenden der API

Mit der Dateneinbettungsschnittstelle können Sie Daten als Stapel (eine Dateneinheit, die aus einer oder mehreren Dateien besteht, die als Einheit erfasst werden sollen) in drei Schritten in die Experience Platform aufnehmen:

1. Erstellen Sie einen neuen Stapel.
2. Hochladen von Dateien in einen angegebenen Datensatz, der dem XDM-Schema der Daten entspricht.
3. Signalisieren Sie das Ende des Stapels.


### Voraussetzungen für die Datenauffüllung

- Die hochzuladenden Daten müssen im Parquet- oder JSON-Format vorliegen.
- Ein in den [Katalogdiensten](../../catalog/home.md)erstellter Datensatz.
- Der Inhalt der Parkettdatei muss mit einer Untergruppe des Schemas des hochgeladenen Datensatzes übereinstimmen.
- Lassen Sie sich nach der Authentifizierung Ihr eindeutiges Zugriffstoken anzeigen.

### Best Practices zur Stapelerfassung

- Die empfohlene Stapelgröße liegt zwischen 256 MB und 100 GB.
- Jeder Stapel sollte maximal 1500 Dateien enthalten.

Um eine Datei hochzuladen, die größer als 512 MB ist, muss die Datei in kleinere Abschnitte unterteilt werden. Anweisungen zum Hochladen einer großen Datei finden Sie [hier](#large-file-upload---create-file).

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

Für alle Anforderungen mit einer Payload (POST, PUT, PATCH) ist ein zusätzlicher Header erforderlich:

- Content-Type: application/json

### Stapel erstellen

Bevor Daten zu einem Datensatz hinzugefügt werden können, müssen sie mit einem Stapel verknüpft werden, der später in einen bestimmten Datensatz hochgeladen wird.

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
| `id` | Die ID des soeben erstellten Stapels (in nachfolgenden Anforderungen verwendet). |
| `relatedObjects.id` | Die ID des Datensatzes, in den die Dateien hochgeladen werden sollen. |

## Datei-Upload

Nachdem Sie erfolgreich einen neuen Stapel zum Hochladen erstellt haben, können Dateien in einen bestimmten Datensatz hochgeladen werden.

Sie können Dateien mit der **Small File Upload-API** hochladen. Wenn Ihre Dateien jedoch zu groß sind und das Gateway-Limit überschritten wird (z. B. erweiterte Timeouts, Anforderungen für die Körpergröße und andere Einschränkungen), können Sie zur **Large File Upload-API** wechseln. Diese API lädt die Datei in Textbausteinen hoch und ordnet Daten mithilfe des **Aufrufs &quot;Large File Upload Complete API** &quot;zusammen.

>[!NOTE]
>
>Die folgenden Beispiele verwenden das [Parquet](https://parquet.apache.org/documentation/latest/) -Dateiformat. Ein Beispiel, das das JSON-Dateiformat verwendet, finden Sie im Entwicklerhandbuch für [Stapelverarbeitung](./api-overview.md).

### Kleine Datei hochladen

Nachdem ein Stapel erstellt wurde, können Daten in einen bereits vorhandenen Datensatz hochgeladen werden.  Die hochgeladene Datei muss mit dem referenzierten XDM-Schema übereinstimmen.

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{BATCH_ID}` | Die ID des Stapels. |
| `{DATASET_ID}` | Die ID des Datensatzes, in den Dateien hochgeladen werden sollen. |
| `{FILE_NAME}` | Der Name der Datei, wie er im Datensatz angezeigt wird. |

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

### Hochladen großer Dateien - Datei erstellen

Um eine große Datei hochzuladen, muss die Datei in kleinere Abschnitte aufgeteilt und einzeln hochgeladen werden.

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}?action=initialize
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{BATCH_ID}` | Die ID des Stapels. |
| `{DATASET_ID}` | Die ID des Datensatzes, in dem die Dateien enthalten sind. |
| `{FILE_NAME}` | Der Name der Datei, wie er im Datensatz angezeigt wird. |

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

### Hochladen großer Dateien - Laden Sie nachfolgende Teile hoch

Nachdem die Datei erstellt wurde, können alle nachfolgenden Abschnitte durch wiederholte PATCH-Anfragen hochgeladen werden, jeweils einen für jeden Abschnitt der Datei.

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{BATCH_ID}` | Die ID des Stapels. |
| `{DATASET_ID}` | Die ID des Datensatzes, in den die Dateien hochgeladen werden sollen. |
| `{FILE_NAME}` | Name der Datei, wie sie im Datensatz angezeigt wird. |

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

## Batch-Fertigstellung

Nachdem alle Dateien in den Stapel hochgeladen wurden, kann der Stapel zur Fertigstellung signalisiert werden. Auf diese Weise werden die **DataSetFile** -Einträge des Katalogs für die abgeschlossenen Dateien erstellt und mit dem oben generierten Stapel verknüpft. Der Katalogstapel wird dann als erfolgreich markiert, wodurch nachgelagerte Flüsse zur Erfassung der verfügbaren Daten ausgelöst werden.

**Anfrage**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{BATCH_ID}` | Die ID des Stapels, der in den Datensatz hochgeladen werden soll. |

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

## Stapelstatus prüfen

Während darauf gewartet wird, dass die Dateien in den Stapel hochgeladen werden, kann der Status des Stapels überprüft werden, um den Fortschritt zu sehen.

**API-Format**

```http
GET /batch/{BATCH_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{BATCH_ID}` | Die ID des überprüften Stapels. |

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
| `{USER_ID}` | Die ID des Benutzers, der den Stapel erstellt oder aktualisiert hat. |

Das `"status"` Feld zeigt den aktuellen Status des angeforderten Stapels an. Die Stapel können einen der folgenden Status haben:

## Stapelverarbeitungsstatus

| Status | Beschreibung |
| ------ | ----------- |
| Abgebrochen | Der Stapel wurde nicht im erwarteten Zeitrahmen abgeschlossen. |
| Abgebrochen | Für den angegebenen Stapel wurde **explizit** ein Abbruchvorgang (über die Batch Ingest-API) aufgerufen. Wenn sich der Stapel im **Status &quot;Geladen** &quot;befindet, kann er nicht abgebrochen werden. |
| Aktiv | Die Charge wurde erfolgreich beworben und steht für den nachgelagerten Verbrauch zur Verfügung. Dieser Status kann synonym mit **Erfolg** verwendet werden. |
| Gelöscht | Die Daten für den Stapel wurden vollständig entfernt. |
| Fehlgeschlagen | Ein Terminal-Status, der entweder auf eine fehlerhafte Konfiguration und/oder auf fehlerhafte Daten zurückzuführen ist. Daten für einen fehlgeschlagenen Stapel werden **nicht** angezeigt. Dieser Status kann synonym mit **Failure** verwendet werden. |
| Inaktiv | Der Stapel wurde erfolgreich beworben, wurde jedoch zurückgesetzt oder ist abgelaufen. Die Partie ist nicht mehr für den nachgelagerten Verbrauch verfügbar. |
| geladen | Die Daten für den Stapel sind abgeschlossen und der Stapel kann beworben werden. |
| Laden | Daten für diesen Stapel werden hochgeladen und der Stapel kann derzeit **nicht** beworben werden. |
| Wiederholung | Die Daten für diesen Stapel werden verarbeitet. Aufgrund eines System- oder vorübergehenden Fehlers ist der Stapel jedoch fehlgeschlagen. Daher wird dieser Stapel erneut versucht. |
| Gestaffelt | Die Staging-Phase des Promotion-Prozesses für einen Stapel ist abgeschlossen und der Erfassungsauftrag wurde ausgeführt. |
| Staging | Die Daten für den Stapel werden verarbeitet. |
| Angehalten | Die Daten für den Stapel werden verarbeitet. Die Batch-Promotion wurde jedoch nach einigen weiteren Zustellversuchen angehalten. |