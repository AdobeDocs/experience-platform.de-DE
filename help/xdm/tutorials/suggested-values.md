---
title: Verwalten von vorgeschlagenen Werten in der API
description: Erfahren Sie, wie Sie einem Zeichenfolgenfeld in der Schema Registry-API empfohlene Werte hinzufügen.
exl-id: 96897a5d-e00a-410f-a20e-f77e223bd8c4
source-git-commit: 19bd5d9c307ac6e1b852e25438ff42bf52a1231e
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 6%

---

# Verwalten von vorgeschlagenen Werten in der API

Für jedes Zeichenfolgenfeld im Experience-Datenmodell (XDM) können Sie eine **enum** , wodurch die Werte, die das Feld erfassen kann, auf einen vordefinierten Satz beschränkt werden. Wenn Sie versuchen, Daten in ein Enum-Feld zu erfassen und der Wert mit keinem der in der Konfiguration definierten Werte übereinstimmt, wird die Aufnahme verweigert.

Fügen Sie im Gegensatz zu Auflistungen **empfohlene Werte** in ein Zeichenfolgenfeld eintragen, werden die Werte, die aufgenommen werden können, nicht eingeschränkt. Stattdessen wirken sich die vorgeschlagenen Werte darauf aus, welche vordefinierten Werte im [Segmentierungsbenutzeroberfläche](../../segmentation/ui/overview.md) , wenn das Zeichenfolgenfeld als Attribut eingefügt wird.

>[!NOTE]
>
>Es gibt eine ungefähre Verzögerung von fünf Minuten, bis die aktualisierten vorgeschlagenen Werte eines Felds in der Segmentierungsbenutzeroberfläche angezeigt werden.

In diesem Handbuch wird beschrieben, wie Sie empfohlene Werte mit dem [Schema Registry-API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Anweisungen dazu finden Sie in der Benutzeroberfläche von Adobe Experience Platform im Abschnitt [UI-Handbuch zu Auflistungen und empfohlenen Werten](../ui/fields/enum.md).

## Voraussetzungen

In diesem Handbuch wird davon ausgegangen, dass Sie mit den Elementen der Schemakomposition in XDM und der Verwendung der Schema Registry-API zum Erstellen und Bearbeiten von XDM-Ressourcen vertraut sind. Wenn Sie eine Einführung benötigen, lesen Sie die folgende Dokumentation:

* [Grundlagen der Schema-Komposition](../schema/composition.md)
* [Handbuch zur Schema Registry-API](../api/overview.md)

Es wird außerdem dringend empfohlen, die [Evolutionsregeln für Auflistungen und empfohlene Werte](../ui/fields/enum.md#evolution) wenn Sie vorhandene Felder aktualisieren. Wenn Sie empfohlene Werte für Schemas verwalten, die an einer Vereinigung teilnehmen, lesen Sie den Abschnitt [Regeln zum Zusammenführen von Auflistungen und vorgeschlagenen Werten](../ui/fields/enum.md#merging).

## Komposition

In der API werden die eingeschränkten Werte für eine **enum** -Feld durch eine `enum` Array, während eine `meta:enum` -Objekt stellt Anzeigenamen für diese Werte bereit:

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

Alternativ können Sie ein Zeichenfolgenfeld definieren, das keine `enum` -Array und verwendet nur die `meta:enum` Objekt zum Markieren **empfohlene Werte**:

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

Da die Zeichenfolge keine `enum` Array zum Definieren von Begrenzungen, sein `meta:enum` -Eigenschaft kann erweitert werden, um neue Werte einzuschließen.

## Verwalten von vorgeschlagenen Werten für Standardfelder

Für vorhandene Standardfelder können Sie [empfohlene Werte hinzufügen](#add-suggested-standard) oder [empfohlene Werte entfernen](#remove-suggested-standard).

### Hinzufügen empfohlener Werte {#add-suggested-standard}

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

### Empfohlene Werte entfernen {#remove-suggested-standard}

Wenn ein Standardzeichenfolgenfeld vordefinierte empfohlene Werte enthält, können Sie alle Werte entfernen, die nicht in der Segmentierung angezeigt werden sollen. Dies geschieht durch Erstellen einer [Anzeigenamendeskriptor](../api/descriptors.md#friendly-name) für das Schema, das eine `xdm:excludeMetaEnum` -Eigenschaft.

**API-Format**

```http
POST /tenant/descriptors
```

**Anfrage**

Die folgende Anfrage entfernt die vorgeschlagenen Werte &quot;[!DNL Web Form Filled Out]&quot; und &quot;[!DNL Media ping]&quot; `eventType` in einem Schema, das auf der [XDM ExperienceEvent-Klasse](../classes/experienceevent.md).

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "@type": "xdm:alternateDisplayInfo",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/xdm:eventType",
        "xdm:excludeMetaEnum": {
          "web.formFilledOut": "Web Form Filled Out",
          "media.ping": "Media ping"
        }
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `@type` | Der Typ des zu definierenden Deskriptors. Bei einem Anzeigenamendeskriptor muss dieser Wert auf `xdm:alternateDisplayInfo`. |
| `xdm:sourceSchema` | Der `$id`-URI des Schemas, wo der Deskriptor definiert wird. |
| `xdm:sourceVersion` | Die Hauptversion des Quellschemas. |
| `xdm:sourceProperty` | Der Pfad zur spezifischen Eigenschaft, deren empfohlene Werte Sie verwalten möchten. Der Pfad sollte mit einem Schrägstrich (`/`) und nicht mit einer enden. Nicht einschließen `properties` im Pfad (verwenden Sie beispielsweise `/personalEmail/address` anstelle von `/properties/personalEmail/properties/address`). |
| `meta:excludeMetaEnum` | Ein Objekt, das die vorgeschlagenen Werte beschreibt, die für das Feld in der Segmentierung ausgeschlossen werden sollen. Schlüssel und Wert für jeden Eintrag müssen mit denen im Original übereinstimmen `meta:enum` des Felds, damit der Eintrag ausgeschlossen wird. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 (Erstellt) sowie die Details des neu erstellten Deskriptors zurück. Die unter `xdm:excludeMetaEnum` wird nun in der Segmentierungsbenutzeroberfläche ausgeblendet.

```json
{
  "@type": "xdm:alternateDisplayInfo",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/xdm:eventType",
  "xdm:excludeMetaEnum": {
    "web.formFilledOut": "Web Form Filled Out"
  },
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## Verwalten von vorgeschlagenen Werten für ein benutzerdefiniertes Feld {#suggested-custom}

So verwalten Sie die `meta:enum` eines benutzerdefinierten Felds können Sie die übergeordnete Klasse, Feldergruppe oder den Datentyp des Felds über eine PATCH-Anfrage aktualisieren.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

In diesem Handbuch wurde beschrieben, wie Sie empfohlene Werte für Zeichenfolgenfelder in der Schema Registry-API verwalten. Siehe Handbuch unter [Definieren benutzerdefinierter Felder in der API](./custom-fields-api.md) für weitere Informationen zum Erstellen verschiedener Feldtypen.
