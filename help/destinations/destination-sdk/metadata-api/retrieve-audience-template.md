---
description: Auf dieser Seite wird der API-Aufruf zum Abrufen einer Zielgruppenvorlage über Adobe Experience Platform Destination SDK veranschaulicht.
title: Abrufen einer Zielgruppenvorlage
exl-id: 44f2d571-49c5-4112-b3ee-bc839f2b0874
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 96%

---

# Abrufen einer Zielgruppenvorlage

>[!IMPORTANT]
>
>**API-Endpunkt**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Auf dieser Seite werden die API-Anfrage und die Payload erläutert, die Sie zum Abrufen einer Zielgruppen-Metadatenvorlage verwenden können, indem Sie den API-Endpunkt `/authoring/audience-templates` verwenden.

Eine ausführliche Beschreibung der Funktionen, die Sie über diesen Endpunkt konfigurieren können, finden Sie unter [Verwaltung von Zielgruppen-Metadaten](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Bei allen von Destination SDK unterstützten Parameternamen und Werten wird **nach Groß-/Kleinschreibung unterschieden**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Erste Schritte mit API-Vorgängen für Zielgruppenvorlagen {#get-started}

Bevor Sie fortfahren, lesen Sie [Erste Schritte](../getting-started.md). Dort finden Sie die nötigen Informationen für den erfolgreichen Aufruf der API, einschließlich Details für den Abruf der erforderlichen Authoring-Berechtigung für Ziele und zu den erforderlichen Kopfzeilen.

## Abrufen einer Zielgruppenvorlage {#retrieve}

Sie können eine vorhandene Zielgruppenvorlage abrufen, indem Sie eine `GET`-Anfrage an den Endpunkt `/authoring/audience-templates` stellen.

**API-Format**

Verwenden Sie das folgende API-Format, um alle Zielgruppenvorlagen für Ihr Konto abzurufen.

```http
GET /authoring/audience-templates
```

Verwenden Sie das folgende API-Format, um eine bestimmte Zielgruppenvorlage abzurufen, die durch den Parameter `{INSTANCE_ID}` bestimmt wird.

```http
GET /authoring/audience-templates/{INSTANCE_ID}
```

Die folgenden beiden Anfragen rufen alle Zielgruppenvorlagen für Ihre IMS-Organisation oder eine bestimmte Zielgruppenvorlage ab, je nachdem, ob Sie den Parameter `INSTANCE_ID` in der Anfrage übergeben.

Wählen Sie die einzelnen Registerkarten unten aus, um die entsprechende Payload anzuzeigen.

>[!BEGINTABS]

>[!TAB Alle Zielgruppenvorlagen abrufen]

Mit der folgenden Anfrage wird die Liste der Zielgruppenvorlagen abgerufen, auf die Sie Zugriff haben, basierend auf der [!DNL IMS Org ID] und der Sandbox-Konfiguration.

+++Anfrage

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Antwort

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit einer Liste von Zielgruppen-Metadatenvorlagen zurückgegeben, auf die Sie Zugriff haben, basierend auf der von Ihnen verwendeten. [!DNL IMS Org ID] und dem Sandbox-Namen. Eine `instanceId` entspricht einer Zielgruppenvorlage.

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

+++

>[!TAB Abrufen einer bestimmten Zielgruppenvorlage]

Mit der folgenden Anfrage wird die Liste der Zielgruppenvorlagen abgerufen, auf die Sie Zugriff haben, basierend auf der [!DNL IMS Org ID] und der Sandbox-Konfiguration.

+++Anfrage

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/audience-templates/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{INSTANCE_ID}` | Die ID der Zielgruppenvorlage, die Sie abrufen möchten. |

+++

+++Antwort

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit den Details der Zielgruppenvorlage zurückgegeben, die der beim Aufruf angegebenen `{INSTANCE_ID}` entspricht.

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

+++

>[!ENDTABS]

## Umgang mit API-Fehlern {#error-handling}

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status](../../../landing/troubleshooting.md#api-status-codes)Codes und [Fehler in der Anfragekopfzeile](../../../landing/troubleshooting.md#request-header-errors) im Handbuch zur Fehlerbehebung bei Experience Platform.

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie mithilfe des API-Endpunkts `/authoring/destination-servers` Details zu Ihrer Ziel-Server-Konfiguration abrufen können. Lesen Sie [Verwenden des Destination SDK zum Konfigurieren Ihres Ziels](../guides/configure-destination-instructions.md), um zu verstehen, wo dieser Schritt in den Prozess der Konfiguration Ihres Ziels passt.
