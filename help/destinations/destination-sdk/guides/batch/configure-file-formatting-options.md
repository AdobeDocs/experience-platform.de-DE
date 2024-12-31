---
description: Konfigurieren von Dateiformatierungsoptionen für dateibasierte Ziele
title: Erfahren Sie, wie Sie mit Destination SDK Dateiformatierungsoptionen für dateibasierte Ziele konfigurieren.
exl-id: e61c7989-1123-4b3b-9781-a6097cd0e2b4
source-git-commit: d47c82339afa602a9d6914c1dd36a4fc9528ea32
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 22%

---

# Konfigurieren von Dateiformatierungsoptionen für dateibasierte Ziele

## Übersicht {#overview}

Destination SDK ermöglicht es Ihnen, die Formatierungs- und Komprimierungsoptionen Ihrer exportierten Dateien umfassend an alle nachgelagerten Anforderungen Ihres Speicherorts anzupassen.

Auf dieser Seite wird beschrieben, wie Sie mit Destination SDK Dateiformatierungsoptionen für dateibasierte Ziele konfigurieren können.

## Voraussetzungen {#prerequisites}

Bevor Sie mit den unten beschriebenen Schritten fortfahren, informieren Sie sich auf der Seite [Erste Schritte ](../../getting-started.md) Destination SDK , wie Sie die erforderlichen Adobe I/O-Authentifizierungsdaten und andere Voraussetzungen für die Arbeit mit Destination SDK-APIs erhalten.

Adobe empfiehlt außerdem, die folgende Dokumentation zu lesen und sich damit vertraut zu machen, bevor Sie fortfahren:

* Jede verfügbare Dateiformatierungsoption wird ausführlich im Abschnitt [Dateiformatierungskonfiguration“ ](../../functionality/destination-server/file-formatting.md).
* Führen Sie die Schritte aus[ um ein dateibasiertes Ziel mithilfe ](../../guides/configure-file-based-destination-instructions.md) -Destination SDK zu konfigurieren.

## Erstellen einer Server- und Dateikonfiguration {#create-server-file-configuration}

Verwenden Sie zunächst den Endpunkt `/destination-server` , um zu bestimmen, welche Dateiformatierungskonfigurationsoptionen Sie für die exportierten Dateien einrichten möchten.

Nachfolgend finden Sie ein Beispiel für eine Ziel-Server-Konfiguration für ein [!DNL Amazon S3]-Ziel mit mehreren ausgewählten Dateiformatierungsoptionen.

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
>**Überprüfen Sie die Experience Platform-Benutzeroberfläche**. Wenn Sie die Dateiformatierungsoptionen mit den in den folgenden Abschnitten demonstrierten Konfigurationen konfigurieren, sollten Sie in der Experience Platform-Benutzeroberfläche überprüfen, wie diese Optionen gerendert werden.

Nachdem Sie im vorherigen Schritt die gewünschten Dateiformatierungsoptionen zum Ziel-Server und zur Dateiformatierungskonfiguration hinzugefügt haben, können Sie jetzt den API-Endpunkt `/destinations` verwenden, um die gewünschten Felder als Kundendatenfelder zur Zielkonfiguration hinzuzufügen.

>[!IMPORTANT]
>
>Dieser Schritt ist optional und bestimmt nur, welche der Dateiformatierungsoptionen Benutzenden in der Experience Platform-Benutzeroberfläche angezeigt werden sollen. Wenn Sie keine Dateiformatierungsoptionen als Kundendatenfelder einrichten, werden die Dateiexporte mit den Standardwerten fortgesetzt, die in der [Server- und Dateikonfiguration“ konfiguriert ](#create-server-file-configuration).

In diesem Schritt können Sie die angezeigten Optionen in beliebiger Reihenfolge gruppieren sowie benutzerdefinierte Gruppierungen, Dropdown-Felder und bedingte Gruppierungen basierend auf den ausgewählten Dateitypen erstellen. Alle diese Einstellungen werden bei der Aufzeichnung und in den weiter unten stehenden Abschnitten angezeigt.

![Bildschirmaufzeichnung mit verschiedenen Dateiformatierungsoptionen für Batch-Dateien.](../../assets/guides/batch/file-formatting-options.gif)

### Sortieren der Dateiformatierungsoptionen {#ordering}

Die Reihenfolge, in der Sie die Dateiformatierungsoptionen als Kundendatenfelder in der Zielkonfiguration hinzufügen, wird in der Benutzeroberfläche angezeigt. Beispielsweise wird die folgende Konfiguration entsprechend in der Benutzeroberfläche angezeigt, wobei die Optionen in der Reihenfolge **[!UICONTROL Trennzeichen]**, **[!UICONTROL Anführungszeichen]**, **[!UICONTROL Escape-Zeichen]**, **[!UICONTROL Leerer Wert]**, **[!UICONTROL Null-Wert]**.

![Bild, das die Reihenfolge der Dateiformatierungsoptionen in der Experience Platform-Benutzeroberfläche anzeigt.](../../assets/guides/batch/file-formatting-order.png)

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

Verwenden Sie dazu `"type": "object"`, um die Gruppe zu erstellen, und fassen Sie die gewünschten Dateiformatierungsoptionen in einem `properties`-Parameter zusammen, wie im folgenden Beispiel gezeigt, wobei die Gruppierung **[!UICONTROL CSV-Optionen]** hervorgehoben ist.

```json {line-numbers="true" start-number="100" highlight="106-128"}
"customerDataFields":[
[...]
{
   "name":"csvOptions",
   "title":"CSV Options",
   "description":"Select your CSV options",
   "type":"object",
   "properties":[
      {
         "name":"delimiter",
         "title":"Delimiter",
         "description":"Select your Delimiter",
         "type":"string",
         "isRequired":false,
         "default":",",
         "namedEnum":[
            {
               "name":"Comma (,)",
               "value":","
            },
            {
               "name":"Tab (\\t)",
               "value":"\t"
            }
         ],
         "readOnly":false,
         "hidden":false
      },
      [...]
   ]
}
[...]
]
```

![Bild mit den CSV-Optionen, die in der Benutzeroberfläche gruppiert werden.](../../assets/guides/batch/file-formatting-grouping.png)

### Erstellen von Dropdown-Selektoren für die Dateiformatierungsoptionen {#dropdown-selectors}

In Situationen, in denen Sie Benutzerinnen und Benutzern die Auswahl zwischen verschiedenen Optionen ermöglichen möchten, z. B. welche Zeichen zum Trennen der Felder in CSV-Dateien verwendet werden sollen, können Sie Dropdown-Felder zur Benutzeroberfläche hinzufügen.

Verwenden Sie dazu das `namedEnum`-Objekt wie unten gezeigt und konfigurieren Sie einen `default`-Wert für die Optionen, die Benutzerinnen und Benutzer auswählen können.

```json {line-numbers="true" start-number="100" highlight="114-124"}
[...]
"customerDataFields":[
[...]
{
   "name":"csvOptions",
   "title":"CSV Options",
   "description":"Select your CSV options",
   "type":"object",
   "properties":[
      {
         "name":"delimiter",
         "title":"Delimiter",
         "description":"Select your Delimiter",
         "type":"string",
         "isRequired":false,
         "default":",",
         "namedEnum":[
            {
               "name":"Comma (,)",
               "value":","
            },
            {
               "name":"Tab (\\t)",
               "value":"\t"
            }
         ],
         "readOnly":false,
         "hidden":false
      },
      [...]
   ]
}
[...]
]
```

![Bildschirmaufzeichnung mit einem Beispiel für Dropdown-Selektoren, die mit der oben gezeigten Konfiguration erstellt wurden.](../../assets/guides/batch/dropdown-options-file-formatting.gif)

### Erstellen bedingter Dateiformatierungsoptionen {#conditional-options}

Sie können bedingte Dateiformatierungsoptionen erstellen, die im Aktivierungs-Workflow nur angezeigt werden, wenn Benutzende einen bestimmten Dateityp für den Export auswählen. Beispielsweise erstellt die folgende Konfiguration eine bedingte Gruppierung für CSV-Dateioptionen. Die CSV-Dateioptionen werden nur angezeigt, wenn Benutzerinnen oder Benutzer CSV als gewünschten Dateityp für den Export auswählen.

Um ein Feld als bedingt festzulegen, verwenden Sie den Parameter `conditional` wie unten gezeigt:

```json
            "conditional": {
                "field": "fileType",
                "operator": "EQUALS",
                "value": "CSV"
            }
```

In einem größeren Kontext können Sie das Feld `conditional`, das in der folgenden Zielkonfiguration verwendet wird, neben der Zeichenfolge `fileType` und dem `csvOptions`-Objekt sehen, in dem es definiert ist.

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

Unten sehen Sie den resultierenden Bildschirm der Benutzeroberfläche, der auf der oben beschriebenen Konfiguration basiert. Wenn die Benutzerinnen oder Benutzer den Dateityp CSV auswählen, werden in der Benutzeroberfläche zusätzliche Dateiformatierungsoptionen angezeigt, die sich auf den CSV-Dateityp beziehen.

![Bildschirmaufzeichnung mit der bedingten Option zur Dateiformatierung für CSV-Dateien.](../../assets/guides/batch/conditional-file-formatting.gif)

### Vollständige API-Anfrage, die alle oben angezeigten Optionen enthält

Die folgende API-Anfrage kombiniert in einer Konfiguration alle Optionen, die in den obigen Abschnitten beschrieben werden.

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

Bei einer erfolgreichen Antwort wird die Zielkonfiguration zurückgegeben, einschließlich der eindeutigen Kennung (`instanceId`) der Konfiguration.

## Bekannte Einschränkungen {#known-limitations}

Eine bestimmte Kombination von Dateiformatierungsoptionen kann zu unerwünschten Ergebnissen beim Dateiexport führen.
Adobe empfiehlt, nicht die folgende Kombination von CSV-Optionen auszuwählen:

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

{style="table-layout:auto"}

Dies würde wie unten dargestellt zu einer Ausgabe führen. Beachten Sie, dass der Nullwert aus der Tabelle fälschlicherweise als Escape-Anführungszeichen exportiert wird.

```csv
Michael,Rose,USA,NY 
James,Smith,"","\"\""
```

## Nächste Schritte {#next-steps}

Durch das Lesen dieses Artikels wissen Sie jetzt, wie Sie mithilfe von Destination SDK benutzerdefinierte Dateiformatierungsoptionen für Ihre exportierten Dateien einrichten können. Als Nächstes kann Ihr Team den [Aktivierungs-Workflow für dateibasierte Ziele“ verwenden](../../../ui/activate-batch-profile-destinations.md) um Daten an das Ziel zu exportieren.
