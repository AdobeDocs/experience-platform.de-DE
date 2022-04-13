---
title: Hinzufügen von vorgeschlagenen Werten zu einem Feld
description: Erfahren Sie, wie Sie einem Zeichenfolgenfeld in der Schema Registry-API empfohlene Werte hinzufügen.
exl-id: 96897a5d-e00a-410f-a20e-f77e223bd8c4
source-git-commit: 4ce9e53ec420a8c9ba07cdfd75e66d854989f8d2
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 1%

---

# Hinzufügen empfohlener Werte zu einem Feld

Im Experience-Datenmodell (XDM) stellt ein Enum-Feld ein Zeichenfolgenfeld dar, das auf eine vordefinierte Untergruppe von Werten beschränkt ist. Aufzählungsfelder können eine Validierung bereitstellen, um sicherzustellen, dass die aufgenommenen Daten einem Satz zulässiger Werte entsprechen. Sie können jedoch auch einen Satz empfohlener Werte für ein Zeichenfolgenfeld definieren, ohne sie als Begrenzungen zu erzwingen.

Im [Schema Registry-API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/), werden die eingeschränkten Werte für ein Aufzählungsfeld durch eine `enum` Array, während eine `meta:enum` -Objekt stellt Anzeigenamen für diese Werte bereit:

```json
"exampleStringField": {
  "type": "string",
  "enum": [
    "value1",
    "value2",
    "value3"
  ],
  "meta:enum": {
    "value1": "Value 1",
    "value2": "Value 2",
    "value3": "Value 3"
  },
  "default": "value1"
}
```

Bei Enum-Feldern erlaubt die Schema Registry nicht `meta:enum` über die in `enum`, da der Versuch, Zeichenfolgenwerte außerhalb dieser Begrenzungen zu erfassen, die Validierung nicht bestanden hat.

Alternativ können Sie ein Zeichenfolgenfeld definieren, das keine `enum` -Array und verwendet nur die `meta:enum` -Objekt, um empfohlene Werte zu kennzeichnen:

```json
"exampleStringField": {
  "type": "string",
  "meta:enum": {
    "value1": "Value 1",
    "value2": "Value 2",
    "value3": "Value 3"
  },
  "default": "value1"
}
```

Da die Zeichenfolge keine `enum` Array zum Definieren von Begrenzungen, sein `meta:enum` -Eigenschaft kann erweitert werden, um neue Werte einzuschließen. In diesem Tutorial wird beschrieben, wie Sie empfohlene Werte zu standardmäßigen und benutzerdefinierten Zeichenfolgenfeldern in der Schema Registry-API hinzufügen.

## Voraussetzungen

In diesem Handbuch wird davon ausgegangen, dass Sie mit den Elementen der Schemakomposition in XDM und der Verwendung der Schema Registry-API zum Erstellen und Bearbeiten von XDM-Ressourcen vertraut sind. Wenn Sie eine Einführung benötigen, lesen Sie die folgende Dokumentation:

* [Grundlagen der Schema-Komposition](../schema/composition.md)
* [Handbuch zur Schema Registry-API](../api/overview.md)

## Hinzufügen empfohlener Werte zu einem Standardfeld

So erweitern Sie die `meta:enum` In einem Standard-Zeichenfolgenfeld können Sie eine [Anzeigenamendeskriptor](../api/descriptors.md#friendly-name) für das betreffende Feld in einem bestimmten Schema.

>[!NOTE]
>
>Empfohlene Werte für Zeichenfolgenfelder können nur auf Schemaebene hinzugefügt werden. Mit anderen Worten, die `meta:enum` eines Standardfelds in einem Schema wirkt sich nicht auf andere Schemas aus, die dasselbe Standardfeld verwenden.

Die folgende Anfrage fügt empfohlene Werte zum Standard hinzu `eventType` -Feld (bereitgestellt von der [XDM ExperienceEvent-Klasse](../classes/experienceevent.md)) für das Schema, das unter `sourceSchema`:

```curl
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "@type": "xdm:alternateDisplayInfo",
        "sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "sourceProperty": "/eventType",
        "title": {
            "en_us": "Enum Event Type"
        },
        "description": {
            "en_us": "Event type field with soft enum values"
        },
        "meta:enum": {
          "eventA": {
            "en_us": "Event Type A"
          },
          "eventB": {
            "en_us": "Event Type B"
          }
        }
      }'
```

Nach Anwendung des Deskriptors antwortet die Schema Registry beim Abrufen des Schemas mit Folgendem (Antwort aus Platzgründen abgeschnitten):

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "title": "Example Schema",
  "properties": {
    "eventType": {
      "type":"string",
      "title": "Enum Event Type",
      "description": "Event type field with soft enum values.",
      "meta:enum": {
        "customEventA": "Custom Event Type A",
        "customEventB": "Custom Event Type B"
      }
    }
  }
}
```

>[!NOTE]
>
>Wenn das Standardfeld bereits Werte unter `meta:enum`, überschreiben die neuen Werte aus dem Deskriptor nicht die vorhandenen Felder und werden stattdessen hinzugefügt:
>
>
```json
>"standardField": {
>   "type":"string",
>   "title": "Example standard enum field",
>   "description": "Standard field with existing enum values.",
>   "meta:enum": {
>       "standardEventA": "Standard Event Type A",
>       "standardEventB": "Standard Event Type B",
>       "customEventA": "Custom Event Type A",
>       "customEventB": "Custom Event Type B"
>   }
>}
>```

## Hinzufügen von vorgeschlagenen Werten zu einem benutzerdefinierten Feld

So erweitern Sie die `meta:enum` eines benutzerdefinierten Felds können Sie die übergeordnete Klasse, Feldergruppe oder den Datentyp des Felds über eine PATCH-Anfrage aktualisieren.

>[!WARNING]
>
>Im Gegensatz zu Standardfeldern wird beim Aktualisieren der `meta:enum` eines benutzerdefinierten Felds wirkt sich auf alle anderen Schemas aus, die dieses Feld verwenden. Wenn Änderungen nicht über Schemata hinweg propagiert werden sollen, sollten Sie stattdessen eine neue benutzerdefinierte Ressource erstellen:
>
>* [Benutzerdefinierte Klasse erstellen](../api/classes.md#create)
>* [Benutzerdefinierte Feldergruppe erstellen](../api/field-groups.md#create)
>* [Benutzerdefinierten Datentyp erstellen](../api/data-types.md#create)


Die folgende Anfrage aktualisiert die `meta:enum` eines von einem benutzerdefinierten Datentyp bereitgestellten Felds &quot;Treuestufe&quot;:

```curl
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
          "op": "replace",
          "path": "/loyaltyLevel/meta:enum",
          "value": {
            "ultra-platinum": "Ultra Platinum",
            "platinum": "Platinum",
            "gold": "Gold",
            "silver": "Silver",
            "bronze": "Bronze"
          }
        }
      ]'
```

Nach der Anwendung der Änderung antwortet die Schema Registry beim Abrufen des Schemas mit Folgendem (Antwort aus Platzgründen abgeschnitten):

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "title": "Example Schema",
  "properties": {
    "loyaltyLevel": {
      "type":"string",
      "title": "Loyalty Level",
      "description": "The loyalty program tier that this customer qualifies for.",
      "meta:enum": {
        "ultra-platinum": "Ultra Platinum",
        "platinum": "Platinum",
        "gold": "Gold",
        "silver": "Silver",
        "bronze": "Bronze"
      }
    }
  }
}
```

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie in der Schema Registry-API empfohlene Werte zu Zeichenfolgenfeldern hinzufügen. Siehe Handbuch unter [Definieren benutzerdefinierter Felder in der API](./custom-fields-api.md) für weitere Informationen zum Erstellen verschiedener Feldtypen.
