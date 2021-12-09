---
description: Auf dieser Seite werden alle API-Vorgänge aufgelistet und beschrieben, die Sie mit dem API-Endpunkt "/authoring/testing/destinationInstance/"ausführen können, um zu testen, ob Ihr Ziel richtig konfiguriert ist, und um die Integrität der Datenflüsse zu Ihrem konfigurierten Ziel zu überprüfen.
title: API-Vorgänge für Zieltests
exl-id: 2b54250d-ec30-4ad7-a8be-b86b14e4f074
source-git-commit: 52ce788f6947300b607dfc2efa09d028f9c2ddd7
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 2%

---

# API-Vorgänge für Zieltests {#template-api-operations}

>[!IMPORTANT]
>
>**API-Endpunkt**: `https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/`

Auf dieser Seite werden alle API-Vorgänge aufgelistet und beschrieben, die Sie mit dem `/authoring/testing/destinationInstance/` API-Endpunkt, um zu testen, ob Ihr Ziel richtig konfiguriert ist, und um die Integrität der Datenflüsse zu Ihrem konfigurierten Ziel zu überprüfen. Eine Beschreibung der von diesem Endpunkt unterstützten Funktionen finden Sie unter [Testen der Zielkonfiguration](./test-destination.md).

Sie stellen Anfragen an den Test-Endpunkt, mit oder ohne Profile zum Aufruf hinzuzufügen. Wenn Sie keine Profile für die Anfrage senden, generiert Adobe diese intern und fügt sie zur Anfrage hinzu.

Sie können die [API zur Profilerstellung](./sample-profile-generation-api.md) , um Profile zu erstellen, die in Anfragen an die Ziel-Test-API verwendet werden.

## Abrufen der Ziel-Instanz-ID {#get-destination-instance-id}

>[!IMPORTANT]
>
>* Um diese API verwenden zu können, müssen Sie über eine bestehende Verbindung zu Ihrem Ziel in der Experience Platform-Benutzeroberfläche verfügen. Lesen [Verbindung zum Ziel herstellen](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) und [Profile und Segmente für ein Ziel aktivieren](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en) für weitere Informationen. Nachdem Sie die Verbindung zu Ihrem Ziel hergestellt haben, rufen Sie die ID der Zielinstanz ab, die Sie in API-Aufrufen an diesen Endpunkt von der URL verwenden sollten, wenn [Durchsuchen einer Verbindung mit Ihrem Ziel](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destination-details-page.html?lang=en).
   >![UI-Bild, wie Sie die Ziel-Instanz-ID abrufen](./assets/get-destination-instance-id.png)


## Erste Schritte mit API-Vorgängen für Zieltests {#get-started}

Bevor Sie fortfahren, lesen Sie bitte die [Erste Schritte](./getting-started.md) für wichtige Informationen, die Sie benötigen, um die API erfolgreich aufrufen zu können, einschließlich Informationen zum Abrufen der erforderlichen Authoring-Berechtigung für Ziele und der erforderlichen Kopfzeilen.

## Testen Sie Ihre Zielkonfiguration, ohne Profile zum -Aufruf hinzuzufügen. {#test-without-adding-profiles}

Sie können Ihre Zielkonfiguration testen, indem Sie eine POST-Anfrage an die `authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}` -Endpunkt und geben die Ziel-Instanz-ID des Ziels an, das Sie testen.

**API-Format**


```http
POST authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

| Abfrageparameter | Beschreibung |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | Die Ziel-Instanz-ID des Ziels, das Sie testen. |

**Anfrage**

Die folgende Anfrage ruft den REST-API-Endpunkt Ihres Ziels auf. Die Anforderung wird von der `{DESTINATION_INSTANCE_ID}` Abfrageparameter.

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/49966037-32cd-4457-a105-2cbf9c01826a' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 zusammen mit der API-Antwort vom REST-API-Endpunkt Ihres Ziels zurück.

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
            "ECID":[
               {
                  "id":"ECID-vlnt6"
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

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `aggregationKey` | Enthält Informationen zur für das Ziel konfigurierten Aggregationsrichtlinie. Weitere Informationen finden Sie im Abschnitt [Aggregationspolitik](./destination-configuration.md#aggregation) im Zielkonfigurationsdokument. |
| `traceId` | Eine eindeutige Kennung für den Vorgang. Bei Auftreten von Fehlern können Sie diese ID zum Zwecke der Fehlerbehebung für das Adobe-Team freigeben. |
| `results.httpCalls.request` | Enthält die Anfrage, die per Adobe an Ihr Ziel gesendet wurde. |
| `results.httpCalls.response` | Enthält die Antwort, die die Adobe von Ihrem Ziel erhalten hat. |
| `inputProfiles` | Umfasst die Profile, die beim Aufruf an Ihr Ziel exportiert wurden. Die Profile stimmen mit Ihrem Quellschema überein. |

{style=&quot;table-layout:auto&quot;}

## Testen Sie Ihre Zielkonfiguration mit Profilen, die zum Aufruf hinzugefügt wurden. {#test-with-added-profiles}

Sie können Ihre Zielkonfiguration testen, indem Sie eine POST-Anfrage an die `authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}` -Endpunkt und geben die Ziel-Instanz-ID des Ziels an, das Sie testen.

**API-Format**

```http
POST authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

| Abfrageparameter | Beschreibung |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | Die Ziel-Instanz-ID des Ziels, das Sie testen. |

**Anfrage**

Die folgende Anfrage ruft den REST-API-Endpunkt Ihres Ziels auf. Die Anforderung wird durch die in der Payload angegebenen Parameter und die `{DESTINATION_INSTANCE_ID}` Abfrageparameter.

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/49966037-32cd-4457-a105-2cbf9c01826a' \
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
            "ECID":[
               {
                  "id":"ECID-Z3i2t"
               }
            ],
            "external_id":[
               {
                  "id":"external_id-h29Fq"
               }
            ]
         },
         "attributes":{
            "firstName":{
               "value":"John"
            }
         }
      }
   ]
}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 zusammen mit der API-Antwort vom REST-API-Endpunkt Ihres Ziels zurück.

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
            "ECID":[
               {
                  "id":"ECID-Z3i2t"
               }
            ],
            "external_id":[
               {
                  "id":"external_id-h29Fq"
               }
            ]
         },
         "attributes":{
            "firstName":{
               "value":"John"
            }
         }
      }
   ]
}
```

## Umgang mit API-Fehlern {#api-error-handling}

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen für die Experience Platform API-Fehlermeldung. Siehe [API-Statuscodes](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) und [Fehler in der Anfragekopfzeile](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) im Handbuch zur Fehlerbehebung bei Platform.

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie Ihr Ziel testen können. Sie können jetzt die Adobe [Self-Service-Dokumentationsprozess](./docs-framework/documentation-instructions.md) , um eine Dokumentationsseite für Ihr Ziel zu erstellen.
