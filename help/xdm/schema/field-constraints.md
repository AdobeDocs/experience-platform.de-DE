---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; Feldergruppe; Feldergruppe; Feldergruppen; Feldergruppen; Feldergruppen; Datentyp; Datentypen; Datentypen; Datentyp; Datentyp; Schemadesign; Schemadesign; Schemadesign; Zuordnung; Datentyp; Datentyp; Datentyp; Datentyp; Datentyp; Schemata; Schemas; Schemadesign; Map; Map
solution: Experience Platform
title: Einschränkungen für XDM-Feldtypen
topic-legacy: overview
description: Eine Referenz für Feldtypbegrenzungen im Experience-Datenmodell (XDM), einschließlich der anderen Serialisierungsformate, denen sie zugeordnet werden können, und wie Sie Ihre eigenen Feldtypen in der API definieren können.
exl-id: 63839a28-6d26-46f1-8bbf-b524e82ac4df
source-git-commit: a3b4dd65b22bb04bcba52c44a09030f51454a9c8
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 13%

---

# Begrenzungen für XDM-Feldtypen

In Experience-Datenmodell (XDM)-Schemas beschränkt der Typ eines Felds, welche Daten das Feld enthalten kann. Dieses Dokument bietet einen Überblick über die einzelnen Kernfeldtypen, einschließlich der anderen Serialisierungsformate, denen sie zugeordnet werden können, und wie Sie Ihre eigenen Feldtypen in der API definieren, um verschiedene Einschränkungen zu erzwingen.

## Erste Schritte

Bevor Sie dieses Handbuch verwenden, lesen Sie bitte die [Grundlagen der Schemakomposition](./composition.md) für eine Einführung in XDM-Schemas, Klassen und Schemafeldgruppen.

Wenn Sie Ihre eigenen Feldtypen in der API definieren möchten, wird dringend empfohlen, mit der [Entwicklerhandbuch zur Schema Registry](../api/getting-started.md) , um zu erfahren, wie Sie Feldergruppen und Datentypen erstellen, in die Ihre benutzerdefinierten Felder eingefügt werden. Wenn Sie zur Erstellung Ihrer Schemas die Experience Platform-Benutzeroberfläche verwenden, finden Sie im Handbuch unter [Definieren von Feldern in der Benutzeroberfläche](../ui/fields/overview.md) um zu erfahren, wie Sie Einschränkungen für Felder implementieren, die Sie in benutzerdefinierten Feldergruppen und Datentypen definieren.

## Basisstruktur und Beispiele {#basic-types}

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

>[!NOTE]
>
>Unter den in den folgenden Tabellen aufgeführten Standard-XDM-Typen ist die [!UICONTROL Zuordnung] Typ ist ebenfalls enthalten. Maps werden in Standardschemata verwendet, wenn Daten als Schlüssel dargestellt werden, die bestimmten Werten zugeordnet sind, oder wenn Schlüssel vernünftigerweise nicht in ein statisches Schema aufgenommen werden können und als Datenwerte behandelt werden müssen.
>
>Viele standardmäßige XDM-Komponenten verwenden Zuordnungstypen. Sie können auch [Definieren von benutzerdefinierten Zuordnungsfeldern](../tutorials/custom-fields-api.md#maps) falls gewünscht. Die Aufnahme des Zuordnungstyps in die folgenden Tabellen soll Ihnen dabei helfen festzustellen, wie Sie Ihre vorhandenen Daten XDM zuordnen können, wenn sie derzeit in einem der unten aufgeführten Formate gespeichert sind.

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

Mit der Schema Registry-API können Sie benutzerdefinierte Felder mithilfe von Formaten und optionalen Einschränkungen definieren. Siehe Handbuch unter [Definieren benutzerdefinierter Felder in der Schema Registry-API](../tutorials/custom-fields-api.md) für weitere Informationen.
