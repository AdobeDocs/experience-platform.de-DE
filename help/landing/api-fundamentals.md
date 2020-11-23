---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Grundlagen der Adobe Experience Platform-API
topic: getting started
translation-type: tm+mt
source-git-commit: b6d62492a60494deb848a88a9334e3ef20a93919
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 56%

---


# Grundlagen der Adobe Experience Platform-API

Adobe Experience Platform APIs employ several underlying technologies and syntaxes that are important to understand in order to effectively manage JSON-based [!DNL Platform] resources. Dieses Dokument bietet einen kurzen Überblick über diese Technologien sowie Links zur externen Dokumentation für weitere Informationen.

## JSON Pointer {#json-pointer}

JSON Pointer ist eine standardisierte Zeichenfolgensyntax ([RFC 6901](https://tools.ietf.org/html/rfc6901)) zur Identifizierung bestimmter Werte in JSON-Dokumenten. Ein JSON Pointer ist eine Zeichenfolge aus Token, die durch `/`-Zeichen getrennt sind und entweder Objektschlüssel oder Array-Indizes angeben. Die Token können eine Zeichenfolge oder eine Zahl sein. JSON Pointer strings are used in many PATCH operations for [!DNL Platform] APIs, as described later in this document. Weitere Informationen zu JSON Pointer finden Sie in der Dokumentation [JSON Pointer – Überblick](https://rapidjson.org/md_doc_pointer.html).

### Beispiel für ein JSON-Schema-Objekt

Das folgende JSON stellt ein vereinfachtes XDM-Schema dar, dessen Felder mit JSON-Zeigerzeichenfolgen referenziert werden können. Beachten Sie, dass alle Felder, die mit benutzerdefinierten Mixins hinzugefügt wurden (z. B. `loyaltyLevel`), unter einem `_{TENANT_ID}` Objekt benannt werden, während Felder, die mit Core Mixins hinzugefügt wurden (z. B. `fullName`), nicht benannt werden.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/85a4bdaa168b01bf44384e049fbd3d2e9b2ffaca440d35b9",
  "meta:altId": "_{TENANT_ID}.schemas.85a4bdaa168b01bf44384e049fbd3d2e9b2ffaca440d35b9",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "Example schema",
  "type": "object",
  "description": "This is an example schema.",
  "properties": {
    "_{TENANT_ID}": {
      "type": "object",
      "properties": {
        "loyaltyLevel": {
          "title": "Loyalty Level",
          "description": "",
          "type": "string",
          "isRequired": false,
          "enum": [
            "platinum",
            "gold",
            "silver",
            "bronze"
          ]
        }
      }
    },
    "person": {
      "title": "Person",
      "description": "An individual actor, contact, or owner.",
      "type": "object",
      "properties": {
        "name": {
          "title": "Full name",
          "description": "The person's full name.",
          "type": "object",
          "properties": {
            "fullName": {
              "title": "Full name",
              "type": "string",
              "description": "The full name of the person, in writing order most commonly accepted in the language of the name.",
            },
            "suffix": {
              "title": "Suffix",
              "type": "string",
              "description": "A group of letters provided after a person's name to provide additional information. The `suffix` is used at the end of someones name. For example Jr., Sr., M.D., PhD, I, II, III, etc.",
            }
          },
          "meta:referencedFrom": "https://ns.adobe.com/xdm/context/person-name",
          "meta:xdmField": "xdm:name"
        }
      }
    }
  }
}
```

### Beispiel für JSON Pointer, die auf dem Schema-Objekt basieren

| JSON Pointer | wird zu |
| --- | --- |
| `"/title"` | `"Example schema"` |
| `"/properties/person/properties/name/properties/fullName"` | (Gibt einen Verweis auf das `fullName` Feld zurück, der von einer Core-Mixin bereitgestellt wird.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | (Gibt einen Verweis auf das `loyaltyLevel` Feld zurück, der von einem benutzerdefinierten Mixin bereitgestellt wird.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>When dealing with the `xdm:sourceProperty` and `xdm:destinationProperty` attributes of [!DNL Experience Data Model] (XDM) descriptors, any `properties` keys must be **excluded** from the JSON Pointer string. See the [!DNL Schema Registry] API developer guide sub-guide on [descriptors](../xdm/api/descriptors.md) for more information.

## JSON Patch {#json-patch}

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