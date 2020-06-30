---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erfassen von Cloud-Datenspeicherung-Daten über Quellschnittstellen und APIs
topic: overview
translation-type: tm+mt
source-git-commit: 6c6bbfc39b5b17c45d5db53bbec5342430a0941a
workflow-type: tm+mt
source-wordcount: '1628'
ht-degree: 2%

---


# Erfassen von Cloud-Datenspeicherung-Daten über Quellschnittstellen und APIs

[!DNL Flow Service] dient zur Erfassung und Zentralisierung von Kundendaten aus unterschiedlichen Quellen innerhalb der Adobe Experience Platform. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

In diesem Lernprogramm werden die Schritte zum Abrufen von Daten aus einer Cloud-Datenspeicherung eines Drittanbieters und zum Übertragen dieser Daten [!DNL Platform] über Quellschnittstellen und APIs beschrieben.

## Erste Schritte

Für dieses Lernprogramm ist es erforderlich, dass Sie über eine gültige Verbindung Zugriff auf eine Cloud-Datenspeicherung eines Drittanbieters haben und Informationen über die Datei erhalten, die Sie einsetzen möchten, [!DNL Platform]einschließlich des Dateipfads und der Dateistruktur. Wenn Sie diese Informationen nicht haben, lesen Sie das Lernprogramm zur [Erforschung einer Cloud-Datenspeicherung von Drittanbietern mithilfe der Flow Service API](../explore/cloud-storage.md) , bevor Sie dieses Lernprogramm durchführen.

Für dieses Lernprogramm müssen Sie außerdem die folgenden Komponenten der Adobe Experience Platform verstehen:

- [Erlebnis-Datenmodell (XDM)-System](../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   - [Grundlagen der Zusammensetzung](../../../../xdm/schema/composition.md)des Schemas: Erfahren Sie mehr über die grundlegenden Bausteine von XDM-Schemas, einschließlich der wichtigsten Grundsätze und Best Practices bei der Schema-Komposition.
   - [Entwicklerhandbuch](../../../../xdm/api/getting-started.md)zur Schema-Registrierung: Enthält wichtige Informationen, die Sie zur erfolgreichen Durchführung von Aufrufen der Schema Registry API kennen müssen. Dazu gehören Ihre `{TENANT_ID}`, das Konzept der &quot;Container&quot; und die erforderlichen Kopfzeilen für Anfragen (mit besonderer Aufmerksamkeit für den Accept-Header und seine möglichen Werte).
- [Katalogdienst](../../../../catalog/home.md): Catalog ist das Datensatzsystem für die Datenposition und -linie innerhalb [!DNL Experience Platform].
- [Stapelverarbeitung](../../../../ingestion/batch-ingestion/overview.md): Mit der Stapeleinbetungs-API können Sie Daten [!DNL Experience Platform] als Batch-Dateien erfassen.
- [Sandboxen](../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service] API eine Verbindung zu einer Cloud-Datenspeicherung herstellen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Lernprogramm finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur [!DNL Experience Platform] Fehlerbehebung.

### Werte für erforderliche Kopfzeilen sammeln

Um [!DNL Platform] APIs aufzurufen, müssen Sie zunächst das [Authentifizierungslehrgang](../../../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungtutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen [!DNL Experience Platform] API-Aufrufen bereit, wie unten dargestellt:

- Genehmigung: Träger `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Sämtliche Ressourcen in [!DNL Experience Platform]und auch die Ressourcen, die [!DNL Flow Service]gehören, werden zu bestimmten virtuellen Sandboxen isoliert. Alle Anforderungen an [!DNL Platform] APIs erfordern einen Header, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

- x-sandbox-name: `{SANDBOX_NAME}`

Für alle Anforderungen, die eine Payload enthalten (POST, PUT, PATCH), ist ein zusätzlicher Medientyp-Header erforderlich:

- Content-Type: `application/json`

## Erstellen einer Ad-hoc-XDM-Klasse und eines Ad-hoc-Schemas

Um externe Daten [!DNL Platform] über Quell-Connectors zu importieren, müssen eine Ad-hoc-XDM-Klasse und ein Schema für die Rohquellendaten erstellt werden.

Um eine Ad-hoc-Klasse und ein Ad-hoc-Schema zu erstellen, führen Sie die im [Ad-hoc-Schema-Lernprogramm](../../../../xdm/tutorials/ad-hoc.md)beschriebenen Schritte aus. Beim Erstellen einer Ad-hoc-Klasse müssen alle in den Quelldaten gefundenen Felder im Anforderungstext beschrieben werden.

Führen Sie die im Entwicklerhandbuch beschriebenen Schritte aus, bis Sie ein Ad-hoc-Schema erstellt haben. Die eindeutige Kennung (`$id`) des Ad-hoc-Schemas ist erforderlich, um mit dem nächsten Schritt dieses Lernprogramms fortzufahren.

## Erstellen einer Quellverbindung {#source}

Bei Erstellung eines Ad-hoc-XDM-Schemas kann jetzt eine Quellverbindung mit einer POST-Anforderung an die [!DNL Flow Service] API erstellt werden. Eine Quellverbindung besteht aus einer Verbindungs-ID, einer Quelldatendatei und einem Verweis auf das Schema, das die Quelldaten beschreibt.

Um eine Quellverbindung zu erstellen, müssen Sie auch einen Enum-Wert für das Datenformatattribut definieren.

Verwenden Sie die folgenden Enum-Werte für **dateibasierte Connectors**:

| Data.format | Enum-Wert |
| ----------- | ---------- |
| Getrennte Dateien | `delimited` |
| JSON-Dateien | `json` |
| Parkettdateien | `parquet` |

Für alle **tabellenbasierten Connectors** verwenden Sie den Enum-Wert: `tabular`.

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
        "name": "Test source connection for a Cloud Storage connector",
        "baseConnectionId": "ac33bd66-1565-4915-b3bd-6615657915c4",
        "description": "Test source connection for a Cloud Storage connector",
        "data": {
            "format": "delimited",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/22a4ab59462a64de551d42dd10ec1f19d8d7246e3f90072a",
                "version": "application/vnd.adobe.xed-full-notext+json; version=1"
            }
        },
        "params": {
            "path": "/backfil/data8.csv",
            "recursive": "true"
        },
        "connectionSpec": {
            "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `baseConnectionId` | Die eindeutige Verbindungs-ID des Cloud-Datenspeicherung-Systems eines Drittanbieters, auf das Sie zugreifen. |
| `data.schema.id` | Die ID des Ad-hoc-XDM-Schemas. |
| `params.path` | Der Pfad der Quelldatei, auf die Sie zugreifen. |
| `connectionSpec.id` | Die mit Ihrem Cloud-Datenspeicherung-System eines Drittanbieters verknüpfte Verbindungsspezifikations-ID. Eine Liste der Verbindungsspezifikations-IDs finden Sie im [Anhang](#appendix) . |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Quellverbindung zurück. Diese ID ist in einem späteren Schritt zum Erstellen eines Datenflusses erforderlich.

```json
{
    "id": "8bae595c-8548-4716-ae59-5c85480716e9",
    "etag": "\"4a00038b-0000-0200-0000-5ebc47fd0000\""
}
```

## Zielgruppe XDM-Schema erstellen {#target}

In früheren Schritten wurde ein Ad-hoc-XDM-Schema zur Strukturierung der Quelldaten erstellt. Damit die Quelldaten in verwendet werden können, [!DNL Platform]muss auch ein Zielgruppe-Schema erstellt werden, um die Quelldaten entsprechend Ihren Anforderungen zu strukturieren. Mit dem Schema Zielgruppe wird dann ein [!DNL Platform] Datensatz erstellt, in dem die Quelldaten enthalten sind.

Ein Zielgruppe-XDM-Schema kann erstellt werden, indem eine POST-Anforderung an die [Schema-Registrierungs-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)ausgeführt wird.

Wenn Sie lieber die Benutzeroberfläche in verwenden möchten, [!DNL Experience Platform]finden Sie im [Schema Editor-Tutorial](../../../../xdm/tutorials/create-schema-ui.md) eine schrittweise Anleitung zum Durchführen ähnlicher Aktionen im Schema-Editor.

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
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e28dd48fab732263816f8b80ae4fdf49ca7ad229ca62e5d6",
    "meta:altId": "_{TENANT_ID}.schemas.e28dd48fab732263816f8b80ae4fdf49ca7ad229ca62e5d6",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema for a Cloud Storage connector",
    "type": "object",
    "description": "Target schema for Cloud Storage",
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
        "repo:createdDate": 1589398474190,
        "repo:lastModifiedDate": 1589398474190,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{LAST_MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "f07723475e933dc30ed411d97986a36f13aa20c820463dd8cf7b74e63f4e7801",
        "meta:globalLibVersion": "1.10.1.1"
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
        "name": "Target dataset for a Cloud Storage connector",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT}/schemas/e28dd48fab732263816f8b80ae4fdf49ca7ad229ca62e5d6",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `schemaRef.id` | Die ID des XDM-Schemas der Zielgruppe. |

**Antwort**

Eine erfolgreiche Antwort gibt ein Array zurück, das die ID des neu erstellten Datensatzes im Format enthält `"@/datasets/{DATASET_ID}"`. Die DataSet-ID ist eine schreibgeschützte, systemgenerierte Zeichenfolge, mit der auf den Datensatz in API-Aufrufen verwiesen wird. Die Zielgruppe DataSet-ID ist in späteren Schritten erforderlich, um eine Zielgruppe- und einen Datendurchlauf zu erstellen.

```json
[
    "@/dataSets/5ebc4be8590b1b191a8dc4ca"
]
```

## Erstellen einer Zielgruppe-Verbindung

Eine Zielgruppe-Verbindung stellt die Verbindung mit dem Ziel dar, in dem die erfassten Daten landen. Um eine Zielgruppe-Verbindung zu erstellen, müssen Sie die mit dem Datensee verknüpfte feste Verbindungs-spec-ID angeben. Diese Verbindungs-Spec-ID lautet: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Sie haben jetzt die eindeutigen Bezeichner, ein Zielgruppe-Schema, einen Zielgruppe-Datensatz und die Verbindungsspezifikations-ID zum Datensee. Mithilfe dieser Bezeichner können Sie mithilfe der [!DNL Flow Service] API eine Verbindung zur Zielgruppe herstellen, um den Datensatz anzugeben, der die eingehenden Quelldaten enthalten soll.

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
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e28dd48fab732263816f8b80ae4fdf49ca7ad229ca62e5d6",
                "version": "application/vnd.adobe.xed-full+json;version=1.0"
            }
        },
        "params": {
            "dataSetId": "5ebc4be8590b1b191a8dc4ca"
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
| `connectionSpec.id` | Die feste Verbindungs-spec-ID zum Datensee. Diese ID lautet: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung der neuen Zielgruppe-Verbindung zurück (`id`). Diese ID ist in späteren Schritten erforderlich.

```json
{
    "id": "1f5af99c-f1ef-4076-9af9-9cf1ef507678",
    "etag": "\"530013e2-0000-0200-0000-5ebc4c110000\""
}
```

## Erstellen einer Zuordnung {#mapping}

Damit die Quelldaten in einen Zielgruppe-Datensatz aufgenommen werden können, müssen sie zunächst dem Zielgruppe-Schema zugeordnet werden, dem der Zielgruppe-Datensatz entspricht. Dies wird erreicht, indem eine POST-Anforderung an den Konvertierungsdienst mit Datenzuordnungen ausgeführt wird, die innerhalb der Anforderungs-Nutzlast definiert sind.

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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/e28dd48fab732263816f8b80ae4fdf49ca7ad229ca62e5d6",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "first_name",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "last_name",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "id",
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
| --- | --- |
| `xdmSchema` | Die ID des XDM-Schemas der Zielgruppe. |

**Antwort**

Eine erfolgreiche Antwort gibt Details der neu erstellten Zuordnung einschließlich ihrer eindeutigen Kennung (`id`) zurück. Dieser Wert ist in einem späteren Schritt erforderlich, um einen Datenflug zu erstellen.

```json
{
    "id": "febec6a6785e45ea9ed594422cc483d7",
    "version": 0,
    "createdDate": 1589398562232,
    "modifiedDate": 1589398562232,
    "createdBy": "28AF22BA5DE6B0B40A494036@AdobeID",
    "modifiedBy": "28AF22BA5DE6B0B40A494036@AdobeID"
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

## Erstellen eines Datenflusses

Der letzte Schritt zur Erfassung von Cloud-Datenspeicherung-Daten besteht darin, einen Datenflug zu erstellen. Jetzt haben Sie die folgenden erforderlichen Werte vorbereitet:

- [Quell-Verbindungs-ID](#source)
- [Target-Verbindungs-ID](#target)
- [Mapping-ID](#mapping)
- [Dataflow-Spezifikation-ID](#specs)

Ein Datennachweis ist für die Planung und Erfassung von Daten aus einer Quelle zuständig. Sie können einen Datenflug erstellen, indem Sie eine POST-Anforderung ausführen und dabei die zuvor genannten Werte in der Nutzlast angeben.

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
        "name": "Cloud Storage flow to AEP",
        "description": "Cloud Storage flow to AEP",
        "flowSpec": {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "8bae595c-8548-4716-ae59-5c85480716e9"
        ],
        "targetConnectionIds": [
            "1f5af99c-f1ef-4076-9af9-9cf1ef507678"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "febec6a6785e45ea9ed594422cc483d7",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1589398646",
            "frequency":"minute",
            "interval":"30"
        }
    }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `flowSpec.id` | Die Flussspec-ID, die im vorherigen Schritt abgerufen wurde. |
| `sourceConnectionIds` | Die Quell-Verbindungs-ID, die in einem früheren Schritt abgerufen wurde. |
| `targetConnectionIds` | Die Zielgruppe-Verbindungs-ID, die in einem früheren Schritt abgerufen wurde. |
| `transformations.params.mappingId` | Die Zuordnungs-ID, die in einem früheren Schritt abgerufen wurde. |
| `scheduleParams.startTime` | Die Zeitdauer des Beginns für den Datendurchlauf in Sekunden. |
| `scheduleParams.frequency` | Die auswählbaren Frequenzwerte umfassen: `once`, `minute`, `hour`, `day`oder `week`. |
| `scheduleParams.interval` | Das Intervall gibt den Zeitraum zwischen zwei aufeinander folgenden Flussläufen an. Der Wert des Intervalls sollte eine Ganzzahl ungleich null sein. Das Intervall ist nicht erforderlich, wenn die Häufigkeit für andere Frequenzwerte festgelegt ist `once` und größer oder gleich `15` sein sollte. |

**Antwort**

Eine erfolgreiche Antwort gibt die ID (`id`) des neu erstellten Datenflusses zurück.

```json
{
    "id": "e0bd8463-0913-4ca1-bd84-6309134ca1f6",
    "etag": "\"04004fe9-0000-0200-0000-5ebc4c8b0000\""
}
```

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