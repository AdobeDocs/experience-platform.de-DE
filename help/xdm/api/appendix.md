---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Entwickleranhang für Schema Registry
topic: developer guide
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 87%

---


# Anhang

This document provides supplemental information related to working with the [!DNL Schema Registry] API.

## Kompatibilitätsmodus

[!DNL Experience Data Model]Das  (XDM) ist eine öffentlich dokumentierte Spezifikation, die von Adobe zur Verbesserung der Interoperabilität, Ausdrucksfähigkeit und Leistungsfähigkeit digitaler Erlebnisse unterstützt wird. Adobe verwaltet den Quell-Code und formale XDM-Definitionen in einem [Open-Source-Projekt auf GitHub](https://github.com/adobe/xdm/). Diese Definitionen werden in XDM Standard Notation geschrieben, wobei JSON-LD (JavaScript Object Notation for Linked Data) und JSON-Schema als Grammatik zur Definition von XDM-Schemas verwendet werden.

Wenn Sie sich die formalen XDM-Definitionen im öffentlichen Repository ansehen, können Sie erkennen, dass sich das Standard-XDM von dem unterscheidet, das Sie in Adobe Experience Platform sehen. What you are seeing in [!DNL Experience Platform] is called Compatibility Mode, and it provides a simple mapping between standard XDM and the way it is used within [!DNL Platform].

### Funktionsweise des Kompatibilitätsmodus

Der Kompatibilitätsmodus ermöglicht es dem XDM JSON-LD-Modell, mit der vorhandenen Dateninfrastruktur zu arbeiten, indem Werte innerhalb des XDM-Standards verändert werden, während die Semantik gleich bleibt. Es verwendet eine verschachtelte JSON-Struktur, die Schemas in einem baumähnlichen Format anzeigt.

Der Hauptunterschied, den Sie zwischen Standard-XDM und Kompatibilitätsmodus bemerken, ist die Entfernung des Präfix „xdm:“ für Feldnamen.

Im Folgenden finden Sie einen Vergleich, der sowohl im Standard-XDM als auch im Kompatibilitätsmodus geburtstagsbezogene Felder (mit entfernten „Beschreibungsattributen“) nebeneinander anzeigt. Beachten Sie, dass die Felder für den Kompatibilitätsmodus einen Verweis auf das XDM-Feld und seinen Datentyp in den Attributen „meta:xdmField“ und „meta:xdmType“ enthalten.

<table>
  <th>Standard-XDM</th>
  <th>Kompatibilitätsmodus</th>
  <tr>
  <td>
  <pre class="JSON language-JSON hljs">
        {
          "xdm:birthDate": {
              "title": "Birth Date",
              "type": "string",
              "format": "date",
          },
          "xdm:birthDayAndMonth": {
              "title": "Birth Date",
              "type": "string",
              "pattern": "[0-1][0-9]-[0-9][0-9]",
          },
          "xdm:birthYear": {
              "title": "Birth year",
              "type": "integer",
              "minimum": 1,
              "maximum": 32767
        }
      </pre>
  </td>
  <td>
  <pre class="JSON language-JSON hljs">
        {
          "birthDate": {
              "title": "Birth Date",
              "type": "string",
              "format": "date",
              "meta:xdmField": "xdm:birthDate",
              "meta:xdmType": "date"
          },
          "birthDayAndMonth": {
              "title": "Birth Date",
              "type": "string",
              "pattern": "[0-1][0-9]-[0-9][0-9]",
              "meta:xdmField": "xdm:birthDayAndMonth",
              "meta:xdmType": "string"
          },
          "birthYear": {
              "title": "Birth year",
              "type": "integer",
              "minimum": 1,
              "maximum": 32767,
              "meta:xdmField": "xdm:birthYear",
              "meta:xdmType": "short"
        }
      </pre>
  </td>
  </tr>
</table>

### Warum ist der Kompatibilitätsmodus erforderlich?

Adobe Experience Platform ist für die Verwendung mit mehreren Lösungen und Diensten konzipiert, die jeweils eigene technische Herausforderungen und Einschränkungen aufweisen (z. B. wie bestimmte Technologien Sonderzeichen handhaben). Um diese Einschränkungen zu überwinden, wurde der Kompatibilitätsmodus entwickelt.

Die meisten [!DNL Experience Platform] Dienste einschließlich [!DNL Catalog], [!DNL Data Lake]und [!DNL Real-time Customer Profile] Verwendung als Standard-XDM [!DNL Compatibility Mode] . Die [!DNL Schema Registry] API verwendet auch [!DNL Compatibility Mode]und die Beispiele in diesem Dokument werden alle mit verwendet [!DNL Compatibility Mode].

It is worthwhile to know that a mapping takes place between standard XDM and the way it is operationalized in [!DNL Experience Platform], but it should not affect your use of [!DNL Platform] services.

The open source project is available to you, but when it comes to interacting with resources through the [!DNL Schema Registry], the API examples in this document provide the best practices you should know and follow.

## Definieren von XDM-Feldtypen in der API {#field-types}

XDM schemas are defined using JSON Schema standards and basic field types, with additional constraints for field names which are enforced by [!DNL Experience Platform]. Mit XDM können Sie zusätzliche Feldtypen mithilfe von Formaten und optionalen Begrenzungen definieren. Die XDM-Feldtypen werden durch das Attribut auf Feldebene verfügbar gemacht, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` : Beim Meta-XDM-Typ handelt sich um einen systemgenerierten Wert. Daher müssen Sie diese Eigenschaft nicht zum JSON für Ihr Feld hinzufügen. Es empfiehlt sich, JSON-Schema-Typen (z. B. Zeichenfolge und Ganzzahl) mit den entsprechenden Min.-/Max.-Einschränkungen zu verwenden, wie in der nachstehenden Tabelle definiert.

In der folgenden Tabelle sind die entsprechenden Formatierungen zur Definition von skalaren Feldtypen und spezifischeren Feldtypen mit optionalen Eigenschaften aufgeführt. Weitere Informationen zu optionalen Eigenschaften und typspezifischen Suchbegriffen finden Sie in der Dokumentation zum [JSON-Schema](https://json-schema.org/understanding-json-schema/reference/type.html).

Suchen Sie zunächst den gewünschten Feldtyp und verwenden Sie den Beispiel-Code, der zum Erstellen Ihrer API-Anfrage bereitgestellt wird.

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


## Zuordnen von XDM-Typen zu anderen Formaten

Die folgende Tabelle beschreibt die Zuordnung zwischen „meta:xdmType“ und anderen Serialisierungsformaten.

| XDM-Typ<br>(meta:xdmType) | JSON<br>(JSON-Schema) | Parquet<br>(type/annotation) | [!DNL Spark] SQL | Java | Scala | .NET | CosmosDB | MongoDB | Aerospike | Protobuf 2 |
|---|---|---|---|---|---|---|---|---|---|---|
| string | Typ: Zeichenfolge | BYTE_ARRAY/UTF8 | StringType | java.lang.String | Zeichenfolge | System.String | Zeichenfolge | string | Zeichenfolge | string |
| number | Typ: Zahl | DOUBLE | DoubleType | java.lang.Double | Double | System.Double | Zahl | double | Double | double |
| long | Typ: Ganzzahl<br>Maximum:2^53+1<br>Minimum:-2^53+1 | INT64 | LongType | java.lang.Long | Long | System.Int64 | Zahl | long | Ganzzahl | int64 |
| int | Typ: Ganzzahl<br>Maximum:2^31<br>Minimum:-2^31 | INT32/INT_32 | IntegerType | java.lang.Integer | Int | System.Int32 | Zahl | int | Ganzzahl | int32 |
| short | Typ: Ganzzahl<br>Maximum:2^15<br>Minimum:-2^15 | INT32/INT_16 | ShortType | java.lang.Short | Short | System.Int16 | Zahl | int | Ganzzahl | int32 |
| byte | Typ: Ganzzahl<br>Maximum:2^7<br>Minimum:-2^7 | INT32/INT_8 | ByteType | java.lang.Short | Byte | System.SByte | Zahl | int | Ganzzahl | int32 |
| boolean | Typ: Boolescher Wert | BOOLEAN | BooleanType | java.lang.Boolean | Boolesch | System.Boolean | Boolesch | bool | Ganzzahl | Ganzzahl | bool |
| date | Typ: Zeichenfolge<br>Format: Datum<br>(RFC 3339, Abschnitt 5.6) | INT32/DATE | DateType | java.util.Date | java.util.Date | System.DateTime | Zeichenfolge | date | Ganzzahl<br>(unix millis) | int64<br>(unix millis) |
| date-time | Typ: Zeichenfolge<br>Format: Datum/Uhrzeit<br>(RFC 3339, Abschnitt 5.6) | INT64/TIMESTAMP_MILLIS | TimestampType | java.util.Date | java.util.Date | System.DateTime | Zeichenfolge | timestamp | Ganzzahl<br>(unix millis) | int64<br>(unix millis) |
| map | object | ZUORDNEN kommentierter Gruppe<br><br>&lt;<span>key_type</span>> MUSS ZEICHENFOLGE sein<br><br>&lt;<span>value_type</span>> Typ der Zuordnungwerte | MapType<br><br>&quot;keyType&quot; MUSS StringType sein<br><br>&quot;valueType&quot; ist Typ der Zuordnungwerte. | java.util.Map | Map | --- | object | object | map | map&lt;<span>key_type, value_type</span>> |
