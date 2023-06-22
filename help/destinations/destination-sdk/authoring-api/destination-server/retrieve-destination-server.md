---
description: Auf dieser Seite wird der API-Aufruf zum Abrufen einer Ziel-Server-Konfiguration über Adobe Experience Platform Destination SDK veranschaulicht.
title: Abrufen einer Ziel-Server-Konfiguration
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: ht
source-wordcount: '464'
ht-degree: 100%

---


# Abrufen einer Ziel-Server-Konfiguration

Auf dieser Seite werden die API-Anfrage und -Payload erläutert, mit deren Hilfe Sie Informationen über eine vorhandene Ziel-Server-Konfiguration abrufen können, indem Sie den API-Endpunkt `/authoring/destination-servers` verwenden.

Eine ausführliche Beschreibung der Funktionen, die von Ziel-Servern verwendet werden, finden Sie in den folgenden Artikeln:

* [Server-Spezifikationen für Ziele, die mit Destination SDK erstellt wurden](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [Vorlagenspezifikationen für Ziele, die mit Destination SDK erstellt wurden](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [Nachrichtenformat](../../../destination-sdk/functionality/destination-server/message-format.md)
* [Konfiguration der Dateiformatierung](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Bei allen von Destination SDK unterstützten Parameternamen und Werten wird **nach Groß-/Kleinschreibung unterschieden**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Erste Schritte mit API-Vorgängen für Ziel-Server {#get-started}

Bevor Sie fortfahren, lesen Sie [Erste Schritte](../../getting-started.md) für wichtige Informationen, die Sie benötigen, um die API erfolgreich aufrufen zu können, einschließlich Informationen zum Abrufen der erforderlichen Authoring-Berechtigung für Ziele und der erforderlichen Kopfzeilen.

## Abrufen einer Ziel-Server-Konfiguration {#retrieve}

Sie können eine vorhandene Ziel-Server-Konfiguration abrufen, indem Sie eine `GET`-Anfrage an den Endpunkt `/authoring/destination-servers` stellen.

>[!TIP]
>
>**API-Endpunkt**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

**API-Format**

Verwenden Sie das folgende API-Format, um alle Ziel-Server-Konfigurationen für Ihr Konto abzurufen.

```http
GET /authoring/destination-servers
```

Verwenden Sie das folgende API-Format, um eine bestimmte Ziel-Server-Konfiguration abzurufen, die durch den Parameter `{INSTANCE_ID}` bestimmt wird.

```http
GET /authoring/destination-servers/{INSTANCE_ID}
```

Die folgenden beiden Anfragen rufen alle Ziel-Server-Konfigurationen für Ihre IMS-Organisation oder eine bestimmte Ziel-Server-Konfiguration ab, je nachdem, ob Sie den Parameter `INSTANCE_ID` in der Anfrage übergeben.

Wählen Sie die einzelnen Registerkarten unten aus, um die entsprechende Payload und ihre Antworten anzuzeigen.

>[!BEGINTABS]

>[!TAB Abrufen aller Ziel-Server-Konfigurationen]

Mit der folgenden Anfrage wird die Liste der Ziel-Server-Konfigurationen abgerufen, auf die Sie Zugriff haben, basierend auf der [!DNL IMS Org ID] und der Sandbox-Konfiguration.

+++Anfrage

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Antwort

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit einer Liste der Ziel-Server-Konfigurationen zurückgegeben, auf die Sie Zugriff haben, basierend auf der von Ihnen verwendeten [!DNL IMS Org ID] und dem Sandbox-Namen. Eine `instanceId` entspricht einem Ziel-Server. Die folgende Beispielantwort enthält zwei Ziel-Server-Konfigurationen.

```json
{
   "items":[
      {
         "instanceId":"2307ec2b-4798-45a4-9239-5d0a2fb0ed67",
         "createdDate":"2020-11-17T06:49:24.331012Z",
         "lastModifiedDate":"2020-11-17T06:49:24.331012Z",
         "name":"Moviestar Destination Server",
         "destinationServerType":"URL_BASED",
         "urlBasedDestination":{
            "url":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"https://go.{% if destination.config.domain == \"US\" %}moviestar.com{% else %}moviestar.eu{% endif%}/api/named_users/tags"
            }
         },
         "httpTemplate":{
            "requestBody":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{ \"audience\": { \"named_user_id\": [ {% for named_user in input.profile.identityMap.named_user_id %} \"{{ named_user.id }}\"{% if not loop.last %},{% endif %} {% endfor %} ] }, {% if addedSegments(input.profile.segmentMembership.ups) is not empty %} \"add\": { \"adobe-segments\": [ {% for added_segment in addedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[added_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} {% if addedSegments(input.profile.segmentMembership.ups) is not empty and removedSegments(input.profile.segmentMembership.ups) is not empty %} , {% endif %} {% if removedSegments(input.profile.segmentMembership.ups) is not empty %} \"remove\": { \"adobe-segments\": [ {% for removed_segment in removedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[removed_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} }"
            },
            "httpMethod":"POST",
            "contentType":"application/json",
            "headers":[
               {
                  "header":"Accept",
                  "value":{
                     "templatingStrategy":"NONE",
                     "value":"application/vnd.moviestar+json; version=3;"
                  }
               }
            ]
         },
         "qos":{
            "name":"freeform"
         }
      },
      {
         "instanceId":"d88de647-a352-4824-8b46-354afc7acbff",
         "createdDate":"2020-11-17T16:50:59.635228Z",
         "lastModifiedDate":"2020-11-17T16:50:59.635228Z",
         "name":"Test11 Destination Server",
         "destinationServerType":"URL_BASED",
         "urlBasedDestination":{
            "url":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"https://go.{% if destination.config.domain == \"US\" %}moviestar.com{% else %}moviestar.eu{% endif%}/api/named_users/tags"
            }
         },
         "httpTemplate":{
            "requestBody":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{ \"audience\": { \"named_user_id\": [ {% for named_user in input.profile.identityMap.named_user_id %} \"{{ named_user.id }}\"{% if not loop.last %},{% endif %} {% endfor %} ] }, {% if addedSegments(input.profile.segmentMembership.ups) is not empty %} \"add\": { \"adobe-segments\": [ {% for added_segment in addedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[added_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} {% if addedSegments(input.profile.segmentMembership.ups) is not empty and removedSegments(input.profile.segmentMembership.ups) is not empty %} , {% endif %} {% if removedSegments(input.profile.segmentMembership.ups) is not empty %} \"remove\": { \"adobe-segments\": [ {% for removed_segment in removedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[removed_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} }"
            },
            "httpMethod":"POST",
            "contentType":"application/json",
            "headers":[
               {
                  "header":"Accept",
                  "value":{
                     "templatingStrategy":"NONE",
                     "value":"application/vnd.moviestar+json; version=3;"
                  }
               }
            ]
         },
         "qos":{
            "name":"freeform"
         }
      }
   ]
}
```

+++

>[!TAB Abrufen einer bestimmten Ziel-Server-Konfiguration]

Die folgende Anfrage ruft eine bestimmte Ziel-Server-Konfiguration ab, die durch den Parameter `{INSTANCE_ID}` bestimmt wird.

+++Anfrage

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{INSTANCE_ID}` | Die ID der Ziel-Server-Konfiguration, die Sie abrufen möchten. |

+++

+++Antwort

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 zurückgegeben, wobei die Konfiguration des Ziel-Servers der `{INSTANCE_ID}` entspricht, die Sie angegeben haben.

```json
{
   "items":[
      {
         "instanceId":"2307ec2b-4798-45a4-9239-5d0a2fb0ed67",
         "createdDate":"2020-11-17T06:49:24.331012Z",
         "lastModifiedDate":"2020-11-17T06:49:24.331012Z",
         "name":"Moviestar Destination Server",
         "destinationServerType":"URL_BASED",
         "urlBasedDestination":{
            "url":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"https://go.{% if destination.config.domain == \"US\" %}moviestar.com{% else %}moviestar.eu{% endif%}/api/named_users/tags"
            }
         },
         "httpTemplate":{
            "requestBody":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{ \"audience\": { \"named_user_id\": [ {% for named_user in input.profile.identityMap.named_user_id %} \"{{ named_user.id }}\"{% if not loop.last %},{% endif %} {% endfor %} ] }, {% if addedSegments(input.profile.segmentMembership.ups) is not empty %} \"add\": { \"adobe-segments\": [ {% for added_segment in addedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[added_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} {% if addedSegments(input.profile.segmentMembership.ups) is not empty and removedSegments(input.profile.segmentMembership.ups) is not empty %} , {% endif %} {% if removedSegments(input.profile.segmentMembership.ups) is not empty %} \"remove\": { \"adobe-segments\": [ {% for removed_segment in removedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[removed_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} }"
            },
            "httpMethod":"POST",
            "contentType":"application/json",
            "headers":[
               {
                  "header":"Accept",
                  "value":{
                     "templatingStrategy":"NONE",
                     "value":"application/vnd.moviestar+json; version=3;"
                  }
               }
            ]
         },
         "qos":{
            "name":"freeform"
         }
      }
   ]
}
```

+++

>[!ENDTABS]

## Umgang mit API-Fehlern {#error-handling}

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status-Codes](../../../../landing/troubleshooting.md#api-status-codes) und [Fehler im Anfrage-Header](../../../../landing/troubleshooting.md#request-header-errors) in der Anleitung zur Fehlerbehebung für Platform.

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie eine Ziel-Server-Konfiguration über den API-Endpunkt `/authoring/destination-servers` von Destination SDK abrufen können.

Weitere Informationen dazu, was Sie mit diesem Endpunkt tun können, finden Sie in den folgenden Artikeln:

* [Erstellen einer Ziel-Server-Konfiguration](create-destination-server.md)
* [Aktualisieren einer Ziel-Server-Konfiguration](update-destination-server.md)
* [Löschen einer Ziel-Server-Konfiguration](delete-destination-server.md)