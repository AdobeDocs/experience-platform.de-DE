---
description: Als Teil des Destination SDK stellt Adobe Entwicklertools bereit, mit denen Sie Ihr Ziel konfigurieren und testen können. Auf dieser Seite wird beschrieben, wie Sie Ihre Zielkonfiguration testen.
title: Testen der Zielkonfiguration
exl-id: 21e4d647-1168-4cb4-a2f8-22d201e39bba
source-git-commit: 3d7151645bc90a2dcbd6b31251ed459029ab77c9
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 1%

---

# Testen der Zielkonfiguration {#developer-tools}

## Übersicht {#overview}

Als Teil des Destination SDK stellt Adobe Entwicklertools bereit, mit denen Sie Ihr Ziel konfigurieren und testen können. Auf dieser Seite wird beschrieben, wie Sie Ihre Zielkonfiguration testen. Informationen zum Erstellen einer Nachrichtenumwandlungsvorlage finden Sie unter [Erstellen und Testen einer Nachrichtenumwandlungsvorlage](./create-template.md).

Um **zu testen, ob Ihr Ziel richtig konfiguriert ist, und um die Integrität der Datenflüsse zu Ihrem konfigurierten Ziel zu überprüfen**, verwenden Sie das *Ziel-Test-Tool*. Mit diesem Tool können Sie Ihre Zielkonfiguration testen, indem Sie Nachrichten an Ihren REST-API-Endpunkt senden.

Nachstehend wird gezeigt, wie das Testen Ihres Ziels in den [Zielkonfigurations-Workflow](./configure-destination-instructions.md) im Destination SDK passt:

![Abbildung, wo der Zieltestschritt in den Zielkonfigurations-Workflow passt](./assets/test-destination-step.png)

## Destination Test Tool {#destination-testing-tool}

Verwenden Sie dieses Tool, um Ihre Zielkonfiguration zu testen, indem Sie Nachrichten an den Partnerendpunkt senden, den Sie in der [Serverkonfiguration](./server-and-template-configuration.md) angegeben haben.

Mit diesem Tool haben Sie nach der Konfiguration Ihres Ziels folgende Möglichkeiten:
* Testen Sie, ob Ihr Ziel richtig konfiguriert ist.
* Überprüfen Sie die Integrität der Datenflüsse zu Ihrem konfigurierten Ziel.

### Informationen zur Verwendung {#how-to-use}

>[!NOTE]
>
>Eine vollständige API-Referenzdokumentation finden Sie unter [API-Vorgänge für Zieltests](./destination-testing-api.md).

Sie können den Ziel-Test-API-Endpunkt mit oder ohne Hinzufügen von Profilen zur Anfrage aufrufen.

Wenn Sie der Anforderung keine Profile hinzufügen, generiert Adobe diese intern und fügt sie der Anforderung hinzu. Wenn Sie Profile generieren möchten, die in dieser Anfrage verwendet werden sollen, lesen Sie den Abschnitt [API-Referenz zur Beispielprofilerstellung](./sample-profile-generation-api.md). Sie müssen Profile basierend auf dem Quell-XDM-Schema generieren, wie in der [API-Referenz](./sample-profile-generation-api.md#generate-sample-profiles-source-schema) dargestellt. Beachten Sie, dass das Quellschema das [Vereinigungsschema](https://experienceleague.adobe.com/docs/experience-platform/profile/union-schemas/union-schema.html?lang=en) der von Ihnen verwendeten Sandbox ist.

Die Antwort enthält das Ergebnis der Verarbeitung der Zielanfrage. Die Anfrage umfasst drei Hauptabschnitte:
* Die von Adobe für das Ziel generierte Anfrage.
* Die von Ihrem Ziel erhaltene Antwort.
* Die Liste der in der Anfrage gesendeten Profile, unabhängig davon, ob die Profile von Ihnen in der Anfrage ](./destination-testing-api.md/#test-with-added-profiles) hinzugefügt wurden oder von Adobe generiert wurden, wenn [der Hauptteil der Ziel-Testanfrage leer war](./destination-testing-api.md#test-without-adding-profiles).[

>[!NOTE]
>
>Adobe kann mehrere Anfrage- und Antwortpaare generieren. Wenn Sie beispielsweise 10 Profile an ein Ziel mit dem Wert `maxUsersPerRequest` 7 senden, gibt es eine Anfrage mit 7 Profilen und eine weitere Anfrage mit 3 Profilen.

**Beispielanfrage mit Profilparametern im Hauptteil**

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '{
   "profiles":[
      {
         "segmentMembership":{
            "ups":{
               "374a9a6c-c719-4cdb-a660-155a2838e6d6":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248585Z",
                  "status":"realized"
               },
               "896f8776-9498-47b4-b994-51cb3f61c2c5":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248605Z",
                  "status":"realized"
               }
            }
         },
         "identityMap":{
            "Email":[
               {
                  "id":"Email-iIyJc"
               }
            ],
            "IDFA":[
               {
                  "id":"IDFA-viPAW"
               }
            ],
            "GAID":[
               {
                  "id":"GAID-Bc6LE"
               }
            ],
            "Email_LC_SHA256":[
               {
                  "id":"Email_LC_SHA256-gEOdj"
               }
            ]
         },
         "attributes":{
            "key":{
               "value":"string"
            }
         }
      }
   ]
}'
```

**Beispielanfrage ohne Profilparameter im Hauptteil**


```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw ''
```

**Beispielantwort**

Beachten Sie, dass der Inhalt des Parameters `results.httpCalls` spezifisch für Ihre REST-API ist.

```json
{
   "results":[
      {
         "aggregationKey":{
            "destinationInstanceId":"string",
            "segmentId":"string",
            "segmentStatus":"realized",
            "identityNamespaces":[
               [
                  "email",
                  "phone"
               ]
            ]
         },
         "httpCalls":[
            {
               "traceId":"a06fec2d-a886-4219-8975-4e4b7ed26539",
               "request":{
                  "body":"{ \"attributes\": [  { \"external_id\": \"external_id-h29Fq\"  , \"AdobeExperiencePlatformSegments\": { \"add\": [  \"Nirvana fans\" ,  \"RHCP fans\"   ], \"remove\": [  ] }  ,  \"key\":  \"string\"    }  ] }",
                  "headers":[
                     {
                        "Content-Type":"application/json"
                     }
                  ],
                  "method":"POST",
                  "uri":"https://api.moviestar.com/users/track"
               },
               "response":{
                  "body":"{\"status\": \"success\"}",
                  "code":"200",
                  "headers":[
                     {
                        "Connection":"keep-alive"
                     },
                     {
                        "Content-Type":"application/json"
                     },
                     {
                        "Server":"nginx"
                     },
                     {
                        "Vary":"Origin,Accept-Encoding"
                     },
                     {
                        "transfer-encoding":"chunked"
                     }
                  ]
               }
            }
         ]
      }
   ],
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "03fb9938-8537-4b4c-87f9-9c4d413a0ee5":{
                  "lastQualificationTime":"2021-06-17T12:25:12.872039Z",
                  "status":"realized"
               },
               "27e05542-d6a3-46c7-9c8e-d59d50229530":{
                  "lastQualificationTime":"2021-06-17T12:25:12.872042Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"john.smith@abc.com"
         },
         "identityMap":{
            "Email":[
               {
                  "id":"Email-iIyJc"
               }
            ],
            "IDFA":[
               {
                  "id":"IDFA-viPAW"
               }
            ],
            "GAID":[
               {
                  "id":"GAID-Bc6LE"
               }
            ],
            "Email_LC_SHA256":[
               {
                  "id":"Email_LC_SHA256-gEOdj"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"string"
            }
         }
      }
   ]
}
```

Beschreibungen der Anforderungs- und Antwortparameter finden Sie unter [API-Vorgänge für Zieltests](./destination-testing-api.md).

## Nächste Schritte

Nachdem Sie Ihr Ziel getestet und bestätigt haben, dass es korrekt konfiguriert ist, verwenden Sie die [API zur Zielveröffentlichung](./destination-publish-api.md), um Ihre Konfiguration zur Überprüfung an Adobe zu senden.
