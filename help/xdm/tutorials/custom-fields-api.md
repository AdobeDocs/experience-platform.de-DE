---
title: Definieren von XDM-Feldern in der Schema Registry-API
description: Erfahren Sie, wie Sie beim Erstellen benutzerdefinierter Experience-Datenmodell (XDM)-Ressourcen in der Schema Registry-API verschiedene Felder definieren können.
exl-id: d79332e3-8448-42af-b250-882bcb0f1e7d
source-git-commit: 7521273c0ea4383b7141e9d7a82953257ff18c34
workflow-type: tm+mt
source-wordcount: '1197'
ht-degree: 2%

---

# Definieren von XDM-Feldern in der Schema Registry-API

Alle Experience-Datenmodell (XDM)-Felder werden mithilfe der standardmäßigen [JSON-Schema](https://json-schema.org/)-Einschränkungen definiert, die für ihren Feldtyp gelten, mit zusätzlichen Einschränkungen für Feldnamen, die von Adobe Experience Platform erzwungen werden. Mit der Schema Registry-API können Sie benutzerdefinierte Felder in Ihren Schemata mithilfe von Formaten und optionalen Einschränkungen definieren. XDM-Feldtypen werden durch das Attribut auf Feldebene `meta:xdmType` verfügbar gemacht.

>[!NOTE]
>
>`meta:xdmType` ist ein systemgenerierter Wert. Daher müssen Sie diese Eigenschaft bei Verwendung der API nicht der JSON für Ihr Feld hinzufügen (außer beim [Erstellen benutzerdefinierter Zuordnungstypen](#custom-maps)). Best Practice ist die Verwendung von JSON-Schematypen (z. B. `string` und `integer`) mit den entsprechenden Min.-/Max.-Beschränkungen, wie in der folgenden Tabelle definiert.

In diesem Handbuch wird die entsprechende Formatierung zum Definieren verschiedener Feldtypen beschrieben, einschließlich derjenigen mit optionalen Eigenschaften. Weitere Informationen zu optionalen Eigenschaften und typspezifischen Suchbegriffen finden Sie in der Dokumentation zum [JSON-Schema](https://json-schema.org/understanding-json-schema/reference/type.html).

Suchen Sie zunächst den gewünschten Feldtyp und verwenden Sie den bereitgestellten Beispiel-Code, um Ihre API-Anfrage zum [Erstellen einer Feldergruppe](../api/field-groups.md#create) oder [Erstellen eines Datentyps](../api/data-types.md#create) zu erstellen.

## [!UICONTROL String] {#string}

[!UICONTROL Zeichenfolge] Felder werden durch `type: string` gekennzeichnet.

```json
"sampleField": {
  "title": "Sample String Field",
  "description": "An example string field.",
  "type": "string"
}
```

Sie können optional durch die folgenden zusätzlichen Eigenschaften einschränken, welche Arten von Werten für die Zeichenfolge eingegeben werden können:

* `pattern`: Ein Regex-Muster zur Einschränkung.
* `minLength`: Eine Mindestlänge für die Zeichenfolge. Zeichenfolgen erhalten standardmäßig einen Mindestwert von `1`.
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

[!UICONTROL URI]-Felder werden durch `type: string` gekennzeichnet, wobei die `format`-Eigenschaft auf `uri` gesetzt ist. Es werden keine anderen Eigenschaften akzeptiert.

```json
"sampleField": {
  "title": "Sample URI Field",
  "description": "An example URI field.",
  "type": "string",
  "format": "uri"
}
```

## [!UICONTROL enum] {#enum}

[!UICONTROL Enum]-Felder müssen `type: string` verwenden, wobei die Enum-Werte selbst unter einem `enum`-Array bereitgestellt werden:

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

Optional können Sie für jeden Wert unter einer `meta:enum`-Eigenschaft kundenseitige Beschriftungen angeben, wobei jede Beschriftung unter `enum` mit einem entsprechenden Wert versehen wird.

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
>Der `meta:enum`-Wert deklariert **keine**-Auflistung und steuert auch keine eigenständige Datenvalidierung. In den meisten Fällen werden die unter `meta:enum` bereitgestellten Zeichenfolgen auch unter `enum` bereitgestellt, um sicherzustellen, dass die Daten eingeschränkt sind. Es gibt jedoch einige Anwendungsfälle, in denen `meta:enum` ohne ein entsprechendes `enum`-Array bereitgestellt wird. Weitere Informationen finden Sie im Tutorial [Definieren ](../tutorials/suggested-values.md) empfohlenen Werten“.

Sie können optional eine `default`-Eigenschaft bereitstellen, um den standardmäßigen `enum` anzugeben, den das Feld verwenden wird, wenn kein Wert angegeben wird.

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
>Wenn kein `default` angegeben ist und das Aufzählungsfeld auf `required` festgelegt ist, schlägt die Validierung bei der Aufnahme jedes Datensatzes fehl, dem ein akzeptierter Wert für dieses Feld fehlt.

## [!UICONTROL Zahl] {#number}

Zahlenfelder werden durch `type: number` gekennzeichnet und haben keine anderen erforderlichen Eigenschaften.

```json
"sampleField": {
  "title": "Sample Number Field",
  "description": "An example number field.",
  "type": "number"
}
```

>[!NOTE]
>
>`number` Typen werden für beliebige numerische Typen verwendet, entweder Ganzzahlen oder Gleitkommazahlen, während [`integer` Typen ](#integer) ganzzahlige Zahlen spezifiziert sind. Weitere Informationen zu den Anwendungsfällen für [ einzelnen Typ finden ](https://json-schema.org/understanding-json-schema/reference/numeric.html) in der JSON-Schemadokumentation zu numerischen .

## [!UICONTROL Integer] {#integer}

[!UICONTROL Ganzzahl]-Felder werden durch `type: integer` gekennzeichnet und haben keine anderen erforderlichen Felder.

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field.",
  "type": "integer"
}
```

>[!NOTE]
>
>Während sich `integer` Typen auf ganzzahlige Zahlen beziehen, werden [`number` Typen ](#number) jedem numerischen Typ verwendet, entweder Ganzzahlen oder Gleitkommazahlen. Weitere Informationen zu den Anwendungsfällen für [ einzelnen Typ finden ](https://json-schema.org/understanding-json-schema/reference/numeric.html) in der JSON-Schemadokumentation zu numerischen .

Optional können Sie den Bereich der Ganzzahl einschränken, indem Sie der Definition `minimum`- und `maximum` hinzufügen. Einige andere numerische Typen, die von der Schema Builder-Benutzeroberfläche unterstützt werden, sind nur `integer` mit bestimmten `minimum` und `maximum` Einschränkungen, wie [[!UICONTROL Long]](#long), [[!UICONTROL Short]](#short) und [[!UICONTROL Byte]](#byte).

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

Das Äquivalent eines [!UICONTROL Long]-Felds, das über die Schema Builder-Benutzeroberfläche erstellt wurde, ist ein [`integer` Feld ](#integer) bestimmten `minimum` und `maximum` Werten (`-9007199254740992` bzw. `9007199254740992`).

```json
"sampleField": {
  "title": "Sample Long Field",
  "description": "An example long field.",
  "type": "integer",
  "minimum": -9007199254740992,
  "maximum": 9007199254740992
}
```

## [!UICONTROL kurz] {#short}

Das Äquivalent eines [!UICONTROL Short]-Felds, das über die Schema Builder-Benutzeroberfläche erstellt wurde, ist ein [`integer` Feld ](#integer) bestimmten `minimum` und `maximum` Werten (`-32768` bzw. `32768`).

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

Das Äquivalent eines [!UICONTROL Byte]-Felds, das über die Schema Builder-Benutzeroberfläche erstellt wurde, ist ein [`integer` Feld ](#integer) bestimmten `minimum` und `maximum` Werten (`-128` bzw. `128`).

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

[!UICONTROL Boolesch] Felder werden durch `type: boolean` gekennzeichnet.

```json
"sampleField": {
  "title": "Sample Boolean Field",
  "description": "An example boolean field.",
  "type": "boolean"
}
```

Sie können optional einen `default` Wert angeben, den das Feld verwendet, wenn bei der Aufnahme kein expliziter Wert angegeben wird.

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
>Wenn kein `default` angegeben ist und das boolesche Feld auf `required` gesetzt ist, schlägt die Validierung bei der Aufnahme jedes Datensatzes fehl, dem ein akzeptierter Wert für dieses Feld fehlt.

## [!UICONTROL Datum] {#date}

[!UICONTROL Datum]-Felder werden durch `type: string` und `format: date` gekennzeichnet. Sie können optional auch ein Array von `examples` bereitstellen, die in Fällen genutzt werden können, in denen Sie eine Beispiel-Datumszeichenfolge für Benutzer anzeigen möchten, die die Daten manuell eingeben.

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

[!UICONTROL DateTime]-Felder werden durch `type: string` und `format: date-time` gekennzeichnet. Sie können optional auch ein Array von `examples` bereitstellen, die in Fällen genutzt werden können, in denen Sie eine Beispiel-Datums-/Uhrzeitzeichenfolge für Benutzer anzeigen möchten, die die Daten manuell eingeben.

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

[!UICONTROL Array]-Felder werden durch `type: array` und ein `items`-Objekt angegeben, das das Schema der Elemente definiert, die das Array akzeptiert.

Sie können Array-Elemente mithilfe von primitiven Typen definieren, z. B. ein Array von Zeichenfolgen:

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

Sie können die Array-Elemente auch auf der Grundlage eines vorhandenen Datentyps definieren, indem Sie über eine `$ref`-Eigenschaft auf die `$id` des Datentyps verweisen. Im Folgenden finden Sie ein Array von [!UICONTROL Zahlungsartikel]-Objekten:

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

[!UICONTROL Objekt]-Felder werden durch `type: object` und ein `properties`-Objekt angegeben, das Untereigenschaften für das Schemafeld definiert.

Jedes unter `properties` definierte Unterfeld kann mit einem beliebigen primitiven `type` oder durch Verweis auf einen vorhandenen Datentyp über eine `$ref`-Eigenschaft definiert werden, die auf den `$id` des betreffenden Datentyps verweist:

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

Sie können auch das gesamte Objekt über definieren, indem Sie auf einen Datentyp verweisen, vorausgesetzt, der betreffende Datentyp selbst ist wie `type: object` definiert:

```json
"sampleField": {
  "title": "Sample Object Field",
  "description": "An example object field using a data type reference.",
  "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction"
}
```

## [!UICONTROL Landkarte] {#map}

Ein Zuordnungsfeld ist im Wesentlichen ein Feld vom Typ [`object` mit ](#object) nicht eingeschränkten Schlüsselsatz. Wie Objekte haben auch Karten einen `type` Wert von `object`, aber ihre `meta:xdmType` ist explizit auf `map` festgelegt.

Eine Zuordnung **darf** keine Eigenschaften definieren. Sie **muss** ein einzelnes `additionalProperties` definieren, um den Typ der in der Zuordnung enthaltenen Werte zu beschreiben (jede Zuordnung kann nur einen einzigen Datentyp enthalten). Der `type` muss entweder `string` oder `integer` sein.

Ein Zuordnungsfeld mit Werten vom Typ Zeichenfolge würde beispielsweise wie folgt definiert werden:

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

Im folgenden Abschnitt finden Sie weitere Details zum Erstellen benutzerdefinierter Zuordnungsfelder.

### Erstellen benutzerdefinierter Zuordnungstypen {#custom-maps}

Um „mapähnliche“ Daten in XDM effizient zu unterstützen, können -Objekte mit einem `meta:xdmType` versehen werden, der auf `map` gesetzt ist, um klarzustellen, dass ein -Objekt so verwaltet werden soll, als wäre der Schlüsselsatz nicht beschränkt. Daten, die in Zuordnungsfelder aufgenommen werden, müssen Zeichenfolgenschlüssel verwenden und nur Zeichenfolgen- oder Ganzzahlwerte (wie durch `additionalProperties.type` bestimmt).

XDM setzt die folgenden Einschränkungen für die Verwendung dieses Speicherhinweises:

* Zuordnungstypen MÜSSEN vom Typ `object` sein.
* Für Zuordnungstypen DÜRFEN KEINE Eigenschaften definiert sein (d. h. sie definieren „leere“ Objekte).
* Zuordnungstypen MÜSSEN ein `additionalProperties.type` enthalten, das die Werte beschreibt, die innerhalb der Zuordnung platziert werden können, entweder `string` oder `integer`.

Stellen Sie sicher, dass Sie Felder vom Typ Zuordnung nur verwenden, wenn dies unbedingt erforderlich ist, da sie die folgenden Leistungseinbußen aufweisen:

* Die Reaktionszeit von [Adobe Experience Platform Query Service](../../query-service/home.md) wird für 100 Millionen Datensätze von drei auf zehn Sekunden reduziert.
* Die Karten müssen weniger als 16 Schlüssel haben, da sonst eine weitere Beeinträchtigung droht.

Die Benutzeroberfläche von Experience Platform weist auch Einschränkungen hinsichtlich der Extraktion der Schlüssel von Feldern vom Typ Zuordnung auf. Während sich Felder vom Typ „Objekt“ erweitern lassen, werden Zuordnungen stattdessen als einzelnes Feld angezeigt.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie verschiedene Feldtypen in der API definieren. Weitere Informationen zur Formatierung von XDM-Feldtypen finden Sie im Handbuch zu [Begrenzungen für XDM-Feldtypen](../schema/field-constraints.md).
