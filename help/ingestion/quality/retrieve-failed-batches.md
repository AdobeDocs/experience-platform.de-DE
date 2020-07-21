---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Abrufen fehlgeschlagener Batches
topic: overview
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 75%

---


# Abrufen fehlgeschlagener Batches mithilfe der API

Adobe Experience Platform bietet für den Upload und die Aufnahme von Daten zwei Methoden. You can either use batch ingestion, which allows you to insert their data using various file types (such as CSVs), or streaming ingestion, which allows you to insert their data to [!DNL Platform] using streaming endpoints in real-time.

This tutorial covers steps for retrieving information about a failed batch using [!DNL Data Ingestion] APIs.

## Erste Schritte

Diese Anleitung setzt Grundkenntnisse der folgenden Komponenten von Adobe Experience Platform voraus:

- [!DNL Experience Data Model (XDM) System](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Experience Platform] organisiert werden.
- [!DNL Data Ingestion](../home.md): Die Methoden, mit denen Daten gesendet werden können [!DNL Experience Platform].

### Lesehilfe für Beispiel-API-Aufrufe

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dabei wird auf Pfade ebenso eingegangen wie auf die erforderlichen Kopfzeilen und die für Anfrage-Payloads zu verwendende Formatierung. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Die in der Dokumentation zu Beispielen für API-Aufrufe verwendeten Konventionen werden im Handbuch zur Fehlerbehebung für unter [Lesehilfe für Beispiel-API-Aufrufe](../../landing/troubleshooting.md#how-do-i-format-an-api-request) erläutert.[!DNL Experience Platform]

### Werte der zu verwendenden Kopfzeilen

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to the [!DNL Schema Registry], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

Alle Anfragen, die eine Payload enthalten (also POST-, PUT- und PATCH-Anfragen), erfordern eine zusätzliche Kopfzeile:

- Content-Type: `application/json`

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
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Cache-Control: no-cache" \
  -H "Content-Type: application/json" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}
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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Mit Abschluss dieses Tutorials haben Sie gelernt, wie Fehler aus fehlgeschlagenen Batches abgerufen werden. Weitere Informationen finden Sie zur Aufnahme von Batches finden Sie im [Batch-Aufnahme-Entwicklerhandbuch](../batch-ingestion/overview.md). Weitere Informationen zur Streaming-Aufnahme finden Sie im [Tutorial zur Erstellung einer Streaming-Verbindung](../tutorials/create-streaming-connection.md).

## Anhang

Dieser Abschnitt enthält Informationen zu anderen möglichen Fehlern bei der Aufnahme.

### Fehlerhaft formatiertes XDM

Wie der Zeitstempel-Fehler im Beispiel zuvor sind auch diese Fehler auf ein falsch formatiertes XDM zurückzuführen. Die Fehlermeldungen sind je nach Art des Problems unterschiedlich. Daher kann an dieser Stelle kein Beispiel für einen spezifischen Fehler angegeben werden.

### Fehlende oder ungültige IMS-Org-ID

Dieser Fehler wird angezeigt, wenn die IMS-Org-ID in der Payload fehlt oder ungültig ist.

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{IMS_ORG}@AdobeOrg] Message has an absent or wrong ims org in the header"
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
        "message": "inletId: [{INLET_ID}] imsOrgId: [{IMS_ORG}@AdobeOrg] Message has unknown xdm format"
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
