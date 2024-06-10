---
description: Auf dieser Seite finden Sie alle Informationen, die Sie zum Überprüfen eines mit Destination SDK erstellten produktiven Ziels übermitteln müssen.
title: Zur Überprüfung eines in der Destination SDK erstellten produktisierten Ziels übermitteln
exl-id: eef0d858-ebd9-426e-91a1-5c93903b0eb5
source-git-commit: 2c778f98815af87453e84f24ba8bf077774349a1
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 36%

---

# Zur Überprüfung eines in der Destination SDK erstellten produktisierten Ziels übermitteln

## Übersicht {#overview}

>[!IMPORTANT]
>
>* Der hier dokumentierte Prozess ist nur für Partner erforderlich, die produktierte (öffentliche) Ziele übermitteln. Wenn Sie ein privates Ziel für Ihren eigenen Gebrauch erstellen, müssen Sie diese Materialien nicht herstellen und mit Adobe teilen.
>
>* Die standardmäßige Antwortzeit von Adobe zur Überprüfung des Ziels beträgt fünf Werktage.
>
>* Wenn das Adobe-Team nach der ersten Übermittlung darum bittet, Ihre Konfigurationen zu aktualisieren, müssen Sie nach der Aktualisierung eine weitere Ziel-Veröffentlichungsanforderung senden.
>
>* Selbst wenn Ihr Ziel im Experience Platform-Katalog live ist, müssen Sie, wenn Sie Ihre Konfigurationen aktualisieren müssen, eine neue Ziel-Veröffentlichungsanforderung senden, damit die Aktualisierungen in den Konfigurationen angezeigt werden.
>
>* Die Zeitleiste der Überprüfung und die erforderlichen Artefakte sind für neue Ziele und vorhandene Ziele, die Sie aktualisieren, identisch.

Bevor Ihr Ziel im [Experience Platform-Zielkatalog](/help/destinations/catalog/overview.md) veröffentlicht werden kann, müssen Sie Adobe bestimmte Informationen über das Ziel und die von Ihnen durchgeführten Tests zukommen lassen, um sicherzustellen, dass die Anwender beim Aktivieren von Daten auf Ihrer Plattform die bestmöglichen Ergebnisse erzielen.

Auf dieser Seite sind alle Informationen aufgeführt, die Sie angeben müssen, wenn Sie ein mit dem Adobe Experience Platform Destination SDK erstelltes Ziel übermitteln oder aktualisieren. Um ein Ziel in Adobe Experience Platform erfolgreich zu übermitteln, senden Sie eine E-Mail an <aepdestsdk@adobe.com>, die folgende Informationen enthält:

* Eine Beschreibung der Anwendungsfälle, die Ihr Ziel löst. Dies ist nur erforderlich, wenn Sie eine neue Zielkonfiguration übermitteln.
* Eine Beschreibung des Grundes für die Zielübermittlung. Dies ist nur erforderlich, wenn Sie eine vorhandene Zielkonfiguration aktualisieren.
* Testergebnisse nach Verwendung des Destination API-Endpunkts zum Ausführen eines HTTP-Aufrufs an Ihr Ziel. Geben Sie an die Adobe einen API-Aufruf für Ihren Ziel-Endpunkt und die API-Antwort weiter, die Sie von Ihrem Ziel-Endpunkt erhalten haben.
* Zusätzliche Anforderungen für dateibasierte Ziele:
   * Geben Sie nach Verwendung der Test-API eine Anfrage und ein Antwort-Beispiel für [Testen Ihres dateibasierten Ziels mit Beispielprofilen](../testing-api/batch-destinations/file-based-destination-testing-api.md).
   * Fügen Sie eine Beispieldatei an, die von Ihrem Ziel generiert und an Ihren Speicherort exportiert wurde.
   * Senden Sie eine Form des Nachweises, dass Sie die exportierte Datei erfolgreich vom Speicherort in Ihr System aufgenommen haben.
* Nachweis, dass Sie eine Anfrage zur Veröffentlichung eines Ziels für Ihr Ziel mithilfe der [Zielveröffentlichungs-API](../publishing-api/create-publishing-request.md) übermittelt haben.
* Eine Dokumentation-PR (Pull-Anfrage) entsprechend den Anweisungen im Abschnitt [Self-Service-Dokumentationsprozess](../docs-framework/documentation-instructions.md).
* Eine Grafikdatei, die als Logo für Ihre Zielkarte im Zielkatalog von Experience Platform angezeigt werden soll.

Detaillierte Informationen zu den einzelnen Elementen finden Sie in den folgenden Abschnitten:

## Beschreibung der Anwendungsfälle {#use-case-description}

Geben Sie eine Beschreibung der Anwendungsfälle an, die Ihr Ziel für Experience Platform-Kunden löst. Ihre Beschreibungen können Anwendungsfällen von vorhandenen Partnern ähneln:

* [Pinterest](/help/destinations/catalog/advertising/pinterest.md): Erstellen Sie Zielgruppen aus Ihren Kundenlisten, Personen, die Ihre Site besucht haben, oder Personen, die bereits mit Ihren Inhalten in Pinterest interagiert haben.
* [Yahoo Data X](/help/destinations/catalog/advertising/datax.md#use-cases): DataX-APIs sind für Advertiser verfügbar, die eine bestimmte Zielgruppe mit E-Mail-Adressen in Verizon Media (VMG) ansprechen möchten, die über die E-Mail-Adresse eingegeben wurde. Dadurch kann schnell eine neue Zielgruppe erstellt und die gewünschte Zielgruppe mithilfe der API nahezu in Echtzeit gepusht werden.

## Grund für die Aktualisierung {#reason-for-update}

>[!NOTE]
>
>Dieser Abschnitt ist nur erforderlich, wenn Sie eine vorhandene Konfiguration aktualisieren.

Geben Sie eine kurze Beschreibung des Problems, das Ihre Übermittlung für das vorhandene Ziel löst. Beispielsweise könnte Ihre Übermittlung den Namen, die Beschreibung und das Logo Ihres Ziels aktualisieren, wenn Sie von der Beta-Version zur allgemeinen Verfügbarkeit wechseln. Oder Ihre Übermittlung kann einen Fehler beheben, der in Ihrer Zielkonfiguration gefunden wurde.

## Testergebnisse nach Verwendung der Test-Ziel-API {#testing-api-response}

Stellen Sie Testergebnisse bereit, nachdem Sie den Endpunkt [Test-Ziel-API](../testing-api/streaming-destinations/streaming-destination-testing-overview.md) verwendet haben, um einen HTTP-Aufruf an Ihr Ziel durchzuführen. Dazu gehören:

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

## Zusätzliche Anforderungen für dateibasierte Ziele {#additional-file-based-destination-requirements}

Bei dateibasierten Zielen müssen Sie einen zusätzlichen Nachweis darüber erbringen, dass Sie Ihr Ziel korrekt eingerichtet haben. Stellen Sie sicher, dass Sie die folgenden Elemente einschließen:

### API-Antwort testen {#testing-api-response-file-based}

Schließen Sie eine Anfrage und ein Antwort-Beispiel ein, nachdem Sie die Test-API verwendet haben, um [Testen Ihres dateibasierten Ziels mit Beispielprofilen](../testing-api/batch-destinations/file-based-destination-testing-api.md).

### Exportierte Datei anhängen {#attach-exported-file}

In der [Einsendenummer](#download-sample-email), fügen Sie eine CSV-Datei an, die von dem von Ihnen eingerichteten Ziel in Ihren Speicherort exportiert wurde.

### Nachweis der erfolgreichen Aufnahme {#proof-of-successful-ingestion}

Schließlich müssen Sie eine Form des Nachweises vorlegen, dass die Daten nach dem Export in den von Ihnen angegebenen Speicherort erfolgreich in Ihr System aufgenommen wurden. Bitte geben Sie eine der folgenden Informationen an:

* Screenshots oder ein kurzes Screenshot-Video, in dem Sie die Datei manuell vom Speicherort abrufen und in Ihr System aufnehmen.
* Screenshots oder ein kurzes Screenshot-Video, in dem die Benutzeroberfläche Ihres Systems bestätigt, dass der von Experience Platform generierte Dateiname erfolgreich in Ihr System aufgenommen wurde.
* Loggen Sie Zeilen aus Ihrem System ein, die Adobe entweder mit dem Dateinamen oder mit den von Experience Platform generierten Daten korrelieren kann.

## Nachweis, dass Sie eine Zielveröffentlichungsanfrage übermittelt haben {#destination-publishing-request-proof}

Nachdem Sie Ihr Ziel erfolgreich getestet haben, müssen Sie die [Zielveröffentlichungs-API](../publishing-api/create-publishing-request.md) verwenden, um das Ziel zur Überprüfung und Veröffentlichung an Adobe zu übermitteln.

Geben Sie die ID der Veröffentlichungsanfrage für Ihr Ziel an. Informationen zum Abrufen der Veröffentlichungsanfrage-ID finden Sie unter [Zielveröffentlichungsanfragen abrufen](../publishing-api/retrieve-publishing-request.md).

## Zieldokumentations-PR (Pull-Anfrage) für produktbezogene Integrationen {#documentation-pr}

Wenn Sie ein unabhängiger Software-Anbieter (ISV) oder Systemintegrator (SI) sind und eine [produktive Integration](../overview.md#productized-custom-integrations), müssen Sie die [Self-Service-Dokumentationsprozess](../docs-framework/documentation-instructions.md) , um eine Produktdokumentationsseite für Ihr Ziel zu erstellen. Stellen Sie als Teil des Übermittlungsprozesses die Pull-Anfrage (PR) für Ihre Zieldokumentation bereit.

## Logo für Ihr Ziel {#logo}

Der Zielkatalog enthält ein Logo für jede Zielkarte. Fügen Sie in Ihrer E-Mail zur Übermittlung ein Bild mit dem Logo für Ihr Ziel ein.

Die Bildanforderungen sind:
* **Format**: `SVG`
* **Größe**: weniger als 2 MB

## Herunterladen einer Beispiel-E-Mail {#download-sample-email}

Laden Sie [hier](../assets/guides/sample-email-submit-destination.rtf) eine Beispiel-E-Mail mit allen Informationen herunter, die Sie Adobe zur Verfügung stellen müssen.
