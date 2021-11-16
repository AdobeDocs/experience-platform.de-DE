---
keywords: Experience Platform; Startseite; beliebte Themen; Quellen; Connectoren; Quell-Connectoren; Quellen-SDK; SDK
title: Konfigurieren von Erkundungsspezifikationen für das Quellen-SDK
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über die Konfigurationen, die Sie für die Verwendung des Sources-SDK vorbereiten müssen.
hide: true
hidefromtoc: true
source-git-commit: ae1a1139c24fd80e9f689e4c637897c905004c5f
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 2%

---


# Configure explore specifications for Sources SDK

Explore specifications defines the parameters required for exploring and inspecting objects contained in your source. Mithilfe von Erkunden-Spezifikationen wird auch das Antwortformat definiert, das zurückgegeben wird, wenn Objekte untersucht und untersucht werden.

>[!TIP]
>
>Die Analysespezifikationen sind hartcodiert und Sie können die unten stehende Payload einfach kopieren und in Ihre Verbindungsspezifikation einfügen.

```json
"exploreSpec": {
  "name": "Resource",
  "type": "Resource",
  "requestSpec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object"
  },
  "responseSpec": {
    "$schema": "http: //json-schema.org/draft-07/schema#",
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
```

| Spezifikationen | Beschreibung | Beispiel |
| --- | --- | --- |
| `name` | Definiert den Namen oder die Kennung der Analysespezifikation. | `Resource` |
| `type` | Definiert den Typ der Analysespezifikation. | `Resource` |
| `requestSpec` | Enthält die Parameter, die zum Erkunden von Objekten in der Verbindung erforderlich sind. |
| `requestSpec.type` | Defines the data type of the request specification. | `object` |
| `responseSpec` | Enthält die Parameter, die das Format der Antwortnachricht definieren, die bei einem Erkundungsaufruf zurückgegeben wird. |
| `responseSpec.type` | Definiert den Datentyp der Antwortspezifikation. | `object` |
| `responseSpec.properties` | Enthält Informationen zur Formatierung der Antwortnachricht. |
| `responseSpec.properties.format` | Defines the formatting of the response schema. | `object` |
| `responseSpec.properties.format.type` | Definiert den Datentyp von Eigenschaften. | `string` |
| `responseSpec.schema` | Enthält Informationen zur Formatierung des Antwortschemas. |
| `responseSpec.schema.type` | Definiert den Datentyp des Schemas. | `object` |
| `responseSpec.schema.properties` | Enthält Informationen zu den Spalten, dem Typ und den Elementen, die in einem Schema gespeichert sind. |
| `responseSpec.schema.properties.columns.items.properties.name` | Displays the name of the file. |
| `responseSpec.schema.properties.columns.items.properties.name.type` | Defines the data type of the file name. | `string` |

{style=&quot;table-layout:auto&quot;}

## Nächste Schritte

Nachdem Sie Ihre Erkundungsspezifikationen ausgefüllt haben, können Sie mit der Erstellung einer vollständigen Verbindungsspezifikation mit dem [!DNL Flow Service] API. See the the [[!DNL Sources SDK] API guide](../api/api-overview.md) for more information.