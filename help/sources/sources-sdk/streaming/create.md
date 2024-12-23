---
title: Erstellen einer neuen Verbindungsspezifikation für das Streaming-SDK mithilfe der Flow Service-API
description: Im folgenden Dokument erfahren Sie, wie Sie eine Verbindungsspezifikation mithilfe der Flow Service-API erstellen und eine neue Quelle über Self-Serve-Quellen integrieren.
exl-id: ad8f6004-4e82-49b5-aede-413d72a1482d
badge: Beta
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 36%

---

# Erstellen einer neuen Verbindungsspezifikation mit der [!DNL Flow Service]-API

>[!NOTE]
>
>Das Streaming-SDK für Self-Serve-Quellen befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta-beschrifteten Quellen finden Sie in der [Quellenübersicht](../../home.md#terms-and-conditions) .

Eine Verbindungsspezifikation stellt die Struktur einer Quelle dar. Sie enthält Informationen zu den Authentifizierungsanforderungen einer Quelle, definiert, wie Quelldaten untersucht und geprüft werden können, und enthält Informationen zu den Attributen einer bestimmten Quelle. Der `/connectionSpecs`-Endpunkt in der [!DNL Flow Service]-API ermöglicht Ihnen die programmgesteuerte Verwaltung der Verbindungsspezifikationen innerhalb Ihrer Organisation.

Im folgenden Dokument erfahren Sie, wie Sie eine Verbindungsspezifikation mit der [!DNL Flow Service] -API erstellen und eine neue Quelle über Self-Serve-Quellen (Streaming-SDK) integrieren.

## Erste Schritte

Bevor Sie fortfahren, lesen Sie das Handbuch [Erste Schritte](./getting-started.md) mit Links zur zugehörigen Dokumentation, einer Anleitung zum Lesen der API-Beispielaufrufe in diesem Dokument und wichtigen Informationen zu den erforderlichen Kopfzeilen, die für die erfolgreiche Ausführung von Aufrufen an eine Experience Platform-API erforderlich sind.

## Sammeln von Artefakten

Um eine neue Streaming-Quelle mithilfe von Self-Serve-Quellen zu erstellen, müssen Sie zunächst eine Koordination mit Adobe durchführen, ein privates Git-Repository anfordern und die Details zu Titel, Beschreibung, Kategorie und Symbol für Ihre Quelle an Adobe ausrichten.

Nach der Bereitstellung müssen Sie Ihr privates Git-Repository wie folgt strukturieren:

* Quellen
   * {your_source}
      * Artefakte
         * {your_source}-category.txt
         * {your_source}-description.txt
         * {your_source}-icon.svg
         * {your_source}-label.txt
         * {your_source}-connectionSpec.json

| Artefakte (Dateinamen) | Beschreibung | Beispiel |
| --- | --- | --- |
| {your_source} | Der Name Ihrer Quelle. Dieser Ordner sollte alle Artefakte enthalten, die mit Ihrer Quelle in Ihrem privaten Git-Repository zusammenhängen. | `medallia` |
| {your_source}-category.txt | Die Kategorie, zu der die Quelle gehört, formatiert als Textdatei. **Hinweis**: Wenn Sie glauben, dass Ihre Quelle nicht in eine der oben genannten Kategorien passt, wenden Sie sich an Ihren Adobe-Kundenbetreuer, um darüber zu diskutieren. | `medallia-category.txt` Geben Sie in der Datei die Kategorie Ihrer Quelle an, z. B.: `streaming`. |
| {your_source}-description.txt | Eine kurze Beschreibung Ihrer Quelle. | [!DNL Medallia] ist eine Marketing-Automatisierungsquelle, mit der Sie [!DNL Medallia] -Daten an Experience Platform übertragen können. |
| {your_source}-icon.svg | Das Bild, das für die Darstellung Ihrer Quelle im Experience Platform-Quellkatalog verwendet werden soll. Dieses Symbol muss eine SVG-Datei sein. |
| {your_source}-label.txt | Der Quellname, wie er im Experience Platform-Quellkatalog angezeigt werden soll. | Medallia |
| {your_source}-connectionSpec.json | Eine JSON-Datei mit der Verbindungsspezifikation Ihrer Quelle. Diese Datei ist zunächst nicht erforderlich, da Sie Ihre Verbindungsspezifikation nach Abschluss dieses Handbuchs füllen werden. | `medallia-connectionSpec.json` |

{style="table-layout:auto"}

>[!TIP]
>
>Während des Testzeitraums Ihrer Verbindungsspezifikation können Sie anstelle der Schlüsselwerte `text` in der Verbindungsspezifikation verwenden.

Nachdem Sie die erforderlichen Dateien zu Ihrem privaten Git-Repository hinzugefügt haben, müssen Sie eine Pull-Anforderung (PA) erstellen, damit Adobe sie überprüfen kann. Wenn Ihr PR genehmigt und zusammengeführt wird, erhalten Sie eine ID, die für Ihre Verbindungsspezifikation verwendet werden kann, um auf den Titel, die Beschreibung und das Symbol Ihrer Quelle zu verweisen.

Führen Sie anschließend die unten beschriebenen Schritte aus, um Ihre Verbindungsspezifikation zu konfigurieren. Weitere Anleitungen zu den verschiedenen Funktionen, die Sie Ihrer Quelle hinzufügen können, wie z. B. erweiterte Planung, benutzerdefiniertes Schema oder verschiedene Paginierungstypen, finden Sie im Handbuch [Konfigurieren von Quellspezifikationen](../config/sourcespec.md).

## Kopieren der Vorlage für die Verbindungsspezifikation

Nachdem Sie die erforderlichen Artefakte gesammelt haben, kopieren Sie die unten stehende Vorlage für die Verbindungsspezifikation in den Texteditor Ihrer Wahl und aktualisieren Sie dann die Attribute in Klammern `{}` mit Informationen, die für Ihre spezifische Quelle relevant sind.

```json
{
  "name": "generic-streaming",
  "type": "generic-streaming",
  "description": "{DESCRIPTION}",
  "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
  "version": "1.0",
  "attributes": {
    "category": "Streaming",
    "isSource": true,
    "documentationLink": "https://docs.adobe.com/content/help/en/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
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
          "key": "generic"
        },
        "description": {
          "text": "Generic Streaming For Authentication Testing 2"
        },
        "label": {
          "text": "Generic Streaming For Authentication Testing 2"
        },
        "frequency": {
          "text": "Generic Streaming"
        }
      }
    }
  },
  "exploreSpec": {
    "type": "StreamingConnection"
  }
}
```

## Erstellen einer Verbindungsspezifikation {#create}

Sobald Sie sich die Vorlage für die Verbindungsspezifikation besorgt haben, können Sie damit beginnen, eine neue Verbindungsspezifikation zu erstellen, indem Sie die passenden Werte eingeben, die Ihrer Quelle entsprechen.

Eine Verbindungsspezifikation kann in zwei verschiedene Teile unterteilt werden: die Quellspezifikationen und die Erkundungsspezifikationen.

Weitere Informationen zu den Abschnitten einer Verbindungsspezifikation finden Sie in den folgenden Dokumenten:

* [Konfigurieren Ihrer Quellspezifikation](../config/sourcespec.md)
* [Konfigurieren Ihrer Erkundungsspezifikation](../config/explorespec.md)

Wenn Ihre Spezifikationsdaten aktualisiert worden sind, können Sie die neue Verbindungsspezifikation übermitteln, indem Sie eine POST-Anfrage an den Endpunkt `/connectionSpecs` der [!DNL Flow Service]-API stellen.

**API-Format**

```http
POST /connectionSpecs
```

**Anfrage**

Die folgende Anfrage ist ein Beispiel für eine vollständig erstellte Verbindungsspezifikation für eine Streaming-Quelle:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "generic-streaming",
      "type": "generic-streaming",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "version": "1.0",
      "attributes": {
          "category": "Streaming",
          "isSource": true,
          "documentationLink": "https://docs.adobe.com/content/help/en/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
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

Bei einer erfolgreichen Antwort wird die neu erstellte Verbindungsspezifikation einschließlich ihrer eindeutigen `id` zurückgegeben.

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
        "documentationLink": "https://docs.adobe.com/content/help/en/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
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

Nachdem Sie eine neue Verbindungsspezifikation erstellt haben, müssen Sie die entsprechende Verbindungsspezifikations-ID zu einer vorhandenen Flussspezifikation hinzufügen. Weitere Informationen finden Sie im Tutorial zum [Aktualisieren von Flussspezifikationen](./update-flow-specs.md).

Informationen zum Ändern der von Ihnen erstellten Verbindungsspezifikation finden Sie im Tutorial zum [Aktualisieren der Verbindungsspezifikationen](./update-connection-specs.md).
