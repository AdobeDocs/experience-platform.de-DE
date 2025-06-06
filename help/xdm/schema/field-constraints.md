---
keywords: Experience Platform;Startseite;beliebte Themen;schema;Schema;Feldergruppe;Feldergruppe;Feldergruppen;Feldergruppen;Datentyp;Datentypen;Datentypen;Datentyp;Schemadesign;Datentyp;Datentyp;Datentyp;Datentyp;Datentyp;Datentyp;Schemas;Schemadesign;Zuordnung;Zuordnung;
solution: Experience Platform
title: Begrenzungen für XDM-Feldtypen
description: Eine Referenz für Feldtypbegrenzungen im Experience-Datenmodell (XDM), einschließlich der anderen Serialisierungsformate, denen sie zugeordnet werden können, und für die Definition Ihrer eigenen Feldtypen in der API.
exl-id: 63839a28-6d26-46f1-8bbf-b524e82ac4df
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 7%

---

# Begrenzungen für XDM-Feldtypen

In Experience-Datenmodell (XDM)-Schemata schränkt der Typ eines Felds ein, welche Art von Daten das Feld enthalten kann. Dieses Dokument bietet einen Überblick über jeden Kernfeldtyp, einschließlich der anderen Serialisierungsformate, denen sie zugeordnet werden können, und wie Sie Ihre eigenen Feldtypen in der API definieren, um verschiedene Einschränkungen durchzusetzen.

## Erste Schritte

Bevor Sie dieses Handbuch verwenden, lesen Sie die [Grundlagen der Schemakomposition](./composition.md) für eine Einführung in XDM-Schemata, Klassen und Schemafeldgruppen.

Wenn Sie Ihre eigenen Feldtypen in der API definieren möchten, wird dringend empfohlen, mit dem [Entwicklerhandbuch zur Schemaregistrierung](../api/getting-started.md) zu beginnen, um zu erfahren, wie Sie Feldergruppen und Datentypen erstellen, um Ihre benutzerdefinierten Felder in einzuschließen. Wenn Sie die Experience Platform-Benutzeroberfläche zum Erstellen Ihrer Schemata verwenden, erfahren Sie im Handbuch unter [Definieren von Feldern in der Benutzeroberfläche](../ui/fields/overview.md) , wie Sie Einschränkungen für Felder implementieren, die Sie in benutzerdefinierten Feldergruppen und Datentypen definieren.

## Basisstruktur und Beispiele {#basic-types}

XDM basiert auf dem JSON-Schema und daher übernehmen XDM-Felder beim Definieren ihres Typs eine ähnliche Syntax. Wenn Sie verstehen, wie verschiedene Feldtypen im JSON-Schema dargestellt werden, können Sie die grundlegenden Einschränkungen jedes Typs angeben. Bei benutzerdefinierten Feldnamen wird nicht zwischen Groß- und Kleinschreibung unterschieden und sie müssen unterschiedliche Namen auf derselben Ebene in Ihrem Schema haben.

>[!NOTE]
>
>Weitere Informationen zu JSON[Schemas und anderen zugrunde liegenden Technologien in Experience Platform-APIs finden ](../../landing/api-fundamentals.md#json-schema) im Handbuch zu den API-Grundlagen .

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
{„type“: „string“}</pre>
      </td>
      <td><code>"Platinum"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL -Nummer]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{type}: „number“&rbrace;</pre>
      </td>
      <td><code>12925.49</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Long]</td>
      <td>
        <pre class="JSON language-JSON hljs">
&lbrace;
  „type“: „integer“,
  „maximum“: 9007199254740991,
  „minimum“: -9007199254740991
&rbrace;</pre>
      </td>
      <td><code>1478108935</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Ganzzahl]</td>
      <td>
        <pre class="JSON language-JSON hljs">
&lbrace;
  „type“: „integer“,
  „maximum“: 2147483648,
  „minimum“: -2147483648
&rbrace;</pre>
      </td>
      <td><code>24906290</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL short]</td>
      <td>
        <pre class="JSON language-JSON hljs">
&lbrace;
  „type“: „integer“,
  „maximum“: 32768,
  „minimum“: -32768
&rbrace;</pre>
      </td>
      <td><code>15781</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Byte]</td>
      <td>
        <pre class="JSON language-JSON hljs">
&lbrace;
  „type“: „integer“,
  „Maximum“: 128,
  „minimum“: -128
&rbrace;</pre>
      </td>
      <td><code>90</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Datum]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
&lbrace;
  „type“: „string“,
  „format“: „date“
&rbrace;</pre>
      </td>
      <td><code>"2019-05-15"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL DateTime]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
&lbrace;
  „type“: „string“,
  „format“: „date-time“
&rbrace;</pre>
      </td>
      <td><code>"2019-05-15T20:20:39+00:00"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Boolesch]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{„type“: „boolean“}</pre>
      </td>
      <td><code>true</code></td>
    </tr>
  </tbody>
</table>

**Alle datumsformatierten Zeichenfolgen müssen dem ISO 8601-Standard entsprechen ([RFC 3339, Abschnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)).*

## Zuordnen von XDM-Typen zu anderen Formaten

In den folgenden Abschnitten wird beschrieben, wie jeder XDM-Typ anderen gängigen Serialisierungsformaten zugeordnet wird:

* [Parquet, Spark SQL und Java](#parquet)
* [Scala, .NET und CosmosDB](#scala)
* [MongoDB, Aerospike und Protobuf 2](#mongo)

>[!NOTE]
>
>Unter den in den folgenden Tabellen aufgelisteten Standard-XDM-Typen ist auch [!UICONTROL &#x200B; Typ &#x200B;]Map“ enthalten. Zuordnungen werden in Standardschemata verwendet, wenn Daten als Schlüssel dargestellt werden, die bestimmten Werten zugeordnet sind, oder wenn Schlüssel nicht sinnvoll in ein statisches Schema aufgenommen werden können und als Datenwerte behandelt werden müssen.
>
>Viele standardmäßige XDM-Komponenten verwenden Zuordnungstypen und Sie können bei [ auch benutzerdefinierte Zuordnungsfelder ](../tutorials/custom-fields-api.md#custom-maps). Die Aufnahme des Zuordnungstyps in die folgenden Tabellen soll Ihnen dabei helfen, zu bestimmen, wie Sie Ihre vorhandenen Daten XDM zuordnen, wenn sie derzeit in einem der unten aufgeführten Formate gespeichert sind.

### Parquet, Spark SQL und Java {#parquet}

| XDM-Typ | Parquet | Spark SQL | Java |
| --- | --- | --- | --- |
| [!UICONTROL String] | Typ: `BYTE_ARRAY`<br>Anmerkung: `UTF8` | `StringType` | `java.lang.String` |
| [!UICONTROL Zahl] | Typ: `DOUBLE` | `LongType` | `java.lang.Double` |
| [!UICONTROL Lang] | Typ: `INT64` | `LongType` | `java.lang.Long` |
| [!UICONTROL Integer] | Typ: `INT32`<br>Anmerkung: `INT_32` | `IntegerType` | `java.lang.Integer` |
| [!UICONTROL kurz] | Typ: `INT32`<br>Anmerkung: `INT_16` | `ShortType` | `java.lang.Short` |
| [!UICONTROL Byte] | Typ: `INT32`<br>Anmerkung: `INT_8` | `ByteType` | `java.lang.Short` |
| [!UICONTROL Datum] | Typ: `INT32`<br>Anmerkung: `DATE` | `DateType` | `java.util.Date` |
| [!UICONTROL DateTime] | Typ: `INT64`<br>Anmerkung: `TIMESTAMP_MILLIS` | `TimestampType` | `java.util.Date` |
| [!UICONTROL Boolesch] | Typ: `BOOLEAN` | `BooleanType` | `java.lang.Boolean` |
| [!UICONTROL Landkarte] | Gruppe mit `MAP` Anmerkungen<br><br>(`<key-type>` muss `STRING` sein) | `MapType`<br><br>(`keyType` muss `StringType` sein) | `java.util.Map` |

{style="table-layout:auto"}

### Scala, .NET und CosmosDB {#scala}

| XDM-Typ | Scala | .NET | CosmosDB |
| --- | --- | --- | --- |
| [!UICONTROL String] | `String` | `System.String` | `String` |
| [!UICONTROL Zahl] | `Double` | `System.Double` | `Number` |
| [!UICONTROL Lang] | `Long` | `System.Int64` | `Number` |
| [!UICONTROL Integer] | `Int` | `System.Int32` | `Number` |
| [!UICONTROL kurz] | `Short` | `System.Int16` | `Number` |
| [!UICONTROL Byte] | `Byte` | `System.SByte` | `Number` |
| [!UICONTROL Datum] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL DateTime] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL Boolesch] | `Boolean` | `System.Boolean` | `Boolean` |
| [!UICONTROL Landkarte] | `Map` | (Nicht angegeben) | `object` |

{style="table-layout:auto"}

### MongoDB, Aerospike und Protobuf 2 {#mongo}

| XDM-Typ | MongoDB | Aerospike | Protobuf 2 |
| --- | --- | --- | --- |
| [!UICONTROL String] | `string` | `String` | `string` |
| [!UICONTROL Zahl] | `double` | `Double` | `double` |
| [!UICONTROL Lang] | `long` | `Integer` | `int64` |
| [!UICONTROL Integer] | `int` | `Integer` | `int32` |
| [!UICONTROL kurz] | `int` | `Integer` | `int32` |
| [!UICONTROL Byte] | `int` | `Integer` | `int32` |
| [!UICONTROL Datum] | `date` | `Integer`<br>(Unix Millisekunden) | `int64`<br>(Unix Millisekunden) |
| [!UICONTROL DateTime] | `timestamp` | `Integer`<br>(Unix Millisekunden) | `int64`<br>(Unix Millisekunden) |
| [!UICONTROL Boolesch] | `bool` | `Integer`<br>(0/1 binär) | `bool` |
| [!UICONTROL Landkarte] | `object` | `map` | `map<key_type, value_type>` |

{style="table-layout:auto"}

## Definieren von XDM-Feldtypen in der API {#define-fields}

Mit der Schema Registry-API können Sie benutzerdefinierte Felder mithilfe von Formaten und optionalen Einschränkungen definieren. Weitere Informationen finden Sie [ Handbuch unter „Definieren benutzerdefinierter Felder in der Schema Registry](../tutorials/custom-fields-api.md)API“.
