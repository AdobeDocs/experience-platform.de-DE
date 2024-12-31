---
description: Erfahren Sie, wie Sie Destination SDK verwenden, um ein Azure Blob Storage-Ziel mit benutzerdefinierten Dateiformatierungsoptionen und benutzerdefinierter Dateinamenkonfiguration zu konfigurieren.
title: Konfigurieren eines Azure Blob Storage-Ziels mit benutzerdefinierten Dateiformatierungsoptionen und benutzerdefinierter Dateinamenkonfiguration.
exl-id: effbd218-3a7c-4986-9fba-f5727a21e480
source-git-commit: d47c82339afa602a9d6914c1dd36a4fc9528ea32
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 8%

---

# Konfigurieren eines [!DNL Azure Blob Storage] Ziels mit benutzerdefinierten Dateiformatierungsoptionen und benutzerdefinierter Dateinamenkonfiguration

## Übersicht {#overview}

Auf dieser Seite wird beschrieben, wie Sie mit Destination SDK ein [!DNL Azure Blob Storage]-Ziel mit benutzerdefinierten [Dateiformatierungsoptionen](configure-file-formatting-options.md) und einer benutzerdefinierten [Dateinamenkonfiguration](../../functionality/destination-configuration/batch-configuration.md#file-name-configuration) konfigurieren.

Auf dieser Seite werden alle Konfigurationsoptionen angezeigt, die für Azure Blob Storage-Ziele verfügbar sind. Sie können die in den folgenden Schritten angezeigten Konfigurationen bearbeiten oder bestimmte Teile der Konfigurationen nach Bedarf löschen.

Detaillierte Beschreibungen der unten verwendeten Parameter finden Sie unter [Konfigurationsoptionen in Destinations SDK](../../functionality/configuration-options.md).

## Voraussetzungen {#prerequisites}

Bevor Sie mit den unten beschriebenen Schritten fortfahren, informieren Sie sich auf der Seite [Erste Schritte ](../../getting-started.md) Destination SDK , wie Sie die erforderlichen Adobe I/O-Authentifizierungsdaten und andere Voraussetzungen für die Arbeit mit Destination SDK-APIs erhalten.

## Schritt 1: Erstellen einer Server- und Dateikonfiguration {#create-server-file-configuration}

Verwenden Sie zunächst den `/destination-server`-Endpunkt, um [eine Server- und Dateikonfiguration zu erstellen](../../authoring-api/destination-server/create-destination-server.md).

**API-Format**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

**Anfrage**

Die folgende Anfrage erstellt eine neue Ziel-Server-Konfiguration, die durch die in der Payload bereitgestellten Parameter konfiguriert wird.
Die nachstehende Payload enthält eine generische Azure Blob-Konfiguration mit benutzerdefinierter [CSV-Dateiformatierung](../../functionality/destination-server/file-formatting.md)-Konfigurationsparametern, die Benutzerinnen und Benutzer in der Experience Platform-Benutzeroberfläche definieren können.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-server \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \ 
 -d '
{
   "name":"Azure Blob server with custom file formatting options and custom file name configuration",
   "description":"Azure Blob server with custom file formatting options and custom file name configuration",
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
}'
```

Eine erfolgreiche Antwort gibt die neue Ziel-Server-Konfiguration zurück, einschließlich der eindeutigen Kennung (`instanceId`) der Konfiguration. Speichern Sie diesen Wert, da er im nächsten Schritt erforderlich ist.

## Schritt 2: Erstellen einer Zielkonfiguration {#create-destination-configuration}

Nachdem Sie im vorherigen Schritt die Ziel-Server- und Dateiformatierungskonfiguration erstellt haben, können Sie jetzt den API-Endpunkt `/destinations` verwenden, um eine Zielkonfiguration zu erstellen.

Um die Server-Konfiguration in [Schritt 1](#create-server-file-configuration) mit dieser Zielkonfiguration zu verbinden, ersetzen Sie den `destinationServerId` in der unten stehenden API-Anfrage mit dem Wert, der beim Erstellen Ihres Ziel-Servers in [Schritt 1](#create-server-file-configuration) erhalten wurde.

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
 -d ' {
   "name":"Azure Blob Storage destination with custom file formatting options and custom file name configuration",
   "description":"Azure Blob Storage destination with custom file formatting options and custom file name configuration",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"AZURE_CONNECTION_STRING"
      }
   ],
   "customerDataFields":[
      {
         "name":"path",
         "title":"Folder path",
         "description":"Enter your Azure Blob folder path",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"container",
         "title":"Azure Blob container name",
         "description":"Enter your Azure Blob container name",
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
      "documentationLink":"https://www.adobe.com/go/destinations-blob-connection-parameters-en",
      "category":"cloudStorage",
      "connectionType":"Azure Blob",
      "frequency":"Batch",
      "flowRunsSupported":true,
      "monitoringSupported":true
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
         "destinationServerId":"{{instanceID of your destination server}}"
      }
   ],
   "schemaConfig":{
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "batchConfig":{
      "allowMandatoryFieldSelection":true,
      "allowJoinKeyFieldSelection":true,
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
      "backfillHistoricalProfileData":true
   }
}'
```

Eine erfolgreiche Antwort gibt die neue Zielkonfiguration zurück, einschließlich der eindeutigen Kennung (`instanceId`) der Konfiguration. Speichern Sie diesen Wert, da er erforderlich ist, wenn Sie weitere HTTP-Anfragen zur Aktualisierung Ihrer Zielkonfiguration durchführen müssen.

## Schritt 3: Überprüfen der Experience Platform-Benutzeroberfläche {#verify-ui}

Basierend auf den oben genannten Konfigurationen wird im Experience Platform-Katalog jetzt eine neue private Zielkarte angezeigt, die Sie verwenden können.

![Bildschirmaufzeichnung, die die Zielkatalogseite mit einer ausgewählten Zielkarte anzeigt.](../../assets/guides/batch/blob-destination-card.gif)

Beachten Sie in den folgenden Bildern und Aufzeichnungen, wie die [ im Aktivierungs-Workflow für dateibasierte Ziele ](/help/destinations/ui/activate-batch-profile-destinations.md) den Optionen übereinstimmen, die Sie in der Zielkonfiguration ausgewählt haben.

Beachten Sie beim Ausfüllen von Details zum Ziel, wie die Felder die benutzerdefinierten Datenfelder sind, die Sie in der Konfiguration eingerichtet haben.

>[!TIP]
>
>Die Reihenfolge, in der Sie die benutzerdefinierten Datenfelder zur Zielkonfiguration hinzufügen, wird nicht in der Benutzeroberfläche angezeigt. Die benutzerdefinierten Datenfelder werden immer in der Reihenfolge angezeigt, die in der folgenden Bildschirmaufzeichnung angezeigt wird.

![Ausfüllen der Zieldetails](../../assets/guides/batch/file-configuration-options.gif)

Beachten Sie bei der Planung von Exportintervallen, wie die Felder angezeigt werden, die Sie in der `batchConfig`-Konfiguration einrichten.
![Exportplanoptionen](../../assets/guides/batch/file-export-scheduling.png)

Beachten Sie beim Anzeigen der Konfigurationsoptionen für Dateinamen, wie die angezeigten Felder die `filenameConfig` Optionen darstellen, die Sie in der Konfiguration festgelegt haben.
![Konfigurationsoptionen für Dateinamen](../../assets/guides/batch/file-naming-options.gif)

Wenn Sie eines der oben genannten Felder anpassen möchten, wiederholen Sie [Schritte 1](#create-server-file-configuration) und [2](#create-destination-configuration), um die Konfigurationen entsprechend Ihren Anforderungen zu ändern.

## Schritt 4: (Optional) Publish - Ihr Ziel {#publish-destination}

>[!NOTE]
>
>Dieser Schritt ist nicht erforderlich, wenn Sie ein privates Ziel für Ihre eigene Verwendung erstellen und es nicht im Zielkatalog veröffentlichen möchten, damit andere Kundinnen und Kunden es verwenden können.

Verwenden Sie nach dem Konfigurieren Ihres Ziels die [Zielveröffentlichungs-API](../../publishing-api/create-publishing-request.md), um Ihre Konfiguration zur Überprüfung an Adobe zu senden.

## Schritt 5: (Optional) Dokumentieren des Ziels {#document-destination}

>[!NOTE]
>
>Dieser Schritt ist nicht erforderlich, wenn Sie ein privates Ziel für Ihre eigene Verwendung erstellen und es nicht im Zielkatalog veröffentlichen möchten, damit andere Kundinnen und Kunden es verwenden können.

Wenn Sie ein unabhängiger Software-Anbieter (ISV) oder Systemintegrator (SI) sind, der eine [produktbezogene Integration](../../overview.md#productized-custom-integrations) erstellt, verwenden Sie den [Self-Service-Dokumentationsprozess](../../docs-framework/documentation-instructions.md), um eine Produktdokumentationsseite für Ihr Ziel im [Experience Platform-Zielkatalog](../../../catalog/overview.md) zu erstellen.

## Nächste Schritte {#next-steps}

Durch das Lesen dieses Artikels wissen Sie jetzt, wie Sie mithilfe von Destination SDK ein benutzerdefiniertes [!DNL Azure Blob Storage] erstellen können. Als Nächstes kann Ihr Team den [Aktivierungs-Workflow für dateibasierte Ziele“ verwenden](../../../ui/activate-batch-profile-destinations.md) um Daten an das Ziel zu exportieren.
