---
keywords: Experience Platform;Startseite;beliebte Themen;Cloud-Speicherdaten;Streaming-Daten;Streaming
solution: Experience Platform
title: Erstellen eines Streaming-Datenflusses für Rohdaten mithilfe der Flow Service-API
type: Tutorial
description: In diesem Tutorial werden die Schritte zum Abrufen von Streaming-Daten und zum Einbringen dieser Daten in Experience Platform mithilfe von Quell-Connectoren und APIs beschrieben.
exl-id: 898df7fe-37a9-4495-ac05-30029258a6f4
source-git-commit: bad1e0a9d86dcce68f1a591060989560435070c5
workflow-type: tm+mt
source-wordcount: '1208'
ht-degree: 35%

---

# Erstellen eines Streaming-Datenflusses für Rohdaten mit der [!DNL Flow Service]-API

In diesem Tutorial werden die Schritte zum Abrufen von Rohdaten aus einem Streaming-Quell-Connector und zum Übertragen dieser Daten in Experience Platform mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten ordnet.
   - [Grundlagen der Schemakomposition](../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemakomposition.
   - [Entwicklerhandbuch zur Schema Registry](../../../../xdm/api/getting-started.md): Enthält wichtige Informationen, die Sie benötigen, um die Schema Registry API erfolgreich aufrufen zu können. Diese umfassen Ihre `{TENANT_ID}`, das Konzept sogenannter „Container“ und die für Anfragen erforderlichen Kopfzeilen, von denen insbesondere die Accept-Kopfzeile und deren mögliche Werte wichtig sind.
- [[!DNL Catalog Service]](../../../../catalog/home.md): Der Katalog ist das „System of Record“ für den Speicherort und die Herkunft von Daten in Experience Platform.
- [[!DNL Streaming ingestion]](../../../../ingestion/streaming-ingestion/overview.md): Die Streaming-Aufnahme für Experience Platform bietet Benutzenden eine Methode, um Daten von Client- und Server-seitigen Geräten in Echtzeit an Experience Platform zu senden.
- [Sandboxes](../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

### Verwenden von Experience Platform-APIs

Informationen zum erfolgreichen Aufrufen von Experience Platform-APIs finden Sie im Handbuch unter [&#x200B; mit Experience Platform-APIs](../../../../landing/api-guide.md).

### Erstellen einer Quellverbindung {#source}

Für dieses Tutorial benötigen Sie außerdem eine gültige Quellverbindungs-ID für einen Streaming-Connector. Wenn Sie nicht über diese Informationen verfügen, finden Sie in den folgenden Tutorials zum Erstellen einer Streaming-Quellverbindung weitere Informationen, bevor Sie dieses Tutorial ausführen:

- [[!DNL Amazon Kinesis]](../create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../create/cloud-storage/eventhub.md)
- [[!DNL Google PubSub]](../create/cloud-storage/google-pubsub.md)

## Erstellen eines XDM-Zielschemas {#target-schema}

Damit die Quelldaten in Experience Platform verwendet werden können, muss ein Zielschema erstellt werden, das die Quelldaten entsprechend Ihren Anforderungen strukturiert. Das Zielschema wird dann verwendet, um einen Experience Platform-Datensatz zu erstellen, in dem die Quelldaten enthalten sind. Dieses XDM-Zielschema erweitert auch die XDM-[!DNL Individual Profile].

Um ein XDM-Zielschema zu erstellen, stellen Sie eine POST-Anfrage an den `/schemas`-Endpunkt der [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

**API-Format**

```http
POST /tenant/schemas
```

**Anfrage**

Die folgende Beispielanfrage erstellt ein XDM-Schema, das die XDM-[!DNL Individual Profile] erweitert.

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

Eine erfolgreiche Antwort gibt Details zum neu erstellten Schema zurück, einschließlich der eindeutigen Kennung (`$id`). Diese ID ist in späteren Schritten erforderlich, um einen Zieldatensatz, eine Zuordnung und einen Datenfluss zu erstellen.

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

Nachdem ein Ziel-XDM-Schema erstellt und seine eindeutige `$id` festgelegt wurde, können Sie jetzt einen Zieldatensatz erstellen, der Ihre Quelldaten enthält. Um einen Zieldatensatz zu erstellen, stellen Sie eine POST-Anfrage an den `dataSets`-Endpunkt der [Catalog Service API](https://www.adobe.io/experience-platform-apis/references/catalog/) und geben Sie dabei die ID des Zielschemas in der Payload an.

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
| `schemaRef.id` | Die URI-`$id` für das XDM-Schema, auf dem der Datensatz basieren soll. |
| `schemaRef.contentType` | Die Version des Schemas. Dieser Wert muss auf `application/vnd.adobe.xed-full-notext+json;version=1` gesetzt werden, wodurch die neueste Nebenversion des Schemas zurückgegeben wird. Weitere Informationen finden Sie im Abschnitt zur [Schemaversionierung](../../../../xdm/api/getting-started.md#versioning) im XDM-API-Handbuch. |

**Antwort**

Eine erfolgreiche Antwort gibt ein -Array zurück, das die ID des neu erstellten Datensatzes im `"@/datasets/{DATASET_ID}"` Format enthält. Die Datensatz-ID ist eine schreibgeschützte, systemgenerierte Zeichenfolge, die verwendet wird, um in API-Aufrufen auf den Datensatz zu verweisen. Die Zieldatensatz-ID ist in späteren Schritten erforderlich, um eine Zielverbindung und einen Datenfluss zu erstellen.

```json
[
    "@/dataSets/5f7187bac6d00f194fb937c0"
]
```

## Erstellen einer Zielverbindung {#target-connection}

Zielverbindungen erstellen und verwalten eine Zielverbindung zu Experience Platform oder einem beliebigen Ort, an dem die übertragenen Daten landen. Zielverbindungen enthalten Informationen zum Datenziel, Datenformat und zur Zielverbindungs-ID, die zum Erstellen eines Datenflusses erforderlich sind. Target-Verbindungsinstanzen sind für einen Mandanten und eine Organisation spezifisch.

Um eine Zielverbindung zu erstellen, stellen Sie eine POST-Anfrage an den `/targetConnections`-Endpunkt der [!DNL Flow Service]-API. Im Rahmen der Anfrage müssen Sie das Datenformat, die im vorherigen Schritt abgerufene `dataSetId` und die feste Verbindungsspezifikations-ID angeben, die mit [!DNL Data Lake] verknüpft ist. Diese ID ist `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

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
| `data.format` | Das angegebene Format der Daten, die Sie an den Data Lake senden. |
| `params.dataSetId` | Die ID des Zieldatensatzes, die im vorherigen Schritt generiert wurde. **Hinweis**: Beim Erstellen einer Zielverbindung müssen Sie eine gültige Datensatz-ID angeben. Eine ungültige Datensatz-ID führt zu einem Fehler. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID, die für die Verbindung mit dem Data Lake verwendet wird. Diese ID lautet: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

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

Um einen Zuordnungssatz zu erstellen, senden Sie eine POST-Anfrage an den `mappingSets`-Endpunkt der [[!DNL Data Prep] API](https://developer.adobe.com/experience-platform-apis/references/data-prep/), wobei Sie das Ziel-XDM-Schema `$id` und die Details der Zuordnungssätze, die Sie erstellen möchten, angeben.

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

## Abrufen einer Liste von Datenflussspezifikationen {#specs}

Ein Datenfluss ist für die Erfassung von Daten aus Quellen und deren Aufnahme in Experience Platform verantwortlich. Um einen Datenfluss zu erstellen, müssen Sie zunächst die Datenflussspezifikationen abrufen, indem Sie eine GET-Anfrage an die [!DNL Flow Service]-API senden.

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

Eine erfolgreiche Antwort gibt eine Liste von Datenflussspezifikationen zurück. Die Datenflussspezifikations-ID, die Sie abrufen müssen, um einen Datenfluss mit einem der [!DNL Amazon Kinesis], [!DNL Azure Event Hubs] oder [!DNL Google PubSub] zu erstellen, ist `d69717ba-71b4-4313-b654-49f9cf126d7a`.

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

>[!NOTE]
>
>Nachdem Sie einen Streaming-Datenfluss erstellt oder aktualisiert haben, ist eine kurze 5-minütige Pause bei der Datenaufnahme erforderlich, um potenzielle Instanzen von Datenverlust oder Datenverlust zu verhindern.

Der letzte Schritt bei der Erfassung von Streaming-Daten besteht darin, einen Datenfluss zu erstellen. Bislang haben Sie die folgenden erforderlichen Werte vorbereitet:

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

## Daten zur Aufnahme posten

In der folgenden Beispiel-Payload finden Sie Beispiele für rohe oder XDM-konforme JSON, die Sie zur Aufnahme senden können.

>[!NOTE]
>
>Sie müssen zwischen der Erstellung eines Datenflusses und der Aufnahme von Streaming-Daten eine Verzögerung von mindestens ca. 5 Minuten hinzufügen. Dadurch kann der Datenfluss vollständig aktiviert werden, bevor Daten aufgenommen werden.

Die folgenden Beispiele gelten für alle:

- [[!DNL Amazon Kinesis]](../create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../create/cloud-storage/eventhub.md)
- [[!DNL Google PubSub]](../create/cloud-storage/google-pubsub.md)

>[!BEGINTABS]

>[!TAB Rohdaten]

```json
'{
      "name": "Johnson Smith",
      "location": {
          "city": "Seattle",
          "country": "United State of America",
          "address": "3692 Main Street"
      },
      "gender": "Male",
      "birthday": {
          "year": 1984,
          "month": 6,
          "day": 9
      }
  }'
```

>[!TAB XDM-Daten]

```json
{
  "header": {
    "schemaRef": {
      "id": "https://ns.adobe.com/aepstreamingservicesint/schemas/73cae7e6db06ebca535cd973e3ece85e66253962f504e7d8",
      "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
    }
  },
  "body": {
    "xdmMeta": {
      "schemaRef": {
        "id": "https://ns.adobe.com/aepstreamingservicesint/schemas/73cae7e6db06ebca535cd973e3ece85e66253962f504e7d8",
        "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
      }
    },
    "xdmEntity": {
      "_id": "acme",
      "workEmail": {
        "address": "mike@acme.com",
        "primary": true,
        "type": "work",
        "status": "active"
      },
      "person": {
        "gender": "male",
        "name": {
          "firstName": "Mike",
          "lastName": "Wazowski"
        },
        "birthDate": "1985-01-01"
      },
      "identityMap": {
        "ecid": [
          {
            "id": "01262118050522051420082102000000000000"
          }
        ]
      }
    }
  }
}
```

>[!ENDTABS]

## Nächste Schritte

In diesem Tutorial haben Sie einen Datenfluss erstellt, um Streaming-Daten von Ihrem Streaming-Connector zu erfassen. Eingehende Daten können jetzt von nachgelagerten Experience Platform-Services wie [!DNL Real-Time Customer Profile] und [!DNL Data Science Workspace] verwendet werden. Weiterführende Informationen finden Sie in folgenden Dokumenten:

- [Übersicht zum Echtzeit-Kundenprofil](../../../../profile/home.md)
- [Übersicht über Data Science Workspace](../../../../data-science-workspace/home.md)
