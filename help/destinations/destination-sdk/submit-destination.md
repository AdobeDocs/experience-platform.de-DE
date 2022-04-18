---
description: Auf dieser Seite finden Sie alle Informationen, die Sie zum Überprüfen eines mit dem Destination SDK erstellten Ziels übermitteln müssen.
title: Übermitteln eines im Destination SDK erstellten Ziels zur Überprüfung
exl-id: eef0d858-ebd9-426e-91a1-5c93903b0eb5
source-git-commit: 7c6d0c8d4d1eea16f13359e9d7a895d767ad3c00
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 87%

---

# Übermitteln eines im Destination SDK erstellten Ziels zur Überprüfung

## Übersicht {#overview}

Bevor Ihr Ziel im [Experience Platform-Zielkatalog](/help/destinations/catalog/overview.md) veröffentlicht werden kann, müssen Sie Adobe bestimmte Informationen über das Ziel und die von Ihnen durchgeführten Tests zukommen lassen, um sicherzustellen, dass die Anwender beim Aktivieren von Daten auf Ihrer Plattform die bestmöglichen Ergebnisse erzielen.

Auf dieser Seite sind alle Informationen aufgeführt, die Sie angeben müssen, wenn Sie ein mit dem Adobe Experience Platform Destination SDK erstelltes Ziel übermitteln oder aktualisieren. Um ein Ziel in Adobe Experience Platform erfolgreich zu übermitteln, senden Sie eine E-Mail an <aepdestsdk@adobe.com>, die folgende Informationen enthält:

* Eine Beschreibung der Anwendungsfälle, die Ihr Ziel löst. Dies ist nicht erforderlich, wenn Sie eine vorhandene Zielkonfiguration aktualisieren.
* Testergebnisse nach Verwendung des Destination API-Endpunkts zum Ausführen eines HTTP-Aufrufs an Ihr Ziel. Bitte teilen Sie Adobe Folgendes mit:
   * Ein API-Aufruf an Ihren Ziel-Endpunkt.
   * Die API-Antwort, die von Ihrem Ziel-Endpunkt empfangen wurde.
* Nachweis, dass Sie eine Anfrage zur Veröffentlichung eines Ziels für Ihr Ziel mithilfe der [Zielveröffentlichungs-API](./destination-publish-api.md) übermittelt haben.
* (Nur für produktive Integrationen) eine Dokumentations-PR (Pull-Anfrage) entsprechend den Anweisungen im Abschnitt [Selbstbedienungs-Dokumentationsprozess](./docs-framework/documentation-instructions.md).
* Eine Grafikdatei, die als Logo für Ihre Zielkarte im Zielkatalog von Experience Platform angezeigt werden soll.

>[!IMPORTANT]
>
>* Die standardmäßige Antwortzeit von Adobe zur Überprüfung von Ziel-Veröffentlichungsanforderungen beträgt fünf Werktage.
>
>* Wenn das Adobe-Team nach der ersten Übermittlung darum bittet, Ihre Konfigurationen zu aktualisieren, müssen Sie nach der Aktualisierung eine weitere Ziel-Veröffentlichungsanforderung senden.
>
>* Selbst wenn Ihr Ziel im Experience Platform-Katalog aktiv ist, müssen Sie, wenn Sie Ihre Konfigurationen aktualisieren müssen, eine neue Ziel-Veröffentlichungsanforderung senden, damit die Aktualisierungen in den Konfigurationen angezeigt werden.


Detaillierte Informationen zu den einzelnen Elementen finden Sie in den folgenden Abschnitten:

## Beschreibung der Anwendungsfälle

Geben Sie eine Beschreibung der Anwendungsfälle an, die Ihr Ziel für Experience Platform-Kunden löst. Ihre Beschreibungen können Anwendungsfällen von vorhandenen Partnern ähneln:

* [Pinterest](/help/destinations/catalog/advertising/pinterest.md): Erstellen Sie Zielgruppen aus Ihren Kundenlisten, Personen, die Ihre Site besucht haben, oder Personen, die bereits mit Ihren Inhalten in Pinterest interagiert haben.
* [Yahoo Data X](/help/destinations/catalog/advertising/datax.md#use-cases): DataX-APIs sind für Werbetreibende verfügbar, die bestimmte Zielgruppen ansprechen möchten, die von E-Mail-Adressen in Verizon Media (VMG) abgeleitet wurden. Sie können schnell ein neues Segment erstellen und mithilfe der Fast-Echtzeit-API von VMG an die gewünschten Zielgruppen senden.

## Testergebnisse nach Verwendung der Test-Ziel-API

Stellen Sie Testergebnisse bereit, nachdem Sie den Endpunkt [Test-Ziel-API](./test-destination.md) verwendet haben, um einen HTTP-Aufruf an Ihr Ziel durchzuführen. Dazu gehören:

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

## Nachweis, dass Sie eine Zielveröffentlichungsanfrage übermittelt haben

Nachdem Sie Ihr Ziel erfolgreich getestet haben, müssen Sie die [Zielveröffentlichungs-API](./destination-publish-api.md) verwenden, um das Ziel zur Überprüfung und Veröffentlichung an Adobe zu übermitteln.

Geben Sie die ID der Veröffentlichungsanfrage für Ihr Ziel an. Weitere Informationen zum Abrufen der Veröffentlichungsanfragen-ID finden Sie unter [Auflisten der Veröffentlichungsanfragen für Ziele](./destination-publish-api.md#retrieve-list).

## Zieldokumentations-PR (Pull-Anfrage) für produktbezogene Integrationen

Wenn Sie als unabhängiger Software-Anbieter (ISV) oder Systemintegrator (SI) eine [produktbezogene Integration](./overview.md#productized-custom-integrations) erstellen, verwenden Sie den [Selbstbedienungs-Dokumentationsprozess](./docs-framework/documentation-instructions.md), um eine Produktdokumentationsseite für Ihr Ziel zu erstellen. Stellen Sie als Teil des Übermittlungsprozesses die Pull-Anfrage (PR) für Ihre Zieldokumentation bereit.

## Logo für Ihr Ziel

Der Zielkatalog enthält ein Logo für jede Zielkarte. Fügen Sie in Ihrer E-Mail zur Übermittlung ein Bild mit dem Logo für Ihr Ziel ein.

Die Bildanforderungen sind:
* **Format**: `SVG`
* **Größe**: weniger als 2 MB

## Herunterladen einer Beispiel-E-Mail

Laden Sie [hier](./assets/sample-email-submit-destination.rtf) eine Beispiel-E-Mail mit allen Informationen herunter, die Sie Adobe zur Verfügung stellen müssen.
