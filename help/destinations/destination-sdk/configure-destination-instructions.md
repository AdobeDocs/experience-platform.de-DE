---
description: Auf dieser Seite wird beschrieben, wie Sie die Referenzinformationen in den Konfigurationsoptionen für das Ziel-SDK verwenden, um Ihr Ziel mithilfe des Ziel-SDK zu konfigurieren.
seo-description: This page describes how to use the reference information in Configuration options for the Destinations SDK to configure your destination using Destination SDK.
seo-title: How to use Destination SDK to configure your destination
title: Verwenden des Destination SDK zum Konfigurieren Ihres Ziels
source-git-commit: 2841adc0ce212a945c35ba38209d4c00c519ad7b
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 0%

---

# Verwenden des Destination SDK zum Konfigurieren Ihres Ziels

## Übersicht {#overview}

Auf dieser Seite wird beschrieben, wie Sie die Referenzinformationen unter [Konfigurationsoptionen in Destinations SDK](./configuration-options.md) verwenden, um Ihr Ziel zu konfigurieren. Die Schritte werden in der folgenden Reihenfolge angeordnet.

## Voraussetzungen {#prerequisites}

Bevor Sie mit den unten dargestellten Schritten fortfahren, lesen Sie die Seite [Erste Schritte für das Ziel-SDK](./getting-started.md) , um Informationen zum Abrufen der erforderlichen Anmeldeinformationen für die Adobe I/O-Authentifizierung und anderer Voraussetzungen für die Verwendung mit Ziel-SDK-APIs zu erhalten.

## Schritte zur Verwendung der Konfigurationsoptionen im Destination SDK zum Einrichten Ihres Ziels {#steps}

![Veranschaulichte Schritte zur Verwendung der Ziel-SDK-Endpunkte](./assets/destination-sdk-steps.png)

## Schritt 1: Erstellen einer Server- und Vorlagenkonfiguration {#create-server-template-configuration}

Erstellen Sie zunächst einen Server und eine Vorlagenkonfiguration mithilfe des Endpunkts `/destinations-server` (siehe [API-Referenz](./destination-server-api.md)). Weitere Informationen zur Server- und Vorlagenkonfiguration finden Sie unter [Server- und Vorlagenspezifikationen](./configuration-options.md#server-and-template) im Referenzabschnitt.

Nachfolgend finden Sie eine Beispielkonfiguration. Beachten Sie, dass die Nachrichtenumwandlungsvorlage im Parameter `requestBody.value` in Schritt 3, [Umwandlungsvorlage erstellen](./configure-destination-instructions.md#create-transformation-template) angesprochen wird.

```json
POST platform.adobe.io/data/core/activation/authoring/destination-servers

{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{endpoint.region}}/items"
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

Nachfolgend finden Sie eine Beispielkonfiguration für eine Zielvorlage, die mithilfe des API-Endpunkts `/destinations` erstellt wird. Weitere Informationen zu dieser Vorlage finden Sie unter [Zielkonfiguration](./destination-configuration.md).

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
   ],
   "inputSchemaId":"cc8621770a9243b98aba4df79898b1ed"
}
```

## Schritt 3: Vorlage für die Nachrichtenumwandlung erstellen - Verwenden Sie die Vorlagensprache, um das Ausgabeformat der Nachricht anzugeben. {#create-transformation-template}

Basierend auf den Payloads, die Ihr Ziel unterstützt, müssen Sie eine Vorlage erstellen, die das Format der exportierten Daten aus dem Adobe-XDM-Format in ein von Ihrem Ziel unterstütztes Format umwandelt. Siehe Vorlagenbeispiele im Abschnitt [Verwenden einer Vorlagensprache für die Identitäts-, Attribute- und Segmentzugehörigkeitstransformationen](./message-format.md#using-templating) und verwenden Sie das [Vorlagenerstellungstool](./create-template.md), das von Adobe bereitgestellt wird.

## Schritt 4: Erstellen der Konfiguration von Zielgruppen-Metadaten {#create-audience-metadata-configuration}

Für einige Ziele erfordert das Ziel-SDK, dass Sie eine Zielgruppen-Metadatenvorlage konfigurieren, um Zielgruppen in Ihrem Ziel programmgesteuert zu erstellen, zu aktualisieren oder zu löschen. Unter [Zielgruppen-Metadatenverwaltung](./audience-metadata-management.md) finden Sie Informationen dazu, wann Sie diese Konfiguration einrichten und wie Sie sie durchführen.

## Schritt 5: Konfiguration von Anmeldedaten erstellen/Authentifizierung einrichten {#set-up-authentication}

Je nachdem, ob Sie in der obigen Zielkonfiguration `"authenticationRule": "CUSTOMER_AUTHENTICATION"` oder `"authenticationRule": "PLATFORM_AUTHENTICATION"` angeben, können Sie die Authentifizierung für Ihr Ziel mithilfe des Endpunkts `/destination` oder `/credentials` einrichten.

* **Der häufigste Fall**: Wenn Sie ausgewählt haben  `"authenticationRule": "CUSTOMER_AUTHENTICATION"` und Ihr Ziel die OAuth 2-Authentifizierungsmethode unterstützt, lesen Sie  [OAuth 2-Authentifizierung](./oauth2-authentication.md).
* Wenn Sie `"authenticationRule": "PLATFORM_AUTHENTICATION"` ausgewählt haben, lesen Sie [Credentials configuration](./credentials-configuration.md) in der Referenzdokumentation.

## Schritt 6: Ziel testen {#test-destination}

Nachdem Sie Ihr Ziel mithilfe der Vorlagen in den vorherigen Schritten eingerichtet haben, können Sie das [Ziel-Testtool](./create-template.md) verwenden, um die Integration zwischen Adobe Experience Platform und Ihrem Ziel zu testen.

Im Rahmen des Testvorgangs Ihres Ziels müssen Sie die Experience Platform-Benutzeroberfläche zum Erstellen von Segmenten verwenden, die Sie für Ihr Ziel aktivieren. Anweisungen zum Erstellen von Segmenten in Experience Platform finden Sie in den beiden unten stehenden Ressourcen:

* [Erstellen einer Dokumentationsseite für Segmente](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=en#create-segment)
* [Videoanleitung zum Erstellen eines Segments](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en)


## Schritt 7: Ziel veröffentlichen {#publish-destination}

Nach dem Konfigurieren und Testen Ihres Ziels. Verwenden Sie die [API zur Zielveröffentlichung](./destination-publish-api.md), um Ihre Konfiguration zur Überprüfung an Adobe zu senden.

## Schritt 8: Ziel dokumentieren {#document-destination}

Wenn Sie ein unabhängiger Softwareanbieter (ISV) oder Systemintegrator (SI) sind und eine [produktisierte Integration](./overview.md#productized-custom-integrations) erstellen, verwenden Sie den [Self-Service-Dokumentationsprozess](./docs-framework/documentation-instructions.md), um eine Produktdokumentationsseite für Ihr Ziel im [Experience League-Zielkatalog](/help/destinations/catalog/overview.md) zu erstellen.