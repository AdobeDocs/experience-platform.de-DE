---
title: Aktualisieren einer Verbindungsspezifikation für Streaming-SDK mithilfe der Flow Service-API
description: Das folgende Dokument beschreibt die Schritte zum Erstellen einer Verbindungsspezifikation mithilfe der Flow Service-API für Selbstbedienungsquellen (Streaming-SDK).
exl-id: 89f96ae1-81d0-47a3-9e21-7dae810ee823
badge: Beta
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 4%

---

# Aktualisieren einer Verbindungsspezifikation mithilfe der Flow Service-API

>[!NOTE]
>
>Selbstbedienungsquellen-Streaming SDK befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Quellen finden Sie ](../../home.md#terms-and-conditions) „Quellen - Übersicht“.

Sie können die Eigenschaften einer Verbindungsspezifikation durch einen PUT-Vorgang aktualisieren. Beim Aktualisieren einer Verbindungsspezifikation über eine PUT-Anfrage muss der Hauptteil alle Felder enthalten, die beim Erstellen einer neuen Verbindungsspezifikation in einer POST-Anfrage erforderlich wären.

**API-Format**

```http
PUT /connectionSpecs/{CONNECTION_SPEC_ID}
```

**Anfrage**

Die folgende Anfrage fügt eine Beschreibung der im vorherigen Tutorial erstellten Streaming-Verbindungsspezifikation hinzu.

```shell
PUT -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/f6c0de0c-0a42-4cd9-9139-8768bf2f1b55' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "generic-streaming",
      "type": "generic-streaming",
      "description": "A sample streaming source for ACME data"
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "version": "1.0",
      "attributes": {
          "category": "Streaming",
          "isSource": true,
          "documentationLink": "https://docs.adobe.com/content/help/de-DE/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
          "uiAttributes": {
            "apiFeatures": {
              "updateSupported": false
            }
          }
        },
        "authSpec": [],
        "name": "generic-streaming",
        "permissionsInfo": {
          "view": [
            {
              "name": "StreamingSource",
              "@type": "lowLevel",
              "permissions": [
                "read"
              ]
            }
          ],
          "manage": [
            {
              "name": "StreamingSource",
              "@type": "lowLevel",
              "permissions": [
                "write"
              ]
            }
          ]
        },
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "sourceSpec": {
          "attributes": {
            "authRequired": false,
            "uiAttributes": {
              "documentationLink": "http://www.adobe.com/go/understanding-data-streaming-ingestion-en",
              "isSource": true,
              "monitoringSupported": false,
              "category": {
                "key": "streaming"
              },
              "icon": {
                "key": "Generic-Streaming"
              },
              "description": {
                "text": "Generic Streaming Connector"
              },
              "label": {
                "text": "Generic"
              },
              "frequency": {
                "text": "streaming"
              }
            }
          }
        },
        "exploreSpec": {
          "type": "StreamingConnection"
          },
        "type": "generic-streaming",
        "version": "1.0"
      }'
```

**Antwort**

Ein erfolgreicher Aufruf gibt die aktualisierten Details der Verbindungsspezifikation zurück, einschließlich ihres aktualisierten Namens.

```json
{
  "items": [
    {
      "id": "bdb5b792-451b-42de-acf8-15f3195821de",
      "createdAt": 1667536504101,
      "updatedAt": 1667536504101,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{CREATED_CLIENT}",
      "sandboxId": "d537df80-c5d7-11e9-aafb-87c71c35cac8",
      "sandboxName": "prod",
      "imsOrgId": "{ORG_ID}",
      "name": "generic-streaming",
      "description": "A sample streaming source for ACME data",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "version": "1.0",
      "type": "generic-streaming",
      "sourceSpec": {
        "attributes": {
          "authRequired": false,
          "uiAttributes": {
            "documentationLink": "http://www.adobe.com/go/understanding-data-streaming-ingestion-en",
            "isSource": true,
            "monitoringSupported": false,
            "category": {
              "key": "streaming"
            },
            "icon": {
              "key": "Generic-Streaming"
            },
            "description": {
              "text": "Generic Streaming Connector"
            },
            "label": {
              "text": "Generic"
            },
            "frequency": {
              "text": "streaming"
            }
          }
        }
      },
      "exploreSpec": {
        "type": "StreamingConnection"
      },
      "attributes": {
        "category": "Streaming",
        "isSource": true,
        "documentationLink": "https://docs.adobe.com/content/help/de-DE/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
        "uiAttributes": {
          "apiFeatures": {
            "updateSupported": false
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
    }
  ]
}
```

## Nächste Schritte

Nachdem Sie die Aktualisierungen Ihrer Verbindungsspezifikation abgeschlossen haben, können Sie jetzt mit [Testen und Senden Ihrer Quelle für die Integration](./submit.md) fortfahren.
