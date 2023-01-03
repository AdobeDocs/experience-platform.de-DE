---
keywords: Experience Platform;Startseite;beliebte Themen;Cloud-Speicherdaten;Streaming-Daten;Streaming
solution: Experience Platform
title: Erstellen eines Streaming-Datenflusses für Rohdaten mithilfe der Flow Service-API
topic-legacy: overview
type: Tutorial
description: In diesem Tutorial werden die Schritte zum Abrufen von Streaming-Daten und deren Einbindung in Platform mithilfe von Quell-Connectoren und APIs beschrieben.
exl-id: 898df7fe-37a9-4495-ac05-30029258a6f4
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 55%

---

# Erstellen Sie einen Streaming-Datenfluss für Rohdaten mithilfe der [!DNL Flow Service] API

In diesem Tutorial werden die Schritte zum Abrufen von Rohdaten aus einem Streaming-Quell-Connector und zum Übertragen dieser Daten in die Experience Platform mithilfe des [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten ordnet.
   - [Grundlagen der Schemakomposition](../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemakomposition.
   - [Entwicklerhandbuch zur Schema Registry](../../../../xdm/api/getting-started.md): Enthält wichtige Informationen, die Sie benötigen, um die Schema Registry API erfolgreich aufrufen zu können. Diese umfassen Ihre `{TENANT_ID}`, das Konzept sogenannter „Container“ und die für Anfragen erforderlichen Kopfzeilen, von denen insbesondere die Accept-Kopfzeile und deren mögliche Werte wichtig sind.
- [[!DNL Catalog Service]](../../../../catalog/home.md): Der Katalog ist das „System of Record“ für den Speicherort und die Herkunft von Daten in Experience Platform.
- [[!DNL Streaming ingestion]](../../../../ingestion/streaming-ingestion/overview.md): Die Streaming-Erfassung für Platform bietet Benutzern eine Methode, Daten von Client- und Server-seitigen Geräten in Echtzeit an die Experience Platform zu senden.
- [Sandboxes](../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Verwenden von Platform-APIs

Informationen darüber, wie Sie Platform-APIs erfolgreich aufrufen können, finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../landing/api-guide.md).

### Erstellen einer Quellverbindung {#source}

Für dieses Tutorial benötigen Sie außerdem eine gültige Quell-Verbindungs-ID für einen Streaming-Connector. Wenn Sie diese Informationen nicht haben, lesen Sie die folgenden Tutorials zum Erstellen einer Streaming-Quellverbindung , bevor Sie dieses Tutorial ausführen:

- [[!DNL Amazon Kinesis]](../create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../create/cloud-storage/eventhub.md)
- [[!DNL Google PubSub]](../create/cloud-storage/google-pubsub.md)

## Erstellen eines XDM-Zielschemas {#target-schema}

Damit die Quelldaten in Platform verwendet werden können, muss ein Zielschema erstellt werden, das die Quelldaten entsprechend Ihren Anforderungen strukturiert. Das Zielschema wird dann verwendet, um einen Platform-Datensatz zu erstellen, in dem die Quelldaten enthalten sind. Dieses Ziel-XDM-Schema erweitert auch das XDM-Schema [!DNL Individual Profile] -Klasse.

Um ein Ziel-XDM-Schema zu erstellen, stellen Sie eine POST-Anfrage an die `/schemas` Endpunkt der [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

**API-Format**

```http
POST /tenant/schemas
```

**Anfrage**

Die folgende Beispielanfrage erstellt ein XDM-Schema, das das XDM-Schema erweitert [!DNL Individual Profile] -Klasse.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "type": "object",
        "title": "Sample schema for a streaming connector",
        "description": "Sample schema for a streaming connector",
        "allOf": [
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
            }
        ],
        "meta:containerId": "tenant",
        "meta:resourceType": "schemas",
        "meta:xdmType": "object",
        "meta:class": "https://ns.adobe.com/xdm/context/profile"
    }'
```

**Antwort**

Eine erfolgreiche Antwort gibt Details zum neu erstellten Schema einschließlich der eindeutigen Kennung (`$id`). Diese ID ist in späteren Schritten erforderlich, um einen Zieldatensatz, eine Zielzuordnung und einen Datenfluss zu erstellen.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
    "meta:altId": "_{TENANT_ID}.schemas.e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Sample schema for a streaming connector",
    "type": "object",
    "description": "Sample schema for a streaming connector",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1604960074752,
        "repo:lastModifiedDate": 1604960074752,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{MODIFIED_USER_ID}",
        "eTag": "8522a151effd974429518ed90c3eaf6efc9bf6ffb6644087a85c6d4455dcd045",
        "meta:globalLibVersion": "1.16.1"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "{SANDBOX_ID}",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Erstellen eines Zieldatensatzes

Mit einem erstellten Ziel-XDM-Schema und seiner eindeutigen `$id` Sie können jetzt einen Zieldatensatz erstellen, der Ihre Quelldaten enthält. Um einen Zieldatensatz zu erstellen, stellen Sie eine POST-Anfrage an die `dataSets` Endpunkt der [Catalog Service-API](https://www.adobe.io/experience-platform-apis/references/catalog/), während die ID des Zielschemas in der Payload angegeben wird.

**API-Format**

```http
POST /catalog/dataSets
```

**Anfrage**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Test streaming dataset",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        },
        "tags": {
            "identity": [
            "enabled:true"
            ],
            "profile": [
            "enabled:true"
            ]
        }
    }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name des zu erstellenden Datensatzes. |
| `schemaRef.id` | Der URI `$id` für das XDM-Schema, auf dem der Datensatz basieren wird. |
| `schemaRef.contentType` | Die Version des Schemas. Dieser Wert muss auf `application/vnd.adobe.xed-full-notext+json;version=1`, die die neueste Nebenversion des Schemas zurückgibt. Weitere Informationen finden Sie im Abschnitt zur [Schemaversionierung](../../../../xdm/api/getting-started.md#versioning) im XDM-API-Handbuch. |

**Antwort**

Eine erfolgreiche Antwort gibt ein Array zurück, das die Kennung des neu erstellten Datensatzes im Format enthält `"@/datasets/{DATASET_ID}"`. Die Datensatz-ID ist eine schreibgeschützte, vom System generierte Zeichenfolge, mit der in API-Aufrufen auf den Datensatz verwiesen wird. Die Ziel-Datensatz-ID ist in späteren Schritten erforderlich, um eine Zielverbindung und einen Datenfluss zu erstellen.

```json
[
    "@/dataSets/5f7187bac6d00f194fb937c0"
]
```

## Erstellen einer Zielverbindung {#target-connection}

Target-Verbindungen erstellen und verwalten eine Zielverbindung zu Platform oder einem beliebigen Standort, an dem die übertragenen Daten landen. Target-Verbindungen enthalten Informationen zu Datenziel, Datenformat und der Zielverbindungs-ID, die zum Erstellen eines Datenflusses erforderlich ist. Target-Verbindungsinstanzen sind spezifisch für einen Mandanten und eine IMS-Organisation.

Um eine Zielverbindung zu erstellen, stellen Sie eine POST-Anfrage an die `/targetConnections` Endpunkt der [!DNL Flow Service] API. Im Rahmen der Anfrage müssen Sie das Datenformat, das `dataSetId` im vorherigen Schritt abgerufen wurden, und die ID der festen Verbindungsspezifikation, an die [!DNL Data Lake]. Diese ID lautet `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

**API-Format**

```http
POST /targetConnections
```

**Anfrage**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Streaming target connection",
        "description": "Streaming target connection",
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        },
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5f7187bac6d00f194fb937c0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID, die für die Verbindung mit der [!DNL Data Lake]. Diese ID lautet: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | Das angegebene Format der Daten, die Sie an [!DNL Data Lake]. |
| `params.dataSetId` | Die ID des Zieldatensatzes, der im vorherigen Schritt abgerufen wurde. |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung der neuen Zielverbindung an (`id`). Diese ID ist in späteren Schritten erforderlich.

```json
{
    "id": "d9300194-6a82-4163-b001-946a821163b8",
    "etag": "\"4006d3e4-0000-0200-0000-5f7189220000\""
}
```

## Erstellen einer Zuordnung {#mapping}

Damit die Quelldaten in einen Zieldatensatz aufgenommen werden können, müssen sie zunächst dem Zielschema zugeordnet werden, zu dem der Zieldatensatz gehört.

Um einen Zuordnungssatz zu erstellen, senden Sie eine POST-Anfrage an den `mappingSets`-Endpunkt der [[!DNL Data Prep] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-prep.yaml), wobei Sie das Ziel-XDM-Schema `$id` und die Details der Zuordnungssätze, die Sie erstellen möchten, angeben.

**API-Format**

```http
POST /mappingSets
```

**Anfrage**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "_{TENANT_ID}.schemas.e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
        "xdmVersion": "1.0",
        "mappings": [
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "firstName",
                "identity": false,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "lastName",
                "identity": false,
                "version": 0
            }
        ]
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `xdmSchema` | `$id` des XDM-Zielschemas. |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Zuordnung zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist in einem späteren Schritt erforderlich, um einen Datenfluss zu erstellen.

```json
{
    "id": "380b032b445a46008e77585e046efe5e",
    "version": 0,
    "createdDate": 1604960750613,
    "modifiedDate": 1604960750613,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Abrufen einer Liste von Datenfluss-Spezifikationen {#specs}

Ein Datenfluss sorgt für die Erfassung von Daten aus Quellen und deren Aufnahme in Platform. Um einen Datenfluss zu erstellen, müssen Sie zunächst die Datenflussspezifikationen abrufen, indem Sie eine GET-Anfrage an die [!DNL Flow Service]-API senden.

**API-Format**

```http
GET /flowSpecs
```

**Anfrage**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Datenflug-Spezifikationen zurück. Die Datenflug-Spezifikations-ID, die Sie abrufen müssen, um einen Datenfluss mit einem der folgenden Elemente zu erstellen [!DNL Amazon Kinesis], [!DNL Azure Event Hubs]oder  [!DNL Google PubSub], ist `d69717ba-71b4-4313-b654-49f9cf126d7a`.

```json
{
    "items": [
        {
            "id": "d69717ba-71b4-4313-b654-49f9cf126d7a",
            "name": "Stream data with optional transformation",
            "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
            "version": "1.0",
            "sourceConnectionSpecIds": [
                "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
                "86043421-563b-46ec-8e6c-e23184711bf6",
                "70116022-a743-464a-bbfe-e226a7f8210c"
            ],
            "targetConnectionSpecIds": [
                "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
                "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                "db4fe783-ef79-4a12-bda9-32b2b1bc3b2c"
            ],
            "transformationSpecs": [
                {
                    "name": "Mapping",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines various params required for different mapping from source to target",
                        "properties": {
                            "mappingId": {
                                "type": "string"
                            }
                        }
                    }
                }
            ],
            "attributes": {
                "uiAttributes": {
                    "apiFeatures": {
                        "flowRunsSupported": false
                    }
                }
            },
            "permissionsInfo": {
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "StreamingSource",
                        "permissions": [
                            "read"
                        ]
                    }
                ],
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "StreamingSource",
                        "permissions": [
                            "write"
                        ]
                    }
                ]
            }
        },
    ]
}
```

## Erstellen eines Datenflusses

Der letzte Schritt bei der Erfassung von Streaming-Daten besteht in der Erstellung eines Datenflusses. Bislang haben Sie die folgenden erforderlichen Werte vorbereitet:

- [Quellverbindungs-ID](#source)
- [Zielverbindungs-ID](#target)
- [Zuordnungs-ID](#mapping)
- [Datenflussspezifikations-ID](#specs)

Ein Datenfluss ist für die Planung und Erfassung von Daten aus einer Quelle verantwortlich. Sie können einen Datenfluss erstellen, indem Sie eine POST-Anfrage ausführen und dabei die oben genannten Werte in der Payload angeben.

**API-Format**

```http
POST /flows
```

**Anfrage**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Streaming dataflow",
        "description": "Streaming dataflow",
        "flowSpec": {
            "id": "d69717ba-71b4-4313-b654-49f9cf126d7a",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "e96d6135-4b50-446e-922c-6dd66672b6b2"
        ],
        "targetConnectionIds": [
            "723222e2-6ab9-4b0b-b222-e26ab9bb0bc2"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "380b032b445a46008e77585e046efe5e",
                    "mappingVersion": 0
                }
            }
        ]
    }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `flowSpec.id` | Die [Flussspezifikations-ID](#specs), die im vorherigen Schritt abgerufen wurde. |
| `sourceConnectionIds` | Die [Quellverbindungs-ID](#source), die in einem früheren Schritt abgerufen wurde. |
| `targetConnectionIds` | Die [Zielverbindungs-ID](#target-connection), die in einem früheren Schritt abgerufen wurde. |
| `transformations.params.mappingId` | Die [Zuordnungs-ID](#mapping), die in einem früheren Schritt abgerufen wurde. |

**Antwort**

Bei einer erfolgreichen Antwort wird die ID (`id`) des neu erstellten Datenflusses angegeben.

```json
{
    "id": "1f086c23-2ea8-4d06-886c-232ea8bd061d",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie einen Datenfluss erstellt, um Streaming-Daten aus Ihrem Streaming-Connector zu erfassen. Eingehende Daten können jetzt von nachgelagerten Platform-Services wie [!DNL Real-Time Customer Profile] und [!DNL Data Science Workspace] verwendet werden. Weiterführende Informationen finden Sie in folgenden Dokumenten:

- [Übersicht über das Echtzeit-Kundenprofil](../../../../profile/home.md)
- [Übersicht über Data Science Workspace](../../../../data-science-workspace/home.md)
