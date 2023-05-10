---
description: Erfahren Sie, wie Sie mit Destination SDK ein SFTP-Ziel mit vordefinierten Dateiformatierungsoptionen und einer benutzerdefinierten Dateinamenkonfiguration konfigurieren.
title: Konfigurieren eines SFTP-Ziels mit vordefinierten Dateiformatierungsoptionen und benutzerdefinierter Dateinamenkonfiguration.
exl-id: 6e0fe019-7fbb-48e4-9469-6cc7fc3cb6e4
source-git-commit: bdeebca9608e7c1ff3ae0cb1aeb444dccb78028f
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 14%

---

# Konfigurieren eines SFTP-Ziels mit vordefinierten Dateiformatierungsoptionen und benutzerdefinierter Dateinamenkonfiguration

## Übersicht {#overview}

Auf dieser Seite wird beschrieben, wie Sie mit Destination SDK ein SFTP-Ziel mit vordefinierten, standardmäßigen [Dateiformatierungsoptionen](../../server-and-file-configuration.md#file-configuration) und benutzerspezifische [Dateinamenkonfiguration](../../file-based-destination-configuration.md#file-name-configuration).

Auf dieser Seite werden alle für SFTP-Ziele verfügbaren Konfigurationsoptionen angezeigt. Sie können die in den folgenden Schritten angezeigten Konfigurationen bearbeiten oder bestimmte Teile der Konfigurationen nach Bedarf löschen.

## Voraussetzungen {#prerequisites}

Bevor Sie mit den unten beschriebenen Schritten fortfahren, lesen Sie bitte die [Erste Schritte mit Destination SDK](../../getting-started.md) Seite mit Informationen zum Abrufen der erforderlichen Anmeldeinformationen für die Adobe I/O-Authentifizierung und anderen Voraussetzungen für die Verwendung mit Destination SDK-APIs.

## Schritt 1: Erstellen einer Server- und Dateikonfiguration {#create-server-file-configuration}

Verwenden Sie zunächst die `/destination-server` -Endpunkt, um eine Server- und Dateikonfiguration zu erstellen. Eine ausführliche Beschreibung der Parameter in der HTTP-Anforderung finden Sie im Abschnitt [Server- und Dateikonfigurationsspezifikationen für dateibasierte Ziele](../../server-and-file-configuration.md#sftp-example) und die zugehörigen [Dateiformatierungskonfigurationen](../../server-and-file-configuration.md#file-configuration).

**API-Format**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

**Anfrage**

Die folgende Anfrage erstellt eine neue Ziel-Server-Konfiguration, die durch die in der Payload bereitgestellten Parameter konfiguriert wird.
Die nachstehende Payload enthält eine allgemeine SFTP-Konfiguration mit vordefinierter Standardkonfiguration [CSV-Dateiformatierung](../../server-and-file-configuration.md#file-configuration) Konfigurationsparameter festlegen, die Benutzer in der Experience Platform-Benutzeroberfläche definieren können.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-server \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "name": "SFTP destination with predefined CSV formatting options",
    "destinationServerType": "FILE_BASED_SFTP",
    "fileBasedSFTPDestination": {
        "hostname": {
            "templatingStrategy": "NONE",
            "value": "{{customerData.hostname}}"
        },
        "rootDirectory": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.remotePath}}"
        },
        "port": 22
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

So verbinden Sie die Serverkonfiguration in [Schritt 1](#create-server-file-configuration) ersetzen Sie die `destinationServerId` -Wert in der API-Anfrage unten mit dem Wert, der beim Erstellen Ihres Zielservers in [Schritt 1](#create-server-file-configuration).

Eine detaillierte Beschreibung der unten verwendeten Parameter finden Sie auf den folgenden Seiten:

* [Authentifizierungskonfiguration](../../authentication-configuration.md#sftp)
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
   "name":"SFTP destination with predefined CSV formatting options",
   "description":"SFTP destination with predefined CSV formatting options",
   "releaseNotes":"",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"SFTP_WITH_PASSWORD"
      },
      {
         "authType":"SFTP_WITH_SSH_KEY"
      }
   ],
   "customerEncryptionConfigurations":[
       
   ],
   "customerDataFields":[
      {
         "name":"remotePath",
         "title":"Root directory",
         "description":"Enter root directory",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"hostname",
         "title":"Hostname",
         "description":"Enter hostname",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-sftp-en",
      "category":"SFTP",
      "connectionType":"SFTP",
      "monitoringSupported":true,
      "flowRunsSupported":true,
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

Basierend auf den obigen Konfigurationen zeigt der Experience Platform-Katalog jetzt eine neue private Zielkarte an, die Sie verwenden können.

![Bildschirmaufzeichnung mit der Zielkatalogseite mit der ausgewählten Zielkarte.](../../assets/destination-card.gif)

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

Durch Lesen dieses Artikels wissen Sie jetzt, wie Sie ein benutzerdefiniertes SFTP-Ziel mithilfe von Destination SDK erstellen können. Als Nächstes kann Ihr Team die [Aktivierungs-Workflow für dateibasierte Ziele](../../../ui/activate-batch-profile-destinations.md) , um Daten an das Ziel zu exportieren.
