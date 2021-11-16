---
keywords: Experience Platform; Startseite; beliebte Themen; Quellen; Connectoren; Quell-Connectoren; Quellen-SDK; SDK
title: Konfigurieren von Erkundungsspezifikationen für das Quellen-SDK
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über die Konfigurationen, die Sie für die Verwendung des Sources-SDK vorbereiten müssen.
hide: true
hidefromtoc: true
source-git-commit: d98cf404fd1a4d150f202154aba87b0089418957
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 2%

---


# Konfigurieren von Erkundungsspezifikationen für das Quellen-SDK

Mithilfe der Spezifikationen werden die Parameter definiert, die zum Erkunden und Überprüfen der in Ihrer Quelle enthaltenen Objekte erforderlich sind. Mithilfe von Erkunden-Spezifikationen wird auch das Antwortformat definiert, das zurückgegeben wird, wenn Objekte untersucht und untersucht werden.

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
| `requestSpec.type` | Definiert den Datentyp der Anforderungsspezifikation. | `object` |
| `responseSpec` | Enthält die Parameter, die das Format der Antwortnachricht definieren, die bei einem Erkundungsaufruf zurückgegeben wird. |
| `responseSpec.type` | Definiert den Datentyp der Antwortspezifikation. | `object` |
| `responseSpec.properties` | Enthält Informationen zur Formatierung der Antwortnachricht. |
| `responseSpec.properties.format` | Definiert die Formatierung des Antwortschemas. | `object` |
| `responseSpec.properties.format.type` | Definiert den Datentyp von Eigenschaften. | `string` |
| `responseSpec.schema` | Enthält Informationen zur Formatierung des Antwortschemas. |
| `responseSpec.schema.type` | Definiert den Datentyp des Schemas. | `object` |
| `responseSpec.schema.properties` | Enthält Informationen zu den Spalten, dem Typ und den Elementen, die in einem Schema gespeichert sind. |
| `responseSpec.schema.properties.columns.items.properties.name` | Zeigt den Namen der Datei an. |
| `responseSpec.schema.properties.columns.items.properties.name.type` | Definiert den Datentyp des Dateinamens. | `string` |

{style=&quot;table-layout:auto&quot;}

## Nächste Schritte

Nachdem Sie Ihre Erkundungsspezifikationen ausgefüllt haben, können Sie mit der Erstellung einer vollständigen Verbindungsspezifikation mit dem [!DNL Flow Service] API. Siehe [[!DNL Sources SDK] API-Handbuch](../api/api-overview.md) für weitere Informationen.