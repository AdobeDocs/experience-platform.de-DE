---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;Mixin;Mixin;Mixins;Mixins;Datentyp;Datentypen;Datentypen;Datentyp;Datenentwurf;Schema-Design;Datentyp;Datentyp;Datentyp;Schema;Schemas;Schema-Design;Map;Map;Map;
solution: Experience Platform
title: XDM-Feldtypeinschränkungen
topic: overview
description: Eine Referenz für XDM-Feldtypeinschränkungen, einschließlich der anderen Serialisierungsformate, denen sie zugeordnet werden können, und wie Sie Ihre eigenen Feldtypen in der API definieren.
translation-type: tm+mt
source-git-commit: e92294b9dcea37ae2a4a398c9d3397dcf5aa9b9e
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 71%

---


# XDM-Feldtypeinschränkungen

Die XDM-Feldtypen, die Sie für Ihre Schema auswählen, beschränken, welche Datentypen diese Felder enthalten können. Dieses Dokument bietet einen Überblick über die einzelnen Kernfeldtypen, einschließlich der anderen Serialisierungsformate, denen sie zugeordnet werden können, und wie Sie Ihre eigenen Feldtypen in der API definieren, um verschiedene Einschränkungen zu erzwingen.

## Erste Schritte

Bevor Sie dieses Handbuch verwenden, lesen Sie bitte die [Grundlagen der Schema-Komposition](./composition.md), um eine Einführung in XDM-Schemas, -Klassen und -Mixins zu erhalten.

Wenn Sie Ihre eigenen Feldtypen definieren möchten, sollten Sie unbedingt mit dem [Schema Registry-Entwicklerhandbuch](../api/getting-started.md) Beginn haben, um zu erfahren, wie Mixins und Datentypen erstellt werden, die Ihre benutzerdefinierten Felder einschließen.

## Zuordnen von XDM-Typen zu anderen Formaten

Die folgende Tabelle beschreibt die Zuordnung zwischen jedem XDM-Typ (`meta:xdmType`) und anderen Serialisierungsformaten.

| XDM-Typ<br>(meta:xdmType) | JSON<br>(JSON-Schema) | Parquet<br>(type/annotation) | [!DNL Spark] SQL | Java | Scala | .NET | CosmosDB | MongoDB | Aerospike | Protobuf 2 |
|---|---|---|---|---|---|---|---|---|---|---|
| string | Typ: Zeichenfolge | BYTE_ARRAY/UTF8 | StringType | java.lang.String | Zeichenfolge | System.String | Zeichenfolge | string | Zeichenfolge | string |
| number | Typ: Zahl | DOUBLE | DoubleType | java.lang.Double | Double | System.Double | Zahl | double | Dublette | dublette |
| long | Typ: Ganzzahl<br>Maximum:2^53+1<br>Minimum:-2^53+1 | INT64 | LongType | java.lang.Long | Long | System.Int64 | Nummer | long | Ganzzahl | int64 |
| int | Typ: Ganzzahl<br>Maximum:2^31<br>Minimum:-2^31 | INT32/INT_32 | IntegerType | java.lang.Integer | Int | System.Int32 | Nummer | int | Ganzzahl | int32 |
| short | Typ: Ganzzahl<br>Maximum:2^15<br>Minimum:-2^15 | INT32/INT_16 | ShortType | java.lang.Short | Short | System.Int16 | Nummer | int | Ganzzahl | int32 |
| Byte | Typ: Ganzzahl<br>Maximum:2^7<br>Minimum:-2^7 | INT32/INT_8 | ByteType | java.lang.Short | Byte | System.SByte | Zahl | int | Ganzzahl | int32 |
| boolean | Typ: Boolescher Wert | BOOLEAN | BooleanType | java.lang.Boolean | Boolesch | System.Boolean | Boolesch | bool | Ganzzahl | Ganzzahl | bool |
| date | Typ: Zeichenfolge<br>Format: Datum<br>(RFC 3339, Abschnitt 5.6) | INT32/DATE | DateType | java.util.Date | java.util.Date | System.DateTime | Zeichenfolge | date | Ganzzahl<br>(unix millis) | int64<br>(unix millis) |
| date-time | Typ: Zeichenfolge<br>Format: Datum/Uhrzeit<br>(RFC 3339, Abschnitt 5.6) | INT64/TIMESTAMP_MILLIS | TimestampType | java.util.Date | java.util.Date | System.DateTime | Zeichenfolge | timestamp | Ganzzahl<br>(unix millis) | int64<br>(unix Millis) |
| map | object | ZUORDNEN kommentierter Gruppe<br><br>&lt;<span>key_type</span>> MUSS ZEICHENFOLGE sein<br><br>&lt;<span>value_type</span>> Typ der Zuordnungwerte | MapType<br><br>&quot;keyType&quot; MUSS StringType sein<br><br>&quot;valueType&quot; ist Typ der Zuordnungwerte. | java.util.Map | Map | --- | object | object | map | map&lt;<span>key_type, value_type</span>> |

## Definieren von XDM-Feldtypen in der API {#define-fields}

XDM-Schema werden mit den Standards [JSON-Schema](https://json-schema.org/) und den grundlegenden Feldtypen definiert, mit zusätzlichen Einschränkungen für Feldnamen, die von [!DNL Experience Platform] erzwungen werden. Mit der [Schema Registry API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) können Sie zusätzliche Feldtypen mithilfe von Formaten und optionalen Einschränkungen definieren. XDM-Feldtypen werden durch das Attribut auf Feldebene, `meta:xdmType`, verfügbar gemacht.

>[!NOTE]
>
>`meta:xdmType` : Beim Meta-XDM-Typ handelt sich um einen systemgenerierten Wert. Daher müssen Sie diese Eigenschaft nicht zum JSON für Ihr Feld hinzufügen. Es empfiehlt sich, JSON-Schema-Typen (z. B. Zeichenfolge und Ganzzahl) mit den entsprechenden Min.-/Max.-Einschränkungen zu verwenden, wie in der nachstehenden Tabelle definiert.

In der folgenden Tabelle sind die entsprechenden Formatierungen zur Definition von skalaren Feldtypen und spezifischeren Feldtypen mit optionalen Eigenschaften aufgeführt. Weitere Informationen zu optionalen Eigenschaften und typspezifischen Suchbegriffen finden Sie in der Dokumentation zum [JSON-Schema](https://json-schema.org/understanding-json-schema/reference/type.html).

Suchen Sie zunächst den gewünschten Feldtyp und verwenden Sie den Beispielcode, der zum Erstellen Ihrer API-Anforderung für [Erstellen einer Mischung](../api/mixins.md#create) oder [zum Erstellen eines Datentyps](../api/data-types.md#create) bereitgestellt wird.

<table>
  <tr>
    <th>Gewünschter Typ<br/>(meta:xdmType)</th>
    <th>JSON<br/>(JSON-Schema)</th>
    <th>Code-Beispiel</th>
  </tr>
  <tr>
    <td>string</td>
    <td>Typ: Zeichenfolge<br/><br/><strong>Optionale Eigenschaften:</strong><br/>
      <ul>
        <li>pattern</li>
        <li>minLength</li>
        <li>maxLength</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
            "type": "string",
            "pattern": "^[A-Z]{2}$",
            "maxLength": 2
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>uri<br/>(xdmType:string)</td>
    <td>Typ: Zeichenfolge<br/>Format: URI</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "string",
          "format": "uri"
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>enum<br/>(xdmType: string)</td>
    <td>Typ: Zeichenfolge<br/><br/><strong>Optionale Eigenschaft:</strong><br/>
      <ul>
        <li>Standard</li>
      </ul>
    </td>
    <td>Geben Sie mit „meta:enum“ Beschriftungen für kundenorientierte Optionen an:
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
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>number</td>
    <td>Typ: Zahl<br/>Minimum: ±2,23×10^308<br/>Maximum: ±1,80×10^308</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "number"
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>long</td>
    <td>Typ: Ganzzahl<br/>Maximum:2^53+1<br>Minimum:-2^53+1</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "integer",
          "minimum": -9007199254740992,
          "maximum": 9007199254740992
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>int</td>
    <td>Typ: Ganzzahl<br/>Maximum:2^31<br>Minimum:-2^31</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "integer",
          "minimum": -2147483648,
          "maximum": 2147483648
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>short</td>
    <td>Typ: Ganzzahl<br/>Maximum:2^15<br>Minimum:-2^15</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "integer",
          "minimum": -32768,
          "maximum": 32768
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>byte</td>
    <td>Typ: Ganzzahl<br/>Maximum:2^7<br>Minimum:-2^7</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "integer",
          "minimum": -128,
          "maximum": 128
          }
      </pre>
    </td>
  </tr>
  <tr>
    <td>boolean</td>
    <td><br/>Typ: Boolescher Wert<br/>{true, false}<br/><br/><strong>Optionale Eigenschaft:</strong><br/>
      <ul>
        <li>Standard</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "boolean",
          "default": false
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>date</td>
    <td>Typ: Zeichenfolge<br/>Format: Datum</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "string",
          "format": "date",
          "examples": ["2004-10-23"]
        }
      </pre>
      date definiert durch <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 3339, Abschnitt 5.6</a>, wobei "full-date" = date-fullyear "-" date-month "-" date-mday (YYYY-MM-DD)
    </td>
  </tr>
  <tr>
    <td>date-time</td>
    <td>Typ: Zeichenfolge<br/>Format: Datum/Uhrzeit</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "string",
          "format": "date-time",
          "examples": ["2004-10-23T12:00:00-06:00"]
        }
      </pre>
      date-time definiert durch <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 3339, Abschnitt 5.6</a>, wobei "date-time" = full-date "T" full-time:<br/>(YYYY-MM-DD'T'HH:MM:SS.SSSSX)
    </td>
  </tr>
  <tr>
    <td>array</td>
    <td>Typ: Array</td>
    <td>items.type kann mit einem beliebigen Skalartyp definiert werden:
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "array",
          "items": {
            "type": "string"
          }
        }
      </pre>
      Array von Objekten, die durch ein anderes Schema definiert werden:<br/>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "array",
          "items": {
            "$ref": "id"
          }
        }
      </pre>
      Dabei ist „id“ die {id} des Referenzschemas.
    </td>
  </tr>
  <tr>
    <td>object</td>
    <td>Typ: Objekt</td>
    <td>properties.{field}.type kann mit einem beliebigen Skalartyp definiert werden:
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
        }
      </pre>
      Feld des Typs „Objekt“, das durch ein Referenz-Schema definiert wird:
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "object",
          "$ref": "id"
        }
      </pre>
      Dabei ist „id“ die {id} des Referenzschemas.
    </td>
  </tr>
  <tr>
    <td>map</td>
    <td>Typ: Objekt<br/><br/><strong>Hinweis:</strong><br/>Die Verwendung des Datentyps „map“ ist für die Verwendung durch Branchen- und Händlerschemas reserviert und steht nicht zur Verwendung in Mandantenfeldern zur Verfügung. Sie wird in Standardschemas verwendet, wenn Daten als Schlüssel dargestellt werden, die einem bestimmten Wert zugeordnet sind oder bei denen Schlüssel vernünftigerweise nicht in ein statisches Schema einbezogen werden können und als Datenwerte behandelt werden müssen.</td>
    <td>Eine „map“ DARF KEINE Eigenschaften definieren. Es MUSS ein einzelnes "[!UICONTROL additionalProperties]"-Schema definieren, um die in der 'map' enthaltenen Werte zu beschreiben. Eine „map“ in XDM kann nur einen einzigen Datentyp enthalten. Werte können eine beliebige gültige XDM-Schema-Definition sein, einschließlich eines Arrays oder eines Objekts, oder als Verweis auf ein anderes Schema (über $ref).<br/><br/>Zuordnungsfeld mit Werten vom Typ „Zeichenfolge“:
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "object",
          "additionalProperties":{
            "type": "string"
          }
        }
      </pre>
    Zuordnungsfeld mit Werten als Array von Zeichenfolgen:
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "object",
          "additionalProperties":{
            "type": "array",
            "items": {
              "type": "string"
            }
          }
        }
      </pre>
    Zuordnungsfeld, das auf ein anderes Schema verweist:
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "object",
          "additionalProperties":{
            "$ref": "id"
          }
        }
      </pre>
      Dabei ist „id“ die {id} des Referenzschemas.
    </td>
  </tr>
</table>
