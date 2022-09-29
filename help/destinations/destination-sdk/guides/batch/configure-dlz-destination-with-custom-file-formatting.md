---
description: Erfahren Sie, wie Sie mit Destination SDK ein Data Landing Zone (DLZ)-Ziel mit benutzerdefinierten Dateiformatierungsoptionen und einer benutzerdefinierten Dateinamenkonfiguration konfigurieren können.
title: Konfigurieren Sie ein Data Landing Zone (DLZ)-Ziel mit benutzerdefinierten Dateiformatierungsoptionen und einer benutzerdefinierten Dateinamenkonfiguration.
exl-id: 3a5c1188-c2b5-4e81-ae41-9fff797f08a6
source-git-commit: 29962e07aa50c97b6098f4c892facf48508d28cf
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 10%

---

# Konfigurieren Sie eine [!DNL Data Landing Zone (DLZ)] Ziel mit benutzerdefinierten Dateiformatierungsoptionen und benutzerdefinierter Dateinamenkonfiguration

## Übersicht {#overview}

Auf dieser Seite wird beschrieben, wie Sie mit Destination SDK eine [!DNL Data Landing Zone] Ziel mit benutzerdefiniertem [Dateiformatierungsoptionen](../../server-and-file-configuration.md#file-configuration) und benutzerspezifische [Dateinamenkonfiguration](../../file-based-destination-configuration.md#file-name-configuration).

Auf dieser Seite werden alle verfügbaren Konfigurationsoptionen für [!DNL Data Landing Zone] Ziele. Sie können die in den folgenden Schritten angezeigten Konfigurationen bearbeiten oder bestimmte Teile der Konfigurationen nach Bedarf löschen.

## Voraussetzungen {#prerequisites}

Bevor Sie mit den unten beschriebenen Schritten fortfahren, lesen Sie bitte die [Erste Schritte mit Destination SDK](../../getting-started.md) Seite mit Informationen zum Abrufen der erforderlichen Anmeldeinformationen für die Adobe I/O-Authentifizierung und anderen Voraussetzungen für die Verwendung mit Destination SDK-APIs.

## Schritt 1: Erstellen einer Server- und Dateikonfiguration {#create-server-file-configuration}

Verwenden Sie zunächst die `/destination-server` -Endpunkt, um eine Server- und Dateikonfiguration zu erstellen. Eine ausführliche Beschreibung der Parameter in der HTTP-Anforderung finden Sie im Abschnitt [Server- und Dateikonfigurationsspezifikationen für dateibasierte Ziele](../../server-and-file-configuration.md#adls-example) und die zugehörigen [Dateiformatierungskonfigurationen](../../server-and-file-configuration.md#file-configuration).

**API-Format**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

**Anfrage**

Die folgende Anfrage erstellt eine neue Ziel-Server-Konfiguration, die durch die in der Payload bereitgestellten Parameter konfiguriert wird.
Die nachstehende Payload enthält eine generische [!DNL Data Landing Zone] Konfiguration mit benutzerdefinierter [CSV-Dateiformatierung](../../server-and-file-configuration.md#file-configuration) Konfigurationsparameter festlegen, die Benutzer in der Experience Platform-Benutzeroberfläche definieren können.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-server \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \ 
 -d '
{
   "name":"DLZ Destination Server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "fileConfigurations":{
         "compression":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.compression}}"
         },
         "fileType":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.fileType}}"
         },
         "csvOptions":{
            "sep":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.sep}}"
            },
            "encoding":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.encoding}}"
            },
            "quote":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.quote}}"
            },
            "quoteAll":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.quoteAll}}"
            },
            "escape":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.escape}}"
            },
            "escapeQuotes":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.escapeQuotes}}"
            },
            "header":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.header}}"
            },
            "ignoreLeadingWhiteSpace":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.ignoreLeadingWhiteSpace}}"
            },
            "nullValue":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.nullValue}}"
            },
            "dateFormat":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.dateFormat}}"
            },
            "charToEscapeQuoteEscaping":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.charToEscapeQuoteEscaping}}"
            },
            "emptyValue":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.dateFormat}}"
            }
         }
      }
   }
}'
```

Eine erfolgreiche Antwort gibt die neue Zielserverkonfiguration zurück, einschließlich der eindeutigen Kennung (`instanceId`) der Konfiguration. Speichern Sie diesen Wert, da er im nächsten Schritt erforderlich ist.

## Schritt 2: Erstellen einer Zielkonfiguration {#create-destination-configuration}

Nachdem Sie die Konfiguration des Zielservers und der Dateiformatierung im vorherigen Schritt erstellt haben, können Sie jetzt die `/destinations` API-Endpunkt zum Erstellen einer Zielkonfiguration.

So verbinden Sie die Serverkonfiguration in [Schritt 1](#create-server-file-configuration) ersetzen Sie die `destinationServerId` -Wert in der API-Anfrage unten mit dem Wert, der beim Erstellen Ihres Zielservers in [Schritt 1](#create-server-file-configuration).

Eine detaillierte Beschreibung der unten verwendeten Parameter finden Sie auf den folgenden Seiten:

* [Authentifizierungskonfiguration](../../authentication-configuration.md#adls)
* [Batch-Zielkonfiguration](../../file-based-destination-configuration.md#batch-configuration)
* [API-Vorgänge für die dateibasierte Zielkonfiguration](../../destination-configuration-api.md#create-file-based)

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
   "name":"DLZ Destination",
   "description":"SSD DLZ Destination",
   "releaseNotes":"Test release notes for DLZ Destination",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
       
   ],
   "customerEncryptionConfigurations":[
       
   ],
   "customerDataFields":[
      {
         "name":"path",
         "title":"Folder path",
         "description":"Enter the path to your Data Landing Zone folder",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"sep",
         "title":"Enter your desired separator for each field and value",
         "description":"Enter your desired separator for each field and value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"encoding",
         "title":"Select the desired CSV file encoding",
         "description":"Select the desired CSV file encoding",
         "type":"string",
         "enum":[
            "UTF-8",
            "UTF-16"
         ],
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quote",
         "title":"Quoted values escape character",
         "description":"Enter the desired character to be used for escaping quoted values.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quoteAll",
         "title":"Escape all quoted values",
         "description":"Select whether to escape all quoted values.",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "default":"true",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escape",
         "title":"Quote escaping character",
         "description":"Enter the desired character to be used for escaping quotes inside an already quoted value.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escapeQuotes",
         "title":"Enclose quoted values within quotes",
         "description":"Select whether values containing quotes should always be enclosed in quotes.",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "isRequired":false,
         "default":"true",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"header",
         "title":"Generate file header.",
         "description":"Select whether to write the names of columns as the first line of the exported files.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"ignoreLeadingWhiteSpace",
         "title":"Ignore leading white space",
         "description":"Select whether leading whitespaces should be trimmed from exported values.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"nullValue",
         "title":"NULL value string format",
         "description":"Enter the string representation of a NULL value. ",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"dateFormat",
         "title":"Date format",
         "description":"Enter the desired date format. ",
         "type":"string",
         "default":"yyyy-MM-dd",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"charToEscapeQuoteEscaping",
         "title":"Quote escaping escape character",
         "description":"Enter the desired character to be used for escaping the escaping of a quote character.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"emptyValue",
         "title":"Empty value string format",
         "description":"Enter the string representation of an empty value.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "default":"",
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
      "documentationLink":"https://www.adobe.io/apis/experienceplatform.html",
      "category":"DLZ",
      "connectionType":"Server-to-server",
      "frequency":"Batch",
      "flowRunsSupported":true,
      "monitoringSupported":true
   },
   "identityNamespaces":{
      "adobe_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "mobile_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false
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
         "authenticationRule":"NONE",
         "destinationServerId":"{{instanceID of your destination server}}"
      }
   ],
   "schemaConfig":{
      "profileRequired":true,
      "identityRequired":true,
      "segmentRequired":true
   },
   "batchConfig":{
      "allowMandatoryFieldSelection":true,
      "autoSelectJoinKeyOnPartnerSchemaSelection":false,
      "joinKeyTitle":"DEDUPLICATION KEY",
      "defaultExportMode":"DAILY_FULL_EXPORT",
      "allowedExportModes":[
         "DAILY_FULL_EXPORT",
         "FIRST_FULL_THEN_INCREMENTAL"
      ],
      "allowedScheduleFrequency":[
         "DAILY",
         "EVERY_3_HOURS",
         "EVERY_6_HOURS",
         "EVERY_12_HOURS",
         "EVERY_8_HOURS",
         "ONCE",
         "EVERY_HOUR"
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
      "allowDedupKeyFieldSelection":true
   },
   "backfillHistoricalProfileData":true
}'
```

Eine erfolgreiche Antwort gibt die neue Zielkonfiguration zurück, einschließlich der eindeutigen Kennung (`instanceId`) der Konfiguration. Notieren Sie sich diesen Wert, da er erforderlich ist, wenn Sie weitere HTTP-Anfragen stellen müssen, um Ihre Zielkonfiguration zu aktualisieren.

## Schritt 3: Überprüfen der Experience Platform-Benutzeroberfläche {#verify-ui}

Basierend auf den obigen Konfigurationen zeigt der Experience Platform-Katalog jetzt eine neue private Zielkarte an, die Sie verwenden können.

![Bildschirmaufzeichnung mit der Zielkatalogseite mit der ausgewählten Zielkarte.](../../assets/dlz-destination-card.gif)

Beachten Sie in den unten stehenden Bildern und Aufzeichnungen, wie die Optionen in der [Aktivierungs-Workflow für dateibasierte Ziele](/help/destinations/ui/activate-batch-profile-destinations.md) mit den Optionen übereinstimmen, die Sie in der Zielkonfiguration ausgewählt haben.

Beachten Sie beim Ausfüllen von Details zum Ziel, wie die angezeigten Felder die benutzerdefinierten Datenfelder sind, die Sie in der Konfiguration eingerichtet haben.

>[!TIP]
>
>Die Reihenfolge, in der Sie die benutzerdefinierten Datenfelder zur Zielkonfiguration hinzufügen, wird nicht in der Benutzeroberfläche angezeigt. Die benutzerdefinierten Datenfelder werden immer in der Reihenfolge angezeigt, die in der nachfolgenden Bildschirmaufzeichnung angezeigt wird.

![Zieldetails ausfüllen](../../assets/file-configuration-options.gif)

Beachten Sie bei der Planung von Exportintervallen, dass die angezeigten Felder die Felder sind, die Sie in der `batchConfig` Konfiguration.
![Planungsoptionen für Exporte](../../assets/file-export-scheduling.png)

Beachten Sie bei der Anzeige der Konfigurationsoptionen für Dateinamen, wie die angezeigten Felder die `filenameConfig` -Optionen, die Sie in der Konfiguration eingerichtet haben.
![Konfigurationsoptionen für Dateinamen](../../assets/file-naming-options.gif)

Wenn Sie eines der oben genannten Felder anpassen möchten, wiederholen Sie [Schritt 1](#create-server-file-configuration) und [two](#create-destination-configuration) um die Konfigurationen nach Bedarf zu ändern.

## Schritt 4: (Optional) Veröffentlichen Sie Ihr Ziel {#publish-destination}

>[!NOTE]
>
>Dieser Schritt ist nicht erforderlich, wenn Sie ein privates Ziel für Ihre eigene Verwendung erstellen und es nicht im Zielkatalog veröffentlichen möchten, damit andere Kunden ihn verwenden können.

Nachdem Sie Ihr Ziel konfiguriert haben, verwenden Sie die [Zielpublikations-API](../../destination-publish-api.md) , um Ihre Konfiguration zur Überprüfung an Adobe zu senden.

## Schritt 5: (Optional) Dokument Ihres Ziels {#document-destination}

>[!NOTE]
>
>Dieser Schritt ist nicht erforderlich, wenn Sie ein privates Ziel für Ihre eigene Verwendung erstellen und es nicht im Zielkatalog veröffentlichen möchten, damit andere Kunden ihn verwenden können.

Wenn Sie ein unabhängiger Software-Anbieter (ISV) oder Systemintegrator (SI) sind, der eine [produktbezogene Integration](../../overview.md#productized-custom-integrations) erstellt, verwenden Sie den [Self-Service-Dokumentationsprozess](../../docs-framework/documentation-instructions.md), um eine Produktdokumentationsseite für Ihr Ziel im [Experience Platform-Zielkatalog](../../../catalog/overview.md) zu erstellen.

## Nächste Schritte {#next-steps}

Durch Lesen dieses Artikels wissen Sie jetzt, wie Sie eine benutzerdefinierte [!DNL Data Landing Zone] Ziel mithilfe von Destination SDK. Als Nächstes kann Ihr Team die [Aktivierungs-Workflow für dateibasierte Ziele](../../../ui/activate-batch-profile-destinations.md) , um Daten an das Ziel zu exportieren.
