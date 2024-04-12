---
keywords: Experience Platform;Startseite;beliebte Themen;Protokolldaten erfassen;Protokolldaten
solution: Experience Platform
title: Erstellen eines Datenflusses für Protokollquellen mithilfe der Flow Service-API
type: Tutorial
description: In diesem Tutorial werden die Schritte zum Abrufen von Daten aus einem Protokollprogramm und deren Aufnahme in Platform mithilfe von Quell-Connectoren und APIs beschrieben.
exl-id: e14e75c2-2a93-45d8-8056-f06075bd4b8d
source-git-commit: f5ac10980e08843f6ed9e892f7e1d4aefc8f0de7
workflow-type: tm+mt
source-wordcount: '1314'
ht-degree: 91%

---

# Erstellen eines Datenflusses für Protokollquellen mithilfe der [!DNL Flow Service]-API

In diesem Tutorial werden die Schritte zum Abrufen von Daten aus einer Protokollquelle und zum Übertragen dieser Daten auf Platform mithilfe der [[!DNL Flow Service] -API](https://www.adobe.io/experience-platform-apis/references/flow-service/) behandelt.

>[!NOTE]
>
>* Um einen Datenfluss zu erstellen, müssen Sie bereits über eine gültige Basis-Verbindungs-ID mit einer Protokollquelle verfügen. Wenn Sie diese ID nicht haben, sehen Sie sich die [Quellen - Übersicht](../../../home.md#protocols) für eine Liste von Protokollquellen, mit denen Sie eine Basisverbindung erstellen können.

## Erste Schritte

Dieses Tutorial setzt außerdem ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten ordnet.
   * [Grundlagen der Schemakomposition](../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemakomposition.
   * [Entwicklerhandbuch zur Schema Registry](../../../../xdm/api/getting-started.md): Enthält wichtige Informationen, die Sie benötigen, um die Schema Registry API erfolgreich aufrufen zu können. Diese umfassen Ihre `{TENANT_ID}`, das Konzept sogenannter „Container“ und die für Anfragen erforderlichen Kopfzeilen, von denen insbesondere die Accept-Kopfzeile und deren mögliche Werte wichtig sind.
* [[!DNL Catalog Service]](../../../../catalog/home.md): Der Katalog ist das „System of Record“ für den Speicherort und die Herkunft von Daten in Experience Platform.
* [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md): Mit der Batch-Aufnahme-API können Sie Daten in Form von Batch-Dateien in Experience Platform aufnehmen.
* [Sandboxes](../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Verwenden von Platform-APIs

Informationen darüber, wie Sie Platform-APIs erfolgreich aufrufen können, finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../landing/api-guide.md).

## Erstellen einer Quellverbindung {#source}

Sie können eine Quellverbindung herstellen, indem Sie eine POST-Anfrage an die [!DNL Flow Service]-API senden. Eine Quellverbindung besteht aus einer Verbindungs-ID, einem Pfad zur Quelldatendatei und einer Verbindungsspezifikations-ID.

Um eine Quellverbindung zu erstellen, müssen Sie auch einen Aufzählungswert für das Datenformat-Attribut definieren.

Verwenden Sie die folgenden Aufzählungswerte für dateibasierte Connectoren:

| Datenformat | Aufzählungswert |
| ----------- | ---------- |
| Durch Trennzeichen getrennt | `delimited` |
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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Generic OData source connection",
        "baseConnectionId": "a5c6b647-e784-4b58-86b6-47e784ab580b",
        "description": "Generic OData source connection",
        "data": {
            "format": "tabular",
        },
        "params": {
            "tableName": "Orders",
            "columns": [
                {
                "name": "OrderID",
                "type": "integer",
                "xdm": {
                    "type": "integer",
                    "minimum": -2147483648,
                    "maximum": 2147483647
                }
                },
                {
                    "name": "CustomerID",
                    "type": "string",
                    "xdm": {
                        "type": "string"
                    }
                },
                {
                    "name": "OrderDate",
                    "type": "string",
                    "meta:xdmType": "date-time",
                    "xdm": {
                        "type": "string",
                        "format": "date-time"
                    }
                },
                {
                    "name": "ShippedDate",
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
            "id": "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `baseConnectionId` | Die Verbindungs-ID Ihres Protokollprogramms |
| `params.path` | Der Pfad der Quelldatei. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID Ihres Protokollprogramms. |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Quellverbindung zurück. Diese ID ist in späteren Schritten zum Erstellen einer Zielverbindung erforderlich.

```json
{
    "id": "0a768941-ddfb-499d-b689-41ddfbf99db0",
    "etag": "\"8f00753e-0000-0200-0000-5e8a547d0000\""
}
```

## Erstellen eines XDM-Zielschemas {#target-schema}

Damit die Quelldaten in Platform verwendet werden können, muss ein Zielschema erstellt werden, das die Quelldaten entsprechend Ihren Anforderungen strukturiert. Das Zielschema wird dann verwendet, um einen Platform-Datensatz zu erstellen, in dem die Quelldaten enthalten sind.

Ein Ziel-XDM-Schema kann erstellt werden, indem eine POST-Anfrage an die [Schema-Registrierungs-API](https://www.adobe.io/experience-platform-apis/references/schema-registry/) durchgeführt wird.

Ausführliche Schritte zum Erstellen eines XDM-Zielschemas finden Sie im Tutorial zum [Erstellen eines Schemas mithilfe der API](../../../../xdm/api/schemas.md).

## Erstellen eines Zieldatensatzes {#target-dataset}

Ein Zieldatensatz kann erstellt werden, indem eine POST-Anfrage an die [Catalog Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) durchgeführt wird, wodurch die ID des Zielschemas in der Payload angegeben wird.

Ausführliche Anweisungen zum Erstellen eines Zieldatensatzes finden Sie im Tutorial zu [Erstellen eines Datensatzes mithilfe der API](../../../../catalog/api/create-dataset.md).

## Erstellen einer Zielverbindung {#target-connection}

Eine Zielverbindung stellt die Verbindung zum Ziel dar, in das die aufgenommenen Daten übernommen werden. Um eine Zielverbindung zu erstellen, müssen Sie die festgelegte Verbindungsspezifikations-ID angeben, die dem Data Lake zugeordnet ist. Diese Verbindungsspezifikations-ID lautet: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Sie verfügen jetzt über die eindeutigen Kennungen, ein Zielschema, einen Zieldatensatz und die Verbindungsspezifikations-ID zum Data Lake. Mit der [!DNL Flow Service]-API können Sie eine Zielverbindung erstellen, indem Sie diese Bezeichner zusammen mit dem Datensatz angeben, der die eingehenden Quelldaten enthalten soll.

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
        "name": "Target Connection for protocols",
        "description": "Target Connection for protocols",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e669d7aba5a02f294fafb7b269af25f7cd4a66ce59193545",
                "version" "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5e8a55ca53662c18af37a83a"
        },
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `data.schema.id` | Die `$id` des XDM-Zielschemas. |
| `params.dataSetId` | Die Kennung des im vorherigen Schritt generierten Zieldatensatzes. **Hinweis**: Sie müssen beim Erstellen einer Zielverbindung eine gültige Datensatz-ID angeben. Eine ungültige Datensatz-ID führt zu einem Fehler. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID, die für die Verbindung mit dem Data Lake verwendet wird. Diese ID lautet: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung der neuen Zielverbindung (`id`) zurück. Dieser Wert ist in einem späteren Schritt zum Erstellen eines Datenflusses erforderlich.

```json
{
    "id": "576d5ecf-f114-4587-ad5e-cff1144587f4",
    "etag": "\"13013506-0000-0200-0000-5e8a56d80000\""
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
    'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/e669d7aba5a02f294fafb7b269af25f7cd4a66ce59193545",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "OrderID",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "CustomerID",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "EmployeeID",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "createdByBatchID",
                "sourceAttribute": "OrderDate",
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
    "id": "37409d3017e24a3eb4a2dc21020f7a5b",
    "version": 0,
    "createdDate": 1586124873209,
    "modifiedDate": 1586124873209,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Nachschlagen von Datenflussspezifikationen {#specs}

Ein Datenfluss sorgt für die Erfassung von Daten aus Quellen und deren Aufnahme in Platform. Um einen Datenfluss zu erstellen, müssen Sie zunächst die Datenflussspezifikationen abrufen, die für die Datenerfassung aus Ihrem Protokollprogramm zuständig sind.

**API-Format**

```http
GET /flowSpecs?property=name=="CRMToAEP"
```

**Anfrage**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name=="CRMToAEP"' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort werden die Details der Datenflussspezifikation zurückgegeben, die für die Übermittlung von Daten aus Ihrer Quelle an Platform sorgt. Die Antwort enthält die eindeutige Flussspezifikation `id`, die erforderlich ist, um einen neuen Datenfluss zu erstellen.

>[!NOTE]
>
>Die nachstehende JSON-Antwort-Payload wird für die Kürze ausgeblendet. Wählen Sie &quot;payload&quot;aus, um die Antwort-Payload anzuzeigen.

+++ Anzeigen der Payload

```json
{
  "id": "14518937-270c-4525-bdec-c2ba7cce3860",
  "name": "CRMToAEP",
  "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
  "version": "1.0",
  "attributes": {
    "isSourceFlow": true,
    "flacValidationSupported": true,
    "frequency": "batch",
    "notification": {
      "category": "sources",
      "flowRun": {
        "enabled": true
      }
    }
  },
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
    "1fe283f6-9bec-11ea-bb37-0242ac130002",
    "fcad62f3-09b0-41d3-be11-449d5a621b69",
    "ea1c2a08-b722-11eb-8529-0242ac130003",
    "35d6c4d8-c9a9-11eb-b8bc-0242ac130003",
    "ff4274f2-c9a9-11eb-b8bc-0242ac130003",
    "ba5126ec-c9ac-11eb-b8bc-0242ac130003",
    "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
    "929e4450-0237-4ed2-9404-b7e1e0a00309",
    "2acf109f-9b66-4d5e-bc18-ebb2adcff8d5",
    "2fa8af9c-2d1a-43ea-a253-f00a00c74412"
  ],
  "targetConnectionSpecIds": [
    "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
  ],
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
  },
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
  "transformationSpec": [
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
    }
}
```

+++

## Erstellen eines Datenflusses

Der letzte Schritt bei der Datenerfassung besteht darin, einen Datenfluss zu erstellen. An dieser Stelle sollten die folgenden erforderlichen Werte bereits vorhanden sein:

* [Quellverbindungs-ID](#source)
* [Zielverbindungs-ID](#target)
* [Zuordnungs-ID](#mapping)
* [Datenflussspezifikations-ID](#specs)

Ein Datenfluss ist für die Planung und Erfassung von Daten aus einer Quelle verantwortlich. Sie können einen Datenfluss erstellen, indem Sie eine POST-Anfrage ausführen und dabei die oben genannten Werte in der Payload angeben.

Um eine Aufnahme zu planen, legen Sie zunächst den Startzeitwert auf die Epochenzeit in Sekunden fest. Anschließend müssen Sie den Frequenzwert auf eine der fünf Optionen festlegen: `once`, `minute`, `hour`, `day` oder `week`. Der Intervallwert gibt den Zeitraum zwischen zwei aufeinanderfolgenden Aufnahmen an. Bei der Erstellung einer einmaligen Aufnahme ist kein Intervall erforderlich. Für alle anderen Frequenzen muss der Intervallwert auf gleich oder größer als `15` festgelegt werden.

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
        "name": "Creating a dataflow for a protocols source",
        "description": "Creating a dataflow for a protocols source",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "0a768941-ddfb-499d-b689-41ddfbf99db0"
        ],
        "targetConnectionIds": [
            "576d5ecf-f114-4587-ad5e-cff1144587f4"
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
                    "mappingId": "7409d3017e24a3eb4a2dc21020f7a5b",
                    "mappingVersion": 0
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
| `flowSpec.id` | Die [Flussspezifikations-ID](#specs), die im vorherigen Schritt abgerufen wurde. |
| `sourceConnectionIds` | Die [Quellverbindungs-ID](#source), die in einem früheren Schritt abgerufen wurde. |
| `targetConnectionIds` | Die [Zielverbindungs-ID](#target-connection), die in einem früheren Schritt abgerufen wurde. |
| `transformations.params.mappingId` | Die [Zuordnungs-ID](#mapping), die in einem früheren Schritt abgerufen wurde. |
| `transformations.params.deltaColum` | Die Spalte, die verwendet wird, um zwischen neuen und vorhandenen Daten zu unterscheiden. Inkrementelle Daten werden basierend auf dem Zeitstempel der ausgewählten Spalte aufgenommen. Das unterstützte Format für `deltaColumn` bei Verwendung von generischen OData ist `yyyy-MM-ddTHH:mm:ssZ`. |
| `transformations.params.mappingId` | Die mit Ihrer Datenbank verknüpfte Zuordnungs-ID. |
| `scheduleParams.startTime` | Die Startzeit für den Datenfluss in Epochenzeit. |
| `scheduleParams.frequency` | Die Häufigkeit, mit der der Datenfluss Daten erfasst. Zulässige Werte sind: `once`, `minute`, `hour`, `day` oder `week`. |
| `scheduleParams.interval` | Das Intervall bezeichnet den Zeitraum zwischen zwei aufeinanderfolgenden Datenflussausführungen. Der Wert des Intervalls sollte eine Ganzzahl ungleich null sein. Das Intervall ist nicht erforderlich, wenn die Häufigkeit auf `once` festgelegt ist, und sollte größer oder gleich `15` für andere Frequenzwerte sein. |

**Antwort**

Bei einer erfolgreichen Antwort wird die ID `id` des neu erstellten Datenflusses zurückgegeben.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "\"04004fe9-0000-0200-0000-5ebc4c8b0000\""
}
```

## Überwachen Ihres Datenflusses

Nachdem Ihr Datenfluss erstellt wurde, können Sie die Datenaufnahme überwachen, um Informationen über die Datenflussausführungen, den Abschlussstatus und Fehler anzuzeigen. Weitere Informationen zum Überwachen von Datenflüssen finden Sie im Tutorial [Überwachen von Datenflüssen in der API](../monitor.md)

## Nächste Schritte

In diesem Tutorial haben Sie einen Quell-Connector erstellt, um Daten aus einem Protokollprogramm nach einem Plan zu erfassen. Eingehende Daten können jetzt von nachgelagerten Platform-Services wie [!DNL Real-Time Customer Profile] und [!DNL Data Science Workspace] verwendet werden. Weiterführende Informationen finden Sie in folgenden Dokumenten:

* [Übersicht zum Echtzeit-Kundenprofil](../../../../profile/home.md)
* [Übersicht über Data Science Workspace](../../../../data-science-workspace/home.md)
