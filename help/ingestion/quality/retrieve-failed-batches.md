---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Abrufen fehlgeschlagener Stapel
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 1%

---


# Abrufen fehlgeschlagener Stapel mit der API

Adobe Experience Platform bietet zwei Methoden zum Hochladen und Erfassen von Daten. Sie können entweder die Stapelverarbeitung verwenden, mit der Sie ihre Daten mit verschiedenen Dateitypen (z. B. CSVs) einfügen können, oder Streaming, mit dem Sie ihre Daten mithilfe von Streaming-Endpunkten in Echtzeit in die Platform einfügen können.

In diesem Lernprogramm werden die Schritte zum Abrufen von Informationen zu einem fehlgeschlagenen Stapel mithilfe von Dateneinschluss-APIs beschrieben.

## Erste Schritte

Dieses Handbuch erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

- [Erlebnis-Datenmodell (XDM)-System](../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
- [Dateneinbettung](../home.md): Die Methoden, mit denen Daten an die Experience Platform gesendet werden können.

### Lesen von Beispiel-API-Aufrufen

In diesem Lernprogramm finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt [zum Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung bei Experience Platformen.

### Werte für erforderliche Kopfzeilen sammeln

Um Platformen-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungslehrgang](../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungtutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform API-Aufrufen bereit, wie unten dargestellt:

- Genehmigung: Träger `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle in der Experience Platform befindlichen Ressourcen, einschließlich derjenigen, die zum Schema-Register gehören, werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an Platform-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxen in der Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Für alle Anforderungen mit einer Payload (POST, PUT, PATCH) ist ein zusätzlicher Header erforderlich:

- Content-Type: `application/json`

### Beispiel für fehlgeschlagenen Stapel

In diesem Lernprogramm werden Beispieldaten mit einem falsch formatierten Zeitstempel verwendet, der den Monatswert auf **00** setzt, wie unten dargestellt:

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

## Fehler beim Abrufen des Stapels

**API-Format**

```http
GET /batches/{BATCH_ID}/failed
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{BATCH_ID}` | Die ID des Stapels, den Sie suchen. |

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

Mit der obigen Antwort können Sie sehen, welche Teile des Stapels erfolgreich waren und fehlgeschlagen sind. Aus dieser Antwort können Sie erkennen, dass die Datei den fehlgeschlagenen Stapel `part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json` enthält.

## Herunterladen des fehlgeschlagenen Stapels

Sobald Sie wissen, welche Datei im Stapel fehlschlug, können Sie die Datei mit dem Fehler herunterladen und die Fehlermeldung anzeigen.

**API-Format**

```http
GET /batches/{BATCH_ID}/failed?path={FAILED_FILE}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{BATCH_ID}` | Die ID des Stapels, der die fehlgeschlagene Datei enthält. |
| `{FAILED_FILE}` | Der Name der Datei mit der fehlerhaften Formatierung. |

**Anfrage**

Mit der folgenden Anforderung können Sie die Datei herunterladen, bei der Fehler bei der Erfassung aufgetreten sind.

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

Da der vorherige erfasste Stapel eine ungültige Datums-Zeit hatte, wird der folgende Validierungsfehler angezeigt.

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

Nach dem Lesen dieses Lernprogramms haben Sie gelernt, wie Fehler aus fehlgeschlagenen Stapeln abgerufen werden. Weitere Informationen zur Stapelverarbeitung finden Sie im [Entwicklerhandbuch](../batch-ingestion/overview.md)zur Stapelverarbeitung. Weitere Informationen zur Streaming-Erfassung finden Sie im Tutorial [Erstellen einer Streaming-Verbindung](../tutorials/create-streaming-connection.md).

## Anhang

Dieser Abschnitt enthält Informationen zu anderen Erfassungsfehlertypen, die auftreten können.

### Falsch formatiertes XDM

Wie der Zeitstempelfehler im vorherigen Beispielablauf sind diese Fehler auf falsch formatierte XDM zurückzuführen. Diese Fehlermeldungen variieren je nach Art des Problems. Daher kann kein bestimmtes Fehlerbeispiel angezeigt werden.

### Fehlende oder ungültige IMS-Organisations-ID

Dieser Fehler wird angezeigt, wenn die IMS-Organisations-ID in der Payload fehlt oder ungültig ist.

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

Dieser Fehler wird angezeigt, wenn die `schemaRef` für die `xdmMeta` Variable fehlt.

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

Dieser Fehler wird angezeigt, wenn die `source` in der Kopfzeile enthaltene Fehlermeldung fehlt `name`.

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

Dieser Fehler wird angezeigt, wenn kein `xdmEntity` vorhanden ist.

```json
{
    "_validationErrors": [
        {
            "message": "Payload body is missing xdmEntity"
        }
    ]
}
```
