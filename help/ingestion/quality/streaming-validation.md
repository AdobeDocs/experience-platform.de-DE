---
keywords: Experience Platform;home;popular topics;streaming;streaming ingestion;streaming ingestion validation;validation;Streaming ingestion validation;validate;Synchronous validation;synchronous validation;Asynchronous validation;asynchronous validation;
solution: Experience Platform
title: Validieren der Streaming-Erfasssung
topic: tutorial
type: Tutorial
description: Mit der Streaming-Erfassung können Sie Ihre Daten mit Streaming-Endpunkten in Echtzeit nach Adobe Experience Platform hochladen. Die Streaming-Erfassungsmethode-APIs unterstützen zwei Überprüfungsmodi - synchron und asynchron.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 23%

---


# Validieren der Streaming-Erfasssung

Mit der Streaming-Erfassung können Sie Ihre Daten mit Streaming-Endpunkten in Echtzeit nach Adobe Experience Platform hochladen. Die Streaming-Erfassungsmethode-APIs unterstützen zwei Überprüfungsmodi - synchron und asynchron.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
- [[!DNL Streaming Ingestion]](../streaming-ingestion/overview.md): Eine der Methoden, mit denen Daten gesendet werden können [!DNL Experience Platform].

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](../../tutorials/authentication.md) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to the [!DNL Schema Registry], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

- Content-Type: `application/json`

### Überprüfungsabdeckung

[!DNL Streaming Validation Service] umfasst die Validierung in folgenden Bereichen:
- Bereich
- Präsenz
- Enum
- Muster
- Typ
- Format

## Synchrone Überprüfung

Die synchrone Validierung ist eine Methode der Validierung, die sofort Rückmeldungen darüber liefert, warum eine Erfassung fehlgeschlagen ist. Bei einem Fehler werden die fehlerhaften Datensätze jedoch abgelegt und können nicht nachgelagert werden. Daher sollte die synchrone Validierung nur während des Entwicklungsprozesses verwendet werden. Bei der synchronen Validierung werden die Aufrufer sowohl über das Ergebnis der XDM-Überprüfung als auch, falls diese fehlgeschlagen ist, über den Grund für den Fehler informiert.

Standardmäßig ist die synchrone Überprüfung nicht aktiviert. Um dies zu aktivieren, müssen Sie den optionalen Parameter &quot;Abfrage&quot; `synchronousValidation=true` bei API-Aufrufen übergeben. Darüber hinaus ist eine synchrone Validierung derzeit nur verfügbar, wenn sich Ihr Stream-Endpunkt im VA7-Rechenzentrum befindet.

Wenn eine Nachricht während der synchronen Überprüfung fehlschlägt, wird die Nachricht nicht in die Ausgabelange geschrieben, was Benutzern sofortige Rückmeldungen gibt.

**API-Format**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{CONNECTION_ID}` | The `id` value of the streaming connection previously created. |

**Anfrage**

Senden Sie die folgende Anforderung mit synchroner Validierung an Ihren Dateneinlass, um Daten zu erfassen:

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?synchronousValidation=true \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | Der JSON-Textkörper einer Daten, die Sie erfassen möchten. |

**Antwort**

Bei aktivierter synchroner Validierung enthält eine erfolgreiche Antwort alle aufgetretenen Validierungsfehler in ihrer Nutzlast:

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

Die oben genannte Antwort Liste, wie viele Verstöße gegen das Schema festgestellt wurden und wie hoch die Verstöße waren. In dieser Antwort heißt es beispielsweise, dass die Schlüssel `workEmail` `person` und Schlüssel nicht im Schema definiert wurden und daher nicht zulässig sind. Er kennzeichnet auch den Wert für `_id` als inkorrekt, da das Schema eine erwartete `string`, aber stattdessen eine `long` eingefügt wurde. Beachten Sie, dass der Überprüfungsdienst die Verarbeitung dieser Meldung **stoppt** , sobald fünf Fehler aufgetreten sind. Andere Nachrichten werden jedoch weiterhin analysiert.

## Asynchrone Überprüfung

Die asynchrone Validierung ist eine Methode der Validierung, die kein sofortiges Feedback liefert. Stattdessen werden die Daten an einen fehlgeschlagenen Stapel gesendet, [!DNL Data Lake] um Datenverluste zu vermeiden. Diese fehlerhaften Daten können später abgerufen werden, um eine weitere Analyse zu erhalten und erneut abzuspielen. Diese Methode sollte bei der Herstellung verwendet werden. Sofern nicht anders angegeben, funktioniert die Streaming-Erfassung im asynchronen Validierungsmodus.

**API-Format**

```http
POST /collection/{CONNECTION_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{CONNECTION_ID}` | The `id` value of the streaming connection previously created. |

**Anfrage**

Senden Sie die folgende Anforderung mit asynchroner Validierung an Ihren Dateneinlass, um Daten zu erfassen:

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
>Es ist kein zusätzlicher Parameter für die Abfrage erforderlich, da die asynchrone Überprüfung standardmäßig aktiviert ist.

**Antwort**

Bei aktivierter asynchroner Validierung gibt eine erfolgreiche Antwort Folgendes zurück:

```json
{
    "inletId": "f6ca9706d61de3b78be69e2673ad68ab9fb2cece0c1e1afc071718a0033e6877",
    "xactionId": "1555445493896:8600:8",
    "receivedTimeMs": 1555445493932,
    "synchronousValidation": {
        "skipped": true
    }
}
```

Bitte beachten Sie, dass in der Antwort angegeben wird, dass die synchrone Validierung übersprungen wurde, da sie nicht explizit angefordert wurde.

## Anhang

Dieser Abschnitt enthält Informationen darüber, was die verschiedenen Statuscodes für Antworten zum Erfassen von Daten bedeuten.

### Status-Codes

| Status-Code | Was bedeutet |
| ----------- | ------------- |
| 200 | Erfolg. Bei der synchronen Validierung bedeutet dies, dass die Validierungsprüfungen bestanden haben. Bei der asynchronen Validierung bedeutet dies, dass die Nachricht nur erfolgreich empfangen wurde. Die Benutzer können den Status der Nachricht ermitteln, indem sie den Datensatz beobachten. |
| 400 | Fehler. Es stimmt etwas mit deiner Anfrage nicht. Eine Fehlermeldung mit weiteren Details erhalten Sie von den Streaming Validation Services. |
| 401 | Fehler. Ihre Anfrage ist nicht autorisiert - Sie müssen sie mit einem Inhabertoken anfordern. Weitere Informationen zur Zugangsanfrage finden Sie in diesem [Tutorial](../../tutorials/authentication.md) oder in diesem [Blog-Beitrag](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f). |
| 500 | Fehler. Es liegt ein interner Systemfehler vor. |
| 501 | Fehler. Das bedeutet, dass die synchrone Validierung für diesen Speicherort **nicht** unterstützt wird. |
| 503 | Fehler. Der Dienst ist derzeit nicht verfügbar. Kunden sollten es mindestens dreimal mit einer exponentiellen Back-off-Strategie versuchen. |