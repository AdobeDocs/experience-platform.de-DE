---
title: Besucheridentifizierung über FPID
description: Erfahren Sie, wie Sie Besuchende mit der Server-API mithilfe der FPID konsistent identifizieren.
seo-description: Learn how to consistently identify visitors via the Server API, by using the FPID
keywords: Edge Network;Gateway;API;Besucher;Besucherin;Identifizierung;FPID
exl-id: c61d2e7c-7b5e-4b14-bd52-13dde34e32e3
source-git-commit: 6798c15b1cee781c41b9faf5cc6dcfa73090a60a
workflow-type: ht
source-wordcount: '348'
ht-degree: 100%

---

# Besucheridentifizierung über FPID

[!DNL First-party IDs] (`FPIDs`) sind Geräte-IDs, die von Kundinnen und Kunden generiert, verwaltet und gespeichert werden. Dadurch erhalten Kundinnen und Kunden Kontrolle über die Identifizierung von Benutzergeräten. Durch den Versand von `FPIDs` generiert das Edge Network keine brandneue `ECID` für eine Anfrage, die keine enthält.

Die `FPID` kann im API-Anfragetext als Teil der `identityMap` gesendet werden, oder aber als Cookie.

Eine `FPID` kann durch das Edge Network deterministisch in eine `ECID` umgewandelt werden, sodass `FPID`-Identitäten vollständig mit Experience Cloud-Lösungen kompatibel sind. Das Beziehen einer `ECID` aus einer bestimmten `FPID` liefert immer dasselbe Ergebnis, sodass Benutzende ein konsistentes Erlebnis haben.

Die auf diese Weise erhaltene `ECID` kann über eine `identity.fetch`-Abfrage abgerufen werden:

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

Bei Anfragen, die sowohl eine `FPID` als auch eine `ECID` enthalten, hat die bereits in der Anfrage vorhandene `ECID` Vorrang vor derjenigen, die aus der `FPID` generiert werden könnte. Mit anderen Worten: Das Edge Network verwendet die bereits vorhandene `ECID` und ignoriert die `FPID`. Eine neue `ECID` wird nur dann generiert, wenn eine `FPID` eigenständig bereitgestellt wird.

Was die Geräte-IDs betrifft, so sollten die `server`-Datenströme die `FPID` als Geräte-ID verwenden. Andere Identitäten (z. B. `EMAIL`) können zwar ebenfalls im Anfragetext angegeben werden, aber das Edge Network verlangt, dass eine primäre Identität ausdrücklich angegeben wird. Die primäre Identität ist die Basisidentität, unter der die Profildaten gespeichert werden.

>[!NOTE]
>
>Anfragen, die keine Identität bzw. keine explizit im Anfragetext festgelegte primäre Identität aufweisen, schlagen fehl.

Die folgende `identityMap`-Feldergruppe hat die korrekte Form für eine `server`-Datenstromanfrage:

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

Die folgende `identityMap`-Feldergruppe führt zu einer Fehlerantwort, wenn sie auf eine `server`-Datenstromanfrage gesetzt wird:

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

Um Benutzende über eine `FPID` zu identifizieren, stellen Sie sicher, dass das `FPID`-Cookie gesendet wurde, bevor Sie eine Anfrage an das Edge Network stellen. Die `FPID` kann in einem Cookie oder als Teil der `identityMap` im Text der Anfrage übergeben werden.

<!--

## Request with `FPID` passed as cookie header

```shell
curl -X POST 'https://edge.adobedc.net/v2/interact?dataStreamId={Data Stream ID}' \
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

## Anfrage mit Übergabe der `FPID` als `identityMap`-Feld

Im folgenden Beispiel wird die [!DNL FPID] als `identityMap`-Parameter übergeben.

```shell
curl -X POST "https://server.adobedc.net/v2/interact?dataStreamId={DATASTREAM_ID}"
-H "Authorization: Bearer {TOKEN}"
-H "x-gw-ims-org-id: {ORG_ID}"
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
