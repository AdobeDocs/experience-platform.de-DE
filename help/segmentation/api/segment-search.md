---
keywords: Experience Platform;Segmentierung;Segmentierungsdienst;Fehlerbehebung;API;SEG;Segment;Segment;Suche;Segmentsuche
title: API-Endpunkt für Segmentsuche
topic-legacy: guide
description: In der Adobe Experience Platform Segmentation Service API wird die Segmentsuche verwendet, um in verschiedenen Datenquellen enthaltene Felder zu suchen und sie in Echtzeit zurückzugeben. Dieses Handbuch enthält Informationen zum besseren Verständnis der Segmentsuche und enthält Beispiel-API-Aufrufe zum Ausführen grundlegender Aktionen mit der API.
exl-id: bcafbed7-e4ae-49c0-a8ba-7845d8ad663b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1201'
ht-degree: 4%

---

# Endpunkt Segmentsuche

Die Segmentsuche dient zum Durchsuchen von Feldern, die in verschiedenen Datenquellen enthalten sind, und zum Zurückgeben in Echtzeit.

Dieses Handbuch enthält Informationen zum besseren Verständnis der Segmentsuche und enthält Beispiel-API-Aufrufe zum Ausführen grundlegender Aktionen mit der API.

## Erste Schritte

Die in diesem Handbuch verwendeten Endpunkte sind Teil der API [!DNL Adobe Experience Platform Segmentation Service]. Bevor Sie fortfahren, lesen Sie bitte im Handbuch [Erste Schritte](./getting-started.md) nach wichtigen Informationen, die Sie kennen müssen, um die API erfolgreich aufzurufen, einschließlich erforderlicher Kopfzeilen und Anleitungen zum Lesen von Beispiel-API-Aufrufen.

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
| `schema.name={SCHEMA}` | **(Erforderlich)** Dabei stellt {SCHEMA} den mit den Suchobjekten verknüpften Schema-Klassenwert dar. Derzeit wird nur `_xdm.context.segmentdefinition` unterstützt. |
| `s={SEARCH_TERM}` | *(Optional)* Dabei stellt {SEARCH_TERM} eine Abfrage dar, die der Implementierung der  [Lucene-Suchsyntax](https://docs.microsoft.com/de-DE/azure/search/query-lucene-syntax) durch Microsoft entspricht. Wenn kein Suchbegriff angegeben ist, werden alle mit `schema.name` verknüpften Datensätze zurückgegeben. Eine ausführlichere Erläuterung finden Sie im [Anhang](#appendix) dieses Dokuments. |

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
| `s={SEARCH_TERM}` | *(Optional)* Dabei enthält {SEARCH_TERM} eine Abfrage, die der Implementierung der  [Lucene-Suchsyntax](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax) durch Microsoft entspricht. Wenn kein Suchbegriff angegeben ist, werden alle mit `schema.name` verknüpften Datensätze zurückgegeben. Eine ausführlichere Erläuterung finden Sie im [Anhang](#appendix) dieses Dokuments. |
| `entityId={ENTITY_ID}` | *(Optional)* Beschränkt Ihre Suche auf den mit {ENTITY_ID} angegebenen Ordner. |
| `limit={LIMIT}` | *(Optional)* Dabei stellt {LIMIT} die Anzahl der zurückzugebenden Suchergebnisse dar. Der Standardwert lautet 50. |
| `page={PAGE}` | *(Optional)* Dabei stellt {PAGE} die Seitenzahl dar, die für die Paginierung der Ergebnisse der gesuchten Abfrage verwendet wird. Beachten Sie, dass die Seitenzahl unter **0** Beginn wird. |


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

Die folgenden Abschnitte enthalten zusätzliche Informationen zur Funktionsweise von Suchbegriffen. Suchbegriffe werden wie folgt geschrieben: `s={FieldName}:{SearchExpression}`. Um beispielsweise nach einem Segment mit dem Namen AAM oder [!DNL Platform] zu suchen, würden Sie die folgende Abfrage verwenden: `s=segmentName:AAM%20OR%20Platform`.

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
| foo AND bar | Eine boolesche Suche. Dies gibt Ergebnisse zurück, wenn **beide** die Wörter &quot;foo&quot;und &quot;bar&quot;in einem der durchsuchbaren Felder gefunden werden. |
| foo OR-Leiste | Eine boolesche Suche. Dies gibt Ergebnisse zurück, wenn **entweder** das Wort &quot;foo&quot;oder das Wort &quot;bar&quot;in einem der durchsuchbaren Felder gefunden werden. |
| foo NOT-Leiste | Eine boolesche Suche. Dadurch werden Ergebnisse zurückgegeben, wenn das Wort &quot;foo&quot;gefunden wird, das Wort &quot;bar&quot;jedoch in keinem der durchsuchbaren Felder gefunden wird. |
| name: foo AND bar | Eine boolesche Suche. Dies gibt Ergebnisse zurück, wenn **beide** die Wörter &quot;foo&quot;und &quot;bar&quot;im Feld &quot;name&quot;gefunden werden. |
| run* | Eine Platzhaltersuche. Die Verwendung eines Sternchen (*) entspricht 0 oder mehr Zeichen. Das bedeutet, dass Ergebnisse zurückgegeben werden, wenn der Inhalt eines durchsuchbaren Feldes ein Wort enthält, das Beginn mit &quot;run&quot;haben. Dies gibt beispielsweise Ergebnisse zurück, wenn die Wörter &quot;läuft&quot;, &quot;running&quot;, &quot;runner&quot;oder &quot;runt&quot;angezeigt werden. |
| Cam? | Eine Platzhaltersuche. Verwenden eines Fragezeichens (?) entspricht nur genau einem Zeichen. Das bedeutet, dass Ergebnisse zurückgegeben werden, wenn der Inhalt eines durchsuchbaren Felds mit &quot;cam&quot;und einem zusätzlichen Brief Beginn wird. Dies gibt beispielsweise Ergebnisse zurück, wenn die Wörter &quot;Camp&quot;oder &quot;Cams&quot;angezeigt werden, gibt jedoch keine Ergebnisse zurück, wenn die Wörter &quot;Camera&quot;oder &quot;Campfire&quot;angezeigt werden. |
| &quot;blauer Schirm&quot; | Eine Wortsuche. Dadurch werden Ergebnisse zurückgegeben, wenn der Inhalt eines durchsuchbaren Feldes den vollständigen Satz &quot;blauer Schirm&quot;enthält. |
| blue\~ | Eine unscharfe Suche. Optional können Sie eine Zahl zwischen 0 und 2 nach der Tilde (~) setzen, um den Bearbeitungsabstand anzugeben. &quot;blue\~1&quot;wäre beispielsweise &quot;blue&quot;, &quot;blues&quot;oder &quot;glue&quot;. Die unscharfe Suche kann nur auf Begriffe angewendet werden, nicht auf Wortgruppen. **** Sie können jedoch an das Ende jedes Wortes in einer Wortgruppe Tildes anhängen. So würde z.B. &quot;camping\~ in\~ the\~ Summer\~&quot; mit &quot;camping im Sommer&quot; übereinstimmen. |
| &quot;hotel flughafen&quot;\~5 | Eine Suche nach der Nähe. Diese Art der Suche wird verwendet, um Begriffe zu finden, die in einem Dokument nahe beieinander liegen. Beispielsweise werden mit der Wortgruppe `"hotel airport"~5` die Begriffe &quot;hotel&quot;und &quot;flughafen&quot;innerhalb von 5 Wörtern in einem Dokument gefunden. |
| `/a[0-9]+b$/` | Eine regelmäßige Suche nach Ausdrücken. Dieser Suchtyp findet eine Übereinstimmung basierend auf dem Inhalt zwischen Schrägstrichen &quot;/&quot;, wie in der RegExp-Klasse dokumentiert. Wenn Sie z. B. Dokumente mit &quot;motel&quot;oder &quot;hotel&quot;suchen möchten, geben Sie `/[mh]otel/` an. Regelmäßige Suchvorgänge mit Ausdrücken werden mit einzelnen Wörtern abgeglichen. |

Weitere Informationen zur Syntax der Abfrage finden Sie in der [Lucene-Abfrage-Syntaxdokumentation](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax).
