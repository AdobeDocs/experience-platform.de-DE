---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: PQL-Konvertierungen
topic: developer guide
translation-type: tm+mt
source-git-commit: 45a196d13b50031d635ceb7c5c952e42c09bd893
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 5%

---


# PQL-Konvertierungen

intro

- Formatierung aus pql/text und pql/json konvertieren

## Erste Schritte

Die in diesem Handbuch verwendeten API-Endpunkte sind Teil der Segmentierungs-API. Bevor Sie fortfahren, lesen Sie bitte das Entwicklerhandbuch für die [Segmentierung](./getting-started.md).

Insbesondere enthält der [Abschnitt](./getting-started.md#getting-started) &quot;Erste Schritte&quot;des Segmentierungsentwicklerhandbuchs Links zu verwandten Themen, eine Anleitung zum Lesen der Beispiel-API-Aufrufe im Dokument und wichtige Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen einer Experience Platform-API erforderlich sind.

## Formatierung aus pql/text und pql/json konvertieren

**API-Format**

```http
POST /segment/conversion
```

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/conversion \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
  "name": "People who ordered in the last 30 days",
  "expression": {
    "type": "PQL",
    "format": "pql/text",
    "value": "workAddress.country = \"US\""
  },
  "schema": {
    "name": "_xdm.context.profile"
  },
  "ttlInDays": 60
}
 '
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `name` | Ein eindeutiger Name für die Segmentdefinition. |
| `expression.type` | Der Ausdruck. Es kann entweder sein `PQL` oder `ARL`. |
| `expression.format` | Das Ausdruck-Format. Es kann entweder sein `pql/text` oder `pql/json`. |
| `expression.value` | Die Abfrage-Zeichenfolge des Ausdrucks, den Sie konvertieren möchten. |
| `schema.name` | Die Klassen-ID des Schemas, auf das Sie verweisen. |
| `ttlInDays` | Eine Ganzzahl, welche die Lebensdauer darstellt (TTL). |

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit Details zu Ihrem konvertierten Segment zurück.

```json
{
    "ttlInDays": 60,
    "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "{\"nodeType\":\"fnApply\",\"fnName\":\"=\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"country\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"workAddress\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}}},{\"nodeType\":\"literal\",\"literalType\":\"String\",\"value\":\"US\"}]}"
    }
}
```

## Nächste Schritte
