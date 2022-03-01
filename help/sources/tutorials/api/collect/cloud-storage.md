---
keywords: Experience Platform; Startseite; beliebte Themen; Cloud-Speicher-Daten
solution: Experience Platform
title: Erstellen eines Datenflusses für Cloud Storage-Quellen mithilfe der Flow Service-API
topic-legacy: overview
type: Tutorial
description: In diesem Tutorial werden die Schritte zum Abrufen von Daten aus einem Drittanbieter-Cloud-Speicher und zum Einbringen dieser Daten in Platform mithilfe von Quell-Connectoren und APIs beschrieben.
exl-id: 95373c25-24f6-4905-ae6c-5000bf493e6f
source-git-commit: 67e6de74ea8f2f4868a39ec1907ee1cac335c9f0
workflow-type: tm+mt
source-wordcount: '1575'
ht-degree: 10%

---

# Erstellen Sie einen Datenfluss für Cloud-Speicher-Quellen mit dem [!DNL Flow Service] API

In diesem Tutorial werden die Schritte zum Abrufen von Daten aus einer Cloud-Speicherquelle und zum Übertragen dieser Daten auf Platform mithilfe von [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>Um einen Datenfluss zu erstellen, müssen Sie bereits über eine gültige Basis-Verbindungs-ID mit einer der folgenden Cloud-Speicherquellen in Platform verfügen:<ul><li>[[!DNL Amazon S3]](../create/cloud-storage/s3.md)</li><li>[[!DNL Apache HDFS]](../create/cloud-storage/hdfs.md)</li><li>[[!DNL Azure Blob]](../create/cloud-storage/blob.md)</li><li>[[!DNL Azure Data Lake Storage Gen2]](../create/cloud-storage/adls-gen2.md)</li><li>[[!DNL Azure File Storage]](../create/cloud-storage/azure-file-storage.md)</li><li>[[!DNL FTP]](../create/cloud-storage/ftp.md)</li><li>[[!DNL Google Cloud Storage]](../create/cloud-storage/google.md)</li><li>[[!DNL Oracle Object Storage]](../create/cloud-storage/oracle-object-storage.md)</li><li>[[!DNL SFTP]](../create/cloud-storage/sftp.md)</li></ul>

## Erste Schritte

Für dieses Tutorial benötigen Sie ein Verständnis der folgenden Komponenten von Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   - [Grundlagen der Schemakomposition](../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   - [Entwicklerhandbuch zur Schema Registry](../../../../xdm/api/getting-started.md): Enthält wichtige Informationen, die Sie benötigen, um die Schema Registry-API erfolgreich aufrufen zu können. Diese umfassen Ihre `{TENANT_ID}`, das Konzept sogenannter „Container“ und die für Anfragen erforderlichen Kopfzeilen, von denen insbesondere die Accept-Kopfzeile und deren mögliche Werte wichtig sind.
- [[!DNL Catalog Service]](../../../../catalog/home.md): Catalog ist „System of Record“ für die Position und Herkunft von Daten in Experience Platform.
- [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md): Mit der Batch-Aufnahme-API können Sie Daten als Batch-Dateien in Experience Platform erfassen.
- [Sandboxes](../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Verwenden von Platform-APIs

Informationen zum erfolgreichen Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../landing/api-guide.md).

## Quellverbindung erstellen {#source}

Sie können eine Quellverbindung erstellen, indem Sie eine POST-Anfrage an die [!DNL Flow Service] API. Eine Quellverbindung besteht aus einer Verbindungs-ID, einem Pfad zur Quelldatendatei und einer Verbindungsspezifikations-ID.

Um eine Quellverbindung zu erstellen, müssen Sie auch einen Enum-Wert für das Datenformat-Attribut definieren.

Verwenden Sie die folgenden Enum-Werte für dateibasierte Quellen:

| Datenformat | Enum-Wert |
| ----------- | ---------- |
| Getrennt | `delimited` |
| JSON | `json` |
| Parquet | `parquet` |

Setzen Sie für alle tabellenbasierten Quellen den Wert auf `tabular`.

- [Erstellen einer Quellverbindung mit benutzerdefinierten getrennten Dateien](#using-custom-delimited-files)
- [Erstellen einer Quellverbindung mit komprimierten Dateien](#using-compressed-files)

**API-Format**

```http
POST /sourceConnections
```

### Erstellen einer Quellverbindung mit benutzerdefinierten getrennten Dateien {#using-custom-delimited-files}

**Anfrage**

Sie können eine durch Trennzeichen getrennte Datei mit einem benutzerdefinierten Trennzeichen aufnehmen, indem Sie eine `columnDelimiter` als Eigenschaft. Jeder einzelne Zeichenwert ist ein zulässiges Spaltentrennzeichen. Wenn kein Komma angegeben wird `(,)` wird als Standardwert verwendet.

Die folgende Beispielanfrage erstellt eine Quellverbindung für einen durch Trennzeichen getrennten Dateityp mit tabulatorgetrennten Werten.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Cloud storage source connection for delimited files",
        "description": "Cloud storage source connector",
        "baseConnectionId": "9e2541a0-b143-4d23-a541-a0b143dd2301",
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
| `baseConnectionId` | Die eindeutige Verbindungs-ID des Cloud-Speichersystems eines Drittanbieters, auf das Sie zugreifen. |
| `data.format` | Ein enum -Wert, der das Datenformatattribut definiert. |
| `data.columnDelimiter` | Sie können ein beliebiges Spaltentrennzeichen für einzelne Zeichen verwenden, um flache Dateien zu sammeln. Diese Eigenschaft ist nur bei der Aufnahme von CSV- oder TSV-Dateien erforderlich. |
| `params.path` | Der Pfad der Quelldatei, auf die Sie zugreifen. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID, die mit Ihrem spezifischen Cloud-Speichersystem von Drittanbietern verknüpft ist. Siehe [Anhang](#appendix) für eine Liste der Verbindungsspezifikations-IDs. |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Quellverbindung. Diese ID ist in einem späteren Schritt erforderlich, um einen Datenfluss zu erstellen.

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

### Erstellen einer Quellverbindung mit komprimierten Dateien {#using-compressed-files}

**Anfrage**

Sie können auch komprimierte JSON- oder durch Trennzeichen getrennte Dateien erfassen, indem Sie deren `compressionType` als Eigenschaft. Die Liste der unterstützten komprimierten Dateitypen lautet:

- `bzip2`
- `gzip`
- `deflate`
- `zipDeflate`
- `tarGzip`
- `tar`

Die folgende Beispielanfrage erstellt eine Quellverbindung für eine komprimierte, durch Trennzeichen getrennte Datei mithilfe einer `gzip` Dateityp.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Cloud storage source connection for compressed files",
        "description": "Cloud storage source connection for compressed files",
        "baseConnectionId": "9e2541a0-b143-4d23-a541-a0b143dd2301",
        "data": {
            "format": "delimited",
            "properties": {
                "compressionType": "gzip"
            }
        },
        "params": {
            "path": "/compressed/files.gzip"
        },
        "connectionSpec": {
            "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
            "version": "1.0"
        }
     }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `data.properties.compressionType` | Bestimmt den komprimierten Dateityp für die Erfassung. Diese Eigenschaft ist nur erforderlich, wenn komprimierte JSON- oder durch Trennzeichen getrennte Dateien aufgenommen werden. |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Quellverbindung. Diese ID ist in einem späteren Schritt erforderlich, um einen Datenfluss zu erstellen.

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

## Erstellen eines XDM-Zielschemas {#target-schema}

Damit die Quelldaten in Platform verwendet werden können, muss ein Zielschema erstellt werden, das die Quelldaten entsprechend Ihren Anforderungen strukturiert. Das Zielschema wird dann verwendet, um einen Platform-Datensatz zu erstellen, in dem die Quelldaten enthalten sind.

Ein Ziel-XDM-Schema kann erstellt werden, indem eine POST-Anfrage an die [Schema Registry-API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

Ausführliche Anweisungen zum Erstellen eines XDM-Zielschemas finden Sie im Tutorial zu [Erstellen eines Schemas mithilfe der API](../../../../xdm/api/schemas.md).

## Zieldatensatz erstellen {#target-dataset}

Ein Zieldatensatz kann erstellt werden, indem eine POST-Anfrage an die [Catalog Service-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), wodurch die ID des Zielschemas in der Payload angegeben wird.

Ausführliche Anweisungen zum Erstellen eines Zieldatensatzes finden Sie im Tutorial zu [Erstellen eines Datensatzes mithilfe der API](../../../../catalog/api/create-dataset.md).

## Erstellen einer Zielverbindung {#target-connection}

Eine Zielverbindung stellt die Verbindung zum Ziel dar, in dem die aufgenommenen Daten landen. Um eine Zielverbindung zu erstellen, müssen Sie die feste Verbindungsspezifikations-ID angeben, die dem Data Lake zugeordnet ist. Diese Verbindungsspezifikations-ID lautet: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Sie verfügen jetzt über die eindeutigen Kennungen eines Zielschemas, eines Zieldatensatzes und der Verbindungsspezifikations-ID zum Data Lake. Mithilfe dieser Kennungen können Sie mithilfe der [!DNL Flow Service] API zum Angeben des Datensatzes, der die eingehenden Quelldaten enthält.

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
                "version": "application/vnd.adobe.xed-full+json;version=1"
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
| `data.schema.id` | Die `$id` des Ziel-XDM-Schemas. |
| `data.schema.version` | Die Version des Schemas. Dieser Wert muss festgelegt werden `application/vnd.adobe.xed-full+json;version=1`, die die neueste Nebenversion des Schemas zurückgibt. |
| `params.dataSetId` | Die ID des Zieldatensatzes. |
| `connectionSpec.id` | Die feste Verbindungsspezifikations-ID zum Data Lake. Diese ID lautet: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung der neuen Zielverbindung (`id`). Diese ID ist in späteren Schritten erforderlich.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Erstellen einer Zuordnung {#mapping}

Damit die Quelldaten in einen Zieldatensatz aufgenommen werden können, müssen sie zunächst dem Zielschema zugeordnet werden, dem der Zieldatensatz entspricht.

Um einen Zuordnungssatz zu erstellen, stellen Sie eine POST-Anfrage an die `mappingSets` Endpunkt der [[!DNL Data Prep] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-prep.yaml) beim Bereitstellen des Ziel-XDM-Schemas `$id` und die Details der Zuordnungssätze, die Sie erstellen möchten.

>[!TIP]
>
>Mithilfe eines Cloud-Speicher-Quell-Connectors können Sie komplexe Datentypen wie Arrays in JSON-Dateien zuordnen.

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
| `xdmSchema` | Die ID des Ziel-XDM-Schemas. |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Zuordnung zurück, einschließlich der eindeutigen Kennung (`id`). Dieser Wert ist in einem späteren Schritt zum Erstellen eines Datenflusses erforderlich.

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

## Datenflussspezifikationen abrufen {#specs}

Ein Datenfluss ist für die Erfassung von Daten aus Quellen und deren Aufnahme in Platform zuständig. Um einen Datenfluss zu erstellen, müssen Sie zunächst die Datenflussspezifikationen abrufen, die für die Erfassung von Cloud-Speicherdaten zuständig sind.

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

Bei einer erfolgreichen Antwort werden die Details der Datenflug-Spezifikation zurückgegeben, die für die Übermittlung von Daten aus Ihrer Quelle an Platform zuständig ist. Die Antwort enthält die eindeutige Flussspezifikation `id` erforderlich, um einen neuen Datenfluss zu erstellen.

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

Der letzte Schritt bei der Erfassung von Cloud-Speicherdaten besteht darin, einen Datenfluss zu erstellen. Jetzt sind die folgenden erforderlichen Werte vorbereitet:

- [Quellverbindungs-ID](#source)
- [Target-Verbindungs-ID](#target)
- [Mapping-ID](#mapping)
- [Dataflow-Spezifikations-ID](#specs)

Ein Datenfluss ist für die Planung und Erfassung von Daten aus einer Quelle verantwortlich. Sie können einen Datenfluss erstellen, indem Sie eine POST-Anfrage ausführen und dabei die oben genannten Werte in der Payload angeben.

>[!NOTE]
>
>Bei der Batch-Erfassung wählt jeder darauf folgende Datenfluss Dateien aus, die basierend auf ihren **letzte Änderung** Zeitstempel. Das bedeutet, dass Batch-Datenflüsse ausgewählte Dateien aus der Quelle verwenden, die neu sind oder seit der letzten Ausführung des Datenflusses geändert wurden.

Um eine Aufnahme zu planen, müssen Sie zunächst den Startzeitwert auf Epochenzeit in Sekunden festlegen. Anschließend müssen Sie den Frequenzwert auf eine der fünf Optionen festlegen: `once`, `minute`, `hour`, `day`oder `week`. Der Intervallwert gibt den Zeitraum zwischen zwei aufeinander folgenden Aufnahmen an und bei der Erstellung einer einmaligen Aufnahme ist kein Intervall erforderlich. Für alle anderen Frequenzen muss der Intervallwert auf gleich oder größer als `15`.

>[!IMPORTANT]
>
>Es wird dringend empfohlen, Ihren Datenfluss für die einmalige Erfassung zu planen, wenn Sie die [FTP-Connector](../../../connectors/cloud-storage/ftp.md).

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
| `flowSpec.id` | Die [Flussspezifikations-ID](#specs) im vorherigen Schritt abgerufen werden. |
| `sourceConnectionIds` | Die [Quell-Verbindungs-ID](#source) in einem früheren Schritt abgerufen. |
| `targetConnectionIds` | Die [Ziel-Verbindungs-ID](#target-connection) in einem früheren Schritt abgerufen. |
| `transformations.params.mappingId` | Die [Zuordnungs-ID](#mapping) in einem früheren Schritt abgerufen. |
| `scheduleParams.startTime` | Die Startzeit für den Datenfluss in Epochenzeit. |
| `scheduleParams.frequency` | Die Häufigkeit, mit der der Datenfluss Daten erfasst. Zulässige Werte sind: `once`, `minute`, `hour`, `day`oder `week`. |
| `scheduleParams.interval` | Das Intervall bezeichnet den Zeitraum zwischen zwei aufeinander folgenden Durchsatzausführungen. Der Wert des Intervalls sollte eine Ganzzahl ungleich null sein. Das Intervall ist nicht erforderlich, wenn die Häufigkeit auf `once` und sollte größer oder gleich sein als `15` für andere Frequenzwerte. |

**Antwort**

Eine erfolgreiche Antwort gibt die ID (`id`) des neu erstellten Datenflusses.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Überwachen Ihres Datenflusses

Nachdem Ihr Datenfluss erstellt wurde, können Sie die erfassten Daten überwachen, um Informationen über die Durchsatzausführungen, den Abschlussstatus und Fehler anzuzeigen. Weitere Informationen zum Überwachen von Datenflüssen finden Sie im Tutorial zu [Überwachen von Datenflüssen in der API](../monitor.md)

## Nächste Schritte

In diesem Tutorial haben Sie einen Quell-Connector erstellt, um Daten aus Ihrem Cloud-Speicher planmäßig zu erfassen. Eingehende Daten können jetzt von nachgelagerten Platform-Diensten wie [!DNL Real-time Customer Profile] und [!DNL Data Science Workspace]. Weitere Informationen finden Sie in den folgenden Dokumenten:

- [Übersicht über das Echtzeit-Kundenprofil](../../../../profile/home.md)
- [Data Science Workspace – Übersicht](../../../../data-science-workspace/home.md)

## Anhang {#appendix}

Im folgenden Abschnitt finden Sie die verschiedenen Connectoren für Cloud-Speicher und deren Verbindungsspezifikationen.

### Verbindungsspezifikation

| Connector-Name | Verbindungsspezifikation |
| -------------- | --------------- |
| [!DNL Amazon S3] (S3) | `ecadc60c-7455-4d87-84dc-2a0e293d997b` |
| [!DNL Amazon Kinesis] (Kinesis) | `86043421-563b-46ec-8e6c-e23184711bf6` |
| [!DNL Azure Blob] (Blob) | `4c10e202-c428-4796-9208-5f1f5732b1cf` |
| [!DNL Azure Data Lake Storage Gen2] (ADLS Gen2) | `b3ba5556-48be-44b7-8b85-ff2b69b46dc4` |
| [!DNL Azure Event Hubs] (Ereignis-Hubs) | `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |
| [!DNL Azure File Storage] | `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |
| [!DNL Google Cloud Storage] | `32e8f412-cdf7-464c-9885-78184cb113fd` |
| [!DNL HDFS] | `54e221aa-d342-4707-bcff-7a4bceef0001` |
| [!DNL Oracle Object Storage] | `c85f9425-fb21-426c-ad0b-405e9bd8a46c` |
| [!DNL SFTP] | `bf367b0d-3d9b-4060-b67b-0d3d9bd06094` |
