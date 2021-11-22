---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; Feldergruppe; Feldergruppe; Feldergruppen; Feldergruppen; Feldergruppen; Datentyp; Datentypen; Datentypen; Datentyp; Datentyp; Schemadesign; Schemadesign; Schemadesign; Zuordnung; Datentyp; Datentyp; Datentyp; Datentyp; Datentyp; Schemata; Schemas; Schemadesign; Map; Map
solution: Experience Platform
title: Einschränkungen für XDM-Feldtypen
topic-legacy: overview
description: Eine Referenz für Feldtypbegrenzungen im Experience-Datenmodell (XDM), einschließlich der anderen Serialisierungsformate, denen sie zugeordnet werden können, und wie Sie Ihre eigenen Feldtypen in der API definieren können.
exl-id: 63839a28-6d26-46f1-8bbf-b524e82ac4df
source-git-commit: 684237122e7384f6c611e1c602c30af2518aba58
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 17%

---

# XDM-Feldtypbegrenzungen

In Experience-Datenmodell (XDM)-Schemas beschränkt der Typ eines Felds, welche Daten das Feld enthalten kann. Dieses Dokument bietet einen Überblick über die einzelnen Kernfeldtypen, einschließlich der anderen Serialisierungsformate, denen sie zugeordnet werden können, und wie Sie Ihre eigenen Feldtypen in der API definieren, um verschiedene Einschränkungen zu erzwingen.

## Erste Schritte

Bevor Sie dieses Handbuch verwenden, lesen Sie bitte die [Grundlagen der Schemakomposition](./composition.md) für eine Einführung in XDM-Schemas, Klassen und Schemafeldgruppen.

Wenn Sie Ihre eigenen Feldtypen in der API definieren möchten, wird dringend empfohlen, mit der [Entwicklerhandbuch zur Schema Registry](../api/getting-started.md) , um zu erfahren, wie Sie Feldergruppen und Datentypen erstellen, in die Ihre benutzerdefinierten Felder eingefügt werden. Wenn Sie zur Erstellung Ihrer Schemas die Experience Platform-Benutzeroberfläche verwenden, finden Sie im Handbuch unter [Definieren von Feldern in der Benutzeroberfläche](../ui/fields/overview.md) um zu erfahren, wie Sie Einschränkungen für Felder implementieren, die Sie in benutzerdefinierten Feldergruppen und Datentypen definieren.

## Basisstruktur und Beispiele

XDM basiert auf dem JSON-Schema und daher erben XDM-Felder bei der Definition ihres Typs eine ähnliche Syntax. Wenn Sie wissen, wie verschiedene Feldtypen im JSON-Schema dargestellt werden, können Sie die grundlegenden Einschränkungen der einzelnen Typen anzeigen.

>[!NOTE]
>
>Siehe [API-Grundlagenhandbuch](../../landing/api-fundamentals.md#json-schema) Weitere Informationen zum JSON-Schema und anderen zugrunde liegenden Technologien in Platform-APIs.

In der folgenden Tabelle wird beschrieben, wie jeder XDM-Typ im JSON-Schema dargestellt wird, zusammen mit einem Beispielwert, der dem Typ entspricht:

<table style="table-layout:auto">
  <thead>
    <tr>
      <th>XDM-Typ</th>
      <th>JSON-Schema</th>
      <th>Beispiel</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>[!UICONTROL String]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type": "string"}</pre>
      </td>
      <td><code>"Platinum"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Double]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type": "number"}</pre>
      </td>
      <td><code>12925.49</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Long]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "integer", "maximum": 9007199254740991, "Minimum": -9007199254740991 }</pre>
      </td>
      <td><code>1478108935</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Integer]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "integer", "maximum": 2147483648, "Minimum": -2147483648 }</pre>
      </td>
      <td><code>24906290</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Short]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "integer", "maximum": 32768, "Minimum": -32768 }</pre>
      </td>
      <td><code>15781</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Byte]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "integer", "maximum": 128, "Minimum": -128 }</pre>
      </td>
      <td><code>90</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Datum]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "string", "format": "date" }</pre>
      </td>
      <td><code>"2019-05-15"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL DateTime]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "string", "format": "date-time" }</pre>
      </td>
      <td><code>"2019-05-15T20:20:39+00:00"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Boolean]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type": "string"}</pre>
      </td>
      <td><code>true</code></td>
    </tr>
  </tbody>
</table>

**Alle datumsformatierten Zeichenfolgen müssen dem ISO 8601-Standard ([RFC 3339, Abschnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)).*

## Zuordnen von XDM-Typen zu anderen Formaten

In den folgenden Abschnitten wird beschrieben, wie die einzelnen XDM-Typen anderen gängigen Serialisierungsformaten zugeordnet werden:

* [Parquet, Spark SQL und Java](#parquet)
* [Scala, .NET und CosmosDB](#scala)
* [MongoDB, Aerospike und Protobuf 2](#mongo)

>[!IMPORTANT]
>
>Unter den in den folgenden Tabellen aufgeführten Standard-XDM-Typen ist die [!UICONTROL Zuordnung] Typ ist ebenfalls enthalten. Maps werden in Standardschemata verwendet, wenn Daten als Schlüssel dargestellt werden, die bestimmten Werten zugeordnet sind, oder wenn Schlüssel vernünftigerweise nicht in ein statisches Schema aufgenommen werden können und als Datenwerte behandelt werden müssen.
>
>Felder vom Typ Zuordnung sind für die Verwendung des Branchen- und Händlerschemas reserviert und können daher nicht in von Ihnen definierten benutzerdefinierten Ressourcen verwendet werden. Die Einbindung des Zuordnungstyps in die folgenden Tabellen soll Ihnen nur bei der Bestimmung der Zuordnung Ihrer vorhandenen Daten zu XDM helfen, wenn diese derzeit in einem der unten aufgeführten Formate gespeichert sind.

### Parquet, Spark SQL und Java {#parquet}

| XDM-Typ | Parquet | Spark SQL | Java |
| --- | --- | --- | --- |
| [!UICONTROL Zeichenfolge] | Typ: `BYTE_ARRAY`<br>Anmerkung: `UTF8` | `StringType` | `java.lang.String` |
| [!UICONTROL Double] | Typ: `DOUBLE` | `LongType` | `java.lang.Double` |
| [!UICONTROL Lang] | Typ: `INT64` | `LongType` | `java.lang.Long` |
| [!UICONTROL Ganzzahl] | Typ: `INT32`<br>Anmerkung: `INT_32` | `IntegerType` | `java.lang.Integer` |
| [!UICONTROL Kurz] | Typ: `INT32`<br>Anmerkung: `INT_16` | `ShortType` | `java.lang.Short` |
| [!UICONTROL Byte] | Typ: `INT32`<br>Anmerkung: `INT_8` | `ByteType` | `java.lang.Short` |
| [!UICONTROL Datum] | Typ: `INT32`<br>Anmerkung: `DATE` | `DateType` | `java.util.Date` |
| [!UICONTROL DateTime] | Typ: `INT64`<br>Anmerkung: `TIMESTAMP_MILLIS` | `TimestampType` | `java.util.Date` |
| [!UICONTROL Boolesch] | Typ: `BOOLEAN` | `BooleanType` | `java.lang.Boolean` |
| [!UICONTROL Landkarte] | `MAP`-kommentierte Gruppe<br><br>(`<key-type>` muss `STRING`) | `MapType`<br><br>(`keyType` muss `StringType`) | `java.util.Map` |

{style=&quot;table-layout:auto&quot;}

### Scala, .NET und CosmosDB {#scala}

| XDM-Typ | Scala | .NET | CosmosDB |
| --- | --- | --- | --- |
| [!UICONTROL Zeichenfolge] | `String` | `System.String` | `String` |
| [!UICONTROL Double] | `Double` | `System.Double` | `Number` |
| [!UICONTROL Lang] | `Long` | `System.Int64` | `Number` |
| [!UICONTROL Ganzzahl] | `Int` | `System.Int32` | `Number` |
| [!UICONTROL Kurz] | `Short` | `System.Int16` | `Number` |
| [!UICONTROL Byte] | `Byte` | `System.SByte` | `Number` |
| [!UICONTROL Datum] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL DateTime] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL Boolesch] | `Boolean` | `System.Boolean` | `Boolean` |
| [!UICONTROL Landkarte] | `Map` | (Nicht angegeben) | `object` |

{style=&quot;table-layout:auto&quot;}

### MongoDB, Aerospike und Protobuf 2 {#mongo}

| XDM-Typ | MongoDB | Aerospike | Protobuf 2 |
| --- | --- | --- | --- |
| [!UICONTROL Zeichenfolge] | `string` | `String` | `string` |
| [!UICONTROL Double] | `double` | `Double` | `double` |
| [!UICONTROL Lang] | `long` | `Integer` | `int64` |
| [!UICONTROL Ganzzahl] | `int` | `Integer` | `int32` |
| [!UICONTROL Kurz] | `int` | `Integer` | `int32` |
| [!UICONTROL Byte] | `int` | `Integer` | `int32` |
| [!UICONTROL Datum] | `date` | `Integer`<br>(Unix-Millisekunden) | `int64`<br>(Unix-Millisekunden) |
| [!UICONTROL DateTime] | `timestamp` | `Integer`<br>(Unix-Millisekunden) | `int64`<br>(Unix-Millisekunden) |
| [!UICONTROL Boolesch] | `bool` | `Integer`<br>(0/1 binär) | `bool` |
| [!UICONTROL Landkarte] | `object` | `map` | `map<key_type, value_type>` |

{style=&quot;table-layout:auto&quot;}

## Definieren von XDM-Feldtypen in der API {#define-fields}

Alle XDM-Felder werden mithilfe des Standards definiert [JSON-Schema](https://json-schema.org/) Einschränkungen, die für ihren Feldtyp gelten, mit zusätzlichen Einschränkungen für Feldnamen, die von [!DNL Experience Platform]. Mit der Schema Registry-API können Sie zusätzliche Feldtypen mithilfe von Formaten und optionalen Einschränkungen definieren. XDM-Feldtypen werden durch das Attribut auf Feldebene verfügbar gemacht, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` ist ein systemgenerierter Wert. Daher müssen Sie diese Eigenschaft bei Verwendung der API nicht zum JSON für Ihr Feld hinzufügen. Es empfiehlt sich, JSON-Schematypen zu verwenden (z. B. `string` und `integer`) mit den entsprechenden Mindest-/Höchstbeschränkungen, wie in der folgenden Tabelle definiert.

In der folgenden Tabelle wird die entsprechende Formatierung zum Definieren verschiedener Feldtypen einschließlich derjenigen mit optionalen Eigenschaften beschrieben. Weitere Informationen zu optionalen Eigenschaften und typspezifischen Suchbegriffen finden Sie in der Dokumentation zum [JSON-Schema](https://json-schema.org/understanding-json-schema/reference/type.html).

Suchen Sie zunächst den gewünschten Feldtyp und verwenden Sie den Beispielcode, der zum Erstellen Ihrer API-Anfrage für bereitgestellt wird. [Erstellen einer Feldergruppe](../api/field-groups.md#create) oder [Erstellen eines Datentyps](../api/data-types.md#create).

<table style="table-layout:auto">
  <tr>
    <th>XDM-Typ</th>
    <th>Optionale Eigenschaften</th>
    <th>Beispiel</th>
  </tr>
  <tr>
    <td>[!UICONTROL String]</td>
    <td>
      <ul>
        <li><code>pattern</code></li>
        <li><code>minLength</code></li>
        <li><code>maxLength</code></li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
            "type": "string",
            "pattern": "^[A-Z]{2}$",
            "maxLength": 2
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL URI]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
          "type": "string",
          "format": "uri"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Enum]</td>
    <td>
      <ul>
        <li><code>default</code></li>
        <li><code>meta:enum</code></li>
      </ul>
    </td>
    <td>Begrenzte Enum-Werte werden unter der <code>enum</code> Array, während optionale kundenorientierte Beschriftungen für jeden Wert unter bereitgestellt werden können. <code>meta:enum</code>:
      <pre class="JSON language-JSON hljs">
"sampleField": {
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
}</pre>
    <br>Beachten Sie Folgendes: <code>meta:enum</code> Wert: <strong>not</strong> Deklarieren Sie eine Auflistung oder führen Sie eine Datenvalidierung allein durch. In den meisten Fällen werden unter <code>meta:enum</code> werden auch <code>enum</code> , um sicherzustellen, dass die Daten begrenzt sind. Es gibt jedoch einige Anwendungsfälle, in denen <code>meta:enum</code> ohne entsprechende <code>enum</code> Array. Siehe Tutorial zu <a href="../tutorials/extend-soft-enum.md">Erweitern von Soft Enves</a> für weitere Informationen.
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Number]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
          "type": "number"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Long]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
          "type": "integer",
          "minimum": -9007199254740992,
          "maximum": 9007199254740992
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Integer]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
          "type": "integer",
          "minimum": -2147483648,
          "maximum": 2147483648
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Short]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
          "type": "integer",
          "minimum": -32768,
          "maximum": 32768
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Byte]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
          "type": "integer",
          "minimum": -128,
          "maximum": 128
  }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Boolean]</td>
    <td>
      <ul>
        <li><code>default</code></li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
          "type": "boolean",
          "default": false
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Datum]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
          "type": "string",
          "format": "date",
          "examples": ["2004-10-23"]
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL DateTime]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "string", "format": "date-time", "example": ["2004-10-23T12:00:00-06:00"] }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Array]</td>
    <td></td>
    <td>Ein Array grundlegender Skalartypen (z. B. Zeichenfolgen):
      <pre class="JSON language-JSON hljs">
"sampleField": {
          "type": "array",
          "items": {
            "type": "string"
  }
}</pre>
      Ein Array von Objekten, die durch ein anderes Schema definiert werden:<br/>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "array", "items": { "$ref": "https://ns.adobe.com/xdm/data/paymentitem" } }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Objekt]</td>
    <td></td>
    <td>Die <code>type</code> -Attribut jedes Unterfelds, das unter <code>properties</code> kann mit einem beliebigen Skalartyp definiert werden:
      <pre class="JSON language-JSON hljs">
"sampleField": {
          "type": "object",
          "properties": {
            "field1": {
              "type": "string"
            },
            "field2": {
              "type": "number"
    }
  }
}</pre>
      Objekttypfelder können definiert werden, indem auf die <code>$id</code> eines Datentyps:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction" }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Map]</td>
    <td></td>
    <td>Karte <strong>darf nicht</strong> definieren beliebige Eigenschaften. Es <strong>must</strong> eine einzelne <code>additionalProperties</code> schema zur Beschreibung des Werttyps, der in der Zuordnung enthalten ist (jede Zuordnung kann nur einen einzigen Datentyp enthalten). Werte können beliebige gültige XDM-Werte sein. <code>type</code> -Attribut oder einen Verweis auf ein anderes Schema mithilfe eines <code>$ref</code> -Attribut.<br/><br/>Ein Zuordnungsfeld mit Werten vom Typ Zeichenfolge:
      <pre class="JSON language-JSON hljs">
"sampleField": {
          "type": "object",
          "additionalProperties":{
            "type": "string"
  }
}</pre>
    Ein Zuordnungsfeld mit Zeichenfolgen-Arrays für Werte:
      <pre class="JSON language-JSON hljs">
"sampleField": {
          "type": "object",
          "additionalProperties":{
            "type": "array",
            "items": {
              "type": "string"
    }
  }
}</pre>
    Ein map -Feld, das auf einen anderen Datentyp verweist:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "additionalProperties":{ "$ref": "https://ns.adobe.com/xdm/data/paymentitem" } }</pre>
    </td>
  </tr>
</table>
