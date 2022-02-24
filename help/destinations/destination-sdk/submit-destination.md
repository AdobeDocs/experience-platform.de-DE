---
description: Auf dieser Seite finden Sie alle Informationen, die Sie zum Überprüfen eines mit Destination SDK erstellten Ziels senden müssen.
title: Zur Überprüfung eines in Destination SDK erstellten Ziels übermitteln
exl-id: eef0d858-ebd9-426e-91a1-5c93903b0eb5
source-git-commit: 111da9ce3e38096d11a1910929ee892e5661722c
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 1%

---

# Zur Überprüfung eines in Destination SDK erstellten Ziels übermitteln

## Übersicht {#overview}

Bevor Ihr Ziel in der [Experience Platform-Zielkatalog](/help/destinations/catalog/overview.md)müssen Sie der Adobe bestimmte Informationen über das Ziel und die von Ihnen durchgeführten Tests bereitstellen, um sicherzustellen, dass Benutzer beim Aktivieren von Daten für Ihre Plattform das bestmögliche Erlebnis erhalten.

Auf dieser Seite finden Sie alle Informationen, die Sie beim Senden oder Aktualisieren eines mit Adobe Experience Platform Destination SDK erstellten Ziels benötigen. Um ein Ziel in Adobe Experience Platform erfolgreich zu senden, senden Sie eine E-Mail an <aepdestsdk@adobe.com> Folgendes umfasst:

* Eine Beschreibung der Anwendungsfälle, die Ihr Ziel löst. Dies ist nicht erforderlich, wenn Sie eine vorhandene Zielkonfiguration aktualisieren.
* Testergebnisse nach Verwendung des Ziel-API-Endpunkts zum Ausführen eines HTTP-Aufrufs an Ihr Ziel. Teilen Sie mit Adobe:
   * Ein API-Aufruf an Ihren Ziel-Endpunkt.
   * Die API-Antwort, die von Ihrem Ziel-Endpunkt empfangen wurde.
* Der Beweis, dass Sie mit dem [Zielpublikations-API](./destination-publish-api.md).
* (Nur für produktive Integrationen) eine Dokumentation-PR (Pull-Anfrage) entsprechend den Anweisungen im Abschnitt [Self-Service-Dokumentationsprozess](./docs-framework/documentation-instructions.md).
* Eine Bilddatei, die als Logo für Ihre Zielkarte im Zielkatalog der Experience Platform angezeigt wird.

Detaillierte Informationen zu den einzelnen Elementen finden Sie in den folgenden Abschnitten:

## Anwendungsfallbeschreibung

Geben Sie eine Beschreibung der Anwendungsfälle an, die Ihr Ziel für Experience Platform-Kunden löst. Ihre Beschreibungen können Nutzungsszenarios von vorhandenen Partnern ähneln:

* [Pinterest](/help/destinations/catalog/advertising/pinterest.md): Erstellen Sie Zielgruppen aus Ihren Kundenlisten, Personen, die Ihre Site besucht haben, oder Personen, die bereits mit Ihren Inhalten in Pinterest interagiert haben.
* [Yahoo Data X](/help/destinations/catalog/advertising/datax.md#use-cases): DataX-APIs sind für Advertiser verfügbar, die eine bestimmte Zielgruppen-Gruppe ansprechen möchten, die von E-Mail-Adressen in Verizon Media (VMG) abgeleitet wurde. Diese können schnell ein neues Segment erstellen und die gewünschte Zielgruppe mithilfe der nahezu Echtzeit-API von VMG übertragen.

## Testergebnisse nach Verwendung der Test-Ziel-API

Stellen Sie die Testergebnisse nach Verwendung der [Test-Ziel-API](./test-destination.md) -Endpunkt verwenden, um einen HTTP-Aufruf an Ihr Ziel durchzuführen. Dazu gehören:

* Die vollständige API-Anfrage (Kopfzeilen und Hauptteil), die mithilfe der Test-API an Ihren Ziel-Endpunkt gesendet wurde.
* Die API-Antwort, die von Ihrem Ziel-Endpunkt empfangen wurde.

Ihre Anfrage und Antwort können beispielsweise in etwa wie folgt aussehen:

**Anfrage**

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

**Antwort**

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

## Nachweis, dass Sie eine Zielveröffentlichungsanforderung gesendet haben

Nachdem Sie Ihr Ziel erfolgreich getestet haben, müssen Sie die [Zielpublikations-API](./destination-publish-api.md) , um das Ziel zur Überprüfung und Veröffentlichung an Adobe zu senden.

Geben Sie die ID der Veröffentlichungsanforderung für Ihr Ziel an. Informationen zum Abrufen der Veröffentlichungsanfrage-ID finden Sie unter [Veröffentlichungsanforderungen des Ziels auflisten](./destination-publish-api.md#retrieve-list).

## Zieldokumentation PR (Pull-Anforderung) für produktionierte Integrationen

Wenn Sie ein unabhängiger Software-Anbieter (ISV) oder Systemintegrator (SI) sind und eine [produktive Integration](./overview.md#productized-custom-integrations), verwenden Sie die [Self-Service-Dokumentationsprozess](./docs-framework/documentation-instructions.md) , um eine Produktdokumentationsseite für Ihr Ziel zu erstellen. Stellen Sie als Teil des Sendevorgangs die Pull-Anforderung (PA) für Ihre Zieldokumentation bereit.

## Logo für Ihr Ziel

Der Zielkatalog enthält ein Logo für jede Zielkarte. Fügen Sie in Ihrer E-Mail zur Übermittlung ein Bild mit dem Logo für Ihr Ziel ein.

Die Bildanforderungen sind:
* **Format**: `SVG`
* **Größe**: weniger als 2 MB

## Beispiel-E-Mail herunterladen

[Download](./assets/sample-email-submit-destination.rtf) eine Beispiel-E-Mail mit allen Informationen, die Sie für Adobe bereitstellen müssen.
