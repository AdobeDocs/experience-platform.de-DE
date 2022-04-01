---
title: Besucheridentifizierung über FPID
description: Erfahren Sie, wie Sie Besucher mithilfe der Server-API mithilfe der FPID konsistent identifizieren.
seo-description: Learn how to consistently identify visitors via the Server API, by using the FPID
keywords: Edge-Netzwerk;Gateway;API;Besucher;Identifizierung;Fpid
source-git-commit: eaeab8fe96a9af399f8288b62b6ca9f31d949cfa
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---


# Besucheridentifizierung über FPID

## Übersicht

[!DNL First-party IDs] (`FPIDs`) sind Geräte-IDs, die von Kunden generiert, verwaltet und gespeichert werden. Dadurch erhalten Kunden Kontrolle über die Identifizierung von Benutzergeräten. Durch Versand `FPIDs`, generiert das Edge-Netzwerk keine brandneue `ECID` für eine Anfrage, die keine enthält.

Die `FPID` kann im API-Anfragetext als Teil der `identityMap` oder kann als Cookie gesendet werden.

Ein `FPID` kann deterministisch in eine `ECID` durch das Edge-Netzwerk, usw. `FPID` Identitäten sind vollständig mit Experience Cloud-Lösungen kompatibel. Beziehen einer `ECID` aus einem bestimmten `FPID` liefert immer dasselbe Ergebnis, sodass Benutzer ein konsistentes Erlebnis haben.

Die `ECID` auf diese Weise abgerufen werden kann, über eine `identity.fetch` Abfrage:

```json
{
   "query":{
      "identity":{
         "fetch":[
            "ECID"
         ]
      }
   }
}
```

Für Anforderungen, die sowohl eine `FPID` und `ECID`, die `ECID` bereits in der -Anfrage vorhanden ist, hat Vorrang vor der , die von der `FPID`. Daher verwendet das Edge-Netzwerk die `ECID` bereits bereitgestellt wurden und keinen aus dem angegebenen `FPID`.

In Bezug auf Geräte-IDs wird die `server` datastreams sollte `FPID` als Geräte-ID. Andere Identitäten (d. h. `EMAIL`) kann auch im Anfrageinhalt bereitgestellt werden. Das Edge-Netzwerk erfordert jedoch, dass explizit eine primäre Identität angegeben wird. Primäre Identität ist die Basisidentität, in der Profildaten gespeichert werden.

>[!NOTE]
>
>Anfragen, die keine Identität bzw. keine explizit im Anfragetext festgelegte primäre Identität aufweisen, schlagen fehl.

Folgendes `identityMap` Feldergruppe für eine `server` Datastream-Anfrage:

```json
{
   "identityMap":{
      "FPID":[
         {
            "id":"123e4567-e89b-12d3-a456-426614174000",
            "authenticatedState":"ambiguous",
            "primary":true
         }
      ],
      "EMAIL":[
         {
            "id":"email@mail.com",
            "authenticatedState":"authenticated"
         }
      ]
   }
}
```

Folgendes `identityMap` Die Feldergruppe führt zu einer Fehlerantwort, wenn sie für eine `server` Datastream-Anfrage:

```json
{
   "identityMap":{
      "FPID":[
         {
            "id":"123e4567-e89b-12d3-a456-426614174000",
            "authenticatedState":"ambiguous"
         }
      ],
      "EMAIL":[
         {
            "id":"email@mail.com",
            "authenticatedState":"authenticated"
         }
      ]
   }
}
```

Die vom Edge Network zurückgegebene Fehlerantwort ähnelt in diesem Fall der folgenden:

```json
{
   "type":"https://ns.adobe.com/aep/errors/EXEG-0306-400",
   "status":400,
   "title":"No primary identity set in request (event)",
   "detail":"No primary identity found in the input event. Update the request accordingly to your schema and try again.",
   "report":{
      "requestId":"{REQUEST_ID}",
      "configId":"{CONFIG_ID}",
      "orgId":"{ORG_ID}"
   }
}
```

## Besucheridentifizierung mit `FPID`

So identifizieren Sie Benutzer über `FPID`stellen sicher, dass `FPID` -Cookie gesendet wurde, bevor Anfragen an das Edge-Netzwerk gesendet wurden. Die `FPID` kann in einem Cookie oder als Teil der `identityMap` im Text der Anfrage.

<!--

## Request with `FPID` passed as cookie header

```shell
curl -X POST 'https://edge.adobedc.net/ee/v2/interact?dataStreamId={Data Stream ID}' \
-H 'cookie: FPID=e98f38e6-6183-442d-8cd2-0e384f4c8aa8' \
-H 'Content-Type: application/json' \
-d '{
    "event": 
        {
            "xdm": {
                "web": {
                    "webPageDetails": {
                        "URL": "https://alloystore.dev"
                    },
                    "webReferrer": {
                        "URL": ""
                    }
                },
                "device": {
                    "screenHeight": 1440,
                    "screenWidth": 3440,
                    "screenOrientation": "landscape"
                },
                "environment": {
                    "type": "browser",
                    "browserDetails": {
                        "viewportWidth": 1907,
                        "viewportHeight": 545
                    }
                },
                "placeContext": {
                    "localTime": "2022-03-21T21:32:59.991-06:00",
                    "localTimezoneOffset": 360
                },
                "timestamp": "2022-03-22T03:32:59.992Z",
                "implementationDetails": {
                    "name": "https://ns.adobe.com/experience/alloy/reactor",
                    "version": "1.0",
                    "environment": "serverapi"
                }
            }
        },
    "query": {
        "identity": {
            "fetch": [
                "ECID"
            ]
        }
    },
    "meta":
        {
            "state":
            {
                "domain": "alloystore.dev",
                "cookiesEnabled": true
            }
        }
}'
```
-->

## Anfrage mit `FPID` übergeben als `identityMap` field

Im folgenden Beispiel wird die [!DNL FPID] als `identityMap` Parameter.

```shell
curl -X POST "https://server.adobedc.net/v2/interact?dataStreamId={DATASTREAM_ID}"
-H "Authorization: Bearer {TOKEN}"
-H "x-gw-ims-org-id: {IMS_ORG_ID}"
-H "x-api-key: {API_KEY}"
-H "Content-Type: application/json"
-d '{
   "event": {
      "xdm": {
         "identityMap": {
            "FPID": [
               {
                  "id": "e98f38e6-6183-442d-8cd2-0e384f4c8aa8",
                  "authenticatedState": "ambiguous",
                  "primary": true
               }
            ]
         },
         "web": {
            "webPageDetails": {
               "URL": "https://alloystore.dev"
            },
            "webReferrer": {
               "URL": ""
            }
         },
         "device": {
            "screenHeight": 1440,
            "screenWidth": 3440,
            "screenOrientation": "landscape"
         },
         "environment": {
            "type": "browser",
            "browserDetails": {
               "viewportWidth": 1907,
               "viewportHeight": 545
            }
         },
         "placeContext": {
            "localTime": "2022-03-21T21:32:59.991-06:00",
            "localTimezoneOffset": 360
         },
         "timestamp": "2022-03-22T03:32:59.992Z",
         "implementationDetails": {
            "name": "https://ns.adobe.com/experience/alloy/reactor",
            "version": "1.0",
            "environment": "serverapi"
         }
      }
   },
   "query": {
      "identity": {
         "fetch": [
            "ECID"
         ]
      }
   }
}'
```
