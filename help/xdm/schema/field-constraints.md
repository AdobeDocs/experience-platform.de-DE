---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; Feldergruppe; Feldergruppe; Feldergruppen; Feldergruppen; Feldergruppen; Datentyp; Datentypen; Datentypen; Datentyp; Datentyp; Schemata; Schemadesign; Schema-Design; map; Map; Map;
solution: Experience Platform
title: Einschränkungen für XDM-Feldtypen
topic-legacy: overview
description: Eine Referenz für Feldtypbegrenzungen im Experience-Datenmodell (XDM), einschließlich der anderen Serialisierungsformate, denen sie zugeordnet werden können, und wie Sie Ihre eigenen Feldtypen in der API definieren können.
exl-id: 63839a28-6d26-46f1-8bbf-b524e82ac4df
source-git-commit: 61025ada3a900a5bd7682e3bb7d4f6cd23347231
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 18%

---

# XDM-Feldtypbegrenzungen

In Experience-Datenmodell (XDM)-Schemas beschränkt der Typ eines Felds, welche Daten das Feld enthalten kann. Dieses Dokument bietet einen Überblick über die einzelnen Kernfeldtypen, einschließlich der anderen Serialisierungsformate, denen sie zugeordnet werden können, und wie Sie Ihre eigenen Feldtypen in der API definieren, um verschiedene Einschränkungen zu erzwingen.

## Erste Schritte

Bevor Sie dieses Handbuch verwenden, lesen Sie die [Grundlagen der Schemakomposition](./composition.md) , um eine Einführung in XDM-Schemas, Klassen und Schemafeldgruppen zu erhalten.

Wenn Sie planen, Ihre eigenen Feldtypen in der API zu definieren, wird dringend empfohlen, mit dem [Entwicklerhandbuch zur Schema Registry](../api/getting-started.md) zu beginnen, um zu erfahren, wie Sie Feldergruppen und Datentypen erstellen, in die Ihre benutzerdefinierten Felder eingeschlossen werden. Wenn Sie zur Erstellung Ihrer Schemas die Experience Platform-Benutzeroberfläche verwenden, finden Sie im Handbuch zum Definieren von  in der Benutzeroberfläche](../ui/fields/overview.md) Informationen dazu, wie Sie Einschränkungen für Felder implementieren, die Sie in benutzerdefinierten Feldergruppen und Datentypen definieren.[

## Basisstruktur und Beispiele

XDM basiert auf dem JSON-Schema und daher erben XDM-Felder bei der Definition ihres Typs eine ähnliche Syntax. Wenn Sie wissen, wie verschiedene Feldtypen im JSON-Schema dargestellt werden, können Sie die grundlegenden Einschränkungen der einzelnen Typen anzeigen.

>[!NOTE]
>
>Weitere Informationen zum JSON-Schema und anderen zugrunde liegenden Technologien in Platform-APIs finden Sie im [API-Grundlagenhandbuch](../../landing/api-fundamentals.md#json-schema) .

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
{
  "type": "integer",
  "maximum": 9007199254740991,
  "minimum": -9007199254740991
}</pre>
      </td>
      <td><code>1478108935</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Integer]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type": "integer",
  "maximum": 2147483648,
  "minimum": -2147483648
}</pre>
      </td>
      <td><code>24906290</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Short]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type": "integer",
  "maximum": 32768,
  "minimum": -32768
}</pre>
      </td>
      <td><code>15781</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Byte]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type": "integer",
  "maximum": 128,
  "minimum": -128
}</pre>
      </td>
      <td><code>90</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Datum]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type": "string",
  "format": "date"
}</pre>
      </td>
      <td><code>"2019-05-15"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL DateTime]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type": "string",
  "format": "date-time"
}</pre>
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

**Alle datumsformatierten Zeichenfolgen müssen dem ISO 8601-Standard ([RFC 3339, Abschnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)) entsprechen.*

## Zuordnen von XDM-Typen zu anderen Formaten

In den folgenden Abschnitten wird beschrieben, wie die einzelnen XDM-Typen anderen gängigen Serialisierungsformaten zugeordnet werden:

* [Parquet, Spark SQL und Java](#parquet)
* [Scala, .NET und CosmosDB](#scala)
* [MongoDB, Aerospike und Protobuf 2](#mongo)

>[!IMPORTANT]
>
>Unter den in den folgenden Tabellen aufgeführten Standard-XDM-Typen ist auch der Typ [!UICONTROL Map] enthalten. Maps werden in Standardschemata verwendet, wenn Daten als Schlüssel dargestellt werden, die bestimmten Werten zugeordnet sind, oder wenn Schlüssel vernünftigerweise nicht in ein statisches Schema aufgenommen werden können und als Datenwerte behandelt werden müssen.
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
| [!UICONTROL Landkarte] | `MAP`-kommentierte Gruppe<br><br> (`<key-type>` muss  `STRING`sein) | `MapType`<br><br>(`keyType` muss  `StringType`) | `java.util.Map` |

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

Alle XDM-Felder werden mit den standardmäßigen [JSON-Schema](https://json-schema.org/)-Einschränkungen definiert, die für ihren Feldtyp gelten, mit zusätzlichen Einschränkungen für Feldnamen, die von [!DNL Experience Platform] erzwungen werden. Mit der Schema Registry-API können Sie zusätzliche Feldtypen mithilfe von Formaten und optionalen Einschränkungen definieren. XDM-Feldtypen werden durch das Attribut auf Feldebene verfügbar gemacht, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` ist ein systemgenerierter Wert. Daher müssen Sie diese Eigenschaft bei Verwendung der API nicht zum JSON für Ihr Feld hinzufügen. Es empfiehlt sich, JSON-Schematypen (wie `string` und `integer`) mit den entsprechenden Min-/Max-Einschränkungen zu verwenden, wie in der folgenden Tabelle definiert.

In der folgenden Tabelle wird die entsprechende Formatierung zum Definieren verschiedener Feldtypen einschließlich derjenigen mit optionalen Eigenschaften beschrieben. Weitere Informationen zu optionalen Eigenschaften und typspezifischen Suchbegriffen finden Sie in der Dokumentation zum [JSON-Schema](https://json-schema.org/understanding-json-schema/reference/type.html).

Suchen Sie zunächst den gewünschten Feldtyp und verwenden Sie den Beispielcode, der zum Erstellen Ihrer API-Anfrage für [Erstellen einer Feldergruppe](../api/field-groups.md#create) oder [Erstellen eines Datentyps](../api/data-types.md#create) bereitgestellt wird.

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
    <td>Begrenzte Enum-Werte werden unter dem Array <code>enum</code> bereitgestellt, während optionale kundenorientierte Beschriftungen für jeden Wert unter <code>meta:enum</code> bereitgestellt werden können:
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
"sampleField": {
  "type": "string",
  "format": "date-time",
  "example": ["2004-10-23T12:00:00-06:00"]
}</pre>
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
"sampleField": {
  "type": "array",
  "items": {
    "$ref": "https://ns.adobe.com/xdm/data/paymentitem"
  }
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Objekt]</td>
    <td></td>
    <td>Das Attribut <code>type</code> jedes unter <code>properties</code> definierten Unterfelds kann mit einem beliebigen Skalartyp definiert werden:
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
      Objekttypfelder können definiert werden, indem auf die <code>$id</code> eines Datentyps verwiesen wird:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "object",
  "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Map]</td>
    <td></td>
    <td>Eine Zuordnung <strong>darf keine</strong> Eigenschaften definieren. <strong>muss</strong> ein einzelnes <code>additionalProperties</code>-Schema definieren, um den Typ der in der Zuordnung enthaltenen Werte zu beschreiben (jede Zuordnung kann nur einen einzigen Datentyp enthalten). Werte können ein beliebiges gültiges XDM <code>type</code>-Attribut oder ein Verweis auf ein anderes Schema mit einem <code>$ref</code>-Attribut sein.<br/><br/>Ein Zuordnungsfeld mit Werten vom Typ Zeichenfolge:
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
"sampleField": {
  "type": "object",
  "additionalProperties":{
    "$ref": "https://ns.adobe.com/xdm/data/paymentitem"
  }
}</pre>
    </td>
  </tr>
</table>
