---
description: Auf dieser Seite werden die Schritte zum Konfigurieren eines Streaming-Ziels mit dem Destination SDK aufgeführt und beschrieben.
title: Verwenden des Destination SDK zum Konfigurieren eines Streaming-Ziels
exl-id: d8aa7353-ba55-4a0d-81c4-ea2762387638
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 65%

---

# Verwenden des Destination SDK zum Konfigurieren eines Streaming-Ziels

## Übersicht {#overview}

Auf dieser Seite wird die Verwendung der Informationen unter [Konfigurationsoptionen im Destinations SDK](../functionality/configuration-options.md) sowie anderen Destination SDK-Funktionen und API-Referenzdokumenten zum Konfigurieren eines [Streaming-Ziels](../../destination-types.md#streaming-destinations) beschrieben. Die Schritte sind im Folgenden in der vorgegebenen Reihenfolge aufgeführt.

## Voraussetzungen {#prerequisites}

Bevor Sie mit den unten dargestellten Schritten fortfahren, informieren Sie sich auf der Seite [Erste Schritte mit dem Destination SDK](../getting-started.md), wie Sie die erforderlichen Adobe I/O-Authentifizierungsdaten und andere Voraussetzungen für die Arbeit mit Destination SDK-APIs erhalten. Dies setzt voraus, dass Sie die Voraussetzungen für Partnerschaft und Berechtigung erfüllt haben und bereit sind, mit der Entwicklung Ihres Ziels zu beginnen.

## Schritte zum Verwenden der Konfigurationsoptionen im Destination SDK zum Einrichten Ihres Ziels {#steps}

![Veranschaulichte Schritte zur Verwendung von Destination SDK-Endpunkten](../assets/guides/destination-sdk-steps.png)

## Schritt 1: Erstellen einer Server- und Vorlagenkonfiguration {#create-server-template-configuration}

Beginnen bei [Erstellen einer Server- und Vorlagenkonfiguration](../authoring-api/destination-server/create-destination-server.md) mithilfe der `/destinations-server` -Endpunkt.

Unten ist eine Beispielkonfiguration dargestellt. Beachten Sie, dass die Nachrichtenumwandlungsvorlage im `requestBody.value`-Parameter in Schritt 3, [Erstellen einer Umwandlungsvorlage](#create-transformation-template), behandelt wird.

```shell
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

```json {line-numbers="true" highlight="14"}
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

## Schritt 2: Erstellen einer Zielkonfiguration {#create-destination-configuration}

Im Folgenden finden Sie eine Beispielkonfiguration für eine Zielvorlage, die mithilfe dem `/destinations`-API-Endpunkt erstellt wurde. Siehe [Zielkonfiguration erstellen](../authoring-api/destination-configuration/create-destination-configuration.md) für weitere Informationen.

Um die Server- und Vorlagenkonfiguration in Schritt 1 mit dieser Zielkonfiguration zu verbinden, fügen Sie die Instanz-ID der Server- und Vorlagenkonfiguration hier als `destinationServerId` hinzu.

>[!IMPORTANT]
>
>Um ein korrekt konfiguriertes Echtzeit-(Streaming-)Ziel zu erstellen, müssen Sie *must* mindestens eine Zielidentität in `identityNamespaces`, wie unten dargestellt. Wenn keine Zielidentität konfiguriert ist, können Benutzer nicht über den [Zuordnungsschritt](../../ui/activate-segment-streaming-destinations.md#mapping) des Aktivierungs-Workflows hinausgehen.

```shell
POST platform.adobe.io/data/core/activation/authoring/destinations
```

```json {line-numbers="true" highlight="74"}
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
   "audienceMetadataConfig":{
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
         "maxBatchAgeInSecs":2400,
         "maxNumEventsInBatch":5000
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

## Schritt 3: Erstellen einer Nachrichtenumwandlungsvorlage – Verwenden Sie die Vorlagensprache, um das Ausgabeformat der Nachricht anzugeben {#create-transformation-template}

Basierend auf den Payloads, die das Ziel unterstützt, müssen Sie eine Vorlage erstellen, die das Format der exportierten Daten aus dem Adobe-XDM-Format in ein vom Ziel unterstütztes Format umwandelt. Siehe Vorlagenbeispiele im Abschnitt . [Verwenden einer Vorlagensprache für die Transformationen von Identität, Attributen und Zielgruppen-Mitgliedschaft](../functionality/destination-server/message-format.md#using-templating) und verwenden Sie [Vorlagen-Authoring-Tool](../testing-api/streaming-destinations/create-template.md) von der Adobe bereitgestellt werden.

Nachdem Sie eine Vorlage für die Nachrichtenumwandlung erstellt haben, die Ihren Anforderungen entspricht, fügen Sie sie der Server- und Vorlagenkonfiguration hinzu, die Sie in Schritt 1 erstellt haben.

```json {line-numbers="true" highlight="13-14"}
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
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{\n    \"users\": [\n        {% for profile in input.profiles %}\n            {{profile|raw}}{% if not loop.last %},{% endif %}\n        {% endfor %}\n    ]\n}"
      },
      "contentType":"application/json"
   }
}
```

## Schritt 4: Erstellen der Zielgruppen-Metadatenkonfiguration {#create-audience-metadata-configuration}

Für einige Ziele erfordert das Destination SDK, dass Sie eine Zielgruppen-Metadatenkonfiguration konfigurieren, um Zielgruppen in Ihrem Ziel programmgesteuert zu erstellen, zu aktualisieren oder zu löschen. Informationen dazu, wann Sie diese Konfiguration einrichten müssen und wie Sie sie durchführen, finden Sie unter [Zielgruppen-Metadatenverwaltung](../functionality/audience-metadata-management.md).

Wenn Sie eine Zielgruppen-Metadatenkonfiguration verwenden, müssen Sie diese mit der Zielkonfiguration verbinden, die Sie in Schritt 2 erstellt haben. Fügen Sie Ihrer Zielkonfiguration die Instanz-ID Ihrer Zielgruppen-Metadatenkonfiguration als `audienceTemplateId` hinzu.

```json {line-numbers="true" highlight="53"}
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
   "audienceMetadataConfig":{
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
         "maxBatchAgeInSecs":2400,
         "maxNumEventsInBatch":5000
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


## Schritt 5: Einrichten der Authentifizierung {#set-up-authentication}

Je nachdem, ob Sie In der obigen Zielkonfiguration `"authenticationRule": "CUSTOMER_AUTHENTICATION"` oder `"authenticationRule": "PLATFORM_AUTHENTICATION"` angeben, können Sie unter Verwendung des Endpunkts `/destination` oder `/credentials` die Authentifizierung für Ihr Ziel einrichten.

Wenn Sie `"authenticationRule": "CUSTOMER_AUTHENTICATION"` in der Zielkonfiguration enthalten sind und Ihr Ziel die OAuth 2-Authentifizierungsmethode unterstützt, lesen Sie [OAuth 2-Authentifizierung](../functionality/destination-configuration/oauth2-authentication.md).

Wenn Sie `"authenticationRule": "PLATFORM_AUTHENTICATION"`, müssen Sie eine [Anmeldekonfiguration](../credentials-api/create-credential-configuration.md).

## Schritt 6: Testen des Ziels {#test-destination}

Nachdem Sie das Ziel mit den Konfigurationsendpunkten in den vorherigen Schritten eingerichtet haben, können Sie das [Zieltest-Tool](../testing-api/streaming-destinations/streaming-destination-testing-overview.md) verwenden, um die Integration zwischen Adobe Experience Platform und Ihrem Ziel zu testen.

Im Rahmen des Testvorgangs Ihres Ziels müssen Sie die Experience Platform-Benutzeroberfläche zum Erstellen von Segmenten verwenden, die Sie für Ihr Ziel aktivieren. Anweisungen zum Erstellen von Zielgruppen in Experience Platform finden Sie in den beiden unten stehenden Ressourcen:

* [Erstellen einer Dokumentationsseite für Zielgruppen](/help/segmentation/ui/overview.md#create-segment)
* [Videoeinführung zum Erstellen einer Zielgruppe](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=de)

## Schritt 7: Veröffentlichen des Ziels {#publish-destination}

>[!NOTE]
>
>Dieser Schritt ist nicht erforderlich, wenn Sie ein privates Ziel für Ihre eigene Verwendung erstellen und es nicht im Zielkatalog veröffentlichen möchten, damit andere Kunden ihn verwenden können.

Verwenden Sie nach dem Konfigurieren und Testen Ihres Ziels die [Zielveröffentlichungs-API](../publishing-api/create-publishing-request.md), um Ihre Konfiguration zur Überprüfung an Adobe zu senden.

## Schritt 8: Dokumentieren des Ziels {#document-destination}

>[!NOTE]
>
>Dieser Schritt ist nicht erforderlich, wenn Sie ein privates Ziel für Ihre eigene Verwendung erstellen und es nicht im Zielkatalog veröffentlichen möchten, damit andere Kunden ihn verwenden können.

Wenn Sie ein unabhängiger Software-Anbieter (ISV) oder Systemintegrator (SI) sind, der eine [produktbezogene Integration](../overview.md#productized-custom-integrations) erstellt, verwenden Sie den [Self-Service-Dokumentationsprozess](../docs-framework/documentation-instructions.md), um eine Produktdokumentationsseite für Ihr Ziel im [Experience Platform-Zielkatalog](/help/destinations/catalog/overview.md) zu erstellen.

## Schritt 9: Ziel für Überprüfung durch die Adobe übermitteln {#submit-for-review}

>[!NOTE]
>
>Dieser Schritt ist nicht erforderlich, wenn Sie ein privates Ziel für Ihre eigene Verwendung erstellen und es nicht im Zielkatalog veröffentlichen möchten, damit andere Kunden ihn verwenden können.

Bevor das Ziel im Experience Platform-Katalog veröffentlicht und für alle Experience Platform-Kunden sichtbar ist, müssen Sie das Ziel offiziell zur Überprüfung durch die Adobe übermitteln. Vollständige Informationen zum [zur Überprüfung eines in der Destination SDK erstellten produktiven Ziels einreichen](../guides/submit-destination.md).
