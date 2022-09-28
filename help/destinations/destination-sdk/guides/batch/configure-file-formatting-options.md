---
description: Dateiformatierungsoptionen für dateibasierte Ziele konfigurieren
title: Erfahren Sie, wie Sie mit Destination SDK Dateiformatierungsoptionen für dateibasierte Ziele konfigurieren.
source-git-commit: 9b4c7da5aa02ae27608c2841b1d825445ac3015e
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 2%

---

# Dateiformatierungsoptionen für dateibasierte Ziele konfigurieren

## Übersicht {#overview}

Mit Destination SDK können Sie die Formatierungs- und Komprimierungsoptionen Ihrer exportierten Dateien umfassend anpassen, um die Anforderungen an den Speicherort zu erfüllen.

Auf dieser Seite wird beschrieben, wie Sie mit Destination SDK Dateiformatierungsoptionen für dateibasierte Ziele konfigurieren.

## Voraussetzungen {#prerequisites}

Bevor Sie mit den unten beschriebenen Schritten fortfahren, lesen Sie bitte die [Erste Schritte mit Destination SDK](../../getting-started.md) Seite mit Informationen zum Abrufen der erforderlichen Anmeldeinformationen für die Adobe I/O-Authentifizierung und anderen Voraussetzungen für die Verwendung mit Destination SDK-APIs.

Adobe empfiehlt Ihnen außerdem, sich mit der folgenden Dokumentation vertraut zu machen, bevor Sie fortfahren:

* Jede verfügbare Dateiformatierungsoption wird ausführlich im Abschnitt [Dateiformatierungskonfiguration](../../server-and-file-configuration.md#file-configuration) Abschnitt.
* Führen Sie die Schritte zum [ein dateibasiertes Ziel konfigurieren](/help/destinations/destination-sdk/configure-file-based-destination-instructions.md) Destination SDK verwenden.

## Erstellen einer Server- und Dateikonfiguration {#create-server-file-configuration}

Verwenden Sie zunächst die `/destination-server` -Endpunkt, um zu bestimmen, welche Dateiformatierungskonfigurationsoptionen Sie für die exportierten Dateien einrichten möchten.

Nachfolgend finden Sie ein Beispiel für eine Zielserverkonfiguration für eine [!DNL Amazon S3] Ziel, wobei mehrere Dateiformatierungsoptionen ausgewählt sind.

>[!TIP]
>
>Zur Erinnerung: Alle verfügbaren Dateiformatierungsoptionen werden im Abschnitt [Dateiformatierungskonfiguration](../../server-and-file-configuration.md#file-configuration) Abschnitt.

**API-Format**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-server \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
{
  "name": "Amazon S3 Server with several CSV Options",
  "destinationServerType": "FILE_BASED_S3",
  "fileBasedS3Destination": {
    "bucket": {
      "templatingStrategy": "PEBBLE_V1",
      "value": "{{customerData.bucket}}"
    },
    "path": {
      "templatingStrategy": "PEBBLE_V1",
      "value": "{{customerData.path}}"
    }
  },
  "fileConfigurations": {
    "compression": {
      "templatingStrategy": "PEBBLE_V1",
      "value": "{% if customerData contains 'compression' and customerData.compression is not empty %}{{customerData.compression}}{% else %}NONE{% endif %}"
    },
    "fileType": {
      "templatingStrategy": "PEBBLE_V1",
      "value": "{{customerData.fileType}}"
    },
    "csvOptions": {
      "sep": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'delimiter' %}{{customerData.csvOptions.delimiter}}{% else %},{% endif %}"
      },
      "quote": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'quote' %}{{customerData.csvOptions.quote}}{% else %}\"{% endif %}"
      },
      "escape": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'escape' %}{{customerData.csvOptions.escape}}{% else %}\\{% endif %}"
      },
      "nullValue": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'nullValue' %}{{customerData.csvOptions.nullValue}}{% else %}null{% endif %}"
      },
      "emptyValue": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'emptyValue' %}{{customerData.csvOptions.emptyValue}}{% else %}{% endif %}"
      }
    }
  }
}
}'
```

## Hinzufügen der Dateiformatierungsoptionen zur Zielkonfiguration {#create-destination-configuration}

>[!TIP]
>
>**Überprüfen der Experience Platform-Benutzeroberfläche**. Wenn Sie die Dateiformatierungsoptionen mit den in den folgenden Abschnitten beschriebenen Konfigurationen konfigurieren, sollten Sie in der Experience Platform-Benutzeroberfläche prüfen, wie diese Optionen dargestellt werden.

Nachdem Sie die gewünschten Dateiformatierungsoptionen im vorherigen Schritt zum Zielserver hinzugefügt und die Dateiformatierungskonfiguration konfiguriert haben, können Sie jetzt die `/destinations` API-Endpunkt zum Hinzufügen der gewünschten Felder als Kundendatenfelder zur Zielkonfiguration.

>[!IMPORTANT]
>
>Dieser Schritt ist optional und bestimmt nur, welche der Dateiformatierungsoptionen Benutzern in der Experience Platform-Benutzeroberfläche angezeigt werden sollen. Wenn Sie keine Dateiformatierungsoptionen als Kundendatenfelder einrichten, werden die Dateiexporte mit den Standardwerten fortgesetzt, die im Abschnitt [Server- und Dateikonfiguration](#create-server-file-configuration).

In diesem Schritt können Sie die angezeigten Optionen in beliebiger Reihenfolge gruppieren. Sie können benutzerdefinierte Gruppierungen, Dropdown-Felder und bedingte Gruppierungen basierend auf den ausgewählten Dateitypen erstellen. Alle diese Einstellungen werden in der Aufzeichnung und in den weiter unten stehenden Abschnitten angezeigt.

![Bildschirmaufzeichnung mit verschiedenen Dateiformatierungsoptionen für Batch-Dateien.](/help/destinations/destination-sdk/assets/guides/batch/file-formatting-options.gif)

### Reihenfolge der Dateiformatierungsoptionen {#ordering}

Die Reihenfolge, in der Sie die Dateiformatierungsoptionen als Kundendatenfelder in der Zielkonfiguration hinzufügen, wird in der Benutzeroberfläche angezeigt. Beispielsweise wird die folgende Konfiguration entsprechend in der Benutzeroberfläche angezeigt, wobei die Optionen in der Reihenfolge angezeigt werden **[!UICONTROL Trennzeichen]**, **[!UICONTROL Anführungszeichen]**, **[!UICONTROL Escape-Zeichen]**, **[!UICONTROL Leerer Wert]**, **[!UICONTROL Nullwert]**.

![Bild, das die Reihenfolge der Dateiformatierungsoptionen in der Benutzeroberfläche &quot;Experience Platform&quot;anzeigt.](/help/destinations/destination-sdk/assets/guides/batch/file-formatting-order.png)

```json
        {
            "name": "csvOptions",
            "title": "CSV Options",
            "description": "Select your CSV options",
            "type": "object",
            "properties": [
                {
                    "name": "delimiter",
                    "title": "Delimiter",
                    "description": "Select your Delimiter",
                    "type": "string",
                    "isRequired": false,
                    "default": ",",
                    "namedEnum": [
                        {
                            "name": "Comma (,)",
                            "value": ","
                        },
                        {
                            "name": "Tab (\\t)",
                            "value": "\t"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "quote",
                    "title": "Quote Character",
                    "description": "Select your Quote character",
                    "type": "string",
                    "isRequired": false,
                    "default": "\u0000",
                    "namedEnum": [
                        {
                            "name": "Double Quotes (\")",
                            "value": "\""
                        },
                        {
                            "name":"Null Character (\u0000)",
                            "value": ""
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "escape",
                    "title": "Escape Character",
                    "description": "Select your Escape character",
                    "type": "string",
                    "isRequired": false,
                    "default": "\\",
                    "namedEnum": [
                        {
                            "name": "Back Slash (\\)",
                            "value": "\\"
                        },
                        {
                            "name": "Single Quote (')",
                            "value": "'"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "emptyValue",
                    "title": "Empty Value",
                    "description": "Select the output value of blank fields",
                    "type": "string",
                    "isRequired": false,
                    "default": "",
                    "namedEnum": [
                        {
                            "name": "Empty String",
                            "value": ""
                        },
                        {
                            "name": "\"\"",
                            "value": "\"\""
                        },
                        {
                            "name": "null",
                            "value": "null"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "nullValue",
                    "title": "Null Value",
                    "description": "Select the output value of 'null' fields",
                    "type": "string",
                    "isRequired": false,
                    "default": "null",
                    "namedEnum": [
                        {
                            "name": "Empty String",
                            "value": ""
                        },
                        {
                            "name": "\"\"",
                            "value": "\"\""
                        },
                        {
                            "name": "null",
                            "value": "null"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                }
```

### Gruppieren der Dateiformatierungsoptionen {#grouping}

Sie können mehrere Dateiformatierungsoptionen in einem Abschnitt gruppieren. Beim Einrichten der Verbindung zum Ziel in der Benutzeroberfläche kann der Benutzer eine visuelle Gruppierung ähnlicher Felder sehen und davon profitieren.

Verwenden Sie dazu `"type": "object"` , um die Gruppe zu erstellen und die gewünschten Dateiformatierungsoptionen innerhalb einer `properties` -Parameter, wie im folgenden Beispiel gezeigt, wobei die Gruppierung **[!UICONTROL CSV-Optionen]** hervorgehoben ist.

```json
        {
            "name": "csvOptions",
            "title": "CSV Options",
            "description": "Select your CSV options",
            "type": "object",
            "properties": [
                {
                    "name": "delimiter",
                    "title": "Delimiter",
                    "description": "Select your Delimiter",
                    "type": "string",
                    "isRequired": false,
                    "default": ",",
                    "namedEnum": [
                        {
                            "name": "Comma (,)",
                            "value": ","
                        },
                        {
                            "name": "Tab (\\t)",
                            "value": "\t"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },

[...]
```

![Bild mit der Gruppierung der CSV-Optionen in der Benutzeroberfläche.](/help/destinations/destination-sdk/assets/guides/batch/file-formatting-grouping.png)

### Erstellen von Dropdown-Selektoren für Dateiformatierungsoptionen {#dropdown-selectors}

In Situationen, in denen Sie Benutzern die Auswahl zwischen verschiedenen Optionen ermöglichen möchten, z. B. welche Zeichen zum Trennen der Felder in CSV-Dateien verwendet werden sollen, können Sie Dropdown-Felder zur Benutzeroberfläche hinzufügen.

Verwenden Sie dazu die `namedEnum` -Objekt wie unten gezeigt und konfigurieren Sie eine `default` für die Optionen, die der Benutzer auswählen kann.

```json
{
   "name": "delimiter",
   "type": "string",
   "title": "Delimiter",
   "description": "Select your Delimiter",
   "namedEnum": [
   {
      "name": "Comma (,)",
      "value": ","
   },
   {
      "name": "Tab (\\t)",
      "value": "\t"
   }
   ],
   "default": ","
},
```

![Bildschirmaufzeichnung mit einem Beispiel für Dropdown-Selektoren, die mit der oben gezeigten Konfiguration erstellt wurden.](/help/destinations/destination-sdk/assets/guides/batch/dropdown-options-file-formatting.gif)

### Optionen zum Formatieren bedingter Dateien erstellen {#conditional-options}

Sie können bedingte Dateiformatierungsoptionen erstellen, die im Aktivierungs-Workflow nur angezeigt werden, wenn der Benutzer einen bestimmten Dateityp zum Export auswählt. Die folgende Konfiguration erstellt beispielsweise eine bedingte Gruppierung für CSV-Dateioptionen. Die CSV-Dateioptionen werden nur angezeigt, wenn der Benutzer CSV als gewünschten Dateityp für den Export auswählt.

Um ein Feld als bedingt festzulegen, verwenden Sie die `conditional` -Parameter wie unten gezeigt:

```json
            "conditional": {
                "field": "fileType",
                "operator": "EQUALS",
                "value": "CSV"
            }
```

In einem größeren Kontext können Sie die `conditional` -Feld, das in der folgenden Zielkonfiguration verwendet wird, neben dem `fileType` und `csvOptions` -Objekt, in dem es definiert ist.

```json
        {
            "name": "fileType",
            "title": "File Type",
            "description": "Select your file type",
            "type": "string",
            "isRequired": true,
            "enum": [
                "PARQUET",
                "CSV",
                "JSON"
            ],
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "csvOptions",
            "title": "CSV Options",
            "description": "Select your CSV options",
            "type": "object",
            "conditional": {
                "field": "fileType",
                "operator": "EQUALS",
                "value": "CSV"
            },            
            "properties": [
                {
                    "name": "delimiter",
                    "title": "Delimiter",
                    "description": "Select your Delimiter",
                    "type": "string",
                    "isRequired": false,
                    "default": ",",
                    "namedEnum": [
                        {
                            "name": "Comma (,)",
                            "value": ","
                        },
                        {
                            "name": "Tab (\\t)",
                            "value": "\t"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "quote",
                    "title": "Quote Character",
                    "description": "Select your Quote character",
                    "type": "string",
                    "isRequired": false,
                    "default": "",
                    "namedEnum": [
                        {
                            "name": "Double Quotes (\")",
                            "value": "\""
                        },
                        {
                            "name":"Null Character (\u0000)",
                            "value": "\u0000"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "escape",
                    "title": "Escape Character",
                    "description": "Select your Escape character",
                    "type": "string",
                    "isRequired": false,
                    "default": "\\",
                    "namedEnum": [
                        {
                            "name": "Back Slash (\\)",
                            "value": "\\"
                        },
                        {
                            "name": "Single Quote (')",
                            "value": "'"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "emptyValue",
                    "title": "Empty Value",
                    "description": "Select the output value of blank fields",
                    "type": "string",
                    "isRequired": false,
                    "default": "",
                    "namedEnum": [
                        {
                            "name": "Empty String",
                            "value": ""
                        },
                        {
                            "name": "\"\"",
                            "value": "\"\""
                        },
                        {
                            "name": "null",
                            "value": "null"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "nullValue",
                    "title": "Null Value",
                    "description": "Select the output value of 'null' fields",
                    "type": "string",
                    "isRequired": false,
                    "default": "null",
                    "namedEnum": [
                        {
                            "name": "Empty String",
                            "value": ""
                        },
                        {
                            "name": "\"\"",
                            "value": "\"\""
                        },
                        {
                            "name": "null",
                            "value": "null"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                }
            ],
            "isRequired": false,
            "readOnly": false,
            "hidden": false
        }
```

Unten sehen Sie den resultierenden Bildschirm der Benutzeroberfläche, der auf der oben beschriebenen Konfiguration basiert. Wenn der Benutzer den Dateityp CSV auswählt, werden in der Benutzeroberfläche zusätzliche Dateiformatierungsoptionen angezeigt, die auf den CSV-Dateityp verweisen.

![Bildschirmaufzeichnung mit der Option zur Formatierung bedingter Dateien für CSV-Dateien.](/help/destinations/destination-sdk/assets/guides/batch/conditional-file-formatting.gif)

### Vollständige API-Anfrage mit allen oben aufgeführten Optionen

Die nachstehende API-Anfrage kombiniert in einer Konfiguration alle in den obigen Abschnitten beschriebenen Optionen.

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
  "name": "My S3 Destination",
  "description": "Test destination",
  "releaseNotes": "Test destination",
  "status": "TEST",
  "sources": [
    "UNIFIED_PROFILE"
  ],
  "customerAuthenticationConfigurations": [
    {
      "authType": "S3"
    }
  ],
  "customerDataFields": [
    {
      "name": "bucket",
      "type": "string",
      "title": "Bucket",
      "description": "Enter your S3 Bucket",
      "isRequired": true
    },
    {
      "name": "path",
      "type": "string",
      "title": "Path",
      "description": "Enter your S3 Path",
      "isRequired": true
    },
    {
      "name": "fileType",
      "type": "string",
      "enum": [
        "CSV",
        "JSON",
        "PARQUET"
      ],
      "title": "File Type",
      "description": "Select your file type",
      "isRequired": true
    },
    {
      "name": "csvOptions",
      "type": "object",
      "title": "CSV Options",
      "description": "Select your CSV options",
      "conditional": {
        "field": "fileType",
        "operator": "EQUALS",
        "value": "CSV"
      },
      "properties": [
        {
          "name": "delimiter",
          "type": "string",
          "title": "Delimiter",
          "description": "Select your Delimiter",
          "namedEnum": [
            {
              "name": "Comma (,)",
              "value": ","
            },
            {
              "name": "Tab (\\t)",
              "value": "\t"
            }
          ],
          "default": ","
        },
        {
          "name": "quote",
          "type": "string",
          "title": "Quote Character",
          "description": "Select your Quote character",
          "namedEnum": [
            {
              "name": "Double Quotes (\")",
              "value": "\""
            },
            {
              "name": "Null Character (\\u0000)",
              "value": "\u0000"
            }
          ],
          "default": "\u0000"
        },
        {
          "name": "escape",
          "type": "string",
          "title": "Escape Character",
          "description": "Select your Escape character",
          "namedEnum": [
            {
              "name": "Back Slash (\\)",
              "value": "\\"
            },
            {
              "name": "Single Quote (')",
              "value": "'"
            }
          ],
          "default": "\\"
        },
        {
          "name": "emptyValue",
          "type": "string",
          "title": "Empty Value",
          "description": "Select the output value of blank fields",
          "namedEnum": [
            {
              "name": "null",
              "value": "null"
            },
            {
              "name": "Empty String",
              "value": ""
            },
            {
              "name": "\"\"",
              "value": "\"\""
            }
          ],
          "default": ""
        },
        {
          "name": "nullValue",
          "type": "string",
          "title": "Null Value",
          "description": "Select the output value of 'null' fields",
          "namedEnum": [
            {
              "name": "null",
              "value": "null"
            },
            {
              "name": "Empty String",
              "value": ""
            },
            {
              "name": "\"\"",
              "value": "\"\""
            }
          ],
          "default": "null"
        }
      ]
    }
  ],
  "uiAttributes": {
    "documentationLink": "https://www.adobe.com/go/aep",
    "category": "cloudStorage",
    "connectionType": "Server-to-server",
    "frequency": "Batch",
    "monitoringSupported": true,
    "flowRunsSupported": true
  },
  "schemaConfig": {
    "profileRequired": true,
    "segmentRequired": true,
    "identityRequired": true
  },
  "batchConfig": {
    "allowMandatoryFieldSelection": true,
    "allowDedupeKeyFieldSelection": true,
    "defaultExportMode": "DAILY_FULL_EXPORT",
    "allowedExportMode": [
      "DAILY_FULL_EXPORT",
      "FIRST_FULL_THEN_INCREMENTAL"
    ],
    "allowedScheduleFrequency": [
      "DAILY",
      "EVERY_3_HOURS",
      "EVERY_6_HOURS",
      "EVERY_8_HOURS",
      "EVERY_12_HOURS",
      "ONCE"
    ],
    "defaultFrequency": "DAILY",
    "defaultStartTime": "00:00",
    "filenameConfig": {
      "allowedFilenameAppendOptions": [
        "SEGMENT_NAME",
        "DESTINATION_INSTANCE_ID",
        "DESTINATION_INSTANCE_NAME",
        "ORGANIZATION_NAME",
        "SANDBOX_NAME",
        "DATETIME",
        "CUSTOM_TEXT"
      ],
      "defaultFilenameAppendOptions": [
        "DATETIME"
      ],
      "defaultFilename": "%DESTINATION%_%SEGMENT_ID%"
    }
  },
  "destinationDelivery": [
    {
      "deliveryMatchers": [
        {
          "type": "SOURCE",
          "value": [
            "batch"
          ]
        }
      ],
      "authenticationRule": "CUSTOMER_AUTHENTICATION",
      "destinationServerId": "<server-id>"
    }
  ]
}'
```

Eine erfolgreiche Antwort gibt die Zielkonfiguration zurück, einschließlich der eindeutigen Kennung (`instanceId`) der Konfiguration.

## Bekannte Einschränkungen {#known-limitations}

Eine bestimmte Kombination von Dateiformatierungsoptionen kann zu unerwünschten Dateiexportergebnissen führen.
Adobe empfiehlt, die folgende Kombination von CSV-Optionen nicht auszuwählen:

```
nullValue -> ""
quote -> "
emptyValue -> ""
```

Betrachten Sie zum Beispiel den Export einer Datei mit den folgenden Werten:

| firstname | lastname | country | state |
|---------|----------|---------|--------|
| Michael | Rose | USA | NY |
| James | Smith |  | null |

{style=&quot;table-layout:auto&quot;}

Dies würde zu einer Ausgabe führen, wie unten dargestellt. Beachten Sie, dass der Nullwert aus der Tabelle fälschlicherweise als maskiertes Anführungszeichen exportiert wird.

```csv
Michael,Rose,USA,NY 
James,Smith,"","\"\""
```

## Nächste Schritte {#next-steps}

Durch Lesen dieses Artikels wissen Sie jetzt, wie Sie benutzerdefinierte Dateiformatierungsoptionen für Ihre exportierten Dateien mithilfe von Destination SDK einrichten. Als Nächstes kann Ihr Team die [Aktivierungs-Workflow für dateibasierte Ziele](../../../ui/activate-batch-profile-destinations.md) , um Daten an das Ziel zu exportieren.
