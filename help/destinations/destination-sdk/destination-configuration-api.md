---
description: Auf dieser Seite werden alle API-Vorgänge aufgelistet und beschrieben, die Sie mit dem API-Endpunkt "/authoring/destinations"ausführen können.
title: API-Endpunktvorgänge für Ziele
exl-id: 96755e9d-be62-432f-b985-91330575b395
source-git-commit: 76a596166edcdbf141b5ce5dc01557d2a0b4caf3
workflow-type: tm+mt
source-wordcount: '2405'
ht-degree: 6%

---

# API-Vorgänge für Ziel-Endpunkte {#destination-configuration}

>[!IMPORTANT]
>
>**API-Endpunkt**: `platform.adobe.io/data/core/activation/authoring/destinations`

Auf dieser Seite werden alle API-Vorgänge aufgelistet und beschrieben, die Sie mit dem API-Endpunkt `/authoring/destinations` ausführen können. Eine Beschreibung der von diesem Endpunkt unterstützten Funktionen finden Sie unter [Zielkonfiguration](./destination-configuration.md).

## Erste Schritte mit Ziel-API-Vorgängen {#get-started}

Bevor Sie fortfahren, lesen Sie zunächst das [Erste-Schritte-Handbuch](./getting-started.md) , um wichtige Informationen zu erhalten, die Sie benötigen, um die API erfolgreich aufrufen zu können. Dazu gehören das Abrufen der erforderlichen Zielerstellungsberechtigung und der erforderlichen Kopfzeilen.

## Erstellen einer Konfiguration für ein Ziel {#create}

Sie können eine neue Zielkonfiguration erstellen, indem Sie eine POST-Anfrage an den Endpunkt `/authoring/destinations` senden.

**API-Format**


```http
POST /authoring/destinations
```

**Anfrage**

Die folgende Anfrage erstellt eine neue Zielkonfiguration, die durch die in der Payload bereitgestellten Parameter konfiguriert wird. Die nachstehende Payload enthält alle Parameter, die vom Endpunkt `/authoring/destinations` akzeptiert werden. Beachten Sie, dass Sie nicht alle Parameter für den Aufruf hinzufügen müssen und dass die Vorlage entsprechend Ihren API-Anforderungen angepasst werden kann.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | Zeichenfolge | Gibt den Titel Ihres Ziels im Experience Platform-Katalog an |
| `description` | Zeichenfolge | Geben Sie eine Beschreibung ein, die Adobe im Zielkatalog der Experience Platform für Ihre Zielkarte verwendet. Ziel für maximal 4-5 Sätze. |
| `status` | Zeichenfolge | Gibt den Lebenszyklusstatus der Zielkarte an. Zulässige Werte sind `TEST`, `PUBLISHED` und `DELETED`. Verwenden Sie `TEST`, wenn Sie Ihr Ziel zum ersten Mal konfigurieren. |
| `customerAuthenticationConfigurations` | Zeichenfolge | Gibt die Konfiguration an, die zum Authentifizieren von Experience Platform-Kunden auf Ihrem Server verwendet wird. Zulässige Werte finden Sie unten unter `authType` . |
| `customerAuthenticationConfigurations.authType` | Zeichenfolge | Akzeptierte Werte sind `OAUTH2, BEARER`. |
| `customerDataFields.name` | Zeichenfolge | Geben Sie einen Namen für das benutzerdefinierte Feld ein, das Sie einführen. |
| `customerDataFields.type` | Zeichenfolge | Gibt an, welchen Typ von benutzerdefiniertem Feld Sie einführen. Akzeptierte Werte sind `string`, `object`, `integer` |
| `customerDataFields.title` | Zeichenfolge | Gibt den Feldnamen an, wie er von den Kunden in der Experience Platform-Benutzeroberfläche angezeigt wird |
| `customerDataFields.description` | Zeichenfolge | Geben Sie eine Beschreibung für das benutzerdefinierte Feld ein. |
| `customerDataFields.isRequired` | Boolesch | Gibt an, ob dieses Feld im Ziel-Setup-Workflow erforderlich ist. |
| `customerDataFields.enum` | Zeichenfolge | Rendert das benutzerdefinierte Feld als Dropdown-Menü und listet die für den Benutzer verfügbaren Optionen auf. |
| `customerDataFields.pattern` | Zeichenfolge | Erzwingt bei Bedarf ein Muster für das benutzerdefinierte Feld. Verwenden Sie reguläre Ausdrücke, um ein Muster zu erzwingen. Wenn Ihre Kunden-IDs beispielsweise keine Zahlen oder Unterstriche enthalten, geben Sie `^[A-Za-z]+$` in dieses Feld ein. |
| `uiAttributes.documentationLink` | Zeichenfolge | Bezieht sich auf die Dokumentationsseite im [Zielkatalog](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) für Ihr Ziel. Verwenden Sie `https://www.adobe.com/go/destinations-YOURDESTINATION-en`, wobei `YOURDESTINATION` der Name Ihres Ziels ist. Für ein Ziel mit dem Namen Moviestar würden Sie `https://www.adobe.com/go/destinations-moviestar-en` verwenden. |
| `uiAttributes.category` | Zeichenfolge | Bezieht sich auf die Ihrem Ziel in Adobe Experience Platform zugewiesene Kategorie. Weitere Informationen finden Sie unter [Zielkategorien](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories). Verwenden Sie einen der folgenden Werte: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `uiAttributes.connectionType` | Zeichenfolge | `Server-to-server` ist derzeit die einzige verfügbare Option. |
| `uiAttributes.frequency` | Zeichenfolge | `Streaming` ist derzeit die einzige verfügbare Option. |
| `identityNamespaces.externalId.acceptsAttributes` | Boolesch | Gibt an, ob Ihr Ziel Standardprofilattribute akzeptiert. Normalerweise werden diese Attribute in der Dokumentation unserer Partner hervorgehoben. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | Boolesch | Gibt an, ob Kunden benutzerdefinierte Namespaces in Ihrem Ziel einrichten können. |
| `identityNamespaces.externalId.allowedAttributesTransformation` | Zeichenfolge | _Wird in der Beispielkonfiguration_ nicht angezeigt. Wird beispielsweise verwendet, wenn der [!DNL Platform]-Kunde einfache E-Mail-Adressen als Attribut hat und Ihre Plattform nur Hash-E-Mails akzeptiert. Hier geben Sie die Konvertierung an, die angewendet werden muss (konvertieren Sie beispielsweise die E-Mail in Kleinbuchstaben und dann den Hash). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | – | Wird in Fällen verwendet, in denen Ihre Plattform [standardmäßige Identitäts-Namespaces](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces) akzeptiert (z. B. IDFA), sodass Sie Platform-Benutzer auf die Auswahl dieser Identitäts-Namespaces beschränken können. <br> Wenn Sie  `acceptedGlobalNamespaces`verwenden, können Sie  `"requiredTransformation":"sha256(lower($))"` zu Kleinbuchstaben und Hash-E-Mail-Adressen oder Telefonnummern verwenden. |
| `destinationDelivery.authenticationRule` | Zeichenfolge | Gibt an, wie [!DNL Platform]-Kunden eine Verbindung zu Ihrem Ziel herstellen. Akzeptierte Werte sind `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Verwenden Sie `CUSTOMER_AUTHENTICATION` , wenn sich Platform-Kunden über einen Benutzernamen und ein Kennwort, ein Trägertoken oder eine andere Authentifizierungsmethode bei Ihrem System anmelden. Sie würden diese Option beispielsweise auswählen, wenn Sie auch `authType: OAUTH2` oder `authType:BEARER` in `customerAuthenticationConfigurations` ausgewählt haben. </li><li> Verwenden Sie `PLATFORM_AUTHENTICATION`, wenn ein globales Authentifizierungssystem zwischen Adobe und Ihrem Ziel vorhanden ist und der [!DNL Platform]-Kunde keine Authentifizierungsberechtigungen angeben muss, um eine Verbindung zu Ihrem Ziel herzustellen. In diesem Fall müssen Sie mithilfe der Konfiguration [Credentials](./credentials-configuration.md) ein Anmeldedatenobjekt erstellen. </li><li>Verwenden Sie `NONE` , wenn keine Authentifizierung erforderlich ist, um Daten an Ihre Zielplattform zu senden. </li></ul> |
| `destinationDelivery.destinationServerId` | Zeichenfolge | Die `instanceId` der [Zielservervorlage](./destination-server-api.md), die für dieses Ziel verwendet wird. |
| `backfillHistoricalProfileData` | Boolesch | Steuert, ob historische Profildaten exportiert werden, wenn Segmente für das Ziel aktiviert werden. <br> <ul><li> `true`:  [!DNL Platform] sendet die historischen Benutzerprofile, die sich für das Segment qualifiziert haben, bevor das Segment aktiviert wird. </li><li> `false`:  [!DNL Platform] enthält nur Benutzerprofile, die sich für das Segment qualifizieren, nachdem das Segment aktiviert wurde. </li></ul> |
| `segmentMappingConfig.mapUserInput` | Boolesch | Steuert, ob die Segmentzuordnungs-ID im Zielaktivierungs-Workflow vom Benutzer eingegeben wird. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | Boolesch | Steuert, ob die Segmentzuordnungs-ID im Zielaktivierungs-Workflow die Experience Platform-Segment-ID ist. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | Boolesch | Steuert, ob die Segmentzuordnungs-ID im Zielaktivierungs-Workflow der Experience Platform-Segmentname ist. |
| `segmentMappingConfig.audienceTemplateId` | Boolesch | Die `instanceId` der [Zielgruppen-Metadatenvorlage](./audience-metadata-api.md), die für dieses Ziel verwendet wird. |
| `schemaConfig.profileFields` | Array | Wenn Sie vordefinierte `profileFields` hinzufügen, wie in der obigen Konfiguration dargestellt, haben die Benutzer die Möglichkeit, die Attribute der Experience Platform den vordefinierten Attributen auf der Zielseite zuzuordnen. |
| `schemaConfig.profileRequired` | Boolesch | Verwenden Sie `true` , wenn Benutzer Profilattribute von der Experience Platform benutzerdefinierten Attributen auf der Zielseite zuordnen können sollen, wie in der obigen Beispielkonfiguration dargestellt. |
| `schemaConfig.segmentRequired` | Boolesch | Verwenden Sie immer `segmentRequired:true`. |
| `schemaConfig.identityRequired` | Boolesch | Verwenden Sie `true` , wenn Benutzer Identitäts-Namespaces von Experience Platform Ihrem gewünschten Schema zuordnen können sollen. |
| `aggregation.aggregationType` | – | Klicken Sie entweder auf `BEST_EFFORT` oder auf `CONFIGURABLE_AGGREGATION`. Die obige Beispielkonfiguration umfasst die Aggregation `BEST_EFFORT` . Ein Beispiel für `CONFIGURABLE_AGGREGATION` finden Sie in der Beispielkonfiguration im Dokument [Zielkonfiguration](./destination-configuration.md#example-configuration) . Die für die konfigurierbare Aggregation relevanten Parameter sind nachfolgend in dieser Tabelle beschrieben. |
| `aggregation.bestEffortAggregation.maxUsersPerRequest` | Ganzzahl | Experience Platform kann mehrere exportierte Profile in einem einzigen HTTP-Aufruf aggregieren. Geben Sie die maximale Anzahl von Profilen an, die Ihr Endpunkt in einem einzelnen HTTP-Aufruf erhalten soll. Beachten Sie, dass dies eine Aggregation mit dem besten Aufwand ist. Wenn Sie beispielsweise den Wert 100 angeben, kann Platform eine beliebige Anzahl von Profilen senden, die kleiner als 100 sind. <br> Wenn Ihr Server nicht mehrere Benutzer pro Anforderung akzeptiert, setzen Sie diesen Wert auf 1. |
| `aggregation.bestEffortAggregation.splitUserById` | Boolesch | Verwenden Sie dieses Flag, wenn der Aufruf an das Ziel nach Identität aufgeteilt werden soll. Setzen Sie dieses Flag auf `true` , wenn Ihr Server für einen bestimmten Namespace nur eine Identität pro Aufruf akzeptiert. |
| `aggregation.configurableAggregation.splitUserById` | Boolesch | Siehe Parameter in Beispielkonfiguration [hier](./destination-configuration.md#example-configuration). Verwenden Sie dieses Flag, wenn der Aufruf an das Ziel nach Identität aufgeteilt werden soll. Setzen Sie dieses Flag auf `true` , wenn Ihr Server für einen bestimmten Namespace nur eine Identität pro Aufruf akzeptiert. |
| `aggregation.configurableAggregation.maxBatchAgeInSecs` | Ganzzahl | *Höchstwert: 3600*. Siehe Parameter in Beispielkonfiguration [hier](./destination-configuration.md#example-configuration). Zusammen mit `maxNumEventsInBatch` bestimmt dies, wie lange die Experience Platform warten soll, bis ein API-Aufruf an Ihren Endpunkt gesendet wird. <br> Wenn Sie beispielsweise den Maximalwert für beide Parameter verwenden, wartet die Experience Platform entweder 3600 Sekunden ODER, bis 10.000 qualifizierte Profile vorhanden sind, bevor der API-Aufruf erfolgt (je nachdem, was früher eintritt). |
| `aggregation.configurableAggregation.maxNumEventsInBatch` | Ganzzahl | *Höchstwert: 10000*. Siehe Parameter in Beispielkonfiguration [hier](./destination-configuration.md#example-configuration). Siehe `maxBatchAgeInSecs` oben. |
| `aggregation.configurableAggregation.aggregationKey` | Boolesch | Siehe Parameter in Beispielkonfiguration [hier](./destination-configuration.md#example-configuration). Ermöglicht die Aggregation der dem Ziel zugeordneten exportierten Profile anhand der folgenden Parameter: <br> <ul><li>Segment-ID</li><li> Segmentstatus </li><li> Identitäts-Namespace </li></ul> |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentId` | Boolesch | Siehe Parameter in Beispielkonfiguration [hier](./destination-configuration.md#example-configuration). Setzen Sie dies auf `true` , wenn Sie Profile gruppieren möchten, die nach Segment-ID an Ihr Ziel exportiert wurden. |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentStatus` | Boolesch | Siehe Parameter in Beispielkonfiguration [hier](./destination-configuration.md#example-configuration). Sie müssen sowohl `includeSegmentId:true` als auch `includeSegmentStatus:true` festlegen, wenn Sie Profile gruppieren möchten, die nach Segment-ID UND Segmentstatus in Ihr Ziel exportiert wurden. |
| `aggregation.configurableAggregation.aggregationKey.includeIdentity` | Boolesch | Siehe Parameter in Beispielkonfiguration [hier](./destination-configuration.md#example-configuration). Setzen Sie dies auf `true` , wenn Sie Profile gruppieren möchten, die nach Identitäts-Namespace an Ihr Ziel exportiert wurden. |
| `aggregation.configurableAggregation.aggregationKey.oneIdentityPerGroup` | Boolesch | Siehe Parameter in Beispielkonfiguration [hier](./destination-configuration.md#example-configuration). Verwenden Sie diesen Parameter, um anzugeben, ob die exportierten Profile in Gruppen einer Identität zusammengefasst werden sollen (GAID, IDFA, Telefonnummern, E-Mail usw.). |
| `aggregation.configurableAggregation.aggregationKey.groups` | Zeichenfolge | Siehe Parameter in Beispielkonfiguration [hier](./destination-configuration.md#example-configuration). Erstellen Sie Listen mit Identitätsgruppen, wenn Sie Profile gruppieren möchten, die nach Gruppen von Identitäts-Namespace in Ihr Ziel exportiert wurden. Beispielsweise können Sie Profile, die die IDs für Mobilgeräte IDFA und GAID enthalten, mithilfe der im Beispiel beschriebenen Konfiguration zu einem Aufruf an Ihr Ziel und zu E-Mails zu einem anderen kombinieren. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zur neu erstellten Zielkonfiguration zurück.

## Zielkonfigurationen auflisten {#retrieve-list}

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
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Die folgende Antwort gibt den HTTP-Status 200 mit einer Liste von Zielkonfigurationen zurück, auf die Sie Zugriff haben, basierend auf der von Ihnen verwendeten IMS-Organisations-ID und dem Sandbox-Namen. Ein `instanceId` entspricht der Vorlage für ein Ziel. Die Antwort wird aus Gründen der Kürze abgeschnitten.

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
| `description` | Zeichenfolge | Geben Sie eine Beschreibung ein, die Adobe im Zielkatalog der Experience Platform für Ihre Zielkarte verwendet. Ziel für maximal 4-5 Sätze. |
| `status` | Zeichenfolge | Gibt den Lebenszyklusstatus der Zielkarte an. Zulässige Werte sind `TEST`, `PUBLISHED` und `DELETED`. Verwenden Sie `TEST`, wenn Sie Ihr Ziel zum ersten Mal konfigurieren. |
| `customerAuthenticationConfigurations` | Zeichenfolge | Gibt die Konfiguration an, die zum Authentifizieren von Experience Platform-Kunden auf Ihrem Server verwendet wird. Zulässige Werte finden Sie unten unter `authType` . |
| `customerAuthenticationConfigurations.authType` | Zeichenfolge | Akzeptierte Werte sind `OAUTH2, BEARER`. |
| `customerDataFields.name` | Zeichenfolge | Geben Sie einen Namen für das benutzerdefinierte Feld ein, das Sie einführen. |
| `customerDataFields.type` | Zeichenfolge | Gibt an, welchen Typ von benutzerdefiniertem Feld Sie einführen. Akzeptierte Werte sind `string`, `object`, `integer` |
| `customerDataFields.title` | Zeichenfolge | Gibt den Feldnamen an, wie er von den Kunden in der Experience Platform-Benutzeroberfläche angezeigt wird |
| `customerDataFields.description` | Zeichenfolge | Geben Sie eine Beschreibung für das benutzerdefinierte Feld ein. |
| `customerDataFields.isRequired` | Boolesch | Gibt an, ob dieses Feld im Ziel-Setup-Workflow erforderlich ist. |
| `customerDataFields.enum` | Zeichenfolge | Rendert das benutzerdefinierte Feld als Dropdown-Menü und listet die für den Benutzer verfügbaren Optionen auf. |
| `customerDataFields.pattern` | Zeichenfolge | Erzwingt bei Bedarf ein Muster für das benutzerdefinierte Feld. Verwenden Sie reguläre Ausdrücke, um ein Muster zu erzwingen. Wenn Ihre Kunden-IDs beispielsweise keine Zahlen oder Unterstriche enthalten, geben Sie `^[A-Za-z]+$` in dieses Feld ein. |
| `uiAttributes.documentationLink` | Zeichenfolge | Bezieht sich auf die Dokumentationsseite im [Zielkatalog](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) für Ihr Ziel. Verwenden Sie `https://www.adobe.com/go/destinations-YOURDESTINATION-en`, wobei `YOURDESTINATION` der Name Ihres Ziels ist. Für ein Ziel mit dem Namen Moviestar würden Sie `https://www.adobe.com/go/destinations-moviestar-en` verwenden. |
| `uiAttributes.category` | Zeichenfolge | Bezieht sich auf die Ihrem Ziel in Adobe Experience Platform zugewiesene Kategorie. Weitere Informationen finden Sie unter [Zielkategorien](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories). Verwenden Sie einen der folgenden Werte: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments` |
| `uiAttributes.connectionType` | Zeichenfolge | `Server-to-server` ist derzeit die einzige verfügbare Option. |
| `uiAttributes.frequency` | Zeichenfolge | `Streaming` ist derzeit die einzige verfügbare Option. |
| `identityNamespaces.externalId.acceptsAttributes` | Boolesch | Gibt an, ob Ihr Ziel Standardprofilattribute akzeptiert. Normalerweise werden diese Attribute in der Dokumentation unserer Partner hervorgehoben. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | Boolesch | Gibt an, ob Kunden benutzerdefinierte Namespaces in Ihrem Ziel einrichten können. Weitere Informationen zu [benutzerdefinierten Namespaces](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#manage-namespaces) in Adobe Experience Platform. |
| `identityNamespaces.externalId.allowedAttributesTransformation` | Zeichenfolge | _Wird in der Beispielkonfiguration_ nicht angezeigt. Wird beispielsweise verwendet, wenn der [!DNL Platform]-Kunde einfache E-Mail-Adressen als Attribut hat und Ihre Plattform nur Hash-E-Mails akzeptiert. Hier geben Sie die Konvertierung an, die angewendet werden muss (konvertieren Sie beispielsweise die E-Mail in Kleinbuchstaben und dann den Hash). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | – | Wird in Fällen verwendet, in denen Ihre Plattform [standardmäßige Identitäts-Namespaces](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces) akzeptiert (z. B. IDFA), sodass Sie Platform-Benutzer auf die Auswahl dieser Identitäts-Namespaces beschränken können. |
| `destinationDelivery.authenticationRule` | Zeichenfolge | Gibt an, wie [!DNL Platform]-Kunden eine Verbindung zu Ihrem Ziel herstellen. Akzeptierte Werte sind `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Verwenden Sie `CUSTOMER_AUTHENTICATION` , wenn sich Platform-Kunden über einen Benutzernamen und ein Kennwort, ein Trägertoken oder eine andere Authentifizierungsmethode bei Ihrem System anmelden. Sie würden diese Option beispielsweise auswählen, wenn Sie auch `authType: OAUTH2` oder `authType:BEARER` in `customerAuthenticationConfigurations` ausgewählt haben. </li><li> Verwenden Sie `PLATFORM_AUTHENTICATION`, wenn ein globales Authentifizierungssystem zwischen Adobe und Ihrem Ziel vorhanden ist und der [!DNL Platform]-Kunde keine Authentifizierungsberechtigungen angeben muss, um eine Verbindung zu Ihrem Ziel herzustellen. In diesem Fall müssen Sie mithilfe der Konfiguration [Credentials](./credentials-configuration.md) ein Anmeldedatenobjekt erstellen. </li><li>Verwenden Sie `NONE` , wenn keine Authentifizierung erforderlich ist, um Daten an Ihre Zielplattform zu senden. </li></ul> |
| `destinationDelivery.destinationServerId` | Zeichenfolge | Die `instanceId` der [Zielservervorlage](./destination-server-api.md), die für dieses Ziel verwendet wird. |
| `destConfigId` | Zeichenfolge | Dieses Feld wird automatisch generiert und erfordert keine Eingabe. |
| `backfillHistoricalProfileData` | Boolesch | Steuert, ob historische Profildaten exportiert werden, wenn Segmente für das Ziel aktiviert werden. <br> <ul><li> `true`:  [!DNL Platform] sendet die historischen Benutzerprofile, die sich für das Segment qualifiziert haben, bevor das Segment aktiviert wird. </li><li> `false`:  [!DNL Platform] enthält nur Benutzerprofile, die sich für das Segment qualifizieren, nachdem das Segment aktiviert wurde. </li></ul> |
| `segmentMappingConfig.mapUserInput` | Boolesch | Steuert, ob die Segmentzuordnungs-ID im Zielaktivierungs-Workflow vom Benutzer eingegeben wird. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | Boolesch | Steuert, ob die Segmentzuordnungs-ID im Zielaktivierungs-Workflow die Experience Platform-Segment-ID ist. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | Boolesch | Steuert, ob die Segmentzuordnungs-ID im Zielaktivierungs-Workflow der Experience Platform-Segmentname ist. |
| `segmentMappingConfig.audienceTemplateId` | Boolesch | Die `instanceId` der [Zielgruppen-Metadatenvorlage](./audience-metadata-management.md), die für dieses Ziel verwendet wird. Lesen Sie zum Einrichten einer Audience-Metadatenvorlage den [API-Verweis für Zielgruppen-Metadaten](./audience-metadata-api.md). |

{style=&quot;table-layout:auto&quot;}

## Vorhandene Zielkonfiguration aktualisieren {#update}

Sie können eine bestehende Zielkonfiguration aktualisieren, indem Sie eine PUT-Anfrage an den `/authoring/destinations`-Endpunkt senden und die Instanz-ID der Zielkonfiguration angeben, die Sie aktualisieren möchten. Geben Sie im Text des Aufrufs die aktualisierte Zielkonfiguration an.

**API-Format**


```http
PUT /authoring/destinations/{INSTANCE_ID}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{INSTANCE_ID}` | Die ID der Zielkonfiguration, die Sie aktualisieren möchten. |

**Anfrage**

Die folgende Anfrage aktualisiert eine vorhandene Zielkonfiguration, die durch die in der Payload bereitgestellten Parameter konfiguriert wird. Im folgenden Beispielaufruf aktualisieren wir die zuvor erstellte Konfiguration [a1/>, um nun GAID-, IDFA- und Hash-E-Mail-IDs als Identitäts-Namespaces zu akzeptieren.](./destination-configuration-api.md#create)

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

## Bestimmte Zielkonfiguration abrufen {#get}

Sie können detaillierte Informationen zu einer bestimmten Zielkonfiguration abrufen, indem Sie eine GET-Anfrage an den Endpunkt `/authoring/destinations` senden und die Instanz-ID der Zielkonfiguration angeben, die Sie abrufen möchten.

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
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit detaillierten Informationen zur angegebenen Zielkonfiguration zurück.

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

Sie können die angegebene Zielkonfiguration löschen, indem Sie eine DELETE-Anfrage an den Endpunkt `/authoring/destinations` senden und im Anfragepfad die Kennung der Zielkonfiguration angeben, die Sie löschen möchten.

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
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 zusammen mit einer leeren HTTP-Antwort zurück.

## Umgang mit API-Fehlern

Die Ziel-SDK-API-Endpunkte folgen den allgemeinen Grundsätzen der Experience Platform API-Fehlermeldung. Weitere Informationen finden Sie unter [API-Status-Codes](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) und [Fehler in der Anforderungsheader](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) im Handbuch zur Fehlerbehebung für Platform.

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie Ihr Ziel mithilfe des API-Endpunkts `/authoring/destinations` konfigurieren. Lesen Sie [wie Sie das Ziel-SDK verwenden, um Ihr Ziel zu konfigurieren](./configure-destination-instructions.md), um zu verstehen, wo dieser Schritt in den Prozess der Konfiguration Ihres Ziels passt.
