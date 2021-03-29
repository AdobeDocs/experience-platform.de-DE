---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;Mixin;Mixin;Mixins;Mixins;Datentyp;Datentypen;Datentypen;Datentyp;Datenentwurf;Schema-Design;Datentyp;Datentyp;Datentyp;Schema;Schemas;Schema-Design;Map;Map;Map;
solution: Experience Platform
title: Einschränkungen des XDM-Feldtyps
topic: Übersicht
description: Eine Referenz für Feldtypeinschränkungen im Experience Data Model (XDM), einschließlich der anderen Serialisierungsformate, denen sie zugeordnet werden können, und wie Sie Ihre eigenen Feldtypen in der API definieren.
translation-type: tm+mt
source-git-commit: 456e595e66436c35c7d081ddf4699263e9c87234
workflow-type: tm+mt
source-wordcount: '1086'
ht-degree: 18%

---


# XDM-Feldtypeinschränkungen

In Experience Data Model-(XDM-)Schemas beschränkt der Feldtyp, welche Daten das Feld enthalten kann. Dieses Dokument bietet einen Überblick über die einzelnen Kernfeldtypen, einschließlich der anderen Serialisierungsformate, denen sie zugeordnet werden können, und wie Sie Ihre eigenen Feldtypen in der API definieren, um verschiedene Einschränkungen zu erzwingen.

## Erste Schritte

Bevor Sie dieses Handbuch verwenden, lesen Sie bitte die [Grundlagen der Schema-Komposition](./composition.md), um eine Einführung in XDM-Schemas, -Klassen und -Mixins zu erhalten.

Wenn Sie Ihre eigenen Feldtypen in der API definieren möchten, sollten Sie unbedingt mit dem [Schema Registry-Entwicklerhandbuch](../api/getting-started.md) Beginn haben, um zu erfahren, wie Mixins und Datentypen erstellt werden, die Ihre benutzerdefinierten Felder einschließen. Wenn Sie die Benutzeroberfläche für die Experience Platform verwenden, um Ihre Schema zu erstellen, lesen Sie das Handbuch zu [Definieren von Feldern in der Benutzeroberfläche](../ui/fields/overview.md), um zu erfahren, wie Sie Einschränkungen für Felder implementieren, die Sie in benutzerdefinierten Mixins und Datentypen definieren.

## Basisstruktur und Beispiele

XDM basiert auf dem JSON-Schema, und deshalb erben XDM-Felder eine ähnliche Syntax, wenn sie ihren Typ definieren. Wenn Sie wissen, wie verschiedene Feldtypen im JSON-Schema dargestellt werden, können Sie die Basisbeschränkungen der einzelnen Typen erkennen.

>[!NOTE]
>
>Weitere Informationen zu JSON-Schemas und anderen zugrunde liegenden Technologien in Plattform-APIs finden Sie im Handbuch [API-Grundlagen](../../landing/api-fundamentals.md#json-schema).

Die folgende Tabelle zeigt, wie jeder XDM-Typ im JSON-Schema dargestellt wird, zusammen mit einem Beispielwert, der dem Typ entspricht:

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
      <td>[!UICONTROL-Zeichenfolge]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type": "string"}</pre>
      </td>
      <td><code>"Platinum"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL-Dublette]</td>
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
      <td>[!UICONTROL-Datum]*</td>
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

Die folgenden Abschnitte beschreiben, wie jeder XDM-Typ anderen gängigen Serialisierungsformaten zugeordnet wird:

* [Parquet, Spark SQL und Java](#parquet)
* [Scala, .NET und CosmosDB](#scala)
* [MongoDB, Aerospike und Protobuf 2](#mongo)

>[!IMPORTANT]
>
>Unter den in den Tabellen unten aufgeführten Standard-XDM-Typen ist auch der Typ [!UICONTROL Map] enthalten. Karten werden in Standard-Schemas verwendet, wenn Daten als Schlüssel dargestellt werden, die bestimmten Werten zugeordnet sind, oder wenn Schlüssel vernünftigerweise nicht in ein statisches Schema eingeschlossen werden können und als Datenwerte behandelt werden müssen.
>
>Kartenfelder sind für die Verwendung von Schemas der Industrie und des Anbieters reserviert und können daher nicht in von Ihnen definierten benutzerdefinierten Ressourcen verwendet werden. Die Aufnahme des Map-Typs in die folgenden Tabellen soll Ihnen nur bei der Bestimmung helfen, wie Sie Ihre vorhandenen Daten XDM zuordnen, wenn sie derzeit in einem der unten aufgeführten Formate gespeichert sind.

### Parquet, Spark SQL und Java {#parquet}

| XDM-Typ | Parkett | Spark SQL | Java |
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
| [!UICONTROL Landkarte] | `MAP`-kommentierte Gruppe<br><br>(`<key-type>` muss  `STRING`sein) | `MapType`<br><br>(`keyType` muss  `StringType`) | `java.util.Map` |

### Scala, .NET und CosmosDB {#scala}

| XDM-Typ | Scala | .NET | CosmosDB |
| --- | --- | --- | --- |
| [!UICONTROL Zeichenfolge] | `String` | `System.String` | `String` |
| [!UICONTROL Dublette] | `Double` | `System.Double` | `Number` |
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
| [!UICONTROL Dublette] | `double` | `Double` | `double` |
| [!UICONTROL Lang] | `long` | `Integer` | `int64` |
| [!UICONTROL Ganzzahl] | `int` | `Integer` | `int32` |
| [!UICONTROL Kurz] | `int` | `Integer` | `int32` |
| [!UICONTROL Byte] | `int` | `Integer` | `int32` |
| [!UICONTROL Datum] | `date` | `Integer`<br>(Unix Millisekunden) | `int64`<br>(Unix Millisekunden) |
| [!UICONTROL DateTime] | `timestamp` | `Integer`<br>(Unix Millisekunden) | `int64`<br>(Unix Millisekunden) |
| [!UICONTROL Boolesch] | `bool` | `Integer`<br>(0/1 binär) | `bool` |
| [!UICONTROL Landkarte] | `object` | `map` | `map<key_type, value_type>` |

{style=&quot;table-layout:auto&quot;}

## Definieren von XDM-Feldtypen in der API {#define-fields}

Alle XDM-Felder werden mit den standardmäßigen Einschränkungen [JSON-Schema](https://json-schema.org/) definiert, die für den jeweiligen Feldtyp gelten, mit zusätzlichen Einschränkungen für Feldnamen, die von [!DNL Experience Platform] erzwungen werden. Mit der Schema Registry API können Sie zusätzliche Feldtypen mithilfe von Formaten und optionalen Einschränkungen definieren. XDM-Feldtypen werden durch das Attribut auf Feldebene, `meta:xdmType`, verfügbar gemacht.

>[!NOTE]
>
>`meta:xdmType` ist ein vom System generierter Wert. Daher müssen Sie diese Eigenschaft nicht zum JSON für Ihr Feld hinzufügen, wenn Sie die API verwenden. Es empfiehlt sich, JSON-Schema-Typen (z. B. `string` und `integer`) mit den entsprechenden Min-/Max-Einschränkungen zu verwenden, wie in der folgenden Tabelle definiert.

In der folgenden Tabelle sind die entsprechenden Formatierungen zur Definition verschiedener Feldtypen, einschließlich derjenigen mit optionalen Eigenschaften, aufgeführt. Weitere Informationen zu optionalen Eigenschaften und typspezifischen Suchbegriffen finden Sie in der Dokumentation zum [JSON-Schema](https://json-schema.org/understanding-json-schema/reference/type.html).

Suchen Sie zunächst den gewünschten Feldtyp und verwenden Sie den Beispielcode, der zum Erstellen Ihrer API-Anforderung für [Erstellen einer Mischung](../api/mixins.md#create) oder [zum Erstellen eines Datentyps](../api/data-types.md#create) bereitgestellt wird.

<table style="table-layout:auto">
  <tr>
    <th>XDM-Typ</th>
    <th>Optionale Eigenschaften</th>
    <th>Beispiel</th>
  </tr>
  <tr>
    <td>[!UICONTROL-Zeichenfolge]</td>
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
    <td>[!UICONTROL-URI]</td>
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
    <td>Eingeschränkte Enum-Werte werden unter dem Array <code>enum</code> bereitgestellt, während optionale kundenorientierte Beschriftungen für jeden Wert unter <code>meta:enum</code> bereitgestellt werden können:
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
    <td>[!UICONTROL-Datum]</td>
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
          "examples": ["2004-10-23T12:00:00-06:00"]
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL-Array]</td>
    <td></td>
    <td>Ein Array mit einfachen Skalartypen (z. B. Zeichenfolgen):
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
  "Elemente": {
    "$ref": "https://ns.adobe.com/xdm/data/paymentitem"
  }
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL-Objekt]</td>
    <td></td>
    <td>Das <code>type</code>-Attribut jedes unter <code>properties</code> definierten Unterfelds kann mit einem beliebigen Skalartyp definiert werden:
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
      Objekttypfelder können durch Verweis auf den Datentyp <code>$id</code> definiert werden:
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
    <td>Eine Map <strong>darf keine Eigenschaften definieren. </strong> <strong>muss</strong> ein einzelnes <code>additionalProperties</code>-Schema definieren, um den Werttyp zu beschreiben, der in der Zuordnung enthalten ist (jede Zuordnung kann nur einen einzigen Datentyp enthalten). Werte können ein beliebiges gültiges XDM <code>type</code>-Attribut oder ein Verweis auf ein anderes Schema mit einem <code>$ref</code>-Attribut sein.<br/><br/>Ein Zuordnungsfeld mit Zeichenfolgentypwerten:
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
    Ein Zuordnungsfeld, das auf einen anderen Datentyp verweist:
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
