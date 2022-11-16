---
description: Auf dieser Seite werden alle API-Abläufe aufgelistet und beschrieben, die Sie mit dem API-Endpunkt „/authoring/destinations“ ausführen können.
title: API-Endpunktvorgänge für Ziele
exl-id: 96755e9d-be62-432f-b985-91330575b395
source-git-commit: 21278b39a2dc12771449b9a471ea4182c6b999a3
workflow-type: tm+mt
source-wordcount: '2545'
ht-degree: 91%

---

# API-Vorgänge für Ziel-Endpunkte {#destination-configuration}

>[!IMPORTANT]
>
>**API-Endpunkt**: `platform.adobe.io/data/core/activation/authoring/destinations`

Auf dieser Seite werden alle API-Vorgänge aufgelistet und beschrieben, die Sie mit dem API-Endpunkt `/authoring/destinations` ausführen können. Eine Beschreibung der von diesem Endpunkt unterstützten Funktionen finden Sie unter [Zielkonfiguration](./destination-configuration.md).

## Erste Schritte mit API-Vorgängen für Ziele {#get-started}

Bevor Sie fortfahren, lesen Sie [Erste Schritte](./getting-started.md). Dort finden Sie die nötigen Informationen für den erfolgreichen Aufruf der API, einschließlich Details für den Abruf der erforderlichen Authoring-Berechtigung für Ziele und zu den erforderlichen Kopfzeilen.

## Erstellen einer Konfiguration für ein Streaming-Ziel {#create}

Sie können eine neue Zielkonfiguration erstellen, indem Sie eine POST-Anfrage an den Endpunkt `/authoring/destinations` senden.

**API-Format**

```http
POST /authoring/destinations
```

**Anfrage**

Die folgende Anfrage erstellt eine neue Streaming-Zielkonfiguration, der durch die in der Payload bereitgestellten Parameter konfiguriert wird. Die nachstehende Payload enthält alle Parameter für Streaming-Ziele, die vom Endpunkt `/authoring/destinations` akzeptiert werden. Beachten Sie, dass Sie nicht alle Parameter für den Aufruf hinzufügen müssen und dass die Vorlage entsprechend Ihren API-Anforderungen angepasst werden kann.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"endpointsInstance",
         "type":"string",
         "title":"Select Endpoint",
         "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
         "isRequired":true,
         "enum":[
            "US",
            "EU",
            "APAC",
            "NZ"
         ]
      },
      {
         "name":"customerID",
         "type":"string",
         "title":"Moviestar Customer ID",
         "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
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
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
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
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `name` | Zeichenfolge | Gibt den Titel Ihres Ziels im Katalog von Experience Platform an |
| `description` | Zeichenfolge | Geben Sie eine Beschreibung ein, die Adobe im Zielkatalog von Experience Platform für Ihre Zielkarte verwenden soll. Es sollten nicht mehr als 4–5 Sätze sein. |
| `status` | Zeichenfolge | Gibt den Lebenszyklusstatus der Zielkarte an. Zulässige Werte sind `TEST`, `PUBLISHED` und `DELETED`. Verwenden Sie `TEST`, wenn Sie Ihr Ziel zum ersten Mal konfigurieren. |
| `customerAuthenticationConfigurations` | Zeichenfolge | Gibt die Konfiguration an, die zum Authentifizieren von Experience Platform-Kunden auf Ihrem Server verwendet wird. Siehe `authType` unten für gültige Werte. |
| `customerAuthenticationConfigurations.authType` | Zeichenfolge | Folgende Werte werden für Streaming-Ziele unterstützt: <ul><li>`OAUTH2`</li><li>`BEARER`</li></ul> Folgende Werte werden für dateibasierte Ziele unterstützt: <ul><li>`S3`</li><li>`AZURE_CONNECTION_STRING`</li><li>`AZURE_SERVICE_PRINCIPAL`</li><li>`SFTP_WITH_SSH_KEY`</li><li>`SFTP_WITH_PASSWORD`</li></ul> |
| `customerDataFields.name` | Zeichenfolge | Geben Sie einen Namen für das benutzerdefinierte Feld ein, das Sie einführen. |
| `customerDataFields.type` | Zeichenfolge | Gibt an, welchen Typ von benutzerdefiniertem Feld Sie einführen. Akzeptierte Werte sind `string`, `object` und `integer` |
| `customerDataFields.title` | Zeichenfolge | Gibt den Feldnamen an, wie er von den Kunden in der Benutzeroberfläche von Experience Platform angezeigt wird |
| `customerDataFields.description` | Zeichenfolge | Geben Sie eine Beschreibung für das benutzerdefinierte Feld ein. |
| `customerDataFields.isRequired` | Boolesch | Gibt an, ob dieses Feld im Ziel-Setup-Workflow erforderlich ist. |
| `customerDataFields.enum` | Zeichenfolge | Rendert das benutzerdefinierte Feld als Dropdown-Menü und listet die für den Benutzer verfügbaren Optionen auf. |
| `customerDataFields.pattern` | Zeichenfolge | Erzwingt bei Bedarf ein Muster für das benutzerdefinierte Feld. Verwenden Sie reguläre Ausdrücke, um ein Muster zu erzwingen. Wenn Ihre Kunden-IDs beispielsweise keine Zahlen oder Unterstriche enthalten, geben Sie in dieses Feld `^[A-Za-z]+$` ein. |
| `uiAttributes.documentationLink` | Zeichenfolge | Weitere Informationen finden Sie auf der Dokumentationsseite im [Zielkatalog](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=de#catalog) für Ihr Ziel. Verwenden Sie `https://www.adobe.com/go/destinations-YOURDESTINATION-en`, wobei `YOURDESTINATION` für den Namen Ihres Ziels steht. Für ein Ziel mit dem Namen „Moviestar“ würden Sie `https://www.adobe.com/go/destinations-moviestar-en` verwenden. Beachten Sie, dass dieser Link nur funktioniert, wenn Adobe Ihr Ziel live festlegt und die Dokumentation veröffentlicht wird. |
| `uiAttributes.category` | Zeichenfolge | Bezieht sich auf die Ihrem Ziel in Adobe Experience Platform zugewiesene Kategorie. Weitere Informationen finden Sie unter [Zielkategorien](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=de#destination-categories). Verwenden Sie einen der folgenden Werte: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `uiAttributes.connectionType` | Zeichenfolge | `Server-to-server` ist derzeit die einzige verfügbare Option. |
| `uiAttributes.frequency` | Zeichenfolge | `Streaming` ist derzeit die einzige verfügbare Option. |
| `identityNamespaces.externalId.acceptsAttributes` | Boolesch | Gibt an, ob Kunden der Identität, die Sie konfigurieren, standardmäßige Profilattribute zuordnen können. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | Boolesch | Gibt an, ob Kunden Identitäten zuordnen können, die zu [benutzerdefinierte Namespaces](/help/identity-service/namespaces.md#manage-namespaces) der Identität, die Sie konfigurieren. |
| `identityNamespaces.externalId.transformation` | Zeichenfolge | _Wird in der Beispielkonfiguration nicht angezeigt_. Wird zum Beispiel verwendet, wenn der [!DNL Platform]-Kunde einfache E-Mail-Adressen als Attribut verwendet und Ihre Plattform nur E-Mails mit Hash akzeptiert. Hier geben Sie die Umwandlung an, die angewendet werden soll (z. B. Umwandlung der E-Mail in Kleinbuchstaben, dann Hash). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | – | Gibt an, [Standard-Identitäts-Namespaces](/help/identity-service/namespaces.md#standard) (z. B. IDFA)-Kunden können der Identität zuordnen, die Sie konfigurieren. <br> Wenn Sie `acceptedGlobalNamespaces` verwenden, können Sie E-Mail-Adressen oder Telefonnummern mithilfe von `"requiredTransformation":"sha256(lower($))"` in Kleinbuchstaben umwandeln und hashen. |
| `destinationDelivery.authenticationRule` | Zeichenfolge | Gibt an, wie [!DNL Platform]-Kunden eine Verbindung zu Ihrem Ziel herstellen. Akzeptierte Werte sind `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Verwenden Sie `CUSTOMER_AUTHENTICATION`, wenn sich Platform-Kunden über einen Benutzernamen und ein Kennwort, ein Träger-Token oder eine andere Authentifizierungsmethode bei Ihrem System anmelden. Sie würden diese Option beispielsweise auswählen, wenn Sie auch `authType: OAUTH2` oder `authType:BEARER` in `customerAuthenticationConfigurations` ausgewählt haben. </li><li> Verwenden Sie `PLATFORM_AUTHENTICATION`, wenn ein globales Authentifizierungssystem zwischen Adobe und Ihrem Ziel existiert und der [!DNL Platform]-Kunde keine Authentifizierungsdaten bereitstellen muss, um eine Verbindung zu Ihrem Ziel herzustellen. In diesem Fall müssen Sie ein Objekt für die [Anmeldeinformationen](./credentials-configuration-api.md) mithilfe der Konfiguration erstellen. </li><li>Verwenden Sie `NONE`, wenn keine Authentifizierung erforderlich ist, um Daten an Ihre Zielplattform zu senden. </li></ul> |
| `destinationDelivery.destinationServerId` | Zeichenfolge | Die `instanceId` der [Ziel-Server-Vorlage](./destination-server-api.md), die für dieses Ziel verwendet wird. |
| `backfillHistoricalProfileData` | Boolesch | Steuert, ob historische Profildaten exportiert werden, wenn Segmente für das Ziel aktiviert werden. <br> <ul><li> `true`: [!DNL Platform] sendet die historischen Benutzerprofile, die sich für das Segment qualifiziert haben, bevor das Segment aktiviert wird. </li><li> `false`: [!DNL Platform] enthält nur Benutzerprofile, die sich für das Segment qualifizieren, nachdem das Segment aktiviert wurde. </li></ul> |
| `segmentMappingConfig.mapUserInput` | Boolesch | Steuert, ob die Segmentzuordnungs-ID im Zielaktivierungs-Workflow vom Benutzer eingegeben wird. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | Boolesch | Steuert, ob die Segmentzuordnungs-ID im Zielaktivierungs-Workflow die Experience Platform-Segment-ID ist. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | Boolesch | Steuert, ob die Segmentzuordnungs-ID im Zielaktivierungs-Workflow der Experience Platform-Segmentname ist. |
| `segmentMappingConfig.audienceTemplateId` | Boolesch | Die `instanceId` der [Zielgruppen-Metadatenvorlage](./audience-metadata-api.md), die für dieses Ziel verwendet wird. |
| `schemaConfig.profileFields` | Array | Beim Hinzufügen vordefinierter `profileFields` wie in der obigen Konfiguration können Benutzer die Attribute von Experience Platform den vordefinierten Attributen des Ziels zuordnen. |
| `schemaConfig.profileRequired` | Boolesch | Verwenden Sie `true`, wenn Benutzer die Zuordnung von Profilattributen aus Experience Platform zu benutzerdefinierten Attributen des Ziels vornehmen dürfen, wie in der obigen Beispielkonfiguration dargestellt. |
| `schemaConfig.segmentRequired` | Boolesch | Verwenden Sie immer `segmentRequired:true`. |
| `schemaConfig.identityRequired` | Boolesch | Verwenden Sie `true`, wenn Benutzer die Zuordnung von Identitäts-Namespaces von Experience Platform zu Ihrem gewünschten Schema vornehmen dürfen. |
| `aggregation.aggregationType` | – | Wählen Sie entweder `BEST_EFFORT` oder `CONFIGURABLE_AGGREGATION`. Die obige Beispielkonfiguration umfasst eine `BEST_EFFORT`-Aggregation. Eine Veranschaulichung der `CONFIGURABLE_AGGREGATION` finden Sie in der Beispielkonfiguration im Dokument [Zielkonfiguration](./destination-configuration.md#example-configuration). Die für die konfigurierbare Aggregation relevanten Parameter sind in der folgenden Tabelle beschrieben. |
| `aggregation.bestEffortAggregation.maxUsersPerRequest` | Ganzzahl | Experience Platform kann mehrere exportierte Profile in einem einzigen HTTP-Aufruf aggregieren. Geben Sie die maximale Anzahl von Profilen an, die Ihr Endpunkt in einem einzelnen HTTP-Aufruf erhalten soll. Beachten Sie, dass dies eine bestmögliche Aggregation ist. Wenn Sie beispielsweise den Wert 100 angeben, kann Platform eine beliebige Anzahl von Profilen senden, solange es weniger als 100 sind. <br> Wenn Ihr Server mehrere Benutzer pro Anforderung nicht akzeptiert, setzen Sie diesen Wert auf 1. |
| `aggregation.bestEffortAggregation.splitUserById` | Boolesch | Verwenden Sie dieses Flag, wenn der Aufruf an das Ziel nach Identität aufgeteilt werden soll. Setzen Sie dieses Flag auf `true`, wenn Ihr Server für einen gegebenen Namespace nur eine Identität pro Aufruf akzeptiert. |
| `aggregation.configurableAggregation.splitUserById` | Boolesch | Siehe Parameter in der Beispielkonfiguration [hier](./destination-configuration.md#example-configuration). Verwenden Sie dieses Flag, wenn der Aufruf an das Ziel nach Identität aufgeteilt werden soll. Setzen Sie dieses Flag auf `true`, wenn Ihr Server für einen gegebenen Namespace nur eine Identität pro Aufruf akzeptiert. |
| `aggregation.configurableAggregation.maxBatchAgeInSecs` | Ganzzahl | <ul><li>*Mindestwert: 1800*</li><li>*Höchstwert: 3600*</li><li>Siehe Parameter in der Beispielkonfiguration [hier](./destination-configuration.md#example-configuration). Konfigurieren Sie einen Wert zwischen den akzeptierten Mindest- und Höchstwerten. Gemeinsam mit `maxNumEventsInBatch`festgelegt ist, bestimmt dieser Parameter, wie lange die Experience Platform warten soll, bis ein API-Aufruf an Ihren -Endpunkt gesendet wird. <br> Wenn Sie beispielsweise den Maximalwert für beide Parameter verwenden, wartet die Experience Platform entweder 3600 Sekunden ODER bis 10.000 qualifizierte Profile vorhanden sind, bevor der API-Aufruf erfolgt (je nachdem, was zuerst eintritt). </li></ul> |
| `aggregation.configurableAggregation.maxNumEventsInBatch` | Ganzzahl | <ul><li>*Mindestwert: 1000*</li><li>*Höchstwert: 10.000*</li><li>Siehe Parameter in der Beispielkonfiguration [hier](./destination-configuration.md#example-configuration). Konfigurieren Sie einen Wert zwischen den akzeptierten Mindest- und Höchstwerten. Eine Beschreibung dieses Parameters finden Sie unter `maxBatchAgeInSecs` direkt oben.</li></ul> |
| `aggregation.configurableAggregation.aggregationKey` | Boolesch | Siehe Parameter in der Beispielkonfiguration [hier](./destination-configuration.md#example-configuration). Ermöglicht die Aggregation der dem Ziel zugeordneten exportierten Profile anhand der folgenden Parameter: <br> <ul><li>Segment-ID</li><li> Segmentstatus </li><li> Identitäts-Namespace </li></ul> |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentId` | Boolesch | Siehe Parameter in der Beispielkonfiguration [hier](./destination-configuration.md#example-configuration). Legen Sie dies auf `true` fest, wenn Sie Profile gruppieren möchten, die nach Segmentkennung in Ihr Ziel exportiert wurden. |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentStatus` | Boolesch | Siehe Parameter in der Beispielkonfiguration [hier](./destination-configuration.md#example-configuration). Sie müssen sowohl `includeSegmentId:true` als auch `includeSegmentStatus:true` festlegen, wenn Sie die an Ihr Ziel exportierten Profile nach Segmentkennung UND Segmentstatus gruppieren möchten. |
| `aggregation.configurableAggregation.aggregationKey.includeIdentity` | Boolesch | Siehe Parameter in der Beispielkonfiguration [hier](./destination-configuration.md#example-configuration). Legen Sie dies auf `true` fest, wenn Sie Profile gruppieren möchten, die nach Identitäts-Namespace zu Ihrem Ziel exportiert wurden. |
| `aggregation.configurableAggregation.aggregationKey.oneIdentityPerGroup` | Boolesch | Siehe Parameter in der Beispielkonfiguration [hier](./destination-configuration.md#example-configuration). Verwenden Sie diesen Parameter, um anzugeben, ob die exportierten Profile in Gruppen einer einzigen Identität zusammengefasst werden sollen (GAID, IDFA, Telefonnummern, E-Mail usw.). |
| `aggregation.configurableAggregation.aggregationKey.groups` | Zeichenfolge | Siehe Parameter in der Beispielkonfiguration [hier](./destination-configuration.md#example-configuration). Erstellen Sie Listen mit Identitätsgruppen, wenn Sie Profile gruppieren möchten, die nach Gruppen von Identitäts-Namespace in Ihr Ziel exportiert wurden. Beispielsweise können Sie Profile, die die Kennungen IDFA und GAID für Mobilgeräte enthalten, mithilfe der im Beispiel beschriebenen Konfiguration zu einem Aufruf an Ihr Ziel und E-Mails zu einem anderen kombinieren. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit Details zu Ihrer neu erstellten Zielkonfiguration zurückgegeben.

## Erstellen der Konfiguration für ein dateibasiertes Ziel {#create-file-based}

Sie können eine neue Zielkonfiguration erstellen, indem Sie eine POST-Anfrage an den Endpunkt `/authoring/destinations` senden.

**API-Format**

```http
POST /authoring/destinations
```

**Anfrage**

Die folgende Anfrage erstellt eine neue [!DNL Amazon S3]-dateibasierte Zielkonfiguration, die anhand der in der Payload angegebenen Parameter konfiguriert wird. Die nachstehende Payload enthält alle Parameter für dateibasierte Ziele, die vom Endpunkt `/authoring/destinations` akzeptiert werden. Beachten Sie, dass Sie nicht alle Parameter für den Aufruf hinzufügen müssen und dass die Vorlage entsprechend Ihren API-Anforderungen angepasst werden kann.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
        "name": "S3 Destination with CSV Options",
        "description": "S3 Destination with CSV Options",
        "releaseNotes": "S3 Destination with CSV Options",
        "status": "TEST",
        "customerAuthenticationConfigurations": [
            {
                "authType": "S3"
            }
        ],
        "customerEncryptionConfigurations": [
            {
                "encryptionAlgo": ""
            }
        ],
        "customerDataFields": [
            {
                "name": "bucket",
                "title": "Select S3 Bucket",
                "description": "Select S3 Bucket",
                "type": "string",
                "isRequired": true,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "path",
                "title": "S3 path",
                "description": "Select S3 Bucket",
                "type": "string",
                "isRequired": true,
                "pattern": "^[A-Za-z]+$",
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "sep",
                "title": "Select separator for each field and value",
                "description": "Select for each field and value",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "encoding",
                "title": "Specify encoding (charset) of saved CSV files",
                "description": "Select encoding of csv files",
                "type": "string",
                "enum": ["UTF-8", "UTF-16"],
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "quote",
                "title": "Select a single character used for escaping quoted values",
                "description": "Select single charachter for escaping quoted values",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "quoteAll",
                "title": "Quote All",
                "description": "Select flag for escaping quoted values",
                "type": "string",
                "enum" : ["true","false"],
                "default": "true",
                "isRequired": true,
                "readOnly": false,
                "hidden": false
            },
             {
                "name": "escape",
                "title": "Select a single character used for escaping quotes",
                "description": "Select a single character used for escaping quotes inside an already quoted value",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "escapeQuotes",
                "title": "Escape quotes",
                "description": "A flag indicating whether values containing quotes should always be enclosed in quotes",
                "type": "string",
                "enum" : ["true","false"],
                "isRequired": false,
                "default": "true",
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "header",
                "title": "header",
                "description": "Writes the names of columns as the first line.",
                "type": "string",
                "isRequired": false,
                "enum" : ["true","false"],
                "readOnly": false,
                "default": "true",
                "hidden": false
            },
            {
                "name": "ignoreLeadingWhiteSpace",
                "title": "Ignore leading white space",
                "description": "A flag indicating whether or not leading whitespaces from values being written should be skipped.",
                "type": "string",
                "isRequired": false,
                "enum" : ["true","false"],
                "readOnly": false,
                "default": "true",
                "hidden": false
            },
            {
                "name": "nullValue",
                "title": "Select the string representation of a null value",
                "description": "Sets the string representation of a null value. ",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "dateFormat",
                "title": "Date format",
                "description": "Select the string that indicates a date format. ",
                "type": "string",
                "default": "yyyy-MM-dd",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
             {
                "name": "charToEscapeQuoteEscaping",
                "title": "Char to escape quote escaping",
                "description": "Sets a single character used for escaping the escape for the quote character",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "emptyValue",
                "title": "Select the string representation of an empty value",
                "description": "Select the string representation of an empty value",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "default": "",
                "hidden": false
            },
            {
                "name": "compression",
                "title": "Select compression",
                "description": "Select compressiont",
                "type": "string",
                "isRequired": true,
                "readOnly": false,
                "enum" : ["SNAPPY","GZIP","DEFLATE", "NONE"]
            },
            {
                "name": "fileType",
                "title": "Select a fileType",
                "description": "Select fileType",
                "type": "string",
                "isRequired": true,
                "readOnly": false,
                "hidden": false,
                "enum" :["csv", "json", "parquet"],
                "default" : "csv"
            }
        ],
        "uiAttributes": {
            "documentationLink": "https://www.adobe.io/apis/experienceplatform.html",
            "category": "S3",
            "iconUrl": "https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
            "connectionType": "S3",
            "flowRunsSupported": true,
            "monitoringSupported": true,
            "frequency": "Batch"
        },
        "destinationDelivery": [
            {
                "deliveryMatchers" : [
                    {
                        "type" : "SOURCE",
                        "value" : [
                            "batch"
                        ]
                    }
                ],
                "authenticationRule": "CUSTOMER_AUTHENTICATION",
                "destinationServerId": "{{destinationServerId}}"
            }
        ],
        "schemaConfig" : {
            "profileRequired" : true,
            "segmentRequired" : true,
            "identityRequired" : true
        },
        "batchConfig":{
            "allowMandatoryFieldSelection": true,
            "allowJoinKeyFieldSelection": true,
            "defaultExportMode": "DAILY_FULL_EXPORT",
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
        "backfillHistoricalProfileData": true
    }
```

Detaillierte Beschreibungen aller oben genannten Parameter finden Sie unter [Dateibasierte Zielkonfiguration](file-based-destination-configuration.md).

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit Details zu Ihrer neu erstellten Zielkonfiguration zurückgegeben.

## Auflisten der Zielkonfigurationen {#retrieve-list}

Sie können eine Liste aller Zielkonfigurationen für Ihre IMS-Organisation abrufen, indem Sie eine GET-Anfrage an den Endpunkt `/authoring/destinations` stellen.

**API-Format**


```http
GET /authoring/destinations
```

**Anfrage**

Mit der folgenden Anfrage wird die Liste der Zielkonfigurationen abgerufen, auf die Sie Zugriff haben, basierend auf der IMS-Organisation und der Sandbox-Konfiguration.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Die folgende Antwort gibt den HTTP-Status 200 mit einer Liste von Zielkonfigurationen zurück, auf die Sie Zugriff haben, basierend auf der von Ihnen verwendeten IMS-Organisations-ID und dem Sandbox-Namen. Eine `instanceId` entspricht der Vorlage für jeweils ein Ziel. Die Antwort wird verkürzt angegeben.

```json
{
   "items":[
      {
         "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
         "createdDate":"2020-10-28T06:14:09.784471Z",
         "lastModifiedDate":"2021-06-28T06:14:09.784471Z",
         "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
         "sandboxName":"prod",
         "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
         "name":"Moviestar",
         "description":"Moviestar is a fictional destination, used for this example.",
         "status":"TEST",
         "customerAuthenticationConfigurations":[
            {
               "authType":"BEARER"
            }
         ],
         "customerDataFields":[
            {
               "name":"endpointsInstance",
               "type":"string",
               "title":"Select Endpoint",
               "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
               "isRequired":true,
               "enum":[
                  "US",
                  "EU",
                  "APAC",
                  "NZ"
               ]
            },
            {
               "name":"customerID",
               "type":"string",
               "title":"Moviestar Customer ID",
               "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
               "isRequired":true,
               "pattern":"^[A-Za-z]+$"
            }
         ],
         "uiAttributes":{
            "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
            "category":"mobile",
            "connectionType":"Server-to-server",
            "frequency":"Streaming"
         },
         "identityNamespaces":{
            "external_id":{
               "acceptsAttributes":true,
               "acceptsCustomNamespaces":true,
               "acceptedGlobalNamespaces":{
                  "Email":{
                     
                  }
               }
            },
            "another_id":{
               "acceptsAttributes":true,
               "acceptsCustomNamespaces":true
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
                  "name":"a_custom_attribute",
                  "title":"a_custom_attribute",
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
         "aggregation":{
            "aggregationType":"BEST_EFFORT",
            "bestEffortAggregation":{
               "maxUsersPerRequest":10,
               "splitUserById":false
            }
         },
         "destinationDelivery":[
            {
               "authenticationRule":"CUSTOMER_AUTHENTICATION",
               "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
            }
         ],
         "destConfigId":"410631b8-f6b3-4b7c-82da-7998aa3f327c",
         "backfillHistoricalProfileData":true
      }
   ]
}
    
```

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `name` | Zeichenfolge | Gibt den Titel Ihres Ziels im Experience Platform-Katalog an. |
| `description` | Zeichenfolge | Geben Sie eine Beschreibung ein, die Adobe im Zielkatalog von Experience Platform für Ihre Zielkarte verwenden soll. Es sollten nicht mehr als 4–5 Sätze sein. |
| `status` | Zeichenfolge | Gibt den Lebenszyklusstatus der Zielkarte an. Zulässige Werte sind `TEST`, `PUBLISHED` und `DELETED`. Verwenden Sie `TEST`, wenn Sie Ihr Ziel zum ersten Mal konfigurieren. |
| `customerAuthenticationConfigurations` | Zeichenfolge | Gibt die Konfiguration an, die zum Authentifizieren von Experience Platform-Kunden auf Ihrem Server verwendet wird. Siehe `authType` unten für gültige Werte. |
| `customerAuthenticationConfigurations.authType` | Zeichenfolge | Akzeptierte Werte sind `OAUTH2, BEARER`. |
| `customerDataFields.name` | Zeichenfolge | Geben Sie einen Namen für das benutzerdefinierte Feld ein, das Sie einführen. |
| `customerDataFields.type` | Zeichenfolge | Gibt an, welchen Typ von benutzerdefiniertem Feld Sie einführen. Akzeptierte Werte sind `string`, `object` und `integer` |
| `customerDataFields.title` | Zeichenfolge | Gibt den Feldnamen an, wie er von den Kunden in der Benutzeroberfläche von Experience Platform angezeigt wird |
| `customerDataFields.description` | Zeichenfolge | Geben Sie eine Beschreibung für das benutzerdefinierte Feld ein. |
| `customerDataFields.isRequired` | Boolesch | Gibt an, ob dieses Feld im Ziel-Setup-Workflow erforderlich ist. |
| `customerDataFields.enum` | Zeichenfolge | Rendert das benutzerdefinierte Feld als Dropdown-Menü und listet die für den Benutzer verfügbaren Optionen auf. |
| `customerDataFields.pattern` | Zeichenfolge | Erzwingt bei Bedarf ein Muster für das benutzerdefinierte Feld. Verwenden Sie reguläre Ausdrücke, um ein Muster zu erzwingen. Wenn Ihre Kunden-IDs beispielsweise keine Zahlen oder Unterstriche enthalten, geben Sie in dieses Feld `^[A-Za-z]+$` ein. |
| `uiAttributes.documentationLink` | Zeichenfolge | Weitere Informationen finden Sie auf der Dokumentationsseite im [Zielkatalog](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) für Ihr Ziel. Verwenden Sie `https://www.adobe.com/go/destinations-YOURDESTINATION-en`, wobei `YOURDESTINATION` für den Namen Ihres Ziels steht. Für ein Ziel mit dem Namen „Moviestar“ würden Sie `https://www.adobe.com/go/destinations-moviestar-en` verwenden. Beachten Sie, dass dieser Link nur funktioniert, wenn Adobe Ihr Ziel live festlegt und die Dokumentation veröffentlicht wird. |
| `uiAttributes.category` | Zeichenfolge | Bezieht sich auf die Ihrem Ziel in Adobe Experience Platform zugewiesene Kategorie. Weitere Informationen finden Sie unter [Zielkategorien](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories). Verwenden Sie einen der folgenden Werte: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments` |
| `uiAttributes.connectionType` | Zeichenfolge | `Server-to-server` ist derzeit die einzige verfügbare Option. |
| `uiAttributes.frequency` | Zeichenfolge | `Streaming` ist derzeit die einzige verfügbare Option. |
| `identityNamespaces.externalId.acceptsAttributes` | Boolesch | Gibt an, ob Kunden der Identität, die Sie konfigurieren, standardmäßige Profilattribute zuordnen können. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | Boolesch | Gibt an, ob Kunden Identitäten zuordnen können, die zu [benutzerdefinierte Namespaces](/help/identity-service/namespaces.md#manage-namespaces) der Identität, die Sie konfigurieren. |
| `identityNamespaces.externalId.transformation` | Zeichenfolge | _Wird in der Beispielkonfiguration nicht angezeigt_. Wird zum Beispiel verwendet, wenn der [!DNL Platform]-Kunde einfache E-Mail-Adressen als Attribut verwendet und Ihre Plattform nur E-Mails mit Hash akzeptiert. Hier geben Sie die Umwandlung an, die angewendet werden soll (z. B. Umwandlung der E-Mail in Kleinbuchstaben, dann Hash). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | – | Gibt an, [Standard-Identitäts-Namespaces](/help/identity-service/namespaces.md#standard) (z. B. IDFA)-Kunden können der Identität zuordnen, die Sie konfigurieren. <br> Wenn Sie `acceptedGlobalNamespaces` verwenden, können Sie E-Mail-Adressen oder Telefonnummern mithilfe von `"requiredTransformation":"sha256(lower($))"` in Kleinbuchstaben umwandeln und hashen. |
| `destinationDelivery.authenticationRule` | Zeichenfolge | Gibt an, wie [!DNL Platform]-Kunden eine Verbindung zu Ihrem Ziel herstellen. Akzeptierte Werte sind `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Verwenden Sie `CUSTOMER_AUTHENTICATION`, wenn sich Platform-Kunden über einen Benutzernamen und ein Kennwort, ein Träger-Token oder eine andere Authentifizierungsmethode bei Ihrem System anmelden. Sie würden diese Option beispielsweise auswählen, wenn Sie auch `authType: OAUTH2` oder `authType:BEARER` in `customerAuthenticationConfigurations` ausgewählt haben. </li><li> Verwenden Sie `PLATFORM_AUTHENTICATION`, wenn ein globales Authentifizierungssystem zwischen Adobe und Ihrem Ziel existiert und der [!DNL Platform]-Kunde keine Authentifizierungsdaten bereitstellen muss, um eine Verbindung zu Ihrem Ziel herzustellen. In diesem Fall müssen Sie ein Objekt für die [Anmeldeinformationen](./authentication-configuration.md) mithilfe der Konfiguration erstellen. </li><li>Verwenden Sie `NONE`, wenn keine Authentifizierung erforderlich ist, um Daten an Ihre Zielplattform zu senden. </li></ul> |
| `destinationDelivery.destinationServerId` | Zeichenfolge | Die `instanceId` der [Ziel-Server-Vorlage](./destination-server-api.md), die für dieses Ziel verwendet wird. |
| `destConfigId` | Zeichenfolge | Dieses Feld wird automatisch generiert und erfordert keine Eingabe. |
| `backfillHistoricalProfileData` | Boolesch | Steuert, ob historische Profildaten exportiert werden, wenn Segmente für das Ziel aktiviert werden. <br> <ul><li> `true`: [!DNL Platform] sendet die historischen Benutzerprofile, die sich für das Segment qualifiziert haben, bevor das Segment aktiviert wird. </li><li> `false`: [!DNL Platform] enthält nur Benutzerprofile, die sich für das Segment qualifizieren, nachdem das Segment aktiviert wurde. </li></ul> |
| `segmentMappingConfig.mapUserInput` | Boolesch | Steuert, ob die Segmentzuordnungs-ID im Zielaktivierungs-Workflow vom Benutzer eingegeben wird. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | Boolesch | Steuert, ob die Segmentzuordnungs-ID im Zielaktivierungs-Workflow die Experience Platform-Segment-ID ist. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | Boolesch | Steuert, ob die Segmentzuordnungs-ID im Zielaktivierungs-Workflow der Experience Platform-Segmentname ist. |
| `segmentMappingConfig.audienceTemplateId` | Boolesch | Die `instanceId` der [Zielgruppen-Metadatenvorlage](./audience-metadata-management.md), die für dieses Ziel verwendet wird. Weitere Informationen zum Einrichten einer Zielgruppen-Metadatenvorlage finden Sie in der [API-Referenz für Zielgruppen-Metadaten](./audience-metadata-api.md). |

{style=&quot;table-layout:auto&quot;}

## Aktualisieren einer vorhandenen Zielkonfiguration {#update}

Sie können eine bestehende Zielkonfiguration aktualisieren, indem Sie eine PUT-Anfrage an den Endpunkt `/authoring/destinations` stellen und die Instanz-ID der Zielkonfiguration angeben, die Sie aktualisieren möchten. Geben Sie im Text des Aufrufs die aktualisierte Zielkonfiguration an.

**API-Format**


```http
PUT /authoring/destinations/{INSTANCE_ID}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{INSTANCE_ID}` | Die ID der Zielkonfiguration, die Sie aktualisieren möchten. |

**Anfrage**

Die folgende Anfrage aktualisiert eine vorhandene Zielkonfiguration, die durch die in der Payload angegebenen Parameter konfiguriert wird. Im folgenden Beispielaufruf aktualisieren wir die [früher erstellte](./destination-configuration-api.md#create) Konfiguration, um nun GAID-, IDFA- und Hash-E-Mail-IDs als Identitäts-Namespaces zu akzeptieren.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
   "createdDate":"2020-10-28T06:14:09.784471Z",
   "lastModifiedDate":"2021-04-28T06:14:09.784471Z",
   "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
   "sandboxName":"prod",
   "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"endpointsInstance",
         "type":"string",
         "title":"Select Endpoint",
         "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
         "isRequired":true,
         "enum":[
            "US",
            "EU",
            "APAC",
            "NZ"
         ]
      },
      {
         "name":"customerID",
         "type":"string",
         "title":"Moviestar Customer ID",
         "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "gaid":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "GAID":{
               
            }
         }
      },
      "idfa":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "IDFA":{
               
            }
         }
      },
      "email_lc_sha256":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation":"sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation":"sha256(lower($))"
            },
            "Email_LC_SHA256":{
               
            }
         }
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
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
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
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```

## Abrufen einer bestimmten Zielkonfiguration {#get}

Sie können detaillierte Informationen über eine bestimmte Zielkonfiguration abrufen, indem Sie eine GET-Anfrage an den Endpunkt `/authoring/destinations` stellen und die Instanz-ID der gewünschten Zielkonfiguration angeben.

**API-Format**


```http
GET /authoring/destinations/{INSTANCE_ID}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{INSTANCE_ID}` | Die ID der Zielkonfiguration, die Sie abrufen möchten. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit detaillierten Informationen zur angegebenen Zielkonfiguration zurückgegeben.

```json
{
   "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
   "createdDate":"2020-10-28T06:14:09.784471Z",
   "lastModifiedDate":"2021-06-04T06:14:09.784471Z",
   "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
   "sandboxName":"prod",
   "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"endpointsInstance",
         "type":"string",
         "title":"Select Endpoint",
         "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
         "isRequired":true,
         "enum":[
            "US",
            "EU",
            "APAC",
            "NZ"
         ]
      },
      {
         "name":"customerID",
         "type":"string",
         "title":"Moviestar Customer ID",
         "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
               
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "gaid":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "GAID":{
               
            }
         }
      },
      "idfa":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "IDFA":{
               
            }
         }
      },
      "email_lc_sha256":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation":"sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation":"sha256(lower($))"
            },
            "Email_LC_SHA256":{
               
            }
         }
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
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
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
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```


## Löschen einer bestimmten Zielkonfiguration {#delete}

Sie können die angegebene Zielkonfiguration löschen, indem Sie eine DELETE-Anfrage an den Endpunkt `/authoring/destinations` stellen und die ID der Zielkonfiguration, die Sie löschen möchten, im Abfragepfad angeben.

**API-Format**

```http
DELETE /authoring/destinations/{INSTANCE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{INSTANCE_ID}` | Die `id` der Zielkonfiguration, die Sie löschen möchten. |

**Anfrage**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 zusammen mit einer leeren HTTP-Antwort zurück.

## Umgang mit API-Fehlern

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status-Codes](../../landing/troubleshooting.md#api-status-codes) und [Fehler im Anfrage-Header](../../landing/troubleshooting.md#request-header-errors) in der Anleitung zur Fehlerbehebung für Platform.

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie Ihr Ziel mithilfe des API-Endpunkts `/authoring/destinations` konfigurieren können. Lesen Sie [Verwenden des Destination SDK zum Konfigurieren Ihres Ziels](./configure-destination-instructions.md), um zu verstehen, wo dieser Schritt in den Prozess der Konfiguration Ihres Ziels passt.
