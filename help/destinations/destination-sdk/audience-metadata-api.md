---
description: Auf dieser Seite werden alle API-Vorgänge beschrieben, die Sie mit dem API-Endpunkt "/authoring/audience-templates"ausführen können.
title: API-Vorgänge für Zielgruppen-Metadaten-Endpunkte
exl-id: 3444da8c-b2be-4254-980a-8cce7560134d
source-git-commit: afdabdebe9b82d828cb1941edb99ca2518a941a2
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 6%

---

# API-Vorgänge für Zielgruppen-Metadaten-Endpunkte

>[!IMPORTANT]
>
>**API-Endpunkt**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Auf dieser Seite werden alle API-Vorgänge aufgelistet und beschrieben, die Sie mit dem `/authoring/audience-templates` API-Endpunkt. Eine Beschreibung der Verwendung dieses Endpunkts finden Sie unter [Zielgruppen-Metadatenverwaltung](./audience-metadata-management.md).

## Erste Schritte mit API-Vorgängen für Zielgruppenvorlagen {#get-started}

Bevor Sie fortfahren, lesen Sie bitte die [Erste Schritte](./getting-started.md) für wichtige Informationen, die Sie benötigen, um die API erfolgreich aufrufen zu können, einschließlich Informationen zum Abrufen der erforderlichen Authoring-Berechtigung für Ziele und der erforderlichen Kopfzeilen.

## Neue Zielgruppenvorlage erstellen {#create}

Sie können eine neue Zielgruppenvorlage erstellen, indem Sie eine POST-Anfrage an die `/authoring/audience-templates` -Endpunkt.

**API-Format**

```http
POST /authoring/audience-templates
```

**Anfrage**

Mit der folgenden Anfrage wird eine neue Zielgruppen-Metadatenvorlage erstellt, die von den in der Payload bereitgestellten Parametern konfiguriert wird. Die nachstehende Payload enthält alle Parameter, die vom `/authoring/audience-templates` -Endpunkt. Beachten Sie, dass Sie nicht alle Parameter für den Aufruf hinzufügen müssen und dass die Vorlage entsprechend Ihren API-Anforderungen angepasst werden kann.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "metadataTemplate":{
      "name":"string",
      "create":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "update":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "delete":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "validate":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "notify":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      }
   },
   "validations":[
      {
         "field":"string",
         "regex":"string"
      }
   ]
}'
```

| Eigenschaft | Typ | Beschreibung |
| -------- | ----------- | ----------- |
| `name` | Zeichenfolge | Der Name der Zielgruppen-Metadatenvorlage für Ihr Ziel. Dieser Name wird in jeder Partner-spezifischen Fehlermeldung in der Experience Platform-Benutzeroberfläche angezeigt, gefolgt von der Fehlermeldung, die von `metadataTemplate.create.errorSchemaMap`. |
| `url` | Zeichenfolge | Die URL und der Endpunkt Ihrer API, die zum Erstellen, Aktualisieren, Löschen oder Überprüfen von Zielgruppen/Segmenten in Ihrer Plattform verwendet wird. Zwei Beispiele für die Branche: `https://adsapi.snapchat.com/v1/adaccounts/{{customerData.accountId}}/segments` und `https://api.linkedin.com/v2/dmpSegments/{{segment.alias}}`. |
| `httpMethod` | Zeichenfolge | Die Methode, die für Ihren Endpunkt verwendet wird, um das Segment/die Zielgruppe in Ihrem Ziel programmgesteuert zu erstellen, zu aktualisieren, zu löschen oder zu validieren. Beispiel: `POST`, `PUT`, `DELETE` |
| `headers.header` | Zeichenfolge | Gibt alle HTTP-Header an, die zum Aufruf Ihrer API hinzugefügt werden sollen. Beispiel: `"Content-Type"` |
| `headers.value` | Zeichenfolge | Gibt den Wert von HTTP-Headern an, die zum Aufruf Ihrer API hinzugefügt werden sollen. Beispiel: `"application/x-www-form-urlencoded"` |
| `requestBody` | Zeichenfolge | Gibt den Inhalt des Nachrichtentextes an, der an Ihre API gesendet werden soll. Die Parameter, die zum `requestBody` -Objekt hängt davon ab, welche Felder Ihre API akzeptiert. Ein Beispiel finden Sie im Abschnitt [Beispiel einer ersten Vorlage](./audience-metadata-management.md#example-1) im Dokument Zielgruppenmetadaten-Funktion . |
| `responseFields.name` | Zeichenfolge | Geben Sie alle Antwortfelder an, die Ihre API beim Aufruf zurückgibt. Ein Beispiel finden Sie im Abschnitt [Vorlagenbeispiele](./audience-metadata-management.md#examples) im Dokument Zielgruppenmetadaten-Funktion . |
| `responseFields.value` | Zeichenfolge | Geben Sie den Wert aller Antwortfelder an, die Ihre API beim Aufruf zurückgibt. |
| `responseErrorFields.name` | Zeichenfolge | Geben Sie alle Antwortfelder an, die Ihre API beim Aufruf zurückgibt. Ein Beispiel finden Sie im Abschnitt [ Vorlagenbeispiele](./audience-metadata-management.md#examples) im Dokument Zielgruppenmetadaten-Funktion . |
| `responseErrorFields.value` | Zeichenfolge | Analysiert alle Fehlermeldungen, die bei API-Aufrufantworten von Ihrem Ziel zurückgegeben werden. Diese Fehlermeldungen werden Benutzern in der Benutzeroberfläche von Experience Platform angezeigt. |
| `validations.field` | Zeichenfolge | Gibt an, ob Überprüfungen für Felder durchgeführt werden sollen, bevor API-Aufrufe an Ihr Ziel gesendet werden. Sie können beispielsweise `{{validations.accountId}}` , um die Konto-ID des Benutzers zu überprüfen. |
| `validations.regex` | Zeichenfolge | Gibt an, wie das Feld strukturiert sein soll, damit die Validierung besteht. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zur neu erstellten Zielgruppenvorlage zurück.

## Aktualisieren der Zielgruppenvorlage {#update}

Sie können eine vorhandene Zielgruppenvorlage aktualisieren, indem Sie eine PUT-Anfrage an die `/authoring/audience-templates` -Endpunkt und die Instanz-ID der Zielgruppenvorlage angeben, die Sie aktualisieren möchten. Geben Sie im Text des Aufrufs die aktualisierte Vorlage an.

**API-Format**

```http
PUT /authoring/audience-templates/{INSTANCE_ID}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{INSTANCE_ID}` | Die ID der Zielgruppen-Metadatenvorlage, die Sie aktualisieren möchten. |

**Anfrage**

Mit der folgenden Anfrage wird eine vorhandene Zielgruppen-Metadatenvorlage aktualisiert, die durch die in der Payload bereitgestellten Parameter konfiguriert wird.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/audience-templates/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "metadataTemplate":{
      "create":{
         "url":"https://api.moviestar.com/v1.0/{{customerData.accountId}}/customaudiences?fields=name,description,account_id&subtype=CUSTOM&name={{segment.name}}&customer_file_source={{segment.metadata.customer_file_source}}&access_token={{authData.accessToken}}",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://api.moviestar.com/v1.0/{{segment.alias}}?field=name,description,account_id&access_token={{authData.accessToken}}&customerAudienceId={{segment.alias}}&&name={{segment.name}}&description={{segment.description}}&customer_file_source={{segment.metadata.customer_file_source}}",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://api.moviestar.com/v1.0/{{segment.alias}}?fields=name,description,account_id&access_token={{authData.accessToken}}&customerAudienceId={{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "validate":{
         "url":"https://api.moviestar.com/v1.0/permissions?access_token={{authData.accessToken}}",
         "httpMethod":"GET",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.data[0].permission}}",
               "name":"Id"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      }
   }
}
```

## Abrufen einer Liste von Zielgruppenvorlagen {#retrieve-list}

Sie können eine Liste aller Zielgruppenvorlagen für Ihre IMS-Organisation abrufen, indem Sie eine GET-Anfrage an die `/authoring/audience-templates` -Endpunkt.

**API-Format**


```http
GET /authoring/audience-templates
```

**Anfrage**

Mit der folgenden Anfrage wird die Liste der Zielgruppenvorlagen abgerufen, auf die Sie Zugriff haben, basierend auf der IMS-Organisation und der Sandbox-Konfiguration.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Die folgende Antwort gibt den HTTP-Status 200 mit einer Liste von Zielgruppen-Metadatenvorlagen zurück, auf die Sie Zugriff haben, basierend auf der von Ihnen verwendeten IMS-Organisations-ID und dem Sandbox-Namen. One `instanceId` entspricht der Vorlage für ein Ziel. Die Antwort wird aus Gründen der Kürze abgeschnitten.

```json
{
   "items":[
      {
         "instanceId":"12a3238f-b509-4a40-b8fb-0a5006e7901d",
         "createdDate":"2021-07-20T13:30:30.843054Z",
         "lastModifiedDate":"2021-07-21T16:33:05.787472Z",
         "metadataTemplate":{
            "create":{
               "url":"https://api.moviestar.com/v2/dmpSegments",
               "httpMethod":"POST",
               "headers":[
                  {
                     "value":"application/json",
                     "header":"Content-Type"
                  },
                  {
                     "value":"Bearer {{authData.accessToken}}",
                     "header":"Authorization"
                  }
               ],
               "requestBody":{
                  "json":{
                     "name":"{{segment.name}}",
                     "type":"USER",
                     "account":"{{customerData.accountId}}",
                     "accessPolicy":"PRIVATE",
                     "destinations":[
                        {
                           "destination":"MOVIESTAR"
                        }
                     ],
                     "sourcePlatform":"ADOBE"
                  }
               },
               "responseFields":[
                  {
                     "value":"{{headers.x-moviestar-id}}",
                     "name":"externalAudienceId"
                  }
               ],
               "responseErrorFields":[
                  {
                     "value":"{{message}}",
                     "name":"message"
                  }
               ]
            },
            "update":{
               "url":"https://api.moviestar.com/v2/dmpSegments/{{segment.alias}}",
               "httpMethod":"POST",
               "headers":[
                  {
                     "value":"application/json",
                     "header":"Content-Type"
                  },
                  {
                     "value":"Bearer {{authData.accessToken}}",
                     "header":"Authorization"
                  }
               ],
               "requestBody":{
                  "json":{
                     "patch":{
                        "$set":{
                           "name":"{{segment.name}}"
                        }
                     }
                  }
               },
               "responseErrorFields":[
                  {
                     "value":"{{message}}",
                     "name":"message"
                  }
               ]
            },
            "delete":{
               "url":"https://api.moviestar.com/v2/dmpSegments/{{segment.alias}}",
               "httpMethod":"DELETE",
               "headers":[
                  {
                     "value":"application/json",
                     "header":"Content-Type"
                  },
                  {
                     "value":"Bearer {{authData.accessToken}}",
                     "header":"Authorization"
                  }
               ],
               "responseErrorFields":[
                  {
                     "value":"{{message}}",
                     "name":"message"
                  }
               ]
            },
            "name":"Moviestar audience template - Third example"
         }
      }
   ]
}
```

## Abrufen einer bestimmten Zielgruppenvorlage {#get}

Sie können detaillierte Informationen zu einer bestimmten Zielgruppenvorlage abrufen, indem Sie eine GET-Anfrage an die `/authoring/audience-templates` -Endpunkt und die Instanz-ID der Zielgruppenvorlage angeben, die Sie abrufen möchten.

**API-Format**

```http
GET /authoring/audience-templates/{INSTANCE_ID}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{INSTANCE_ID}` | Die ID der Zielgruppen-Metadatenvorlage, die Sie abrufen möchten. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/audience-templates/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit detaillierten Informationen zur angegebenen Zielgruppenvorlage zurück.

```json
{
   "instanceId":"34ab9cc2-2536-44a5-9dc5-b2fea60b3bd6",
   "createdDate":"2021-07-26T19:30:52.012490Z",
   "lastModifiedDate":"2021-07-27T21:25:42.763478Z",
   "metadataTemplate":{
      "create":{
         "url":"https://api.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}",
                     "source_type":"FIRST_PARTY",
                     "ad_account_id":"{{customerData.accountId}}",
                     "retention_in_days":180
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
         "httpMethod":"PUT",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "id":"{{segment.alias}}",
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}"
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://adsapi.moviestar.com/v1/segments/{{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "name":"Moviestar destination audience template - Example 1"
   }
}
```


## Löschen einer bestimmten Zielgruppenvorlage {#delete}

Sie können die angegebene Zielgruppenvorlage löschen, indem Sie eine DELETE-Anfrage an die `/authoring/audience-templates` -Endpunkt und die Kennung der Zielgruppenvorlage angeben, die Sie im Anfragepfad löschen möchten.

**API-Format**

```http
DELETE /authoring/audience-templates/{INSTANCE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{INSTANCE_ID}` | Die `id` der Zielgruppenvorlage, die Sie löschen möchten. |

**Anfrage**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/audience-templates/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
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

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wann Zielgruppen-Metadatenvorlagen verwendet und wie eine Zielgruppen-Metadatenvorlage mithilfe der `/authoring/audience-templates` API-Endpunkt. Lesen [Verwendung von Destination SDK zum Konfigurieren Ihres Ziels](./configure-destination-instructions.md) um zu verstehen, wo dieser Schritt in den Prozess der Konfiguration Ihres Ziels passt.
