---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Datensatzes mit APIs
topic: datasets
translation-type: tm+mt
source-git-commit: a6a1ecd9ce49c0a55e14b0d5479ca7315e332904
workflow-type: tm+mt
source-wordcount: '1263'
ht-degree: 1%

---


# Erstellen eines Datensatzes mit APIs

In diesem Dokument werden allgemeine Schritte zum Erstellen eines Datensatzes mit Adobe Experience Platform-APIs und zum Ausfüllen des Datensatzes mit einer Datei beschrieben.

## Erste Schritte

Dieses Handbuch erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

* [Stapelverarbeitung](../../ingestion/batch-ingestion/overview.md): Mit Experience Platform können Sie Daten als Batch-Dateien erfassen.
* [Erlebnis-Datenmodell (XDM)-System](../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
* [Sandboxen](../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Plattforminstanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die Plattform-APIs erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Lernprogramm finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

### Werte für erforderliche Kopfzeilen sammeln

Um Aufrufe an Plattform-APIs durchzuführen, müssen Sie zunächst das [Authentifizierungstraining](../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungstreutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform API-Aufrufen bereit, wie unten dargestellt:

* Genehmigung: Träger `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in Experience Platform werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an Plattform-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Weitere Informationen zu Sandboxes in Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Für alle Anforderungen mit einer Payload (POST, PUT, PATCH) ist ein zusätzlicher Header erforderlich:

* Content-Type: application/json

## Tutorial

Um einen Datensatz zu erstellen, muss zunächst ein Schema definiert werden. Ein Schema ist ein Regelsatz, der die Darstellung von Daten unterstützt. Schema beschreiben nicht nur die Datenstruktur, sondern bieten auch Einschränkungen und Erwartungen, die angewendet und zur Validierung von Daten verwendet werden können, während sie zwischen Systemen verschoben werden.

Mit diesen Standarddefinitionen können Daten unabhängig von der Herkunft konsistent interpretiert werden. Zudem entfällt die Notwendigkeit für anwendungsübergreifende Übersetzungen. Weitere Informationen zum Erstellen von Schemas finden Sie im Leitfaden zu den [Grundlagen der Schema-Komposition](../../xdm/schema/composition.md)

## Schema des Datensatzes nachschlagen

Dieses Tutorial beginnt an der Stelle, an der das [Schema Registry API-Tutorial](../../xdm/tutorials/create-schema-api.md) endet, wobei das Schema der Treuemitglieder verwendet wird, das während dieses Tutorials erstellt wurde.

Wenn Sie das Lernprogramm zur Registrierung des Schemas noch nicht abgeschlossen haben, Beginn bitte dort und fahren Sie mit diesem Lernprogramm nur fort, nachdem Sie das erforderliche Schema erstellt haben.

Der folgende Aufruf kann zur Ansicht des Schemas &quot;Treuemitglieder&quot;verwendet werden, das Sie im Lernprogramm zur Schema-Registrierung-API erstellt haben:

**API-Format**

```HTTP
GET /tenant/schemas/{schema meta:altId or URL encoded $id URI}
```

**Anfrage**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Das Format des Antwortobjekts hängt vom Accept-Header ab, der in der Anforderung gesendet wird. Die einzelnen Eigenschaften in dieser Antwort wurden aus Platzgründen minimiert.

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "properties": {
        "repositoryCreatedBy": {},
        "repositoryLastModifiedBy": {},
        "createdByBatchID": {},
        "modifiedByBatchID": {},
        "_repo": {},
        "identityMap": {},
        "_id": {},
        "timeSeriesEvents": {},
        "person": {},
        "homeAddress": {},
        "personalEmail": {},
        "homePhone": {},
        "mobilePhone": {},
        "faxPhone": {},
        "_{TENANT_ID}": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "loyalty": {
                    "title": "Loyalty",
                    "description": "Loyalty Info",
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:referencedFrom": "https://ns.adobe.com/{TENANT_ID}/datatypes/49b594dabe6bec545c8a6d1a0991a4dd",
                    "properties": {
                        "loyaltyId": {
                            "title": "Loyalty Identifier",
                            "type": "string",
                            "description": "Loyalty Identifier.",
                            "meta:xdmType": "string"
                        },
                        "loyaltyLevel": {
                            "title": "Loyalty Level",
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "loyaltyPoints": {
                            "title": "Loyalty Points",
                            "type": "integer",
                            "description": "Loyalty points total.",
                            "meta:xdmType": "int"
                        },
                        "memberSince": {
                            "title": "Member Since",
                            "type": "string",
                            "format": "date-time",
                            "description": "Date the member joined the Loyalty Program.",
                            "meta:xdmType": "date-time"
                        }
                    }
                }
            }
        }
    },
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.4",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551843052271,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## Datensatz erstellen

Mit dem Schema &quot;Treuemitglieder&quot;können Sie jetzt einen Datensatz erstellen, der auf das Schema verweist.

**API-Format**

```HTTP
POST /dataSets
```

**Anfrage**

```SHELL
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name":"LoyaltyMembersDataset",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    }
}'
```

>[!NOTE] In diesem Tutorial wird das [Parquet](https://parquet.apache.org/documentation/latest/) -Dateiformat für alle Beispiele verwendet. Ein Beispiel, das das JSON-Dateiformat verwendet, finden Sie im Entwicklerhandbuch für die [Stapelverarbeitung](../../ingestion/batch-ingestion/api-overview.md)

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 201 (Erstellt) und ein Antwortobjekt zurück, das aus einem Array mit der ID des neu erstellten Datensatzes im Format `"@/datasets/{DATASET_ID}"`besteht. Die DataSet-ID ist eine schreibgeschützte, systemgenerierte Zeichenfolge, mit der auf den Datensatz in API-Aufrufen verwiesen wird.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```

## Stapel erstellen

Bevor Sie Daten zu einem Datensatz hinzufügen können, müssen Sie einen Stapel erstellen, der mit dem Datensatz verknüpft ist. Der Stapel wird dann zum Hochladen verwendet.

**API-Format**

```HTTP
POST /batches
```

**Anfrage**

Der Anforderungstext enthält das Feld &quot;datasetId&quot;, dessen Wert der im vorherigen Schritt `{DATASET_ID}` generierte Wert ist.

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

**Antwort**

Bei einer erfolgreichen Antwort werden HTTP-Status 201 (Erstellt) und ein Antwortobjekt mit Details zum neu erstellten Stapel zurückgegeben, einschließlich einer `id`schreibgeschützten, vom System erstellten Zeichenfolge.

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{IMS_ORG}",
    "updated": 1552694873602,
    "status": "loading",
    "created": 1552694873602,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "5c8c3c555033b814b69f947f"
        }
    ],
    "version": "1.0.0",
    "tags": {
        "acp_producer": [
            "{CREATED_CLIENT}"
        ],
        "acp_stagePath": [
            "{CREATED_CLIENT}/stage/5d01230fc78a4e4f8c0c6b387b4b8d1c"
        ],
        "use_plan_b_batch_status": [
            "false"
        ]
    },
    "createdUser": "{CREATED_BY}",
    "updatedUser": "{CREATED_BY}",
    "externalId": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "createdClient": "{CREATED_CLIENT}",
    "inputFormat": {
        "format": "parquet"
    }
}
```

## Hochladen von Dateien in einen Stapel

Nachdem Sie erfolgreich einen neuen Stapel zum Hochladen erstellt haben, können Sie jetzt Dateien in den jeweiligen Datensatz hochladen. Beachten Sie, dass Sie bei der Definition des Datensatzes das Dateiformat als Parkett angegeben haben. Daher müssen die hochgeladenen Dateien in diesem Format vorliegen.

>[!NOTE] Die größte unterstützte Datei zum Hochladen von Daten ist 512 MB. Wenn Ihre Datendatei größer als diese ist, muss sie in Blöcke mit nicht mehr als 512 MB aufgeteilt werden, die einzeln hochgeladen werden sollen. Sie können jede Datei im selben Stapel hochladen, indem Sie diesen Schritt für jede Datei wiederholen und dieselbe Stapel-ID verwenden. Die Anzahl der hochzuladenden Dateien ist unbegrenzt.

**API-Format**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{BATCH_ID}` | Der `id` Stapel, in den Sie hochladen. |
| `{DATASET_ID}` | Der `id` Datensatz, in dem der Stapel beibehalten wird. |
| `{FILE_NAME}` | Der Name der Datei, die Sie hochladen. |

**Anfrage**

```SHELL
curl -X PUT 'https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c/datasets/5c8c3c555033b814b69f947f/files/loyaltyData.parquet' \
  -H 'content-type: application/octet-stream' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  --data-binary '@{FILE_PATH_AND_NAME}.parquet'
```

**Antwort**

Eine erfolgreich hochgeladene Datei gibt einen leeren Antworttext und HTTP-Status 200 (OK) zurück.

## Batch-Fertigstellung

Nachdem Sie alle Ihre Datendateien in den Stapel hochgeladen haben, können Sie den Stapel zur Fertigstellung signalisieren. Nach Abschluss der Signalisierung erstellt der Dienst Katalogeinträge `DataSetFile` für die hochgeladenen Dateien und verknüpft sie mit dem zuvor erstellten Stapel. Der Katalogstapel ist als erfolgreich markiert, wodurch alle nachgelagerten Flüsse ausgelöst werden, die dann mit den jetzt verfügbaren Daten arbeiten können.

**API-Format**

```HTTP
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parameter | Beschreibung |
| --- | --- |
| `{BATCH_ID}` | Der `id` Stapel, den Sie als abgeschlossen kennzeichnen. |

**Anfrage**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c?action=COMPLETE" \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Antwort**

Ein erfolgreich abgeschlossener Stapel gibt einen leeren Antworttext und HTTP-Status 200 zurück (OK).

## Überwachen der Erfassung

Je nach Datengröße dauert die Erfassung von Stapeln unterschiedlich lange. Sie können den Status eines Stapels überwachen, indem Sie einen `batch` Anforderungsparameter mit der Batch-ID an eine `GET /batches` Anforderung anhängen. Die API fragt den Datensatz nach dem Status des Stapels von der Erfassung ab, bis der `status` in der Antwort angegebene Abschluss (&quot;Erfolg&quot;oder &quot;Fehler&quot;) angezeigt wird.

**API-Format**

```HTTP
GET /batches?batch={BATCH_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{BATCH_ID}` | Der `id` zu überwachende Stapel. |

**Anfrage**

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?batch=5d01230fc78a4e4f8c0c6b387b4b8d1c' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Antwort**

Eine positive Antwort gibt ein Objekt zurück, dessen `status` Attribut den Wert `success`:

```JSON
{
    "5b7129a879323401ef2a6486": {
        "imsOrg": "{IMS_ORG}",
        "created": 1534142888068,
        "createdClient": "{CREATED_CLIENT}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1534142955152,
        "replay": {},
        "status": "success",
        "errors": [],
        "version": "1.0.3",
        "availableDates": {},
        "relatedObjects": [
            {
                "type": "batch",
                "id": "29285e08378f4a41827e7e70fb7cb8f0"
            }
        ],
        "metrics": {
            "startTime": 1534142943819,
            "endTime": 1534142951760,
            "recordsRead": 108,
            "recordsWritten": 108
        }
    }
}
```

Eine negative Antwort gibt ein Objekt mit dem Wert `"failed"` in seinem `"status"` Attribut zurück und enthält alle relevanten Fehlermeldungen:

```JSON
{
    "5b96ce65badcf701e51f075d": {
        "imsOrg": "{IMS_ORG}",
        "status": "failed",
        "relatedObjects": [
            {
                "type": "batch",
                "id": "29285e08378f4a41827e7e70fb7cb8f0"
            }
        ],
        "replay": {},
        "availableDates": {},
        "metrics": {
            "startTime": 1536610322329,
            "endTime": 1536610438083,
            "recordsRead": 4004,
            "recordsWritten": 4004,
            "failureReason": "Job aborted due to stage failure: Task 0 in stage 1.0 failed 4 times,:"
        },
        "errors": [
            {
                "code": "0070000017",
                "description": "Unknown error occurred."
            },
            {
                "code": "unknown",
                "description": "Job aborted."
            }
        ],
        "created": 1536609893629,
        "createdClient": "{CREATED_CLIENT}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1536610442814,
        "version": "1.0.5"
    }
}
```

>[!NOTE] Ein empfohlener Abfrageintervall beträgt zwei Minuten.

## Daten aus dem Datensatz lesen

Mit der Stapel-ID können Sie die Datenzugriff-API verwenden, um alle Dateien, die in den Stapel hochgeladen wurden, zu lesen und zu überprüfen. Die Antwort gibt ein Array mit einer Liste von Datei-IDs zurück, wobei jede Datei im Stapel auf eine Datei verweist.

Sie können die Datenzugriff-API auch verwenden, um den Namen, die Größe in Byte und einen Link zum Herunterladen der Datei oder des Ordners zurückzugeben.

Ausführliche Anweisungen zum Arbeiten mit der Datenzugriffs-API finden Sie im Entwicklerhandbuch für [Datenzugriff](../../data-access/home.md).

## Schema des Datensatzes aktualisieren

Sie können Felder hinzufügen und zusätzliche Daten in von Ihnen erstellte Datensätze erfassen. Dazu müssen Sie zunächst das Schema aktualisieren, indem Sie zusätzliche Eigenschaften hinzufügen, die die neuen Daten definieren. Dies kann mithilfe von PATCH- und/oder PUT-Vorgängen erfolgen, um das vorhandene Schema zu aktualisieren.

Weitere Informationen zum Aktualisieren von Schemas finden Sie im [Schema Registry API Developer Guide](../../xdm/api/getting-started.md).

Nachdem Sie das Schema aktualisiert haben, können Sie die Schritte in diesem Lernprogramm wiederholen, um neue Daten zu erfassen, die dem überarbeiteten Schema entsprechen.

Es ist wichtig, sich zu merken, dass die Evolution des Schemas rein additiv ist, d. h., dass ein Schema nicht mehr verändert werden darf, sobald es in der Registrierung gespeichert und zur Datenaufnahme verwendet wurde. Weitere Informationen zu Best Practices für das Erstellen von Schema zur Verwendung mit Adobe Experience Platform finden Sie im Handbuch zu den [Grundlagen der Schema-Komposition](../../xdm/schema/composition.md).