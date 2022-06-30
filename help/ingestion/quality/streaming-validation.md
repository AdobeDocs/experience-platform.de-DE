---
keywords: Experience Platform; Startseite; beliebte Themen; Streaming; Streaming-Erfassung; Validierung der Streaming-Erfassung; Validierung; Validierung der Streaming-Erfassung; Validierung; synchrone Validierung; synchrone Validierung; asynchrone Validierung; asynchrone Validierung;
solution: Experience Platform
title: Validierung der Streaming-Erfassung
topic-legacy: tutorial
type: Tutorial
description: Mit der Streaming-Erfassung können Sie Ihre Daten mithilfe von Streaming-Endpunkten in Echtzeit in Adobe Experience Platform hochladen. Streaming-Aufnahme-APIs unterstützen zwei Validierungsmodi - synchron und asynchron.
exl-id: 6e9ac943-6d73-44de-a13b-bef6041d3834
source-git-commit: ec8eb0e805f7127dd8712fc3fe08057d1d8c10c1
workflow-type: tm+mt
source-wordcount: '917'
ht-degree: 25%

---

# Validieren der Streaming-Erfasssung

Mit der Streaming-Erfassung können Sie Ihre Daten mithilfe von Streaming-Endpunkten in Echtzeit in Adobe Experience Platform hochladen. Streaming-Aufnahme-APIs unterstützen zwei Validierungsmodi - synchron und asynchron.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von [!DNL Experience Platform] organisiert werden.
- [[!DNL Streaming Ingestion]](../streaming-ingestion/overview.md): Eine der Methoden zum Senden von Daten an [!DNL Experience Platform].

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform], einschließlich derjenigen, die [!DNL Schema Registry], werden auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an [!DNL Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

- Content-Type: `application/json`

### Validierungsabdeckung

[!DNL Streaming Validation Service] umfasst Validierungen in den folgenden Bereichen:
- Bereich
- Präsenz
- Enum
- Muster
- Typ
- Format

## Synchrone Überprüfung

Die synchrone Validierung ist eine Methode zur Validierung, die sofort Rückmeldungen darüber liefert, warum eine Aufnahme fehlgeschlagen ist. Bei einem Fehler werden jedoch die Datensätze, die bei der Validierung fehlschlagen, verworfen und können nicht nachgelagert gesendet werden. Daher sollte die synchrone Validierung nur während des Entwicklungsprozesses verwendet werden. Bei der synchronen Validierung werden die Aufrufer sowohl über das Ergebnis der XDM-Validierung als auch über den Grund für das Fehlschlagen informiert, wenn dies fehlgeschlagen ist.

Standardmäßig ist die synchrone Validierung nicht aktiviert. Um dies zu aktivieren, müssen Sie den optionalen Abfrageparameter übergeben `syncValidation=true` bei API-Aufrufen. Darüber hinaus ist eine synchrone Validierung derzeit nur verfügbar, wenn sich Ihr Stream-Endpunkt im VA7-Rechenzentrum befindet.

>[!NOTE]
>
>Die `syncValidation` Der Abfrageparameter ist nur für den Einzelnachrichten-Endpunkt verfügbar und kann nicht für den Batch-Endpunkt verwendet werden.

Wenn eine Nachricht während der synchronen Validierung fehlschlägt, wird sie nicht in die Ausgabeschlange geschrieben, die Benutzern sofortiges Feedback gibt.

>[!NOTE]
>
>Schemaänderungen sind möglicherweise nicht sofort verfügbar, da Änderungen zwischengespeichert werden. Die Aktualisierung des Caches dauert bis zu fünfzehn Minuten.

**API-Format**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{CONNECTION_ID}` | Die `id` -Wert der zuvor erstellten Streaming-Verbindung. |

**Anfrage**

Senden Sie die folgende Anfrage zur Aufnahme von Daten an Ihren Daten-Inlet mit synchroner Validierung:

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?syncValidation=true \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | Der JSON-Textkörper einer Daten, die Sie erfassen möchten. |

**Antwort**

Wenn die synchrone Validierung aktiviert ist, enthält eine erfolgreiche Antwort alle aufgetretenen Validierungsfehler in ihrer Payload:

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [6aca7aa2d87ebd6b2780ca5724d94324a14475f140a2b69373dd5c714430dfd4] imsOrgId: [7BF122A65C5B3FE40A494026@AdobeOrg] Message is invalid",
        "cause": {
            "_streamingValidation": [
                {
                    "schemaLocation": "#",
                    "pointerToViolation": "#",
                    "causingExceptions": [
                        {
                            "schemaLocation": "#",
                            "pointerToViolation": "#",
                            "causingExceptions": [],
                            "keyword": "additionalProperties",
                            "message": "extraneous key [workEmail] is not permitted"
                        },
                        {
                            "schemaLocation": "#",
                            "pointerToViolation": "#",
                            "causingExceptions": [],
                            "keyword": "additionalProperties",
                            "message": "extraneous key [person] is not permitted"
                        },
                        {
                            "schemaLocation": "#/properties/_id",
                            "pointerToViolation": "#/_id",
                            "causingExceptions": [],
                            "keyword": "type",
                            "message": "expected type: String, found: Long"
                        }
                    ],
                    "message": "3 schema violations found"
                }
            ]
        }
    }
}
```

In der obigen Antwort wird aufgelistet, wie viele Schemafehlungen gefunden wurden und welche Verstöße aufgetreten sind. In dieser Antwort wird beispielsweise angegeben, dass die Schlüssel `workEmail` und `person` wurden nicht im Schema definiert und sind daher nicht zulässig. Es markiert auch den Wert für `_id` nicht korrekt ist, da das Schema eine `string`, aber a `long` stattdessen eingefügt wurde. Beachten Sie, dass der Validierungsdienst nach fünf Fehlern **stop** verarbeitet diese Nachricht. Andere Nachrichten werden jedoch weiterhin analysiert.

## Asynchrone Validierung

Die asynchrone Validierung ist eine Validierungsmethode, die kein unmittelbares Feedback liefert. Stattdessen werden die Daten an einen fehlgeschlagenen Batch in [!DNL Data Lake] um Datenverlust zu vermeiden. Diese fehlgeschlagenen Daten können später zur weiteren Analyse und Wiedergabe abgerufen werden. Diese Methode sollte in der Produktion verwendet werden. Sofern nicht anders angefordert, erfolgt die Streaming-Erfassung im asynchronen Validierungsmodus.

**API-Format**

```http
POST /collection/{CONNECTION_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{CONNECTION_ID}` | Die `id` -Wert der zuvor erstellten Streaming-Verbindung. |

**Anfrage**

Senden Sie die folgende Anfrage mit asynchroner Validierung an den Daten-Inlet, um Daten zu erfassen:

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID} \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | Der JSON-Textkörper einer Daten, die Sie erfassen möchten. |

>[!NOTE]
>
>Es ist kein zusätzlicher Abfrageparameter erforderlich, da die asynchrone Validierung standardmäßig aktiviert ist.

**Antwort**

Bei aktivierter asynchroner Validierung gibt eine erfolgreiche Antwort Folgendes zurück:

```json
{
    "inletId": "f6ca9706d61de3b78be69e2673ad68ab9fb2cece0c1e1afc071718a0033e6877",
    "xactionId": "1555445493896:8600:8",
    "receivedTimeMs": 1555445493932,
    "syncValidation": {
        "skipped": true
    }
}
```

Beachten Sie, dass in der Antwort angegeben wird, dass die synchrone Validierung übersprungen wurde, da sie nicht explizit angefordert wurde.

## Anhang

Dieser Abschnitt enthält Informationen darüber, was die verschiedenen Status-Codes für Antworten zur Aufnahme von Daten bedeuten.

### Status-Codes

| Status-Code | Bedeutung |
| ----------- | ------------- |
| 200 | Erfolgreich. Bei der synchronen Validierung bedeutet dies, dass die Validierungsprüfungen bestanden haben. Bei der asynchronen Validierung bedeutet dies, dass die Nachricht nur erfolgreich empfangen wurde. Benutzer können den Status einer Nachricht ermitteln, indem sie den Datensatz beobachten. |
| 400 | Fehler. Mit deiner Anfrage stimmt etwas nicht. Von den Streaming-Validierungsdiensten wird eine Fehlermeldung mit weiteren Details empfangen. |
| 401 | Fehler. Ihre Anfrage ist nicht autorisiert - Sie müssen sie mit einem Trägertoken anfordern. Weitere Informationen zum Anfordern des Zugriffs finden Sie in diesem [Tutorial](https://www.adobe.com/go/platform-api-authentication-en) oder [Blogpost](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f). |
| 500 | Fehler. Es gibt einen internen Systemfehler. |
| 501 | Fehler. Das bedeutet, dass die synchrone Validierung **not** unterstützt. |
| 503 | Fehler. Der Dienst ist derzeit nicht verfügbar. Clients sollten es mindestens dreimal mit einer exponentiellen Back-off-Strategie versuchen. |
