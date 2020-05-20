---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erfassen von Daten aus einem Kundenerfolgssystem über Quellschnittstellen und APIs
topic: overview
translation-type: tm+mt
source-git-commit: c216e321fd913773578107df027d953f10d99a36
workflow-type: tm+mt
source-wordcount: '1496'
ht-degree: 2%

---


# Erfassen von Daten aus einem Kundenerfolgssystem über Quellschnittstellen und APIs

Mit dem Flow-Dienst werden Kundendaten aus verschiedenen Quellen innerhalb der Adobe Experience Platform erfasst und zentralisiert. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

In diesem Lernprogramm werden die Schritte zum Abrufen von Daten aus einem Customer Success-System (&quot;CS&quot;) und zum Integrieren in die Plattform über Quellschnittstellen und APIs beschrieben.

## Erste Schritte

Für dieses Lernprogramm ist es erforderlich, dass Sie über eine gültige Basisverbindung Zugriff auf ein CS-System eines Drittanbieters haben und Informationen über die Datei erhalten, die Sie in Platform einführen möchten, einschließlich des Dateipfads und der Dateistruktur. Wenn Sie diese Informationen nicht haben, lesen Sie das Lernprogramm zur [Erforschung einer Datenbank oder eines NoSQL-Systems mit der Flow Service API](../explore/customer-success.md) , bevor Sie dieses Lernprogramm durchführen.

Für dieses Lernprogramm müssen Sie außerdem die folgenden Komponenten der Adobe Experience Platform verstehen:

* [Erlebnis-Datenmodell (XDM)-System](../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Zusammensetzung](../../../../xdm/schema/composition.md)des Schemas: Erfahren Sie mehr über die grundlegenden Bausteine von XDM-Schemas, einschließlich der wichtigsten Grundsätze und Best Practices bei der Schema-Komposition.
   * [Entwicklerhandbuch](../../../../xdm/api/getting-started.md)zur Schema-Registrierung: Enthält wichtige Informationen, die Sie zur erfolgreichen Durchführung von Aufrufen der Schema Registry API kennen müssen. Dazu gehören Ihre `{TENANT_ID}`, das Konzept der &quot;Container&quot; und die erforderlichen Kopfzeilen für Anfragen (mit besonderer Aufmerksamkeit für den Accept-Header und seine möglichen Werte).
* [Katalogdienst](../../../../catalog/home.md): Catalog ist das Datensatzsystem für die Datenposition und -linie in der Experience Platform.
* [Stapelverarbeitung](../../../../ingestion/batch-ingestion/overview.md): Mit der Batch Ingestion API können Sie Daten als Batch-Dateien in Experience Platform erfassen.
* [Sandboxen](../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Plattforminstanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der Flow Service API eine erfolgreiche Verbindung zu einem CS-System herzustellen.

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
        "name": "Source connection for CS",
        "baseConnectionId": "60a5c8b9-3c30-43ba-a5c8-b93c3093ba66",
        "description": "Source Connection for CS to ingest Account",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/classes/51dd6dce662f8aebe4353c74bbb49c77cb3cbcd6c6b29021",
                "version": "application/vnd.adobe.xed-full-notext+json; version=1"
            }
        },
        "params": {
            "path": "Account"
        },
        "connectionSpec": {
            "id": "eb13cb25-47ab-407f-ba89-c0125281c563",
            "version": "1.0"
    }
}'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `baseConnectionId` | Die ID einer Basisverbindung für ein CS-System |
| `data.schema.id` | Die `$id` des Ad-hoc-XDM-Schemas. |
| `params.path` | Der Pfad der Quelldatei. |
| `connectionSpec.id` | Die Verbindungs-Spezifikations-ID für ein CS-System. |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Quellverbindung zurück. Diese ID ist in späteren Schritten erforderlich, um eine Zielgruppe zu erstellen.

```json
{
    "id": "01b7cbea-cf18-4552-b7cb-eacf18055294",
    "etag": "\"2103ac94-0000-0200-0000-5e543ad70000\""
}
```

## Zielgruppe XDM-Schema erstellen {#target}

In früheren Schritten wurde ein Ad-hoc-XDM-Schema zur Strukturierung der Quelldaten erstellt. Damit die Quelldaten in Platform verwendet werden können, muss auch ein Zielgruppe-Schema erstellt werden, um die Quelldaten entsprechend Ihren Anforderungen zu strukturieren. Mit dem Schema Zielgruppe wird dann ein Plattformdataset erstellt, in dem die Quelldaten enthalten sind. Dieses XDM-Schema der Zielgruppe erweitert auch die XDM Individual Profil-Klasse.

Ein Zielgruppe-XDM-Schema kann erstellt werden, indem eine POST-Anforderung an die [Schema-Registrierungs-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)ausgeführt wird.

Wenn Sie die Benutzeroberfläche in Experience Platform bevorzugen, finden Sie im [Schema Editor-Tutorial](../../../../xdm/tutorials/create-schema-ui.md) eine schrittweise Anleitung zum Durchführen ähnlicher Aktionen im Schema-Editor.

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
        "title": "Target schema for CS",
        "description": "Target schema for CS",
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
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/deb3e1096c35d8311b5d80868c4bd5b3cdfd4b3150e7345f",
    "meta:altId": "_{TENANT_ID}.schemas.deb3e1096c35d8311b5d80868c4bd5b3cdfd4b3150e7345f",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema for CS",
    "type": "object",
    "description": "Target schema for CS",
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
        "repo:createdDate": 1582578764554,
        "repo:lastModifiedDate": 1582578764554,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{LAST_MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "213e4bf7cbac74e3a9e6f988da321e2f7353acacd9ea651a5652bd49b28b8d2a"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}"
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
        "name": "Target Dataset for CS",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/deb3e1096c35d8311b5d80868c4bd5b3cdfd4b3150e7345f",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `schemaRef.id` | Die `$id` der Zielgruppe XDM Schema. |

**Antwort**

Eine erfolgreiche Antwort gibt ein Array zurück, das die ID des neu erstellten Datensatzes im Format enthält `"@/datasets/{DATASET_ID}"`. Die DataSet-ID ist eine schreibgeschützte, systemgenerierte Zeichenfolge, mit der auf den Datensatz in API-Aufrufen verwiesen wird. Speichern Sie die Zielgruppe-Dataset-ID wie in den späteren Schritten zum Erstellen einer Zielgruppe- und eines Datenflusses erforderlich.

```json
[
    "@/dataSets/5e543e8a60b15218ad44b95f"
]
```

## Erstellen einer Datenbank-Basisverbindung

Um externe Daten in Platform zu erfassen, muss zunächst eine Verbindung zur Experience Platform-Datenbank aufgebaut werden.

Gehen Sie zum Erstellen einer Datenbankverbindung zum DataSet wie im Lernprogramm zur [Datenbankverbindung beschrieben vor](../create-dataset-base-connection.md).

Führen Sie die im Entwicklerhandbuch beschriebenen Schritte aus, bis Sie eine Datenbank-Basisverbindung erstellt haben. Rufen Sie den eindeutigen Bezeichner ab und speichern Sie ihn (`$id`) und verwenden Sie ihn im nächsten Schritt als Basis-Verbindungs-ID, um eine Zielgruppe zu erstellen.

## Erstellen einer Zielgruppe-Verbindung

Sie haben jetzt die eindeutigen Bezeichner für eine DataSet-Basisverbindung, ein Zielgruppe-Schema und einen Dataset für die Zielgruppe. Sie können jetzt eine Zielgruppe-Verbindung mit der Flow Service API erstellen, um den Datensatz anzugeben, der die eingehenden Quelldaten enthalten soll.

**API-Format**

```http
POST /targetConnections
```

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
        "name": "Target Connection for CS",
        "description": "Target Connection for CS",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}}/schemas/deb3e1096c35d8311b5d80868c4bd5b3cdfd4b3150e7345f",
                "version": "application/vnd.adobe.xed-full+json;version=1.0"
            }
        },
        "params": {
            "dataSetId": "5e543e8a60b15218ad44b95f"
        },
            "connectionSpec": {
            "id": "eb13cb25-47ab-407f-ba89-c0125281c563",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `baseConnectionId` | Die ID der Datenbankverbindung Ihres Datensatzes. |
| `data.schema.id` | Die `$id` der Zielgruppe XDM Schema. |
| `params.dataSetId` | Die ID des Zielgruppe-Datensatzes. |
| `connectionSpec.id` | Die Verbindungs-ID für Ihr Kundenerfolgssystem. |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung der neuen Zielgruppe-Verbindung zurück (`id`). Dieser Wert ist in einem späteren Schritt erforderlich, um einen Datenflug zu erstellen.

```json
{
    "id": "5ebaf0b3-66dc-46bf-baf0-b366dc76bfd5",
    "etag": "\"5d02211d-0000-0200-0000-5e543f0f0000\""
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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/deb3e1096c35d8311b5d80868c4bd5b3cdfd4b3150e7345f",
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

## Spezifikationen zum Nachschlagen von Datenblättern {#specs}

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

Bei einer erfolgreichen Antwort werden die Details der Datenaflow-Spezifikation zurückgegeben, die für die Übertragung von Daten aus Ihrem CS-System in die Plattform verantwortlich ist. Diese ID ist im nächsten Schritt erforderlich, um einen neuen Datendurchlauf zu erstellen.

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
            "01b7cbea-cf18-4552-b7cb-eacf18055294"
        ],
        "targetConnectionIds": [
            "5ebaf0b3-66dc-46bf-baf0-b366dc76bfd5"
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

**Antwort**

Eine erfolgreiche Antwort gibt die ID `id` des neu erstellten Datenflusses zurück.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```

## Nächste Schritte

In diesem Lernprogramm haben Sie einen Quell-Connector erstellt, um Daten aus einem CS-System planmäßig zu erfassen. Eingehende Daten können jetzt von nachgeschalteten Plattformdiensten wie Real-time Customer Profil und Data Science Workspace verwendet werden. Weitere Informationen finden Sie in den folgenden Dokumenten:

* [Übersicht über das Echtzeit-Kundenprofil](../../../../profile/home.md)
* [Übersicht über den Data Science Workspace](../../../../data-science-workspace/home.md)