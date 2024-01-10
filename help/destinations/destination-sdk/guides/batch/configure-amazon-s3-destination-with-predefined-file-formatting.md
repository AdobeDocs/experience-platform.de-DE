---
description: Erfahren Sie, wie Sie mit Destination SDK ein Amazon S3-Ziel mit vordefinierten Dateiformatierungsoptionen und einer benutzerdefinierten Dateinamenkonfiguration konfigurieren.
title: Konfigurieren Sie ein Amazon S3-Ziel mit vordefinierten Dateiformatierungsoptionen und einer benutzerdefinierten Dateinamenkonfiguration.
exl-id: 0ecd3575-dcda-4e5c-af5c-247d4ea13fa1
source-git-commit: 45ba0db386f065206f89ed30bfe7b0c1b44f6173
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 8%

---

# Konfigurieren Sie eine [!DNL Amazon S3] Ziel mit vordefinierten Dateiformatierungsoptionen und benutzerdefinierter Dateinamenkonfiguration

## Übersicht {#overview}

Auf dieser Seite wird beschrieben, wie Sie mit Destination SDK ein Amazon S3-Ziel mit vordefinierten, standardmäßigen [Dateiformatierungsoptionen](configure-file-formatting-options.md) und benutzerspezifische [Dateinamenkonfiguration](../../functionality/destination-configuration/batch-configuration.md#file-name-configuration).

Auf dieser Seite werden alle verfügbaren Konfigurationsoptionen für [!DNL Amazon S3] Ziele. Sie können die in den folgenden Schritten angezeigten Konfigurationen bearbeiten oder bestimmte Teile der Konfigurationen nach Bedarf löschen.

Detaillierte Beschreibungen der unten verwendeten Parameter finden Sie unter [Konfigurationsoptionen im Ziel-SDK](../../functionality/configuration-options.md).

## Voraussetzungen {#prerequisites}

Bevor Sie mit den unten beschriebenen Schritten fortfahren, lesen Sie bitte die [Erste Schritte mit Destination SDK](../../getting-started.md) Seite mit Informationen zum Abrufen der erforderlichen Adobe I/O-Authentifizierungsberechtigungen und anderen Voraussetzungen für die Verwendung mit Destination SDK-APIs.

## Schritt 1: Erstellen einer Server- und Dateikonfiguration {#create-server-file-configuration}

Verwenden Sie zunächst die `/destination-server` Endpunkt zu [Erstellen einer Server- und Dateikonfiguration](../../authoring-api/destination-server/create-destination-server.md).

**API-Format**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

**Anfrage**

Die folgende Anfrage erstellt eine neue Zielserverkonfiguration, die durch die in der Payload bereitgestellten Parameter konfiguriert wird.
Die nachstehende Payload enthält eine generische [!DNL Amazon S3] Konfiguration mit vordefinierter Standardkonfiguration [CSV-Dateiformatierung](../../functionality/destination-server/file-formatting.md) Konfigurationsparameter, die Benutzer in der Experience Platform-Benutzeroberfläche definieren können.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-server \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "name": "Amazon S3 destination server with predefined default CSV options",
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
}'
```

Eine erfolgreiche Antwort gibt die neue Zielserverkonfiguration zurück, einschließlich der eindeutigen Kennung (`instanceId`) der Konfiguration. Speichern Sie diesen Wert, da er im nächsten Schritt erforderlich ist.

## Schritt 2: Erstellen einer Zielkonfiguration {#create-destination-configuration}

Nachdem Sie die Konfiguration des Zielservers und der Dateiformatierung im vorherigen Schritt erstellt haben, können Sie jetzt die `/destinations` API-Endpunkt zum Erstellen einer Zielkonfiguration.

So verbinden Sie die Serverkonfiguration in [Schritt 1](#create-server-file-configuration) in diese Zielkonfiguration eingeben, ersetzen Sie die `destinationServerId` -Wert in der API-Anfrage unten mit der `instanceId` Wert, der beim Erstellen des Zielservers in [Schritt 1](#create-server-file-configuration).

**API-Format**

```http
POST platform.adobe.io/data/core/activation/authoring/destinations
```

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Amazon S3 destination with predefined CSV formatting options",
   "description":"Amazon S3 destination with predefined CSV formatting options",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
   ],
   "customerEncryptionConfigurations":[
       
   ],
   "customerDataFields":[
      {
         "name":"bucketName",
         "title":"Enter the name of your Amazon S3 bucket",
         "description":"Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "pattern": "(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Enter the path to your S3 bucket folder",
         "description":"Enter the path to your S3 bucket folder",
         "type":"string",
         "isRequired":true,
         "pattern": "^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"compression",
         "title":"Compression format",
         "description":"Select the desired file compression format.",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "enum":[
            "SNAPPY",
            "GZIP",
            "DEFLATE",
            "NONE"
         ]
      },
      {
         "name":"fileType",
         "title":"File type",
         "description":"Select the exported file type.",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false,
         "enum":[
            "csv",
            "json",
            "parquet"
         ],
         "default":"csv"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-amazon-s3-en",
      "category":"cloudStorage",
      "icon":{
         "key":"amazonS3"
      },
      "connectionType":"S3",
      "flowRunsSupported":true,
      "monitoringSupported":true,
      "frequency":"Batch"
   },
   "destinationDelivery":[
      {
         "deliveryMatchers":[
            {
               "type":"SOURCE",
               "value":[
                  "batch"
               ]
            }
         ],
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ],
   "schemaConfig":{
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "batchConfig":{
      "allowMandatoryFieldSelection":true,
      "allowDedupeKeyFieldSelection":true,
      "defaultExportMode":"DAILY_FULL_EXPORT",
      "allowedExportMode":[
         "DAILY_FULL_EXPORT",
         "FIRST_FULL_THEN_INCREMENTAL"
      ],
      "allowedScheduleFrequency":[
         "DAILY",
         "EVERY_3_HOURS",
         "EVERY_6_HOURS",
         "EVERY_8_HOURS",
         "EVERY_12_HOURS",
         "ONCE"
      ],
      "defaultFrequency":"DAILY",
      "defaultStartTime":"00:00",
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
      },
      "backfillHistoricalProfileData":true
   }
}'
```

Eine erfolgreiche Antwort gibt die neue Zielkonfiguration zurück, einschließlich der eindeutigen Kennung (`instanceId`) der Konfiguration. Notieren Sie sich diesen Wert, da er erforderlich ist, wenn Sie weitere HTTP-Anfragen stellen müssen, um Ihre Zielkonfiguration zu aktualisieren.

## Schritt 3: Überprüfen der Experience Platform-Benutzeroberfläche {#verify-ui}

Basierend auf den obigen Konfigurationen zeigt der Experience Platform-Katalog nun eine neue private Zielkarte an, die Sie verwenden können.

![Bildschirmaufzeichnung mit der Zielkatalogseite mit der ausgewählten Zielkarte.](../../assets/guides/batch/destination-card.gif)

Beachten Sie in den unten stehenden Bildern und Aufzeichnungen, wie die Optionen in der [Aktivierungs-Workflow für dateibasierte Ziele](../../../ui/activate-batch-profile-destinations.md) entsprechen den Optionen, die Sie in der Zielkonfiguration ausgewählt haben.

Beachten Sie beim Ausfüllen von Details zum Ziel, wie die angezeigten Felder die benutzerdefinierten Datenfelder sind, die Sie in der Konfiguration eingerichtet haben.

>[!TIP]
>
>Die Reihenfolge, in der Sie die benutzerdefinierten Datenfelder zur Zielkonfiguration hinzufügen, wird nicht in der Benutzeroberfläche angezeigt. Die Kundendatenfelder werden immer in der Reihenfolge angezeigt, die in der unten stehenden Bildschirmaufzeichnung angezeigt wird.

![Bildschirmaufzeichnung, die die in Ihrer Konfiguration definierten Kundendatenfelder anzeigt.](../../assets/guides/batch/file-configuration-options.gif)

Beachten Sie bei der Planung von Exportintervallen, dass die angezeigten Felder die Felder sind, die Sie in der `batchConfig` Konfiguration.
![Planungsoptionen für Exporte](../../assets/guides/batch/file-export-scheduling.png)

Beachten Sie bei der Anzeige der Konfigurationsoptionen für Dateinamen, wie die angezeigten Felder die `filenameConfig` -Optionen, die Sie in der -Konfiguration eingerichtet haben.
![Konfigurationsoptionen für Dateinamen](../../assets/guides/batch/file-naming-options.gif)

Wenn Sie eines der oben genannten Felder anpassen möchten, wiederholen Sie [Schritt 1](#create-server-file-configuration) und [two](#create-destination-configuration) um die Konfigurationen nach Bedarf zu ändern.

## Schritt 4: (Optional) Ziel veröffentlichen {#publish-destination}

>[!NOTE]
>
>Dieser Schritt ist nicht erforderlich, wenn Sie ein privates Ziel für Ihre eigene Verwendung erstellen und es nicht im Zielkatalog veröffentlichen möchten, damit andere Kunden ihn verwenden können.

Nachdem Sie Ihr Ziel konfiguriert haben, verwenden Sie die [Zielpublikations-API](../../publishing-api/create-publishing-request.md) , um Ihre Konfiguration zur Überprüfung an Adobe zu senden.

## Schritt 5: (Optional) Ziel dokumentieren {#document-destination}

>[!NOTE]
>
>Dieser Schritt ist nicht erforderlich, wenn Sie ein privates Ziel für Ihre eigene Verwendung erstellen und es nicht im Zielkatalog veröffentlichen möchten, damit andere Kunden ihn verwenden können.

Wenn Sie ein unabhängiger Software-Anbieter (ISV) oder Systemintegrator (SI) sind, der eine [produktbezogene Integration](../../overview.md#productized-custom-integrations) erstellt, verwenden Sie den [Self-Service-Dokumentationsprozess](../../docs-framework/documentation-instructions.md), um eine Produktdokumentationsseite für Ihr Ziel im [Experience Platform-Zielkatalog](../../../catalog/overview.md) zu erstellen.

## Nächste Schritte {#next-steps}

Durch Lesen dieses Artikels wissen Sie jetzt, wie Sie eine benutzerdefinierte [!DNL Amazon S3] Ziel mithilfe von Destination SDK. Als Nächstes kann Ihr Team die [Aktivierungs-Workflow für dateibasierte Ziele](../../../ui/activate-batch-profile-destinations.md) , um Daten an das Ziel zu exportieren.
