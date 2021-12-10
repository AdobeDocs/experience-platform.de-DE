---
description: Auf dieser Seite werden die Schritte zum Konfigurieren eines Streaming-Ziels mit Destination SDK aufgeführt und beschrieben.
title: Verwenden von Destination SDK zum Konfigurieren eines Streaming-Ziels
exl-id: d8aa7353-ba55-4a0d-81c4-ea2762387638
source-git-commit: b3d0f0c43b60895961cee2ee54518c0450e2e2f7
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 0%

---

# Verwenden von Destination SDK zum Konfigurieren eines Streaming-Ziels

## Übersicht {#overview}

Auf dieser Seite wird die Verwendung der Informationen unter [Konfigurationsoptionen im Ziel-SDK](./configuration-options.md) und in anderen Destination SDK-Funktionen und API-Referenzdokumenten zum Konfigurieren eines [Streaming-Ziel](/help/destinations/destination-types.md#streaming-destinations). Die Schritte werden in der folgenden Reihenfolge angeordnet.

>[!NOTE]
>
>Die Konfiguration eines Batch-Ziels über Destination SDK wird derzeit nicht unterstützt.

## Voraussetzungen {#prerequisites}

Bevor Sie mit den unten dargestellten Schritten fortfahren, lesen Sie bitte die [Erste Schritte mit Destination SDK](./getting-started.md) Seite mit Informationen zum Abrufen der erforderlichen Anmeldeinformationen für die Adobe I/O-Authentifizierung und anderen Voraussetzungen für die Verwendung mit Destination SDK-APIs.

## Schritte zum Verwenden der Konfigurationsoptionen in Destination SDK zum Einrichten Ihres Ziels {#steps}

![Veranschaulichte Schritte zur Verwendung von Destination SDK-Endpunkten](./assets/destination-sdk-steps.png)

## Schritt 1: Erstellen einer Server- und Vorlagenkonfiguration {#create-server-template-configuration}

Erstellen Sie zunächst einen Server und eine Vorlagenkonfiguration mit dem `/destinations-server` Endpunkt (lesen) [API-Referenz](./destination-server-api.md)). Weitere Informationen zur Server- und Vorlagenkonfiguration finden Sie unter [Server- und Vorlagenspezifikationen](./configuration-options.md#server-and-template) im Referenzabschnitt.

Nachfolgend finden Sie eine Beispielkonfiguration. Beachten Sie, dass die Nachrichtenumwandlungsvorlage in `requestBody.value` -Parameter wird in Schritt 3 behandelt; [Umwandlungsvorlage erstellen](./configure-destination-instructions.md#create-transformation-template).

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

Im Folgenden finden Sie eine Beispielkonfiguration für eine Zielvorlage, die mithilfe der `/destinations` API-Endpunkt. Weitere Informationen zu dieser Vorlage finden Sie unter [Zielkonfiguration](./destination-configuration.md).

Um die Server- und Vorlagenkonfiguration in Schritt 1 mit dieser Zielkonfiguration zu verbinden, fügen Sie die Instanz-ID des Servers und die Vorlagenkonfiguration als `destinationServerId` hier.

>[!IMPORTANT]
>
>Um ein korrekt konfiguriertes Ziel zu erstellen, müssen Sie *must* mindestens eine Zielidentität in `identityNamespaces`, wie unten dargestellt. Wenn keine Zielidentität konfiguriert ist, können Benutzer nicht über die [Zuordnungsschritt](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) des Aktivierungs-Workflows.

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

## Schritt 3: Vorlage für die Nachrichtenumwandlung erstellen - Verwenden Sie die Vorlagensprache, um das Ausgabeformat der Nachricht anzugeben. {#create-transformation-template}

Basierend auf den Payloads, die Ihr Ziel unterstützt, müssen Sie eine Vorlage erstellen, die das Format der exportierten Daten aus dem Adobe-XDM-Format in ein von Ihrem Ziel unterstütztes Format umwandelt. Siehe Vorlagenbeispiele im Abschnitt . [Verwenden einer Vorlagensprache für die Transformationen von Identitäten, Attributen und Segmentzugehörigkeiten](./message-format.md#using-templating) und verwenden Sie [Vorlagen-Authoring-Tool](./create-template.md) von der Adobe bereitgestellt werden.

Nachdem Sie eine Vorlage für die Nachrichtenumwandlung erstellt haben, die für Sie funktioniert, fügen Sie sie zur Server- und Vorlagenkonfiguration hinzu, die Sie in Schritt 1 erstellt haben.

## Schritt 4: Erstellen der Konfiguration von Zielgruppen-Metadaten {#create-audience-metadata-configuration}

Für einige Ziele erfordert Destination SDK, dass Sie eine Zielgruppen-Metadatenkonfiguration konfigurieren, um Zielgruppen in Ihrem Ziel programmgesteuert zu erstellen, zu aktualisieren oder zu löschen. Siehe [Zielgruppen-Metadatenverwaltung](./audience-metadata-management.md) Informationen dazu, wann Sie diese Konfiguration einrichten müssen und wie Sie sie durchführen.

Wenn Sie eine Zielgruppen-Metadatenkonfiguration verwenden, müssen Sie sie mit der Zielkonfiguration verbinden, die Sie in Schritt 2 erstellt haben. Fügen Sie die Instanz-ID Ihrer Audience-Metadatenkonfiguration Ihrer Zielkonfiguration als `audienceTemplateId`.

## Schritt 5: Konfiguration von Anmeldedaten erstellen/Authentifizierung einrichten {#set-up-authentication}

Je nachdem, ob `"authenticationRule": "CUSTOMER_AUTHENTICATION"` oder `"authenticationRule": "PLATFORM_AUTHENTICATION"` In der obigen Zielkonfiguration können Sie die Authentifizierung für Ihr Ziel einrichten, indem Sie die `/destination` oder `/credentials` -Endpunkt.

* **häufigster Fall**: Wenn Sie `"authenticationRule": "CUSTOMER_AUTHENTICATION"` in der Zielkonfiguration enthalten sind und Ihr Ziel die OAuth 2-Authentifizierungsmethode unterstützt, lesen Sie [OAuth 2-Authentifizierung](./oauth2-authentication.md).
* Wenn Sie `"authenticationRule": "PLATFORM_AUTHENTICATION"`, siehe [Authentifizierungskonfiguration](./authentication-configuration.md#when-to-use).

## Schritt 6: Ziel testen {#test-destination}

Nachdem Sie Ihr Ziel mithilfe der Konfigurations-Endpunkte in den vorherigen Schritten eingerichtet haben, können Sie die [Zieltestwerkzeug](./test-destination.md) , um die Integration zwischen Adobe Experience Platform und Ihrem Ziel zu testen.

Im Rahmen des Testvorgangs Ihres Ziels müssen Sie die Experience Platform-Benutzeroberfläche zum Erstellen von Segmenten verwenden, die Sie für Ihr Ziel aktivieren. Anweisungen zum Erstellen von Segmenten in Experience Platform finden Sie in den beiden unten stehenden Ressourcen:

* [Erstellen einer Dokumentationsseite für Segmente](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=en#create-segment)
* [Videoanleitung zum Erstellen eines Segments](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en)

## Schritt 7: Ziel veröffentlichen {#publish-destination}

Verwenden Sie nach dem Konfigurieren und Testen Ihres Ziels die [Zielpublikations-API](./destination-publish-api.md) , um Ihre Konfiguration zur Überprüfung an Adobe zu senden.

## Schritt 8: Ziel dokumentieren {#document-destination}

Wenn Sie ein unabhängiger Software-Anbieter (ISV) oder Systemintegrator (SI) sind und eine [produktive Integration](./overview.md#productized-custom-integrations), verwenden Sie die [Self-Service-Dokumentationsprozess](./docs-framework/documentation-instructions.md) , um eine Produktdokumentationsseite für Ihr Ziel in der [Experience Platform-Zielkatalog](/help/destinations/catalog/overview.md).
