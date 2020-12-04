---
keywords: Experience Platform;home;popular topics;third-party database;third party database
solution: Experience Platform
title: Erfassen von Daten aus einer Drittanbieter-Datenbank über Quellschnittstellen und APIs
topic: overview
type: Tutorial
description: In diesem Lernprogramm werden die Schritte zum Abrufen von Daten aus einer Drittanbieter-Datenbank und zum Integrieren dieser Daten in die Plattform über Quellschnittstellen und APIs beschrieben.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '1626'
ht-degree: 15%

---


# Erfassen von Daten aus einer Drittanbieter-Datenbank über Quellschnittstellen und APIs

[!DNL Flow Service] wird zur Erfassung und Zentralisierung von Kundendaten aus unterschiedlichen Quellen innerhalb von Adobe Experience Platform verwendet. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

In diesem Lernprogramm werden die Schritte zum Abrufen von Daten aus einer Datenbank eines Drittanbieters und zum Einbinden dieser Daten [!DNL Platform] über Quell-Connectors und die [[!DNL Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) -API beschrieben.

## Erste Schritte

Dieses Lernprogramm erfordert eine gültige Verbindung zu einer Datenbank eines Drittanbieters sowie Informationen über die Datei, die Sie einführen möchten [!DNL Platform] (einschließlich Pfad und Struktur der Datei). Wenn Sie diese Informationen nicht haben, lesen Sie das Tutorial zur [Erforschung einer Datenbank mithilfe der Flow Service API](../explore/database-nosql.md) , bevor Sie dieses Tutorial durchführen.

Für dieses Lernprogramm müssen Sie außerdem die folgenden Komponenten von Adobe Experience Platform kennen:

* [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Entwicklerhandbuch](../../../../xdm/api/getting-started.md)zur Schema-Registrierung: Enthält wichtige Informationen, die Sie zur erfolgreichen Durchführung von Aufrufen der Schema Registry API kennen müssen. Diese umfassen Ihre `{TENANT_ID}`, das Konzept sogenannter „Container“ und die für Anfragen erforderlichen Kopfzeilen, von denen insbesondere die Accept-Kopfzeile und deren mögliche Werte wichtig sind.
* [[!DNL Catalog Service]](../../../../catalog/home.md): Catalog ist das Datensatzsystem für die Datenposition und -linie innerhalb [!DNL Experience Platform].
* [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md): Mit der Stapeleinbetungs-API können Sie Daten [!DNL Experience Platform] als Batch-Dateien erfassen.
* [Sandboxen](../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

The following sections provide additional information that you will need to know in order to successfully connect to a third-parry database using the [[!DNL Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) API.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](../../../../tutorials/authentication.md) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to [!DNL Flow Service], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* `x-sandbox-name: {SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* `Content-Type: application/json`

## Erstellen einer Quellverbindung {#source}

You can create a source connection by making a POST request to the [!DNL Flow Service] API. Eine Quellverbindung besteht aus einer Verbindungs-ID, einem Pfad zur Quelldatendatei und einer Verbindungs-Spec-ID.

Um eine Quellverbindung zu erstellen, müssen Sie auch einen Enum-Wert für das Datenformatattribut definieren.

Verwenden Sie die folgenden Enum-Werte für dateibasierte Connectors:

| Data.format | Enum-Wert |
| ----------- | ---------- |
| Getrennte Dateien | `delimited` |
| JSON-Dateien | `json` |
| Parkettdateien | `parquet` |

Für alle tabellenbasierten Connectors verwenden Sie den Enum-Wert: `tabular`.

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
        "name": "Database Source Connector",
        "baseConnectionId": "d5cbb5bc-44cc-41a2-8bb5-bc44ccf1a2fb",
        "description": "A test source connector for a third-party database",
        "data": {
            "format": "tabular",
        },
        "params": {
            "path": "ADMIN.E2E"
        },
        "connectionSpec": {
            "id": "d6b52d86-f0f8-475f-89d4-ce54c8527328",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `baseConnectionId` | Die Verbindungs-ID der Datenquelle Ihres Drittanbieters. |
| `params.path` | Der Pfad der Quelldatei. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID der Datenquelle Ihres Drittanbieters. Eine Liste der Datenbankspezifikations-IDs finden Sie im [Anhang](#appendix) . |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Quellverbindung zurück. Diese ID ist in späteren Schritten erforderlich, um eine Zielgruppe zu erstellen.

```json
{
    "id": "2f7356d9-a866-47ea-b356-d9a86687ea7a",
    "etag": "\"c8006055-0000-0200-0000-5ecd79520000\""
}
```

## Zielgruppe XDM-Schema erstellen {#target-schema}

In früheren Schritten wurde ein Ad-hoc-XDM-Schema zur Strukturierung der Quelldaten erstellt. Damit die Quelldaten in verwendet werden können, [!DNL Platform]muss auch ein Zielgruppe-Schema erstellt werden, um die Quelldaten entsprechend Ihren Anforderungen zu strukturieren. Mit dem Schema Zielgruppe wird dann ein [!DNL Platform] Datensatz erstellt, in dem die Quelldaten enthalten sind. Diese Zielgruppe XDM Schema erweitert auch die [!DNL XDM Individual Profile] Klasse.

Ein Zielgruppe XDM-Schema kann erstellt werden, indem eine POST an die [Schema Registry-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)angefordert wird. If you would prefer to use the user interface in [!DNL Experience Platform], the [Schema Editor tutorial](../../../../xdm/tutorials/create-schema-ui.md) provides step-by-step instructions for performing similar actions in the Schema Editor.

**API-Format**

```http
POST /tenant/schemas
```

**Anfrage**

Die folgende Beispielanforderung erstellt ein XDM-Schema, das die XDM- [!DNL Individual Profile] Klasse erweitert.

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
        "title": "Database Source Connector Target Schema",
        "description": "Target schema for a third-party database",
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

Eine erfolgreiche Antwort gibt Details zum neu erstellten Schema einschließlich seiner eindeutigen Kennung (`$id`) zurück. Diese ID ist in späteren Schritten erforderlich, um einen Zielgruppe-Datensatz, eine Zuordnung und einen Datendurchlauf zu erstellen.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/c44dd18673370dbf16243ba6e6fd9ae62c7916ec10477727",
    "meta:altId": "_{TENANT_ID}.schemas.c44dd18673370dbf16243ba6e6fd9ae62c7916ec10477727",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema for an Oracle connector 5/26/20",
    "type": "object",
    "description": "Target schema for Database",
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
        "repo:createdDate": 1590523478581,
        "repo:lastModifiedDate": 1590523478581,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{LAST_MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "34fdf36fc3029999a07270c4e7719d8a627f7e93e2fbc13888b3c11fb08983c0",
        "meta:globalLibVersion": "1.10.2.1"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Zielgruppen-Dataset erstellen

Ein Zielgruppen-Datensatz kann erstellt werden, indem eine POST an die [Katalogdienst-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)angefordert wird und die ID des Zielgruppe-Schemas innerhalb der Nutzlast angegeben wird.

**API-Format**

```http
POST /dataSets
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
        "name": "Target dataset for a third-party database source connector",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c44dd18673370dbf16243ba6e6fd9ae62c7916ec10477727",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `schemaRef.id` | Die ID des XDM-Schemas der Zielgruppe. |

**Antwort**

A successful response returns an array containing the ID of the newly created dataset in the format `"@/datasets/{DATASET_ID}"`. Die Datensatz-ID ist eine schreibgeschützte, vom System generierte Zeichenfolge, mit der in API-Aufrufen auf den Datensatz verwiesen wird. Speichern Sie die Zielgruppe-Dataset-ID wie in den späteren Schritten zum Erstellen einer Zielgruppe- und eines Datenflusses erforderlich.

```json
[
    "@/dataSets/5ecd766e4bab17191b78e892"
]
```

## Erstellen einer Zielgruppe-Verbindung {#target-connection}

Sie haben jetzt die eindeutigen Bezeichner für eine Datenbankverbindung, ein Schema für die Zielgruppe und einen Datensatz für die Zielgruppe. Mithilfe dieser Bezeichner können Sie mithilfe der [[!DNL Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) API eine Verbindung zur Zielgruppe herstellen, um den Datensatz anzugeben, der die eingehenden Quelldaten enthalten soll.

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
        "name": "Target Connection for a third-party database source connector",
        "description": "Target Connection for a third-party database source connector",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c44dd18673370dbf16243ba6e6fd9ae62c7916ec10477727",
                "version": "application/vnd.adobe.xed-full+json;version=1.0"
            }
        },
        "params": {
            "dataSetId": "5ecd766e4bab17191b78e892"
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
| `params.dataSetId` | Die ID des Zielgruppe-Datensatzes, der im vorherigen Schritt erfasst wurde. |
| `connectionSpec.id` | Die feste Verbindungs-spec-ID für den Datensee. Diese Verbindungs-Spec-ID lautet: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung der neuen Zielgruppe-Verbindung zurück (`id`). Dieser Wert ist in einem späteren Schritt erforderlich, um einen Datenflug zu erstellen.

```json
{
    "id": "e66fdb22-06df-48ac-afdb-2206dff8ac10",
    "etag": "\"7e03773a-0000-0200-0000-5ecd768d0000\""
}
```

## Erstellen einer Zuordnung {#mapping}

Damit die Quelldaten in einen Zielgruppe-Datensatz aufgenommen werden können, müssen sie zunächst dem Zielgruppe-Schema zugeordnet werden, dem der Zielgruppe-Datensatz entspricht. Dies wird erreicht, indem eine POST an die [!DNL Conversion Service] API mit Datenzuordnungen ausgeführt wird, die innerhalb der Anforderungsnutzlast definiert sind.

**API-Format**

```http
POST /mappingSets
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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c44dd18673370dbf16243ba6e6fd9ae62c7916ec10477727",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "person.name.fullName",
                "sourceAttribute": "NAME",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_repo.createDate",
                "sourceAttribute": "DOB",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "ID",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            }
        ]
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `xdmSchema` | Die `$id` der Zielgruppe XDM Schema. |

**Antwort**

Eine erfolgreiche Antwort gibt Details der neu erstellten Zuordnung einschließlich ihrer eindeutigen Kennung (`id`) zurück. Diese ID ist in einem späteren Schritt zum Erstellen eines Datenflusses erforderlich.

```json
{
    "id": "d9d94124417d4df48ea3d00e28eb4327",
    "version": 0,
    "createdDate": 1590523552440,
    "modifiedDate": 1590523552440,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Datennachrichtenspezifikationen abrufen {#specs}

Ein Datennachweis ist für das Sammeln von Daten aus Quellen und deren Umsetzung zuständig [!DNL Platform]. Um einen Datenflug zu erstellen, müssen Sie zunächst die Datenaflow-Spezifikationen abrufen, indem Sie eine GET an die [[!DNL Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) API senden. Dataflow-Spezifikationen sind für die Erfassung von Daten aus einer externen Datenbank oder einem NoSQL-System verantwortlich.

**API-Format**

```http
GET /flowSpecs?property=name=="CRMToAEP"
```

**Anfrage**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name=="CRMToAEP"' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort werden die Details der Datenaflow-Spezifikation zurückgegeben, die für das Übertragen von Daten aus Ihrer Datenbank oder Ihrem NoSQL-System in [!DNL Platform]verantwortlich ist. Diese ID ist im nächsten Schritt erforderlich, um einen neuen Datendurchlauf zu erstellen.

```json
{
    "items": [
        {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "name": "CRMToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "transformationSpecs": [
                {
                    "name": "Copy",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "properties": {
                            "deltaColumn": {
                                "type": "object",
                                "properties": {
                                    "name": {
                                        "type": "string"
                                    },
                                    "dateFormat": {
                                        "type": "string"
                                    },
                                    "timezone": {
                                        "type": "string"
                                    }
                                },
                                "required": [
                                    "name"
                                ]
                            }
                        },
                        "required": [
                            "deltaColumn"
                        ]
                    }
                },
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
            }
        }
    ]
}
```

## Datenfluss erstellen

Der letzte Schritt zur Datenerfassung besteht darin, einen Datenflug zu erstellen. An dieser Stelle sollten die folgenden erforderlichen Werte vorbereitet sein:

* [Quell-Verbindungs-ID](#source)
* [Zielgruppen-Verbindungs-ID](#target)
* [Mapping-ID](#mapping)
* [Dataflow-Spezifikation-ID](#specs)

Ein Datenaflow ist für die Planung und Erfassung von Daten aus einer Quelle zuständig. Sie können einen Datenflug erstellen, indem Sie eine POST anfordern und dabei die zuvor genannten Werte in der Nutzlast angeben.

Um eine Erfassung zu planen, müssen Sie zunächst den Zeitwert des Beginns auf Epochenzeit in Sekunden festlegen. Dann müssen Sie den Frequenzwert auf eine der fünf Optionen einstellen: `once`, `minute`, `hour`, `day`oder `week`. Der Wert &quot;interval&quot;gibt den Zeitraum zwischen zwei aufeinander folgenden Aufrufen an. Für die Erstellung einer einmaligen Erfassung ist kein Intervall erforderlich. Bei allen anderen Frequenzen muss der Intervallwert auf gleich oder größer als `15`eingestellt werden.

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
        "name": "Dataflow for a third-party database and Platform,
        "description": "collecting ADMIN.E2E",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "89cf81c9-47b4-463a-8f81-c947b4863afb"
        ],
        "targetConnectionIds": [
            "e66fdb22-06df-48ac-afdb-2206dff8ac10"
        ],
        "transformations": [
            {
                "name": "Copy",
                "params": {
                    "deltaColumn": {
                        "name": "updatedAt",
                        "dateFormat": "YYYY-MM-DD",
                        "timezone": "UTC"
                    }
                }
            },
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "d9d94124417d4df48ea3d00e28eb4327",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1590523836",
            "frequency":"minute",
            "interval":"15",
            "backfill": "true"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `flowSpec.id` | Die im vorherigen Schritt abgerufene [Flussspec-ID](#specs) . |
| `sourceConnectionIds` | Die [Quell-Verbindungs-ID](#source) , die in einem früheren Schritt abgerufen wurde. |
| `targetConnectionIds` | Die in einem früheren Schritt abgerufene [Zielgruppe-Verbindungs-ID](#target-connection) . |
| `transformations.params.mappingId` | Die in einem früheren Schritt abgerufene [Zuordnungs-ID](#mapping) . |
| `transformations.params.deltaColum` | Die angegebene Spalte, die verwendet wird, um zwischen neuen und vorhandenen Daten zu unterscheiden. Inkrementelle Daten werden basierend auf dem Zeitstempel der ausgewählten Spalte erfasst. Das unterstützte Datumsformat für `deltaColumn` ist `yyyy-MM-dd HH:mm:ss`. Wenn Sie die Datenspeicherung &quot;Blaue Tabelle&quot;verwenden, `deltaColumn` wird das unterstützte Format `yyyy-MM-ddTHH:mm:ssZ`verwendet. |
| `transformations.params.mappingId` | Die mit Ihrer Datenbank verknüpfte Zuordnungs-ID. |
| `scheduleParams.startTime` | Die Beginn-Zeit für den Datenflug in Epochenzeit. |
| `scheduleParams.frequency` | Die Häufigkeit, mit der der Datenfluss Daten erfasst. Zu den zulässigen Werten gehören: `once`, `minute`, `hour`, `day`oder `week`. |
| `scheduleParams.interval` | Das Intervall gibt den Zeitraum zwischen zwei aufeinander folgenden Flussläufen an. Der Wert des Intervalls sollte eine Ganzzahl ungleich null sein. Das Intervall ist nicht erforderlich, wenn die Häufigkeit für andere Frequenzwerte festgelegt ist `once` und größer oder gleich `15` sein sollte. |

**Antwort**

A successful response returns the ID (`id`) of the newly created dataflow.

```json
{
    "id": "e0bd8463-0913-4ca1-bd84-6309134ca1f6",
    "etag": "\"04004fe9-0000-0200-0000-5ebc4c8b0000\""
}
```

## Überwachen des Datenflusses

Nachdem der Datenfluss erstellt wurde, können Sie die Daten überwachen, die durch ihn erfasst werden, um Informationen zu den Flussläufen, zum Abschlussstatus und zu Fehlern anzuzeigen. Weitere Informationen zum Überwachen von Datenflüssen finden Sie im Lernprogramm zum [Überwachen von Datenflüssen in der API. ](../monitor.md)


## Nächste Schritte

In diesem Tutorial haben Sie einen Quell-Connector erstellt, mit dem Daten aus einer Datenbank eines Drittanbieters planmäßig erfasst werden. Eingehende Daten können nun von nachgelagerten [!DNL Platform] Diensten wie [!DNL Real-time Customer Profile] und [!DNL Data Science Workspace]genutzt werden. Weitere Informationen finden Sie in den folgenden Dokumenten:

* [Übersicht über das Echtzeit-Kundenprofil](../../../../profile/home.md)
* [Übersicht über den Data Science Workspace](../../../../data-science-workspace/home.md)

## Anhang

Im folgenden Abschnitt werden die verschiedenen Cloud-Datenspeicherung-Quellschnittstellen und deren Verbindungsspezifikationen Liste.

### Verbindungsspezifikation

| Connector-Name | Verbindungs-Spec-ID |
| -------------- | --------------- |
| [!DNL Amazon Redshift] | `3416976c-a9ca-4bba-901a-1f08f66978ff` |
| [!DNL Apache Hive] on [!DNL Azure HDInsights] | `aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f` |
| [!DNL Apache Spark] on [!DNL Azure HDInsights] | `6a8d82bc-1caf-45d1-908d-cadabc9d63a6` |
| [!DNL Azure Data Explorer] | `0479cc14-7651-4354-b233-7480606c2ac3` |
| [!DNL Azure Synapse Analytics] | `a49bcc7d-8038-43af-b1e4-5a7a089a7d79` |
| [!DNL Azure Table Storage] | `ecde33f2-c56f-46cc-bdea-ad151c16cd69` |
| [!DNL CouchBase] | `1fe283f6-9bec-11ea-bb37-0242ac130002` |
| [!DNL Google BigQuery] | `3c9b37f8-13a6-43d8-bad3-b863b941fedd` |
| [!DNL IBM DB2] | `09182899-b429-40c9-a15a-bf3ddbc8ced7` |
| [!DNL MariaDB] | `000eb99-cd47-43f3-827c-43caf170f015` |
| [!DNL Microsoft SQL Server] | `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec` |
| [!DNL MySQL] | `26d738e0-8963-47ea-aadf-c60de735468a` |
| [!DNL Oracle] | `d6b52d86-f0f8-475f-89d4-ce54c8527328` |
| [!DNL Phoenix] | `102706fb-a5cd-42ee-afe0-bc42f017ff43` |
| [!DNL PostgreSQL] | `74a1c565-4e59-48d7-9d67-7c03b8a13137` |