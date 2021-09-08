---
description: Die Server- und Vorlagenspezifikationen können im Adobe Experience Platform Destination SDK über den allgemeinen Endpunkt "/authoring/destination-servers"konfiguriert werden.
title: Konfigurationsoptionen für Server- und Vorlagenspezifikationen im Destination SDK
source-git-commit: d2452bf0e59866d3deca57090001c4c5a0935525
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 7%

---

# Konfigurationsoptionen für Server- und Vorlagenspezifikationen

## Übersicht {#overview}

Die Server- und Vorlagenspezifikationen können im Adobe Experience Platform Destination SDK über den allgemeinen Endpunkt `/authoring/destination-servers` konfiguriert werden. Eine vollständige Liste der Vorgänge, die Sie für den Endpunkt ausführen können, finden Sie unter [API-Endpunktoperationen für Ziele](./destination-server-api.md).

## Beispielkonfiguration  {#example-configuration}

```json
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
         "value":"{ \"attributes\": [ {% for ns in [\"external_id\", \"yourdestination_id\"] %} {% if input.profile.identityMap[ns] is not empty and first_namespace_encountered %} , {% endif %} {% set first_namespace_encountered = true %} {% for identity in input.profile.identityMap[ns]%} { \"{{ ns }}\": \"{{ identity.id }}\" {% if input.profile.segmentMembership.ups is not empty %} , \"AEPSegments\": { \"add\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"realized\" or segment.value.status == \"existing\" %} {% if added_segment_found %} , {% endif %} {% set added_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ], \"remove\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"exited\" %} {% if removed_segment_found %} , {% endif %} {% set removed_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ] } {% set removed_segment_found = false %} {% set added_segment_found = false %} {% endif %} {% if input.profile.attributes is not empty %} , {% endif %} {% for attribute in input.profile.attributes %} \"{{ attribute.key }}\": {% if attribute.value is empty %} null {% else %} \"{{ attribute.value.value }}\" {% endif %} {% if not loop.last%} , {% endif %} {% endfor %} } {% if not loop.last %} , {% endif %} {% endfor %} {% endfor %} ] }"
      },
      "contentType":"application/json"
   }
}
```

## Serverspezifikationen {#server-specs}

![Serverkonfiguration hervorgehoben](./assets/server-configuration.png)

Kunden können Daten über HTTP-Exporte von Adobe Experience Platform an Ihr Ziel aktivieren. Die Serverkonfiguration enthält Informationen zum Server, der die Nachrichten erhält (der Server auf Ihrer Seite).

Dieser Prozess stellt Benutzerdaten als eine Reihe von HTTP-Nachrichten an Ihre Zielplattform bereit. Die folgenden Parameter bilden die Vorlage für HTTP-Server-Spezifikationen.

| Parameter | Typ | Beschreibung |
|---|---|---|
| `name` | Zeichenfolge | Stellt einen Anzeigenamen Ihres Servers dar, der nur für Adobe sichtbar ist. Dieser Name ist für Partner oder Kunden nicht sichtbar. Beispiel `Moviestar destination server`. |
| `destinationServerType` | Zeichenfolge | `URL_BASED` ist derzeit die einzige verfügbare Option. |
| `templatingStrategy` | Zeichenfolge | <ul><li>Verwenden Sie `PEBBLE_V1` , wenn die Adobe die URL im unten stehenden Feld `value` transformieren muss. Verwenden Sie diese Option, wenn Sie einen Endpunkt wie haben: `https://api.moviestar.com/data/{{endpoint.region}}/items` </li><li> Verwenden Sie `NONE` , wenn keine Transformation auf der Adobe-Seite erforderlich ist, z. B. wenn Sie einen Endpunkt wie haben: `https://api.moviestar.com/data/items` </li></ul> |
| `value` | Zeichenfolge | Geben Sie die Adresse des API-Endpunkts ein, mit dem sich Experience Platform verbinden soll. |

{style=&quot;table-layout:auto&quot;}

<!--

|Parameter | Type | Description|
|---------|----------|------|
|`hostname` | String | This is the hostname of your server. Example `https://data-in.acmecompany.net`.  |
|`port` | integer | The server port of your destination, for example `443`, `80`. |
|`maxUsersPerRequest` | integer | Specifies the maximum number of users per request allowed for your server. |
|`path` | String | This represents the url path and parameters of your server. Example:  `/path/to/import` |
|`httpMethod` | String | The method that Adobe will use in calls to your server. Options are `GET`, `PUT`, `POST`, `DELETE`, `PATCH`, `OPTIONS`, `HEAD`. |
|`contentType` | String | Defines how to structure the content sent to your servers. Supported options are JSON and XML. |

-->

## Vorlagenspezifikationen {#template-specs}

![Vorlagenkonfiguration hervorgehoben](./assets/template-configuration.png)

Mit der Vorlagenspezifikation können Sie konfigurieren, wie Sie die exportierte Nachricht an Ihr Ziel formatieren. Adobe verwendet eine Vorlagensprache ähnlich [Jinja](https://jinja.palletsprojects.com/en/2.11.x/), um die Felder aus dem XDM-Schema in ein Format umzuwandeln, das von Ihrem Ziel unterstützt wird. Weitere Informationen zur Transformation finden Sie unter den folgenden Links:

* [Nachrichtenformat](./message-format.md)
* [Verwenden einer Vorlagensprache für die Transformationen von Identitäten, Attributen und Segmentzugehörigkeiten ](./message-format.md#using-templating)

>[!TIP]
>
>Adobe bietet ein [Entwickler-Tool](./create-template.md), mit dem Sie eine Nachrichtenumwandlungsvorlage erstellen und testen können.

| Parameter | Typ | Beschreibung |
|---|---|---|
| `httpMethod` | Zeichenfolge | Die Methode, die Adobe bei Aufrufen an Ihren Server verwendet. Die Optionen sind `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `templatingStrategy` | Zeichenfolge | Verwenden Sie `PEBBLE_V1`. |
| `value` | Zeichenfolge | Diese Zeichenfolge ist die mit Zeichen versehene Version, die die Daten von Platform-Kunden in das Format umwandelt, das Ihr Dienst erwartet. <br> Informationen zum Schreiben der Vorlage finden Sie im Abschnitt  [Vorlage verwenden](./message-format.md#using-templating). <br> Weiterführende Informationen zur Maskierung von Zeichen finden Sie im  [RFC JSON-Standard, Abschnitt 7](https://tools.ietf.org/html/rfc8259#section-7). <br> Ein Beispiel für eine einfache Umwandlung finden Sie im Abschnitt  [Profil - ](./message-format.md#attributes) Attribution - Umwandlung. |
| `contentType` | Zeichenfolge | Der Inhaltstyp, den Ihr Server akzeptiert. Dieser Wert ist höchstwahrscheinlich `application/json`. |

{style=&quot;table-layout:auto&quot;}

<!--

|`requestBody` | String | The request body contains the data exported from Real-time CDP, activated to your destination. <br> We need to know which data format macros your destination should support. See [Outbound Template Macros](https://docs.adobe.com/content./en/audience-manager/user-guide/implementation-integration-guides/receiving-audience-data/batch-outbound-data-transfers/outbound-template-macros.html) and [Outbound Macro Examples](https://docs.adobe.com/content./en/audience-manager/user-guide/implementation-integration-guides/receiving-audience-data/batch-outbound-data-transfers/outbound-macro-examples.html) for examples from Adobe's DMP, Audience Manager. <br> See also, [Message format](#message-format) for further information.  |
|`queryParameters` | String | Request parameters defined as macros. See above.|



<br>&nbsp;

#### Example

A valid HTTP specs template could look like below:

```

{
  "name": "ACME company HTTP template",
  "type": "HTTP", 
  "httpTemplate": {
    "httpMethod": "POST",
    "requestBody": "{"AdvertiserId":"12345", "DataCenterId": 2, "SegmentID":"dfd215e4-8d6b-4fdb-90b9-fab4456f2c9d","Data":[{"Name":"4321"}]}",
    "queryParameters": "{"AdvertiserId":"12345", "DataCenterId": 2, "SegmentID":"dfd215e4-8d6b-4fdb-90b9-fab4456f2c9d","Data":[{"Name":"4321"}]}",
    "contentType": "JSON"
  }
}

```

// commenting out this part as these types of destination specs are not supported in phase one

### File specifications

File-based destinations deliver file exports containing segment qualifications and profile attributes to your preferred storage location. If you want to set up a batch file-based destination, the template we'll use will be as below:

## Server specs

The server configuration contains information about the server receiving the messages (the server on your side). 
Adobe Real-time CDP currently supports three types of server configurations:
* URL
* File-based SFTP
* File-based S3

For URL destinations, you would provide us your server's information, for File-based SFTP and File-based S3 you would provide information as to the storage locations where files should be delivered.
Provide us the necessary information about your server or storage locations, as shown in the sections below.


**urlBasedDestination**

|Parameter | Type | Description|
|---------|----------|------|
|`hostname` | String | This is the hostname of your server. Example `https://data-in.acmecompany.net`.  |
|`port` | integer | The server port of your destination, for example `443`, `80`. |
|`maxUsersPerRequest` | integer | Specifies the maximum number of users per request allowed for your server. |
|`path` | String | This represents the url path and parameters of your server. Example:  `/path/to/import` |


// commenting out this part as these types of destination specs are not supported in phase one

**SFTP Destinations**

For FTP destinations, we need the protocol details below:

Parameter | Type | 
---------|----------|
 hostname | String | 
 port | integer | 
 rootDirectory | String | 
 moveToWhenCompleted | integer | 
 tmpFileRename | integer | 
 encryptionMode | String |
 filenameSuffix | String | 

**Amazon S3 Destinations**

For Amazon S3 destinations, we need the protocol details below:

Parameter | Description | 
---------|----------|
 bucket | Your Amazon S3 bucket name | 
 path | Your Amazon S3 bucket path | 

-->
