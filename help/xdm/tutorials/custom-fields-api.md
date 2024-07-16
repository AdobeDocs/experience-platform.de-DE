---
title: Definieren von XDM-Feldern in der Schema Registry-API
description: Erfahren Sie, wie Sie beim Erstellen benutzerdefinierter Experience-Datenmodell (XDM)-Ressourcen in der Schema Registry-API verschiedene Felder definieren.
exl-id: d79332e3-8448-42af-b250-882bcb0f1e7d
source-git-commit: a3140d5216857ef41c885bbad8c69d91493b619d
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 1%

---

# Definieren von XDM-Feldern in der Schema Registry-API

Alle Experience-Datenmodell (XDM)-Felder werden mit den standardmäßigen [JSON-Schema](https://json-schema.org/) -Einschränkungen definiert, die für ihren Feldtyp gelten, mit zusätzlichen Einschränkungen für Feldnamen, die von Adobe Experience Platform erzwungen werden. Mit der Schema Registry-API können Sie benutzerdefinierte Felder in Ihren Schemas definieren, indem Sie Formate und optionale Einschränkungen verwenden. XDM-Feldtypen werden durch das Attribut auf Feldebene, `meta:xdmType`, verfügbar gemacht.

>[!NOTE]
>
>`meta:xdmType` ist ein vom System generierter Wert. Daher müssen Sie diese Eigenschaft nicht zum JSON für Ihr Feld hinzufügen, wenn Sie die API verwenden (außer beim Erstellen benutzerdefinierter Zuordnungstypen [). ](#custom-maps) Es empfiehlt sich, JSON-Schematypen (z. B. `string` und `integer`) mit den entsprechenden Min-/Max-Einschränkungen zu verwenden, wie in der folgenden Tabelle definiert.

In diesem Handbuch wird die geeignete Formatierung zum Definieren verschiedener Feldtypen beschrieben, einschließlich derjenigen mit optionalen Eigenschaften. Weitere Informationen zu optionalen Eigenschaften und typspezifischen Suchbegriffen finden Sie in der Dokumentation zum [JSON-Schema](https://json-schema.org/understanding-json-schema/reference/type.html).

Suchen Sie zunächst den gewünschten Feldtyp und verwenden Sie den Beispielcode, der zum Erstellen Ihrer API-Anfrage für das [Erstellen einer Feldergruppe](../api/field-groups.md#create) oder [Erstellen eines Datentyps](../api/data-types.md#create) bereitgestellt wird.

## [!UICONTROL String] {#string}

[!UICONTROL String] -Felder sind durch `type: string` gekennzeichnet.

```json
"sampleField": {
  "title": "Sample String Field",
  "description": "An example string field.",
  "type": "string"
}
```

Sie können optional mithilfe der folgenden zusätzlichen Eigenschaften einschränken, welche Arten von Werten für die Zeichenfolge eingegeben werden können:

* `pattern`: Ein Regex-Muster, durch das eingeschränkt werden soll.
* `minLength`: Eine Mindestlänge für die Zeichenfolge.
* `maxLength`: Eine maximale Länge für die Zeichenfolge.

```json
"sampleField": {
  "title": "Sample String Field",
  "description": "An example string field with added constraints.",
  "type": "string",
  "pattern": "^[A-Z]{2}$",
  "maxLength": 2
}
```

## [!UICONTROL URI] {#uri}

[!UICONTROL URI] -Felder werden durch `type: string` gekennzeichnet, wobei die Eigenschaft `format` auf `uri` gesetzt ist. Es werden keine anderen Eigenschaften akzeptiert.

```json
"sampleField": {
  "title": "Sample URI Field",
  "description": "An example URI field.",
  "type": "string",
  "format": "uri"
}
```

## [!UICONTROL Enum] {#enum}

[!UICONTROL Enum] -Felder müssen `type: string` verwenden, wobei die Enum-Werte selbst unter einem `enum` -Array bereitgestellt werden:

```json
"sampleField": {
  "title": "Sample Enum Field",
  "description": "An example enum field.",
  "type": "string",
  "enum": [
      "value1",
      "value2",
      "value3"
  ]
}
```

Sie können optional für jeden Wert unter einer `meta:enum` -Eigenschaft kundenorientierte Beschriftungen angeben, wobei jede Beschriftung einem entsprechenden Wert unter `enum` zugeordnet wird.

```json
"sampleField": {
  "title": "Sample Enum Field",
  "description": "An example enum field with customer-facing labels.",
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
  }
}
```

>[!NOTE]
>
>Der `meta:enum` -Wert deklariert **nicht** eine Auflistung oder führt eine Datenvalidierung allein durch. In den meisten Fällen werden unter `meta:enum` bereitgestellte Zeichenfolgen auch unter `enum` bereitgestellt, um sicherzustellen, dass die Daten eingeschränkt sind. Es gibt jedoch einige Anwendungsfälle, in denen `meta:enum` ohne ein entsprechendes `enum` -Array bereitgestellt wird. Weitere Informationen finden Sie im Tutorial zum Definieren der vorgeschlagenen Werte [](../tutorials/suggested-values.md) .

Sie können optional eine `default` -Eigenschaft angeben, um den standardmäßigen `enum` -Wert anzugeben, den das Feld verwendet, wenn kein Wert angegeben ist.

```json
"sampleField": {
  "title": "Sample Enum Field",
  "description": "An example enum field with customer-facing labels and a default value.",
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

>[!IMPORTANT]
>
>Wenn kein `default` -Wert angegeben wird und das Enum-Feld auf `required` gesetzt ist, schlägt die Überprüfung bei der Aufnahme eines Datensatzes fehl, wenn für dieses Feld ein anerkannter Wert fehlt.

## [!UICONTROL Nummer] {#number}

Zahlenfelder werden durch `type: number` angegeben und haben keine anderen erforderlichen Eigenschaften.

```json
"sampleField": {
  "title": "Sample Number Field",
  "description": "An example number field.",
  "type": "number"
}
```

>[!NOTE]
>
>`number`-Typen werden für jeden numerischen Typ verwendet, entweder Ganzzahlen oder Gleitkommazahlen, während [`integer` Typen](#integer) speziell für ganzzahlige Zahlen verwendet werden. Weitere Informationen zu den Anwendungsfällen für jeden Typ finden Sie in der Dokumentation zum [JSON-Schema für numerische Typen](https://json-schema.org/understanding-json-schema/reference/numeric.html) .

## [!UICONTROL Integer] {#integer}

[!UICONTROL Integer] -Felder sind durch `type: integer` gekennzeichnet und haben keine anderen erforderlichen Felder.

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field.",
  "type": "integer"
}
```

>[!NOTE]
>
>Während `integer`-Typen sich speziell auf ganzzahlige Zahlen beziehen, werden [`number` Typen](#number) für alle numerischen Typen verwendet, entweder Ganzzahlen oder Gleitkommazahlen. Weitere Informationen zu den Anwendungsfällen für jeden Typ finden Sie in der Dokumentation zum [JSON-Schema für numerische Typen](https://json-schema.org/understanding-json-schema/reference/numeric.html) .

Optional können Sie den Bereich der Ganzzahl einschränken, indem Sie der Definition die Eigenschaften `minimum` und `maximum` hinzufügen. Mehrere andere numerische Typen, die von der Schema Builder-Benutzeroberfläche unterstützt werden, sind nur `integer`-Typen mit bestimmten `minimum`- und `maximum`-Einschränkungen, z. B. [[!UICONTROL Long]](#long), [[!UICONTROL Short]](#short) und [[!UICONTROL Byte]](#byte).

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field with added constraints.",
  "type": "integer",
  "minimum": 1,
  "maximum": 100
}
```

## [!UICONTROL Long] {#long}

Das Äquivalent eines [!UICONTROL Long] -Felds, das über die Schema Builder-Benutzeroberfläche erstellt wurde, ist ein Feld vom Typ [`integer` mit bestimmten `minimum` - und `maximum` -Werten (`-9007199254740992` bzw. `9007199254740992` ).](#integer)

```json
"sampleField": {
  "title": "Sample Long Field",
  "description": "An example long field.",
  "type": "integer",
  "minimum": -9007199254740992,
  "maximum": 9007199254740992
}
```

## [!UICONTROL short] {#short}

Das Äquivalent eines [!UICONTROL Short] -Felds, das über die Schema Builder-Benutzeroberfläche erstellt wird, ist ein Feld vom Typ [`integer` mit bestimmten `minimum` - und `maximum` -Werten (`-32768` bzw. `32768` ).](#integer)

```json
"sampleField": {
  "title": "Sample Short Field",
  "description": "An example short field.",
  "type": "integer",
  "minimum": -32768,
  "maximum": 32768
}
```

## [!UICONTROL Byte] {#byte}

Das Äquivalent eines [!UICONTROL Byte] -Felds, das über die Schema Builder-Benutzeroberfläche erstellt wird, ist ein Feld vom Typ [`integer` mit bestimmten `minimum` - und `maximum` -Werten (`-128` bzw. `128`).](#integer)

```json
"sampleField": {
  "title": "Sample Byte Field",
  "description": "An example byte field.",
  "type": "integer",
  "minimum": -128,
  "maximum": 128
}
```

## [!UICONTROL Boolean] {#boolean}

Die Felder [!UICONTROL Boolesch] sind durch `type: boolean` gekennzeichnet.

```json
"sampleField": {
  "title": "Sample Boolean Field",
  "description": "An example boolean field.",
  "type": "boolean"
}
```

Sie können optional einen `default` -Wert angeben, den das Feld verwendet, wenn während der Aufnahme kein expliziter Wert angegeben wird.

```json
"sampleField": {
  "title": "Sample Boolean Field",
  "description": "An example boolean field with a default value.",
  "type": "boolean",
  "default": false
}
```

>[!IMPORTANT]
>
>Wenn kein `default` -Wert angegeben wird und das boolesche Feld auf `required` gesetzt ist, schlägt die Überprüfung bei der Aufnahme für jeden Datensatz fehl, für den ein anerkannter Wert für dieses Feld fehlt.

## [!UICONTROL Datum] {#date}

Die Felder [!UICONTROL Datum] sind durch `type: string` und `format: date` gekennzeichnet. Sie können optional auch ein Array von `examples` angeben, das verwendet werden soll, wenn Sie eine Beispieldatumszeichenfolge für Benutzer anzeigen möchten, die die Daten manuell eingeben.

```json
"sampleField": {
  "title": "Sample Date Field",
  "description": "An example date field with an example array item.",
  "type": "string",
  "format": "date",
  "examples": ["2004-10-23"]
}
```

## [!UICONTROL DateTime] {#date-time}

Die Felder [!UICONTROL DateTime] sind durch `type: string` und `format: date-time` gekennzeichnet. Sie können optional auch ein Array von &quot;`examples`&quot;bereitstellen, das verwendet werden kann, wenn Sie eine Beispiel-Datum-Uhrzeit-Zeichenfolge für Benutzer anzeigen möchten, die die Daten manuell eingeben.

```json
"sampleField": {
  "title": "Sample Datetime Field",
  "description": "An example datetime field with an example array item.",
  "type": "string",
  "format": "date-time",
  "examples": ["2004-10-23T12:00:00-06:00"]
}
```

## [!UICONTROL Array] {#array}

[!UICONTROL Array] -Felder werden durch `type: array` und ein `items` -Objekt angegeben, das das Schema der Elemente definiert, die das Array akzeptiert.

Sie können Array-Elemente mithilfe von Primitive-Typen definieren, z. B. ein Array von Zeichenfolgen:

```json
"sampleField": {
  "title": "Sample Array Field",
  "description": "An example array field using a primitive type.",
  "type": "array",
  "items": {
    "type": "string"
  }
}
```

Sie können die Array-Elemente auch auf Grundlage eines vorhandenen Datentyps definieren, indem Sie über eine `$ref` -Eigenschaft auf das `$id` des Datentyps verweisen. Im Folgenden finden Sie ein Array von [!UICONTROL Zahlungselement] -Objekten:

```json
"sampleField": {
  "title": "Sample Array Field",
  "description": "An example array field using a data type reference.",
  "type": "array",
  "items": {
    "$ref": "https://ns.adobe.com/xdm/data/paymentitem"
  }
}
```

## [!UICONTROL Objekt] {#object}

[!UICONTROL Objekt] -Felder werden durch `type: object` und ein `properties` -Objekt angegeben, das Untereigenschaften für das Schemafeld definiert.

Das unter `properties` definierte Unterfeld kann mit einem beliebigen Primitive `type` oder durch Referenzierung eines vorhandenen Datentyps über eine `$ref` -Eigenschaft definiert werden, die auf das `$id` des betreffenden Datentyps verweist:

```json
"sampleField": {
  "title": "Sample Object Field",
  "description": "An example object field.",
  "type": "object",
  "properties": {
    "field1": {
      "type": "string"
    },
    "field2": {
      "$ref": "https://ns.adobe.com/xdm/common/measure"
    }
  }
}
```

Sie können auch das gesamte Objekt definieren, indem Sie auf einen Datentyp verweisen, vorausgesetzt, der betreffende Datentyp ist selbst als `type: object` definiert:

```json
"sampleField": {
  "title": "Sample Object Field",
  "description": "An example object field using a data type reference.",
  "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction"
}
```

## [!UICONTROL Landkarte] {#map}

Ein Zuordnungsfeld ist im Wesentlichen ein Feld vom Typ [`object` ](#object) mit einem nicht beschränkten Satz von Schlüsseln. Wie Objekte haben Karten den Wert `type` von `object`, ihre `meta:xdmType` sind jedoch explizit auf `map` eingestellt.

Eine Zuordnung **darf keine** Eigenschaften definieren. **muss** ein einzelnes `additionalProperties`-Schema definieren, um den in der Zuordnung enthaltenen Datentyp zu beschreiben (jede Zuordnung kann nur einen einzigen Datentyp enthalten). Der `type` -Wert muss entweder `string` oder `integer` sein.

Ein Zuordnungsfeld mit Zeichenfolgenwerten würde beispielsweise wie folgt definiert:

```json
"sampleField": {
  "title": "Sample Map Field",
  "description": "An example map field.",
  "type": "object",
  "meta:xdmType": "map",
  "additionalProperties": {
    "type": "string"
  }
}
```

Weitere Informationen zum Erstellen von benutzerdefinierten Zuordnungsfeldern finden Sie im folgenden Abschnitt.

### Erstellen benutzerdefinierter Zuordnungstypen {#custom-maps}

Um &quot;map-like&quot;-Daten in XDM effizient zu unterstützen, können Objekte mit einer &quot;`meta:xdmType`&quot;-Einstellung auf &quot;`map`&quot;kommentiert werden, um deutlich zu machen, dass ein Objekt so verwaltet werden soll, als wäre der Schlüsselsatz nicht beschränkt. Daten, die in Zuordnungsfelder aufgenommen werden, müssen Zeichenfolgenschlüssel und nur String- oder Ganzzahlwerte verwenden (wie durch `additionalProperties.type` bestimmt).

XDM legt die folgenden Einschränkungen für die Verwendung dieses Speicherhinweises fest:

* Zuordnungstypen MÜSSEN vom Typ `object` sein.
* Für Zuordnungstypen dürfen KEINE Eigenschaften definiert sein (d. h. sie definieren &quot;leere&quot;Objekte).
* Zuordnungstypen MÜSSEN ein `additionalProperties.type` -Feld enthalten, das die Werte beschreibt, die auf der Zuordnung platziert werden können, entweder `string` oder `integer`.

Stellen Sie sicher, dass Sie nur Felder vom Typ Zuordnung verwenden, wenn dies unbedingt erforderlich ist, da sie die folgenden Leistungsbeeinträchtigungen aufweisen:

* Die Antwortzeit von [Adobe Experience Platform Query Service](../../query-service/home.md) wird für 100 Millionen Datensätze von drei Sekunden auf zehn Sekunden reduziert.
* Karten mit weniger als 16 Schlüsseln müssen vorhanden sein. Andernfalls besteht die Gefahr einer weiteren Verschlechterung.

Die Benutzeroberfläche von Platform weist außerdem Einschränkungen hinsichtlich der Art und Weise auf, wie die Schlüssel von Feldern vom Typ Zuordnung extrahiert werden können. Während Objekttypen erweitert werden können, werden Zuordnungen stattdessen als ein einzelnes Feld angezeigt.

## Nächste Schritte

In diesem Handbuch wurde die Definition verschiedener Feldtypen in der API beschrieben. Weitere Informationen zur Formatierung von XDM-Feldtypen finden Sie im Handbuch zu [XDM-Feldtypbegrenzungen](../schema/field-constraints.md).
