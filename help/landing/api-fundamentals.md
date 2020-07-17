---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Grundlagen der Adobe Experience Platform-API
topic: getting started
translation-type: tm+mt
source-git-commit: f910351d49de9c4a18a444b99b7f102f4ce3ed5b
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 66%

---


# Grundlagen der Adobe Experience Platform-API

Adobe Experience Platform APIs employ several underlying technologies and syntaxes that are important to understand in order to effectively manage JSON-based [!DNL Platform] resources. Dieses Dokument bietet einen kurzen Überblick über diese Technologien sowie Links zur externen Dokumentation für weitere Informationen.

## JSON Pointer {#json-pointer}

JSON Pointer ist eine standardisierte Zeichenfolgensyntax ([RFC 6901](https://tools.ietf.org/html/rfc6901)) zur Identifizierung bestimmter Werte in JSON-Dokumenten. Ein JSON Pointer ist eine Zeichenfolge aus Token, die durch `/`-Zeichen getrennt sind und entweder Objektschlüssel oder Array-Indizes angeben. Die Token können eine Zeichenfolge oder eine Zahl sein. JSON Pointer strings are used in many PATCH operations for [!DNL Platform] APIs, as described later in this document. Weitere Informationen zu JSON Pointer finden Sie in der Dokumentation [JSON Pointer – Überblick](https://rapidjson.org/md_doc_pointer.html).

### Beispiel für ein JSON-Schema-Objekt

```json
{
    "type": "object",
    "title": "Loyalty Member Details",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Loyalty Program Mixin.",
    "definitions": {
        "loyalty": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "loyaltyId": {
                            "title": "Loyalty Identifier",
                            "type": "string",
                            "description": "Loyalty Identifier.",
                            "meta:xdmType": "string"
                        },
                        "loyaltyLevel": {
                            "title": "Loyalty Level",
                            "description": "The current loyalty program level to which the individual member belongs.",
                            "type": "string",
                            "enum": [
                                "platinum",
                                "gold",
                                "silver",
                                "bronze"
                            ],
                            "meta:enum": {
                                "platinum": "Platinum",
                                "gold": "Gold",
                                "silver": "Silver",
                                "bronze": "Bronze"
                            },
                            "meta:xdmType": "string"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    }
}
```

### Beispiel für JSON Pointer, die auf dem Schema-Objekt basieren

| JSON Pointer | wird zu |
|--- | ---|
| `"/title"` | „Details zu Loyalitätsmitgliedern“ |
| `"/definitions/loyalty"` | (Gibt den Inhalt des `loyalty`-Objekts zurück) |
| `"/definitions/loyalty/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/definitions/loyalty/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NHinweis]
>
>
>When dealing with the `xdm:sourceProperty` and `xdm:destinationProperty` attributes of [!DNL Experience Data Model] (XDM) descriptors, any `properties` keys must be **excluded** from the JSON Pointer string. See the [!DNL Schema Registry] API developer guide sub-guide on [descriptors](../xdm/api/descriptors.md) for more information.

## JSON Patch

There are many PATCH operations for [!DNL Platform] APIs that accept JSON Patch objects for their request payloads. JSON Patch ist ein standardisiertes Format ([RFC 6902](https://tools.ietf.org/html/rfc6902)) zur Beschreibung von Änderungen an einem JSON-Dokument. Damit können Sie Teilaktualisierungen zu JSON definieren, ohne das gesamte Dokument in einem Anfragetext senden zu müssen.

### Beispiel für ein JSON Patch-Objekt

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`: Die Art des Patch-Vorgangs. While JSON Patch supports several different operation types, not all PATCH operations in [!DNL Platform] APIs are compatible with every operation type. Verfügbare Vorgangsarten sind:
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`: Der Teil der zu aktualisierenden JSON-Struktur, der mit der [JSON Pointer](#json-pointer)-Notation identifiziert wird.

Je nach der in `op` angegebenen Vorgangsart benötigt das JSON Patch-Objekt möglicherweise zusätzliche Eigenschaften. Weitere Informationen zu den verschiedenen JSON Patch-Vorgängen und deren benötigter Syntax finden Sie in der [JSON Patch-Dokumentation](http://jsonpatch.com/).

## JSON-Schema

JSON-Schema ist ein Format, mit dem die Struktur von JSON-Daten beschrieben und validiert wird. Das [Experience Data Model (XDM)](../xdm/home.md) nutzt JSON-Schema-Funktionen, um Beschränkungen in Bezug auf die Struktur und das Format der aufgenommenen Kundenerlebnisdaten zu erzwingen. Weitere Informationen zum JSON-Schema finden Sie in der [offiziellen Dokumentation](https://json-schema.org/).

## Nächste Schritte

This document introduced some of the technologies and syntaxes involved with managing JSON-based resources for [!DNL Experience Platform]. For more information on working with [!DNL Platform] APIs, including best practices and answers to frequently asked questions, refer to the [Platform troubleshooting guide](troubleshooting.md).