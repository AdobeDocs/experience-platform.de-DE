---
keywords: Experience Platform;Startseite;beliebte Themen;Streaming;Streaming-Aufnahme;Streaming-Aufnahme-Validierung;Validierung;Streaming-Aufnahme-Validierung;Validierung;Validieren;synchrone Validierung;synchrone Validierung;asynchrone Validierung;
solution: Experience Platform
title: Validierung der Streaming-Aufnahme
type: Tutorial
description: 'Mit der Streaming-Aufnahme können Sie Ihre Daten mithilfe von Streaming-Endpunkten in Echtzeit in Adobe Experience Platform hochladen. Streaming-Aufnahme-APIs unterstützen zwei Validierungsmodi: synchron und asynchron.'
exl-id: 6e9ac943-6d73-44de-a13b-bef6041d3834
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 23%

---

# Validieren der Streaming-Aufnahme

Mit der Streaming-Aufnahme können Sie Ihre Daten mithilfe von Streaming-Endpunkten in Echtzeit in Adobe Experience Platform hochladen. Streaming-Aufnahme-APIs unterstützen zwei Validierungsmodi: synchron und asynchron.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von [!DNL Experience Platform] organisiert werden.
- [[!DNL Streaming Ingestion]](../streaming-ingestion/overview.md): Eine der Methoden zum Senden von Daten an [!DNL Experience Platform].

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Experience Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform], einschließlich der Ressourcen, die zum [!DNL Schema Registry] gehören, sind in bestimmten virtuellen Sandboxes isoliert. Bei allen Anfragen an [!DNL Experience Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in [!DNL Experience Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

- Content-Type: `application/json`

### Validierungsabdeckung

[!DNL Streaming Validation Service] umfasst die Validierung in den folgenden Bereichen:

- Bereich
- Präsenz
- Aufzählung
- Muster
- Typ
- Format

## Synchrone Überprüfung

Die synchrone Validierung ist eine Validierungsmethode, die sofortiges Feedback darüber liefert, warum eine Aufnahme fehlgeschlagen ist. Bei einem Fehler werden die Datensätze, die die Validierung nicht bestehen, jedoch gelöscht und daran gehindert, nachgelagert gesendet zu werden. Daher sollte die synchrone Validierung nur während des Entwicklungsprozesses verwendet werden. Bei der synchronen Validierung werden die Aufrufer sowohl über das Ergebnis der XDM-Validierung als auch, falls sie fehlschlägt, über den Grund für den Fehler informiert.

Standardmäßig ist die synchrone Validierung nicht aktiviert. Um sie zu aktivieren, müssen Sie bei API-Aufrufen den optionalen Abfrageparameter `syncValidation=true` übergeben. Darüber hinaus ist die synchrone Validierung derzeit nur verfügbar, wenn sich Ihr Stream-Endpunkt im VA7-Rechenzentrum befindet.

>[!NOTE]
>
>Der `syncValidation` Abfrageparameter ist nur für den einzelnen Nachrichtenendpunkt verfügbar und kann nicht für den Batch-Endpunkt verwendet werden.

Wenn eine Nachricht bei der synchronen Validierung fehlschlägt, wird die Nachricht nicht in die Ausgabeschlange geschrieben, was Benutzern sofortiges Feedback liefert.

>[!NOTE]
>
>Schemaänderungen sind möglicherweise nicht sofort verfügbar, da Änderungen zwischengespeichert werden. Warten Sie bis zu 15 Minuten, bis der Cache aktualisiert ist.

**API-Format**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{CONNECTION_ID}` | Der `id` der zuvor erstellten Streaming-Verbindung. |

**Anfrage**

Senden Sie die folgende Anfrage, um Daten mit synchroner Validierung in Ihr Dateneingangsmodul aufzunehmen:

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?syncValidation=true \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | Der JSON-Hauptteil einer Daten, die Sie aufnehmen möchten. |

**Antwort**

Bei aktivierter synchroner Validierung enthält eine erfolgreiche Antwort alle aufgetretenen Validierungsfehler in der Payload:

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

Die obige Antwort listet auf, wie viele Schemaverletzungen gefunden wurden und welche Verstöße begangen wurden. In dieser Antwort wird beispielsweise angegeben, dass die Schlüssel `workEmail` und `person` nicht im Schema definiert wurden und daher nicht zulässig sind. Außerdem wird der Wert für `_id` als falsch gekennzeichnet, da das Schema eine `string` erwartet, stattdessen jedoch eine `long` eingefügt wurde. Beachten Sie, dass der Validierungs-Service die Verarbeitung dieser Nachricht **, wenn fünf Fehler** sind. Andere Nachrichten werden jedoch weiterhin geparst.

## Asynchrone Validierung

Asynchrone Validierung ist eine Validierungsmethode, die kein sofortiges Feedback liefert. Stattdessen werden die Daten an einen fehlgeschlagenen Batch gesendet, [!DNL Data Lake] Datenverlust zu vermeiden. Diese fehlgeschlagenen Daten können später zur weiteren Analyse und Wiederholung abgerufen werden. Diese Methode sollte in der Produktion verwendet werden. Sofern nicht anders angefordert, erfolgt die Streaming-Aufnahme im asynchronen Validierungsmodus.

**API-Format**

```http
POST /collection/{CONNECTION_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{CONNECTION_ID}` | Der `id` der zuvor erstellten Streaming-Verbindung. |

**Anfrage**

Senden Sie die folgende Anfrage, um Daten mit asynchroner Validierung in Ihr Dateneingangsmodul aufzunehmen:

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID} \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | Der JSON-Hauptteil einer Daten, die Sie aufnehmen möchten. |

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

Dieser Abschnitt enthält Informationen darüber, was die verschiedenen Status-Codes für Antworten bei der Datenaufnahme bedeuten.

### Status-Codes

| Status-Code | Was es bedeutet |
| ----------- | ------------- |
| 200 | Erfolgreich. Für die synchrone Validierung bedeutet dies, dass die Validierungsprüfungen bestanden wurden. Für die asynchrone Validierung bedeutet dies, dass nur die Nachricht erfolgreich empfangen wurde. Benutzer können den möglichen Nachrichtenstatus ermitteln, indem sie den Datensatz beobachten. |
| 400 | Fehler. Mit Ihrer Anfrage stimmt etwas nicht. Von den Streaming-Validierungs-Services wird eine Fehlermeldung mit weiteren Details empfangen. |
| 401 | Fehler. Ihre Anfrage ist nicht autorisiert - Sie müssen sie mit einem Bearer-Token anfordern. Weitere Informationen zum Anfordern des Zugriffs finden Sie in diesem [Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) oder in [Blogpost](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f). |
| 500 | Fehler. Es liegt ein interner Systemfehler vor. |
| 501 | Fehler. Das bedeutet, dass die synchrone Validierung für **Speicherort** unterstützt wird. |
| 503 | Fehler. Der Dienst ist derzeit nicht verfügbar. Clients sollten mindestens dreimal einen erneuten Versuch starten, indem sie eine exponentielle Back-off-Strategie verwenden. |
