---
description: Die Server- und Dateikonfigurationsspezifikationen für dateibasierte Ziele können im Adobe Experience Platform Destination SDK über den Endpunkt /destination-servers konfiguriert werden.
title: Konfigurationsoptionen für dateibasierte Ziel-Server-Spezifikationen
exl-id: 56434e36-0458-45d9-961d-f6505de998f7
source-git-commit: 29962e07aa50c97b6098f4c892facf48508d28cf
workflow-type: tm+mt
source-wordcount: '1248'
ht-degree: 57%

---

# Server- und Dateikonfiguration für dateibasierte Ziel-Server-Spezifikationen

## Übersicht {#overview}

Auf dieser Seite werden alle Serverkonfigurationsoptionen für Ihre dateibasierten Zielserver beschrieben und gezeigt, wie Sie verschiedene Dateikonfigurationsoptionen für Benutzer einrichten, die Dateien von Experience Platform an Ihr Ziel exportieren.

Die Server- und Dateikonfigurationsspezifikationen für dateibasierte Ziele können im Adobe Experience Platform Destination SDK über den Endpunkt `/destination-servers` konfiguriert werden. Lesen Sie [API-Endpunktvorgänge des Ziel-Servers](./destination-server-api.md), um eine vollständige Liste der Vorgänge zu erhalten, die Sie am Endpunkt ausführen können.

Die folgenden Abschnitte enthalten Zielserverspezifikationen, die für jeden unterstützten Batch-Zieltyp in Destination SDK spezifisch sind.

## Dateibasierte Amazon-S3-Ziel-Server-Spezifikation {#s3-example}

Das folgende Beispiel zeigt eine korrekte Zielserverkonfiguration für ein Amazon S3-Ziel.

```json
{
    "name": "S3 destination",
    "destinationServerType": "FILE_BASED_S3",
    "fileBasedS3Destination": {
        "bucket": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.bucket}}"
        },
        "path": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.path}}"
        }
    },
    "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| Parameter | Typ | Beschreibung |
|---|---|---|
| `name` | Zeichenfolge | Der Name Ihrer Zielverbindung. |
| `destinationServerType` | Zeichenfolge | Legen Sie diesen Wert entsprechend Ihrer Zielplattform fest. Wählen Sie für [!DNL Amazon S3] den Wert `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden Sie `PEBBLE_V1`. |
| `fileBasedS3Destination.bucket.value` | Zeichenfolge | Der Name des [!DNL Amazon S3]-Buckets, der von diesem Ziel verwendet werden soll. |
| `fileBasedS3Destination.path.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden Sie `PEBBLE_V1`. |
| `fileBasedS3Destination.path.value` | Zeichenfolge | Der Pfad zum Zielordner, in dem die exportierten Dateien gespeichert werden. |
| `fileConfigurations` | Objekt | Siehe [Dateiformatierungskonfiguration](#file-configuration) für ausführliche Erläuterungen zu diesem Abschnitt. |

{style=&quot;table-layout:auto&quot;}

## Spezifikation des dateibasierten SFTP-Ziel-Servers {#sftp-example}

Das folgende Beispiel zeigt eine korrekte Zielserverkonfiguration für ein SFTP-Ziel.

```json
{
   "name":"File-based SFTP destination server",
   "destinationServerType":"FILE_BASED_SFTP",
   "fileBasedSftpDestination":{
      "rootDirectory":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.rootDirectory}}"
      },
      "hostName":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.hostName}}"
      },
      "port": 22,
      "encryptionMode" : "PGP"
   },
    "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| Parameter | Typ | Beschreibung |
|---|---|---|
| `name` | Zeichenfolge | Der Name Ihrer Zielverbindung. |
| `destinationServerType` | Zeichenfolge | Legen Sie diesen Wert entsprechend Ihrer Zielplattform fest. Wählen Sie für [!DNL SFTP]-Ziele `FILE_BASED_SFTP`. |
| `fileBasedSftpDestination.rootDirectory.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden Sie `PEBBLE_V1`. |
| `fileBasedSftpDestination.rootDirectory.value` | Zeichenfolge | Das Stammverzeichnis des Zielspeichers. |
| `fileBasedSftpDestination.hostName.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden Sie `PEBBLE_V1`. |
| `fileBasedSftpDestination.hostName.value` | Zeichenfolge | Der Host-Name des Zielspeichers. |
| `port` | Ganzzahl | Der SFTP-Datei-Server-Port. |
| `encryptionMode` | Zeichenfolge | Gibt an, ob eine Dateiverschlüsselung verwendet werden soll. Unterstützte Werte: <ul><li>PGP</li><li>Keine</li></ul> |
| `fileConfigurations` | Objekt | Siehe [Dateiformatierungskonfiguration](#file-configuration) für ausführliche Erläuterungen zu diesem Abschnitt. |

{style=&quot;table-layout:auto&quot;}

## Dateibasierte Ziel-Server-Spezifikation für [!DNL Azure Data Lake Storage] ([!DNL ADLS]) {#adls-example}

Das folgende Beispiel zeigt eine korrekte Zielserverkonfiguration für eine [!DNL Azure Data Lake Storage] Ziel.

```json
{
   "name":"ADLS destination server",
   "destinationServerType":"FILE_BASED_ADLS_GEN2",
   "fileBasedAdlsGen2Destination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   },
  "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| Parameter | Typ | Beschreibung |
|---|---|---|
| `name` | Zeichenfolge | Der Name Ihrer Zielverbindung. |
| `destinationServerType` | Zeichenfolge | Legen Sie diesen Wert entsprechend Ihrer Zielplattform fest. Wählen Sie für [!DNL Azure Data Lake Storage]-Ziele `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden Sie `PEBBLE_V1`. |
| `fileBasedAdlsGen2Destination.path.value` | Zeichenfolge | Der Pfad zum Zielordner, in dem die exportierten Dateien gespeichert werden. |
| `fileConfigurations` | Objekt | Siehe [Dateiformatierungskonfiguration](#file-configuration) für ausführliche Erläuterungen zu diesem Abschnitt. |

{style=&quot;table-layout:auto&quot;}

## Dateibasierte Ziel-Server-Spezifikation für [!DNL Azure Blob Storage] {#blob-example}

Das folgende Beispiel zeigt eine korrekte Zielserverkonfiguration für eine [!DNL Azure Blob Storage] Ziel.

```json
{
   "name":"Blob destination server",
   "destinationServerType":"FILE_BASED_AZURE_BLOB",
   "fileBasedAzureBlobDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "container":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.container}}"
      }
   },
  "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| Parameter | Typ | Beschreibung |
|---|---|---|
| `name` | Zeichenfolge | Der Name Ihrer Zielverbindung. |
| `destinationServerType` | Zeichenfolge | Legen Sie diesen Wert entsprechend Ihrer Zielplattform fest. Wählen Sie für [!DNL Azure Blob Storage]-Ziele `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden Sie `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.path.value` | Zeichenfolge | Der Pfad zum Zielordner, in dem die exportierten Dateien gespeichert werden. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden Sie `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.container.value` | Zeichenfolge | Der Name des [!DNL Azure Blob Storage]-Containers, der von diesem Ziel verwendet werden soll. |
| `fileConfigurations` | Objekt | Siehe [Dateiformatierungskonfiguration](#file-configuration) für ausführliche Erläuterungen zu diesem Abschnitt. |

{style=&quot;table-layout:auto&quot;}

## Dateibasierte Ziel-Server-Spezifikation für [!DNL Data Landing Zone] ([!DNL DLZ]) {#dlz-example}

Das folgende Beispiel zeigt eine korrekte Zielserverkonfiguration für eine [!DNL Data Landing Zone] ([!DNL DLZ]).

```json
{
   "name":"DLZ destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "useCase": "Your use case"
   },
   "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| Parameter | Typ | Beschreibung |
|---|---|---|
| `name` | Zeichenfolge | Der Name Ihrer Zielverbindung. |
| `destinationServerType` | Zeichenfolge | Legen Sie diesen Wert entsprechend Ihrer Zielplattform fest. Wählen Sie für [!DNL Data Landing Zone]-Ziele `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | Zeichenfolge | *Erforderlich.*  Verwenden Sie `PEBBLE_V1`. |
| `fileBasedDlzDestination.path.value` | Zeichenfolge | Der Pfad zum Zielordner, in dem die exportierten Dateien gespeichert werden. |
| `fileConfigurations` | Objekt | Siehe [Dateiformatierungskonfiguration](#file-configuration) für ausführliche Erläuterungen zu diesem Abschnitt. |

{style=&quot;table-layout:auto&quot;}

## Dateibasierte Ziel-Server-Spezifikation für [!DNL Google Cloud Storage] {#gcs-example}

Das folgende Beispiel zeigt eine korrekte Zielserverkonfiguration für eine [!DNL Google Cloud Storage] Ziel.

```json
{
   "name":"Google Cloud Storage Server",
   "destinationServerType":"FILE_BASED_GOOGLE_CLOUD",
   "fileBasedGoogleCloudStorageDestination":{
      "bucket":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucket}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   },
   "fileConfigurations":{
      // See the file formatting configuration section further below on this page
   }
}
```

| Parameter | Typ | Beschreibung |
|---|---|---|
| `name` | Zeichenfolge | Der Name Ihrer Zielverbindung. |
| `destinationServerType` | Zeichenfolge | Legen Sie diesen Wert entsprechend Ihrer Zielplattform fest. Wählen Sie für [!DNL Google Cloud Storage]-Ziele `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | Zeichenfolge | *Erforderlich.*  Verwenden Sie `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | Zeichenfolge | Der Name des [!DNL Google Cloud Storage]-Buckets, der von diesem Ziel verwendet werden soll. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden Sie `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.path.value` | Zeichenfolge | Der Pfad zum Zielordner, in dem die exportierten Dateien gespeichert werden. |
| `fileConfigurations` | Objekt | Siehe [Dateiformatierungskonfiguration](#file-configuration) für ausführliche Erläuterungen zu diesem Abschnitt. |

{style=&quot;table-layout:auto&quot;}

## Dateiformatierung {#file-configuration}

In diesem Abschnitt werden die Dateiformatierungseinstellungen für die exportierten `CSV`-Dateien beschrieben. Sie können verschiedene Eigenschaften der exportierten Dateien an die Anforderungen des Dateiempfangssystems auf Ihrer Seite anpassen, um die aus Experience Platform empfangenen Dateien optimal zu lesen und zu interpretieren.

>[!NOTE]
>
>CSV-Optionen werden nur beim Exportieren von CSV-Dateien unterstützt. Der `fileConfigurations`-Abschnitt ist bei der Einrichtung eines neuen Ziel-Servers nicht erforderlich. Wenn Sie keine Werte im API-Aufruf für die CSV-Optionen übergeben, werden die Standardwerte aus der [Referenztabelle weiter unten](#file-formatting-reference-and-example) verwendet.

### Dateikonfigurationen mit CSV-Optionen und `templatingStrategy` auf `NONE` {#file-configuration-templating-none}

Im folgenden Konfigurationsbeispiel werden alle CSV-Optionen korrigiert. Die in den einzelnen `csvOptions` -Parameter sind endgültig und Benutzer können sie nicht ändern.

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

### Dateikonfigurationen mit CSV-Optionen und `templatingStrategy` auf `PEBBLE_V1` {#file-configuration-templating-pebble}

Im folgenden Konfigurationsbeispiel wurde keine der CSV-Optionen korrigiert. Die `value` in jedem `csvOptions` -Parameter in einem entsprechenden Kundendatenfeld über die `/destinations` Endpunkt (z. B. `customerData.quote` für `quote` Dateiformatierung) und Benutzer können über die Experience Platform-Benutzeroberfläche zwischen den verschiedenen Optionen wählen, die Sie im entsprechenden Kundendatenfeld konfigurieren.

```json
  "fileConfigurations": {
    "compression": {
      "templatingStrategy": "PEBBLE_V1",
      "value": "{% if customerData contains 'compression' and customerData.compression is not empty %}{{customerData.compression}}{% else %}NONE{% endif %}"
    },
    "fileType": {
      "templatingStrategy": "PEBBLE_V1",
      "value": "{{customerData.fileType}}"
    },
    "csvOptions": {
      "sep": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'delimiter' %}{{customerData.csvOptions.delimiter}}{% else %},{% endif %}"
      },
      "quote": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'quote' %}{{customerData.csvOptions.quote}}{% else %}\"{% endif %}"
      },
      "escape": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'escape' %}{{customerData.csvOptions.escape}}{% else %}\\{% endif %}"
      },
      "nullValue": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'nullValue' %}{{customerData.csvOptions.nullValue}}{% else %}null{% endif %}"
      },
      "emptyValue": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'emptyValue' %}{{customerData.csvOptions.emptyValue}}{% else %}{% endif %}"
      }
    }
  }
```

### Vollständige Referenz und Beispiele für unterstützte Dateiformatierungsoptionen {#file-formatting-reference-and-example}

>[!TIP]
>
>Die im Folgenden beschriebenen CSV-Dateiformatierungsoptionen werden ebenfalls im Abschnitt [Apache Spark-Anleitung für CSV-Dateien](https://spark.apache.org/docs/latest/sql-data-sources-csv.html). Die unten verwendeten Beschreibungen stammen aus dem Apache Spark-Handbuch.

Nachstehend finden Sie eine vollständige Referenz aller verfügbaren Dateiformatierungsoptionen in Destination SDK zusammen mit Ausgabebeispielen für jede Option.

| Feld | Erforderlich/Optional | Beschreibung | Standardwert | Beispielausgabe 1 | Beispielausgabe 2 |
|---|---|---|---|---|---|
| `templatingStrategy` | Erforderlich | Für jede Dateiformatierungsoption, die Sie konfigurieren, müssen Sie den Parameter hinzufügen `templatingStrategy`, der zwei Werte haben kann: <br><ul><li>`NONE`: Verwenden Sie diesen Wert, wenn Sie nicht zulassen möchten, dass Benutzer zwischen verschiedenen Werten für eine Konfiguration auswählen können. Siehe [diese Konfiguration](#file-configuration-templating-none) für ein Beispiel, bei dem die Dateiformatierungsoptionen korrigiert wurden.</li><li>`PEBBLE_V1`: Verwenden Sie diesen Wert, wenn Sie Benutzern die Auswahl zwischen verschiedenen Werten für eine Konfiguration ermöglichen möchten. In diesem Fall müssen Sie auch ein entsprechendes Kundendatenfeld im `/destination` Endpunktkonfiguration, um die verschiedenen Optionen für Benutzer in der Benutzeroberfläche zu überdecken. Siehe [diese Konfiguration](#file-configuration-templating-pebble) Beispiel: Benutzer können für Optionen zur Dateiformatierung zwischen verschiedenen Werten wählen.</li></ul> | – | – | – |
| `compression.value` | Optional | Komprimierungs-Codec zum Speichern von Daten in einer Datei. Unterstützte Werte: `none`, `bzip2`, `gzip`, `lz4` und `snappy`. | `none` | – | – |
| `fileType.value` | Optional | Spezifiziert das Ausgabedateiformat. Unterstützte Werte: `csv`, `parquet` und `json`. | `csv` | – | – |
| `csvOptions.quote.value` | Optional | *Nur für`"fileType.value": "csv"`*. Legt ein einzelnes Zeichen fest, das zum Maskieren von angegebenen Werten verwendet wird, wobei das Trennzeichen Teil des Werts sein kann. | `null` | – | – |
| `csvOptions.quoteAll.value` | Optional | *Nur für`"fileType.value": "csv"`*. Gibt an, ob alle Werte immer in Anführungszeichen gesetzt werden sollen. Mit der Standardeinstellung werden nur Werte mit Escape-Zeichen versehen, die ein Anführungszeichen haben. | `false` | `quoteAll`:`false` --> `male,John,"TestLastName"` | `quoteAll`:`true` -->`"male","John","TestLastName"` |
| `csvOptions.delimiter.value` | Optional | *Nur für`"fileType.value": "csv"`*. Legt für jedes Feld und jeden Wert ein Trennzeichen fest. Dieses Trennzeichen kann ein oder mehrere Zeichen sein. | `,` | `delimiter`:`,` —> `comma-separated values"` | `delimiter`:`\t` —> `tab-separated values` |
| `csvOptions.escape.value` | Optional | *Nur für`"fileType.value": "csv"`*. Legt ein einzelnes Zeichen fest, das zum Maskieren von Anführungszeichen verwendet wird, die innerhalb eines bereits mit Anführungszeichen versehenen Werts liegen. | `\` | `"escape"`:`"\\"` —> `male,John,"Test,\"LastName5"` | `"escape"`:`"'"` —> `male,John,"Test,'''"LastName5"` |
| `csvOptions.escapeQuotes.value` | Optional | *Nur für`"fileType.value": "csv"`*. Gibt an, ob Werte, die Anführungszeichen enthalten, immer in Anführungszeichen gesetzt werden sollen. Standardmäßig werden alle Werte mit Escape-Zeichen versehen, die ein Anführungszeichen enthalten. | `true` | – | – |
| `csvOptions.header.value` | Optional | *Nur für`"fileType.value": "csv"`*. Gibt an, ob die Namen der Spalten als erste Zeile in die exportierte Datei geschrieben werden sollen. | `true` | – | – |
| `csvOptions.ignoreLeadingWhiteSpace.value` | Optional | *Nur für`"fileType.value": "csv"`*. Gibt an, ob vorangestellte Leerzeichen aus Werten entfernt werden sollen. | `true` | `ignoreLeadingWhiteSpace`:`true` —> `"male","John","TestLastName"` | `ignoreLeadingWhiteSpace`:`false`--> `"    male","John","TestLastName"` |
| `csvOptions.ignoreTrailingWhiteSpace.value` | Optional | *Nur für`"fileType.value": "csv"`*. Gibt an, ob nachfolgende Leerzeichen aus Werten beschnitten werden sollen. | `true` | `ignoreTrailingWhiteSpace`:`true` —> `"male","John","TestLastName"` | `ignoreTrailingWhiteSpace`:`false`—> `"male    ","John","TestLastName"` |
| `csvOptions.nullValue.value` | Optional | *Nur für`"fileType.value": "csv"`*. Legt die Zeichenfolgendarstellung eines Nullwerts fest. | `""` | `nullvalue`:`""` —> `male,"",TestLastName` | `nullvalue`:`"NULL"` —> `male,NULL,TestLastName` |
| `csvOptions.dateFormat.value` | Optional | *Nur für`"fileType.value": "csv"`*. Gibt das Datumsformat an. | `yyyy-MM-dd` | `dateFormat`:`yyyy-MM-dd` —> `male,TestLastName,John,2022-02-24` | `dateFormat`:`MM/dd/yyyy` —> `male,TestLastName,John,02/24/2022` |
| `csvOptions.timestampFormat.value` | Optional | *Nur für`"fileType.value": "csv"`*. Legt die Zeichenfolge für ein Zeitstempelformat fest. | `yyyy-MM-dd'T'HH:mm:ss[.SSS][XXX]` | – | – |
| `csvOptions.charToEscapeQuoteEscaping.value` | Optional | *Nur für`"fileType.value": "csv"`*. Legt ein einzelnes Zeichen fest, das zum Maskieren des Escape-Zeichens für das Anführungszeichen verwendet wird. | `\` wenn Escape- und Anführungszeichen unterschiedlich sind. `\0` wenn Escape- und Anführungszeichen identisch sind. | – | – |
| `csvOptions.emptyValue.value` | Optional | *Nur für`"fileType.value": "csv"`*. Legt die Zeichenfolgendarstellung eines leeren Werts fest. | `""` | `"emptyValue":""` --> `male,"",John` | `"emptyValue":"empty"` —> `male,empty,John` |

{style=&quot;table-layout:auto&quot;}