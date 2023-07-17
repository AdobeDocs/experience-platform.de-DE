---
description: Erfahren Sie, wie Sie über den Endpunkt „/destination-servers“ Dateiformatierungsoptionen für dateibasierte Ziele konfigurieren, die mit Adobe Experience Platform Destination SDK erstellt wurden.
title: Konfiguration der Dateiformatierung
source-git-commit: 5a6359e5731b36763e86eba8c79e60d74fb3b4c8
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 98%

---


# Konfiguration der Dateiformatierung

Destination SDK unterstützt einen flexiblen Funktionssatz, den Sie entsprechend Ihren Integrationsanforderungen konfigurieren können. Zu diesen Funktionen gehört die Unterstützung für [!DNL CSV]-Dateiformatierung.

Wenn Sie dateibasierte Ziele durch Destination SDK erstellen, können Sie definieren, wie die exportierten CSV-Dateien formatiert werden sollen. Sie können viele Formatierungsoptionen anpassen, u. a.:

* Ob die CSV-Datei einen Header enthalten soll;
* Welches Zeichen für Anführungszeichen von Werten verwendet werden soll;
* Wie leere Werte aussehen sollten.

Je nach Zielkonfiguration sehen Benutzerinnen und Benutzer bestimmte Optionen in der Benutzeroberfläche, wenn sie eine Verbindung zu einem dateibasierten Ziel herstellen. Wie diese Optionen aussehen, können Sie in der Dokumentation zu den [Dateiformatierungsoptionen für dateibasierte Ziele](../../../ui/batch-destinations-file-formatting-options.md) nachlesen.


Dateiformatierungseinstellungen sind Teil der Ziel-Server-Konfiguration für dateibasierte Ziele.

Informationen dazu, wo diese Komponente in eine mit Destination SDK erstellte Integration passt, finden Sie im Diagramm in der Dokumentation zu [Konfigurationsoptionen](../configuration-options.md) oder im Handbuch zur [Verwendung von Destination SDK zum Konfigurieren eines dateibasierten Ziels](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Die Dateiformatierungsoptionen können über den Endpunkt `/authoring/destination-servers` konfiguriert werden. Detaillierte Beispiele für API-Aufrufe, in denen Sie die auf dieser Seite angezeigten Komponenten konfigurieren können, finden Sie auf den folgenden API-Referenzseiten.

* [Erstellen einer Ziel-Server-Konfiguration](../../authoring-api/destination-server/create-destination-server.md)
* [Aktualisieren einer Ziel-Server-Konfiguration](../../authoring-api/destination-server/update-destination-server.md)

Auf dieser Seite werden alle unterstützten Dateiformatierungseinstellungen für exportierte `CSV`-Dateien beschrieben.

>[!IMPORTANT]
>
>Bei allen von Destination SDK unterstützten Parameternamen und Werten wird **nach Groß-/Kleinschreibung unterschieden**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Unterstützte Integrationstypen {#supported-integration-types}

Die nachstehende Tabelle beschreibt ausführlich, welche Integrationstypen die auf dieser Seite beschriebenen Funktionen unterstützen.

| Integrationstyp | Unterstützt Funktionen |
|---|---|
| Echtzeit-Integrationen (Streaming) | Nein |
| Dateibasierte (Batch-)Integrationen | Ja |

## Unterstützte Parameter {#supported-parameters}

Sie können verschiedene Eigenschaften der exportierten Dateien ändern, um sie an die Anforderungen des Dateiempfangssystems Ihres Ziels anzupassen, damit die von Experience Platform empfangenen Dateien optimal gelesen und interpretiert werden können.

>[!NOTE]
>
>CSV-Optionen werden nur beim Exportieren von CSV-Dateien unterstützt. Der `fileConfigurations`-Abschnitt ist bei der Einrichtung eines neuen Ziel-Servers nicht erforderlich. Wenn Sie im API-Aufruf keine Werte für die CSV-Optionen übergeben, werden die Standardwerte aus der [folgenden Tabelle](#file-formatting-reference-and-example) verwendet.


## CSV-Optionen, bei denen Benutzerinnen und Benutzer keine Konfigurationsoptionen auswählen können {#file-configuration-templating-none}

Im folgenden Konfigurationsbeispiel sind alle CSV-Optionen vordefiniert. Die in den einzelnen Parametern der `csvOptions` definierten Exporteinstellungen sind endgültig und können von den Benutzerinnen und Benutzern nicht geändert werden.

```json
"fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        },
        "maxFileRowCount":5000000
    }
```

## CSV-Optionen, in denen Benutzerinnen und Benutzer Konfigurationsoptionen auswählen können {#file-configuration-templating-pebble}

Im folgenden Konfigurationsbeispiel ist keine der CSV-Optionen vordefiniert. Der `value` in jedem `csvOptions`-Parameter wird im entsprechenden Kundendatenfeld über den Endpunkt `/destinations` konfiguriert (z. B. [`customerData.quote`](../../functionality/destination-configuration/customer-data-fields.md#conditional-options) für die `quote`-Dateiformatierung), und Benutzerinnen und Benutzer können in der Experience Platform-Benutzeroberfläche zwischen den verschiedenen Optionen wählen, die Sie im entsprechenden Kundendatenfeld konfigurieren. Wie diese Optionen aussehen, können Sie in der Dokumentation zu den [Dateiformatierungsoptionen für dateibasierte Ziele](../../../ui/batch-destinations-file-formatting-options.md) nachlesen.

```json
{
   "fileConfigurations":{
      "compression":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{% if customerData contains 'compression' and customerData.compression is not empty %}{{customerData.compression}}{% else %}NONE{% endif %}"
      },
      "fileType":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.fileType}}"
      },
      "csvOptions":{
         "sep":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'delimiter' %}{{customerData.csvOptions.delimiter}}{% else %},{% endif %}"
         },
         "quote":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'quote' %}{{customerData.csvOptions.quote}}{% else %}\"{% endif %}"
         },
         "escape":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'escape' %}{{customerData.csvOptions.escape}}{% else %}\\{% endif %}"
         },
         "nullValue":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'nullValue' %}{{customerData.csvOptions.nullValue}}{% else %}null{% endif %}"
         },
         "emptyValue":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'emptyValue' %}{{customerData.csvOptions.emptyValue}}{% else %}{% endif %}"
         }
      },
      "maxFileRowCount":5000000
   }
}
```

## Vollständige Referenz und Beispiele für unterstützte Dateiformatierungsoptionen {#file-formatting-reference-and-example}

>[!TIP]
>
>Die im Folgenden beschriebenen CSV-Dateiformatierungsoptionen werden ebenfalls im Abschnitt [Apache Spark-Anleitung für CSV-Dateien](https://spark.apache.org/docs/latest/sql-data-sources-csv.html) dokumentiert. Die unten verwendeten Beschreibungen stammen aus dem Apache Spark-Handbuch.

Nachstehend finden Sie eine vollständige Referenz aller verfügbaren Dateiformatierungsoptionen in Destination SDK zusammen mit Ausgabebeispielen für jede Option.

| Feld | Erforderlich/Optional | Beschreibung | Standardwert | Beispielausgabe 1 | Beispielausgabe 2 |
|---|---|---|---|---|---|
| `templatingStrategy` | Erforderlich | Für jede Dateiformatierungsoption, die Sie konfigurieren, müssen Sie den Parameter `templatingStrategy` hinzufügen, der zwei Werte haben kann: <br><ul><li>`NONE`: Verwenden Sie diesen Wert, wenn Sie nicht zulassen möchten, dass Benutzerinnen und Benutzer zwischen verschiedenen Werten für eine Konfiguration auswählen können. Siehe [diese Konfiguration](#file-configuration-templating-none) für ein Beispiel, bei dem die Dateiformatierungsoptionen fest sind.</li><li>`PEBBLE_V1`: Verwenden Sie diesen Wert, wenn Sie Benutzerinnen und Benutzern die Auswahl zwischen verschiedenen Werten für eine Konfiguration ermöglichen möchten. In diesem Fall müssen Sie auch ein entsprechendes Kundendatenfeld in der Konfiguration des Endpunkts `/destination` festlegen, damit die verschiedenen Optionen für die Benutzerinnen und Benutzer in der Benutzeroberfläche angezeigt werden. In [dieser Konfiguration](#file-configuration-templating-pebble) sehen Sie ein Beispiel, wo Benutzerinnen und Benutzer für die Optionen zur Dateiformatierung zwischen verschiedenen Werten wählen können.</li></ul> | – | – | – |
| `compression.value` | Optional | Komprimierungs-Codec zum Speichern von Daten in einer Datei. Unterstützte Werte: `none`, `bzip2`, `gzip`, `lz4` und `snappy`. | `none` | – | – |
| `fileType.value` | Optional | Spezifiziert das Ausgabedateiformat. Unterstützte Werte: `csv`, `parquet` und `json`. | `csv` | – | – |
| `csvOptions.quote.value` | Optional | *Nur für`"fileType.value": "csv"`*. Legt ein einzelnes Zeichen fest, das zum Maskieren von angegebenen Werten verwendet wird, wobei das Trennzeichen Teil des Werts sein kann. | `null` | – | – |
| `csvOptions.quoteAll.value` | Optional | *Nur für`"fileType.value": "csv"`*. Gibt an, ob alle Werte immer in Anführungszeichen gesetzt werden sollen. Mit der Standardeinstellung werden nur Werte mit Escape-Zeichen versehen, die ein Anführungszeichen haben. | `false` | `quoteAll`:`false` --> `male,John,"TestLastName"` | `quoteAll`:`true` -->`"male","John","TestLastName"` |
| `csvOptions.delimiter.value` | Optional | *Nur für`"fileType.value": "csv"`*. Legt für jedes Feld und jeden Wert ein Trennzeichen fest. Dieses Trennzeichen kann aus einem oder mehreren Zeichen bestehen. | `,` | `delimiter`:`,` --> `comma-separated values"` | `delimiter`:`\t` --> `tab-separated values` |
| `csvOptions.escape.value` | Optional | *Nur für`"fileType.value": "csv"`*. Legt ein einzelnes Zeichen fest, das zum Maskieren von Anführungszeichen verwendet wird, die innerhalb eines bereits mit Anführungszeichen versehenen Werts liegen. | `\` | `"escape"`:`"\\"` --> `male,John,"Test,\"LastName5"` | `"escape"`:`"'"` --> `male,John,"Test,'''"LastName5"` |
| `csvOptions.escapeQuotes.value` | Optional | *Nur für`"fileType.value": "csv"`*. Gibt an, ob Werte, die Anführungszeichen enthalten, immer in Anführungszeichen gesetzt werden sollen. Standardmäßig werden alle Werte mit Escape-Zeichen versehen, die ein Anführungszeichen enthalten. | `true` | – | – |
| `csvOptions.header.value` | Optional | *Nur für`"fileType.value": "csv"`*. Gibt an, ob die Namen der Spalten als erste Zeile in die exportierte Datei geschrieben werden sollen. | `true` | – | – |
| `csvOptions.ignoreLeadingWhiteSpace.value` | Optional | *Nur für`"fileType.value": "csv"`*. Gibt an, ob vorangestellte Leerzeichen aus Werten entfernt werden sollen. | `true` | `ignoreLeadingWhiteSpace`:`true` --> `"male","John","TestLastName"` | `ignoreLeadingWhiteSpace`:`false`--> `"    male","John","TestLastName"` |
| `csvOptions.ignoreTrailingWhiteSpace.value` | Optional | *Nur für`"fileType.value": "csv"`*. Gibt an, ob nachgestellte Leerzeichen aus Werten entfernt werden sollen. | `true` | `ignoreTrailingWhiteSpace`:`true` --> `"male","John","TestLastName"` | `ignoreTrailingWhiteSpace`:`false`--> `"male    ","John","TestLastName"` |
| `csvOptions.nullValue.value` | Optional | *Nur für`"fileType.value": "csv"`*. Legt die Zeichenfolgendarstellung eines Nullwerts fest. | `""` | `nullvalue`:`""` --> `male,"",TestLastName` | `nullvalue`:`"NULL"` --> `male,NULL,TestLastName` |
| `csvOptions.dateFormat.value` | Optional | *Nur für`"fileType.value": "csv"`*. Gibt das Datumsformat an. | `yyyy-MM-dd` | `dateFormat`:`yyyy-MM-dd` --> `male,TestLastName,John,2022-02-24` | `dateFormat`:`MM/dd/yyyy` --> `male,TestLastName,John,02/24/2022` |
| `csvOptions.timestampFormat.value` | Optional | *Nur für`"fileType.value": "csv"`*. Legt die Zeichenfolge für ein Zeitstempelformat fest. | `yyyy-MM-dd'T'HH:mm:ss[.SSS][XXX]` | – | – |
| `csvOptions.charToEscapeQuoteEscaping.value` | Optional | *Nur für`"fileType.value": "csv"`*. Legt ein einzelnes Zeichen fest, das zum Maskieren des Escape-Zeichens für das Anführungszeichen verwendet wird. | `\` wenn Escape- und Anführungszeichen unterschiedlich sind. `\0` wenn Escape- und Anführungszeichen identisch sind. | – | – |
| `csvOptions.emptyValue.value` | Optional | *Nur für`"fileType.value": "csv"`*. Legt die Zeichenfolgendarstellung eines leeren Werts fest. | `""` | `"emptyValue":""` --> `male,"",John` | `"emptyValue":"empty"` --> `male,empty,John` |
| `maxFileRowCount` | Optional | Gibt die maximale Anzahl von Zeilen pro exportierter Datei zwischen 1.000.000 und 10.000.000 Zeilen an. | 5.000.000 |

{style="table-layout:auto"}

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Artikels sollten Sie ein besseres Verständnis davon haben, wie die Dateiformatierung in einer Ziel-Server-Konfiguration funktioniert und wie Sie sie konfigurieren können.

Weitere Informationen zu den anderen Ziel-Server-Komponenten finden Sie in den folgenden Artikeln:

* [Server-Spezifikationen für Ziele, die mit Destination SDK erstellt wurden](server-specs.md)
* [Vorlagenspezifikationen](templating-specs.md)
* [Nachrichtenformat](message-format.md)