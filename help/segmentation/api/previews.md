---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Vorschauen
topic: developer guide
translation-type: tm+mt
source-git-commit: 45a196d13b50031d635ceb7c5c952e42c09bd893
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 4%

---


# Entwicklerhandbuch für Vorschauen

intro

- Eine neue Vorschau erstellen
- Abrufen der Ergebnisse einer bestimmten Vorschau
- Abbrechen oder Löschen einer bestimmten Vorschau

## Erste Schritte

Die in diesem Handbuch verwendeten API-Endpunkte sind Teil der Segmentierungs-API. Bevor Sie fortfahren, lesen Sie bitte das Entwicklerhandbuch für die [Segmentierung](./getting-started.md).

Insbesondere enthält der [Abschnitt](./getting-started.md#getting-started) &quot;Erste Schritte&quot;des Segmentierungsentwicklerhandbuchs Links zu verwandten Themen, eine Anleitung zum Lesen der Beispiel-API-Aufrufe im Dokument und wichtige Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen einer Experience Platform-API erforderlich sind.

## Eine neue Vorschau erstellen

Sie können eine neue Vorschau erstellen, indem Sie eine POST-Anforderung an den `/preview` Endpunkt senden.

**API-Format**

```http
POST /preview
```

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/preview \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
  "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
  "predicateType": "pql/text",
  "predicateModel": "_xdm.context.profile",
  "graphType": "pdg"
}
 '
```

body info

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 201 (Erstellt) mit Details zu Ihrer neu erstellten Vorschau zurück.

```json
{
  "state": "NEW",
  "previewQueryId": "e890068b-f5ca-4a8f-a6b5-af87ff0caac3",
  "previewQueryStatus": "NEW",
  "previewId": "MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow",
  "previewExecutionId": 0
}
```

Antwortinformationen, x-location ist nicht vorhanden.

## Abrufen der Ergebnisse einer bestimmten Vorschau

Sie können detaillierte Informationen zu einer bestimmten Vorschau abrufen, indem Sie eine GET-Anforderung an den `/preview` Endpunkt senden und den `id` Wert der Vorschau im Anforderungspfad angeben.

**API-Format**

```http
GET /preview/{PREVIEW_ID}
```

- `{PREVIEW_ID}`: Der `id` Wert der Vorschau, die Sie abrufen möchten.

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit detaillierten Informationen zur angegebenen Vorschau zurück.

```json
{
  "state": "RESULT_READY",
  "page": {
    "offset": 0,
    "size": 0
  },
  "results": [],
  "link": {
    "nextPage": ""
  },
  "previewSampledResultsCount": 0
}
```

## Abbrechen oder Löschen einer bestimmten Vorschau

Sie können eine bestimmte Vorschau löschen, indem Sie eine DELETE-Anforderung an den `/preview` Endpunkt senden und den `id` Wert der Vorschau im Anforderungspfad angeben.

**API-Format**

```http
DELETE /preview/{PREVIEW_ID}
```

- `{PREVIEW_ID}` Der `id` Wert der Vorschau, die Sie löschen möchten.

**Anfrage**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit der folgenden Meldung zurück:

```json
{
  "status": true,
  "message": "KILLED"
}
```

## Nächste Schritte
