---
title: Erstellen eines Datenflusses, um Daten aus einem CRM in Experience Platform aufzunehmen
description: Erfahren Sie, wie Sie mit der Flow Service-API einen Datenfluss erstellen und Quelldaten in Experience Platform aufnehmen.
exl-id: b07dd640-bce6-4699-9d2b-b7096746934a
source-git-commit: b4f8d44c3ce9507ff158cf051b7a4b524b293c64
workflow-type: tm+mt
source-wordcount: '2112'
ht-degree: 10%

---

# Erstellen eines Datenflusses, um Daten aus einem CRM in Experience Platform aufzunehmen

Lesen Sie dieses Handbuch, um zu erfahren, wie Sie mithilfe der -API einen Datenfluss erstellen [[!DNL Flow Service]  Daten in Adobe Experience Platform ](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Experience Platform voraus:

* [Batch-Aufnahme](../../../../ingestion/batch-ingestion/overview.md): So können Sie schnell und effizient große Datenmengen in Batches hochladen.
* [Katalog-Service](../../../../catalog/datasets/overview.md): Datensätze in Experience Platform organisieren und verfolgen.
* [Datenvorbereitung](../../../../data-prep/home.md): Transformieren und Zuordnen Ihrer eingehenden Daten entsprechend Ihren Schemaanforderungen.
* [Datenflüsse](../../../../dataflows/home.md): Richten Sie die Pipelines ein und verwalten Sie sie, die Ihre Daten von Quellen zu Zielen verschieben.
* [Experience-Datenmodell(XDM)-Schemata](../../../../xdm/home.md): Strukturieren Sie Ihre Daten mithilfe von XDM-Schemata, damit sie in Experience Platform verwendet werden können.
* [Sandboxes](../../../../sandboxes/home.md): Sicheres Testen und Entwickeln in isolierten Umgebungen ohne Auswirkungen auf die Produktionsdaten.
* [Quellen](../../../home.md): Erfahren Sie, wie Sie Ihre externen Datenquellen mit Experience Platform verbinden.

### Verwenden von Experience Platform-APIs

Informationen zum erfolgreichen Aufrufen von Experience Platform-APIs finden Sie im Handbuch unter [ mit Experience Platform-APIs](../../../../landing/api-guide.md).

### Basisverbindung erstellen {#base}

Um einen Datenfluss für Ihre Quelle zu erstellen, benötigen Sie ein vollständig authentifiziertes Quellkonto und die entsprechende Basisverbindungs-ID. Wenn Sie diese ID nicht haben, suchen Sie im [Quellkatalog](../../../home.md) nach einer Liste von Quellen, für die Sie eine Basisverbindung erstellen können.

### Erstellen eines XDM-Zielschemas {#target-schema}

Ein Experience-Datenmodell (XDM)-Schema bietet eine standardisierte Möglichkeit, Kundenerlebnisdaten in Experience Platform zu organisieren und zu beschreiben. Um Ihre Quelldaten in Experience Platform aufzunehmen, müssen Sie zunächst ein Ziel-XDM-Schema erstellen, das die Struktur und die Datentypen definiert, die Sie aufnehmen möchten. Dieses Schema dient als Blueprint für den Experience Platform-Datensatz, in dem sich Ihre aufgenommenen Daten befinden.

Sie können ein Ziel-XDM-Schema erstellen, indem Sie eine POST-Anfrage an die [Schema Registry-API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/) senden. Ausführliche Anweisungen zum Erstellen eines XDM-Zielschemas finden Sie in den folgenden Handbüchern:

* [Erstellen eines Schemas mithilfe der API](../../../../xdm/api/schemas.md).
* [Erstellen eines Schemas über die Benutzeroberfläche](../../../../xdm/tutorials/create-schema-ui.md).

Nach der Erstellung ist das Ziel-XDM-Schema `$id` später für Ihren Zieldatensatz und Ihre Zuordnung erforderlich.

### Erstellen eines Zieldatensatzes {#target-dataset}

Ein Datensatz ist ein Konstrukt zur Datenspeicherung und -verwaltung, das typischerweise wie eine Tabelle mit Spalten (Schema) und Zeilen (Feldern) strukturiert ist. Daten, die erfolgreich in Experience Platform aufgenommen werden, werden im Data Lake als Datensätze gespeichert. In diesem Schritt können Sie entweder einen neuen Datensatz erstellen oder einen vorhandenen Datensatz verwenden.

Sie können einen Zieldatensatz erstellen, indem Sie eine POST-Anfrage an die [Catalog Service API](https://developer.adobe.com/experience-platform-apis/references/catalog/) senden und dabei die ID des Zielschemas in der Payload angeben. Ausführliche Anweisungen zum Erstellen eines Zieldatensatzes finden Sie im Handbuch unter [Erstellen eines Datensatzes mithilfe der API](../../../../catalog/api/create-dataset.md).

>[!TIP]
>
>Wenn Sie Ihre Daten in das Echtzeit-Kundenprofil aufnehmen möchten, müssen Sie sicherstellen, dass sowohl Ihre Ziel-XDM-Schemata als auch Ihr Zieldatensatz für das Profil aktiviert sind.

+++Beispiel anzeigen

**API-Format**

```HTTP
POST /dataSets
```

**Anfrage**

Das folgende Beispiel zeigt, wie ein Zieldatensatz erstellt wird, der für die Aufnahme von Echtzeit-Kundenprofilen aktiviert ist. In dieser Anfrage wird die `unifiedProfile`-Eigenschaft auf `true` (unter dem `tags`-Objekt) festgelegt, wodurch Experience Platform angewiesen wird, den Datensatz in das Echtzeit-Kundenprofil aufzunehmen.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "ACME Target Dataset",
    "schemaRef": {
      "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
      "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "tags": {
      "unifiedProfile": [
        "enabled: true"
      ]
    }
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Ein beschreibender Name für Ihren Zieldatensatz. Verwenden Sie einen klaren und eindeutigen Namen, um die Identifizierung und Verwaltung Ihres Datensatzes in zukünftigen Vorgängen zu erleichtern. |
| `schemaRef.id` | Die ID Ihres XDM-Zielschemas. |
| `tags.unifiedProfile` | Ein boolescher Wert, der Experience Platform darüber informiert, ob die Daten in das Echtzeit-Kundenprofil aufgenommen werden sollen. |

**Antwort**

Eine erfolgreiche Antwort gibt die ID Ihres Zieldatensatzes zurück. Diese ID ist später erforderlich, um eine Zielverbindung zu erstellen.

```json
[
    "@/dataSets/6889f4f89b982b2b90bc1207"
]
```

+++

## Erstellen einer Quellverbindung {#source}

Eine Quellverbindung definiert, wie Daten von einer externen Quelle in Experience Platform importiert werden. Sie gibt sowohl das Quellsystem als auch das Format der eingehenden Daten an und verweist auf eine Basisverbindung, die Authentifizierungsdetails enthält. Jede Quellverbindung ist für Ihre Organisation eindeutig.

* Bei dateibasierten Quellen (z. B. Cloud-Speichern) kann eine Quellverbindung Einstellungen wie Spaltentrennzeichen, Kodierungstyp, Komprimierungstyp, reguläre Ausdrücke für die Dateiauswahl und die Frage enthalten, ob Dateien rekursiv aufgenommen werden sollen.
* Bei tabellenbasierten Quellen (z. B. Datenbanken, CRMs und Anbietern von Marketing-Automatisierung) kann eine Quellverbindung Details wie den Tabellennamen und Spaltenzuordnungen angeben.

Um eine Quellverbindung zu erstellen, stellen Sie eine POST-Anfrage an den `/sourceConnections`-Endpunkt der [!DNL Flow Service]-API und geben Sie Ihre Basisverbindungs-ID, Verbindungsspezifikations-ID und den Pfad zur Quelldatendatei an.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "ACME source connection",
    "description": "A source connection for ACME contact data",
    "baseConnectionId": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "data": {
      "format": "tabular"
    },
    "params": {
      "tableName": "Contact",
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
      "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
      "version": "1.0"
    }
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Ein beschreibender Name für Ihre Quellverbindung. Verwenden Sie einen klaren und eindeutigen Namen, um die Identifizierung und Verwaltung Ihrer Verbindung in zukünftigen Vorgängen zu erleichtern. |
| `description` | Eine optionale Beschreibung, die Sie hinzufügen können, um zusätzliche Informationen zu Ihrer Quellverbindung bereitzustellen. |
| `baseConnectionId` | Die `id` Ihrer -Basisverbindung. Sie können diese ID abrufen, indem Sie Ihre Quelle mithilfe der [!DNL Flow Service]-API für Experience Platform authentifizieren. |
| `data.format` | Das Format Ihrer Daten. Legen Sie diesen Wert für tabellenbasierte Quellen (z. B. Datenbanken, CRMs und Anbieter von Marketing-Automatisierung) auf `tabular` fest. |
| `params.tableName` | Der Name der Tabelle in Ihrem Quellkonto, die Sie in Experience Platform aufnehmen möchten. |
| `params.columns` | Die spezifischen Tabellenspalten der Daten, die Sie in Experience Platform aufnehmen möchten. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID der Quelle, die Sie verwenden. |

**Antwort**

Bei einer erfolgreichen Antwort wird die ID Ihrer Quellverbindung zurückgegeben. Diese ID ist erforderlich, um einen Datenfluss zu erstellen und Ihre Daten aufzunehmen.

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

## Erstellen einer Zielverbindung {#target}

Eine Zielverbindung stellt die Verbindung zum Ziel dar, in das die aufgenommenen Daten übernommen werden. Um eine Zielverbindung zu erstellen, müssen Sie die feste Verbindungsspezifikations-ID angeben, die mit dem Data Lake verknüpft ist. Diese Verbindungsspezifikations-ID lautet: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

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
      "name": "ACME target connection",
      "description": "ACME target connection",
      "data": {
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "6889f4f89b982b2b90bc1207"
      },
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
    }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Ein beschreibender Name für Ihre Zielverbindung. Verwenden Sie einen klaren und eindeutigen Namen, um die Identifizierung und Verwaltung Ihrer Verbindung in zukünftigen Vorgängen zu erleichtern. |
| `description` | Eine optionale Beschreibung, die Sie hinzufügen können, um zusätzliche Informationen zu Ihrer Zielverbindung bereitzustellen. |
| `data.schema.id` | Die ID Ihres XDM-Zielschemas. |
| `params.dataSetId` | Die ID Ihres Zieldatensatzes. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID des Data Lake. Diese ID ist fest: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

## Zuordnung {#mapping}

Ordnen Sie anschließend Ihre Quelldaten dem Zielschema zu, dem Ihr Zieldatensatz entspricht. Um eine Zuordnung zu erstellen, stellen Sie eine POST-Anfrage an den `mappingSets` der [[!DNL Data Prep] API](https://developer.adobe.com/experience-platform-apis/references/data-prep/). Geben Sie Ihre Ziel-XDM-Schema-ID und die Details der Zuordnungssätze an, die Sie erstellen möchten.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `xdmSchema` | `$id` des XDM-Zielschemas. |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Zuordnung zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist in einem späteren Schritt erforderlich, um einen Datenfluss zu erstellen.

```json
{
    "id": "93ddfa69c4864d978832b1e5ef6ec3b9",
    "version": 0,
    "createdDate": 1612309018666,
    "modifiedDate": 1612309018666,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Abrufen von Datenflussspezifikationen {#flow-specs}

Bevor Sie einen Datenfluss erstellen können, müssen Sie zunächst die Datenflussspezifikationen abrufen, die Ihrer Quelle entsprechen. Um diese Informationen abzurufen, stellen Sie eine GET-Anfrage an den `/flowSpecs` der [!DNL Flow Service]-API.

**API-Format**

```http
GET /flowSpecs?property=name=="{NAME}"
```

| Abfrageparameter | Beschreibung |
| --- | --- |
| `property=name=="{NAME}"` | Der Name Ihrer Datenflussspezifikation. <ul><li>Legen Sie für dateibasierte Quellen (z. B. Cloud-Speicher) diesen Wert auf `CloudStorageToAEP` fest.</li><li>Legen Sie für tabellenbasierte Quellen (z. B. Datenbanken, CRMs und Anbieter von Marketing-Automatisierung) diesen Wert auf `CRMToAEP` fest.</li></ul> |

**Anfrage**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name=="CRMToAEP"' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Datenflussspezifikation zurück, die für die Übermittlung von Daten aus Ihrer Quelle an Experience Platform verantwortlich ist. Die Antwort enthält die eindeutige Flussspezifikation `id`, die erforderlich ist, um einen neuen Datenfluss zu erstellen.

Um sicherzustellen, dass Sie die richtige Datenflussspezifikation verwenden, überprüfen Sie das `items.sourceConnectionSpecIds`-Array in der Antwort. Bestätigen Sie, dass die Verbindungsspezifikations-ID für Ihre Quelle in dieser Liste enthalten ist.

+++Zum Anzeigen auswählen

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
                "a8b6a1a4-5735-42b4-952c-85dce0ac38b5",
                "6a8d82bc-1caf-45d1-908d-cadabc9d63a6",
                "aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f",
                "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
                "ecde33f2-c56f-46cc-bdea-ad151c16cd69",
                "09182899-b429-40c9-a15a-bf3ddbc8ced7",
                "0479cc14-7651-4354-b233-7480606c2ac3",
                "d6b52d86-f0f8-475f-89d4-ce54c8527328",
                "a8f4d393-1a6b-43f3-931f-91a16ed857f4",
                "fcad62f3-09b0-41d3-be11-449d5a621b69",
                "ea1c2a08-b722-11eb-8529-0242ac130003",
                "35d6c4d8-c9a9-11eb-b8bc-0242ac130003",
                "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
                "2acf109f-9b66-4d5e-bc18-ebb2adcff8d5",
                "2fa8af9c-2d1a-43ea-a253-f00a00c74412",
                "e9d7ec6b-0873-4e57-ad21-b3a7c65e310b"
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
            "runSpec": {
                "name": "ProviderParams",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "description": "defines various params required for creating flow run.",
                    "properties": {
                        "startTime": {
                            "type": "integer",
                            "description": "An integer that defines the start time of the run. The value is represented in Unix epoch time."
                        },
                        "windowStartTime": {
                            "type": "integer",
                            "description": "An integer that defines the start time of the window against which data is to be pulled. The value is represented in Unix epoch time."
                        },
                        "windowEndTime": {
                            "type": "integer",
                            "description": "An integer that defines the end time of the window against which data is to be pulled. The value is represented in Unix epoch time."
                        },
                        "deltaColumn": {
                            "type": "object",
                            "description": "The delta column is required to partition the data and separate newly ingested data from historic data.",
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
                        "startTime",
                        "windowStartTime",
                        "windowEndTime",
                        "deltaColumn"
                    ]
                }
            },
            "attributes": {
                "recordTypeEnabled": true,
                "defaultRecordType": "profile",
                "isSourceFlow": true,
                "flacValidationSupported": true,
                "isDraftModeSupported": true,
                "frequency": "batch",
                "notification": {
                    "category": "sources",
                    "flowRun": {
                        "enabled": true
                    }
                }
            },
            "permissionsInfo": {
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "write"
                        ]
                    }
                ],
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "read"
                        ]
                    }
                ]
            }
        }
    ]
}
```

+++

## Erstellen eines Datenflusses {#dataflow}

Ein Datenfluss ist eine konfigurierte Pipeline, die Daten über Experience Platform-Services hinweg überträgt. Sie definiert, wie Daten aus externen Quellen (z. B. Datenbanken, Cloud-Speicher oder APIs) aufgenommen, verarbeitet und an Zieldatensätze weitergeleitet werden. Diese Datensätze werden dann von Services wie Identity Service, Echtzeit-Kundenprofil und Zielen für die Aktivierung und Analyse verwendet.

Um einen Datenfluss zu erstellen, müssen Sie Werte für die folgenden Elemente angeben:

* [Quellverbindungs-ID](#source)
* [Zielverbindungs-ID](#target)
* [Zuordnungs-ID](#mapping)
* [Datenflussspezifikations-ID](#flow-specs)

In diesem Schritt können Sie die folgenden Parameter in `scheduleParams` verwenden, um einen Aufnahmezeitplan für Ihren Datenfluss zu konfigurieren:

| Zeitplanparameter | Beschreibung |
| --- | --- |
| `startTime` | Die Epochenzeit (in Sekunden), zu der der Datenfluss starten soll. |
| `frequency` | Die Häufigkeit der Aufnahme. Konfigurieren Sie die Häufigkeit , um anzugeben, wie oft der Datenfluss ausgeführt werden soll. Sie können Ihre Häufigkeit auf Folgendes festlegen: <ul><li>`once`: Legen Sie für die Häufigkeit `once` fest, um eine einmalige Aufnahme zu erstellen. Die Einstellungen für Intervall und Aufstockung sind für einmalige Aufnahmeaufträge nicht verfügbar. Standardmäßig ist die Zeitplanfrequenz auf einmal festgelegt.</li><li>`minute`: Legen Sie für die Häufigkeit `minute` fest, um Ihren Datenfluss so zu planen, dass Daten pro Minute aufgenommen werden.</li><li>`hour`: Legen Sie für die Häufigkeit `hour` fest, um Ihren Datenfluss zu planen und Daten stündlich aufzunehmen.</li><li>`day`: Legen Sie für Ihre Häufigkeit `day` fest, um Ihren Datenfluss zu planen und Daten täglich aufzunehmen.</li><li>`week`: Legen Sie für die Häufigkeit `week` fest, um Ihren Datenfluss so zu planen, dass Daten wöchentlich aufgenommen werden.</li></ul> |
| `interval` | Das Intervall zwischen aufeinander folgenden Aufnahmen (erforderlich für alle Häufigkeiten außer `once`). Konfigurieren Sie die Intervalleinstellung, um den Zeitrahmen zwischen jeder Aufnahme festzulegen. Wenn Ihre Häufigkeit beispielsweise auf „Tag“ und das Intervall auf 15 eingestellt ist, wird der Datenfluss alle 15 Tage ausgeführt. Das Intervall kann nicht auf null festgelegt werden. Der akzeptierte Mindestintervallwert für jede Häufigkeit ist wie folgt:<ul><li>`once`: Nicht zutreffend</li><li>`minute`: 15</li><li>`hour`: 1</li><li>`day`: 1</li><li>`week`: 1</li></ul> |
| `backfill` | Gibt an, ob historische Daten vor dem `startTime` aufgenommen werden sollen. |

{style="table-layout:auto"}


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
      "name": "ACME Contact Dataflow",
      "description": "A dataflow for ACME contact data",
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
                  "mappingId": "93ddfa69c4864d978832b1e5ef6ec3b9",
                  "mappingVersion": 0
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
| --- | --- |
| `name` | Ein beschreibender Name für Ihren Datenfluss. Verwenden Sie einen klaren und eindeutigen Namen, um die Identifizierung und Verwaltung Ihres Datenflusses in zukünftigen Vorgängen zu erleichtern. |
| `description` | Eine optionale Beschreibung, die Sie hinzufügen können, um zusätzliche Informationen für Ihren Datenfluss bereitzustellen. |
| `flowSpec.id` | Die ID der Flussspezifikation, die Ihrer Quelle entspricht. |
| `sourceConnectionIds` | Die Quellverbindungs-ID , die in einem früheren Schritt generiert wurde. |
| `targetConnectionIds` | Die ID der Zielverbindung , die in einem früheren Schritt generiert wurde. |
| `transformations.params.deltaColum` | Die Spalte, die verwendet wird, um zwischen neuen und vorhandenen Daten zu unterscheiden. Inkrementelle Daten werden basierend auf dem Zeitstempel der ausgewählten Spalte aufgenommen. Für `deltaColumn` wird das Format `yyyy-MM-dd HH:mm:ss` unterstützt. [!DNL Microsoft Dynamics] wird für `deltaColumn` das Format `yyyy-MM-ddTHH:mm:ssZ`. |
| `transformations.params.deltaColumn.dateFormat` | Das Datumsformat, das für die Delta-Spalte verwendet werden soll. |
| `transformations.params.deltaColumn.timeZone` | Die Zeitzone, die bei der Interpretation der Werte in der Delta-Spalte verwendet werden soll. |
| `transformations.params.mappingId` | Die Zuordnungs-ID , die in einem früheren Schritt generiert wurde. |
| `scheduleParams.startTime` | Die Startzeit für den Datenfluss in Epochenzeit (Sekunden seit Unix-Epoche). Bestimmt, wann der Datenfluss seine erste Ausführung startet. |
| `scheduleParams.frequency` | Die Häufigkeit, mit der der Datenfluss ausgeführt wird. Zulässige Werte sind: `once`, `minute`, `hour`, `day` oder `week`. |
| `scheduleParams.interval` | Das Intervall zwischen aufeinander folgenden Datenflussausführungen, basierend auf der ausgewählten Häufigkeit. Muss eine Ganzzahl ungleich null sein. Wenn Ihre Häufigkeit beispielsweise auf Minute und das Intervall 15 beträgt, wird der Datenfluss alle 15 Minuten ausgeführt. |
| `scheduleParams.backfill` | Ein boolescher Wert (`true` oder `false`), der bestimmt, ob historische Daten (Aufstockung) aufgenommen werden, wenn der Datenfluss zum ersten Mal erstellt wird. |

{style="table-layout:auto"}

**Antwort**

Bei einer erfolgreichen Antwort wird die ID (`id`) des neu erstellten Datenflusses angegeben.

```json
{
    "id": "ae0a9777-b322-4ac1-b0ed-48ae9e497c7e",
    "etag": "\"770029f8-0000-0200-0000-6019e7d40000\""
}
```

### Validieren des API-Workflows über die Benutzeroberfläche {#validate-in-ui}

Sie können die Experience Platform-Benutzeroberfläche verwenden, um die Erstellung Ihres Datenflusses zu überprüfen. Navigieren Sie zum *[!UICONTROL Quellen]*-Katalog in der Experience Platform-Benutzeroberfläche und wählen Sie **[!UICONTROL Datenflüsse]** in der Kopfzeile aus. Verwenden Sie anschließend die Spalte [!UICONTROL Datenflussname] und suchen Sie den Datenfluss, den Sie mithilfe der [!DNL Flow Service]-API erstellt haben.

![Die Datenflussschnittstelle des Arbeitsbereichs „Quellen“ in der Experience Platform-Benutzeroberfläche](../../../images/tutorials/validations/dataflows-interface.png)

Sie können Ihren Datenfluss außerdem über die Schnittstelle [!UICONTROL Datenflussaktivität] überprüfen. Verwenden Sie die rechte Leiste, um die [!UICONTROL API-Nutzung] Informationen Ihres Datenflusses anzuzeigen. In diesem Abschnitt werden dieselbe Datenfluss-ID, Datensatz-ID und Zuordnungs-ID angezeigt, die während des Erstellungsprozesses eines Datenflusses in [!DNL Flow Service] generiert wurde.

![Die Datenflussansichtsseite des Arbeitsbereichs „Quellen“.](../../../images/tutorials/validations/api-usage.png)

## Nächste Schritte

Dieses Tutorial führte Sie durch den Prozess zum Erstellen eines Datenflusses in Experience Platform mithilfe der [!DNL Flow Service]-API. Sie haben gelernt, wie Sie die erforderlichen Komponenten erstellen und konfigurieren, einschließlich des XDM-Zielschemas, des Datensatzes, der Quellverbindung, der Zielverbindung und des Datenflusses selbst. Wenn Sie diese Schritte ausführen, können Sie die Aufnahme von Daten aus externen Quellen in Experience Platform automatisieren, sodass nachgelagerte Services wie Echtzeit-Kundenprofil und Ziele Ihre aufgenommenen Daten für erweiterte Anwendungsfälle nutzen können.

### Überwachen Ihres Datenflusses

Nachdem Ihr Datenfluss erstellt wurde, können Sie dessen Leistung direkt in der Experience Platform-Benutzeroberfläche überwachen. Dazu gehören das Tracking von Aufnahmeraten, Erfolgsmetriken und eventuell auftretenden Fehlern. Weitere Informationen zum Überwachen von Datenflüssen finden Sie im Tutorial [Überwachen von Konten und Datenflüssen](../../../../dataflows/ui/monitor-sources.md).

### Aktualisieren des Datenflusses

Um Konfigurationen für die Planung, Zuordnung oder allgemeine Informationen Ihrer Datenflüsse zu aktualisieren, besuchen Sie das Tutorial [Aktualisieren von Quelldatenflüssen](../../api/update-dataflows.md).

## Löschen des Datenflusses

Datenflüsse, die nicht mehr erforderlich sind oder nicht korrekt erstellt wurden, können Sie löschen, indem Sie dazu die Funktion **[!UICONTROL Löschen]** im Arbeitsbereich **[!UICONTROL Datenflüsse]** verwenden. Weitere Informationen zum Löschen von Datenflüssen finden Sie im Tutorial [Löschen von Datenflüssen](../../api/delete.md).
