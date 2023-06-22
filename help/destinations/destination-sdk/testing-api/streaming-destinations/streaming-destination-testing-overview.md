---
description: Erfahren Sie, wie Sie mit der Zieltest-API Ihre Streaming-Zielkonfiguration testen können, bevor Sie sie veröffentlichen.
title: Streaming-Zieltest-API – Überblick
exl-id: 21e4d647-1168-4cb4-a2f8-22d201e39bba
source-git-commit: 0befd65b91e49cacab67c76fd9ed5d77bf790b9d
workflow-type: ht
source-wordcount: '508'
ht-degree: 100%

---


# Streaming-Zieltest-API – Überblick

Als Teil des Destination SDK bietet Adobe Entwickler-Tools, mit denen Sie Ihr Ziel konfigurieren und testen können. Auf dieser Seite wird beschrieben, wie Sie Ihre Zielkonfiguration testen. Informationen zum Erstellen einer Nachrichtenumwandlungsvorlage finden Sie unter [Erstellen und Testen einer Nachrichtenumwandlungsvorlage](../../testing-api/streaming-destinations/create-template.md).

Um zu **testen, ob Ihr Ziel richtig konfiguriert ist, und die Integrität der Datenflüsse zu Ihrem konfigurierten Ziel zu überprüfen**, verwenden Sie das *Test-Tool für Ziele*. Mit diesem Tool können Sie Ihre Zielkonfiguration testen, indem Sie Nachrichten an Ihren REST-API-Endpunkt senden.

Nachstehend wird gezeigt, wie das Testen Ihres Ziels in den [Zielkonfigurations-Workflow](../../guides/configure-destination-instructions.md) in Destination SDK passt:

![Abbildung, wo der Zieltestschritt in den Zielkonfigurations-Workflow passt](../../assets/testing-api/test-destination-step.png)

## Test-Tool für Ziele – Zweck und Voraussetzungen {#destination-testing-tool}

Verwenden Sie das Test-Tool für Ziele, um Ihre Zielkonfiguration zu testen, indem Sie Nachrichten an den Partnerendpunkt senden, den Sie im Abschnitt [Server-Konfiguration](../../authoring-api/destination-server/create-destination-server.md) bereitgestellt haben.

Bevor Sie das Tool verwenden, stellen Sie Folgendes sicher:
* Konfigurieren Sie Ihr Ziel, indem Sie die im [Zielkonfigurations-Workflow](../../authoring-api/destination-configuration/create-destination-configuration.md)beschriebenen Schritte ausführen, und
* Erstellen Sie eine Verbindung zu Ihrem Ziel, wie im Abschnitt [Abrufen der Ziel-Instanz-ID](../../testing-api/streaming-destinations/destination-testing-api.md#get-destination-instance-id) beschrieben.

Mit diesem Tool haben Sie nach der Konfiguration Ihres Ziels folgende Möglichkeiten:
* Testen, ob Ihr Ziel richtig konfiguriert ist.
* Überprüfen der Integrität der Datenflüsse zu Ihrem konfigurierten Ziel.

### Informationen zur Verwendung {#how-to-use}

>[!NOTE]
>
>Eine vollständige API-Referenzdokumentation finden Sie unter [Vorgänge der Zieltest-API](../../testing-api/streaming-destinations/destination-testing-api.md).

Sie können den Zieltest-API-Endpunkt mit oder ohne Hinzufügen von Profilen zur Anfrage aufrufen.

Wenn Sie der Anfrage keine Profile hinzufügen, generiert Adobe diese intern und fügt sie der Anfrage hinzu. Informationen zum Generieren von Profilen für die Verwendung in dieser Anfrage finden Sie in der [API-Referenz zur Profilgenerierung](../../testing-api/streaming-destinations/sample-profile-generation-api.md). Sie müssen Profile basierend auf dem Quell-XDM-Schema generieren, wie in der [API-Referenz](../../testing-api/streaming-destinations/sample-profile-generation-api.md#generate-sample-profiles-source-schema) beschrieben. Beachten Sie, dass das Quellschema das [Vereinigungsschema](../../../../profile/ui/union-schema.md) der von Ihnen verwendeten Sandbox ist.

Die Antwort enthält das Ergebnis der Verarbeitung der Zielanfrage. Die Anfrage umfasst drei Hauptabschnitte:
* Die von Adobe für das Ziel generierte Anfrage.
* Die von Ihrem Ziel erhaltene Antwort.
* Die Liste der in der Anfrage gesendeten Profile, unabhängig davon, ob es sich um Profile handelt, [die Sie in der Anfrage hinzugefügt haben](../../testing-api/streaming-destinations/destination-testing-api.md#test-with-added-profiles) oder ob sie von Adobe generiert wurden, falls [der Hauptteil der Zieltestanfrage leer war](../../testing-api/streaming-destinations/destination-testing-api.md#test-without-adding-profiles).

>[!NOTE]
>
>Adobe kann mehrere Anfrage- und Antwortpaare generieren. Wenn Sie beispielsweise 10 Profile an ein Ziel senden, für das `maxUsersPerRequest` den Wert 7 hat, gibt es eine Anfrage mit 7 Profilen und eine weitere Anfrage mit 3 Profilen.

**Beispielanfrage mit Profilparametern im Hauptteil**

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
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
--header 'x-gw-ims-org-id: {ORG_ID}' \
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

Beschreibungen der Anfrage- und Antwortparameter finden Sie unter [Vorgänge der Zieltest-API](../../testing-api/streaming-destinations/destination-testing-api.md).

## Nächste Schritte

Nachdem Sie Ihr Ziel getestet und bestätigt haben, dass es korrekt konfiguriert ist, verwenden Sie die [Zielpublikations-API](../../publishing-api/create-publishing-request.md), um Ihre Konfiguration zur Überprüfung an Adobe zu senden.
