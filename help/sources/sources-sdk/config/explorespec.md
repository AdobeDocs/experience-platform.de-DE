---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;Connectoren;Quell-Connectoren;Quellen-SDK;SDK
title: Konfigurieren von Erkundungsspezifikationen für Self-Serve-Quellen (Batch-SDK)
description: Dieses Dokument bietet einen Überblick über die Konfigurationen, die Sie für die Verwendung von Self-Serve-Quellen (Batch SDK) vorbereiten müssen.
exl-id: 423a7e56-9dd1-4071-bd26-ee4f9f206122
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 6%

---

# Konfigurieren von Erkundungsspezifikationen für Self-Serve-Quellen (Batch-SDK)

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
| `name` | Definiert den Namen oder die Kennung der Explorationsspezifikation. | `Resource` |
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

{style="table-layout:auto"}

## Nächste Schritte

Nachdem Sie Ihre Analysespezifikationen ausgefüllt haben, können Sie mit der Erstellung einer vollständigen Verbindungsspezifikation mit der [!DNL Flow Service] -API fortfahren. Weitere Informationen finden Sie im API-Handbuch [Self-Serve-Sources (Batch SDK)](../api/api-overview.md) .
