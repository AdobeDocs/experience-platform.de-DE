---
keywords: Experience Platform; Startseite; beliebte Themen; Abrufen fehlgeschlagener Batches; fehlgeschlagene Batches; Batch-Erfassung; Batch-Erfassung; fehlgeschlagene Batches; Abrufen fehlgeschlagener Batches; Abrufen fehlgeschlagener Batches; Herunterladen fehlgeschlagener Batches; Herunterladen fehlgeschlagener Batches;
solution: Experience Platform
title: Abrufen fehlgeschlagener Batches mit der Data Access API
type: Tutorial
description: In diesem Tutorial wird erläutert, wie Sie mithilfe von APIs für die Datenaufnahme Informationen aus einem fehlgeschlagenen Batch abrufen.
exl-id: 5fb9f28d-091e-4124-8d8e-b8a675938d3a
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 80%

---

# Abrufen fehlgeschlagener Batches mit der Data Access API

Adobe Experience Platform bietet für den Upload und die Aufnahme von Daten zwei Methoden. Sie können entweder die Batch-Erfassung verwenden, um ihre Daten mit verschiedenen Dateitypen (z. B. CSV-Dateien) einzufügen, oder die Streaming-Erfassung, mit der Sie ihre Daten in [!DNL Platform] Verwendung von Streaming-Endpunkten in Echtzeit.

In diesem Tutorial werden die Schritte zum Abrufen von Informationen zu einem fehlgeschlagenen Batch mithilfe von [!DNL Data Ingestion] APIs.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von [!DNL Experience Platform] organisiert werden.
- [[!DNL Data Ingestion]](../home.md): Die Methoden, mit denen Daten an [!DNL Experience Platform] gesendet werden können.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform], einschließlich derjenigen, die [!DNL Schema Registry], werden auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an [!DNL Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

- `Content-Type: application/json`

### Beispiel für fehlgeschlagenen Batch

In diesem Tutorial werden Beispieldaten mit einem fehlerhaft formatierten Zeitstempel verwendet, der für den Monat den Wert **00** festlegt, wie unten dargestellt:

```json
{
    "body": {
        "xdmEntity": {
            "id": "c8d11988-6b56-4571-a123-b6ce74236036",
            "timestamp": "2018-00-10T22:07:56Z",
            "environment": {
                "browserDetails": {
                    "userAgent": "Mozilla\/5.0 (Windows NT 5.1) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/29.0.1547.57 Safari\/537.36 OPR\/16.0.1196.62",
                    "acceptLanguage": "en-US",
                    "cookiesEnabled": true,
                    "javaScriptVersion": "1.6",
                    "javaEnabled": true
                },
                "colorDepth": 32,
                "viewportHeight": 799,
                "viewportWidth": 414
            }
        }
    }
}
```

Die obige Payload wird aufgrund des fehlerhaften Zeitstempels nicht ordnungsgemäß mit dem XDM-Schema validiert.

## Abrufen des fehlgeschlagenen Batches

**API-Format**

```http
GET /batches/{BATCH_ID}/failed
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{BATCH_ID}` | Die ID des Batches, den Sie nachschlagen. |

**Anfrage**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

```json
{
    "data": [
        {
            "name": "_SUCCESS",
            "length": "0",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/{BATCH_ID}/failed?path=_SUCCESS"
                }
            }
        },
        {
            "name": "part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json",
            "length": "1800",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/{BATCH_ID}/failed?path=part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 2
    }
}
```

Aus der Antwort oben ist ersichtlich, bei welchen Blöcken aus dem Batch die Aufnahme erfolgreich war und bei welchen sie fehlschlug. Diese Antwort hier zeigt, dass die Datei `part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json` den fehlgeschlagenen Batch enthält.

## Herunterladen des fehlgeschlagenen Batches

Sobald Sie wissen, welche Datei aus dem Batch fehlschlug, können Sie die entsprechende Datei herunterladen und sich die Fehlermeldung anzeigen lassen.

**API-Format**

```http
GET /batches/{BATCH_ID}/failed?path={FAILED_FILE}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{BATCH_ID}` | Die ID des Batches, der die fehlgeschlagene Datei enthält. |
| `{FAILED_FILE}` | Der Name der Datei mit der fehlerhaften Formatierung. |

**Anfrage**

Mit der nachfolgenden Anfrage können Sie die Datei herunterladen, bei der Fehler bei der Aufnahme aufgetreten sind.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path={FAILED_FILE}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Da der zuvor aufgenommene Batch einen ungültigen Wert für Datum/Zeit aufwies, wird der folgende Validierungsfehler angezeigt.

```json
{
    "_validationErrors": [
        {
            "causingExceptions": [],
            "keyword": "format",
            "message": "[2018-00-23T22:07:01Z] is not a valid date-time. Expected [yyyy-MM-dd'T'HH:mm:ssZ, yyyy-MM-dd'T'HH:mm:ss.[0-9]{1-9}Z, yyyy-MM-dd'T'HH:mm:ss[+-]HH:mm, yyyy-MM-dd'T'HH:mm:ss.[0-9]{1,9}[+-]HH:mm]",
            "pointerToViolation": "#/timestamp",
            "schemaLocation": "#/properties/timestamp"
        }
    ]
}
```

## Nächste Schritte

Mit Abschluss dieses Tutorials haben Sie gelernt, wie Fehler aus fehlgeschlagenen Batches abgerufen werden. Weitere Informationen finden Sie zur Aufnahme von Batches finden Sie im [Entwicklerhandbuch zur Batch-Erfassung](../batch-ingestion/overview.md). Weitere Informationen zur Streaming-Erfassung finden Sie im [Tutorial zur Erstellung einer Streaming-Verbindung](../tutorials/create-streaming-connection.md).

## Anhang

Dieser Abschnitt enthält Informationen zu anderen möglichen Fehlern bei der Aufnahme.

### Fehlerhaft formatiertes XDM

Wie der Zeitstempel-Fehler im Beispiel zuvor sind auch diese Fehler auf ein falsch formatiertes XDM zurückzuführen. Die Fehlermeldungen sind je nach Art des Problems unterschiedlich. Daher kann an dieser Stelle kein Beispiel für einen spezifischen Fehler angegeben werden.

### Fehlende oder ungültige Organisations-ID

Dieser Fehler wird angezeigt, wenn die Organisations-ID in der Payload fehlt oder ungültig ist.

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{ORG_ID}@AdobeOrg] Message has an absent or wrong ims org in the header"
    }
}
```

### Fehlendes XDM-Schema

Dieser Fehler wird angezeigt, wenn `schemaRef` für `xdmMeta` fehlt.

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{ORG_ID}@AdobeOrg] Message has unknown xdm format"
    }
}
```

### Fehlender Quellname

Dieser Fehler wird angezeigt, wenn für die `source` in der Kopfzeile der `name` fehlt.

```json
{
    "_errors":{
        "_streamingValidation": [
            {
                "message": "Payload header is missing Source Name"
            }
        ]
    }
}
```

### Fehlende XDM-Entität

Dieser Fehler wird angezeigt, wenn `xdmEntity` nicht vorhanden ist.

```json
{
    "_validationErrors": [
        {
            "message": "Payload body is missing xdmEntity"
        }
    ]
}
```
