---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Datensatzes mithilfe von APIs
topic: datasets
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '1234'
ht-degree: 82%

---


# Erstellen eines Datensatzes mithilfe von APIs

In diesem Dokument werden die grundlegenden Schritte für die Erstellung eines Datensatzes mithilfe der Adobe Experience Platform-APIs erläutert und aufgezeigt, wie der Datensatz anhand einer Datei befüllt wird.

## Erste Schritte

Diese Anleitung setzt Grundkenntnisse der folgenden Komponenten von Adobe Experience Platform voraus:

* [Stapelverarbeitung](../../ingestion/batch-ingestion/overview.md): [!DNL Experience Platform] erlaubt Ihnen, Daten als Batch-Dateien zu erfassen.
* [!DNL Experience Data Model (XDM) System](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Experience Platform] organisiert werden.
* [!DNL Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

The following sections provide additional information that you will need to know in order to successfully make calls to the [!DNL Platform] APIs.

### Lesehilfe für Beispiel-API-Aufrufe

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dabei wird auf Pfade ebenso eingegangen wie auf die erforderlichen Kopfzeilen und die für Anfrage-Payloads zu verwendende Formatierung. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Die in der Dokumentation zu Beispielen für API-Aufrufe verwendeten Konventionen werden im Handbuch zur Fehlerbehebung für unter [Lesehilfe für Beispiel-API-Aufrufe](../../landing/troubleshooting.md#how-do-i-format-an-api-request) erläutert.[!DNL Experience Platform]

### Werte der zu verwendenden Kopfzeilen

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

Alle Anfragen, die eine Payload enthalten (also POST-, PUT- und PATCH-Anfragen), erfordern eine zusätzliche Kopfzeile:

* Content-Type: application/json

## Tutorial

Um einen Datensatz zu erstellen, muss zunächst ein Schema definiert werden. Ein Schema ist ein Satz von Regeln für die Darstellung von Daten. Schemas dienen zur Beschreibung der Datenstruktur. Über sie können zugleich auch Einschränkungen und Erwartungen angewendet werden, um Daten bei ihrem Austausch zwischen Systemen zu validieren.

Dank dieser Standarddefinitionen ist eine konsistente Interpretation von Daten unabhängig von ihrer Herkunft möglich, was auch deren Übersetzung für unterschiedliche Anwendungen unnötig macht. Weitere Informationen zur Erstellung von Schemas finden Sie unter [Grundlagen zum Aufbau von Schemas](../../xdm/schema/composition.md)

## Nachschlagen eines Datensatzschemas

Dieses Tutorial setzt das im [Tutorial zur Schema Registry API](../../xdm/tutorials/create-schema-api.md) Gelernte fort und greift dazu das darin erstellte „Loyalty Members“-Schema auf.

If you have not completed the [!DNL Schema Registry] tutorial, please start there and continue with this dataset tutorial only once you have composed the necessary schema.

The following call can be used to view the Loyalty Members schema you created during the [!DNL Schema Registry] API tutorial:

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

Das Format der Objektausgabe von der in der Anfrage verwendeten Accept-Kopfzeile ab. Die einzelnen Eigenschaften in dieser Antwort wurden aus Platzgründen ausgeblendet.

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

## Erstellen eines Datensatzes

Mit dem vorliegenden „Loyalty Members“-Schema können Sie jetzt einen Datensatz erstellen, der auf das Schema verweist.

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

>[!NOTE]
>
>Für alle Beispiele in diesem Tutorial wird das [Parquet](https://parquet.apache.org/documentation/latest/)-Dateiformat verwendet. Ein Beispiel unter Verwendung des JSON-Dateiformats finden Sie im [Batch-Aufnahme-Entwicklerhandbuch](../../ingestion/batch-ingestion/api-overview.md).

**Antwort**

Bei erfolgreicher Anfrage wird der HTTP-Statuscode 201 (Erstellung bestätigt) mit einem Antwortobjekt zurückgegeben, das ein Array mit der ID des neu erstellten Datensatzes im Format `"@/datasets/{DATASET_ID}"` beinhaltet. Die Datensatz-ID ist eine schreibgeschützte, vom System generierte Zeichenfolge, die als Verweis auf den Datensatz in API-Aufrufen dient.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```

## Erstellen eines Batches

Bevor Sie Daten zu einem Datensatz hinzufügen können, müssen Sie einen Batch erstellen, der dem Datensatz zugeordnet ist. Der Batch wird dann zum Hochladen verwendet.

**API-Format**

```HTTP
POST /batches
```

**Anfrage**

Der Anfragetext umfasst das Feld „datasetId“ mit dem Wert `{DATASET_ID}`, der im vorherigen Schritt generiert wurde.

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

Bei erfolgreicher Anfrage wird der HTTP-Statuscode 201 (Erstellung bestätigt) mit einem Antwortobjekt zurückgegeben, das den neu erstellten Batch einschließlich seiner `id`, einer schreibgeschützten, vom System generierten Zeichenfolge beinhaltet.

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

## Hochladen von Dateien in einen Batch

Nachdem der Batch für den Upload erfolgreich erstellt wurde, können Sie Dateien in den jeweiligen Datensatz hochladen. Hierbei ist zu beachten, dass Sie für den Datensatz das Parquet-Dateiformat definiert haben. Demensprechend können sie nur Dateien hochladen, die in diesem Format vorliegen.

>[!NOTE]
>
>Die maximal unterstützte Dateigröße für den Daten-Upload beträgt 512 MB. Wenn Ihre Datendatei diese Größe übersteigt, muss sie in Blöcke von maximal 512 MB unterteilt werden, die nacheinander hochgeladen werden. Um die einzelnen Dateien in den Batch hochzuladen, wiederholen Sie diesen Schritt für jede Datei unter Verwendung derselben Batch-ID. Für die Anzahl der für den Upload in einem Batch enthaltenen Dateien bestehen keine Beschränkungen.

**API-Format**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{BATCH_ID}` | Die `id` des Batches, in den Sie hochladen. |
| `{DATASET_ID}` | Die `id` des Datensatzes, in dem der Batch festgehalten wird. |
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

Bei erfolgreichem Upload einer Datei wird für diese ein leerer Antworttext und der HTTP-Statuscode 200 (OK) zurückgegeben.

## Kennzeichnen der Fertigstellung eines Batches

Nachdem Sie alle Ihre Datendateien in den Batch hochgeladen haben, können Sie ihn als fertiggestellt kennzeichnen. Signaling completion causes the service to create [!DNL Catalog] `DataSetFile` entries for the uploaded files and associate them with the batch generated previously. The [!DNL Catalog] batch is marked successful, which triggers any downstream flows that can then work on the now available data.

**API-Format**

```HTTP
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parameter | Beschreibung |
| --- | --- |
| `{BATCH_ID}` | Die `id` des Batches, den Sie als fertiggestellt markieren. |

**Anfrage**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c?action=COMPLETE" \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Antwort**

Bei erfolgreicher Fertigstellung eines Batches wird für diesen ein leerer Antworttext und der HTTP-Statuscode 200 (OK) zurückgegeben.

## Überwachen der Datenaufnahme

Abhängig vom jeweiligen Datenvolumen beansprucht die Batch-Aufnahme unterschiedlich viel Zeit. Sie können den Status eines Batches überwachen, indem Sie den Anfrageparameter `batch` unter Angabe der Batch-ID an eine `GET /batches`-Anfrage anfügen. Die API ruft den Status des im Datensatz aufzunehmenden Batches so lange ab, bis in der Antwort der `status` der Fertigstellung als erfolgreich („success“) bzw. fehlgeschlagen („failure“) angegeben wird.

**API-Format**

```HTTP
GET /batches?batch={BATCH_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{BATCH_ID}` | Die `id` des Batches, den Sie überwachen möchten. |

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

Eine positive Antwort gibt ein Objekt zurück, dessen Attribut `status` den Wert `success` aufweist:

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

Eine negative Antwort gibt ein Objekt mit dem Wert `"failed"` im Attribut `"status"` sowie alle zugehörigen Fehlermeldungen zurück:

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

>[!NOTE]
>
>Als Abrufintervall werden zwei Minuten empfohlen.

## Einlesen von Daten aus dem Datensatz

Sie können über die Batch-ID die Data Access API aufrufen, um die in einen Batch hochgeladenen Dateien einzulesen und zu überprüfen. Die Antwort gibt ein Array mit einer Liste von Datei-IDs zurück, die jeweils auf eine im Batch enthaltene Datei verweisen.

Sie können die Data Access API auch verwenden, um den Namen, die Größe in Bytes und einen Link zum Herunterladen der Datei oder des Ordners abzurufen.

Einzelheiten zur Arbeit mit der Data Access API finden Sie im [Entwicklerhandbuch zum Thema Datenzugriff](../../data-access/home.md).

## Aktualisieren des Datensatzschemas

Sie können Felder hinzufügen und zusätzliche Daten in von Ihnen erstellten Datensätzen aufnehmen. Dazu müssen Sie zunächst das Schema aktualisieren, indem Sie zusätzliche Eigenschaften hinzufügen, die die neuen Daten definieren. Die Aktualisierung eines vorhandenen Schemas erfolgt mittels PATCH- und/oder PUT-Operationen.

Weitere Informationen zur Aktualisierung von Schemas finden Sie im [Schema Registry API-Entwicklerhandbuch](../../xdm/api/getting-started.md).

Nach Aktualisierung des Schemas können Sie neue, mit dem überarbeiteten Schema übereinstimmende Daten aufnehmen, indem Sie die in diesem Tutorial erläuterten Schritte wiederholen.

Wichtig dabei: Die Entwicklung von Schemas ist vollständig additiv ausgelegt, d. h., ein Schema kann nicht mehr grundlegend verwendet werden, wenn es einmal in der Registry gespeichert und zur Datenaufnahme verwendet wurde. Weitere Informationen zu Best Practices rund um die Erstellung von Schemas für die Verwendung mit Adobe Experience Platform finden Sie unter [Grundlagen zum Aufbau von Schemas](../../xdm/schema/composition.md).