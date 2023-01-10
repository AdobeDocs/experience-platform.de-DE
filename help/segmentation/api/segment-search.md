---
keywords: Experience Platform;Segmentierung;Segmentierungsdienst;Fehlerbehebung;API;Suche;Segment;Segment;Suche;Segmentsuche
title: Segment Search API Endpoint
description: In der Adobe Experience Platform Segmentation Service-API wird die Segmentsuche verwendet, um Felder aus verschiedenen Datenquellen zu durchsuchen und nahezu in Echtzeit zurückzugeben. Dieses Handbuch enthält Informationen zum besseren Verständnis der Segmentsuche sowie Beispiel-API-Aufrufe zum Ausführen grundlegender Aktionen mithilfe der API.
exl-id: bcafbed7-e4ae-49c0-a8ba-7845d8ad663b
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1201'
ht-degree: 6%

---

# Segmentsuchendpunkt

Die Segmentsuche wird verwendet, um Felder zu durchsuchen, die in verschiedenen Datenquellen enthalten sind, und sie nahezu in Echtzeit zurückzugeben.

Dieses Handbuch enthält Informationen zum besseren Verständnis der Segmentsuche sowie Beispiel-API-Aufrufe zum Ausführen grundlegender Aktionen mithilfe der API.

## Erste Schritte

Die in diesem Handbuch verwendeten API-Endpunkte sind Teil der [!DNL Adobe Experience Platform Segmentation Service]-. Bevor Sie fortfahren, lesen Sie bitte die [Erste Schritte](./getting-started.md) für wichtige Informationen, die Sie benötigen, um die API erfolgreich aufrufen zu können, einschließlich erforderlicher Kopfzeilen und Informationen zum Lesen von Beispiel-API-Aufrufen.

Zusätzlich zu den erforderlichen Kopfzeilen, die im Abschnitt &quot;Erste Schritte&quot;beschrieben werden, benötigen alle Anforderungen an den Segmentsuchendpunkt die folgende zusätzliche Kopfzeile:

- x-ups-search-version: &quot;1.0&quot;

### Durchsuchen mehrerer Namespaces

Dieser Suchendpunkt kann verwendet werden, um über verschiedene Namespaces hinweg zu suchen und eine Liste mit Suchergebnissen zurückzugeben. Es können mehrere Parameter verwendet werden, getrennt durch das kaufmännische Und-Zeichen (&amp;).

**API-Format**

```http
GET /search/namespaces?schema.name={SCHEMA}
GET /search/namespaces?schema.name={SCHEMA}&s={SEARCH_TERM}
```

| Parameter | Beschreibung |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Erforderlich)** Wobei {SCHEMA} den Schemaklasse-Wert darstellt, der den Suchobjekten zugeordnet ist. Derzeit wird nur `_xdm.context.segmentdefinition` unterstützt. |
| `s={SEARCH_TERM}` | *(Optional)* Dabei stellt {SEARCH_TERM} eine Abfrage dar, die der Implementierung von Microsoft entspricht. [Suchsyntax von Lucene](https://docs.microsoft.com/de-DE/azure/search/query-lucene-syntax). Wenn kein Suchbegriff angegeben ist, werden alle Datensätze, die mit `schema.name` zurückgegeben. Eine ausführlichere Erläuterung finden Sie im Abschnitt [Anhang](#appendix) dieses Dokuments. |

**Anfrage**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/namespaces?schema.name=_xdm.context.segmentdefinition \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

### Suche nach einzelnen Entitäten

Mit diesem Suchendpunkt können Sie eine Liste aller im angegebenen Namespace indizierten Volltext-Objekte abrufen. Es können mehrere Parameter verwendet werden, getrennt durch das kaufmännische Und-Zeichen (&amp;).

**API-Format**

```http
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&s={SEARCH_TERM}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| Parameter | Beschreibung |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Erforderlich)** Wobei {SCHEMA} den Schemaklasse-Wert enthält, der den Suchobjekten zugeordnet ist. Derzeit wird nur `_xdm.context.segmentdefinition` unterstützt. |
| `namespace={NAMESPACE}` | **(Erforderlich)** Dabei enthält {NAMESPACE} den Namespace, in dem Sie suchen möchten. |
| `s={SEARCH_TERM}` | *(Optional)* Dabei enthält {SEARCH_TERM} eine Abfrage, die der Implementierung von Microsoft entspricht. [Suchsyntax von Lucene](https://docs.microsoft.com/de-DE/azure/search/query-lucene-syntax). Wenn kein Suchbegriff angegeben ist, werden alle Datensätze, die mit `schema.name` zurückgegeben. Eine ausführlichere Erläuterung finden Sie im Abschnitt [Anhang](#appendix) dieses Dokuments. |
| `entityId={ENTITY_ID}` | *(Optional)* Beschränkt Ihre Suche auf den angegebenen Ordner, der mit {ENTITY_ID} angegeben wird. |
| `limit={LIMIT}` | *(Optional)* Wobei {LIMIT} die Anzahl der zurückzugebenden Suchergebnisse darstellt. Der Standardwert lautet 50. |
| `page={PAGE}` | *(Optional)* Dabei steht {PAGE} für die Seitennummer, die zum Paginieren der Ergebnisse der gesuchten Abfrage verwendet wird. Beachten Sie, dass die Seitenzahl bei **0**. |


**Anfrage**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/entities?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 zurück, wobei die Ergebnisse mit der Suchabfrage übereinstimmen.

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

### Abrufen von Strukturinformationen über ein Suchobjekt

Mit diesem Suchendpunkt können Sie die Strukturinformationen zum angeforderten Suchobjekt abrufen.

**API-Format**

```http
GET /search/taxonomy?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| Parameter | Beschreibung |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Erforderlich)** Wobei {SCHEMA} den Schemaklasse-Wert enthält, der den Suchobjekten zugeordnet ist. Derzeit wird nur `_xdm.context.segmentdefinition` unterstützt. |
| `namespace={NAMESPACE}` | **(Erforderlich)** Dabei enthält {NAMESPACE} den Namespace, in dem Sie suchen möchten. |
| `entityId={ENTITY_ID}` | **(Erforderlich)** Die ID des Suchobjekts, für das Sie die Strukturinformationen abrufen möchten, angegeben mit {ENTITY_ID}. |

**Anfrage**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/taxonomy?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments&entityId=porsche11037 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit detaillierten Strukturinformationen zum angeforderten Suchobjekt zurück.

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

Nach dem Lesen dieses Handbuchs haben Sie jetzt ein besseres Verständnis davon, wie die Segmentsuche funktioniert.

## Anhang {#appendix}

Die folgenden Abschnitte enthalten zusätzliche Informationen zur Funktionsweise von Suchbegriffen. Suchabfragen werden wie folgt geschrieben: `s={FieldName}:{SearchExpression}`. Um beispielsweise nach einem Segment mit dem Namen AAM oder [!DNL Platform]verwenden, würden Sie die folgende Suchabfrage verwenden: `s=segmentName:AAM%20OR%20Platform`.

> !![NOTE] Für Best Practices sollte der Suchausdruck wie im oben gezeigten Beispiel HTML-kodiert sein.

### Suchfelder {#search-fields}

In der folgenden Tabelle sind die Felder aufgeführt, die im Suchabfrageparameter gesucht werden können.

| Feldname | Beschreibung |
| ---------- | ----------- |
| folderId | Der Ordner oder die Ordner mit der Ordner-ID der angegebenen Suche. |
| folderLocation | Der Speicherort bzw. die Speicherorte mit dem Ordnerspeicherort der angegebenen Suche. |
| parentFolderId | Das Segment oder den Ordner mit der übergeordneten Ordner-ID der angegebenen Suche. |
| segmentId | Das Segment stimmt mit der Segment-ID Ihrer angegebenen Suche überein. |
| segmentName | Das Segment stimmt mit dem Segmentnamen der angegebenen Suche überein. |
| segmentDescription | Das Segment stimmt mit der Segmentbeschreibung der angegebenen Suche überein. |

### Suchausdruck {#search-expression}

In der folgenden Tabelle finden Sie die Details zur Funktionsweise von Suchabfragen bei der Verwendung der Segmentsuche-API.

>!![NOTE] Die folgenden Beispiele werden in einem nicht-HTML-kodierten Format angezeigt, um eine bessere Übersichtlichkeit zu erzielen. Best Practices finden Sie unter HTML-Kodierung Ihres Suchausdrucks.

| Beispielsuchausdruck | Beschreibung |
| ------------------------- | ----------- |
| foo | Suchen Sie nach einem beliebigen Wort. Dies gibt Ergebnisse zurück, wenn das Wort &quot;foo&quot;in einem der durchsuchbaren Felder gefunden wird. |
| foo AND bar | Eine boolesche Suche. Dies gibt Ergebnisse zurück, wenn **both** Die Wörter &quot;foo&quot; und &quot;bar&quot; befinden sich in allen durchsuchbaren Feldern. |
| foo OR bar | Eine boolesche Suche. Dies gibt Ergebnisse zurück, wenn **entweder** das Wort &quot;foo&quot; oder das Wort &quot;bar&quot; finden Sie in allen durchsuchbaren Feldern. |
| foo NOT bar | Eine boolesche Suche. Dies gibt Ergebnisse zurück, wenn das Wort &quot;foo&quot;gefunden wird, das Wort &quot;bar&quot;jedoch in keinem der durchsuchbaren Felder gefunden wird. |
| name: foo AND bar | Eine boolesche Suche. Dies gibt Ergebnisse zurück, wenn **both** Die Wörter &quot;foo&quot; und &quot;bar&quot; finden Sie im Feld &quot;name&quot;. |
| run* | Eine Platzhaltersuche. Die Verwendung eines Sternchens (*) entspricht 0 oder mehr Zeichen, d. h. es werden Ergebnisse ausgegeben, wenn der Inhalt eines durchsuchbaren Felds ein Wort enthält, das mit &quot;run&quot;beginnt. Dies gibt beispielsweise Ergebnisse zurück, wenn die Wörter &quot;wird ausgeführt&quot;, &quot;läuft&quot;, &quot;runner&quot;oder &quot;runt&quot;angezeigt werden. |
| Cam? | Eine Platzhaltersuche. Verwenden eines Fragezeichens (?) entspricht nur genau einem Zeichen. Das bedeutet, dass Ergebnisse ausgegeben werden, wenn der Inhalt eines durchsuchbaren Felds mit &quot;cam&quot;und einem zusätzlichen Buchstaben beginnt. Dies gibt beispielsweise Ergebnisse zurück, wenn die Wörter &quot;Camp&quot;oder &quot;Cams&quot;angezeigt werden, aber keine Ergebnisse zurückgeben, wenn die Wörter &quot;Camera&quot;oder &quot;Campfire&quot;angezeigt werden. |
| &quot;blauer Regenschirm&quot; | Eine Satzsuche. Dies gibt Ergebnisse zurück, wenn der Inhalt eines durchsuchbaren Felds den vollständigen Wortlaut &quot;blauer Schirm&quot;enthält. |
| blue\~ | Eine unscharfe Suche. Optional können Sie eine Zahl zwischen 0 und 2 nach der Tilde (~) setzen, um den Bearbeitungsabstand anzugeben. Beispielsweise würde &quot;blue\~1&quot;&quot;blue&quot;, &quot;blues&quot;oder &quot;kleue&quot;zurückgeben. Unscharfe Suche kann **only** auf Begriffe, nicht auf Sätze angewendet werden. Sie können jedoch am Ende jedes Wortes in einer Wortgruppe Tildes anhängen. Beispielsweise würde &quot;camping\~ in\~ the\~ summer\~&quot;mit &quot;camping im Sommer&quot;übereinstimmen. |
| &quot;Hotel Airport&quot;\~5 | Näherungssuche. Diese Art der Suche wird verwendet, um Begriffe zu finden, die in einem Dokument nahe beieinander liegen. Beispielsweise die Wortgruppe `"hotel airport"~5` findet die Begriffe &quot;Hotel&quot; und &quot;Flughafen&quot; innerhalb von 5 Wörtern voneinander in einem Dokument. |
| `/a[0-9]+b$/` | Suche nach regulären Ausdrücken. Diese Art der Suche findet eine Übereinstimmung basierend auf dem Inhalt zwischen Schrägstrichen &quot;/&quot;, wie in der RegExp-Klasse dokumentiert. Um beispielsweise Dokumente zu finden, die &quot;motel&quot;oder &quot;hotel&quot;enthalten, geben Sie `/[mh]otel/`. Die Suche nach regulären Ausdrücken wird mit einzelnen Wörtern abgeglichen. |

Eine ausführlichere Dokumentation zur Abfragesyntax finden Sie im Abschnitt [Dokumentation zur Lucene-Abfragesyntax](https://docs.microsoft.com/de-DE/azure/search/query-lucene-syntax).
