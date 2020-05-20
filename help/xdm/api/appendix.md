---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Schema Registry Developer-Anhang
topic: developer guide
translation-type: tm+mt
source-git-commit: f7c87cc86bfc5017ec5c712d05e39be5c14a7147
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 4%

---


# Anhang

Dieses Dokument enthält zusätzliche Informationen zum Arbeiten mit der Schema Registry API.

## Kompatibilitätsmodus

Das Experience Data Model (XDM) ist eine öffentlich dokumentierte Spezifikation, die von Adobe zur Verbesserung der Interoperabilität, Ausdrucksfähigkeit und Leistungsfähigkeit digitaler Erlebnisse unterstützt wird. Adobe verwaltet den Quellcode und formale XDM-Definitionen in einem [Open-Source-Projekt auf GitHub](https://github.com/adobe/xdm/). Diese Definitionen werden in XDM Standard Notation geschrieben, wobei JSON-LD (JavaScript Object Notation for Linked Data) und JSON-Schema als Grammatik zur Definition von XDM-Schemas verwendet werden.

Wenn Sie sich die formalen XDM-Definitionen im öffentlichen Repository ansehen, können Sie erkennen, dass sich der Standard-XDM von dem unterscheidet, was Sie in Adobe Experience Platform sehen. Was Sie in Experience Platform sehen, wird als &quot;Kompatibilitätsmodus&quot;bezeichnet und bietet eine einfache Zuordnung zwischen Standard-XDM und der Art und Weise, wie es in der Plattform verwendet wird.

### Funktionsweise des Kompatibilitätsmodus

Der Kompatibilitätsmodus ermöglicht es dem XDM JSON-LD-Modell, mit der vorhandenen Dateninfrastruktur zu arbeiten, indem Werte innerhalb des XDM-Standards verändert werden, während die Semantik gleich bleibt. Es verwendet eine verschachtelte JSON-Struktur, die Schemas in einem baumähnlichen Format anzeigt.

Der Hauptunterschied, den Sie zwischen Standard-XDM und Kompatibilitätsmodus bemerken werden, ist die Entfernung des Präfix &quot;xdm:&quot;für Feldnamen.

Im Folgenden finden Sie einen Vergleich, der sowohl im Standard-XDM- als auch im Kompatibilitätsmodus Geburtstagsbezogene Felder (mit entfernten &quot;Beschreibungsattributen&quot;) nebeneinander anzeigt. Beachten Sie, dass die Felder für den Kompatibilitätsmodus einen Verweis auf das XDM-Feld und seinen Datentyp in den Attributen &quot;meta:xdmField&quot;und &quot;meta:xdmType&quot;enthalten.

<table>
  <th>Standard-XDM</th>
  <th>Kompatibilitätsmodus</th>
  <tr>
  <td>
  <pre class="JSON language-JSON hljs">
        { "xdm:bornDate": { "title": "Geburtsdatum", "Typ": "string", "format": "date", }, "xdm:bornDayAndMonth": { "title": "Geburtsdatum", "Typ": "string", "pattern": "[0-1][0-9]-[0-9][0-9]", }, "xdm:bornYear": { "title": "Geburtsjahr", "Typ": "integer", "minimum": 1, "Maximum": 32767 }
      </pre>
  </td>
  <td>
  <pre class="JSON language-JSON hljs">
        { "bornDate": { "title": "Geburtsdatum", "Typ": "string", "format": "date", "meta:xdmField": "xdm:bornDate", "meta:xdmType": "date" }, "bornDayAndMonth": { "title": "Geburtsdatum", "Typ": "string", "pattern": "[0-1][0-9]-[0-9][0-9]", "meta:xdmField": "xdm:bornDayAndMonth", "meta:xdmType": "string" }, "bornYear": { "title": "Geburtsjahr", "Typ": "integer", "minimum": 1, "Maximum": 32767, "meta:xdmField": "xdm:bornYear", "meta:xdmType": "short" }
      </pre>
  </td>
  </tr>
</table>

### Warum ist der Kompatibilitätsmodus erforderlich?

Adobe Experience Platform ist für die Verwendung mit mehreren Lösungen und Diensten konzipiert, die jeweils eigene technische Herausforderungen und Einschränkungen aufweisen (z. B. wie bestimmte Technologien Sonderzeichen handhaben). Um diese Einschränkungen zu überwinden, wurde der Kompatibilitätsmodus entwickelt.

Die meisten Experience Platform-Dienste, einschließlich Catalog, Data Lake und Echtzeit-Kundendaten, verwenden den Kompatibilitätsmodus anstelle des Standard-XDM. Die Schema Registry API verwendet auch den Kompatibilitätsmodus. Die Beispiele in diesem Dokument werden alle mithilfe des Kompatibilitätsmodus angezeigt.

Es lohnt sich zu wissen, dass eine Zuordnung zwischen Standard-XDM und der Art und Weise erfolgt, wie sie in Experience Platform operalisiert wird, sollte jedoch nicht Ihre Verwendung von Platform-Diensten beeinträchtigen.

Das Open-Source-Projekt steht Ihnen zur Verfügung, aber wenn es darum geht, mit Ressourcen über die Schema-Registrierung zu interagieren, bieten die API-Beispiele in diesem Dokument die Best Practices, die Sie kennen und befolgen sollten.

## Definieren von XDM-Feldtypen in der API {#field-types}

XDM-Schema werden mithilfe von JSON-Schema-Standards und einfachen Feldtypen definiert, mit zusätzlichen Einschränkungen für Feldnamen, die von Experience Platform erzwungen werden. Mit XDM können Sie zusätzliche Feldtypen mithilfe von Formaten und optionalen Einschränkungen definieren. Die XDM-Feldtypen werden durch das Attribut auf Feldebene offen gelegt, `meta:xdmType`.

>[!NOTE] `meta:xdmType` ist ein systemgenerierter Wert. Daher müssen Sie diese Eigenschaft nicht zum JSON für Ihr Feld hinzufügen. Es empfiehlt sich, JSON-Schema-Typen (z. B. String und Ganzzahl) mit den entsprechenden Min/Max-Einschränkungen zu verwenden, wie in der folgenden Tabelle definiert.

In der folgenden Tabelle sind die entsprechenden Formatierungen zur Definition von skalaren Feldtypen und spezifischeren Feldtypen mit optionalen Eigenschaften aufgeführt. Weitere Informationen zu optionalen Eigenschaften und typspezifischen Suchbegriffen finden Sie in der Dokumentation zum [JSON-Schema](https://json-schema.org/understanding-json-schema/reference/type.html).

Suchen Sie zunächst den gewünschten Feldtyp und verwenden Sie den Beispielcode, der zum Erstellen Ihrer API-Anforderung bereitgestellt wird.

<table>
  <tr>
    <th>Gewünschter Typ<br/>(meta:xdmType)</th>
    <th>JSON<br/>(JSON-Schema)</th>
    <th>Codebeispiel</th>
  </tr>
  <tr>
    <td>Zeichenfolge</td>
    <td>type:<br/><br/><strong>stringOptional-Eigenschaften:</strong><br/>
      <ul>
        <li>pattern</li>
        <li>minLength</li>
        <li>maxLength</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "string", "pattern": "^[A-Z]{2}$", "maxLength": 2 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>uri<br/>(xdmType:string)</td>
    <td>type:<br/>Zeichenformat: uri</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "string", "format": "uri" }
      </pre>
    </td>
  </tr>
  <tr>
    <td>enum<br/>(xdmType: string)</td>
    <td>type:<br/><br/><strong>stringOptional-Eigenschaft:</strong><br/>
      <ul>
        <li>Standard</li>
      </ul>
    </td>
    <td>Geben Sie mit "meta:enum"Beschriftungen für kundenorientierte Optionen an:
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "string", "enum": [ "value1", "value2", "value3" ], "meta:enum": { "value1": "Value 1", "value2": "Value 2", "value3": "Value 3" }, "default": "value1" }
      </pre>
    </td>
  </tr>
  <tr>
    <td>number</td>
    <td>type:<br/>numerminimum: ±2,23×10^308<br/>Maximal: ±1,80×10^308</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "number" }
      </pre>
    </td>
  </tr>
  <tr>
    <td>long</td>
    <td>type:<br/>integerMaximum:2^53+1<br>minimum:-2^53+1</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "integer", "minimum": -9007199254740992, "Maximal": 9007199254740992 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>int</td>
    <td>type:<br/>integerMaximum:2^31<br>minimum:-2^31</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "integer", "minimum": -2147483648, "Maximal": 2147483648 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>short</td>
    <td>type:<br/>integerMaximum:2^15<br>minimum:-2^15</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "integer", "minimum": -32768, "Maximum": 32768 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>byte</td>
    <td>type:<br/>integerMaximum:2^7<br>minimum:-2^7</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "integer", "minimum": -128, "Maximum": 128 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>Boolescher Wert</td>
    <td><br/>type: boolean<br/>{true, false}<br/><br/><strong>Optional, Eigenschaft:</strong><br/>
      <ul>
        <li>Standard</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "boolean", "default": false }
      </pre>
    </td>
  </tr>
  <tr>
    <td>date</td>
    <td>type:<br/>Zeichenformat: date</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "string", "format": "date", "example": ["2004-10-23"] }
      </pre>
      Datum gemäß <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 3339, Abschnitt 5.6</a>, wobei "Volldatum" = Datum-Volljahr "-" Datum-Monat "-" Datum-Tag-Tag (JJJJ-MM-TT)
    </td>
  </tr>
  <tr>
    <td>date-time</td>
    <td>type:<br/>Zeichenformat: date-time</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "string", "format": "date-time", "example": ["2004-10-23T12:00:00-06:00"] }
      </pre>
      Date-Time gemäß <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 3339, Abschnitt 5.6</a>, wobei "date-time" = full-date "T" full-time:<br/>(YYYY-MM-DD'T'HH:MM:SS.SSSSX)
    </td>
  </tr>
  <tr>
    <td>array</td>
    <td>type: array</td>
    <td>items.type kann mit einem beliebigen Skalartyp definiert werden:
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "array", "items": { "type": "string" } }
      </pre>
      Array von Objekten, die durch ein anderes Schema definiert werden:<br/>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "array", "items": { "$ref": "id" } }
      </pre>
      Dabei ist "id"die {id} des Referenz-Schemas.
    </td>
  </tr>
  <tr>
    <td>object</td>
    <td>type: object</td>
    <td>zu erhalten.{field}.type kann mit einem beliebigen Skalartyp definiert werden:
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "object", "properties": { "field1": { "type": "string" }, "field2": { "type": "number" } } }
      </pre>
      Feld des Typs "Objekt", das durch ein Referenz-Schema definiert wird:
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "object", "$ref": "id" }
      </pre>
      Dabei ist "id"die {id} des Referenz-Schemas.
    </td>
  </tr>
  <tr>
    <td>map</td>
    <td>type:<br/><br/><strong>objectHinweis:Die</strong><br/>Verwendung des Datentyps "map"ist für die Verwendung durch Branchen- und Händlerfelder reserviert und steht nicht zur Verwendung in Mietfeldern zur Verfügung. Sie wird in Standard-Schemas verwendet, wenn Daten als Schlüssel dargestellt werden, die einem bestimmten Wert zugeordnet sind, oder bei denen Schlüssel vernünftigerweise nicht in ein statisches Schema einbezogen werden können und als Datenwerte behandelt werden müssen.</td>
    <td>Eine 'Map' DARF KEINE Eigenschaften definieren. Es MUSS ein einzelnes "additionalProperties"-Schema definieren, um die in der "map" enthaltenen Werte zu beschreiben. Eine "Map" in XDM kann nur einen einzigen Datentyp enthalten. Werte können eine beliebige gültige XDM-Schema-Definition sein, einschließlich eines Arrays oder eines Objekts, oder als Verweis auf ein anderes Schema (über $ref).<br/><br/>Feld mit Werten vom Typ "String"zuordnen:
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "object", "additionalProperties":{ "type": "string" } }
      </pre>
    Zuordnungsfeld mit Werten als Array von Zeichenfolgen:
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "object", "additionalProperties":{ "type": "array", "items": { "type": "string" } } }
      </pre>
    Zuordnungsfeld, das auf ein anderes Schema verweist:
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "object", "additionalProperties":{ "$ref": "id" } }
      </pre>
      Dabei ist "id"die {id} des Referenz-Schemas.
    </td>
  </tr>
</table>


## Zuordnen von XDM-Typen zu anderen Formaten

Die folgende Tabelle beschreibt die Zuordnung zwischen &quot;meta:xdmType&quot;und anderen Serialisierungsformaten.

| XDM-Typ<br>(meta:xdmType) | JSON<br>(JSON-Schema) | Parquet<br>(type/annotation) | Spark SQL | Java | Scala | .NET | CosmosDB | MongoDB | Aerospike | Protokoll 2 |
|---|---|---|---|---|---|---|---|---|---|---|
| Zeichenfolge | type:string | BYTE_ARRAY/UTF8 | StringType | java.lang.String | Zeichenfolge | System.String | Zeichenfolge | Zeichenfolge | Zeichenfolge | Zeichenfolge |
| number | type:number | DUBLETTE | DoubleType | java.lang.Double | Doppelt | System.Double | Zahl | Dublette | Doppelt | Dublette |
| long | type:<br>integerMaximum:2^53+1<br>minimum:-2^53+1 | INT64 | LongType | java.lang.Long | lang | System.Int64 | Zahl | long | Ganzzahl | int64 |
| int | type:<br>integerMaximum:2^31<br>minimum:-2^31 | INT32/INT_32 | IntegerType | java.lang.Integer | Int | System.Int32 | Zahl | int | Ganzzahl | int32 |
| short | type:<br>integerMaximum:2^15<br>minimum:-2^15 | INT32/INT_16 | ShortType | java.lang.Short | Short | System.Int16 | Zahl | int | Ganzzahl | int32 |
| byte | type:<br>integerMaximum:2^7<br>minimum:-2^7 | INT32/INT_8 | ByteType | java.lang.Short | Byte | System.SByte | Zahl | int | Ganzzahl | int32 |
| Boolescher Wert | Typ:boolean | BOOLEAN | BooleanType | java.lang.Boolean | Boolesch | System.Boolean | Boolesch | bool | Ganzzahl | Ganzzahl | bool |
| date | Typ:<br>stringformat:date<br>(RFC 3339, Abschnitt 5.6) | INT32/DATE | DateType | java.util.Date | java.util.Date | System.DateTime | Zeichenfolge | date | Integer<br>(Unix-Millis) | int64<br>(Unix-Millis) |
| date-time | type:<br>stringformat:date-time<br>(RFC 3339, Abschnitt 5.6) | INT64/TIMESTAMP_MILLIS | TimestampType | java.util.Date | java.util.Date | System.DateTime | Zeichenfolge | timestamp | Integer<br>(Unix-Millis) | int64<br>(Unix-Millis) |
| map | object | MAP-kommentierte Gruppe<br><br>&lt;<span>Schlüssel_Typ</span>> MUSS STRING<br><br>&lt;<span>Wert_Typ</span>> Typ der Map-Wertesein | MapType<br><br>&quot;keyType&quot;MUSS StringType<br><br>&quot;valueType&quot;der Typ der Map-Werte sein. | java.util.Map | Landkarte | --- | object | object | map | map&lt;<span>key_type, value_type</span>> |
