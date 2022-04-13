---
title: Definieren von XDM-Feldern in der Schema Registry-API
description: Erfahren Sie, wie Sie beim Erstellen benutzerdefinierter Experience-Datenmodell (XDM)-Ressourcen in der Schema Registry-API verschiedene Felder definieren.
exl-id: d79332e3-8448-42af-b250-882bcb0f1e7d
source-git-commit: 4ce9e53ec420a8c9ba07cdfd75e66d854989f8d2
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 13%

---

# Definieren von XDM-Feldern in der Schema Registry-API

Alle Felder des Experience-Datenmodells (XDM) werden mit dem Standard [JSON-Schema](https://json-schema.org/) Einschränkungen, die für ihren Feldtyp gelten, mit zusätzlichen Einschränkungen für Feldnamen, die von Adobe Experience Platform erzwungen werden. Mit der Schema Registry-API können Sie benutzerdefinierte Felder in Ihren Schemas definieren, indem Sie Formate und optionale Einschränkungen verwenden. XDM-Feldtypen werden durch das Attribut auf Feldebene verfügbar gemacht, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` ist ein vom System generierter Wert. Daher müssen Sie diese Eigenschaft nicht zum JSON für Ihr Feld hinzufügen, wenn Sie die API verwenden (es sei denn, [Erstellen benutzerdefinierter Zuordnungstypen](#maps)). Es empfiehlt sich, JSON-Schematypen zu verwenden (z. B. `string` und `integer`) mit den entsprechenden Mindest-/Höchstbeschränkungen, wie in der folgenden Tabelle definiert.

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
    <br>Beachten Sie Folgendes: <code>meta:enum</code> Wert: <strong>not</strong> Deklarieren Sie eine Auflistung oder führen Sie eine Datenvalidierung allein durch. In den meisten Fällen werden unter <code>meta:enum</code> werden auch <code>enum</code> , um sicherzustellen, dass die Daten begrenzt sind. Es gibt jedoch einige Anwendungsfälle, in denen <code>meta:enum</code> ohne entsprechende <code>enum</code> Array. Siehe Tutorial zu <a href="../tutorials/suggested-values.md">Definieren empfohlener Werte</a> für weitere Informationen.
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
    <td>Bei einem Feld vom Typ Zuordnung handelt es sich im Wesentlichen um ein Feld vom Typ Objekt mit einem nicht beschränkten Satz von Schlüsseln. Wie Objekte haben Karten eine <code>type</code> Wert von <code>object</code>, aber ihre <code>meta:xdmType</code> explizit auf <code>map</code>.<br><br>Karte <strong>darf nicht</strong> definieren beliebige Eigenschaften. Es <strong>must</strong> eine einzelne <code>additionalProperties</code> schema zur Beschreibung des Werttyps, der in der Zuordnung enthalten ist (jede Zuordnung kann nur einen einzigen Datentyp enthalten). Die <code>type</code> Wert muss entweder <code>string</code> oder <code>integer</code>.<br/><br/>Ein Zuordnungsfeld mit Werten vom Typ Zeichenfolge:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "meta:xdmType": "map", "additionalProperties":{ "type": "string" } }</pre>
    Weitere Informationen zum Erstellen benutzerdefinierter Zuordnungstypen in XDM finden Sie im folgenden Abschnitt .
    </td>
  </tr>
</table>

## Erstellen benutzerdefinierter Zuordnungstypen {#maps}

Um &quot;map-ähnliche&quot;Daten in XDM effizient zu unterstützen, können Objekte mit einer `meta:xdmType` auf `map` , um deutlich zu machen, dass ein Objekt so verwaltet werden sollte, als wäre der Schlüsselsatz nicht eingeschränkt. Daten, die in Zuordnungsfelder aufgenommen werden, müssen Zeichenfolgenschlüssel und nur Zeichenfolgen- oder Ganzzahlwerte verwenden (wie durch `additionalProperties.type`).

XDM legt die folgenden Einschränkungen für die Verwendung dieses Speicherhinweises fest:

* Zuordnungstypen MÜSSEN vom Typ sein `object`.
* Für Zuordnungstypen dürfen KEINE Eigenschaften definiert sein (d. h. sie definieren &quot;leere&quot;Objekte).
* Zuordnungstypen MÜSSEN Folgendes enthalten: `additionalProperties.type` -Feld, das die Werte beschreibt, die in der Zuordnung platziert werden können, entweder `string` oder `integer`.

Stellen Sie sicher, dass Sie nur Felder vom Typ Zuordnung verwenden, wenn dies unbedingt erforderlich ist, da sie die folgenden Leistungsbeeinträchtigungen aufweisen:

* Die Antwortzeit von Adobe Experience Platform Query Service wird für 100 Millionen Datensätze von drei Sekunden auf zehn Sekunden reduziert.
* Karten mit weniger als 16 Schlüsseln müssen vorhanden sein. Andernfalls besteht die Gefahr einer weiteren Verschlechterung.

Die Benutzeroberfläche von Platform weist außerdem Einschränkungen hinsichtlich der Art und Weise auf, wie die Schlüssel von Feldern vom Typ Zuordnung extrahiert werden können. Während Objekttypen erweitert werden können, werden Zuordnungen stattdessen als ein einzelnes Feld angezeigt.

## Nächste Schritte

In diesem Handbuch wurde die Definition verschiedener Feldtypen in der API beschrieben. Weitere Informationen zur Formatierung von XDM-Feldtypen finden Sie im Handbuch unter [XDM-Feldtypbegrenzungen](../schema/field-constraints.md).
