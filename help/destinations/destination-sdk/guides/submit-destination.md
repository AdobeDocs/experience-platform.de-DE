---
description: Auf dieser Seite finden Sie alle Informationen, die Sie benötigen, um ein produktbezogenes Ziel zur Überprüfung zu übermitteln, wenn Sie es mit Destination SDK erstellen.
title: Ein produktbezogenes Ziel zur Überprüfung einreichen
exl-id: eef0d858-ebd9-426e-91a1-5c93903b0eb5
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 35%

---

# Ein produktbezogenes Ziel zur Überprüfung einreichen

## Überblick {#overview}

>[!IMPORTANT]
>
>* Der hier dokumentierte Prozess ist nur für Partner erforderlich, die produktbezogene (öffentliche) Ziele einreichen. Wenn Sie ein privates Ziel für Ihre eigene Verwendung erstellen, müssen Sie diese Materialien nicht erstellen und mit Adobe teilen.
>
>* Die standardmäßige Antwortzeit von Adobe zur Überprüfung von Zielveröffentlichungsanfragen beträgt fünf Werktage.
>
>* Wenn Sie vom Adobe-Team nach der ersten Übermittlung aufgefordert werden, Aktualisierungen an Ihren Konfigurationen vorzunehmen, müssen Sie nach den Aktualisierungen eine weitere Anfrage zum Ziel der Veröffentlichung senden.
>
>* Wenn Sie Aktualisierungen an Ihren Konfigurationen vornehmen müssen, müssen Sie auch nach der Live-Schaltung Ihres Ziels im Experience Platform-Katalog eine neue Anfrage zum Ziel der Veröffentlichung senden, damit die Aktualisierungen in den Konfigurationen widergespiegelt werden.
>
>* Die Zeitleiste der Überprüfung und die erforderlichen Artefakte sind für neue Ziele und vorhandene Ziele, die Sie aktualisieren, identisch.

Bevor Ihr Ziel im [Experience Platform-Zielkatalog](/help/destinations/catalog/overview.md) veröffentlicht werden kann, müssen Sie Adobe bestimmte Informationen über das Ziel und die von Ihnen durchgeführten Tests zukommen lassen, um sicherzustellen, dass die Anwender beim Aktivieren von Daten auf Ihrer Plattform die bestmöglichen Ergebnisse erzielen.

Auf dieser Seite sind alle Informationen aufgeführt, die Sie angeben müssen, wenn Sie ein mit dem Adobe Experience Platform Destination SDK erstelltes Ziel übermitteln oder aktualisieren. Um ein Ziel in Adobe Experience Platform erfolgreich zu übermitteln, senden Sie eine E-Mail an <aepdestsdk@adobe.com>, die folgende Informationen enthält:

* Eine Beschreibung der Anwendungsfälle, die Ihr Ziel löst. Dies ist nur erforderlich, wenn Sie eine neue Zielkonfiguration senden.
* Eine Beschreibung des Grundes für die Übermittlung Ihres Ziels. Dies ist nur erforderlich, wenn Sie eine vorhandene Zielkonfiguration aktualisieren.
* Testergebnisse nach Verwendung des Destination API-Endpunkts zum Ausführen eines HTTP-Aufrufs an Ihr Ziel. Bitte teilen Sie Adobe einen API-Aufruf an Ihren Ziel-Endpunkt und die API-Antwort, die von Ihrem Ziel-Endpunkt empfangen wurde.
* Eine Bildschirmaufzeichnung, die das Benutzererlebnis für jemanden zeigt, der eine Verbindung zu Ihrem Ziel herstellt und die Aktivierungsschritte durchläuft.
* Zusätzliche Anforderungen für dateibasierte Ziele:
   * Geben Sie eine Anfrage und ein Beispiel für eine Antwort frei, nachdem Sie die Test[API verwendet haben, um Ihr dateibasiertes Ziel mit Beispielprofilen zu &#x200B;](../testing-api/batch-destinations/file-based-destination-testing-api.md).
   * Hängen Sie eine Beispieldatei an, die von Ihrem Ziel generiert und an Ihren Speicherort exportiert wurde.
   * Senden Sie eine Form des Nachweises, dass Sie die exportierte Datei vom Speicherort erfolgreich in Ihr System aufgenommen haben.
* Nachweis, dass Sie eine Anfrage zur Veröffentlichung eines Ziels für Ihr Ziel mithilfe der [Zielveröffentlichungs-API](../publishing-api/create-publishing-request.md) übermittelt haben.
* Eine Dokumentations-PR (Pull-Anfrage) entsprechend den Anweisungen im Abschnitt [Selbstbedienungs-Dokumentationsprozess](../docs-framework/documentation-instructions.md).
* Eine Grafikdatei, die als Logo für Ihre Zielkarte im Zielkatalog von Experience Platform angezeigt werden soll.

Detaillierte Informationen zu den einzelnen Elementen finden Sie in den folgenden Abschnitten:

## Beschreibung der Anwendungsfälle {#use-case-description}

Geben Sie eine Beschreibung der Anwendungsfälle an, die Ihr Ziel für Experience Platform-Kunden löst. Ihre Beschreibungen können Anwendungsfällen von vorhandenen Partnern ähneln:

* [Pinterest](/help/destinations/catalog/advertising/pinterest.md): Erstellen Sie Zielgruppen aus Ihren Kundenlisten, Personen, die Ihre Site besucht haben, oder Personen, die bereits mit Ihren Inhalten in Pinterest interagiert haben.
* [Yahoo Data X](/help/destinations/catalog/advertising/datax.md#use-cases): DataX-APIs sind für Werbetreibende verfügbar, die bestimmte Zielgruppen ansprechen möchten, die von E-Mail-Adressen in Verizon Media (VMG) abgeleitet wurden. Sie können schnell eine neue Zielgruppe erstellen und mithilfe der Fast-Echtzeit-API von VMG an die gewünschte Zielgruppe senden.

## Grund für die Aktualisierung {#reason-for-update}

>[!NOTE]
>
>Dieser Abschnitt ist nur erforderlich, wenn Sie eine vorhandene Konfiguration aktualisieren.

Geben Sie eine kurze Beschreibung des Problems an, das durch Ihre Übermittlung für das vorhandene Ziel gelöst wird. Ihre Übermittlung kann beispielsweise den Namen, die Beschreibung und das Logo Ihres Ziels aktualisieren, wenn Sie von der Betaversion zur allgemeinen Verfügbarkeit wechseln. Oder Ihre Übermittlung behebt einen Fehler, der in Ihrer Zielkonfiguration entdeckt wurde.

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

Bei dateibasierten Zielen müssen Sie einen zusätzlichen Nachweis dafür erbringen, dass Sie Ihr Ziel korrekt eingerichtet haben. Stellen Sie sicher, dass Sie die folgenden Elemente einbeziehen:

### Testen der API-Antwort {#testing-api-response-file-based}

Fügen Sie nach Verwendung der Test-API eine Anfrage und ein Antwortbeispiel [, um Ihr dateibasiertes Ziel mit Beispielprofilen zu &#x200B;](../testing-api/batch-destinations/file-based-destination-testing-api.md).

### Exportierte Datei anhängen {#attach-exported-file}

Hängen Sie in Ihrer [Einreichungs-E](#download-sample-email)Mail) eine CSV-Datei an, die von dem von Ihnen eingerichteten Ziel an Ihren Speicherort exportiert wurde.

### Nachweis der erfolgreichen Aufnahme {#proof-of-successful-ingestion}

Schließlich müssen Sie eine Art von Nachweis dafür erbringen, dass die Daten erfolgreich in Ihr System aufgenommen wurden, nachdem sie an den von Ihnen angegebenen Speicherort exportiert wurden. Geben Sie eines der folgenden Elemente an:

* Screenshots oder ein kurzes Screenshot-Video, in dem Sie die Datei manuell vom Speicherort abrufen und in Ihr System aufnehmen.
* Screenshots oder ein kurzes Screenshot-Video, in dem die Benutzeroberfläche Ihres Systems bestätigt, dass der von Experience Platform generierte Dateiname erfolgreich in Ihr System aufgenommen wurde.
* Protokollieren Sie Zeilen von Ihrem System, die Adobe entweder mit dem Dateinamen oder mit den von Experience Platform generierten Daten korrelieren kann.

## Nachweis, dass Sie eine Zielveröffentlichungsanfrage übermittelt haben {#destination-publishing-request-proof}

Nachdem Sie Ihr Ziel erfolgreich getestet haben, müssen Sie die [Zielveröffentlichungs-API](../publishing-api/create-publishing-request.md) verwenden, um das Ziel zur Überprüfung und Veröffentlichung an Adobe zu übermitteln.

Geben Sie die ID der Veröffentlichungsanfrage für Ihr Ziel an. Informationen zum Abrufen der Veröffentlichungsanfrage-ID finden Sie unter Abrufen [Veröffentlichungsanfragen für Ziele](../publishing-api/retrieve-publishing-request.md).

## Zieldokumentations-PR (Pull-Anfrage) für produktbezogene Integrationen {#documentation-pr}

Wenn Sie als unabhängiger Software-Anbieter (ISV) oder Systemintegrator (SI) eine [produktbezogene Integration](../overview.md#productized-custom-integrations) erstellen, müssen Sie den [Self-Service-Dokumentationsprozess](../docs-framework/documentation-instructions.md) verwenden, um eine Produktdokumentationsseite für Ihr Ziel zu erstellen. Stellen Sie als Teil des Übermittlungsprozesses die Pull-Anfrage (PR) für Ihre Zieldokumentation bereit.

## Logo für Ihr Ziel {#logo}

Der Zielkatalog enthält ein Logo für jede Zielkarte. Fügen Sie in Ihrer E-Mail zur Übermittlung ein Bild mit dem Logo für Ihr Ziel ein.

Die Bildanforderungen sind:

* **Format**: `SVG`
* **Größe**: weniger als 2 MB

## Herunterladen einer Beispiel-E-Mail {#download-sample-email}

Laden Sie [hier](../assets/guides/sample-email-submit-destination.rtf) eine Beispiel-E-Mail mit allen Informationen herunter, die Sie Adobe zur Verfügung stellen müssen.
