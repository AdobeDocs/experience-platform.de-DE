---
keywords: Experience Platform; Startseite; beliebte Themen; Datensatz; Datensatz; Datensatz; Datensatz erstellen; Datensatz erstellen
solution: Experience Platform
title: Datensatz mit APIs erstellen
description: In diesem Dokument werden die grundlegenden Schritte für die Erstellung eines Datensatzes mithilfe der Adobe Experience Platform-APIs erläutert und aufgezeigt, wie der Datensatz anhand einer Datei befüllt wird.
exl-id: 3a5f48cf-ad05-4b9e-be1d-ff213a26a477
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '1304'
ht-degree: 87%

---

# Erstellen eines Datensatzes mithilfe von APIs

In diesem Dokument werden die grundlegenden Schritte für die Erstellung eines Datensatzes mithilfe der Adobe Experience Platform-APIs erläutert und aufgezeigt, wie der Datensatz anhand einer Datei befüllt wird.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Batch-Erfassung](../../ingestion/batch-ingestion/overview.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten als Batch-Dateien.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von [!DNL Experience Platform] organisiert werden.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um erfolgreich Aufrufe an die [!DNL Platform] APIs.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an [!DNL Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

* Content-Type: application/json

## Tutorial

Um einen Datensatz zu erstellen, muss zunächst ein Schema definiert werden. Ein Schema ist ein Satz von Regeln für die Darstellung von Daten. Schemas dienen zur Beschreibung der Datenstruktur. Über sie können zugleich auch Einschränkungen und Erwartungen angewendet werden, um Daten bei ihrem Austausch zwischen Systemen zu validieren.

Diese Standarddefinitionen ermöglichen eine konsistente Interpretation der Daten, unabhängig von ihrer Herkunft, und machen eine anwendungsübergreifende Übersetzung überflüssig. Weitere Informationen zur Erstellung von Schemas finden Sie unter [Grundlagen zum Aufbau von Schemas](../../xdm/schema/composition.md)

## Nachschlagen eines Datensatzschemas

Dieses Tutorial setzt das im [Tutorial zur Schema Registry-API](../../xdm/tutorials/create-schema-api.md) Gelernte fort und greift dazu das darin erstellte „Loyalty Members“-Schema auf.

Wenn Sie die [!DNL Schema Registry] Tutorial, beginnen Sie dort und fahren Sie mit diesem Tutorial nur fort, wenn Sie das erforderliche Schema erstellt haben.

Der folgende Aufruf kann verwendet werden, um das &quot;Loyalty Members&quot;-Schema anzuzeigen, das Sie während der [!DNL Schema Registry] API-Tutorial:

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "imsOrg": "{ORG_ID}",
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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name":"LoyaltyMembersDataset",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    }
}'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `schemaRef.id` | Der URI-`$id`-Wert für das XDM-Schema, auf dem der Datensatz basieren soll. |
| `schemaRef.contentType` | Gibt das Format und die Version des Schemas an. Weitere Informationen finden Sie im Abschnitt zur [Schemaversionierung](../../xdm/api/getting-started.md#versioning) im XDM-API-Handbuch. |

>[!NOTE]
>
>In diesem Tutorial wird die [Apache Parquet](https://parquet.apache.org/docs/) Dateiformat für alle Beispiele. Ein Beispiel unter Verwendung des JSON-Dateiformats finden Sie im [Entwicklerhandbuch zur Batch-Erfassung](../../ingestion/batch-ingestion/api-overview.md).

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 (Erstellt) und ein Antwortobjekt zurück, das aus einem Array mit der Kennung des neu erstellten Datensatzes im Format `"@/datasets/{DATASET_ID}"` besteht. Die Datensatz-ID ist eine schreibgeschützte, vom System generierte Zeichenfolge, mit der in API-Aufrufen auf den Datensatz verwiesen wird.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

**Antwort**

Bei erfolgreicher Antwort wird der HTTP-Status-Code 201 (Erstellung bestätigt) mit einem Antwortobjekt zurückgegeben, das den neu erstellten Batch einschließlich seiner `id`, einer schreibgeschützten, vom System generierten Zeichenfolge, beinhaltet.

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{ORG_ID}",
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

Nachdem der Batch für den Upload erfolgreich erstellt wurde, können Sie Dateien in den jeweiligen Datensatz hochladen. Beachten Sie dabei, dass Sie bei der Definition des Datensatzes das Dateiformat als Parquet angegeben haben. Demensprechend können sie nur Dateien hochladen, die in diesem Format vorliegen.

>[!NOTE]
>
> Die maximal unterstützte Dateigröße für den Daten-Upload beträgt 512 MB. Wenn Ihre Datendatei diese Größe übersteigt, muss sie in Blöcke von maximal 512 MB unterteilt werden, die nacheinander hochgeladen werden. Um die einzelnen Dateien in den Batch hochzuladen, wiederholen Sie diesen Schritt für jede Datei unter Verwendung derselben Batch-ID. Für die Anzahl der für den Upload in einem Batch enthaltenen Dateien bestehen keine Beschränkungen.

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
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  --data-binary '@{FILE_PATH_AND_NAME}.parquet'
```

**Antwort**

Bei erfolgreichem Upload einer Datei wird für diese ein leerer Antworttext und der HTTP-Statu-Code 200 (OK) zurückgegeben.

## Kennzeichnen der Fertigstellung eines Batches

Nachdem Sie alle Ihre Datendateien in den Batch hochgeladen haben, können Sie ihn als fertiggestellt kennzeichnen. Die Fertigstellung der Signatur bewirkt, dass der Dienst [!DNL Catalog] `DataSetFile` -Einträge für die hochgeladenen Dateien und verknüpfen sie mit dem zuvor generierten Batch. Die [!DNL Catalog] Batch wurde als erfolgreich markiert, wodurch alle nachgelagerten Flüsse Trigger werden, die dann mit den jetzt verfügbaren Daten arbeiten können.

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
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Antwort**

Bei erfolgreicher Fertigstellung eines Batches wird für diesen ein leerer Antworttext und der HTTP-Status-Code 200 (OK) zurückgegeben.

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
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Antwort**

Eine positive Antwort gibt ein Objekt zurück, dessen Attribut `status` den Wert `success` aufweist:

```JSON
{
    "5b7129a879323401ef2a6486": {
        "imsOrg": "{ORG_ID}",
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
        "imsOrg": "{ORG_ID}",
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

Weitere Informationen zur Aktualisierung von Schemas finden Sie im [Schema Registry-API-Entwicklerhandbuch](../../xdm/api/getting-started.md).

Nach Aktualisierung des Schemas können Sie neue, mit dem überarbeiteten Schema übereinstimmende Daten aufnehmen, indem Sie die in diesem Tutorial erläuterten Schritte wiederholen.

Wichtig dabei: Die Entwicklung von Schemas ist vollständig additiv ausgelegt, d. h., ein Schema kann nicht mehr grundlegend verwendet werden, wenn es einmal in der Registry gespeichert und zur Datenaufnahme verwendet wurde. Weitere Informationen zu Best Practices rund um die Erstellung von Schemas für die Verwendung mit Adobe Experience Platform finden Sie unter [Grundlagen zum Aufbau von Schemas](../../xdm/schema/composition.md).
