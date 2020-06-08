---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erfassen von Daten aus einer Drittanbieter-Datenbank über Quellschnittstellen und APIs
topic: overview
translation-type: tm+mt
source-git-commit: 4a831a0e72ac614bb4646ea3aa5f511984e5aa07
workflow-type: tm+mt
source-wordcount: '1607'
ht-degree: 2%

---


# Erfassen von Daten aus einer Drittanbieter-Datenbank über Quellschnittstellen und APIs

Mit dem Flow-Dienst werden Kundendaten aus verschiedenen Quellen innerhalb der Adobe Experience Platform erfasst und zentralisiert. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

In diesem Lernprogramm werden die Schritte zum Abrufen von Daten aus einer Drittanbieter-Datenbank und zum Integrieren dieser Daten in die Plattform über Quellschnittstellen und APIs beschrieben.

## Erste Schritte

Für dieses Lernprogramm ist eine gültige Verbindung zu einer Datenbank eines Drittanbieters sowie Informationen über die Datei erforderlich, die Sie in Platform einbringen möchten (einschließlich Pfad und Struktur der Datei). Wenn Sie diese Informationen nicht haben, lesen Sie das Tutorial zur [Erforschung einer Datenbank mithilfe der Flow Service API](../explore/database-nosql.md) , bevor Sie dieses Tutorial durchführen.

Für dieses Lernprogramm müssen Sie außerdem die folgenden Komponenten der Adobe Experience Platform verstehen:

* [Erlebnis-Datenmodell (XDM)-System](../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Zusammensetzung](../../../../xdm/schema/composition.md)des Schemas: Erfahren Sie mehr über die grundlegenden Bausteine von XDM-Schemas, einschließlich der wichtigsten Grundsätze und Best Practices bei der Schema-Komposition.
   * [Entwicklerhandbuch](../../../../xdm/api/getting-started.md)zur Schema-Registrierung: Enthält wichtige Informationen, die Sie zur erfolgreichen Durchführung von Aufrufen der Schema Registry API kennen müssen. Dazu gehören Ihre `{TENANT_ID}`, das Konzept der &quot;Container&quot; und die erforderlichen Kopfzeilen für Anfragen (mit besonderer Aufmerksamkeit für den Accept-Header und seine möglichen Werte).
* [Katalogdienst](../../../../catalog/home.md): Catalog ist das Datensatzsystem für die Datenposition und -linie in der Experience Platform.
* [Stapelverarbeitung](../../../../ingestion/batch-ingestion/overview.md): Mit der Batch Ingestion API können Sie Daten als Batch-Dateien in Experience Platform erfassen.
* [Sandboxen](../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Plattforminstanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der Flow Service API eine Verbindung zu einer Datenbank oder einem NoSQL-System herstellen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Lernprogramm finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

### Werte für erforderliche Kopfzeilen sammeln

Um Aufrufe an Plattform-APIs durchzuführen, müssen Sie zunächst das [Authentifizierungstraining](../../../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungstreutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform API-Aufrufen bereit, wie unten dargestellt:

* Genehmigung: Träger `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in Experience Platform, einschließlich derer, die zu Flow Service gehören, werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an Plattform-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

* x-sandbox-name: `{SANDBOX_NAME}`

Für alle Anforderungen, die eine Payload enthalten (POST, PUT, PATCH), ist ein zusätzlicher Medientyp-Header erforderlich:

* Content-Type: `application/json`

## Erstellen einer Ad-hoc-XDM-Klasse und eines Ad-hoc-Schemas

Um externe Daten über Quell-Connectors in die Plattform zu bringen, müssen eine Ad-hoc-XDM-Klasse und ein Schema für die Rohquellendaten erstellt werden.

Um eine Ad-hoc-Klasse und ein Ad-hoc-Schema zu erstellen, führen Sie die im [Ad-hoc-Schema-Lernprogramm](../../../../xdm/tutorials/ad-hoc.md)beschriebenen Schritte aus. Beim Erstellen einer Ad-hoc-Klasse müssen alle in den Quelldaten gefundenen Felder im Anforderungstext beschrieben werden.

Führen Sie die im Entwicklerhandbuch beschriebenen Schritte aus, bis Sie ein Ad-hoc-Schema erstellt haben. Rufen Sie die eindeutige Kennung (`$id`) des Ad-hoc-Schemas ab und speichern Sie sie und fahren Sie dann mit dem nächsten Schritt dieses Lernprogramms fort.

## Erstellen einer Quellverbindung {#source}

Wenn ein Ad-hoc-XDM-Schema erstellt wurde, kann jetzt eine Quellverbindung mit einer POST-Anforderung an die Flow Service API erstellt werden. Eine Quellverbindung besteht aus einer Basisverbindung, einer Quelldatendatei und einem Verweis auf das Schema, das die Quelldaten beschreibt.

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
        "name": "Source Connection for database or NoSQL",
        "baseConnectionId": "54c22133-3a01-4d3b-8221-333a01bd3b03",
        "description": "Source Connection for database or NoSQL to ingest test1.Mytable",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c8c2b32d6f6a53d5ffc7212c37b3a9369282404a7bd551e8",
                "version": "application/vnd.adobe.xed-full-notext+json; version=1"
            }
        },
        "params": {
            "path": "test1.Mytable"
        },
        "connectionSpec": {
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "version": "1.0"
        }
}'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `baseConnectionId` | Die ID einer Datenbankverbindung. |
| `data.schema.id` | Die `$id` des Ad-hoc-XDM-Schemas. |
| `params.path` | Der Pfad der Quelldatei. |
| `connectionSpec.id` | Die Verbindungs-Spezifikations-ID für eine Datenbank oder ein NoSQL-System. |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Quellverbindung zurück. Diese ID ist in späteren Schritten erforderlich, um eine Zielgruppe zu erstellen.

```json
{
    "id": "beefc650-f2dc-45e2-afc6-50f2dcc5e2b8",
    "etag": "\"1600f153-0000-0200-0000-5e4710880000\""
}
```

## Zielgruppe XDM-Schema erstellen {#target}

In früheren Schritten wurde ein Ad-hoc-XDM-Schema zur Strukturierung der Quelldaten erstellt. Damit die Quelldaten in Platform verwendet werden können, muss auch ein Zielgruppe-Schema erstellt werden, um die Quelldaten entsprechend Ihren Anforderungen zu strukturieren. Mit dem Schema Zielgruppe wird dann ein Plattformdataset erstellt, in dem die Quelldaten enthalten sind. Dieses XDM-Schema der Zielgruppe erweitert auch die XDM Individual Profil-Klasse.

Ein Zielgruppe-XDM-Schema kann erstellt werden, indem eine POST-Anforderung an die [Schema-Registrierungs-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)ausgeführt wird. Wenn Sie die Benutzeroberfläche in Experience Platform bevorzugen, finden Sie im [Schema Editor-Tutorial](../../../../xdm/tutorials/create-schema-ui.md) eine schrittweise Anleitung zum Durchführen ähnlicher Aktionen im Schema-Editor.

**API-Format**

```http
POST /tenant/schemas
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
        "title": "Target schema for database or NoSQL",
        "description": "Target schema for database or NoSQL",
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
    }'
```

**Antwort**

Eine erfolgreiche Antwort gibt Details zum neu erstellten Schema einschließlich seiner eindeutigen Kennung (`$id`) zurück. Diese ID ist in späteren Schritten erforderlich, um einen Zielgruppe-Datensatz, eine Zuordnung und einen Datendurchlauf zu erstellen.

```json
{
    "$id": "https://ns.adobe.com/{TENANT}/schemas/a9d63c5e3fab2687e064577959d0b91e274823f91f2f578e",
    "meta:altId": "_{TENANT}.schemas.a9d63c5e3fab2687e064577959d0b91e274823f91f2f578e",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema for database or NoSQL",
    "type": "object",
    "description": "Target schema for database or NoSQL",
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
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/common/extensible"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1581716110281,
        "repo:lastModifiedDate": 1581716110281,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{LAST_MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "6360f2175b40462ff25ec8735dc93a7e3af6a8faadd80a1cc500a59721e1a424"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "{TENANT_ID}"
}
```

## Zielgruppen-Dataset erstellen

Ein Zielgruppen-Datensatz kann erstellt werden, indem eine POST-Anforderung an die [Katalogdienst-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)ausgeführt wird und die ID des Zielgruppe-Schemas innerhalb der Nutzlast angegeben wird.

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
        "name": "Target Dataset for database or NoSQL",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/a9d63c5e3fab2687e064577959d0b91e274823f91f2f578e",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `schemaRef.id` | Die ID des XDM-Schemas der Zielgruppe. |

**Antwort**

Eine erfolgreiche Antwort gibt ein Array zurück, das die ID des neu erstellten Datensatzes im Format enthält `"@/datasets/{DATASET_ID}"`. Die DataSet-ID ist eine schreibgeschützte, systemgenerierte Zeichenfolge, mit der auf den Datensatz in API-Aufrufen verwiesen wird. Speichern Sie die Zielgruppe-Dataset-ID wie in den späteren Schritten zum Erstellen einer Zielgruppe- und eines Datenflusses erforderlich.

```json
[
    "@/dataSets/5e47161fa49bb818ad7f47bd"
]
```

## Erstellen einer Datenbank-Basisverbindung

Um externe Daten in Platform zu erfassen, muss zunächst eine Verbindung zur Experience Platform-Datenbank aufgebaut werden.

Gehen Sie zum Erstellen einer Datenbankverbindung zum DataSet wie im Lernprogramm zur [Datenbankverbindung beschrieben vor](../create-dataset-base-connection.md).

Führen Sie die im Entwicklerhandbuch beschriebenen Schritte aus, bis Sie eine Datenbank-Basisverbindung erstellt haben. Rufen Sie den eindeutigen Bezeichner ab und speichern Sie ihn (`$id`) und verwenden Sie ihn im nächsten Schritt als Basis-Verbindungs-ID, um eine Zielgruppe zu erstellen.

## Erstellen einer Zielgruppe-Verbindung

Sie haben jetzt die eindeutigen Bezeichner für eine Datenbankverbindung, ein Schema für die Zielgruppe und einen Datensatz für die Zielgruppe. Mithilfe dieser Bezeichner können Sie mithilfe der Flow Service API eine Verbindung zur Zielgruppe herstellen, um das Dataset anzugeben, das die eingehenden Quelldaten enthalten soll.

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
        "baseConnectionId": "d6c3988d-14ef-4000-8398-8d14ef000021",
        "name": "Target Connection for database or NoSQL",
        "description": "Target Connection for database or NoSQL",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/a9d63c5e3fab2687e064577959d0b91e274823f91f2f578e",
                "version": "application/vnd.adobe.xed-full+json;version=1.0"
            }
        },
        "params": {
            "dataSetId": "5e47161fa49bb818ad7f47bd"
        },
        "connectionSpec": {
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `baseConnectionId` | Die ID der Datenbankverbindung Ihres Datensatzes. |
| `data.schema.id` | Die `$id` der Zielgruppe XDM Schema. |
| `params.dataSetId` | Die ID des Zielgruppe-Datensatzes. |
| `connectionSpec.id` | Die Verbindungs-Spezifikations-ID der Drittanbieter-Datenbank. |

>[!NOTE] Achten Sie beim Erstellen einer Zielgruppe darauf, den Datenbasisverbindungswert für die Basisverbindung `id` im Gegensatz zur Basisverbindung des Drittanbieter-Quell-Connectors zu verwenden.

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung der neuen Zielgruppe-Verbindung zurück (`id`). Dieser Wert ist in einem späteren Schritt erforderlich, um einen Datenflug zu erstellen.

```json
{
    "id": "4f3845b6-87d9-4702-b845-b687d9270297",
    "etag": "\"2a007aa8-0000-0200-0000-5e597aaf0000\""
}
```

## Erstellen einer Zuordnung {#mapping}

Damit die Quelldaten in einen Zielgruppe-Datensatz aufgenommen werden können, müssen sie zunächst dem Zielgruppe-Schema zugeordnet werden, dem der Zielgruppe-Datensatz entspricht. Dies wird erreicht, indem eine POST-Anforderung an die Konversions-Dienst-API mit Datenzuordnungen ausgeführt wird, die innerhalb der Anforderungs-Nutzlast definiert sind.

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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/a9d63c5e3fab2687e064577959d0b91e274823f91f2f578e",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "person.name",
                "sourceAttribute": "Name",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "mobilePhone.number",
                "sourceAttribute": "Phone",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "personalEmail.address",
                "sourceAttribute": "email",
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
    "id": "ab91c736-1f3d-4b09-8424-311d3d3e3cea",
    "version": 1,
    "createdDate": 1568047685000,
    "modifiedDate": 1568047703000,
    "inputSchemaRef": {
        "id": null,
        "contentType": null
    },
    "outputSchemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/efea012ad5deefcdf51afd23ceb3583f",
        "contentType": "1.0"
    },
    "mappings": [
        {
            "id": "7bbea5c0f0ef498aa20aa2e2e5c22290",
            "version": 0,
            "createdDate": 1568047685000,
            "modifiedDate": 1568047685000,
            "sourceType": "text/x.schema-path",
            "source": "Id",
            "destination": "_id",
            "identity": false,
            "primaryIdentity": false,
            "matchScore": 0.0,
            "sourceAttribute": "Id",
            "destinationXdmPath": "_id"
        },
        {
            "id": "def7fd7db2244f618d072e8315f59c05",
            "version": 0,
            "createdDate": 1568047685000,
            "modifiedDate": 1568047685000,
            "sourceType": "text/x.schema-path",
            "source": "FirstName",
            "destination": "person.name.firstName",
            "identity": false,
            "primaryIdentity": false,
            "matchScore": 0.0,
            "sourceAttribute": "FirstName",
            "destinationXdmPath": "person.name.firstName"
        },
        {
            "id": "e974986b28c74ed8837570f421d0b2f4",
            "version": 0,
            "createdDate": 1568047685000,
            "modifiedDate": 1568047685000,
            "sourceType": "text/x.schema-path",
            "source": "LastName",
            "destination": "person.name.lastName",
            "identity": false,
            "primaryIdentity": false,
            "matchScore": 0.0,
            "sourceAttribute": "LastName",
            "destinationXdmPath": "person.name.lastName"
        }
    ],
    "status": "PUBLISHED",
    "xdmVersion": "1.0",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/2574494fdb01fa14c25b52d717ccb828",
        "contentType": "1.0"
    },
    "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/2574494fdb01fa14c25b52d717ccb828"
}
```

## Datennachrichtenspezifikationen abrufen {#specs}

Ein Datennachweis ist dafür verantwortlich, Daten aus Quellen zu sammeln und sie in Plattform zu bringen. Um einen Datenflug zu erstellen, müssen Sie zunächst die Datenaflow-Spezifikationen abrufen, indem Sie eine GET-Anforderung an die Flow Service API ausführen. Dataflow-Spezifikationen sind für die Erfassung von Daten aus einer externen Datenbank oder einem NoSQL-System verantwortlich.

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

Bei einer erfolgreichen Antwort werden die Details der Datenaflow-Spezifikation zurückgegeben, die für das Übertragen von Daten aus Ihrer Datenbank oder Ihrem NoSQL-System in die Plattform verantwortlich ist. Diese ID ist im nächsten Schritt erforderlich, um einen neuen Datendurchlauf zu erstellen.

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

## Erstellen eines Datenflusses

Der letzte Schritt zur Datenerfassung besteht darin, einen Datenflug zu erstellen. An dieser Stelle sollten die folgenden erforderlichen Werte vorbereitet sein:

* [Quell-Verbindungs-ID](#source)
* [Zielgruppen-Verbindungs-ID](#target)
* [Mapping-ID](#mapping)
* [Dataflow-Spezifikation-ID](#specs)

Ein Datennachweis ist für die Planung und Erfassung von Daten aus einer Quelle zuständig. Sie können einen Datenflug erstellen, indem Sie eine POST-Anforderung ausführen und dabei die zuvor genannten Werte in der Nutzlast angeben.

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
        "name": "Dataflow between database or NoSQL Platform",
        "description": "Inbound data to Platform",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "beefc650-f2dc-45e2-afc6-50f2dcc5e2b8"
        ],
        "targetConnectionIds": [
            "4f3845b6-87d9-4702-b845-b687d9270297"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "ab91c736-1f3d-4b09-8424-311d3d3e3cea",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1567411548",
            "frequency":"minute",
            "interval":"30"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `flowSpec.id` | Die mit Ihrer Datenbank verknüpfte Datenfadenspezifikations-ID. |
| `sourceConnectionIds` | Die der Datenbank zugeordnete Quell-Verbindungs-ID. |
| `targetConnectionIds` | Die mit der Zielgruppe verknüpfte Verbindungs-ID. |
| `transformations.params.mappingId` | Die mit Ihrer Datenbank verknüpfte Zuordnungs-ID. |

**Antwort**

Eine erfolgreiche Antwort gibt die ID (`id`) des neu erstellten Datenflusses zurück.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```

## Nächste Schritte

In diesem Tutorial haben Sie einen Quell-Connector erstellt, mit dem Daten aus einer Datenbank eines Drittanbieters planmäßig erfasst werden. Eingehende Daten können jetzt von nachgeschalteten Plattformdiensten wie Real-time Customer Profil und Data Science Workspace verwendet werden. Weitere Informationen finden Sie in den folgenden Dokumenten:

* [Übersicht über das Echtzeit-Kundenprofil](../../../../profile/home.md)
* [Übersicht über den Data Science Workspace](../../../../data-science-workspace/home.md)

## Anhang

Im folgenden Abschnitt werden die verschiedenen Cloud-Datenspeicherung-Quellschnittstellen und deren Verbindungsspezifikationen Liste.

### Verbindungsspezifikation

| Connector-Name | Verbindungs-Spec-ID |
| -------------- | --------------- |
| Amazon Redshift | `3416976c-a9ca-4bba-901a-1f08f66978ff` |
| Apache Hive auf Azurblauer HDInsights | `aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f` |
| Apache Spark auf Azurblauen HDInsights | `6a8d82bc-1caf-45d1-908d-cadabc9d63a6` |
| Blue Data Explorer | `0479cc14-7651-4354-b233-7480606c2ac3` |
| Azurblase Synapse Analytics | `a49bcc7d-8038-43af-b1e4-5a7a089a7d79` |
| Datenspeicherung | `ecde33f2-c56f-46cc-bdea-ad151c16cd69` |
| CouchBase | `1fe283f6-9bec-11ea-bb37-0242ac130002` |
| Google BigQuery | `3c9b37f8-13a6-43d8-bad3-b863b941fedd` |
| IBM DB2 | `09182899-b429-40c9-a15a-bf3ddbc8ced7` |
| MariaDB | `000eb99-cd47-43f3-827c-43caf170f015` |
| Microsoft SQL Server | `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec` |
| MySQL | `26d738e0-8963-47ea-aadf-c60de735468a` |
| Oracle | `d6b52d86-f0f8-475f-89d4-ce54c8527328` |
| Phoenix | `102706fb-a5cd-42ee-afe0-bc42f017ff43` |
| PostgreSQL | `74a1c565-4e59-48d7-9d67-7c03b8a13137` |