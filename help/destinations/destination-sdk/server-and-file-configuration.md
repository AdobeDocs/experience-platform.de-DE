---
description: Die Server- und Dateikonfigurationsspezifikationen für dateibasierte Ziele können im Adobe Experience Platform Destination SDK über den Endpunkt /destination-servers konfiguriert werden.
title: (Beta) Konfigurationsoptionen für dateibasierte Ziel-Server-Spezifikationen
source-git-commit: bc357e2e93b80edb5f7825bf2dee692f14bd7297
workflow-type: ht
source-wordcount: '748'
ht-degree: 100%

---

# (Beta) Server- und Dateikonfiguration für dateibasierte Ziel-Server-Spezifikationen

## Übersicht {#overview}

>[!IMPORTANT]
>
>Die Funktion zum Konfigurieren und Übermitteln dateibasierter Ziele mithilfe des Adobe Experience Platform Destination SDK ist derzeit als Beta-Version verfügbar. Dokumentation und Funktionalität können sich ändern.

Auf dieser Seite werden alle Server-Konfigurationsoptionen für Ihre dateibasierten Ziel-Server beschrieben. Zusätzlich erfahren Sie, wie Sie verschiedene Dateikonfigurationsoptionen für Benutzer einrichten, die Dateien aus Experience Platform in Ihr Ziel exportieren.

Die Server- und Dateikonfigurationsspezifikationen für dateibasierte Ziele können im Adobe Experience Platform Destination SDK über den Endpunkt `/destination-servers` konfiguriert werden. Lesen Sie [API-Endpunktvorgänge des Ziel-Servers](./destination-server-api.md), um eine vollständige Liste der Vorgänge zu erhalten, die Sie am Endpunkt ausführen können.

## Dateibasierte Amazon-S3-Ziel-Server-Spezifikation {#s3-example}

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
| `destinationServerType` | Zeichenfolge | Legen Sie diesen Wert entsprechend Ihrer Zielplattform fest. Wählen Sie für [!DNL Amazon S3] den Wert `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden Sie `PEBBLE_V1`. |
| `fileBasedS3Destination.bucket.value` | Zeichenfolge | Der Name des [!DNL Amazon S3]-Buckets, der von diesem Ziel verwendet werden soll. |
| `fileBasedS3Destination.path.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden Sie `PEBBLE_V1`. |
| `fileBasedS3Destination.path.value` | Zeichenfolge | Der Pfad zum Zielordner, in dem die exportierten Dateien gespeichert werden. |

## Spezifikation des dateibasierten SFTP-Ziel-Servers {#sftp-example}

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
| `destinationServerType` | Zeichenfolge | Legen Sie diesen Wert entsprechend Ihrer Zielplattform fest. Wählen Sie für [!DNL SFTP]-Ziele `FILE_BASED_SFTP`. |
| `fileBasedSftpDestination.rootDirectory.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden Sie `PEBBLE_V1`. |
| `fileBasedSftpDestination.rootDirectory.value` | Zeichenfolge | Das Stammverzeichnis des Zielspeichers. |
| `fileBasedSftpDestination.hostName.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden Sie `PEBBLE_V1`. |
| `fileBasedSftpDestination.hostName.value` | Zeichenfolge | Der Host-Name des Zielspeichers. |
| `port` | Ganzzahl | Der SFTP-Datei-Server-Port. |
| `encryptionMode` | Zeichenfolge | Gibt an, ob eine Dateiverschlüsselung verwendet werden soll. Unterstützte Werte: <ul><li>PGP</li><li>Keine</li></ul> |

## Dateibasierte Ziel-Server-Spezifikation für [!DNL Azure Data Lake Storage] ([!DNL ADLS]) {#adls-example}

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
| `destinationServerType` | Zeichenfolge | Legen Sie diesen Wert entsprechend Ihrer Zielplattform fest. Wählen Sie für [!DNL Azure Data Lake Storage]-Ziele `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden Sie `PEBBLE_V1`. |
| `fileBasedAdlsGen2Destination.path.value` | Zeichenfolge | Der Pfad zum Zielordner, in dem die exportierten Dateien gespeichert werden. |

## Dateibasierte Ziel-Server-Spezifikation für [!DNL Azure Blob Storage] {#blob-example}

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
| `destinationServerType` | Zeichenfolge | Legen Sie diesen Wert entsprechend Ihrer Zielplattform fest. Wählen Sie für [!DNL Azure Blob Storage]-Ziele `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden Sie `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.path.value` | Zeichenfolge | Der Pfad zum Zielordner, in dem die exportierten Dateien gespeichert werden. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden Sie `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.container.value` | Zeichenfolge | Der Name des [!DNL Azure Blob Storage]-Containers, der von diesem Ziel verwendet werden soll. |

## Dateibasierte Ziel-Server-Spezifikation für [!DNL Data Landing Zone] ([!DNL DLZ]) {#dlz-example}

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
| `destinationServerType` | Zeichenfolge | Legen Sie diesen Wert entsprechend Ihrer Zielplattform fest. Wählen Sie für [!DNL Data Landing Zone]-Ziele `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | Zeichenfolge | *Erforderlich.*  Verwenden Sie `PEBBLE_V1`. |
| `fileBasedDlzDestination.path.value` | Zeichenfolge | Der Pfad zum Zielordner, in dem die exportierten Dateien gespeichert werden. |

## Dateibasierte Zieldateikonfiguration {#file-configuration}

In diesem Abschnitt werden die Dateiformatierungseinstellungen für die exportierten `CSV`-Dateien beschrieben. Sie können verschiedene Eigenschaften der exportierten Dateien an die Anforderungen des Dateiempfangssystems auf Ihrer Seite anpassen, um die aus Experience Platform empfangenen Dateien optimal zu lesen und zu interpretieren.

>[!NOTE]
>
>CSV-Optionen werden nur beim Exportieren von CSV-Dateien unterstützt. Der `fileConfigurations`-Abschnitt ist bei der Einrichtung eines neuen Ziel-Servers nicht erforderlich. Wenn Sie im API-Aufruf keine Werte für die CSV-Optionen übergeben, werden die Standardwerte aus der folgenden Tabelle verwendet.

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
| `compression.value` | Optional | Komprimierungs-Codec zum Speichern von Daten in einer Datei. Unterstützte Werte: `none`, `bzip2`, `gzip`, `lz4` und `snappy`. | `none` |
| `fileType.value` | Optional | Spezifiziert das Ausgabedateiformat. Unterstützte Werte: `csv`, `parquet` und `json`. | `csv` |
| `csvOptions.quote.value` | Optional | *Nur für`"fileType.value": "csv"`*. Legt ein einzelnes Zeichen fest, das zum Maskieren von angegebenen Werten verwendet wird, wobei das Trennzeichen Teil des Werts sein kann. | `null` |
| `csvOptions.quoteAll.value` | Optional | *Nur für`"fileType.value": "csv"`*. Gibt an, ob alle Werte immer in Anführungszeichen gesetzt werden sollen. Mit der Standardeinstellung werden nur Werte mit Escape-Zeichen versehen, die ein Anführungszeichen haben. | `false` |
| `csvOptions.escape.value` | Optional | *Nur für`"fileType.value": "csv"`*. Legt ein einzelnes Zeichen fest, das zum Maskieren von Anführungszeichen verwendet wird, die innerhalb eines bereits mit Anführungszeichen versehenen Werts liegen. | `\` |
| `csvOptions.escapeQuotes.value` | Optional | *Nur für`"fileType.value": "csv"`*. Gibt an, ob Werte, die Anführungszeichen enthalten, immer in Anführungszeichen gesetzt werden sollen. Standardmäßig werden alle Werte mit Escape-Zeichen versehen, die ein Anführungszeichen enthalten. | `true` |
| `csvOptions.header.value` | Optional | *Nur für`"fileType.value": "csv"`*. Gibt an, ob die Spaltennamen als erste Zeile geschrieben werden sollen. | `true` |
| `csvOptions.ignoreLeadingWhiteSpace.value` | Optional | *Nur für`"fileType.value": "csv"`*. Gibt an, ob vorangestellte Leerzeichen aus Werten entfernt werden sollen. | `true` |
| `csvOptions.ignoreTrailingWhiteSpace.value` | Optional | *Nur für`"fileType.value": "csv"`*. Gibt an, ob nachfolgende Leerzeichen aus Werten entfernt werden sollen. | `true` |
| `csvOptions.nullValue.value` | Optional | *Nur für`"fileType.value": "csv"`*. Legt die Zeichenfolgendarstellung eines Nullwerts fest. | `""` |
| `csvOptions.dateFormat.value` | Optional | *Nur für`"fileType.value": "csv"`*. Gibt das Datumsformat an. | `yyyy-MM-dd` |
| `csvOptions.timestampFormat.value` | Optional | *Nur für`"fileType.value": "csv"`*. Legt die Zeichenfolge für ein Zeitstempelformat fest. | `yyyy-MM-dd'T'HH:mm:ss[.SSS][XXX]` |
| `csvOptions.charToEscapeQuoteEscaping.value` | Optional | *Nur für`"fileType.value": "csv"`*. Legt ein einzelnes Zeichen fest, das zum Maskieren des Escape-Zeichens für das Anführungszeichen verwendet wird. | `\` wenn Escape- und Anführungszeichen unterschiedlich sind. `\0` wenn Escape- und Anführungszeichen identisch sind. |
| `csvOptions.emptyValue.value` | Optional | *Nur für`"fileType.value": "csv"`*. Legt die Zeichenfolgendarstellung eines leeren Werts fest. | `""` |
| `csvOptions.lineSep.value` | Optional | *Nur für`"fileType.value": "csv"`*. Definiert das Zeilentrennzeichen, das zum Schreiben verwendet werden soll. Die maximale Länge beträgt 1 Zeichen. | `\n` |
