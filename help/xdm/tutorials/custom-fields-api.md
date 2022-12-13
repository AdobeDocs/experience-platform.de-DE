---
title: Definieren von XDM-Feldern in der Schema Registry-API
description: Erfahren Sie, wie Sie beim Erstellen benutzerdefinierter Experience-Datenmodell (XDM)-Ressourcen in der Schema Registry-API verschiedene Felder definieren.
exl-id: d79332e3-8448-42af-b250-882bcb0f1e7d
source-git-commit: 0947eb38bdb18cb3783723cb11be79d3d32a3b76
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 3%

---

# Definieren von XDM-Feldern in der Schema Registry-API

Alle Felder des Experience-Datenmodells (XDM) werden mit dem Standard [JSON-Schema](https://json-schema.org/) Einschränkungen, die für ihren Feldtyp gelten, mit zusätzlichen Einschränkungen für Feldnamen, die von Adobe Experience Platform erzwungen werden. Mit der Schema Registry-API können Sie benutzerdefinierte Felder in Ihren Schemas definieren, indem Sie Formate und optionale Einschränkungen verwenden. XDM-Feldtypen werden durch das Attribut auf Feldebene verfügbar gemacht, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` ist ein vom System generierter Wert. Daher müssen Sie diese Eigenschaft nicht zum JSON für Ihr Feld hinzufügen, wenn Sie die API verwenden (es sei denn, [Erstellen benutzerdefinierter Zuordnungstypen](#custom-maps)). Es empfiehlt sich, JSON-Schematypen zu verwenden (z. B. `string` und `integer`) mit den entsprechenden Mindest-/Höchstbeschränkungen, wie in der folgenden Tabelle definiert.

In diesem Handbuch wird die geeignete Formatierung zum Definieren verschiedener Feldtypen beschrieben, einschließlich derjenigen mit optionalen Eigenschaften. Weitere Informationen zu optionalen Eigenschaften und typspezifischen Suchbegriffen finden Sie in der Dokumentation zum [JSON-Schema](https://json-schema.org/understanding-json-schema/reference/type.html).

Suchen Sie zunächst den gewünschten Feldtyp und verwenden Sie den Beispielcode, der zum Erstellen Ihrer API-Anfrage für bereitgestellt wird. [Erstellen einer Feldergruppe](../api/field-groups.md#create) oder [Erstellen eines Datentyps](../api/data-types.md#create).

## [!UICONTROL Zeichenfolge] {#string}

[!UICONTROL Zeichenfolge] -Felder werden durch `type: string`.

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

[!UICONTROL URI] -Felder werden durch `type: string` mit `format` Eigenschaft auf `uri`. Es werden keine anderen Eigenschaften akzeptiert.

```json
"sampleField": {
  "title": "Sample URI Field",
  "description": "An example URI field.",
  "type": "string",
  "format": "uri"
}
```

## [!UICONTROL Enum] {#enum}

[!UICONTROL Enum] -Felder müssen `type: string`, wobei die Enum-Werte selbst unter einer `enum` array:

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

Sie können optionale kundenorientierte Beschriftungen für jeden Wert unter `meta:enum` -Eigenschaft, wobei jeder Titel einem entsprechenden `enum` -Wert.

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
>Die `meta:enum` Wert: **not** Deklarieren Sie eine Auflistung oder führen Sie eine Datenvalidierung allein durch. In den meisten Fällen werden unter `meta:enum` werden auch `enum` , um sicherzustellen, dass die Daten begrenzt sind. Es gibt jedoch einige Anwendungsfälle, in denen `meta:enum` ohne entsprechende `enum` Array. Siehe Tutorial zu [Definieren empfohlener Werte](../tutorials/suggested-values.md) für weitere Informationen.

Sie können optional eine `default` -Eigenschaft zum Angeben der Standardeinstellung `enum` -Wert, den das Feld verwendet, wenn kein Wert angegeben ist.

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
>Wenn nicht `default` -Wert angegeben und das Enum-Feld auf `required`festgelegt ist, schlägt die Validierung bei der Erfassung fehl, wenn für dieses Feld ein Wert fehlt.

## [!UICONTROL Zahl] {#number}

Zahlenfelder werden durch `type: number` und keine anderen erforderlichen Eigenschaften aufweisen.

```json
"sampleField": {
  "title": "Sample Number Field",
  "description": "An example number field.",
  "type": "number"
}
```

>[!NOTE]
>
>`number` -Typen werden für alle numerischen Typen verwendet, entweder Ganzzahlen oder Gleitkommazahlen, während [`integer` Typen](#integer) werden speziell für ganzzahlige Zahlen verwendet. Siehe Abschnitt [JSON-Schema-Dokumentation zu numerischen Typen](https://json-schema.org/understanding-json-schema/reference/numeric.html) für weitere Informationen zu den Anwendungsfällen für jeden Typ.

## [!UICONTROL Ganzzahl] {#integer}

[!UICONTROL Ganzzahl] -Felder werden durch `type: integer` und haben keine weiteren erforderlichen Felder.

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field.",
  "type": "integer"
}
```

>[!NOTE]
>
>while `integer` Typen beziehen sich insbesondere auf ganzzahlige Zahlen; [`number` Typen](#number) werden für alle numerischen Typen verwendet, entweder Ganzzahlen oder Gleitkommazahlen. Siehe Abschnitt [JSON-Schema-Dokumentation zu numerischen Typen](https://json-schema.org/understanding-json-schema/reference/numeric.html) für weitere Informationen zu den Anwendungsfällen für jeden Typ.

Sie können den Bereich der Ganzzahl optional einschränken, indem Sie `minimum` und `maximum` -Eigenschaften der Definition. Mehrere andere numerische Typen, die von der Schema Builder-Benutzeroberfläche unterstützt werden, sind `integer` Typen mit bestimmten `minimum` und `maximum` Einschränkungen wie [[!UICONTROL Lang]](#long), [[!UICONTROL Short]](#short)und [[!UICONTROL Byte]](#byte).

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field with added constraints.",
  "type": "integer",
  "minimum": 1,
  "maximum": 100
}
```

## [!UICONTROL Lang] {#long}

Das Äquivalent eines [!UICONTROL Lang] -Feld, das über die Schema Builder-Benutzeroberfläche erstellt wurde, ist ein [`integer` Typfeld](#integer) mit spezifischen `minimum` und `maximum` -Werte (`-9007199254740992` und `9007199254740992`, bzw. ).

```json
"sampleField": {
  "title": "Sample Long Field",
  "description": "An example long field.",
  "type": "integer",
  "minimum": -9007199254740992,
  "maximum": 9007199254740992
}
```

## [!UICONTROL Kurz] {#short}

Das Äquivalent eines [!UICONTROL Short] -Feld, das über die Schema Builder-Benutzeroberfläche erstellt wurde, ist ein [`integer` Typfeld](#integer) mit spezifischen `minimum` und `maximum` -Werte (`-32768` und `32768`, bzw. ).

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

Das Äquivalent eines [!UICONTROL Byte] -Feld, das über die Schema Builder-Benutzeroberfläche erstellt wurde, ist ein [`integer` Typfeld](#integer) mit spezifischen `minimum` und `maximum` -Werte (`-128` und `128`, bzw. ).

```json
"sampleField": {
  "title": "Sample Byte Field",
  "description": "An example byte field.",
  "type": "integer",
  "minimum": -128,
  "maximum": 128
}
```

## [!UICONTROL Boolesch] {#boolean}

[!UICONTROL Boolesch] -Felder werden durch `type: boolean`.

```json
"sampleField": {
  "title": "Sample Boolean Field",
  "description": "An example boolean field.",
  "type": "boolean"
}
```

Sie können optional eine `default` -Wert, den das Feld verwendet, wenn während der Erfassung kein expliziter Wert angegeben wird.

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
>Wenn nicht `default` -Wert angegeben und das boolesche Feld auf `required`festgelegt ist, schlägt die Validierung bei der Erfassung fehl, wenn für dieses Feld ein Wert fehlt.

## [!UICONTROL Datum] {#date}

[!UICONTROL Datum] -Felder werden durch `type: string` und `format: date`. Sie können optional auch ein Array von `examples` , um zu nutzen, wenn Sie eine Beispieldatumszeichenfolge für die manuelle Eingabe der Daten durch Benutzer anzeigen möchten.

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

[!UICONTROL DateTime] -Felder werden durch `type: string` und `format: date-time`. Sie können optional auch ein Array von `examples` , um zu nutzen, wenn Sie eine Beispiel-Datums-Uhrzeit-Zeichenfolge für Benutzer anzeigen möchten, die die Daten manuell eingeben.

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

[!UICONTROL Array] -Felder werden durch `type: array` und `items` -Objekt, das das Schema der Elemente definiert, die das Array akzeptiert.

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

Sie können die Array-Elemente auch basierend auf einem vorhandenen Datentyp definieren, indem Sie auf die `$id` des Datentyps durch `$ref` -Eigenschaft. Im Folgenden finden Sie ein Array von [!UICONTROL Zahlungselement] Objekte:

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

[!UICONTROL Objekt] -Felder werden durch `type: object` und `properties` -Objekt, das Untereigenschaften für das Schemafeld definiert.

Die einzelnen Unterfelder, die unter `properties` kann mit einem beliebigen Primitive definiert werden `type` oder durch Referenzierung eines vorhandenen Datentyps über eine `$ref` -Eigenschaft, die auf die `$id` des betreffenden Datentyps:

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

Sie können auch das gesamte Objekt definieren, indem Sie auf einen Datentyp verweisen, vorausgesetzt der betreffende Datentyp ist selbst definiert als `type: object`:

```json
"sampleField": {
  "title": "Sample Object Field",
  "description": "An example object field using a data type reference.",
  "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction"
}
```

## [!UICONTROL Landkarte] {#map}

Ein Zuordnungsfeld ist im Wesentlichen ein [`object`-Typ-Feld](#object) mit einem unbeschränkten Satz von Schlüsseln. Wie Objekte haben Karten eine `type` Wert von `object`, aber ihre `meta:xdmType` explizit auf `map`.

Karte **darf nicht** definieren beliebige Eigenschaften. Es **must** eine einzelne `additionalProperties` schema zur Beschreibung des Werttyps, der in der Zuordnung enthalten ist (jede Zuordnung kann nur einen einzigen Datentyp enthalten). Die `type` Wert muss entweder `string` oder `integer`.

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

Um &quot;map-ähnliche&quot;Daten in XDM effizient zu unterstützen, können Objekte mit einer `meta:xdmType` auf `map` , um deutlich zu machen, dass ein Objekt so verwaltet werden sollte, als wäre der Schlüsselsatz nicht eingeschränkt. Daten, die in Zuordnungsfelder aufgenommen werden, müssen Zeichenfolgenschlüssel und nur Zeichenfolgen- oder Ganzzahlwerte verwenden (wie durch `additionalProperties.type`).

XDM legt die folgenden Einschränkungen für die Verwendung dieses Speicherhinweises fest:

* Zuordnungstypen MÜSSEN vom Typ sein `object`.
* Für Zuordnungstypen dürfen KEINE Eigenschaften definiert sein (d. h. sie definieren &quot;leere&quot;Objekte).
* Zuordnungstypen MÜSSEN Folgendes enthalten: `additionalProperties.type` -Feld, das die Werte beschreibt, die in der Zuordnung platziert werden können, entweder `string` oder `integer`.

Stellen Sie sicher, dass Sie nur Felder vom Typ Zuordnung verwenden, wenn dies unbedingt erforderlich ist, da sie die folgenden Leistungsbeeinträchtigungen aufweisen:

* Reaktionszeit von [Adobe Experience Platform Query Service](../../query-service/home.md) wird bei 100 Millionen Datensätzen von drei auf zehn Sekunden reduziert.
* Karten mit weniger als 16 Schlüsseln müssen vorhanden sein. Andernfalls besteht die Gefahr einer weiteren Verschlechterung.

Die Benutzeroberfläche von Platform weist außerdem Einschränkungen hinsichtlich der Art und Weise auf, wie die Schlüssel von Feldern vom Typ Zuordnung extrahiert werden können. Während Objekttypen erweitert werden können, werden Zuordnungen stattdessen als ein einzelnes Feld angezeigt.

## Nächste Schritte

In diesem Handbuch wurde die Definition verschiedener Feldtypen in der API beschrieben. Weitere Informationen zur Formatierung von XDM-Feldtypen finden Sie im Handbuch unter [XDM-Feldtypbegrenzungen](../schema/field-constraints.md).
