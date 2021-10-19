---
description: Diese Seite Liste und beschreibt die Schritte zum Konfigurieren eines Streaming-Ziels mit dem Ziel-SDK.
title: Verwenden von Destination SDK zum Konfigurieren eines Streaming-Ziels
exl-id: d8aa7353-ba55-4a0d-81c4-ea2762387638
source-git-commit: a7c36f1a157b6020fede53e5c1074d966f26cf3d
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 0%

---

# Verwenden von Destination SDK zum Konfigurieren eines Streaming-Ziels

## Übersicht {#overview}

Diese Seite beschreibt die Verwendung der Informationen in [Konfigurationsoptionen im Ziel-SDK](./configuration-options.md) und in anderen Ziel-SDK-Funktionen und API-Referenzfunktionen, um eine [Streaming-Ziel](/help/destinations/destination-types.md#streaming-destinations). Die Schritte sind in der folgenden Reihenfolge angeordnet.

>[!NOTE]
>
>Das Konfigurieren eines Stapelziels über das Ziel-SDK wird derzeit nicht unterstützt.

## Voraussetzungen {#prerequisites}

Bevor Sie zu den unten dargestellten Schritten fortfahren, lesen Sie bitte die [Start des Ziel-SDK](./getting-started.md) Informationen zum Erhalt der erforderlichen Anmeldedaten für die Authentifizierung der Adobe I/O und anderer Voraussetzungen für die Arbeit mit Ziel-SDK-APIs.

## Schritte zum Verwenden der Konfigurationsoptionen im Ziel-SDK, um Ihr Ziel einzurichten {#steps}

![Veranschaulichte Schritte zur Verwendung der Ziel-SDK-Endpunkte](./assets/destination-sdk-steps.png)

## Schritt 1: Server- und Vorlagenkonfiguration erstellen {#create-server-template-configuration}

Beginn durch Erstellen einer Server- und Vorlagenkonfiguration mit `/destinations-server` Endpunkt (lesen [API-Verweis](./destination-server-api.md)). Weitere Informationen zur Server- und Vorlagenkonfiguration finden Sie unter [Server- und Vorlagenspezifikationen](./configuration-options.md#server-and-template) im Referenzabschnitt.

Im Folgenden finden Sie eine Beispielkonfiguration. Beachten Sie, dass die Umwandlungsvorlage der Nachricht in `requestBody.value` Parameter wird in Schritt 3 angesprochen; [Umwandlungsvorlage erstellen](./configure-destination-instructions.md#create-transformation-template).

```json
POST platform.adobe.io/data/core/activation/authoring/destination-servers

{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"insert after you create a template in step 3"
      },
      "contentType":"application/json"
   }
}
```

## Schritt 2: Zielkonfiguration erstellen {#create-destination-configuration}

Unten wird eine Beispielkonfiguration für eine Zielvorlage angezeigt, die mithilfe der `/destinations` API-Endpunkt. Weitere Informationen zu dieser Vorlage finden Sie unter [Zielkonfiguration](./destination-configuration.md).

Um die Server- und Vorlagenkonfiguration in Schritt 1 mit dieser Zielkonfiguration zu verbinden, fügen Sie die Instanz-ID des Servers und der Vorlagenkonfiguration als `destinationServerId` hier.

```json
POST platform.adobe.io/data/core/activation/authoring/destinations
 
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
         "pattern":""
      }
   ],
   "uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
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
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "aggregationPolicyId":null,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":true,
            "groups":null
         },
         "splitUserById":true,
         "maxBatchAgeInSecs":360,
         "maxNumEventsInBatch":100
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ]
}
```

## Schritt 3: Umwandlungsvorlage zum Erstellen von Nachrichten - Verwenden Sie die Vorlagensprache, um das Format der Nachrichtenausgabe anzugeben. {#create-transformation-template}

Basierend auf den Nutzlasten, die Ihr Ziel unterstützt, müssen Sie eine Vorlage erstellen, die das Format der exportierten Daten aus dem XDM-Format der Adobe in ein von Ihrem Ziel unterstütztes Format transformiert. Siehe Vorlagenbeispiele im Abschnitt [Verwenden einer Vorlagensprache für Identitäts-, Attribute- und Segmentmitgliedstransformationen](./message-format.md#using-templating) und verwenden Sie [Vorlagen-Authoring-Tool](./create-template.md) bereitgestellt von der Adobe.

Nachdem Sie eine für Sie funktionierende Umwandlungsvorlage erstellt haben, fügen Sie sie der in Schritt 1 erstellten Server- und Vorlagenkonfiguration hinzu.

## Schritt 4: Audience-Metadatenkonfiguration erstellen {#create-audience-metadata-configuration}

Für einige Ziele erfordert das Ziel-SDK die Konfiguration einer Audience-Metadatenkonfiguration, um Audiencen in Ihrem Ziel programmgesteuert zu erstellen, zu aktualisieren oder zu löschen. Siehe [Audience-Metadatenverwaltung](./audience-metadata-management.md) für Informationen darüber, wann Sie diese Konfiguration einrichten müssen und wie Sie sie durchführen.

Wenn Sie eine Audience-Metadatenkonfiguration verwenden, müssen Sie sie mit der Zielkonfiguration verbinden, die Sie in Schritt 2 erstellt haben. hinzufügen Sie die Instanz-ID Ihrer Audience-Metadatenkonfiguration in Ihrer Zielkonfiguration als `audienceTemplateId`.

## Schritt 5: Anmeldeinformationen erstellen/Authentifizierung einrichten {#set-up-authentication}

Je nachdem, ob Sie `"authenticationRule": "CUSTOMER_AUTHENTICATION"` oder `"authenticationRule": "PLATFORM_AUTHENTICATION"` in der oben stehenden Zielkonfiguration können Sie die Authentifizierung für Ihr Ziel einrichten, indem Sie `/destination` oder `/credentials` Endpunkt.

* **Häufigster Fall**: Bei Auswahl von `"authenticationRule": "CUSTOMER_AUTHENTICATION"` in der Zielkonfiguration und Ihr Ziel unterstützt die OAuth 2-Authentifizierungsmethode, lesen Sie [OAuth 2-Authentifizierung](./oauth2-authentication.md).
* Bei Auswahl von `"authenticationRule": "PLATFORM_AUTHENTICATION"`, verweisen auf [Anmeldeinformationen-Konfiguration](./credentials-configuration.md) in der Referenzdokumentation.

## Schritt 6: Ziel testen {#test-destination}

Nachdem Sie Ihr Ziel mithilfe der Konfigurations-Endpunkte in den vorherigen Schritten eingerichtet haben, können Sie die [Ziel-Testwerkzeug](./create-template.md) um die Integration zwischen Adobe Experience Platform und Ihrem Ziel zu testen.

Im Rahmen des Testvorgangs Ihres Ziels müssen Sie die Benutzeroberfläche &quot;Experience Platform&quot;zum Erstellen von Segmenten verwenden, die Sie für Ihr Ziel aktivieren. Weitere Informationen zum Erstellen von Segmenten in der Experience Platform finden Sie in den beiden folgenden Ressourcen:

* [Segmentdokumentationsseite erstellen](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=en#create-segment)
* [exemplarische Vorgehensweise für Segmentvideo erstellen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en)

## Schritt 7: Ziel veröffentlichen {#publish-destination}

Verwenden Sie nach dem Konfigurieren und Testen des Ziels die [Ziel-Veröffentlichungs-API](./destination-publish-api.md) , um Ihre Konfiguration zur Überprüfung an die Adobe zu senden.

## Schritt 8: Dokument Ihres Ziels {#document-destination}

Wenn Sie ein unabhängiger Software-Hersteller (ISV) oder System Integrator (SI) sind und eine [produktive Integration](./overview.md#productized-custom-integrations), verwenden Sie [Self-Service-Dokumentationsverfahren](./docs-framework/documentation-instructions.md) , um eine Produktdokumentationsseite für Ihr Ziel zu erstellen in [Experience League-Zielkatalog](/help/destinations/catalog/overview.md).
