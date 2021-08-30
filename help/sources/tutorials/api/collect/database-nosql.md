---
keywords: Experience Platform; Startseite; beliebte Themen; Datenbankdatenbank; Datenbank von Drittanbietern
solution: Experience Platform
title: Erfassen von Daten aus einer Datenbank mithilfe von Quell-Connectoren und APIs
topic-legacy: overview
type: Tutorial
description: In diesem Tutorial werden die Schritte zum Abrufen und Erfassen von Daten aus einer Datenbank in Platform mithilfe von Quell-Connectoren und APIs beschrieben.
exl-id: 1e1f9bbe-eb5e-40fb-a03c-52df957cb683
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '1641'
ht-degree: 20%

---

# Erfassen von Daten aus einer Datenbank mithilfe von Quell-Connectoren und APIs

In diesem Tutorial werden die Schritte zum Abrufen von Daten aus einer Datenbank von Drittanbietern und deren Aufnahme in Platform über Quell-Connectoren und die [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) beschrieben.

## Erste Schritte

Für dieses Tutorial benötigen Sie eine gültige Verbindung zu einer Datenbank sowie Informationen über die Datei, die Sie in Platform einbringen möchten (einschließlich Pfad und Struktur der Datei). Wenn Sie nicht über diese Informationen verfügen, lesen Sie zunächst das Tutorial zum [Erkunden einer Datenbank mithilfe der Flow Service-API](../explore/database-nosql.md) , bevor Sie dieses Tutorial ausführen.

Für dieses Tutorial benötigen Sie außerdem ein Verständnis der folgenden Komponenten von Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Entwicklerhandbuch zur Schema Registry](../../../../xdm/api/getting-started.md): Enthält wichtige Informationen, die Sie benötigen, um die Schema Registry-API erfolgreich aufrufen zu können. Diese umfassen Ihre `{TENANT_ID}`, das Konzept sogenannter „Container“ und die für Anfragen erforderlichen Kopfzeilen, von denen insbesondere die Accept-Kopfzeile und deren mögliche Werte wichtig sind.
* [[!DNL Catalog Service]](../../../../catalog/home.md): Catalog ist „System of Record“ für die Position und Herkunft von Daten in Experience Platform.
* [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md): Mit der Batch-Aufnahme-API können Sie Daten als Batch-Dateien in Experience Platform erfassen.
* [Sandboxes](../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der API [[!DNL Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) erfolgreich eine Verbindung zu einer Drittanbieter-Datenbank herstellen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

### Sammeln von Werten für erforderliche Kopfzeilen

Um Platform-APIs aufrufen zu können, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de#platform-apis) abschließen. Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle Ressourcen in der Experience Platform, einschließlich der Ressourcen, die zu [!DNL Flow Service] gehören, werden auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an Platform-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* `x-sandbox-name: {SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* `Content-Type: application/json`

## Quellverbindung erstellen {#source}

Sie können eine Quellverbindung erstellen, indem Sie eine POST-Anfrage an die [!DNL Flow Service]-API richten. Eine Quellverbindung besteht aus einer Verbindungs-ID, einem Pfad zur Quelldatendatei und einer Verbindungsspezifikations-ID.

Um eine Quellverbindung zu erstellen, müssen Sie auch einen Enum-Wert für das Datenformat-Attribut definieren.

Verwenden Sie die folgenden Enum-Werte für dateibasierte Connectoren:

| Datenformat | Enum-Wert |
| ----------- | ---------- |
| Getrennt | `delimited` |
| JSON | `json` |
| Parquet | `parquet` |

Setzen Sie für alle tabellenbasierten Connectoren den Wert auf `tabular`.

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
        "name": "Database source connection",
        "baseConnectionId": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
        "description": "Database source connection",
        "data": {
            "format": "tabular"
        },
        "params": {
            "tableName": "test1.Mytable",
            "columns": [
                {
                    "name": "TestID",
                    "type": "string",
                    "xdm": {
                        "type": "string"
                    }
                },
                {
                    "name": "Name",
                    "type": "string",
                    "xdm": {
                        "type": "string"
                    }
                },
                {
                    "name": "Datefield",
                    "type": "string",
                    "meta:xdmType": "date-time",
                    "xdm": {
                        "type": "string",
                        "format": "date-time"
                    }
                }
            ]
        },
        "connectionSpec": {
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `baseConnectionId` | Die Verbindungs-ID Ihrer Datenbankquelle. |
| `params.path` | Der Pfad der Quelldatei. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID Ihrer Datenbankquelle. Eine Liste der Datenbankspezifikations-IDs finden Sie im Anhang [Anhang](#appendix) . |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Quellverbindung zurück. Diese ID ist in späteren Schritten zum Erstellen einer Zielverbindung erforderlich.

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

## Erstellen eines XDM-Zielschemas {#target-schema}

Damit die Quelldaten in Platform verwendet werden können, muss ein Ziel-XDM-Schema erstellt werden, um die Quelldaten entsprechend Ihren Anforderungen zu strukturieren. Das Ziel-XDM-Schema wird dann verwendet, um einen Platform-Datensatz zu erstellen, in dem die Quelldaten enthalten sind. Dieses Ziel-XDM-Schema erweitert auch die Klasse [!DNL XDM Individual Profile] .

Ein Ziel-XDM-Schema kann durch Ausführung einer POST-Anfrage an die [Schema Registry-API](https://www.adobe.io/experience-platform-apis/references/schema-registry/) erstellt werden.

**API-Format**

```http
POST /tenant/schemas
```

**Anfrage**

Die folgende Beispielanfrage erstellt ein XDM-Schema, das die XDM-Klasse [!DNL Individual Profile] erweitert.

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
        "title": "Database target XDM schema",
        "description": "Database target XDM schema",
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

Eine erfolgreiche Antwort gibt Details zum neu erstellten Schema zurück, einschließlich der eindeutigen Kennung (`$id`). Diese ID ist in späteren Schritten erforderlich, um einen Zieldatensatz, eine Zielzuordnung und einen Datenfluss zu erstellen.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
    "meta:altId": "_{TENANT_ID}.schemas.52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Database target XDM schema",
    "type": "object",
    "description": "Database target XDM schema",
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
        "repo:createdDate": 1612308675206,
        "repo:lastModifiedDate": 1612308675206,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{MODIFIEDD_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "7c5c09e62421e6b172c925f059ac524a99f348dd837b5f13abd77ee91aa6bb61",
        "meta:globalLibVersion": "1.18.4"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "{SANDBOX_ID}",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Zieldatensatz erstellen

Ein Zieldatensatz kann erstellt werden, indem eine POST-Anfrage an die [Catalog Service-API](https://www.adobe.io/experience-platform-apis/references/catalog/) gesendet wird, wobei die Kennung des Zielschemas in der Payload angegeben wird.

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
        "name": "Database target dataset",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `schemaRef.id` | Die ID des Ziel-XDM-Schemas. |
| `schemaRef.contentType` | Die Version des Schemas. Dieser Wert muss auf `application/vnd.adobe.xed-full-notext+json;version=1` gesetzt werden, was die neueste Nebenversion des Schemas zurückgibt. |

**Antwort**

Eine erfolgreiche Antwort gibt ein Array zurück, das die Kennung des neu erstellten Datensatzes im Format `"@/datasets/{DATASET_ID}"` enthält. Die Datensatz-ID ist eine schreibgeschützte, vom System generierte Zeichenfolge, mit der in API-Aufrufen auf den Datensatz verwiesen wird. Speichern Sie die Ziel-Datensatz-ID so, wie es in späteren Schritten erforderlich ist, um eine Zielverbindung und einen Datenfluss zu erstellen.

```json
[
    "@/dataSets/6019e0e7c5dcf718db5ebc71"
]
```

## Erstellen einer Zielverbindung {#target-connection}

Eine Zielverbindung stellt die Verbindung zum Ziel dar, in dem die aufgenommenen Daten landen. Um eine Zielverbindung zu erstellen, müssen Sie die feste Verbindungsspezifikations-ID angeben, die mit dem Data Lake verknüpft ist. Diese Verbindungsspezifikations-ID lautet: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Sie verfügen jetzt über die eindeutigen Kennungen eines Zielschemas, eines Zieldatensatzes und der Verbindungsspezifikations-ID zum Data Lake. Mit der API [!DNL Flow Service] können Sie eine Zielverbindung erstellen, indem Sie diese Kennungen zusammen mit dem Datensatz angeben, der die eingehenden Quelldaten enthalten wird.

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
        "name": "Database target connection",
        "description": "Database target connection",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "6019e0e7c5dcf718db5ebc71"
        },
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `data.schema.id` | Das `$id` des Ziel-XDM-Schemas. |
| `data.schema.version` | Die Version des Schemas. Dieser Wert muss auf `application/vnd.adobe.xed-full+json;version=1` gesetzt werden, was die neueste Nebenversion des Schemas zurückgibt. |
| `params.dataSetId` | Die ID des Zieldatensatzes, der im vorherigen Schritt erfasst wurde. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID, die für die Verbindung mit dem Data Lake verwendet wird. Diese ID lautet: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung der neuen Zielverbindung (`id`) zurück. Dieser Wert ist in einem späteren Schritt zum Erstellen eines Datenflusses erforderlich.

```json
{
    "id": "320f119a-5ac1-4ab1-88ea-eb19e674ea2e",
    "etag": "\"c0038936-0000-0200-0000-6019e1190000\""
}
```

## Erstellen einer Zuordnung {#mapping}

Damit die Quelldaten in einen Zieldatensatz aufgenommen werden können, müssen sie zunächst dem Zielschema zugeordnet werden, dem der Zieldatensatz entspricht. Dies wird erreicht, indem eine POST-Anfrage an die [!DNL Conversion Service]-API mit Datenzuordnungen ausgeführt wird, die in der Anfrage-Payload definiert sind.

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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "TestID",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.fullName",
                "sourceAttribute": "Name",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.birthDate",
                "sourceAttribute": "Datefield",
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
| `xdmSchema` | Das `$id` des Ziel-XDM-Schemas. |

**Antwort**

Eine erfolgreiche Antwort gibt Details zum neu erstellten Mapping zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist in einem späteren Schritt erforderlich, um einen Datenfluss zu erstellen.

```json
{
    "id": "0b090130b58b4819afc78b6dc98b484d",
    "version": 0,
    "createdDate": 1612309018666,
    "modifiedDate": 1612309018666,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Datenflussspezifikationen abrufen {#specs}

Ein Datenfluss ist für die Erfassung von Daten aus Quellen und deren Aufnahme in Platform zuständig. Um einen Datenfluss zu erstellen, müssen Sie zunächst die Datenflussspezifikationen abrufen, indem Sie eine GET-Anfrage an die API [[!DNL Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) senden. Dataflow-Spezifikationen sind für die Erfassung von Daten aus einer externen Datenbank oder einem NoSQL-System verantwortlich.

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

Bei einer erfolgreichen Antwort werden die Details der Datenflug-Spezifikation zurückgegeben, die für die Übermittlung von Daten aus Ihrer Quelle an Platform zuständig ist. Die Antwort enthält die eindeutige Flussspezifikation `id`, die zum Erstellen eines neuen Datenflusses erforderlich ist.

```json
{
    "items": [
        {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "name": "CRMToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "sourceConnectionSpecIds": [
                "3416976c-a9ca-4bba-901a-1f08f66978ff",
                "38ad80fe-8b06-4938-94f4-d4ee80266b07",
                "d771e9c1-4f26-40dc-8617-ce58c4b53702",
                "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
                "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
                "3000eb99-cd47-43f3-827c-43caf170f015",
                "26d738e0-8963-47ea-aadf-c60de735468a",
                "74a1c565-4e59-48d7-9d67-7c03b8a13137",
                "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
                "4f63aa36-bd48-4e33-bb83-49fbcd11c708",
                "cb66ab34-8619-49cb-96d1-39b37ede86ea",
                "eb13cb25-47ab-407f-ba89-c0125281c563",
                "1f372ff9-38a4-4492-96f5-b9a4e4bd00ec",
                "37b6bf40-d318-4655-90be-5cd6f65d334b",
                "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
                "221c7626-58f6-4eec-8ee2-042b0226f03b",
                "a8b6a1a4-5735-42b4-952c-85dce0ac38b5",
                "6a8d82bc-1caf-45d1-908d-cadabc9d63a6",
                "aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f",
                "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
                "ecde33f2-c56f-46cc-bdea-ad151c16cd69",
                "102706fb-a5cd-42ee-afe0-bc42f017ff43",
                "09182899-b429-40c9-a15a-bf3ddbc8ced7",
                "0479cc14-7651-4354-b233-7480606c2ac3",
                "d6b52d86-f0f8-475f-89d4-ce54c8527328",
                "a8f4d393-1a6b-43f3-931f-91a16ed857f4",
                "1fe283f6-9bec-11ea-bb37-0242ac130002"
            ],
            "targetConnectionSpecIds": [
                "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
            ],
            "optionSpec": {
                "name": "OptionSpec",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "errorDiagnosticsEnabled": {
                            "title": "Error diagnostics.",
                            "description": "Flag to enable detailed and sample error diagnostics summary.",
                            "type": "boolean",
                            "default": false
                        },
                        "partialIngestionPercent": {
                            "title": "Partial ingestion threshold.",
                            "description": "Percentage which defines the threshold of errors allowed before the run is marked as failed.",
                            "type": "number",
                            "exclusiveMinimum": 0
                        }
                    }
                }
            },
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
                        "frequency": {
                            "type": "string",
                            "enum": [
                                "once",
                                "minute",
                                "hour",
                                "day",
                                "week"
                            ]
                        },
                        "interval": {
                            "type": "integer"
                        },
                        "backfill": {
                            "type": "boolean",
                            "default": true
                        }
                    },
                    "required": [
                        "startTime",
                        "frequency"
                    ],
                    "if": {
                        "properties": {
                            "frequency": {
                                "const": "once"
                            }
                        }
                    },
                    "then": {
                        "allOf": [
                            {
                                "not": {
                                    "required": [
                                        "interval"
                                    ]
                                }
                            },
                            {
                                "not": {
                                    "required": [
                                        "backfill"
                                    ]
                                }
                            }
                        ]
                    },
                    "else": {
                        "required": [
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
            },
            "attributes": {
                "notification": {
                    "category": "sources",
                    "flowRun": {
                        "enabled": true
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

Der letzte Schritt bei der Datenerfassung besteht darin, einen Datenfluss zu erstellen. An dieser Stelle sollten die folgenden erforderlichen Werte vorbereitet werden:

* [Quellverbindungs-ID](#source)
* [Target-Verbindungs-ID](#target)
* [Mapping-ID](#mapping)
* [Dataflow-Spezifikations-ID](#specs)

Ein Datenfluss ist für die Planung und Erfassung von Daten aus einer Quelle verantwortlich. Sie können einen Datenfluss erstellen, indem Sie eine POST-Anfrage ausführen und dabei die oben genannten Werte in der Anfrage-Payload angeben.

Um eine Aufnahme zu planen, müssen Sie zunächst den Startzeitwert auf Epochenzeit in Sekunden festlegen. Anschließend müssen Sie den Frequenzwert auf eine der fünf Optionen festlegen: `once`, `minute`, `hour`, `day` oder `week`. Der Intervallwert gibt den Zeitraum zwischen zwei aufeinander folgenden Aufnahmen an und bei der Erstellung einer einmaligen Aufnahme ist kein Intervall erforderlich. Für alle anderen Frequenzen muss der Intervallwert auf `15` oder größer gesetzt werden.

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
        "name": "Database dataflow using BigQuery",
        "description": "collecting test1.Mytable",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "b7581b59-c603-4df1-a689-d23d7ac440f3"
        ],
        "targetConnectionIds": [
            "320f119a-5ac1-4ab1-88ea-eb19e674ea2e"
        ],
        "transformations": [
            {
                "name": "Copy",
                "params": {
                    "deltaColumn": {
                        "name": "Datefield",
                        "dateFormat": "YYYY-MM-DD",
                        "timezone": "UTC"
                    }
                }
            },
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "0b090130b58b4819afc78b6dc98b484d",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1612310466",
            "frequency":"minute",
            "interval":"15",
            "backfill": "true"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `flowSpec.id` | Die [Flussspezifikations-ID](#specs), die im vorherigen Schritt abgerufen wurde. |
| `sourceConnectionIds` | Die [Quell-Verbindungs-ID](#source) wurde in einem früheren Schritt abgerufen. |
| `targetConnectionIds` | Die [Ziel-Verbindungs-ID](#target-connection), die in einem früheren Schritt abgerufen wurde. |
| `transformations.params.mappingId` | Die [Zuordnungs-ID](#mapping), die in einem früheren Schritt abgerufen wurde. |
| `transformations.params.deltaColum` | Die benannte Spalte, die verwendet wird, um zwischen neuen und vorhandenen Daten zu unterscheiden. Inkrementelle Daten werden basierend auf dem Zeitstempel der ausgewählten Spalte erfasst. Das unterstützte Datumsformat für `deltaColumn` ist `yyyy-MM-dd HH:mm:ss`. Wenn Sie Azure Table Storage verwenden, wird das Format `deltaColumn` von `yyyy-MM-ddTHH:mm:ssZ` unterstützt. |
| `transformations.params.mappingId` | Die Ihrer Datenbank zugeordnete Zuordnungs-ID. |
| `scheduleParams.startTime` | Die Startzeit für den Datenfluss in Epochenzeit. |
| `scheduleParams.frequency` | Die Häufigkeit, mit der der Datenfluss Daten erfasst. Zulässige Werte sind: `once`, `minute`, `hour`, `day` oder `week`. |
| `scheduleParams.interval` | Das Intervall bezeichnet den Zeitraum zwischen zwei aufeinander folgenden Durchsatzausführungen. Der Wert des Intervalls sollte eine Ganzzahl ungleich null sein. Das Intervall ist nicht erforderlich, wenn die Häufigkeit auf `once` gesetzt ist, und sollte für andere Frequenzwerte größer oder gleich `15` sein. |

**Antwort**

Eine erfolgreiche Antwort gibt die ID (`id`) des neu erstellten Datenflusses zurück.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"770029f8-0000-0200-0000-6019e7d40000\""
}
```

## Überwachen Ihres Datenflusses

Nachdem Ihr Datenfluss erstellt wurde, können Sie die erfassten Daten überwachen, um Informationen über die Durchsatzausführungen, den Abschlussstatus und Fehler anzuzeigen. Weitere Informationen zum Überwachen von Datenflüssen finden Sie im Tutorial zum [Überwachen von Datenflüssen in der API ](../monitor.md)

## Nächste Schritte

In diesem Tutorial haben Sie einen Quell-Connector erstellt, um Daten aus einer Datenbank auf geplanter Basis zu erfassen. Eingehende Daten können jetzt von nachgelagerten Platform-Diensten wie [!DNL Real-time Customer Profile] und [!DNL Data Science Workspace] verwendet werden. Weitere Informationen finden Sie in den folgenden Dokumenten:

* [Übersicht über das Echtzeit-Kundenprofil](../../../../profile/home.md)
* [Data Science Workspace – Übersicht](../../../../data-science-workspace/home.md)

## Anhang

Im folgenden Abschnitt finden Sie die verschiedenen Connectoren für Cloud-Speicher und deren Verbindungsspezifikationen.

### Verbindungsspezifikation

| Connector-Name | Verbindungsspezifikations-ID |
| -------------- | --------------- |
| [!DNL Amazon Redshift] | `3416976c-a9ca-4bba-901a-1f08f66978ff` |
| [!DNL Apache Hive] on  [!DNL Azure HDInsights] | `aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f` |
| [!DNL Apache Spark] on  [!DNL Azure HDInsights] | `6a8d82bc-1caf-45d1-908d-cadabc9d63a6` |
| [!DNL Azure Data Explorer] | `0479cc14-7651-4354-b233-7480606c2ac3` |
| [!DNL Azure Synapse Analytics] | `a49bcc7d-8038-43af-b1e4-5a7a089a7d79` |
| [!DNL Azure Table Storage] | `ecde33f2-c56f-46cc-bdea-ad151c16cd69` |
| [!DNL Couchbase] | `1fe283f6-9bec-11ea-bb37-0242ac130002` |
| [!DNL Google BigQuery] | `3c9b37f8-13a6-43d8-bad3-b863b941fedd` |
| [!DNL Greenplum] | `37b6bf40-d318-4655-90be-5cd6f65d334b` |
| [!DNL IBM DB2] | `09182899-b429-40c9-a15a-bf3ddbc8ced7` |
| [!DNL MariaDB] | `000eb99-cd47-43f3-827c-43caf170f015` |
| [!DNL Microsoft SQL Server] | `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec` |
| [!DNL MySQL] | `26d738e0-8963-47ea-aadf-c60de735468a` |
| [!DNL Oracle] | `d6b52d86-f0f8-475f-89d4-ce54c8527328` |
| [!DNL Phoenix] | `102706fb-a5cd-42ee-afe0-bc42f017ff43` |
| [!DNL PostgreSQL] | `74a1c565-4e59-48d7-9d67-7c03b8a13137` |
