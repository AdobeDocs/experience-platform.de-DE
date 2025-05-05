---
description: Auf dieser Seite werden die Schritte zum Konfigurieren eines dateibasierten Ziels mithilfe des Destination SDK aufgeführt und beschrieben.
title: Verwenden des Destination SDK zum Konfigurieren eines dateibasierten Ziels
exl-id: 84d73452-88e4-4e0f-8fc7-d0d8e10f9ff5
source-git-commit: 804370a778a4334603f3235df94edaa91b650223
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 55%

---

# Verwenden des Destination SDK zum Konfigurieren eines dateibasierten Ziels

## Überblick {#overview}

Auf dieser Seite wird beschrieben, wie Sie die Informationen in [Konfigurationsoptionen im Destination SDK](../functionality/configuration-options.md) und in anderen Destination SDK-Funktionen und API-Referenzdokumenten verwenden können, um ein [dateibasiertes Ziel](../../destination-types.md#file-based) zu konfigurieren. Die Schritte sind im Folgenden in der vorgegebenen Reihenfolge aufgeführt.

## Voraussetzungen {#prerequisites}

Bevor Sie mit den unten dargestellten Schritten fortfahren, informieren Sie sich auf der Seite [Erste Schritte mit dem Destination SDK](../getting-started.md), wie Sie die erforderlichen Adobe I/O-Authentifizierungs-Anmeldedaten und andere Voraussetzungen für die Arbeit mit Destination SDK-APIs erhalten.

## Schritte zum Verwenden der Konfigurationsoptionen im Destination SDK zum Einrichten Ihres Ziels {#steps}

![Veranschaulichte Schritte zur Verwendung von Destination SDK-Endpunkten](../assets/guides/destination-sdk-steps-batch.png)

## Schritt 1: Erstellen einer Server- und Dateikonfiguration {#create-server-file-configuration}

Erstellen Sie zunächst [Server- und Dateikonfiguration](../authoring-api/destination-server/create-destination-server.md) mithilfe des `/destinations-server`-Endpunkts.

Nachfolgend finden Sie eine Beispielkonfiguration für ein [!DNL Amazon S3]-Ziel. Weitere Informationen zu den in der Konfiguration verwendeten Feldern und zum Konfigurieren anderer Typen dateibasierter Ziele finden Sie unter den entsprechenden [Server-Konfigurationen](../functionality/destination-server/server-specs.md).

**API-Format**

```shell
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

```json
{
    "name": "S3 destination",
    "destinationServerType": "FILE_BASED_S3",
    "fileBasedS3Destination": {
        "bucket": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.bucketName}}"
        },
        "path": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.path}}"
        }
    },
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
        }
    }
}
```

## Schritt 2: Erstellen einer Zielkonfiguration {#create-destination-configuration}

Unten sehen Sie ein Beispiel für eine Zielkonfiguration, die mithilfe des `/destinations`-API-Endpunkts erstellt wurde.

Um die Server- und Dateikonfiguration aus Schritt 1 mit dieser Zielkonfiguration zu verbinden, fügen Sie die `instance ID` der Server- und Dateikonfiguration wie hier `destinationServerId` hinzu.

**API-Format**

```http
POST platform.adobe.io/data/core/activation/authoring/destinations
```

```json {line-numbers="true" highlight="83"}
{
    "name": "Amazon S3 destination",
    "description": "Amazon S3 destination is a fictional destination, used for this example.",
    "status": "Test",
    "customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
    "customerEncryptionConfigurations": [],
    "customerDataFields": [
        {
            "name": "bucketName",
            "title": "Amazon S3 bucket name",
            "description": "Enter the Amazon S3 Bucket name that will host the exported files.",
            "type": "string",
            "isRequired": true,
            "pattern": "(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "path",
            "title": "Amazon S3 path",
            "description": "Enter Amazon S3 folder path",
            "type": "string",
            "isRequired": true,
            "pattern": "^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "compression",
            "title": "Select compression type",
            "description": "Select the file compression type used by the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "enum": [
                "GZIP",
                "NONE",
                "bzip2",
                "lz4",
                "snappy",
                "deflate"
            ]
        },
        {
            "name": "fileType",
            "title": "Select a file format",
            "description": "Select the file format to be used by the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "hidden": false,
            "enum": [
                "csv",
                "json",
                "parquet"
            ],
            "default": "csv"
        }
    ],
    "uiAttributes": {
        "documentationLink": "https://www.adobe.com/go/destinations-YOURDESTINATION-en",
        "category": "S3",
        "connectionType": "S3",
        "flowRunsSupported": true,
        "monitoringSupported": true,
        "frequency": "Batch"
    },
    "destinationDelivery": [
        {
            "deliveryMatchers": [
                {
                    "type": "SOURCE",
                    "value": [
                        "batch"
                    ]
                }
            ],
            "authenticationRule": "CUSTOMER_AUTHENTICATION",
            "destinationServerId": "eec25bde-4f56-4c02-a830-9aa9ec73ee9d"
        }
    ],
    "schemaConfig": {
        "profileRequired": true,
        "segmentRequired": true,
        "identityRequired": true
    },
    "batchConfig": {
        "allowMandatoryFieldSelection": true,
        "allowDedupeKeyFieldSelection": true,
        "defaultExportMode": "DAILY_FULL_EXPORT",
        "allowedExportMode": [
            "DAILY_FULL_EXPORT",
            "FIRST_FULL_THEN_INCREMENTAL"
        ],
        "allowedScheduleFrequency": [
            "DAILY",
            "EVERY_3_HOURS",
            "EVERY_6_HOURS",
            "EVERY_8_HOURS",
            "EVERY_12_HOURS",
            "ONCE"
        ],
        "defaultFrequency": "DAILY",
        "defaultStartTime": "00:00",
       "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_ID",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%"
      }
    },
    "backfillHistoricalProfileData": true
}
```

## Schritt 3: Erstellen einer Zielgruppen-Metadatenkonfiguration {#create-audience-metadata-configuration}

Für einige Ziele erfordert das Destination SDK, dass Sie eine Zielgruppen-Metadatenkonfiguration konfigurieren, um Zielgruppen in Ihrem Ziel programmgesteuert zu erstellen, zu aktualisieren oder zu löschen. Informationen dazu, wann Sie diese Konfiguration einrichten müssen und wie Sie sie durchführen, finden Sie unter [Zielgruppen-Metadatenverwaltung](../functionality/audience-metadata-management.md).

Wenn Sie eine Zielgruppen-Metadatenkonfiguration verwenden, müssen Sie diese mit der Zielkonfiguration verbinden, die Sie in Schritt 2 erstellt haben. Fügen Sie die Instanz-ID Ihrer Zielgruppen-Metadatenkonfiguration als `audienceTemplateId` zu Ihrer Zielkonfiguration hinzu.

```json {line-numbers="true" highlight="90"}
{
    "name": "Amazon S3 destination",
    "description": "Amazon S3 destination is a fictional destination, used for this example.",
    "status": "Test",
    "customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
    "customerEncryptionConfigurations": [],
    "customerDataFields": [
        {
            "name": "bucketName",
            "title": "Amazon S3 bucket name",
            "description": "Enter the Amazon S3 Bucket name that will host the exported files.",
            "type": "string",
            "isRequired": true,
            "pattern": "(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "path",
            "title": "Amazon S3 path",
            "description": "Enter Amazon S3 folder path",
            "type": "string",
            "isRequired": true,
            "pattern": "^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "compression",
            "title": "Select compression type",
            "description": "Select the file compression type used by the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "enum": [
                "GZIP",
                "NONE",
                "bzip2",
                "lz4",
                "snappy",
                "deflate"
            ]
        },
        {
            "name": "fileType",
            "title": "Select a file format",
            "description": "Select the file format to be used by the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "hidden": false,
            "enum": [
                "csv",
                "json",
                "parquet"
            ],
            "default": "csv"
        }
    ],
    "uiAttributes": {
        "documentationLink": "http://www.adobe.com/go/destinations-YOURDESTINATION-en",
        "category": "S3",
        "connectionType": "S3",
        "flowRunsSupported": true,
        "monitoringSupported": true,
        "frequency": "Batch"
    },
    "destinationDelivery": [
        {
            "deliveryMatchers": [
                {
                    "type": "SOURCE",
                    "value": [
                        "batch"
                    ]
                }
            ],
            "authenticationRule": "CUSTOMER_AUTHENTICATION",
            "destinationServerId": "eec25bde-4f56-4c02-a830-9aa9ec73ee9d"
        }
    ],
    "segmentMappingConfig":{
        "mapExperiencePlatformSegmentName":false,
        "mapExperiencePlatformSegmentId":false,
        "mapUserInput":false
    },
    "audienceMetadataConfig":{
        "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
    },   
    "schemaConfig": {
        "profileRequired": true,
        "segmentRequired": true,
        "identityRequired": true
    },
    "batchConfig": {
        "allowMandatoryFieldSelection": true,
        "allowDedupeKeyFieldSelection": true,
        "defaultExportMode": "DAILY_FULL_EXPORT",
        "allowedExportMode": [
            "DAILY_FULL_EXPORT",
            "FIRST_FULL_THEN_INCREMENTAL"
        ],
        "allowedScheduleFrequency": [
            "DAILY",
            "EVERY_3_HOURS",
            "EVERY_6_HOURS",
            "EVERY_8_HOURS",
            "EVERY_12_HOURS",
            "ONCE"
        ],
        "defaultFrequency": "DAILY",
        "defaultStartTime": "00:00",
       "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_ID",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%"
      }
    },
    "backfillHistoricalProfileData": true
}
```

## Schritt 4: Einrichten der Authentifizierung {#set-up-authentication}

Je nachdem, ob Sie `"authenticationRule": "CUSTOMER_AUTHENTICATION"` oder `"authenticationRule": "PLATFORM_AUTHENTICATION"` in der obigen Zielkonfiguration angeben, können Sie die Authentifizierung für Ihr Ziel einrichten, indem Sie den Endpunkt `/destination` oder `/credentials` verwenden.

>[!NOTE]
>
>`CUSTOMER_AUTHENTICATION` ist die häufigere der beiden Authentifizierungsregeln und die zu verwendende, wenn Sie Benutzerinnen und Benutzer auffordern, Ihrem Ziel eine bestimmte Form der Authentifizierung bereitzustellen, bevor sie eine Verbindung einrichten und Daten exportieren können.

* Wenn Sie in der Zielkonfiguration `"authenticationRule": "CUSTOMER_AUTHENTICATION"` ausgewählt haben, finden Sie in den folgenden Abschnitten Informationen zu den Authentifizierungstypen, die vom Destination SDK für dateibasierte Ziele unterstützt werden:

   * [Amazon S3-Authentifizierung](../functionality/destination-configuration/customer-authentication.md#s3)
   * [Azure Blob](../functionality/destination-configuration/customer-authentication.md#blob)
   * [Azure Data Lake Storage](../functionality/destination-configuration/customer-authentication.md#adls)
   * [Google Cloud Storage](../functionality/destination-configuration/customer-authentication.md#gcs)
   * [SFTP-Authentifizierung mit SSH-Schlüssel](../functionality/destination-configuration/customer-authentication.md#sftp-ssh)
   * [SFTP-Authentifizierung mit Passwort](../functionality/destination-configuration/customer-authentication.md#sftp-password)

* Wenn Sie `"authenticationRule": "PLATFORM_AUTHENTICATION"` ausgewählt haben, lesen Sie die [Dokumentation zur Berechtigungskonfigurations-API](../credentials-api/create-credential-configuration.md#when-to-use).


## Schritt 5: Testen des Ziels {#test-destination}

Nachdem Sie das Ziel mit den Konfigurationsendpunkten in den vorherigen Schritten eingerichtet haben, können Sie das [Zieltest-Tool](../testing-api/batch-destinations/file-based-destination-testing-overview.md) verwenden, um die Integration zwischen Adobe Experience Platform und Ihrem Ziel zu testen.

Im Rahmen des Testvorgangs Ihres Ziels müssen Sie die Experience Platform-Benutzeroberfläche verwenden, um Zielgruppen zu erstellen, die Sie für Ihr Ziel aktivieren. Anweisungen zum Erstellen von Zielgruppen in Experience Platform finden Sie in den beiden folgenden Ressourcen:

* [Erstellen einer Audience - Dokumentationsseite](/help/segmentation/ui/audience-portal.md#create-audience)
* [Erstellen einer Zielgruppe - Videoanleitung](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=de)

## Schritt 6: Veröffentlichen des Ziels {#publish-destination}

>[!NOTE]
>
>Dieser Schritt ist nicht erforderlich, wenn Sie ein privates Ziel für Ihre eigene Verwendung erstellen und es nicht im Zielkatalog veröffentlichen möchten, damit andere Kundinnen und Kunden es verwenden können.

Verwenden Sie nach dem Konfigurieren und Testen Ihres Ziels die [Zielveröffentlichungs-API](../publishing-api/create-publishing-request.md), um Ihre Konfiguration zur Überprüfung an Adobe zu senden.

## Schritt 7: Dokumentieren des Ziels {#document-destination}

>[!NOTE]
>
>Dieser Schritt ist nicht erforderlich, wenn Sie ein privates Ziel für Ihre eigene Verwendung erstellen und es nicht im Zielkatalog veröffentlichen möchten, damit andere Kundinnen und Kunden es verwenden können.

Wenn Sie ein unabhängiger Software-Anbieter (ISV) oder Systemintegrator (SI) sind, der eine [produktbezogene Integration](../overview.md#productized-custom-integrations) erstellt, verwenden Sie den [Self-Service-Dokumentationsprozess](../docs-framework/documentation-instructions.md), um eine Produktdokumentationsseite für Ihr Ziel im [Experience Platform-Zielkatalog](/help/destinations/catalog/overview.md) zu erstellen.

## Schritt 8: Übermitteln des Ziels zur Überprüfung durch Adobe {#submit-for-review}

>[!NOTE]
>
>Dieser Schritt ist nicht erforderlich, wenn Sie ein privates Ziel für Ihre eigene Verwendung erstellen und es nicht im Zielkatalog veröffentlichen möchten, damit andere Kundinnen und Kunden es verwenden können.

Bevor das Ziel im Experience Platform-Katalog veröffentlicht und für alle Experience Platform-Kundinnen und -Kunden sichtbar werden kann, müssen Sie das Ziel schließlich offiziell zur Überprüfung durch Adobe übermitteln. Hier finden Sie vollständige Informationen zum [Einreichen eines in Destination SDK erstellten produktbezogenen Ziels zur Überprüfung](../guides/submit-destination.md).
