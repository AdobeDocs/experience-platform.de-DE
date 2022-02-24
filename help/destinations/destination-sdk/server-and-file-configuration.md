---
description: Die Server- und Dateikonfigurationsspezifikationen für dateibasierte Ziele können in Adobe Experience Platform Destination SDK über den Endpunkt /destination-servers konfiguriert werden.
title: (Beta) Konfigurationsoptionen für dateibasierte Zielserverspezifikationen
source-git-commit: bc357e2e93b80edb5f7825bf2dee692f14bd7297
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 12%

---

# (Beta) Server- und Dateikonfiguration für dateibasierte Zielserverspezifikationen

## Übersicht {#overview}

>[!IMPORTANT]
>
>Die Funktion zum Konfigurieren und Senden dateibasierter Ziele mithilfe von Adobe Experience Platform Destination SDK ist derzeit als Beta-Version verfügbar. Dokumentation und Funktionalität können sich ändern.

Auf dieser Seite werden alle Serverkonfigurationsoptionen für Ihre dateibasierten Zielserver beschrieben und Sie erfahren, wie Sie verschiedene Dateikonfigurationsoptionen für Benutzer einrichten, die Dateien aus der Experience Platform in Ihr Ziel exportieren.

Die Server- und Dateikonfigurationsspezifikationen für dateibasierte Ziele können in Adobe Experience Platform Destination SDK über die `/destination-servers` -Endpunkt. Lesen [API-Endpunktvorgänge des Zielservers](./destination-server-api.md) für eine vollständige Liste der Vorgänge, die Sie am -Endpunkt ausführen können.

## Dateibasierte Amazon S3-Zielserverspezifikation {#s3-example}

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
       // see File-based destinations file configuration
    }
}
```

| Parameter | Typ | Beschreibung |
|---|---|---|
| `name` | Zeichenfolge | Der Name Ihrer Zielverbindung. |
| `destinationServerType` | Zeichenfolge | Legen Sie diesen Wert entsprechend Ihrer Zielplattform fest. Für [!DNL Amazon S3], setzen Sie dies auf `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden von `PEBBLE_V1`. |
| `fileBasedS3Destination.bucket.value` | Zeichenfolge | Der Name der [!DNL Amazon S3] -Bucket, der von diesem Ziel verwendet werden soll. |
| `fileBasedS3Destination.path.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden von `PEBBLE_V1`. |
| `fileBasedS3Destination.path.value` | Zeichenfolge | Der Pfad zum Zielordner, in dem die exportierten Dateien gehostet werden. |

## Spezifikation des dateibasierten SFTP-Zielservers {#sftp-example}

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
       // see File-based destinations file configuration
    }
}
```

| Parameter | Typ | Beschreibung |
|---|---|---|
| `name` | Zeichenfolge | Der Name Ihrer Zielverbindung. |
| `destinationServerType` | Zeichenfolge | Legen Sie diesen Wert entsprechend Ihrer Zielplattform fest. Für [!DNL SFTP] Ziele, setzen Sie dies auf `FILE_BASED_SFTP`. |
| `fileBasedSftpDestination.rootDirectory.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden von `PEBBLE_V1`. |
| `fileBasedSftpDestination.rootDirectory.value` | Zeichenfolge | Der Stammordner des Zielspeichers. |
| `fileBasedSftpDestination.hostName.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden von `PEBBLE_V1`. |
| `fileBasedSftpDestination.hostName.value` | Zeichenfolge | Der Hostname des Zielspeichers. |
| `port` | Ganzzahl | Der SFTP-Dateiserver-Port. |
| `encryptionMode` | Zeichenfolge | Gibt an, ob die Dateiverschlüsselung verwendet werden soll. Unterstützte Werte: <ul><li>PGP</li><li>Keine</li></ul> |

## Dateibasiert [!DNL Azure Data Lake Storage] ([!DNL ADLS]) Ziel-Server-Spezifikation {#adls-example}

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
       // see File-based destinations file configuration
    }
}
```

| Parameter | Typ | Beschreibung |
|---|---|---|
| `name` | Zeichenfolge | Der Name Ihrer Zielverbindung. |
| `destinationServerType` | Zeichenfolge | Legen Sie diesen Wert entsprechend Ihrer Zielplattform fest. Für [!DNL Azure Data Lake Storage] Ziele, setzen Sie dies auf `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden von `PEBBLE_V1`. |
| `fileBasedAdlsGen2Destination.path.value` | Zeichenfolge | Der Pfad zum Zielordner, in dem die exportierten Dateien gehostet werden. |

## Dateibasiert [!DNL Azure Blob Storage] Zielserverspezifikation {#blob-example}

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
       // see File-based destinations file configuration
    }
}
```

| Parameter | Typ | Beschreibung |
|---|---|---|
| `name` | Zeichenfolge | Der Name Ihrer Zielverbindung. |
| `destinationServerType` | Zeichenfolge | Legen Sie diesen Wert entsprechend Ihrer Zielplattform fest. Für [!DNL Azure Blob Storage] Ziele, setzen Sie dies auf `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden von `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.path.value` | Zeichenfolge | Der Pfad zum Zielordner, in dem die exportierten Dateien gehostet werden. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden von `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.container.value` | Zeichenfolge | Der Name der [!DNL Azure Blob Storage] Container, der von diesem Ziel verwendet werden soll. |

## Dateibasiert [!DNL Data Landing Zone] ([!DNL DLZ]) Ziel-Server-Spezifikation {#dlz-example}

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
       // see File-based destinations file configuration
    }
}
```

| Parameter | Typ | Beschreibung |
|---|---|---|
| `name` | Zeichenfolge | Der Name Ihrer Zielverbindung. |
| `destinationServerType` | Zeichenfolge | Legen Sie diesen Wert entsprechend Ihrer Zielplattform fest. Für [!DNL Data Landing Zone] Ziele, setzen Sie dies auf `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | Zeichenfolge | *Erforderlich.*  Verwenden von `PEBBLE_V1`. |
| `fileBasedDlzDestination.path.value` | Zeichenfolge | Der Pfad zum Zielordner, in dem die exportierten Dateien gehostet werden. |

## Dateibasierte Zieldateikonfiguration {#file-configuration}

In diesem Abschnitt werden die Dateiformatierungseinstellungen für die exportierte `CSV` Dateien. Sie können verschiedene Eigenschaften der exportierten Dateien an die Anforderungen des Dateiempfangssystems auf Ihrer Seite anpassen, um die von Experience Platform empfangenen Dateien optimal zu lesen und zu interpretieren.

>[!NOTE]
>
>CSV-Optionen werden nur beim Exportieren von CSV-Dateien unterstützt. Die `fileConfigurations` ist bei der Einrichtung eines neuen Zielservers nicht erforderlich. Wenn Sie keine Werte im API-Aufruf für die CSV-Optionen übergeben, werden die Standardwerte aus der folgenden Tabelle verwendet.

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
            },
            "lineSep": {
                "templatingStrategy": "NONE",
                "value": "\n"
            }
        }
    }
```

| Feld | Erforderlich/Optional | Beschreibung | Standardwert |
|---|---|---|---|
| `compression.value` | Optional | Komprimierungs-Codec zum Speichern von Daten in einer Datei. Unterstützte Werte: `none`, `bzip2`, `gzip`, `lz4`und `snappy`. | `none` |
| `fileType.value` | Optional | Gibt das Ausgabedateiformat an. Unterstützte Werte: `csv`, `parquet`und `json`. | `csv` |
| `csvOptions.quote.value` | Optional | *Nur für`"fileType.value": "csv"`*. Legt ein einzelnes Zeichen fest, das zum Maskieren von angegebenen Werten verwendet wird, wobei das Trennzeichen Teil des Werts sein kann. | `null` |
| `csvOptions.quoteAll.value` | Optional | *Nur für`"fileType.value": "csv"`*. Gibt an, ob alle Werte immer in Anführungszeichen gesetzt werden sollen. Die Standardeinstellung ist, dass nur Werte mit einem Anführungszeichen als Escape-Zeichen verwendet werden. | `false` |
| `csvOptions.escape.value` | Optional | *Nur für`"fileType.value": "csv"`*. Legt ein einzelnes Zeichen fest, das zum Maskieren von Anführungszeichen innerhalb eines bereits zitierten Werts verwendet wird. | `\` |
| `csvOptions.escapeQuotes.value` | Optional | *Nur für`"fileType.value": "csv"`*. Gibt an, ob Werte, die Anführungszeichen enthalten, immer in Anführungszeichen gesetzt werden sollen. Standardmäßig werden alle Werte mit einem Anführungszeichen als Escape-Zeichen verwendet. | `true` |
| `csvOptions.header.value` | Optional | *Nur für`"fileType.value": "csv"`*. Gibt an, ob die Spaltennamen als erste Zeile geschrieben werden sollen. | `true` |
| `csvOptions.ignoreLeadingWhiteSpace.value` | Optional | *Nur für`"fileType.value": "csv"`*. Gibt an, ob vorangestellte Leerzeichen aus Werten beschnitten werden sollen. | `true` |
| `csvOptions.ignoreTrailingWhiteSpace.value` | Optional | *Nur für`"fileType.value": "csv"`*. Gibt an, ob nachfolgende Leerzeichen aus Werten entfernt werden sollen. | `true` |
| `csvOptions.nullValue.value` | Optional | *Nur für`"fileType.value": "csv"`*. Legt die Zeichenfolgendarstellung eines Nullwerts fest. | `""` |
| `csvOptions.dateFormat.value` | Optional | *Nur für`"fileType.value": "csv"`*. Gibt das Datumsformat an. | `yyyy-MM-dd` |
| `csvOptions.timestampFormat.value` | Optional | *Nur für`"fileType.value": "csv"`*. Legt die Zeichenfolge fest, die ein Zeitstempelformat angibt. | `yyyy-MM-dd'T'HH:mm:ss[.SSS][XXX]` |
| `csvOptions.charToEscapeQuoteEscaping.value` | Optional | *Nur für`"fileType.value": "csv"`*. Legt ein einzelnes Zeichen fest, das zum Escapen des Escape-Zeichens für das Anführungszeichen verwendet wird. | `\` wenn die Escape- und Anführungszeichen unterschiedlich sind. `\0` wenn das Escape- und das Anführungszeichen identisch sind. |
| `csvOptions.emptyValue.value` | Optional | *Nur für`"fileType.value": "csv"`*. Legt die Zeichenfolgendarstellung eines leeren Werts fest. | `""` |
| `csvOptions.lineSep.value` | Optional | *Nur für`"fileType.value": "csv"`*. Definiert das Zeilentrennzeichen, das zum Schreiben verwendet werden soll. Die maximale Länge beträgt 1 Zeichen. | `\n` |
