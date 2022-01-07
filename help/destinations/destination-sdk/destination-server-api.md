---
description: Auf dieser Seite werden alle API-Vorgänge aufgelistet und beschrieben, die Sie mit dem API-Endpunkt "/authoring/destination-servers"ausführen können. Die Server- und Vorlagenspezifikationen für Ihr Ziel können in Adobe Experience Platform Destination SDK über den allgemeinen Endpunkt "/authoring/destination-servers"konfiguriert werden.
title: API-Vorgänge für Ziel-Server-Endpunkte
exl-id: a144b0fb-d34f-42d1-912b-8576296e59d2
source-git-commit: 6dd8a94e46b9bee6d1407e7ec945a722d8d7ecdb
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 7%

---

# API-Vorgänge für Ziel-Server-Endpunkte

>[!IMPORTANT]
>
>**API-Endpunkt**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

Auf dieser Seite werden alle API-Vorgänge aufgelistet und beschrieben, die Sie mit dem `/authoring/destination-servers` API-Endpunkt. Die Server- und Vorlagenspezifikationen für Ihr Ziel können in Adobe Experience Platform Destination SDK über den allgemeinen Endpunkt konfiguriert werden. `/authoring/destination-servers`. Eine Beschreibung der von diesem Endpunkt bereitgestellten Funktionalität finden Sie unter [Server- und Vorlagenspezifikationen](./server-and-template-configuration.md).

## Erste Schritte mit API-Vorgängen für Zielserver {#get-started}

Bevor Sie fortfahren, lesen Sie bitte die [Erste Schritte](./getting-started.md) für wichtige Informationen, die Sie benötigen, um die API erfolgreich aufrufen zu können, einschließlich Informationen zum Abrufen der erforderlichen Authoring-Berechtigung für Ziele und der erforderlichen Kopfzeilen.

## Erstellen einer Konfiguration für einen Zielserver {#create}

Sie können eine neue Zielserverkonfiguration erstellen, indem Sie eine POST-Anfrage an die `/authoring/destination-servers` -Endpunkt.

**API-Format**


```http
POST /authoring/destination-servers
```

**Anfrage**

Die folgende Anfrage erstellt eine neue Zielserverkonfiguration, die durch die in der Payload bereitgestellten Parameter konfiguriert wird. Die nachstehende Payload enthält alle Parameter, die vom `/authoring/destination-servers` -Endpunkt. Beachten Sie, dass Sie nicht alle Parameter für den Aufruf hinzufügen müssen und dass die Vorlage entsprechend Ihren API-Anforderungen angepasst werden kann.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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
         "value":"{ \"attributes\": [ {% for ns in [\"external_id\", \"yourdestination_id\"] %} {% if input.profile.identityMap[ns] is not empty and first_namespace_encountered %} , {% endif %} {% set first_namespace_encountered = true %} {% for identity in input.profile.identityMap[ns]%} { \"{{ ns }}\": \"{{ identity.id }}\" {% if input.profile.segmentMembership.ups is not empty %} , \"AEPSegments\": { \"add\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"realized\" or segment.value.status == \"existing\" %} {% if added_segment_found %} , {% endif %} {% set added_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ], \"remove\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"exited\" %} {% if removed_segment_found %} , {% endif %} {% set removed_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ] } {% set removed_segment_found = false %} {% set added_segment_found = false %} {% endif %} {% if input.profile.attributes is not empty %} , {% endif %} {% for attribute in input.profile.attributes %} \"{{ attribute.key }}\": {% if attribute.value is empty %} null {% else %} \"{{ attribute.value.value }}\" {% endif %} {% if not loop.last%} , {% endif %} {% endfor %} } {% if not loop.last %} , {% endif %} {% endfor %} {% endfor %} ] }"
      },
      "contentType":"application/json"
   }
}
```

| Parameter | Typ | Beschreibung |
| -------- | ----------- | ----------- |
| `name` | Zeichenfolge | *Erforderlich.* Stellt einen Anzeigenamen Ihres Servers dar, der nur für Adobe sichtbar ist. Dieser Name ist für Partner oder Kunden nicht sichtbar. Beispiel `Moviestar destination server`. |
| `destinationServerType` | Zeichenfolge | *Erforderlich.* `URL_BASED` ist derzeit die einzige verfügbare Option. |
| `urlBasedDestination.url.templatingStrategy` | Zeichenfolge | *Erforderlich.* <ul><li>Verwendung `PEBBLE_V1` , wenn die Adobe die URL im `value` unten. Verwenden Sie diese Option, wenn Sie einen Endpunkt wie haben: `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> Verwendung `NONE` wenn keine Transformation auf der Seite der Adobe erforderlich ist, z. B. wenn Sie einen Endpunkt wie: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | Zeichenfolge | *Erforderlich.* Geben Sie die Adresse des API-Endpunkts ein, mit dem sich Experience Platform verbinden soll. |
| `httpTemplate.httpMethod` | Zeichenfolge | *Erforderlich.* Die Methode, die Adobe bei Aufrufen an Ihren Server verwendet. Optionen sind `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `httpTemplate.requestBody.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden von `PEBBLE_V1`. |
| `httpTemplate.requestBody.value` | Zeichenfolge | *Erforderlich.* Diese Zeichenfolge ist die mit Zeichen versehene Version, die die Daten von Platform-Kunden in das Format umwandelt, das Ihr Dienst erwartet. <br> <ul><li> Informationen zum Schreiben der Vorlage finden Sie in der [Verwenden des Vorlagenabschnitts](./message-format.md#using-templating). </li><li> Weitere Informationen zum Escapen von Zeichen finden Sie im Abschnitt [RFC JSON-Standard, Abschnitt 7](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Ein Beispiel für eine einfache Umwandlung finden Sie im Abschnitt [Profilattribute](./message-format.md#attributes) Umwandlung. </li></ul> |
| `httpTemplate.contentType` | Zeichenfolge | *Erforderlich.* Der Inhaltstyp, den Ihr Server akzeptiert. Dieser Wert ist höchstwahrscheinlich `application/json`. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zur neu erstellten Zielserverkonfiguration zurück.

## Zielserverkonfigurationen auflisten {#retrieve-list}

Sie können eine Liste aller Zielserverkonfigurationen für Ihre IMS-Organisation abrufen, indem Sie eine GET-Anfrage an die `/authoring/destination-servers` -Endpunkt.

**API-Format**


```http
GET /authoring/destination-servers
```

**Anfrage**

Mit der folgenden Anfrage wird die Liste der Zielserverkonfigurationen abgerufen, auf die Sie Zugriff haben, basierend auf der IMS-Organisation und der Sandbox-Konfiguration.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Die folgende Antwort gibt den HTTP-Status 200 mit einer Liste der Zielserverkonfigurationen zurück, auf die Sie Zugriff haben, basierend auf der von Ihnen verwendeten IMS-Organisations-ID und dem Sandbox-Namen. One `instanceId` entspricht der Vorlage für einen Zielserver. Die Antwort wird aus Gründen der Kürze abgeschnitten.

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

## Vorhandene Zielserverkonfiguration aktualisieren {#update}

Sie können eine vorhandene Zielserverkonfiguration aktualisieren, indem Sie eine PUT-Anfrage an die `/authoring/destination-servers` -Endpunkt und geben die Instanz-ID der Zielserverkonfiguration an, die Sie aktualisieren möchten. Geben Sie im Hauptteil des Aufrufs die aktualisierte Zielserverkonfiguration an.

**API-Format**


```http
PUT /authoring/destination-servers/{INSTANCE_ID}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{INSTANCE_ID}` | Die ID der Zielserverkonfiguration, die Sie aktualisieren möchten. |

**Anfrage**

Die folgende Anfrage aktualisiert eine vorhandene Zielserverkonfiguration, die durch die in der Payload bereitgestellten Parameter konfiguriert wird.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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
         "value":"{ \"attributes\": [ {% for ns in [\"external_id\", \"yourdestination_id\"] %} {% if input.profile.identityMap[ns] is not empty and first_namespace_encountered %} , {% endif %} {% set first_namespace_encountered = true %} {% for identity in input.profile.identityMap[ns]%} { \"{{ ns }}\": \"{{ identity.id }}\" {% if input.profile.segmentMembership.ups is not empty %} , \"AEPSegments\": { \"add\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"realized\" or segment.value.status == \"existing\" %} {% if added_segment_found %} , {% endif %} {% set added_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ], \"remove\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"exited\" %} {% if removed_segment_found %} , {% endif %} {% set removed_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ] } {% set removed_segment_found = false %} {% set added_segment_found = false %} {% endif %} {% if input.profile.attributes is not empty %} , {% endif %} {% for attribute in input.profile.attributes %} \"{{ attribute.key }}\": {% if attribute.value is empty %} null {% else %} \"{{ attribute.value.value }}\" {% endif %} {% if not loop.last%} , {% endif %} {% endfor %} } {% if not loop.last %} , {% endif %} {% endfor %} {% endfor %} ] }"
      },
      "contentType":"application/json"
   }
}
```





## Abrufen einer bestimmten Zielserverkonfiguration {#get}

Sie können detaillierte Informationen zu einer bestimmten Zielserverkonfiguration abrufen, indem Sie eine GET-Anfrage an die `/authoring/destination-servers` -Endpunkt und geben die Instanz-ID der Zielserverkonfiguration an, die Sie aktualisieren möchten.

**API-Format**


```http
GET /authoring/destination-servers/{INSTANCE_ID}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{INSTANCE_ID}` | Die ID der Zielserverkonfiguration, die Sie abrufen möchten. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destination-servers/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit detaillierten Informationen zur angegebenen Zielserverkonfiguration zurück.

```json
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
         "value":"{ \"attributes\": [ {% for ns in [\"external_id\", \"yourdestination_id\"] %} {% if input.profile.identityMap[ns] is not empty and first_namespace_encountered %} , {% endif %} {% set first_namespace_encountered = true %} {% for identity in input.profile.identityMap[ns]%} { \"{{ ns }}\": \"{{ identity.id }}\" {% if input.profile.segmentMembership.ups is not empty %} , \"AEPSegments\": { \"add\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"realized\" or segment.value.status == \"existing\" %} {% if added_segment_found %} , {% endif %} {% set added_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ], \"remove\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"exited\" %} {% if removed_segment_found %} , {% endif %} {% set removed_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ] } {% set removed_segment_found = false %} {% set added_segment_found = false %} {% endif %} {% if input.profile.attributes is not empty %} , {% endif %} {% for attribute in input.profile.attributes %} \"{{ attribute.key }}\": {% if attribute.value is empty %} null {% else %} \"{{ attribute.value.value }}\" {% endif %} {% if not loop.last%} , {% endif %} {% endfor %} } {% if not loop.last %} , {% endif %} {% endfor %} {% endfor %} ] }"
      },
      "contentType":"application/json"
   }
}
```


## Löschen einer bestimmten Zielserverkonfiguration {#delete}

Sie können die angegebene Zielserverkonfiguration löschen, indem Sie eine DELETE-Anfrage an die `/authoring/destination-servers` -Endpunkt und geben Sie die ID der Zielserverkonfiguration an, die Sie im Anfragepfad löschen möchten.

**API-Format**

```http
DELETE /authoring/destination-servers/{INSTANCE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{INSTANCE_ID}` | Die `id` der Zielserverkonfiguration, die Sie löschen möchten. |

**Anfrage**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destination-servers/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 zusammen mit einer leeren HTTP-Antwort zurück.

## Umgang mit API-Fehlern

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen der Experience Platform API-Fehlermeldung. Siehe [API-Statuscodes](../../landing/troubleshooting.md#api-status-codes) und [Fehler in der Anfragekopfzeile](../../landing/troubleshooting.md#request-header-errors) im Handbuch zur Fehlerbehebung bei Platform.

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie Ihren Zielserver konfigurieren und Vorlagen mithilfe der `/authoring/destination-servers` API-Endpunkt. Lesen [Verwendung von Destination SDK zum Konfigurieren Ihres Ziels](./configure-destination-instructions.md) um zu verstehen, wo dieser Schritt in den Prozess der Konfiguration Ihres Ziels passt.
