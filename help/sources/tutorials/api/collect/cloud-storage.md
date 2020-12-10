---
keywords: Experience Platform;home;popular topics;cloud storage data
solution: Experience Platform
title: Erfassen von Cloud-Datenspeicherung-Daten über Quellschnittstellen und APIs
topic: overview
type: Tutorial
description: In diesem Lernprogramm werden die Schritte zum Abrufen von Daten aus einer Cloud-Datenspeicherung eines Drittanbieters und deren anschließender Integration in die Plattform über Quellschnittstellen und APIs beschrieben.
translation-type: tm+mt
source-git-commit: 7f24413a99b57e28ca2106214b7eedb5b068b045
workflow-type: tm+mt
source-wordcount: '1599'
ht-degree: 16%

---


# Erfassen von Cloud-Datenspeicherung-Daten über Quellschnittstellen und APIs

In diesem Lernprogramm werden die Schritte zum Abrufen von Daten aus einer Cloud-Datenspeicherung eines Drittanbieters und deren anschließender Integration in die Plattform über Quellschnittstellen und die [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)beschrieben.

## Erste Schritte

Für dieses Lernprogramm ist es erforderlich, dass Sie über eine gültige Verbindung Zugriff auf eine Cloud-Datenspeicherung eines Drittanbieters haben und Informationen über die Datei erhalten, die Sie einsetzen möchten, [!DNL Platform]einschließlich des Dateipfads und der Dateistruktur. Wenn Sie diese Informationen nicht haben, lesen Sie das Tutorial zur [Erforschung einer Cloud-Datenspeicherung von Drittanbietern mithilfe [!DNL Flow Service] der API](../explore/cloud-storage.md) , bevor Sie dieses Tutorial durchführen.

Für dieses Lernprogramm müssen Sie außerdem die folgenden Komponenten von Adobe Experience Platform kennen:

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   - [Grundlagen der Schemakomposition](../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   - [Entwicklerhandbuch](../../../../xdm/api/getting-started.md)zur Schema-Registrierung: Enthält wichtige Informationen, die Sie zur erfolgreichen Durchführung von Aufrufen der Schema Registry API kennen müssen. Diese umfassen Ihre `{TENANT_ID}`, das Konzept sogenannter „Container“ und die für Anfragen erforderlichen Kopfzeilen, von denen insbesondere die Accept-Kopfzeile und deren mögliche Werte wichtig sind.
- [[!DNL Catalog Service]](../../../../catalog/home.md): Catalog ist das Datensatzsystem für die Datenposition und -linie innerhalb [!DNL Experience Platform].
- [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md): Mit der Stapeleinbetungs-API können Sie Daten [!DNL Experience Platform] als Batch-Dateien erfassen.
- [Sandboxen](../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.
The following sections provide additional information that you will need to know in order to successfully connect to a cloud storage using the [!DNL Flow Service] API.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](../../../../tutorials/authentication.md) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to [!DNL Flow Service], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

- `x-sandbox-name: {SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

- `Content-Type: application/json`

## Erstellen einer Quellverbindung {#source}

You can create a source connection by making a POST request to the [!DNL Flow Service] API. Eine Quellverbindung besteht aus einer Verbindungs-ID, einem Pfad zur Quelldatendatei und einer Verbindungs-Spec-ID.

Um eine Quellverbindung zu erstellen, müssen Sie auch einen Enum-Wert für das Datenformatattribut definieren.

Verwenden Sie die folgenden Enum-Werte für dateibasierte Connectors:

| Datenformat | Enum-Wert |
| ----------- | ---------- |
| Getrennt | `delimited` |
| JSON | `json` |
| Parkett | `parquet` |

Legen Sie für alle tabellenbasierten Connectors den Wert auf `tabular`.

>[!NOTE]
>
>Sie können CSV- und TSV-Datenspeicherung mit einem Cloud-Quellanschluss erfassen, indem Sie ein Spaltentrennzeichen als Eigenschaft angeben. Jeder einzelne Zeichenwert ist ein zulässiges Spaltentrennzeichen. Wenn das Attribut nicht angegeben ist, `(,)` wird als Standardwert ein Komma verwendet.

**API-Format**

```http
POST /sourceConnections
```

**Anfrage**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Cloud storage source connector",
        "connectionId": "9e2541a0-b143-4d23-a541-a0b143dd2301",
        "description": "Cloud storage source connector",
        "data": {
            "format": "delimited",
            "columnDelimiter": "\t"
        },
        "params": {
            "path": "/ingestion-demos/leads/tsv_data/*.tsv",
            "recursive": "true"
        },
            "connectionSpec": {
            "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `connectionId` | Die eindeutige Verbindungs-ID des Cloud-Datenspeicherung-Systems eines Drittanbieters, auf das Sie zugreifen. |
| `data.format` | Ein Enum-Wert, der das Datenformatattribut definiert. |
| `data.columnDelimiter` | Sie können ein beliebiges Trennzeichen für einzelne Zeichenspalten verwenden, um einfache Dateien zu erfassen. Diese Eigenschaft ist nur beim Eingeben von CSV- oder TSV-Dateien erforderlich. |
| `params.path` | Der Pfad der Quelldatei, auf die Sie zugreifen. |
| `connectionSpec.id` | Die mit Ihrem Cloud-Datenspeicherung-System eines Drittanbieters verknüpfte Verbindungsspezifikations-ID. Eine Liste der Verbindungsspezifikations-IDs finden Sie im [Anhang](#appendix) . |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Quellverbindung zurück. Diese ID ist in einem späteren Schritt zum Erstellen eines Datenflusses erforderlich.

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

## Zielgruppe XDM-Schema erstellen {#target-schema}

Damit die Quelldaten in verwendet werden können, [!DNL Platform]muss ein Zielgruppe-Schema erstellt werden, um die Quelldaten entsprechend Ihren Anforderungen zu strukturieren. Mit dem Schema Zielgruppe wird dann ein [!DNL Platform] Datensatz erstellt, in dem die Quelldaten enthalten sind.

Ein Zielgruppe XDM-Schema kann erstellt werden, indem eine POST an die [Schema Registry-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)angefordert wird.

**API-Format**

```http
POST /schemaregistry/tenant/schemas
```

**Anfrage**

Die folgende Beispielanforderung erstellt ein XDM-Schema, das die XDM Individual Profil-Klasse erweitert.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "type": "object",
        "title": "Target schema for a Cloud Storage connector",
        "description": "Target schema for a Cloud Storage connector",
        "allOf": [
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
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

Eine erfolgreiche Antwort gibt Details zum neu erstellten Schema einschließlich seiner eindeutigen Kennung (`$id`) zurück. Diese ID ist in späteren Schritten erforderlich, um einen Zielgruppe-Datensatz, eine Zuordnung und einen Datendurchlauf zu erstellen.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
    "meta:altId": "_{TENANT_ID}.schemas.995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema cloud storage",
    "type": "object",
    "description": "Target schema for cloud storage",
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
    "imsOrg": "{IMS_ORG}",
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
        "repo:createdDate": 1597783248870,
        "repo:lastModifiedDate": 1597783248870,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{LAST_MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "596661ec6c7a9c6ae530676e98290a4a58ca29540ed92489cf4478b2bf013a65",
        "meta:globalLibVersion": "1.13.3"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "{TENANT_ID}"
}
```

## Zielgruppen-Dataset erstellen

Ein Zielgruppen-Datensatz kann erstellt werden, indem eine POST an die [Katalogdienst-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)angefordert wird und die ID des Zielgruppe-Schemas innerhalb der Nutzlast angegeben wird.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Target dataset for cloud storage",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `schemaRef.id` | Die ID des XDM-Schemas der Zielgruppe. |

**Antwort**

A successful response returns an array containing the ID of the newly created dataset in the format `"@/datasets/{DATASET_ID}"`. Die Datensatz-ID ist eine schreibgeschützte, vom System generierte Zeichenfolge, mit der in API-Aufrufen auf den Datensatz verwiesen wird. Die Zielgruppe DataSet-ID ist in späteren Schritten erforderlich, um eine Zielgruppe- und einen Datendurchlauf zu erstellen.

```json
[
    "@/dataSets/5f3c3cedb2805c194ff0b69a"
]
```

## Erstellen einer Zielgruppe-Verbindung {#target-connection}

Eine Zielgruppe-Verbindung stellt die Verbindung mit dem Ziel dar, in dem die erfassten Daten landen. Um eine Verbindung zur Zielgruppe herzustellen, müssen Sie die mit dem Data Lake verknüpfte eindeutige Verbindungsspezifikations-ID angeben. Diese Verbindungs-Spec-ID lautet: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Sie haben jetzt die eindeutigen Bezeichner ein Zielgruppe-Schema, einen Zielgruppe-Datensatz und die Verbindungsspezifikations-ID zum Data Lake. Mithilfe dieser Bezeichner können Sie mithilfe der [!DNL Flow Service] API eine Verbindung zur Zielgruppe herstellen, um den Datensatz anzugeben, der die eingehenden Quelldaten enthalten soll.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Target Connection for a Cloud Storage connector",
        "description": "Target Connection for a Cloud Storage connector",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
                "version": "application/vnd.adobe.xed-full+json;version=1.0"
            }
        },
        "params": {
            "dataSetId": "5f3c3cedb2805c194ff0b69a"
        },
            "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `data.schema.id` | Die `$id` der Zielgruppe XDM Schema. |
| `params.dataSetId` | Die ID des Zielgruppe-Datensatzes. |
| `connectionSpec.id` | Die feste Verbindungs-spec-ID zum Data Lake. Diese ID lautet: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung der neuen Zielgruppe-Verbindung zurück (`id`). Diese ID ist in späteren Schritten erforderlich.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Erstellen einer Zuordnung {#mapping}

Damit die Quelldaten in einen Zielgruppe-Datensatz aufgenommen werden können, müssen sie zunächst dem Zielgruppe-Schema zugeordnet werden, dem der Zielgruppe-Datensatz entspricht. Dies wird erreicht, indem eine POST an den Konvertierungsdienst mit Datenzuordnungen ausgeführt wird, die innerhalb der Anforderungs-Nutzlast definiert sind.

**API-Format**

```http
POST /conversion/mappingSets
```

**Anfrage**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "Id",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "FirstName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "LastName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            }
        ]
    }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `xdmSchema` | Die ID des XDM-Schemas der Zielgruppe. |

**Antwort**

Eine erfolgreiche Antwort gibt Details der neu erstellten Zuordnung einschließlich ihrer eindeutigen Kennung (`id`) zurück. Dieser Wert ist in einem späteren Schritt erforderlich, um einen Datenflug zu erstellen.

```json
{
    "id": "bf5286a9c1ad4266baca76ba3adc9366",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Datennachrichtenspezifikationen abrufen {#specs}

Ein Datennachweis ist für das Sammeln und Einfügen von Daten aus Quellen zuständig [!DNL Platform]. Um einen Datenflug zu erstellen, müssen Sie zunächst die Datenaflow-Spezifikationen abrufen, die für die Erfassung von Cloud-Datenspeicherung-Daten zuständig sind.

**API-Format**

```http
GET /flowSpecs?property=name=="CloudStorageToAEP"
```

**Anfrage**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name==%22CloudStorageToAEP%22' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort werden die Details der Datenfeldspezifikation zurückgegeben, die für das Übertragen von Daten aus Ihrer Cloud-Datenspeicherung in [!DNL Platform]zuständig ist. Die Antwort enthält eine eindeutige Flussspec-ID. Diese ID ist im nächsten Schritt erforderlich, um einen neuen Datendurchlauf zu erstellen.

```json
{
    "items": [
        {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "name": "CloudStorageToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "sourceConnectionSpecIds": [
                "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
                "ecadc60c-7455-4d87-84dc-2a0e293d997b",
                "b7829c2f-2eb0-4f49-a6ee-55e33008b629",
                "4c10e202-c428-4796-9208-5f1f5732b1cf",
                "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
                "32e8f412-cdf7-464c-9885-78184cb113fd",
                "b7bf2577-4520-42c9-bae9-cad01560f7bc",
                "998b8ae3-cec0-43b7-8abe-40b1eb4ee069",
                "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8"
            ],
            "targetConnectionSpecIds": [
                "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
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
                            },
                            "mappingVersion": {
                                "type": "string"
                            }
                        }
                    }
                }
            ],
            "scheduleSpec": {
                "name": "PeriodicSchedule",
                "type": "Periodic",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "startTime": {
                            "description": "epoch time",
                            "type": "integer"
                        },
                        "endTime": {
                            "description": "epoch time",
                            "type": "integer"
                        },
                        "interval": {
                            "type": "integer"
                        },
                        "frequency": {
                            "type": "string",
                            "enum": [
                                "minute",
                                "hour",
                                "day",
                                "week"
                            ]
                        },
                        "backfill": {
                            "type": "boolean",
                            "default": true
                        }
                    },
                    "required": [
                        "startTime",
                        "frequency",
                        "interval"
                    ],
                    "if": {
                        "properties": {
                            "frequency": {
                                "const": "minute"
                            }
                        }
                    },
                    "then": {
                        "properties": {
                            "interval": {
                                "minimum": 15
                            }
                        }
                    },
                    "else": {
                        "properties": {
                            "interval": {
                                "minimum": 1
                            }
                        }
                    }
                }
            },
            "permissionsInfo": {
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "read"
                        ]
                    }
                ],
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "write"
                        ]
                    }
                ]
            }
        }
    ]
}
```

## Datenfluss erstellen

Der letzte Schritt zur Erfassung von Cloud-Datenspeicherung-Daten besteht darin, einen Datenflug zu erstellen. Jetzt haben Sie die folgenden erforderlichen Werte vorbereitet:

- [Quell-Verbindungs-ID](#source)
- [Zielgruppen-Verbindungs-ID](#target)
- [Mapping-ID](#mapping)
- [Dataflow-Spezifikation-ID](#specs)

Ein Datenaflow ist für die Planung und Erfassung von Daten aus einer Quelle zuständig. Sie können einen Datenflug erstellen, indem Sie eine POST anfordern und dabei die zuvor genannten Werte in der Nutzlast angeben.

Um eine Erfassung zu planen, müssen Sie zunächst den Zeitwert des Beginns auf Epochenzeit in Sekunden festlegen. Dann müssen Sie den Frequenzwert auf eine der fünf Optionen einstellen: `once`, `minute`, `hour`, `day`oder `week`. Der Wert &quot;interval&quot;gibt den Zeitraum zwischen zwei aufeinander folgenden Aufrufen an. Für die Erstellung einer einmaligen Erfassung ist kein Intervall erforderlich. Bei allen anderen Frequenzen muss der Intervallwert auf gleich oder größer als `15`eingestellt werden.

>[!IMPORTANT]
>
>Es wird dringend empfohlen, den Datenfluss bei Verwendung des [FTP-Connectors](../../../connectors/cloud-storage/ftp.md)für eine einmalige Erfassung zu planen.

**API-Format**

```http
POST /flows
```

**Anfrage**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Cloud Storage flow to Platform",
        "description": "Cloud Storage flow to Platform",
        "flowSpec": {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "26b53912-1005-49f0-b539-12100559f0e2"
        ],
        "targetConnectionIds": [
            "f7eb08fa-5f04-4e45-ab08-fa5f046e45ee"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1597784298",
            "frequency":"minute",
            "interval":"30"
        }
    }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `flowSpec.id` | Die im vorherigen Schritt abgerufene [Flussspec-ID](#specs) . |
| `sourceConnectionIds` | Die [Quell-Verbindungs-ID](#source) , die in einem früheren Schritt abgerufen wurde. |
| `targetConnectionIds` | Die in einem früheren Schritt abgerufene [Zielgruppe-Verbindungs-ID](#target-connection) . |
| `transformations.params.mappingId` | Die in einem früheren Schritt abgerufene [Zuordnungs-ID](#mapping) . |
| `scheduleParams.startTime` | Die Beginn-Zeit für den Datenflug in Epochenzeit. |
| `scheduleParams.frequency` | Die Häufigkeit, mit der der Datenfluss Daten erfasst. Zu den zulässigen Werten gehören: `once`, `minute`, `hour`, `day`oder `week`. |
| `scheduleParams.interval` | Das Intervall gibt den Zeitraum zwischen zwei aufeinander folgenden Flussläufen an. Der Wert des Intervalls sollte eine Ganzzahl ungleich null sein. Das Intervall ist nicht erforderlich, wenn die Häufigkeit für andere Frequenzwerte festgelegt ist `once` und größer oder gleich `15` sein sollte. |

**Antwort**

A successful response returns the ID (`id`) of the newly created dataflow.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Überwachen des Datenflusses

Nachdem der Datenfluss erstellt wurde, können Sie die Daten überwachen, die durch ihn erfasst werden, um Informationen zu den Flussläufen, zum Abschlussstatus und zu Fehlern anzuzeigen. Weitere Informationen zum Überwachen von Datenflüssen finden Sie im Lernprogramm zum [Überwachen von Datenflüssen in der API.](../monitor.md)

## Nächste Schritte

In diesem Lernprogramm haben Sie einen Quell-Connector erstellt, um Daten aus Ihrer Cloud-Datenspeicherung planmäßig zu erfassen. Eingehende Daten können nun von nachgelagerten [!DNL Platform] Diensten wie [!DNL Real-time Customer Profile] und [!DNL Data Science Workspace]genutzt werden. Weitere Informationen finden Sie in den folgenden Dokumenten:

- [Übersicht über das Echtzeit-Kundenprofil](../../../../profile/home.md)
- [Übersicht über den Data Science Workspace](../../../../data-science-workspace/home.md)

## Anhang {#appendix}

Im folgenden Abschnitt werden die verschiedenen Cloud-Datenspeicherung-Quellschnittstellen und deren Verbindungsspezifikationen Liste.

### Verbindungsspezifikation

| Connector-Name | Verbindungsspezifikation |
| -------------- | --------------- |
| [!DNL Amazon S3] (S3) | `ecadc60c-7455-4d87-84dc-2a0e293d997b` |
| [!DNL Amazon Kinesis] (Kinesis) | `86043421-563b-46ec-8e6c-e23184711bf6` |
| [!DNL Azure Blob] (Blob) | `4c10e202-c428-4796-9208-5f1f5732b1cf` |
| [!DNL Azure Data Lake Storage Gen2] (ADLS Gen2) | `0ed90a81-07f4-4586-8190-b40eccef1c5a` |
| [!DNL Azure Event Hubs] (Ereignis-Hubs) | `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |
| [!DNL Azure File Storage] | `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |
| [!DNL Google Cloud Storage] | `32e8f412-cdf7-464c-9885-78184cb113fd` |
| HDFS | `54e221aa-d342-4707-bcff-7a4bceef0001` |
| SFTP | `bf367b0d-3d9b-4060-b67b-0d3d9bd06094` |