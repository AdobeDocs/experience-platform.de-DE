---
keywords: Experience Platform;segmentation;segmentation service;troubleshooting;API;seg;
solution: Adobe Experience Platform
title: Endpunktleitfaden für die Segmentsuche
topic: guide
translation-type: tm+mt
source-git-commit: 41a5d816f9dc6e7c26141ff5e9173b1b5631d75e
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 5%

---


# Endpunktleitfaden zur Segmentsuche

Die Segmentsuche dient zum Durchsuchen von Feldern, die in verschiedenen Datenquellen enthalten sind, und zum Zurückgeben in Echtzeit.

Dieses Handbuch enthält Informationen zum besseren Verständnis der Segmentsuche und enthält Beispiel-API-Aufrufe zum Ausführen grundlegender Aktionen mit der API.

## Erste Schritte

The endpoints used in this guide are part of the [!DNL Adobe Experience Platform Segmentation Service] API. Before continuing, please review the [getting started guide](./getting-started.md) for important information that you need to know in order to successfully make calls to the API, including required headers and how to read example API calls.

Zusätzlich zu den erforderlichen Kopfzeilen, die im Abschnitt &quot;Erste Schritte&quot;beschrieben werden, benötigen alle Anforderungen an den Endpunkt &quot;Segmentsuche&quot;die folgende zusätzliche Kopfzeile:

- x-ups-search-version: &quot;1.0&quot;

### Mehrere Namensraum durchsuchen

Dieser Suchendpunkt kann verwendet werden, um über verschiedene Namensraum hinweg zu suchen und eine Liste der Suchzählergebnisse zurückzugeben. Es können mehrere Parameter verwendet werden, die durch das kaufmännische Und (&amp;) getrennt werden.

**API-Format**

```http
GET /search/namespaces?schema.name={SCHEMA}
GET /search/namespaces?schema.name={SCHEMA}&s={SEARCH_TERM}
```

| Parameter | Beschreibung |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Erforderlich)** Dabei stellt {SCHEMA} den Schema-Klassenwert dar, der den Suchobjekten zugeordnet ist. Derzeit wird nur `_xdm.context.segmentdefinition` unterstützt. |
| `s={SEARCH_TERM}` | *(Optional)* Wobei {SEARCH_TERM} eine Abfrage darstellt, die der Implementierung der [Lucene-Suchsyntax](https://docs.microsoft.com/de-DE/azure/search/query-lucene-syntax)durch Microsoft entspricht. Wenn kein Suchbegriff angegeben ist, werden alle damit verbundenen Datensätze zurückgegeben `schema.name` . Eine ausführlichere Erläuterung finden Sie im [Anhang](#appendix) dieses Dokuments. |

**Anfrage**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/namespaces?schema.name=_xdm.context.segmentdefinition \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit folgenden Informationen zurück.

```json
{
  "namespaces": [
    {
      "namespace": "AAMTraits",
      "displayName": "AAMTraits",
      "count": 45
    },
    {
      "namespace": "AAMSegments",
      "displayName": "AAMSegment",
      "count": 10
    },
    {
      "namespace": "SegmentsAISegments",
      "displayName": "SegmentSAISegment",
      "count": 3
    }
  ],
  "totalCount": 3,
  "status": {
    "message": "Success"
  }
}
```

### Einzelne Entitäten suchen

Mit diesem Suchendpunkt kann eine Liste aller im Volltext indexierten Objekte innerhalb des angegebenen Namensraums abgerufen werden. Es können mehrere Parameter verwendet werden, die durch das kaufmännische Und (&amp;) getrennt werden.

**API-Format**

```http
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&s={SEARCH_TERM}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| Parameter | Beschreibung |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Erforderlich)** Dabei enthält {SCHEMA} den mit den Suchobjekten verknüpften Schema-Klassenwert. Derzeit wird nur `_xdm.context.segmentdefinition` unterstützt. |
| `namespace={NAMESPACE}` | **(Erforderlich)** Dabei enthält {NAMENSRAUM} den Namensraum, in dem Sie suchen möchten. |
| `s={SEARCH_TERM}` | *(Optional)* Wobei {SEARCH_TERM} eine Abfrage enthält, die der Implementierung der [Lucene-Suchsyntax](https://docs.microsoft.com/de-DE/azure/search/query-lucene-syntax)durch Microsoft entspricht. Wenn kein Suchbegriff angegeben ist, werden alle damit verbundenen Datensätze zurückgegeben `schema.name` . Eine ausführlichere Erläuterung finden Sie im [Anhang](#appendix) dieses Dokuments. |
| `entityId={ENTITY_ID}` | *(Optional)* Schränkt Ihre Suche auf den mit {ENTITY_ID} angegebenen Ordner ein. |
| `limit={LIMIT}` | *(Optional)* Dabei stellt {LIMIT} die Anzahl der zurückzugebenden Suchergebnisse dar. Der Standardwert lautet 50. |
| `page={PAGE}` | *(Optional)* Dabei steht {PAGE} für die Seitenzahl, die zur Paginierung der Ergebnisse der gesuchten Abfrage verwendet wird. Bitte beachten Sie, dass die Seitenzahl um **0** Beginn ist. |


**Anfrage**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/entities?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 zurück, wobei die Ergebnisse mit der Abfrage der Suche übereinstimmen.

```json
{
  "entities": [
    {
       "id": "1012667",
       "base64EncodedSourceId": "RFVGamdydHpEdy01ZTE1ZGJlZGE4YjAxMzE4YWExZWY1MzM1",
       "sourceId": "DUFjgrtzDw-5e15dbeda8b01318aa1ef533",
       "isFolder": true,
       "parentFolderId": "974139",
       "name": "aam-47995 verification (100)"
    },
    {
       "id": "14653311",
       "base64EncodedSourceId": "REVGamduLVgzdy01ZTE2ZjRhNjc1ZDZhMDE4YThhZDM3NmY1",
       "sourceId": "DEFjgn-X3w-5e16f4a675d6a018a8ad376f",
       "isFolder": false,
       "parentFolderId": "324050",
       "name": "AAM - Heavy equipment",
       "description": "AAM - Acme Equipment"
    }
 
 ],
  "page": {
    "totalCount": 2,
    "totalPages": 1,
    "pageOffset": 0,
    "pageSize": 10
  },
  "status": {
    "message": "Success"
  }
}
```

### Abrufen von Strukturinformationen zu einem Suchobjekt

Mit diesem Suchendpunkt können Sie die Strukturinformationen zum angeforderten Suchobjekt abrufen.

**API-Format**

```http
GET /search/taxonomy?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| Parameter | Beschreibung |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Erforderlich)** Dabei enthält {SCHEMA} den mit den Suchobjekten verknüpften Schema-Klassenwert. Derzeit wird nur `_xdm.context.segmentdefinition` unterstützt. |
| `namespace={NAMESPACE}` | **(Erforderlich)** Dabei enthält {NAMENSRAUM} den Namensraum, in dem Sie suchen möchten. |
| `entityId={ENTITY_ID}` | **(Erforderlich)** Die ID des Suchobjekts, über das Sie die Strukturinformationen abrufen möchten, angegeben mit {ENTITY_ID}. |

**Anfrage**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/taxonomy?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments&entityId=porsche11037 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit detaillierten Strukturinformationen zum angeforderten Suchobjekt zurück.

```json
{
    "taxonomy": [
        {
            "id": "0",
            "base64EncodedSourceId": "RFVGZ01BLTVlNjgzMGZjMzk3YjQ1MThhYWExYTA4Zg2",
            "name": "AAMTraits for Cars",
            "parentFolderId": "root"
        },
        {
            "id": "150561",
            "base64EncodedSourceId": "RFVGamdpRk1BZy01ZTY4MzBmYzM5N2I0NTE4YWFhMWEwOGY1",
            "name": "Fast Cars",
            "parentFolderId": "carTraits"
        },
        {
            "id": "porsche11037",
            "base64EncodedSourceId": "REFGZ01CLTVlNjczMGZjMzk3YjQ1MThhZGIxYTA4Zg==",
            "name": "Porsche",
            "parentFolderId": "redCarsFolderId"
        }
    ],
    "status": {
        "message": "Success"
    }
}
```

## Nächste Schritte

Nach dem Lesen dieses Handbuchs haben Sie nun ein besseres Verständnis dafür, wie die Segmentsuche funktioniert.

## Anhang {#appendix}

Die folgenden Abschnitte enthalten zusätzliche Informationen zur Funktionsweise von Suchbegriffen. Suchbegriffe werden wie folgt geschrieben: `s={FieldName}:{SearchExpression}`. Um beispielsweise nach einem Segment namens AAM oder Platform zu suchen, würden Sie die folgende Abfrage verwenden: `s=segmentName:AAM%20OR%20Platform`.

> !![NOTE] Für Best Practices sollte der Ausdruck für die Suche wie oben gezeigt HTML-kodiert sein.

### Suchfelder {#search-fields}

In der folgenden Tabelle werden die Felder Liste, die im Suchparameter &quot;Abfrage&quot;durchsucht werden können.

| Feldname | Beschreibung |
| ---------- | ----------- |
| folderId | Der oder die Ordner, die die Ordner-ID der angegebenen Suche enthalten. |
| folderLocation | Der Speicherort bzw. die Orte, an denen sich der Ordnerspeicherort der angegebenen Suche befindet/befinden. |
| parentFolderId | Das Segment oder der Ordner, das bzw. der die übergeordnete Ordner-ID der angegebenen Suche enthält. |
| segmentId | Das Segment stimmt mit der Segment-ID Ihrer angegebenen Suche überein. |
| segmentName | Das Segment stimmt mit dem Segmentnamen Ihrer angegebenen Suche überein. |
| segmentDescription | Das Segment stimmt mit der Segmentbeschreibung Ihrer angegebenen Suche überein. |

### Ausdruck suchen {#search-expression}

In der folgenden Tabelle werden die Einzelheiten der Funktionsweise von Abfragen bei der Segmentsuche-API Liste.

>!![NOTE] Die folgenden Beispiele werden in einem nicht-HTML-kodierten Format angezeigt, um mehr Klarheit zu schaffen. Für Best Practices kodieren Sie Ihren Ausdruck mit HTML.

| Beispiel für einen Ausdruck | Beschreibung |
| ------------------------- | ----------- |
| foo | Suchen Sie nach einem beliebigen Wort. Dadurch werden Ergebnisse zurückgegeben, wenn das Wort &quot;foo&quot;in einem der durchsuchbaren Felder gefunden wird. |
| foo AND bar | Eine boolesche Suche. Dadurch werden Ergebnisse zurückgegeben, wenn **beide** Wörter &quot;foo&quot;und &quot;bar&quot;in einem der durchsuchbaren Felder gefunden werden. |
| foo OR-Leiste | Eine boolesche Suche. Dadurch werden Ergebnisse zurückgegeben, wenn **entweder** das Wort &quot;foo&quot;oder das Wort &quot;bar&quot;in einem der durchsuchbaren Felder gefunden werden. |
| foo NOT-Leiste | Eine boolesche Suche. Dadurch werden Ergebnisse zurückgegeben, wenn das Wort &quot;foo&quot;gefunden wird, das Wort &quot;bar&quot;jedoch in keinem der durchsuchbaren Felder gefunden wird. |
| name: foo AND bar | Eine boolesche Suche. Dies gibt Ergebnisse zurück, wenn **beide** Wörter &quot;foo&quot;und &quot;bar&quot;im Feld &quot;name&quot;gefunden werden. |
| run* | Eine Platzhaltersuche. Die Verwendung eines Sternchen (*) entspricht 0 oder mehr Zeichen. Das bedeutet, dass Ergebnisse zurückgegeben werden, wenn der Inhalt eines durchsuchbaren Feldes ein Wort enthält, das Beginn mit &quot;run&quot;haben. Dies gibt beispielsweise Ergebnisse zurück, wenn die Wörter &quot;läuft&quot;, &quot;running&quot;, &quot;runner&quot;oder &quot;runt&quot;angezeigt werden. |
| Cam? | Eine Platzhaltersuche. Verwenden eines Fragezeichens (?) entspricht nur genau einem Zeichen. Das bedeutet, dass Ergebnisse zurückgegeben werden, wenn der Inhalt eines durchsuchbaren Felds mit &quot;cam&quot;und einem zusätzlichen Brief Beginn wird. Dies gibt beispielsweise Ergebnisse zurück, wenn die Wörter &quot;Camp&quot;oder &quot;Cams&quot;angezeigt werden, gibt jedoch keine Ergebnisse zurück, wenn die Wörter &quot;Camera&quot;oder &quot;Campfire&quot;angezeigt werden. |
| &quot;blauer Schirm&quot; | Eine Wortsuche. Dadurch werden Ergebnisse zurückgegeben, wenn der Inhalt eines durchsuchbaren Feldes den vollständigen Satz &quot;blauer Schirm&quot;enthält. |
| blue\~ | Eine unscharfe Suche. Optional können Sie eine Zahl zwischen 0 und 2 nach der Tilde (~) setzen, um den Bearbeitungsabstand anzugeben. &quot;blue\~1&quot;wäre beispielsweise &quot;blue&quot;, &quot;blues&quot;oder &quot;glue&quot;. Die unscharfe Suche kann **nur** auf Begriffe angewendet werden, nicht auf Ausdrücke. Sie können jedoch an das Ende jedes Wortes in einer Wortgruppe Tildes anhängen. So würde z.B. &quot;camping\~ in\~ the\~ Summer\~&quot; mit &quot;camping im Sommer&quot; übereinstimmen. |
| &quot;hotel flughafen&quot;\~5 | Eine Suche nach der Nähe. Diese Art der Suche wird verwendet, um Begriffe zu finden, die in einem Dokument nahe beieinander liegen. So `"hotel airport"~5` werden beispielsweise die Begriffe &quot;hotel&quot;und &quot;flughafen&quot;in einem Dokument innerhalb von 5 Wörtern voneinander getrennt. |
| `/a[0-9]+b$/` | Eine regelmäßige Suche nach Ausdrücken. Dieser Suchtyp findet eine Übereinstimmung basierend auf dem Inhalt zwischen Schrägstrichen &quot;/&quot;, wie in der RegExp-Klasse dokumentiert. Wenn Sie z. B. Dokumente mit &quot;motel&quot;oder &quot;hotel&quot;suchen möchten, geben Sie `/[mh]otel/`an. Regelmäßige Suchvorgänge mit Ausdrücken werden mit einzelnen Wörtern abgeglichen. |

Weitere Informationen zur Syntax der Abfrage finden Sie in der [Lucene-Abfrage-Syntaxdokumentation](https://docs.microsoft.com/de-DE/azure/search/query-lucene-syntax).
