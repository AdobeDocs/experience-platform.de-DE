---
title: Flussspezifikationen für das Streaming-SDK mithilfe der Flow Service-API aktualisieren
description: Das folgende Dokument enthält Schritte zum Abrufen und Aktualisieren von Flussspezifikationen mithilfe der Flow Service-API für Self-Serve-Quellen (Streaming-SDK).
exl-id: cc9dab7a-08fa-4c6c-bbac-cb658a6376fb
badge: Beta
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 13%

---

# Flussspezifikationen mithilfe der [!DNL Flow Service]-API aktualisieren

>[!NOTE]
>
>Das Streaming-SDK für Self-Serve-Quellen befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta-beschrifteten Quellen finden Sie in der [Quellenübersicht](../../home.md#terms-and-conditions) .

Nachdem Sie eine neue Verbindungsspezifikations-ID generiert haben, müssen Sie diese ID einer Flussspezifikation hinzufügen, um einen Datenfluss zu erstellen.

Flussspezifikationen enthalten Informationen, die einen Fluss definieren, einschließlich der von ihm unterstützten Quell- und Zielverbindungs-IDs, Transformationsspezifikationen, die auf die Daten angewendet werden müssen, und Planungsparameter, die zum Generieren eines Datenflusses erforderlich sind. Sie können Flussspezifikationen mithilfe des Endpunkts `/flowSpecs` bearbeiten.

Das folgende Dokument enthält Schritte zum Abrufen und Aktualisieren von Flussspezifikationen mithilfe der [!DNL Flow Service] API für Self-Serve-Quellen (Streaming-SDK).

## Erste Schritte

Bevor Sie fortfahren, lesen Sie das Handbuch [Erste Schritte](./getting-started.md) mit Links zur zugehörigen Dokumentation, einer Anleitung zum Lesen der API-Beispielaufrufe in diesem Dokument und wichtigen Informationen zu den erforderlichen Kopfzeilen, die für die erfolgreiche Ausführung von Aufrufen an eine Experience Platform-API erforderlich sind.

## Flussspezifikation nachschlagen {#lookup}

Quellen, die mit der Vorlage `generic-streaming` erstellt wurden, verwenden alle die Flussspezifikation `GenericStreamingAEP`. Diese Flussspezifikation kann abgerufen werden, indem eine GET-Anfrage an den `/flowSpecs/` -Endpunkt gesendet und der `flowSpec.id` von `e77fde5a-22a8-11ed-861d-0242ac120002` angegeben wird.

**API-Format**

```http
GET /flowSpecs/e77fde5a-22a8-11ed-861d-0242ac120002
```

**Anfrage**

Mit der folgenden Anfrage wird die Flussspezifikation `e77fde5a-22a8-11ed-861d-0242ac120002` abgerufen.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flowSpecs/e77fde5a-22a8-11ed-861d-0242ac120002' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Spezifikation des abgefragten Flusses zurück.

```json
{
  "items": [
    {
      "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
      "name": "GenericStreamingAEP",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "version": "1.0",
      "sourceConnectionSpecIds": [
        "e77fd9d2-22a8-11ed-861d-0242ac120002"
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
            },
            "inletUrl": {
              "title": "Inlet Url.",
              "description": "Inlet Url which defines the streaming endpoint.",
              "type": "string"
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
        }
      ],
      "attributes": {
        "isSourceFlow": true,
        "flacValidationSupported": true,
        "frequency": "streaming",
        "uiAttributes": {
          "apiFeatures": {
            "updateSupported": true,
            "flowRunsSupported": true
          }
        }
      },
      "permissionsInfo": {
        "manage": [
          {
            "@type": "lowLevel",
            "name": "StreamingSource",
            "permissions": [
              "write"
            ]
          }
        ],
        "view": [
          {
            "@type": "lowLevel",
            "name": "StreamingSource",
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

## Aktualisieren einer Flussspezifikation {#update}

Sie können die Felder einer Flussspezifikation über einen PUT-Vorgang aktualisieren. Beim Aktualisieren einer Flussspezifikation über eine PUT-Anfrage muss der Hauptteil alle Felder enthalten, die beim Erstellen einer neuen Flussspezifikation in einer POST-Anfrage erforderlich sind.

>[!IMPORTANT]
>
>Wenn Sie eine Verbindungsspezifikation für eine neue Quelle erstellen, müssen Sie deren Spezifikations-ID dem Array `sourceConnectionSpecIds` der Flussspezifikationen hinzufügen, die Ihrer Quelle entsprechen. Dadurch wird sichergestellt, dass Ihre neue Quelle von einer vorhandenen Flussspezifikation unterstützt wird, sodass Sie den Datenfluss-Erstellungsprozess mit Ihrer neuen Quelle abschließen können.

**API-Format**

```http
PUT /flowSpecs/e77fde5a-22a8-11ed-861d-0242ac120002
```

**Anfrage**

Mit der folgenden Anfrage wird die Flussspezifikation von `e77fde5a-22a8-11ed-861d-0242ac120002` aktualisiert und enthält die Verbindungsspezifikations-ID `bdb5b792-451b-42de-acf8-15f3195821de`.

```shell
PUT -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/e77fde5a-22a8-11ed-861d-0242ac120002' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
      "name": "GenericStreamingAEP",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "version": "1.0",
      "sourceConnectionSpecIds": [
          "e77fd9d2-22a8-11ed-861d-0242ac120002",
          "bdb5b792-451b-42de-acf8-15f3195821de"
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
                  },
                  "inletUrl": {
                      "title": "Inlet Url.",
                      "description": "Inlet Url which defines the streaming endpoint.",
                      "type": "string"
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
          }
      ],
      "attributes": {
          "isSourceFlow": true,
          "flacValidationSupported": true,
          "frequency": "streaming",
          "uiAttributes": {
              "apiFeatures": {
                  "updateSupported": true,
                  "flowRunsSupported": true
              }
          }
      },
      "permissionsInfo": {
          "view": [
              {
                  "@type": "lowLevel",
                  "name": "StreamingSource",
                  "permissions": [
                      "read"
                  ]
              }
          ],
          "manage": [
              {
                  "@type": "lowLevel",
                  "name": "StreamingSource",
                  "permissions": [
                      "write"
                  ]
              }
          ]
      }
  }'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Spezifikation des abgefragten Flusses zurück, einschließlich der aktualisierten Liste mit `sourceConnectionSpecIds`.

```json
{
    "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
    "updatedAt": 1633393222979,
    "updatedBy": "1633393222979",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "{SANDBOX_NAME}",
    "imsOrgId": "{ORG_ID}",
    "name": "GenericStreamingAEP",
    "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
    "version": "1.0",
      "sourceConnectionSpecIds": [
        "e77fd9d2-22a8-11ed-861d-0242ac120002"
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
            },
            "inletUrl": {
              "title": "Inlet Url.",
              "description": "Inlet Url which defines the streaming endpoint.",
              "type": "string"
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
        }
      ],
      "attributes": {
        "isSourceFlow": true,
        "flacValidationSupported": true,
        "frequency": "streaming",
        "uiAttributes": {
          "apiFeatures": {
            "updateSupported": true,
            "flowRunsSupported": true
          }
        }
      },
      "permissionsInfo": {
        "manage": [
          {
            "@type": "lowLevel",
            "name": "StreamingSource",
            "permissions": [
              "write"
            ]
          }
        ],
        "view": [
          {
            "@type": "lowLevel",
            "name": "StreamingSource",
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

## Nächste Schritte

Nachdem Ihre neue Verbindungsspezifikation der entsprechenden Flussspezifikation hinzugefügt wurde, können Sie jetzt mit dem Testen und Senden Ihrer neuen Quelle fortfahren. Weitere Informationen finden Sie im Handbuch zum [Testen und Senden einer neuen Quelle](./submit.md) .
