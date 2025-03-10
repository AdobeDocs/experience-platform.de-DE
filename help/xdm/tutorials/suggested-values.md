---
title: Vorgeschlagene Werte in der API verwalten
description: Erfahren Sie, wie Sie in der Schema Registry-API vorgeschlagene Werte zu einem Zeichenfolgenfeld hinzufügen.
exl-id: 96897a5d-e00a-410f-a20e-f77e223bd8c4
source-git-commit: a3140d5216857ef41c885bbad8c69d91493b619d
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 1%

---

# Vorgeschlagene Werte in der API verwalten

Für jedes Zeichenfolgenfeld im Experience-Datenmodell (XDM) können Sie eine **Aufzählung** definieren, die die Werte, die das Feld aufnehmen kann, auf einen vordefinierten Satz einschränkt. Wenn Sie versuchen, Daten in ein Aufzählungsfeld aufzunehmen, und der Wert mit keinem der in der Konfiguration definierten übereinstimmt, wird die Aufnahme verweigert.

Im Gegensatz zu Auflistungen schränkt das Hinzufügen **empfohlenen Werte** zu einem Zeichenfolgenfeld nicht die Werte ein, die es aufnehmen kann. Stattdessen beeinflussen vorgeschlagene Werte, welche vordefinierten Werte in der [Segmentierungsbenutzeroberfläche) verfügbar sind](../../segmentation/ui/overview.md) wenn das Zeichenfolgenfeld als Attribut einbezogen wird.

>[!NOTE]
>
>Die aktualisierten empfohlenen Werte eines Felds, die in der Segmentierungs-Benutzeroberfläche angezeigt werden sollen, vergehen ungefähr fünf Minuten.

In diesem Handbuch wird beschrieben, wie Sie vorgeschlagene Werte mithilfe der [Schema Registry-API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/) verwalten. Anweisungen dazu, wie Sie dies in der Adobe Experience Platform-Benutzeroberfläche tun, finden Sie im [UI-Handbuch zu Auflistungen und empfohlenen Werten](../ui/fields/enum.md).

## Voraussetzungen

In diesem Handbuch wird davon ausgegangen, dass Sie mit den Elementen der Schemakomposition in XDM und der Verwendung der Schema Registry-API zum Erstellen und Bearbeiten von XDM-Ressourcen vertraut sind. Bitte lesen Sie die folgende Dokumentation, wenn Sie eine Einführung benötigen:

* [Grundlagen der Schema-Komposition](../schema/composition.md)
* [Handbuch zur Schema Registry-API](../api/overview.md)

Es wird außerdem dringend empfohlen, die [Entwicklungsregeln für Aufzählungen und empfohlene Werte“ zu überprüfen](../ui/fields/enum.md#evolution) wenn Sie vorhandene Felder aktualisieren. Wenn Sie vorgeschlagene Werte für Schemata verwalten, die Teil einer Vereinigung sind, finden Sie weitere Informationen unter [Regeln für das Zusammenführen von Auflistungen und vorgeschlagenen Werten](../ui/fields/enum.md#merging).

## Komposition

In der API werden die eingeschränkten Werte für ein **enum**-Feld durch ein `enum`-Array dargestellt, während ein `meta:enum`-Objekt Anzeigenamen für diese Werte bereitstellt:

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

Bei Aufzählungsfeldern ermöglicht die Schemaregistrierung keine Erweiterung von `meta:enum` über die unter `enum` angegebenen Werte hinaus, da der Versuch, Zeichenfolgenwerte außerhalb dieser Einschränkungen aufzunehmen, die Validierung nicht bestehen würde.

Alternativ können Sie ein Zeichenfolgenfeld definieren, das kein `enum`-Array enthält und das `meta:enum`-Objekt nur zur Kennzeichnung von (vorgeschlagenen **Werten**:

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

Da die Zeichenfolge über kein `enum`-Array zum Definieren von Einschränkungen verfügt, kann ihre `meta:enum`-Eigenschaft erweitert werden, um neue Werte einzuschließen.

<!-- ## Manage suggested values for standard fields

For existing standard fields, you can [add suggested values](#add-suggested-standard) or [remove suggested values](#remove-suggested-standard). -->

## Hinzufügen empfohlener Werte zu einem Standardfeld {#add-suggested-standard}

Um die `meta:enum` eines standardmäßigen Zeichenfolgenfelds zu erweitern, können Sie für das [ Feld in einem bestimmten Schema einen ](../api/descriptors.md#friendly-name)Deskriptor für benutzerfreundliche Namen“ erstellen.

>[!NOTE]
>
>Die vorgeschlagenen Werte für Zeichenfolgenfelder können nur auf Schemaebene hinzugefügt werden. Mit anderen Worten: Die Erweiterung der `meta:enum` eines Standardfelds in einem Schema wirkt sich nicht auf andere Schemata aus, die dasselbe Standardfeld verwenden.

Die folgende Anfrage fügt dem `eventType`-Standardfeld (bereitgestellt von der [XDM ExperienceEvent-Klasse](../classes/experienceevent.md)) vorgeschlagene Werte für das unter `sourceSchema` identifizierte Schema hinzu:

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

Nach Anwendung des Deskriptors antwortet die Schemaregistrierung beim Abrufen des Schemas mit dem folgenden Code (Antwort aus Platzgründen abgeschnitten):

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
>Wenn das Standardfeld bereits Werte unter `meta:enum` enthält, überschreiben die neuen Werte aus dem Deskriptor nicht die vorhandenen Felder und werden stattdessen zu hinzugefügt:
>
>```json
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

<!-- ### Remove suggested values {#remove-suggested-standard}

If a standard string field has predefined suggested values, you can remove any values that you do not wish to see in segmentation. This is done through by creating a [friendly name descriptor](../api/descriptors.md#friendly-name) for the schema that includes an `xdm:excludeMetaEnum` property.

**API format**

```http
POST /tenant/descriptors
```

**Request**

The following request removes the suggested values "[!DNL Web Form Filled Out]" and "[!DNL Media ping]" for `eventType` in a schema based on the [XDM ExperienceEvent class](../classes/experienceevent.md).

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

| Property | Description |
| --- | --- |
| `@type` | The type of descriptor being defined. For a friendly name descriptor, this value must be set to `xdm:alternateDisplayInfo`. |
| `xdm:sourceSchema` | The `$id` URI of the schema where the descriptor is being defined. |
| `xdm:sourceVersion` | The major version of the source schema. |
| `xdm:sourceProperty` | The path to the specific property whose suggested values you want to manage. The path should begin with a slash (`/`) and not end with one. Do not include `properties` in the path (for example, use `/personalEmail/address` instead of `/properties/personalEmail/properties/address`). |
| `meta:excludeMetaEnum` | An object that describes the suggested values that should be excluded for the field in segmentation. The key and value for each entry must match those included in the original `meta:enum` of the field in order for the entry to be excluded.  |

{style="table-layout:auto"}

**Response**

A successful response returns HTTP status 201 (Created) and the details of the newly created descriptor. The suggested values included under `xdm:excludeMetaEnum` will now be hidden from the Segmentation UI.

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
``` -->

## Vorgeschlagene Werte für ein benutzerdefiniertes Feld verwalten {#suggested-custom}

Um die `meta:enum` eines benutzerdefinierten Felds zu verwalten, können Sie die übergeordnete Klasse, Feldergruppe oder den Datentyp des Felds über eine PATCH-Anfrage aktualisieren.

>[!WARNING]
>
>Im Gegensatz zu Standardfeldern wirkt sich die Aktualisierung der `meta:enum` eines benutzerdefinierten Felds auf alle anderen Schemata aus, die dieses Feld verwenden. Wenn Sie nicht möchten, dass Änderungen sich über Schemata hinweg ausbreiten, sollten Sie stattdessen eine neue benutzerdefinierte Ressource erstellen:
>
>* [Erstellen einer benutzerdefinierten Klasse](../api/classes.md#create)
>* [Erstellen einer benutzerdefinierten Feldergruppe](../api/field-groups.md#create)
>* [Erstellen eines benutzerdefinierten Datentyps](../api/data-types.md#create)

Die folgende Anfrage aktualisiert die `meta:enum` eines Felds der Treuestufe, das von einem benutzerdefinierten Datentyp bereitgestellt wird:

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

Nach Anwendung der Änderung antwortet die Schemaregistrierung beim Abrufen des Schemas wie folgt (Antwort aus Platzgründen gekürzt):

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

In diesem Handbuch wurde beschrieben, wie Sie vorgeschlagene Werte für Zeichenfolgenfelder in der Schema Registry-API verwalten. Weitere Informationen zum Erstellen [ verschiedenen Feldtypen finden Sie ](./custom-fields-api.md) Handbuch unter „Definieren benutzerdefinierter Felder in der API“.
