---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Schätzungen
topic: developer guide
translation-type: tm+mt
source-git-commit: 16ebff522c5b08e4c100f5d2f972ef4db64656a7
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 3%

---


# Schätzungen

intro

- Abrufen der Ergebnisse eines bestimmten Schätzauftrags

## Erste Schritte

Die in diesem Handbuch verwendeten API-Endpunkte sind Teil der Segmentierungs-API. Bevor Sie fortfahren, lesen Sie bitte das Entwicklerhandbuch für die [Segmentierung](./getting-started.md).

Insbesondere enthält der [Abschnitt](./getting-started.md#getting-started) &quot;Erste Schritte&quot;des Segmentierungsentwicklerhandbuchs Links zu verwandten Themen, eine Anleitung zum Lesen der Beispiel-API-Aufrufe im Dokument und wichtige Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen einer Experience Platform-API erforderlich sind.

## Abrufen der Ergebnisse eines bestimmten Schätzauftrags

Sie können Details zu einem bestimmten Schätzauftrag abrufen, indem Sie eine GET-Anforderung an den `/estimate` Endpunkt senden und den `id` Wert des Schätzauftrags im Anforderungspfad angeben.

**API-Format**

```http
GET /estimate/{PREVIEW_ID}
```

- `{PREVIEW_ID}`: Der `id` Wert des Schätzauftrags, den Sie abrufen möchten.

**Anfrage**

Die folgende Anforderung ruft die Ergebnisse eines bestimmten Schätzauftrags ab.

//Vorschauen-ID abrufen

```shell
curl -X GET https://platform.adobe.io/data/core/ups/estimate/{PREVIEW_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit Details zum Schätzauftrag zurück.

```json
{
  "estimatedSize": 0,
  "numRowsToRead": 1,
  "state": "RESULT_READY",
  "profilesReadSoFar": 1,
  "standardError": 0,
  "error": {
    "description": "",
    "traceback": ""
  },
  "profilesMatchedSoFar": 0,
  "totalRows": 1,
  "confidenceInterval": "95%",
  "_links": {
    "preview": "https://platform.adobe.io/data/core/ups/preview/app-32be0328-3f31-4b64-8d84-acd0c4fbdad3/execution/0?previewQueryId=e890068b-f5ca-4a8f-a6b5-af87ff0caac3"
  }
}
```

## Nächste Schritte

Jetzt, wo Sie wissen, wie Sie die geschätzten Auftragsergebnisse abrufen können, können Sie