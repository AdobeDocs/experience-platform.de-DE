---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Grundlagen der Experience Platform-API
description: Dieses Dokument bietet einen kurzen Überblick über einige der zugrunde liegenden Technologien und Syntaxen, die mit Experience Platform-APIs verbunden sind.
exl-id: cd69ba48-f78c-4da5-80d1-efab5f508756
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 53%

---

# Grundlagen der Experience Platform-API

Adobe Experience Platform-APIs verwenden verschiedene zugrunde liegende Technologien und Syntaxen, die für eine effektive Verwaltung von JSON-basierten Anwendungen wichtig sind [!DNL Platform] Ressourcen. Dieses Dokument bietet einen kurzen Überblick über diese Technologien sowie Links zur externen Dokumentation für weitere Informationen.

## JSON Pointer {#json-pointer}

JSON Pointer ist eine standardisierte Zeichenfolgensyntax ([RFC 6901](https://tools.ietf.org/html/rfc6901)) zur Identifizierung bestimmter Werte in JSON-Dokumenten. Ein JSON Pointer ist eine Zeichenfolge aus Token, die durch `/`-Zeichen getrennt sind und entweder Objektschlüssel oder Array-Indizes angeben. Die Token können eine Zeichenfolge oder eine Zahl sein. JSON Pointer-Zeichenfolgen werden in vielen PATCH-Vorgängen für [!DNL Platform] APIs, wie weiter unten in diesem Dokument beschrieben. Weitere Informationen zu JSON Pointer finden Sie in der Dokumentation [JSON Pointer – Überblick](https://rapidjson.org/md_doc_pointer.html).

### Beispiel für ein JSON-Schema-Objekt

Die folgende JSON-Datei stellt ein vereinfachtes XDM-Schema dar, dessen Felder mithilfe von JSON Pointer-Zeichenfolgen referenziert werden können. Beachten Sie, dass alle Felder, die mit benutzerdefinierten Schemafeldgruppen hinzugefügt wurden (z. B. `loyaltyLevel`) werden unter einem Namespace `_{TENANT_ID}` -Objekt, während Felder, die mit Kernfeldgruppen hinzugefügt wurden (z. B. `fullName`) nicht.

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
| `"/properties/person/properties/name/properties/fullName"` | (Gibt einen Verweis auf die `fullName` -Feld, das von einer Kernfeldgruppe bereitgestellt wird.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | (Gibt einen Verweis auf die `loyaltyLevel` -Feld, das von einer benutzerdefinierten Feldergruppe bereitgestellt wird.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>Bei der Behandlung von `xdm:sourceProperty` und `xdm:destinationProperty` -Attribute [!DNL Experience Data Model] (XDM)-Deskriptoren, beliebige `properties` Schlüssel müssen **ausgeschlossen** aus der JSON Pointer-Zeichenfolge. Siehe [!DNL Schema Registry] Unterhandbuch für API-Entwickler zu [deskriptoren](../xdm/api/descriptors.md) für weitere Informationen.

## JSON Patch {#json-patch}

Es gibt viele PATCH-Vorgänge für [!DNL Platform] APIs, die JSON Patch-Objekte für ihre Anfrage-Payloads akzeptieren. JSON Patch ist ein standardisiertes Format ([RFC 6902](https://tools.ietf.org/html/rfc6902)) zur Beschreibung von Änderungen an einem JSON-Dokument. Damit können Sie Teilaktualisierungen zu JSON definieren, ohne das gesamte Dokument in einem Anfragetext senden zu müssen.

### Beispiel für ein JSON Patch-Objekt

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`: Die Art des Patch-Vorgangs. Während JSON Patch mehrere verschiedene Vorgangsarten unterstützt, sind nicht alle PATCH-Vorgänge in [!DNL Platform] APIs sind mit jedem Vorgangstyp kompatibel. Verfügbare Vorgangsarten sind:
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`: Der Teil der zu aktualisierenden JSON-Struktur, der mit der [JSON Pointer](#json-pointer)-Notation identifiziert wird.

Je nach der in `op` angegebenen Vorgangsart benötigt das JSON Patch-Objekt möglicherweise zusätzliche Eigenschaften. Weitere Informationen zu den verschiedenen JSON Patch-Vorgängen und deren benötigter Syntax finden Sie in der [JSON Patch-Dokumentation](https://datatracker.ietf.org/doc/html/rfc6902).

## JSON-Schema {#json-schema}

JSON-Schema ist ein Format, mit dem die Struktur von JSON-Daten beschrieben und validiert wird. Das [Experience Data Model (XDM)](../xdm/home.md) nutzt JSON-Schema-Funktionen, um Beschränkungen in Bezug auf die Struktur und das Format der aufgenommenen Kundenerlebnisdaten zu erzwingen. Weitere Informationen zum JSON-Schema finden Sie in der [offiziellen Dokumentation](https://json-schema.org/).

## Nächste Schritte

In diesem Dokument wurden einige der Technologien und Syntaxen für die Verwaltung von JSON-basierten Ressourcen für [!DNL Experience Platform]. Siehe Abschnitt [Erste Schritte](api-guide.md) Weitere Informationen zum Arbeiten mit Platform-APIs, einschließlich Best Practices. Antworten auf häufig gestellte Fragen finden Sie im Abschnitt [Handbuch zur Fehlerbehebung bei Platform](troubleshooting.md).
