---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Grundlagen der Adobe Experience Platformen-API
topic: getting started
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 3%

---


# Grundlagen der Adobe Experience Platformen-API

Adobe Experience Platformen-APIs verwenden verschiedene zugrunde liegende Technologien und Syntaxen, die für eine effektive Verwaltung von JSON-basierten [!DNL Platform] Ressourcen wichtig sind. Dieses Dokument bietet einen kurzen Überblick über diese Technologien sowie Links zur externen Dokumentation für weitere Informationen.

## JSON-Zeiger {#json-pointer}

JSON Pointer ist eine standardisierte Zeichenfolgensyntax ([RFC 6901](https://tools.ietf.org/html/rfc6901)) zur Identifizierung bestimmter Werte in JSON-Dokumenten. Ein JSON-Zeiger ist eine Zeichenfolge aus Token, die durch `/` Zeichen getrennt ist und entweder Objektschlüssel oder Array-Indizes angeben. Die Token können eine Zeichenfolge oder eine Zahl sein. JSON-Zeigerzeichenfolgen werden in vielen PATCH-Vorgängen für [!DNL Platform] APIs verwendet, wie weiter unten in diesem Dokument beschrieben. Weitere Informationen zu JSON-Zeiger finden Sie in der [JSON-Zeiger-Übersichtsdokumentation](https://rapidjson.org/md_doc_pointer.html).

### Beispiel für ein JSON-Schema

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

### Beispiel für JSON-Zeiger, die auf dem Schema-Objekt basieren

| JSON-Zeiger | Löst |
|--- | ---|
| `"/title"` | &quot;Details zu Treuemitgliedern&quot; |
| `"/definitions/loyalty"` | (Gibt den Inhalt des `loyalty` Objekts zurück) |
| `"/definitions/loyalty/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/definitions/loyalty/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NHinweis]
>
>
>Beim Umgang mit den `xdm:sourceProperty` und `xdm:destinationProperty` Attributen von [!DNL Experience Data Model] (XDM-)Deskriptoren müssen alle `properties` Schlüssel aus der JSON-Zeigerzeichenfolge **ausgeschlossen** werden. Weitere Informationen finden Sie im Unterhandbuch zu [Deskriptoren](../xdm/api/descriptors.md) im Handbuch für die API-Entwickler der Schema-Registrierung.

## JSON-Patch

Es gibt viele PATCH-Vorgänge für [!DNL Platform] APIs, die JSON Patch-Objekte für ihre Anforderungs-Nutzdaten akzeptieren. JSON Patch ist ein standardisiertes Format ([RFC 6902](https://tools.ietf.org/html/rfc6902)) zur Beschreibung von Änderungen an einem JSON-Dokument. Damit können Sie Teilaktualisierungen zu JSON definieren, ohne das gesamte Dokument in einem Anforderungstext senden zu müssen.

### Beispiel für ein JSON-Patch-Objekt

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`: Die Art des Patch-Vorgangs. Obwohl JSON Patch mehrere verschiedene Operationstypen unterstützt, sind nicht alle PATCH-Vorgänge in [!DNL Platform] APIs mit jedem Operationstyp kompatibel. Verfügbare Vorgangsarten sind:
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`: Der Teil der zu aktualisierenden JSON-Struktur, der mit der [JSON-Zeigernotation](#json-pointer) identifiziert wird.

Je nach dem in `op`dem JSON Patch-Objekt angegebenen Operationstyp sind möglicherweise zusätzliche Eigenschaften erforderlich. Weitere Informationen zu den verschiedenen JSON Patch-Operationen und deren benötigter Syntax finden Sie in der [JSON Patch-Dokumentation](http://jsonpatch.com/).

## JSON-Schema

JSON-Schema ist ein Format, mit dem die Struktur von JSON-Daten beschrieben und validiert wird. [Das Experience Data Model (XDM)](../xdm/home.md) nutzt JSON-Schema-Funktionen, um Beschränkungen in Bezug auf die Struktur und das Format der erfassten Kundenerlebnisdaten zu erzwingen. Weitere Informationen zum JSON-Schema finden Sie in der [offiziellen Dokumentation](https://json-schema.org/).

## Nächste Schritte

In diesem Dokument wurden einige der Technologien und Syntaxen eingeführt, die mit der Verwaltung von JSON-basierten Ressourcen für [!DNL Experience Platform]die Arbeit verbunden sind. Weitere Informationen zum Arbeiten mit [!DNL Platform] APIs, einschließlich Best Practices und Antworten auf häufig gestellte Fragen, finden Sie im Handbuch zur Fehlerbehebung für [Platformen](troubleshooting.md).