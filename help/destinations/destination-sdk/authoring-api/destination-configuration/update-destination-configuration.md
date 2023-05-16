---
description: Auf dieser Seite wird der API-Aufruf veranschaulicht, mit dem eine bestehende Zielkonfiguration über Adobe Experience Platform Destination SDK aktualisiert wird.
title: Zielkonfiguration aktualisieren
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 28%

---


# Zielkonfiguration aktualisieren

Auf dieser Seite werden die API-Anfrage und die Payload erläutert, die Sie verwenden können, um eine vorhandene Zielkonfiguration mithilfe der `/authoring/destinations` API-Endpunkt.

>[!TIP]
>
>Jeder Aktualisierungsvorgang für produktive/öffentliche Ziele ist erst sichtbar, nachdem Sie die [Publishing-API](../../publishing-api/create-publishing-request.md) und senden Sie die Aktualisierung zur Überprüfung der Adobe.

Eine ausführliche Beschreibung der Funktionen einer Zielkonfiguration finden Sie in den folgenden Artikeln:

* [Konfiguration der Kundenauthentifizierung](../../functionality/destination-configuration/customer-authentication.md)
* [OAuth 2-Authentifizierung](../../functionality/destination-configuration/oauth2-authentication.md)
* [Benutzerdefinierte Datenfelder](../../functionality/destination-configuration/customer-data-fields.md)
* [Benutzeroberflächenattribute](../../functionality/destination-configuration/ui-attributes.md)
* [Schemakonfiguration](../../functionality/destination-configuration/schema-configuration.md)
* [Identitäts-Namespace-Konfiguration](../../functionality/destination-configuration/identity-namespace-configuration.md)
* [Zielbereitstellung](../../functionality/destination-configuration/destination-delivery.md)
* [Konfiguration von Zielgruppen-Metadaten](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [Konfiguration von Zielgruppen-Metadaten](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [Aggregationsrichtlinie](../../functionality/destination-configuration/aggregation-policy.md)
* [Batch-Konfiguration](../../functionality/destination-configuration/batch-configuration.md)
* [Historische Profilqualifikationen](../../functionality/destination-configuration/historical-profile-qualifications.md)

>[!IMPORTANT]
>
>Alle von Destination SDK unterstützten Parameternamen und Werte sind **Groß-/Kleinschreibung**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Erste Schritte mit API-Vorgängen zur Zielkonfiguration {#get-started}

Bevor Sie fortfahren, lesen Sie [Erste Schritte](../../getting-started.md). Dort finden Sie die nötigen Informationen für den erfolgreichen Aufruf der API, einschließlich Details für den Abruf der erforderlichen Authoring-Berechtigung für Ziele und zu den erforderlichen Kopfzeilen.

## Zielkonfiguration aktualisieren {#update}

Sie können eine [vorhandene](create-destination-configuration.md) Zielkonfiguration durch `PUT` Anfrage an `/authoring/destinations` -Endpunkt mit der aktualisierten Payload.

>[!TIP]
>
>API-Endpunkt: `platform.adobe.io/data/core/activation/authoring/destinations`

So rufen Sie eine vorhandene Zielkonfiguration und die zugehörigen `{INSTANCE_ID}`, siehe Artikel zu [Abrufen einer Zielkonfiguration](retrieve-destination-configuration.md).

**API-Format**

```http
PUT /authoring/destinations/{INSTANCE_ID}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{INSTANCE_ID}` | Die ID der Zielkonfiguration, die Sie aktualisieren möchten. So rufen Sie eine vorhandene Zielkonfiguration und die zugehörigen `{INSTANCE_ID}`, siehe [Abrufen einer Zielkonfiguration](retrieve-destination-configuration.md). |

+++Anfrage

Die folgende Anfrage aktualisiert das Ziel, das wir in erstellt haben [Dieses Beispiel](create-destination-configuration.md#create) mit verschiedenen `filenameConfig` Optionen.

```shell {line-numbers="true" highlight="115-128"}
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/{INSTANCE_ID} \
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
         "name":"bucket",
         "title":"Enter the name of your Amazon S3 bucket",
         "description":"Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Enter the path to your S3 bucket folder",
         "description":"Enter the path to your S3 bucket folder",
         "type":"string",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$",
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
         "ONCE"
      ],
      "defaultFrequency":"DAILY",
      "defaultStartTime":"00:00",
      "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%_%DESTINATION_INSTANCE_ID%,"
      },
      "backfillHistoricalProfileData":true
   }
}'
```

+++

+++Antwort

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit den Details Ihrer aktualisierten Zielkonfiguration zurück.

+++

## Umgang mit API-Fehlern {#error-handling}

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status-Codes](../../../../landing/troubleshooting.md#api-status-codes) und [Fehler im Anfrage-Header](../../../../landing/troubleshooting.md#request-header-errors) in der Anleitung zur Fehlerbehebung für Platform.

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie eine Zielkonfiguration über die Destination SDK aktualisieren können `/authoring/destinations` API-Endpunkt.

Weitere Informationen dazu, was Sie mit diesem Endpunkt tun können, finden Sie in den folgenden Artikeln:

* [Erstellen einer Zielkonfiguration](create-destination-configuration.md)
* [Abrufen einer Zielkonfiguration](retrieve-destination-configuration.md)
* [Zielkonfiguration löschen](delete-destination-configuration.md)