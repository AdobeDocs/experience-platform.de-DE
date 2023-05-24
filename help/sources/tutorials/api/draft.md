---
title: Erstellen von Entwürfen Ihrer Flow Service-Entitäten-API
description: Erfahren Sie, wie Sie Entwürfe Ihrer Basisverbindung, Quellverbindung, Zielverbindung und Datenfluss mithilfe der Flow Service-API erstellen.
exl-id: aad6a302-1905-4a23-bc3d-39e76c9a22da
source-git-commit: ebd650355a5a4c2a949739384bfd5c8df9577075
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 23%

---

# Erstellen Sie Entwürfe Ihrer [!DNL Flow Service] Entitäten, die die API verwenden

Sie können die `mode=draft` Abfrageparameter im [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>) , um [!DNL Flow Service] -Entitäten, wie z. B. Ihre Basisverbindungen, Quellverbindungen, Zielverbindungen und Datenflüsse zu einem Entwurfsstatus.

Entwürfe können später mit neuen Informationen aktualisiert und dann veröffentlicht werden, sobald sie fertig sind, indem Sie die `op=publish` Abfrageparameter.

In diesem Tutorial erfahren Sie, wie Sie Ihre [!DNL Flow Service] -Entitäten in den Entwurfsstatus versetzt werden, damit Sie Ihre Workflows anhalten und speichern können, um sie zu einem späteren Zeitpunkt abzuschließen.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Verwenden von Platform-APIs

Informationen darüber, wie Sie Platform-APIs erfolgreich aufrufen können, finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../landing/api-guide.md).

### Unterstützung für Entwurfsmodus prüfen

Sie müssen außerdem überprüfen, ob die Verbindungsspezifikations-ID und die entsprechende Flussspezifikations-ID der verwendeten Quelle für den Entwurfsmodus aktiviert sind.

>[!BEGINTABS]

>[!TAB Details zur Verbindungsspezifikation nachschlagen]

+++Anfrage Die folgende Anfrage ruft die Informationen zur Verbindungsspezifikation für ab [!DNL Azure File Storage]:

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/be5ec48c-5b78-49d5-b8fa-7c89ec4569b8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Antwort

Eine erfolgreiche Antwort gibt die Informationen zur Verbindungsspezifikation für Ihre Quelle zurück. Um zu überprüfen, ob der Entwurfsmodus für Ihre Quelle unterstützt wird, überprüfen Sie, ob die `items[0].attributes.isDraftModeSupported` hat den Wert `true`.

```json {line-numbers="true" start-line="1" highlight="252"}
{
    "items": [
        {
            "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
            "name": "azure-file-storage",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "type": "basicAuthentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params",
                        "properties": {
                            "host": {
                                "type": "string",
                                "description": "Specifies the Azure File Storage endpoint."
                            },
                            "userid": {
                                "type": "string",
                                "description": "Specify the user to access the Azure File Storage."
                            },
                            "password": {
                                "type": "string",
                                "description": "Specify the storage access key",
                                "format": "password"
                            }
                        },
                        "required": [
                            "host",
                            "userid",
                            "password"
                        ]
                    }
                }
            ],
            "sourceSpec": {
                "name": "CloudStorage",
                "type": "CloudStorage",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "path": {
                            "type": "string",
                            "description": "input path for copying files, can be a folder path, file path or a wildcard pattern"
                        },
                        "recursive": {
                            "type": "boolean",
                            "description": "indicates recursive copy in case of folder or wild card path, default is false"
                        }
                    },
                    "required": [
                        "path"
                    ]
                },
                "attributes": {
                    "uiAttributes": {
                        "documentationLink": "http://www.adobe.com/go/sources-azure-file-storage-en",
                        "isSource": true,
                        "category": {
                            "key": "cloudStorage"
                        },
                        "icon": {
                            "key": "azureFileStorage"
                        },
                        "description": {
                            "key": "azureFileStorageDescription"
                        },
                        "label": {
                            "key": "azureFileStorageLabel"
                        }
                    }
                }
            },
            "exploreSpec": {
                "name": "FileSystem",
                "type": "FileSystem",
                "requestSpec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "description": "defines explorable objects",
                    "properties": {
                        "objectType": {
                            "type": "string",
                            "enum": [
                                "file",
                                "folder",
                                "root"
                            ]
                        }
                    },
                    "allOf": [
                        {
                            "if": {
                                "properties": {
                                    "objectType": {
                                        "enum": [
                                            "file"
                                        ]
                                    }
                                }
                            },
                            "then": {
                                "properties": {
                                    "object": {
                                        "type": "string",
                                        "description": "defines file to get schema or preview of."
                                    },
                                    "fileType": {
                                        "type": "string",
                                        "enum": [
                                            "delimited"
                                        ]
                                    },
                                    "preview": {
                                        "type": "boolean"
                                    }
                                },
                                "required": [
                                    "object",
                                    "fileType"
                                ]
                            }
                        },
                        {
                            "if": {
                                "properties": {
                                    "objectType": {
                                        "enum": [
                                            "folder"
                                        ]
                                    }
                                }
                            },
                            "then": {
                                "properties": {
                                    "object": {
                                        "type": "string"
                                    }
                                },
                                "required": [
                                    "object"
                                ]
                            }
                        }
                    ]
                },
                "responseSpec": {
                    "root": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "array",
                        "description": "lists tables/items under the database/container requested.",
                        "items": {
                            "type": "object",
                            "properties": {
                                "type": {
                                    "type": "string",
                                    "description": "defines type of an item."
                                },
                                "name": {
                                    "type": "string",
                                    "description": "defines display name of an item."
                                },
                                "path": {
                                    "type": "string",
                                    "description": "defines path of an item."
                                },
                                "canPreview": {
                                    "type": "boolean",
                                    "default": false,
                                    "description": "defines whether an item is previewable or not."
                                },
                                "canFetchSchema": {
                                    "type": "boolean",
                                    "default": false,
                                    "description": "defines whether schema can be fetched for an item or not."
                                }
                            }
                        }
                    },
                    "folder": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "array",
                        "items": {
                            "type": "object",
                            "properties": {
                                "type": {
                                    "type": "string"
                                },
                                "name": {
                                    "type": "string"
                                },
                                "path": {
                                    "type": "string"
                                },
                                "canPreview": {
                                    "type": "boolean",
                                    "default": false
                                },
                                "canFetchSchema": {
                                    "type": "boolean",
                                    "default": false
                                }
                            }
                        }
                    },
                    "file": {
                        "delimited": {
                            "$schema": "http://json-schema.org/draft-07/schema#",
                            "type": "object",
                            "properties": {
                                "format": {
                                    "type": "string"
                                },
                                "schema": {
                                    "type": "object",
                                    "properties": {
                                        "columns": {
                                            "type": "array",
                                            "items": {
                                                "type": "object",
                                                "properties": {
                                                    "name": {
                                                        "type": "string"
                                                    },
                                                    "type": {
                                                        "type": "string"
                                                    }
                                                }
                                            }
                                        }
                                    }
                                },
                                "data": {
                                    "type": "array",
                                    "items": {
                                        "type": "object"
                                    }
                                }
                            }
                        }
                    }
                }
            },
            "attributes": {
                "category": "Cloud Storage",
                "connectorName": "Azure File Storage",
                "isSource": true,
                "isDraftModeSupported": true,
                "uiAttributes": {
                    "apiFeatures": {
                        "explorePaginationSupported": false
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

>[!TAB Details zur Flussspezifikation nachschlagen]

+++ Anfrage Die folgende Anfrage ruft die Details der Flussspezifikationen für eine Cloud-Speicherquelle ab:

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name==%22CloudStorageToAEP%22' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Antwort

Bei einer erfolgreichen Antwort werden die Informationen zur Flussspezifikation für Ihre Quelle zurückgegeben. Um zu überprüfen, ob der Entwurfsmodus für Ihre Quelle unterstützt wird, überprüfen Sie, ob die `items[0].attributes.isDraftModeSupported` hat den Wert `true`.

```json {line-numbers="true" start-line="1" highlight="167"}
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
        "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
        "54e221aa-d342-4707-bcff-7a4bceef0001",
        "c85f9425-fb21-426c-ad0b-405e9bd8a46c",
        "26f526f2-58f4-4712-961d-e41bf1ccc0e8"
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
        },
        {
          "name": "Encryption",
          "spec": {
            "$schema": "http://json-schema.org/draft-07/schema#",
            "type": "object",
            "description": "defines various params required for encrypted data ingestion",
            "properties": {
              "publicKeyId": {
                "type": "string",
                "description": "publicKeyId returned in encryptionKey creation API. One must use the publicKeyId corresponding to the same publicKey they used for encrypting the files"
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

>[!ENDTABS]



## Erstellen einer Basisverbindung für Entwurf {#create-a-draft-base-connection}

Um eine Basisverbindung für Entwurf zu erstellen, stellen Sie eine POST-Anfrage an die `/connections` Endpunkt der [!DNL Flow Service] API und Bereitstellung `mode=draft` als Abfrageparameter.

**API-Format**

```http
POST /connections?mode=draft
```

| Parameter | Beschreibung |
| --- | --- |
| `mode` | Ein vom Benutzer bereitgestellter Abfrageparameter, der den Status der Basisverbindung bestimmt. Um eine Basisverbindung als Entwurf festzulegen, legen Sie `mode` nach `draft`. |

**Anfrage**

Die folgende Anfrage erstellt den Entwurf der Basisverbindung für die [!DNL Azure File Storage] source:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "ACME Azure File Storage Base Connection",
        "description": "Azure File Storage base connection for ACME data (DRAFT)",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST}",
                    "userId": "{USER_ID}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
            "version": "1.0"
        }
      }'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Basis-Verbindungs-ID und das entsprechende eTag für Ihre Entwurfsbasisverbindung zurück. Sie können diese ID später verwenden, um Ihre Basisverbindung zu aktualisieren und zu veröffentlichen.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## Veröffentlichen der Basisverbindung für Entwurf {#publish-your-draft-base-connection}

Sobald Ihr Entwurf zur Veröffentlichung bereit ist, stellen Sie eine POST-Anfrage an die `/connections` -Endpunkt und geben Sie die ID der Basisverbindung für den Entwurf an, die Sie veröffentlichen möchten, sowie einen Aktionsvorgang für die Veröffentlichung.

**API-Format**

```http
POST /connections/{BASE_CONNECTION_ID}/action?op=publish
```

| Parameter | Beschreibung |
| --- | --- |
| `op` | Ein Aktionsvorgang, der den Status der abgefragten Basisverbindung aktualisiert. Um eine Entwurfsbasisverbindung zu veröffentlichen, legen Sie `op` nach `publish`. |

**Anfrage**

Die folgende Anfrage veröffentlicht die Entwurfsbasisverbindung für [!DNL Azure File Storage] , die in einem früheren Schritt erstellt wurde.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f9377f50-607a-4818-b77f-50607a181860/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Bei einer erfolgreichen Antwort werden die ID und das entsprechende eTag für Ihre veröffentlichte Basisverbindung zurückgegeben.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## Erstellen einer Quellverbindung für Entwurf {#create-a-draft-source-connection}

Um eine Quellverbindung für Entwurf zu erstellen, stellen Sie eine POST-Anfrage an die `/sourceConnections` Endpunkt der [!DNL Flow Service] API und Bereitstellung `mode=draft` als Abfrageparameter.

**API-Format**

```http
POST /sourceConnections?mode=draft
```

| Parameter | Beschreibung |
| --- | --- |
| `mode` | Ein vom Benutzer bereitgestellter Abfrageparameter, der den Status der Quellverbindung bestimmt. Um eine Quellverbindung als Entwurf festzulegen, legen Sie `mode` nach `draft`. |

**Anfrage**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections?mode=draft' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Azure File Storage Source Connection",
      "description: "Azure File Storage source connection for ACME data (DRAFT)",
      "baseConnectionId": "f9377f50-607a-4818-b77f-50607a181860",
      "data": {
          "format": "delimited",
      },
      "params": {
          "path": "/acme/summerCampaign/account.csv",
          "type": "file"
      },
      "connectionSpec": {
          "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
          "version": "1.0"
      }
  }'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Kennung der Quellverbindung und das entsprechende eTag für Ihre Entwurfsquellenverbindung zurück. Sie können diese ID später verwenden, um Ihre Quellverbindung zu aktualisieren und zu veröffentlichen.

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

## Veröffentlichen der Quellverbindung des Entwurfs {#publish-your-draft-source-connection}

>[!NOTE]
>
>Sie können eine Quellverbindung nicht veröffentlichen, wenn die zugehörige Basisverbindung noch im Entwurfszustand ist. Stellen Sie sicher, dass Ihre Basisverbindung zuerst veröffentlicht wird, bevor Sie Ihre Quellverbindung veröffentlichen.

Sobald Ihr Entwurf zur Veröffentlichung bereit ist, stellen Sie eine POST-Anfrage an die `/sourceConnections` -Endpunkt und geben Sie die ID der Quellverbindung des Entwurfs an, die Sie veröffentlichen möchten, sowie einen Aktionsvorgang für die Veröffentlichung.

**API-Format**

```http
POST /sourceConnections/{SOURCE_CONNECTION_ID}/action?op=publish
```

| Parameter | Beschreibung |
| --- | --- |
| `op` | Ein Aktionsvorgang, der den Status der abgefragten Quellverbindung aktualisiert. Um eine Quellverbindung für Entwurf zu veröffentlichen, legen Sie `op` nach `publish`. |

**Anfrage**

Die folgende Anfrage veröffentlicht den Entwurf der Quellverbindung für [!DNL Azure File Storage] , die in einem früheren Schritt erstellt wurde.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/26b53912-1005-49f0-b539-12100559f0e2/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Bei einer erfolgreichen Antwort werden die ID und das entsprechende eTag für Ihre veröffentlichte Quellverbindung zurückgegeben.

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

## Erstellen einer Entwurfs-Zielverbindung {#create-a-draft-target-connection}

Um eine Entwurfs-Zielverbindung zu erstellen, stellen Sie eine POST-Anfrage an die `/targetConnections` Endpunkt der [!DNL Flow Service] API und Bereitstellung `mode=draft` als Abfrageparameter.

**API-Format**

```http
POST /targetConnections?mode=draft
```

| Parameter | Beschreibung |
| --- | --- |
| `mode` | Ein vom Benutzer bereitgestellter Abfrageparameter, der den Status der Zielverbindung bestimmt. Um eine Zielverbindung als Entwurf festzulegen, legen Sie `mode` nach `draft`. |

**Anfrage**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections?mode=draft' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Azure File Storage Target Connection",
      "description": "Azure File Storage target connection ACME data (DRAFT)",
      "data": {
          "schema": {
              "id": "{SCHEMA_ID}",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "{DATASET_ID}"
      },
          "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
  }'
```

**Antwort**

Bei einer erfolgreichen Antwort werden die Ziel-Verbindungs-ID und das entsprechende eTag für Ihre Entwurfs-Zielverbindung zurückgegeben. Sie können diese ID später verwenden, um Ihre Zielverbindung zu aktualisieren und zu veröffentlichen.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Veröffentlichen der Entwurfs-Zielverbindung {#publish-your-draft-target-connection}

>[!NOTE]
>
>Sie können eine Zielverbindung nicht veröffentlichen, wenn die zugehörige Basisverbindung noch im Entwurfszustand ist. Stellen Sie sicher, dass Ihre Basisverbindung zuerst veröffentlicht wird, bevor Sie Ihre Zielverbindung veröffentlichen.

Sobald Ihr Entwurf zur Veröffentlichung bereit ist, stellen Sie eine POST-Anfrage an die `/targetConnections` -Endpunkt und geben Sie die ID der Entwurfs-Zielverbindung an, die Sie veröffentlichen möchten, sowie einen Aktionsvorgang für die Veröffentlichung.

**API-Format**

```http
POST /targetConnections/{TARGET_CONNECTION_ID}/action?op=publish
```

| Parameter | Beschreibung |
| --- | --- |
| `op` | Ein Aktionsvorgang, der den Status der abgefragten Zielverbindung aktualisiert. Um eine Entwurfs-Zielverbindung zu veröffentlichen, legen Sie `op` nach `publish`. |

**Anfrage**

Die folgende Anfrage veröffentlicht den Entwurf der Zielverbindung für [!DNL Azure File Storage] , die in einem früheren Schritt erstellt wurde.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dbc5c132-bc2a-4625-85c1-32bc2a262558/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Bei einer erfolgreichen Antwort werden die ID und das entsprechende eTag für Ihre veröffentlichte Zielverbindung zurückgegeben.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Erstellen eines Entwurfs-Datenflusses {#create-a-draft-dataflow}

Um einen Datenfluss als Entwurf festzulegen, stellen Sie eine POST-Anfrage an den `/flows`-Endpunkt und fügen `mode=draft` als Abfrageparameter hinzu. Auf diese Weise können Sie einen Datenfluss erstellen und als Entwurf speichern.

**API-Format**

```http
POST /flows?mode=draft
```

| Parameter | Beschreibung |
| --- | --- |
| `mode` | Ein von der Benutzerin bzw. dem Benutzer eingegebener Abfrageparameter, der den Status des Datenflusses bestimmt. Um einen Datenfluss als Entwurf festzulegen, legen Sie `mode` auf `draft` fest. |

**Anfrage**

Mit der folgenden Anfrage wird ein Datenflussentwurf erstellt.

```shell
  'https://platform.adobe.io/data/foundation/flowservice/flows?mode=draft' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "ACME Azure File Storage Dataflow",
    "description": "Azure File Storage dataflow for ACME data (DRAFT)",
    "sourceConnectionIds": [
        "26b53912-1005-49f0-b539-12100559f0e2"
    ],
    "targetConnectionIds": [
        "dbc5c132-bc2a-4625-85c1-32bc2a262558"
    ],
    "flowSpec": {
        "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
        "version": "1.0"
    }
  }'
```

**Antwort**

Bei einer erfolgreichen Antwort werden die Fluss-ID und das entsprechende eTag für Ihren Datenfluss im Entwurf zurückgegeben. Sie können diese ID später verwenden, um Ihren Datenfluss zu aktualisieren und zu veröffentlichen.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

## Veröffentlichen des Entwurfs eines Datenflusses {#publish-your-draft-dataflow}

>[!NOTE]
>
>Sie können einen Datenfluss nicht veröffentlichen, wenn die zugehörigen Quell- und Zielverbindungen sich noch im Entwurfsstatus befinden. Stellen Sie sicher, dass Ihre Quell- und Zielverbindungen zuerst veröffentlicht werden, bevor Sie Ihren Datenfluss veröffentlichen.

Sobald Ihr Entwurf zur Veröffentlichung bereit ist, stellen Sie eine POST-Anfrage an den `/flows`-Endpunkt und geben Sie die ID des Datenflussentwurfs an, den Sie veröffentlichen möchten, sowie einen Aktionsvorgang für die Veröffentlichung.

**API-Format**

```http
POST /flows/{FLOW_ID}/action?op=publish
```

| Parameter | Beschreibung |
| --- | --- |
| `op` | Ein Aktionsvorgang, der den Status des abgefragten Datenflusses aktualisiert. Um einen Datenfluss-Entwurf zu veröffentlichen, legen Sie `op` auf `publish` fest. |

**Anfrage**

Mit der folgenden Anfrage wird Ihr Datenfluss-Entwurf veröffentlicht.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows/c9751426-dff8-49b0-965f-50defcf4187b/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Bei einer erfolgreichen Antwort werden die ID und das entsprechende `etag` Ihres Datenflusses zurückgegeben.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie gelernt, wie Sie Entwürfe Ihrer [!DNL Flow Service] -Entitäten und veröffentlichen Sie diese Entwürfe. Weitere Informationen zu Quellen finden Sie im [Quellen - Übersicht](../../home.md).