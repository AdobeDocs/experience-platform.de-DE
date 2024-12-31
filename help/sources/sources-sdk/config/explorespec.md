---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;Connectoren;Quell-Connectoren;Quellen-SDK;SDK
title: Konfigurieren von Erkundungsspezifikationen für Selbstbedienungsquellen (Batch-SDK)
description: Dieses Dokument bietet einen Überblick über die Konfigurationen, die Sie für die Verwendung von Selbstbedienungsquellen (Batch-SDK) vorbereiten müssen.
exl-id: 423a7e56-9dd1-4071-bd26-ee4f9f206122
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 6%

---

# Konfigurieren von Erkundungsspezifikationen für Selbstbedienungsquellen (Batch-SDK)

In den Erkundungsspezifikationen werden die Parameter definiert, die zum Untersuchen und Überprüfen von in der Quelle enthaltenen Objekten erforderlich sind. In den Analysespezifikationen wird auch das Antwortformat definiert, das zurückgegeben wird, wenn Objekte untersucht und geprüft werden.

>[!TIP]
>
>Erkunden-Spezifikationen sind hartcodiert und Sie können einfach die unten stehende Payload kopieren und in Ihre Verbindungsspezifikation einfügen.

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

| Erkunden von Spezifikationen | Beschreibung | Beispiel |
| --- | --- | --- |
| `name` | Definiert den Namen oder die Kennung der Erkundungsspezifikation. | `Resource` |
| `type` | Definiert den Typ der Explorationsspezifikation. | `Resource` |
| `requestSpec` | Enthält die Parameter, die erforderlich sind, um Objekte in der Verbindung zu untersuchen. |
| `requestSpec.type` | Definiert den Datentyp der Anfragespezifikation. | `object` |
| `responseSpec` | Enthält die Parameter, die das Format der Antwortnachricht definieren, die für einen Erkundungsaufruf zurückgegeben wird. |
| `responseSpec.type` | Definiert den Datentyp der Antwortspezifikation. | `object` |
| `responseSpec.properties` | Enthält Informationen zur Formatierung der Antwortnachricht. |
| `responseSpec.properties.format` | Definiert die Formatierung des Antwortschemas. | `object` |
| `responseSpec.properties.format.type` | Definiert den Datentyp der Eigenschaften. | `string` |
| `responseSpec.schema` | Enthält Informationen zur Formatierung des Antwortschemas. |
| `responseSpec.schema.type` | Definiert den Datentyp des Schemas. | `object` |
| `responseSpec.schema.properties` | Enthält Informationen zu den Spalten, dem Typ und den Elementen, die in einem Schema enthalten sind. |
| `responseSpec.schema.properties.columns.items.properties.name` | Zeigt den Namen der Datei an. |
| `responseSpec.schema.properties.columns.items.properties.name.type` | Definiert den Datentyp des Dateinamens. | `string` |

{style="table-layout:auto"}

## Nächste Schritte

Wenn Ihre Erkundungsspezifikationen ausgefüllt sind, können Sie mit der Erstellung einer vollständigen Verbindungsspezifikation mithilfe der [!DNL Flow Service]-API fortfahren. Weitere Informationen finden [ im API-Handbuch ](../api/api-overview.md) Selbstbedienungsquellen (Batch-SDK) .
