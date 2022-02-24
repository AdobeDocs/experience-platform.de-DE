---
description: Mit dieser Konfiguration können Sie grundlegende Informationen wie Zielname, Kategorie, Beschreibung, Logo und mehr angeben. Die Einstellungen in dieser Konfiguration bestimmen auch, wie Experience Platform-Benutzer sich bei Ihrem Ziel authentifizieren, wie es in der Experience Platform-Benutzeroberfläche angezeigt wird und welche Identitäten an Ihr Ziel exportiert werden können.
title: (Beta) Dateibasierte Zielkonfigurationsoptionen für die Destination SDK
source-git-commit: 5186e90b850f1e75ec358fa01bfb8a5edac29277
workflow-type: tm+mt
source-wordcount: '1899'
ht-degree: 7%

---

# (Beta) Dateibasierte Zielkonfiguration {#destination-configuration}

## Übersicht {#overview}

>[!IMPORTANT]
>
>Die dateibasierte Zielunterstützung in Adobe Experience Platform Destination SDK ist derzeit als Beta-Version verfügbar. Dokumentation und Funktionalität können sich ändern.

Mit dieser Konfiguration können Sie wichtige Informationen für Ihr dateibasiertes Ziel angeben, z. B. Ihren Zielnamen, Ihre Kategorie, eine Beschreibung und mehr. Die Einstellungen in dieser Konfiguration bestimmen auch, wie Experience Platform-Benutzer sich bei Ihrem Ziel authentifizieren, wie es in der Experience Platform-Benutzeroberfläche angezeigt wird und welche Identitäten an Ihr Ziel exportiert werden können.

Diese Konfiguration verbindet auch die anderen Konfigurationen, die erforderlich sind, damit Ihr Ziel funktioniert - Zielserver und Zielgruppen-Metadaten - mit dieser Konfiguration. Erfahren Sie, wie Sie auf die beiden Konfigurationen in einer [Abschnitt weiter unten](./destination-configuration.md#connecting-all-configurations).

Sie können die in diesem Dokument beschriebenen Funktionen mithilfe der `/authoring/destinations` API-Endpunkt. Lesen [API-Endpunktvorgänge für Ziele](./destination-configuration-api.md) für eine vollständige Liste der Vorgänge, die Sie am -Endpunkt ausführen können.

## Beispiel für eine Amazon S3-Zielkonfiguration {#batch-example-configuration}

```json
{
   "name":"S3 Destination with CSV Options",
   "description":"S3 Destination with CSV Options",
   "status":"TEST",
   "maxProfileAttributes": "2000",
   "maxIdentityAttributes": "10",
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
   ],
   "customerEncryptionConfigurations":[],
   "customerDataFields":[
      {
         "name":"bucket",
         "title":"Amazon S3 bucket name",
         "description":"Enter your Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Amazon S3 bucket path",
         "description":"Enter your S3 bucket path",
         "type":"string",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"sep",
         "title":"Enter a separator for each field and value",
         "description":"Enter a separator character for each field and value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"encoding",
         "title":"Specify encoding (charset) of saved CSV files",
         "description":"Select encoding of csv files",
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
         "title":"Select a single character used for escaping quoted values",
         "description":"Select single charachter for escaping quoted values",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quoteAll",
         "title":"Escape all quoted values",
         "description":"Select whether to escape all quoted values",
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
         "title":"Select a single character used for escaping quotes",
         "description":"Select a single character used for escaping quotes inside an already quoted value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escapeQuotes",
         "title":"Escape quotes",
         "description":"A flag indicating whether values containing quotes should always be enclosed in quotes",
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
         "title":"header",
         "description":"Writes the names of columns as the first line.",
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
         "description":"A flag indicating whether or not leading whitespaces from values being written should be skipped.",
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
         "title":"Select the string representation of a null value",
         "description":"Sets the string representation of a null value. ",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"dateFormat",
         "title":"Date format",
         "description":"Select the string that indicates a date format. ",
         "type":"string",
         "default":"yyyy-MM-dd",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"charToEscapeQuoteEscaping",
         "title":"Char to escape quote escaping",
         "description":"Sets a single character used for escaping the escape for the quote character",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"emptyValue",
         "title":"Select the string representation of an empty value",
         "description":"Select the string representation of an empty value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "default":"",
         "hidden":false
      },
      {
         "name":"compression",
         "title":"Select compression",
         "description":"Select compressiont",
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
         "title":"Select a fileType",
         "description":"Select fileType",
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
      "documentationLink":"http://www.adobe.com/go/YOURDESTINATION-en",
      "category":"S3",
      "iconUrl":"https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
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
   "identityNamespaces": {
        "adobe_id": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": true
        },
        "mobile_id": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": true
        }
    },
   "segmentMappingConfig":{
       "mapExperiencePlatformSegmentName":false,
       "mapExperiencePlatformSegmentId":false,
       "mapUserInput":false,
       "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "schemaConfig":{
      "profileFields":[
           {
              "name":"phoneNo",
              "title":"phoneNo",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           }
        ],
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
      "defaultStartTime":"00:00"
   },
   "backfillHistoricalProfileData":true
}
```

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `name` | Zeichenfolge | Gibt den Titel Ihres Ziels im Experience Platform-Katalog an. |
| `description` | Zeichenfolge | Geben Sie im Zielkatalog der Experience Platform eine Beschreibung für Ihre Zielkarte ein. Ziel für maximal 4-5 Sätze. |
| `status` | Zeichenfolge | Gibt den Lebenszyklusstatus der Zielkarte an. Zulässige Werte sind `TEST`, `PUBLISHED` und `DELETED`. Verwendung `TEST` wenn Sie Ihr Ziel zum ersten Mal konfigurieren. |
| `maxProfileAttributes` | Zeichenfolge | Gibt die maximale Anzahl von Profilattributen an, die Kunden zum Ziel exportieren können. Der Standardwert lautet `2000`. |
| `maxIdentityAttributes` | Zeichenfolge | Gibt die maximale Anzahl von Identitäts-Namespaces an, die Kunden zum Ziel exportieren können. Der Standardwert lautet `10`. |

{style=&quot;table-layout:auto&quot;}

## Benutzerauthentifizierungskonfigurationen {#customer-authentication-configurations}

Dieser Abschnitt in der Zielkonfiguration generiert die [Neues Ziel konfigurieren](/help/destinations/ui/connect-destination.md) in der Experience Platform-Benutzeroberfläche, auf der Benutzer die Experience Platform mit den Konten verbinden, die sie mit Ihrem Ziel haben.

```json
"customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
```

Welche [Authentifizierungsoption](authentication-configuration.md##supported-authentication-types) Sie geben im `authType` -Feld wird die Benutzerseite wie folgt für die Experience Platform generiert:

### Amazon S3-Authentifizierung

Wenn Sie den Authentifizierungstyp Amazon S3 konfigurieren, müssen Benutzer die S3-Anmeldeinformationen eingeben.

![Benutzeroberflächen-Rendering mit S3-Authentifizierung](assets/s3-authentication-ui.png)

### Azure Blob-Authentifizierung  {#blob}

Wenn Sie den Authentifizierungstyp Azure Blob konfigurieren, müssen Benutzer die Verbindungszeichenfolge eingeben.

![UI-Rendering mit Blob-Authentifizierung](assets/blob-authentication-ui.png)

### SFTP mit Kennwortauthentifizierung

Wenn Sie den SFTP-Authentifizierungstyp mit Kennwort konfigurieren, müssen Benutzer den SFTP-Benutzernamen und das Kennwort sowie die SFTP-Domäne und den Port eingeben (der Standardanschluss ist 22).

![UI-Rendering mit SFTP mit Kennwortauthentifizierung](assets/sftp-password-authentication-ui.png)

### SFTP mit SSH-Schlüsselauthentifizierung

Wenn Sie den Authentifizierungstyp SFTP mit SSH-Schlüssel konfigurieren, müssen Benutzer den SFTP-Benutzernamen und SSH-Schlüssel sowie die SFTP-Domäne und den Port eingeben (der Standardanschluss ist 22).

![UI-Rendering mit SFTP mit SSH-Schlüsselauthentifizierung](assets/sftp-key-authentication-ui.png)

## Kundendatenfelder {#customer-data-fields}

Verwenden Sie diesen Abschnitt, um Benutzer aufzufordern, benutzerdefinierte Felder für Ihr Ziel auszufüllen, wenn sie in der Experience Platform-Benutzeroberfläche eine Verbindung zum Ziel herstellen.

Im folgenden Beispiel: `customerDataFields` erfordert, dass Benutzer einen Namen für ihr Ziel eingeben und eine [!DNL Amazon S3] Behältername und Ordnerpfad sowie Komprimierungstyp und Dateiformat.

```json
 "customerDataFields":[
      {
         "name":"bucket",
         "title":"Amazon S3 bucket name",
         "description":"Enter your Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Amazon S3 bucket path",
         "description":"Enter your S3 bucket path",
         "type":"string",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"sep",
         "title":"Enter a separator for each field and value",
         "description":"Enter a separator character for each field and value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"encoding",
         "title":"Specify encoding (charset) of saved CSV files",
         "description":"Select encoding of csv files",
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
         "title":"Select a single character used for escaping quoted values",
         "description":"Select single charachter for escaping quoted values",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quoteAll",
         "title":"Escape all quoted values",
         "description":"Select whether to escape all quoted values",
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
         "title":"Select a single character used for escaping quotes",
         "description":"Select a single character used for escaping quotes inside an already quoted value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escapeQuotes",
         "title":"Escape quotes",
         "description":"A flag indicating whether values containing quotes should always be enclosed in quotes",
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
         "title":"header",
         "description":"Writes the names of columns as the first line.",
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
         "description":"A flag indicating whether or not leading whitespaces from values being written should be skipped.",
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
         "title":"Select the string representation of a null value",
         "description":"Sets the string representation of a null value. ",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"dateFormat",
         "title":"Date format",
         "description":"Select the string that indicates a date format. ",
         "type":"string",
         "default":"yyyy-MM-dd",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"charToEscapeQuoteEscaping",
         "title":"Char to escape quote escaping",
         "description":"Sets a single character used for escaping the escape for the quote character",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"emptyValue",
         "title":"Select the string representation of an empty value",
         "description":"Select the string representation of an empty value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "default":"",
         "hidden":false
      },
      {
         "name":"compression",
         "title":"Select compression",
         "description":"Select compressiont",
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
         "title":"Select a fileType",
         "description":"Select fileType",
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
```

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `name` | Zeichenfolge | Geben Sie einen Namen für das benutzerdefinierte Feld ein, das Sie einführen. |
| `title` | Zeichenfolge | Gibt den Feldnamen an, wie er von den Kunden in der Experience Platform-Benutzeroberfläche angezeigt wird. |
| `description` | Zeichenfolge | Geben Sie eine Beschreibung für das benutzerdefinierte Feld ein. |
| `type` | Zeichenfolge | Gibt an, welchen Typ von benutzerdefiniertem Feld Sie einführen. Akzeptierte Werte sind `string`, `object`, `integer`. |
| `isRequired` | Boolesch | Gibt an, ob dieses Feld im Ziel-Setup-Workflow erforderlich ist. |
| `pattern` | Zeichenfolge | Erzwingt bei Bedarf ein Muster für das benutzerdefinierte Feld. Verwenden Sie reguläre Ausdrücke, um ein Muster zu erzwingen. Wenn Ihre Kunden-IDs beispielsweise keine Zahlen oder Unterstriche enthalten, geben Sie `^[A-Za-z]+$` in dieses Feld ein. |
| `enum` | Zeichenfolge | Rendert das benutzerdefinierte Feld als Dropdown-Menü und listet die für den Benutzer verfügbaren Optionen auf. |
| `default` | Zeichenfolge | Definiert den Standardwert aus einem `enum` Liste. |

{style=&quot;table-layout:auto&quot;}

## Benutzeroberflächenattribute {#ui-attributes}

Dieser Abschnitt bezieht sich auf die UI-Elemente in der obigen Konfiguration, die von Adobe für Ihr Ziel in der Adobe Experience Platform-Benutzeroberfläche verwendet werden sollte.

```json
"uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/YOURDESTINATION-en",
      "category":"S3",
      "iconUrl":"https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
      "connectionType":"S3",
      "flowRunsSupported":true,
      "monitoringSupported":true,
      "frequency":"Batch"
   }
```

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `documentationLink` | Zeichenfolge | Weitere Informationen finden Sie auf der Dokumentationsseite im [Zielkatalog](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) für Ihr Ziel. Verwendung `http://www.adobe.com/go/destinations-YOURDESTINATION-en`, wobei `YOURDESTINATION` ist der Name Ihres Ziels. Für ein Ziel mit dem Namen Moviestar würden Sie `http://www.adobe.com/go/destinations-moviestar-en` |
| `category` | Zeichenfolge | Bezieht sich auf die Ihrem Ziel in Adobe Experience Platform zugewiesene Kategorie. Weitere Informationen finden Sie unter [Zielkategorien](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html). Verwenden Sie einen der folgenden Werte: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `iconUrl` | Zeichenfolge | Die URL, unter der das Symbol gehostet wird, das auf der Zielkatalogkarte angezeigt werden soll. |
| `connectionType` | Zeichenfolge | Der Verbindungstyp, je nach Ziel. Unterstützte Werte: <ul><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li></ul> |
| `flowRunsSupported` | Boolesch | Gibt an, ob die Zielverbindung im [FlusslaufUI](../../dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard). Wenn Sie diese Einstellung `true`: <ul><li>Die **[!UICONTROL Letztes Datenfluss-Ausführungsdatum]** und **[!UICONTROL Ausführungsstatus des letzten Datenflusses]** werden auf der Zieldurchsuchen-Seite angezeigt.</li><li>Die **[!UICONTROL Datenfluss-Abläufe]** und **[!UICONTROL Aktivierungsdaten]** werden auf der Zielansichtsseite angezeigt.</li></ul> |
| `monitoringSupported` | Boolesch | Gibt an, ob die Zielverbindung im [Monitoring-Benutzeroberfläche](../ui/destinations-workspace.md#browse). Wenn Sie diese Einstellung `true`, die **[!UICONTROL Anzeigen in der Überwachung]** wird auf der Zieldurchsuchen-Seite angezeigt. |
| `frequency` | Zeichenfolge | Bezieht sich auf den vom Ziel unterstützten Datenexport-Typ. Legen Sie fest auf `Batch` für dateibasierte Ziele. |

{style=&quot;table-layout:auto&quot;}

## Zielversand {#destination-delivery}

```json
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
   ]
```

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `authenticationRule` | Zeichenfolge | Gibt an, wie [!DNL Platform] -Kunden stellen eine Verbindung zu Ihrem Ziel her. Akzeptierte Werte sind `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Verwendung `CUSTOMER_AUTHENTICATION` wenn sich Platform-Kunden über eine der folgenden Methoden bei Ihrem System anmelden: <ul><li>`"authType": "S3"`</li><li>`"authType":"AZURE_CONNECTION_STRING"`</li><li>`"authType":"AZURE_SERVICE_PRINCIPAL"`</li><li>`"authType":"SFTP_WITH_SSH_KEY"`</li><li>`"authType":"SFTP_WITH_PASSWORD"`</li></ul> </li><li> Verwendung `PLATFORM_AUTHENTICATION` wenn es ein globales Authentifizierungssystem zwischen Adobe und Ihrem Ziel und der [!DNL Platform] Der Kunde muss keine Authentifizierungsberechtigungen bereitstellen, um eine Verbindung zu Ihrem Ziel herzustellen. In diesem Fall müssen Sie mithilfe der [Anmeldeinformationen](./credentials-configuration-api.md) Konfiguration. </li><li>Verwendung `NONE` wenn keine Authentifizierung erforderlich ist, um Daten an Ihre Zielplattform zu senden. </li></ul> |
| `destinationServerId` | Zeichenfolge | Die `instanceId` des [Zielserverkonfiguration](./destination-server-api.md) für dieses Ziel verwendet. |

{style=&quot;table-layout:auto&quot;}

## Konfiguration der Segmentzuordnung {#segment-mapping}

Dieser Abschnitt der Zielkonfiguration bezieht sich darauf, wie Segmentmetadaten wie Segmentnamen oder IDs zwischen Experience Platform und Ihrem Ziel freigegeben werden sollen.

Durch die `audienceTemplateId`, verknüpft dieser Abschnitt diese Konfiguration auch mit der [Konfiguration von Zielgruppen-Metadaten](./audience-metadata-management.md).

```json
   "segmentMappingConfig":{
       "mapExperiencePlatformSegmentName":false,
       "mapExperiencePlatformSegmentId":false,
       "mapUserInput":false,
       "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
```

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `mapExperiencePlatformSegmentName` | Boolesch | Steuert, ob die Segmentzuordnungs-ID im Zielaktivierungs-Workflow der Experience Platform-Segmentname ist. |
| `mapExperiencePlatformSegmentId` | Boolesch | Steuert, ob die Segmentzuordnungs-ID im Zielaktivierungs-Workflow die Experience Platform-Segment-ID ist. |
| `mapUserInput` | Boolesch | Steuert, ob die Segmentzuordnungs-ID im Zielaktivierungs-Workflow vom Benutzer eingegeben wird. |
| `audienceTemplateId` | Boolesch | Die `instanceId` des [Zielgruppen-Metadatenvorlage](./audience-metadata-management.md) für dieses Ziel verwendet. Lesen Sie zum Einrichten einer Audience-Metadatenvorlage die [API-Referenz für Zielgruppen-Metadaten](./audience-metadata-api.md). |

## Schemakonfiguration im Zuordnungsschritt {#schema-configuration}

Verwenden Sie die Parameter in `schemaConfig` , um den Zuordnungsschritt des Zielaktivierungs-Workflows zu aktivieren. Mithilfe der unten beschriebenen Parameter können Sie bestimmen, ob Experience Platform-Benutzer Profilattribute und/oder Identitäten Ihrem dateibasierten Ziel zuordnen können.

```json
"schemaConfig":{
      "profileFields":[
           {
              "name":"phoneNo",
              "title":"phoneNo",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           }
        ],
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
```

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `profileFields` | Array | Beim Hinzufügen vordefinierter Elemente `profileFields`, können Experience Platform-Benutzer Platform-Attribute den vordefinierten Attributen in Ihrem Ziel zuordnen. |
| `profileRequired` | Boolesch | Verwendung `true` , wenn Benutzer in der Lage sein sollten, Profilattribute von Experience Platform benutzerdefinierten Attributen auf der Zielseite zuzuordnen, wie in der obigen Beispielkonfiguration dargestellt. |
| `segmentRequired` | Boolesch | Immer verwenden `segmentRequired:true`. |
| `identityRequired` | Boolesch | Verwendung `true` , wenn Benutzer in der Lage sein sollten, Identitäts-Namespaces von Experience Platform Ihrem gewünschten Schema zuzuordnen. |

{style=&quot;table-layout:auto&quot;}

### Dynamische Schemakonfiguration im Zuordnungsschritt {#dynamic-schema-configuration}

Adobe Experience Platform Destination SDK unterstützt von Partnern definierte Schemata. Mit einem von Partnern definierten Schema können Benutzer Profilattribute und Identitäten benutzerdefinierten Schemas zuordnen, die von Zielpartnern definiert werden, ähnlich wie bei der [Streaming-Ziele](destination-configuration.md#schema-configuration) Arbeitsablauf.

Verwenden Sie die Parameter in  `dynamicSchemaConfig` , um Ihr eigenes Schema zu definieren, dem Platform-Profilattribute und/oder Identitäten zugeordnet werden können.

```json
"schemaConfig":{
   "dynamicSchemaConfig":{
      "dynamicEnum": {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}",
         "value": "Schema Name",
         "responseFormat": "SCHEMA"
      }
   },
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
}
```

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `profileRequired` | Boolesch | Verwendung `true` , wenn Benutzer in der Lage sein sollten, Profilattribute von Experience Platform benutzerdefinierten Attributen auf der Zielseite zuzuordnen, wie in der obigen Beispielkonfiguration dargestellt. |
| `segmentRequired` | Boolesch | Immer verwenden `segmentRequired:true`. |
| `identityRequired` | Boolesch | Verwendung `true` , wenn Benutzer in der Lage sein sollten, Identitäts-Namespaces von Experience Platform Ihrem gewünschten Schema zuzuordnen. |
| `destinationServerId` | Zeichenfolge | Die `instanceId` des [Zielserverkonfiguration](./destination-server-api.md) für dieses Ziel verwendet. |
| `authenticationRule` | Zeichenfolge | Gibt an, wie [!DNL Platform] -Kunden stellen eine Verbindung zu Ihrem Ziel her. Akzeptierte Werte sind `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Verwendung `CUSTOMER_AUTHENTICATION` wenn sich Platform-Kunden über eine der folgenden Methoden bei Ihrem System anmelden: <ul><li>`"authType": "S3"`</li><li>`"authType":"AZURE_CONNECTION_STRING"`</li><li>`"authType":"AZURE_SERVICE_PRINCIPAL"`</li><li>`"authType":"SFTP_WITH_SSH_KEY"`</li><li>`"authType":"SFTP_WITH_PASSWORD"`</li></ul> </li><li> Verwendung `PLATFORM_AUTHENTICATION` wenn es ein globales Authentifizierungssystem zwischen Adobe und Ihrem Ziel und der [!DNL Platform] Der Kunde muss keine Authentifizierungsberechtigungen bereitstellen, um eine Verbindung zu Ihrem Ziel herzustellen. In diesem Fall müssen Sie mithilfe der [Anmeldeinformationen](./credentials-configuration-api.md) Konfiguration. </li><li>Verwendung `NONE` wenn keine Authentifizierung erforderlich ist, um Daten an Ihre Zielplattform zu senden. </li></ul> |
| `value` | Zeichenfolge | Der Name des Schemas, das in der Experience Platform-Benutzeroberfläche im Zuordnungsschritt angezeigt werden soll. |
| `responseFormat` | Zeichenfolge | Immer auf `SCHEMA` beim Definieren eines benutzerdefinierten Schemas. |

{style=&quot;table-layout:auto&quot;}

## Identitäten und Attribute {#identities-and-attributes}

Die Parameter in diesem Abschnitt bestimmen, welche Identitäten Ihr Ziel akzeptiert. Diese Konfiguration füllt auch die Zielidentitäten und -attribute im [Zuordnungsschritt](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) der Experience Platform-Benutzeroberfläche, in der Benutzer Identitäten und Attribute aus ihren XDM-Schemas dem Schema in Ihrem Ziel zuordnen.


```json
"identityNamespaces": {
        "adobe_id": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": true
        },
        "mobile_id": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": true
        }
    },
```

Sie müssen angeben, [!DNL Platform] Identitäten, die Kunden an Ihr Ziel exportieren können. Einige Beispiele: [!DNL Experience Cloud ID], gehashte E-Mail, Geräte-ID ([!DNL IDFA], [!DNL GAID]). Diese Werte sind [!DNL Platform] Identitäts-Namespaces, die Kunden Identitäts-Namespaces von Ihrem Ziel aus zuordnen können. Sie können auch angeben, ob Kunden benutzerdefinierte Namespaces Identitäten zuordnen können, die von Ihrem Ziel unterstützt werden.

Identitäts-Namespaces erfordern keine 1:1-Korrespondenz zwischen [!DNL Platform] und Ihr Ziel.
Kunden können beispielsweise eine [!DNL Platform] [!DNL IDFA] Namespace zu [!DNL IDFA] -Namespace von Ihrem Ziel aus oder sie können denselben [!DNL Platform] [!DNL IDFA] Namespace zu einem [!DNL Customer ID] -Namespace in Ihrem Ziel.

## Batch-Konfiguration {#batch-configuration}

Dieser Abschnitt bezieht sich auf die Dateiexporteinstellungen in der obigen Konfiguration, die die Adobe für Ihr Ziel in der Adobe Experience Platform-Benutzeroberfläche verwenden sollte.

```json
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
         "ONCE",
         "EVERY_HOUR"
      ],
      "defaultFrequency":"DAILY",
      "defaultStartTime":"00:00"
   }
```

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `allowMandatoryFieldSelection` | Boolesch | Legen Sie fest auf `true` , damit Kunden angeben können, welche Profilattribute obligatorisch sind. Der Standardwert ist `false`. Siehe [Obligatorische Attribute](../ui/activate-batch-profile-destinations.md#mandatory-attributes) für weitere Informationen. |
| `allowDedupeKeyFieldSelection` | Boolesch | Legen Sie fest auf `true` , damit Kunden Deduplizierungsschlüssel angeben können. Der Standardwert ist `false`.  Siehe [Deduplizierungsschlüssel](../ui/activate-batch-profile-destinations.md#deduplication-keys) für weitere Informationen. |
| `defaultExportMode` | Enum | Definiert den standardmäßigen Dateiexportmodus. Unterstützte Werte:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul><br>Der Standardwert ist `DAILY_FULL_EXPORT`. Siehe [Batch-Aktivierungsdokumentation](../ui/activate-batch-profile-destinations.md#scheduling) für Details zur Planung von Dateiexporten. |
| `allowedExportModes` | Liste | Definiert die für Kunden verfügbaren Dateiexportmodi. Unterstützte Werte:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> |
| `allowedScheduleFrequency` | Liste | Definiert die für Kunden verfügbare Dateiexportfrequenz. Unterstützte Werte:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> |
| `defaultFrequency` | Enum | Definiert die standardmäßige Dateiexportfrequenz.Unterstützte Werte:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> <br>Der Standardwert ist `DAILY`. |
| `defaultStartTime` | Zeichenfolge | Definiert die standardmäßige Startzeit für den Dateiexport. Verwendet das Dateiformat von 24 Stunden. Der Standardwert ist &quot;00:00&quot;. |

## Historische Profilqualifikationen {#profile-backfill}

Sie können die `backfillHistoricalProfileData` in der Zielkonfiguration zu bestimmen, ob historische Profilqualifikationen an Ihr Ziel exportiert werden sollen.

```json
   "backfillHistoricalProfileData":true
```

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `backfillHistoricalProfileData` | Boolesch | Steuert, ob historische Profildaten exportiert werden, wenn Segmente für das Ziel aktiviert werden. <br> <ul><li> `true`: [!DNL Platform] sendet die historischen Benutzerprofile, die sich für das Segment qualifiziert haben, bevor das Segment aktiviert wird. </li><li> `false`: [!DNL Platform] enthält nur Benutzerprofile, die sich für das Segment qualifizieren, nachdem das Segment aktiviert wurde. </li></ul> |

## Wie diese Konfiguration alle erforderlichen Informationen für Ihr Ziel verbindet {#connecting-all-configurations}

Einige Ihrer Zieleinstellungen müssen über das [Zielserver](./server-and-file-configuration.md) oder [Konfiguration von Zielgruppen-Metadaten](./audience-metadata-management.md). Die hier beschriebene Zielkonfiguration verbindet alle diese Einstellungen, indem sie wie folgt auf die beiden anderen Konfigurationen verweist:

* Verwenden Sie die `destinationServerId` , um auf den Zielserver und die Vorlagenkonfiguration zu verweisen, die für Ihr Ziel eingerichtet sind.
* Verwenden Sie die `audienceMetadataId` , um auf die für Ihr Ziel eingerichtete Audience-Metadatenkonfiguration zu verweisen.
