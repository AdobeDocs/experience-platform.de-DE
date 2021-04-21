---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Grundlagen der Experience Platform-API
topic-legacy: getting started
description: In diesem Dokument erhalten Sie einen kurzen Überblick über einige der mit Experience Platform-APIs verbundenen Technologien und Syntaxen.
exl-id: cd69ba48-f78c-4da5-80d1-efab5f508756
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 52%

---

# Grundlagen der Experience Platform-API

Adobe Experience Platform-APIs verwenden verschiedene zugrunde liegende Technologien und Syntaxen, die für eine effektive Verwaltung der JSON-basierten [!DNL Platform]-Ressourcen wichtig sind. Dieses Dokument bietet einen kurzen Überblick über diese Technologien sowie Links zur externen Dokumentation für weitere Informationen.

## JSON Pointer {#json-pointer}

JSON Pointer ist eine standardisierte Zeichenfolgensyntax ([RFC 6901](https://tools.ietf.org/html/rfc6901)) zur Identifizierung bestimmter Werte in JSON-Dokumenten. Ein JSON Pointer ist eine Zeichenfolge aus Token, die durch `/`-Zeichen getrennt sind und entweder Objektschlüssel oder Array-Indizes angeben. Die Token können eine Zeichenfolge oder eine Zahl sein. JSON-Zeigerzeichenfolgen werden in vielen PATCH-Operationen für [!DNL Platform]-APIs verwendet, wie weiter unten in diesem Dokument beschrieben. Weitere Informationen zu JSON Pointer finden Sie in der Dokumentation [JSON Pointer – Überblick](https://rapidjson.org/md_doc_pointer.html).

### Beispiel für ein JSON-Schema-Objekt

Das folgende JSON stellt ein vereinfachtes XDM-Schema dar, dessen Felder mit JSON-Zeigerzeichenfolgen referenziert werden können. Beachten Sie, dass alle Felder, die mit benutzerdefinierten Mixins hinzugefügt wurden (z. B. `loyaltyLevel`), unter einem `_{TENANT_ID}`-Objekt benannt werden, während Felder, die mit Core Mixins (z. B. `fullName`) hinzugefügt wurden, nicht benannt werden.

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
| `"/properties/person/properties/name/properties/fullName"` | (Gibt einen Verweis auf das `fullName`-Feld zurück, das von einer Core-Mixin bereitgestellt wird.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | (Gibt einen Verweis auf das `loyaltyLevel`-Feld zurück, das von einem benutzerdefinierten Mixin bereitgestellt wird.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>Beim Umgang mit den Attributen `xdm:sourceProperty` und `xdm:destinationProperty` von [!DNL Experience Data Model] (XDM)-Deskriptoren müssen alle `properties`-Schlüssel **aus der JSON-Zeigerzeichenfolge ausgeschlossen werden.** Weitere Informationen finden Sie im Unterhandbuch [!DNL Schema Registry] API-Entwicklerhandbuch unter [Deskriptoren](../xdm/api/descriptors.md).

## JSON Patch {#json-patch}

Es gibt viele PATCH-Vorgänge für [!DNL Platform]-APIs, die JSON Patch-Objekte für ihre Anforderungsnutzdaten akzeptieren. JSON Patch ist ein standardisiertes Format ([RFC 6902](https://tools.ietf.org/html/rfc6902)) zur Beschreibung von Änderungen an einem JSON-Dokument. Damit können Sie Teilaktualisierungen zu JSON definieren, ohne das gesamte Dokument in einem Anfragetext senden zu müssen.

### Beispiel für ein JSON Patch-Objekt

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`: Die Art des Patch-Vorgangs. Während JSON Patch mehrere verschiedene Operationstypen unterstützt, sind nicht alle PATCH-Vorgänge in [!DNL Platform]-APIs mit jedem Operationstyp kompatibel. Verfügbare Vorgangsarten sind:
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`: Der Teil der zu aktualisierenden JSON-Struktur, der mit der [JSON Pointer](#json-pointer)-Notation identifiziert wird.

Je nach der in `op` angegebenen Vorgangsart benötigt das JSON Patch-Objekt möglicherweise zusätzliche Eigenschaften. Weitere Informationen zu den verschiedenen JSON Patch-Vorgängen und deren benötigter Syntax finden Sie in der [JSON Patch-Dokumentation](http://jsonpatch.com/).

## JSON-Schema {#json-schema}

JSON-Schema ist ein Format, mit dem die Struktur von JSON-Daten beschrieben und validiert wird. Das [Experience Data Model (XDM)](../xdm/home.md) nutzt JSON-Schema-Funktionen, um Beschränkungen in Bezug auf die Struktur und das Format der aufgenommenen Kundenerlebnisdaten zu erzwingen. Weitere Informationen zum JSON-Schema finden Sie in der [offiziellen Dokumentation](https://json-schema.org/).

## Nächste Schritte

Dieses Dokument führte einige der Technologien und Syntaxen ein, die mit der Verwaltung von JSON-basierten Ressourcen für [!DNL Experience Platform] verbunden sind. Weitere Informationen zum Arbeiten mit Plattform-APIs, einschließlich Best Practices, finden Sie im Handbuch [Erste Schritte](api-guide.md). Antworten auf häufig gestellte Fragen finden Sie im Handbuch [Plattformfehlerbehebung](troubleshooting.md).
