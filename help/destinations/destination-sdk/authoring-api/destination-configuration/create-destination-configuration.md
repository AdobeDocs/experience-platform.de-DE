---
description: Erfahren Sie, wie Sie einen API-Aufruf strukturieren, um eine Zielkonfiguration über Adobe Experience Platform Destination SDK zu erstellen.
title: Erstellen einer Zielkonfiguration
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 94%

---


# Erstellen einer Zielkonfiguration

Diese Seite veranschaulicht die API-Anfrage und die Payload, die Sie verwenden können, um Ihre eigene Zielkonfiguration unter Verwendung des API-Endpunkts `/authoring/destinations` zu erstellen.

Eine ausführliche Beschreibung der Funktionen, die Sie über diesen Endpunkt konfigurieren können, finden Sie in den folgenden Artikeln:

* [Konfiguration der Kundenauthentifizierung](../../functionality/destination-configuration/customer-authentication.md)
* [OAuth 2-Authentifizierung](../../functionality/destination-configuration/oauth2-authentication.md)
* [Benutzerdefinierte Datenfelder](../../functionality/destination-configuration/customer-data-fields.md)
* [Benutzeroberflächenattribute](../../functionality/destination-configuration/ui-attributes.md)
* [Schemakonfiguration](../../functionality/destination-configuration/schema-configuration.md)
* [Konfiguration von Identity-Namespaces](../../functionality/destination-configuration/identity-namespace-configuration.md)
* [Zielbereitstellung](../../functionality/destination-configuration/destination-delivery.md)
* [Konfiguration von Zielgruppen-Metadaten](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [Konfiguration von Zielgruppen-Metadaten](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [Aggregationsrichtlinie](../../functionality/destination-configuration/aggregation-policy.md)
* [Batch-Konfiguration](../../functionality/destination-configuration/batch-configuration.md)
* [Historische Profilqualifikationen](../../functionality/destination-configuration/historical-profile-qualifications.md)

>[!IMPORTANT]
>
>Bei allen von Destination SDK unterstützten Parameternamen und Werten wird **nach Groß-/Kleinschreibung unterschieden**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Erste Schritte mit API-Vorgängen für die Zielkonfiguration {#get-started}

Bevor Sie fortfahren, lesen Sie [Erste Schritte](../../getting-started.md). Dort finden Sie die nötigen Informationen für den erfolgreichen Aufruf der API, einschließlich Details für den Abruf der erforderlichen Authoring-Berechtigung für Ziele und zu den erforderlichen Kopfzeilen.

## Erstellen einer Zielkonfiguration {#create}

Sie können eine neue Zielkonfiguration erstellen, indem Sie eine POST-Anfrage an den Endpunkt `/authoring/destinations` senden.

>[!TIP]
>
>**API-Endpunkt**: `platform.adobe.io/data/core/activation/authoring/destinations`

**API-Format**

```http
POST /authoring/destinations
```

Die folgende Anfrage erstellt eine neue [!DNL Amazon S3]-Zielkonfiguration, die durch die in der Payload bereitgestellten Parameter konfiguriert wird. Die nachstehende Payload enthält alle Parameter für dateibasierte Ziele, die vom Endpunkt `/authoring/destinations` akzeptiert werden.

Beachten Sie, dass Sie nicht alle Parameter für den API-Aufruf hinzufügen müssen und dass die Payload entsprechend Ihren API-Anforderungen angepasst werden kann.

+++Anfrage

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

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `name` | Zeichenfolge | Gibt den Titel Ihres Ziels im Experience Platform-Katalog an. |
| `description` | Zeichenfolge | Geben Sie eine Beschreibung ein, die Adobe im Zielkatalog von Experience Platform für Ihre Zielkarte verwenden soll. Es sollten nicht mehr als 4–5 Sätze sein. ![Platform-UI-Bild, das die Zielbeschreibung anzeigt.](../../assets/authoring-api/destination-configuration/destination-description.png "Zielbeschreibung"){width="100" zoomable="yes"} |
| `status` | Zeichenfolge | Gibt den Lebenszyklusstatus der Zielkarte an. Zulässige Werte sind `TEST`, `PUBLISHED` und `DELETED`. Verwenden Sie `TEST`, wenn Sie Ihr Ziel zum ersten Mal konfigurieren. |
| `customerAuthenticationConfigurations.authType` | Zeichenfolge | Gibt die Konfiguration an, die zum Authentifizieren von Experience Platform-Kundinnen und -Kunden auf Ihrem Ziel-Server verwendet wird. Siehe [Konfiguration der Kundenauthentifizierung](../../functionality/destination-configuration/customer-authentication.md) für detaillierte Informationen zu den unterstützten Authentifizierungstypen. |
| `customerDataFields.name` | Zeichenfolge | Geben Sie einen Namen für das benutzerdefinierte Feld ein, das Sie einführen. <br/><br/> Siehe [Kundendatenfelder](../../functionality/destination-configuration/customer-data-fields.md) für detaillierte Informationen zu diesen Einstellungen. ![Platform-UI-Bild mit Feldern zu Kundendaten.](../../assets/authoring-api/destination-configuration/customer-data-fields.png "Kundendatenfeld"){width="100" zoomable="yes"} |
| `customerDataFields.type` | Zeichenfolge | Gibt an, welchen Typ von benutzerdefiniertem Feld Sie einführen. Akzeptierte Werte sind `string`, `object` und `integer`. <br/><br/> Siehe [Kundendatenfelder](../../functionality/destination-configuration/customer-data-fields.md) für detaillierte Informationen zu diesen Einstellungen. |
| `customerDataFields.title` | Zeichenfolge | Gibt den Feldnamen an, wie er den Kundinnen und Kunden in der Benutzeroberfläche von Experience Platform angezeigt wird. <br/><br/> Siehe [Kundendatenfelder](../../functionality/destination-configuration/customer-data-fields.md) für detaillierte Informationen zu diesen Einstellungen. |
| `customerDataFields.description` | Zeichenfolge | Geben Sie eine Beschreibung für das benutzerdefinierte Feld ein. Siehe [Kundendatenfelder](../../functionality/destination-configuration/customer-data-fields.md) für detaillierte Informationen zu diesen Einstellungen. |
| `customerDataFields.isRequired` | Boolesch | Gibt an, ob dieses Feld im Ziel-Setup-Workflow erforderlich ist. <br/><br/> Siehe [Kundendatenfelder](../../functionality/destination-configuration/customer-data-fields.md) für detaillierte Informationen zu diesen Einstellungen. |
| `customerDataFields.enum` | Zeichenfolge | Rendert das benutzerdefinierte Feld als Dropdown-Menü und listet die für Benutzende verfügbaren Optionen auf. <br/><br/> Siehe [Kundendatenfelder](../../functionality/destination-configuration/customer-data-fields.md) für detaillierte Informationen zu diesen Einstellungen. |
| `customerDataFields.default` | Zeichenfolge | Definiert den Standardwert aus einer `enum`-Liste. |
| `customerDataFields.pattern` | Zeichenfolge | Erzwingt bei Bedarf ein Muster für das benutzerdefinierte Feld. Verwenden Sie reguläre Ausdrücke, um ein Muster zu erzwingen. Wenn Ihre Kunden-IDs beispielsweise keine Zahlen oder Unterstriche enthalten, geben Sie in dieses Feld `^[A-Za-z]+$` ein. <br/><br/> Siehe [Kundendatenfelder](../../functionality/destination-configuration/customer-data-fields.md) für detaillierte Informationen zu diesen Einstellungen. |
| `uiAttributes.documentationLink` | Zeichenfolge | Weitere Informationen finden Sie auf der Dokumentationsseite im [Zielkatalog](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=de#catalog) für Ihr Ziel. Verwenden Sie `https://www.adobe.com/go/destinations-YOURDESTINATION-en`, wobei `YOURDESTINATION` für den Namen Ihres Ziels steht. Für ein Ziel mit dem Namen „Moviestar“ würden Sie `https://www.adobe.com/go/destinations-moviestar-en` verwenden. Beachten Sie, dass dieser Link nur funktioniert, wenn Adobe Ihr Ziel live stellt und die Dokumentation veröffentlicht wird. <br/><br/> Siehe [Benutzeroberflächenattribute](../../functionality/destination-configuration/ui-attributes.md) für detaillierte Informationen zu diesen Einstellungen. ![Platform-UI-Bild, das den Dokumentations-Link anzeigt.](../../assets/authoring-api/destination-configuration/documentation-url.png "Dokumentations-URL"){width="100" zoomable="yes"} |
| `uiAttributes.category` | Zeichenfolge | Bezieht sich auf die Ihrem Ziel in Adobe Experience Platform zugewiesene Kategorie. Weitere Informationen finden Sie unter [Zielkategorien](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=de#destination-categories). Verwenden Sie einen der folgenden Werte: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. <br/><br/> Siehe [Benutzeroberflächenattribute](../../functionality/destination-configuration/ui-attributes.md) für detaillierte Informationen zu diesen Einstellungen. |
| `uiAttributes.connectionType` | Zeichenfolge | Der Verbindungstyp, je nach Ziel. Unterstützte Werte: <ul><li>`Server-to-server`</li><li>`Cloud storage`</li><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li><li>`DLZ`</li></ul> |
| `uiAttributes.frequency` | Zeichenfolge | Bezieht sich auf die Art des Datenexports, die vom Ziel unterstützt wird. Setzen Sie diesen auf `Streaming` für API-basierte Integrationen oder auf `Batch`, wenn Sie Dateien in Ihre Ziele exportieren. |
| `identityNamespaces.externalId.acceptsAttributes` | Boolesch | Gibt an, ob Kundinnen und Kunden der Identität, die Sie konfigurieren, standardmäßige Profilattribute zuordnen können. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | Boolesch | Gibt an, ob Kundinnen und Kunden Identitäten, die zu [benutzerdefinierten Namespaces](/help/identity-service/namespaces.md#manage-namespaces) gehören, der Identität zuordnen können, die Sie konfigurieren. |
| `identityNamespaces.externalId.transformation` | Zeichenfolge | _Wird in der Beispielkonfiguration nicht angezeigt_. Wird zum Beispiel verwendet, wenn der [!DNL Platform]-Kunde einfache E-Mail-Adressen als Attribut verwendet und Ihre Plattform nur E-Mails mit Hash akzeptiert. Hier geben Sie die Umwandlung an, die angewendet werden soll (z. B. Umwandlung der E-Mail in Kleinbuchstaben, dann Hash). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | – | Gibt an, welche [Standard-Identity-Namespaces](/help/identity-service/namespaces.md#standard) (z. B. IDFA) Kundinnen und Kunden der Identität zuordnen können, die Sie konfigurieren. <br> Wenn Sie `acceptedGlobalNamespaces` verwenden, können Sie E-Mail-Adressen oder Telefonnummern mithilfe von `"requiredTransformation":"sha256(lower($))"` in Kleinbuchstaben umwandeln und hashen. |
| `destinationDelivery.authenticationRule` | Zeichenfolge | Gibt an, wie [!DNL Platform]-Kundinnen und -Kunden eine Verbindung zu Ihrem Ziel herstellen. Akzeptierte Werte sind `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Verwenden Sie `CUSTOMER_AUTHENTICATION`, wenn sich Platform-Kundinnen und -Kunden über einen Benutzernamen und ein Kennwort, ein Bearer-Token oder eine andere Authentifizierungsmethode bei Ihrem System anmelden. Sie würden diese Option beispielsweise auswählen, wenn Sie auch `authType: OAUTH2` oder `authType:BEARER` in `customerAuthenticationConfigurations` ausgewählt haben. </li><li> Verwenden Sie `PLATFORM_AUTHENTICATION`, wenn ein globales Authentifizierungssystem zwischen Adobe und Ihrem Ziel existiert und der [!DNL Platform]-Kunde keine Authentifizierungsdaten bereitstellen muss, um eine Verbindung zu Ihrem Ziel herzustellen. In diesem Fall müssen Sie ein Anmeldeinformationen-Objekt mithilfe der Konfiguration der [Anmeldeinformationen-API](../../credentials-api/create-credential-configuration.md) erstellen. </li><li>Verwenden Sie `NONE`, wenn keine Authentifizierung erforderlich ist, um Daten an Ihre Zielplattform zu senden. </li></ul> |
| `destinationDelivery.destinationServerId` | Zeichenfolge | Die `instanceId` der [Ziel-Server-Vorlage](../destination-server/create-destination-server.md), die für dieses Ziel verwendet wird. |
| `backfillHistoricalProfileData` | Boolesch | Steuert, ob historische Profildaten exportiert werden, wenn Zielgruppen für das Ziel aktiviert werden. Setzen Sie diesen Parameter immer auf `true`. |
| `segmentMappingConfig.mapUserInput` | Boolesch | Steuert, ob die Zielgruppen-Mapping-ID im Zielaktivierungs-Workflow vom Benutzer eingegeben wird. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | Boolesch | Steuert, ob die Zielgruppen-Mapping-ID im Zielgruppen-Aktivierungsworkflow die Experience Platform-Zielgruppen-ID ist. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | Boolesch | Steuert, ob die Zielgruppen-Mapping-ID im Zielgruppen-Aktivierungsarbeitsablauf der Zielgruppenname der Experience Platform ist. |
| `segmentMappingConfig.audienceTemplateId` | Boolesch | Die `instanceId` der [Zielgruppen-Metadatenvorlage](../../metadata-api/create-audience-template.md), die für dieses Ziel verwendet wird. |
| `schemaConfig.profileFields` | Array | Beim Hinzufügen vordefinierter `profileFields` wie in der obigen Konfiguration können Benutzerinnen und Benutzer die Attribute von Experience Platform den vordefinierten Attributen Ihres Ziels zuordnen. |
| `schemaConfig.profileRequired` | Boolesch | Verwenden Sie `true`, wenn Benutzerinnen und Benutzer die Zuordnung von Profilattributen aus Experience Platform zu benutzerdefinierten Attributen des Ziels vornehmen dürfen, wie in der obigen Beispielkonfiguration dargestellt. |
| `schemaConfig.segmentRequired` | Boolesch | Verwenden Sie immer `segmentRequired:true`. |
| `schemaConfig.identityRequired` | Boolesch | Verwenden Sie `true`, wenn Benutzerinnen und Benutzer die Zuordnung von Identity-Namespaces von Experience Platform zu Ihrem gewünschten Schema vornehmen dürfen. |

{style="table-layout:auto"}

+++

+++Antwort

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit Details zu Ihrer neu erstellten Zielkonfiguration zurückgegeben.

+++

## Umgang mit API-Fehlern

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status-Codes](../../../../landing/troubleshooting.md#api-status-codes) und [Fehler im Anfrage-Header](../../../../landing/troubleshooting.md#request-header-errors) in der Anleitung zur Fehlerbehebung für Platform.

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie über den API-Endpunkt `/authoring/destinations` von Destination SDK eine neue Zielkonfiguration erstellen.

Weitere Informationen dazu, was Sie mit diesem Endpunkt tun können, finden Sie in den folgenden Artikeln:

* [Abrufen einer Zielkonfiguration](retrieve-destination-configuration.md)
* [Aktualisieren einer Zielkonfiguration](update-destination-configuration.md)
* [Löschen einer Zielkonfiguration](delete-destination-configuration.md)

Informationen dazu, wo dieser Endpunkt in den Prozess zur Zielbearbeitung passt, finden Sie in den folgenden Artikeln:

* [Verwenden des Destination SDK zum Konfigurieren eines Streaming-Ziels](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Verwenden des Destination SDK zum Konfigurieren eines dateibasierten Ziels](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)
