---
title: API-Endpunkt für die Segmentsuche
description: In der Segmentierungs-Service-API von Adobe Experience Platform wird die Segmentsuche verwendet, um Felder aus verschiedenen Datenquellen zu suchen und sie nahezu in Echtzeit zurückzugeben. Dieses Handbuch enthält Informationen zum besseren Verständnis der Segmentsuche sowie Beispiele für API-Aufrufe zum Ausführen einfacher Aktionen mithilfe der -API.
role: Developer
exl-id: bcafbed7-e4ae-49c0-a8ba-7845d8ad663b
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1178'
ht-degree: 5%

---

# Endpunkt der Segmentsuche

Die Segmentsuche wird verwendet, um Felder aus verschiedenen Datenquellen zu suchen und sie nahezu in Echtzeit zurückzugeben.

Dieses Handbuch enthält Informationen zum besseren Verständnis der Segmentsuche sowie Beispiele für API-Aufrufe zum Ausführen einfacher Aktionen mithilfe der -API.

## Erste Schritte

Die in diesem Handbuch verwendeten Endpunkte sind Teil der [!DNL Adobe Experience Platform Segmentation Service]-API. Bevor Sie fortfahren, lesen Sie den Abschnitt [Erste Schritte](./getting-started.md). Dort erhalten Sie wichtige Informationen darüber, wie Sie die API aufrufen und die erforderlichen Kopfzeilen sowie Beispiele für API-Aufrufe lesen können.

Zusätzlich zu den erforderlichen Kopfzeilen, die im Abschnitt Erste Schritte beschrieben sind, erfordern alle Anfragen an den Segmentsuchendpunkt die folgende zusätzliche Kopfzeile:

- x-ups-search-version: „1.0“

### Suchen über mehrere Namespaces hinweg

Dieser Suchendpunkt kann verwendet werden, um über verschiedene Namespaces hinweg zu suchen und eine Liste von Suchergebnissen zurückzugeben. Es können mehrere Parameter verwendet werden, die durch kaufmännische Und-Zeichen (&amp;) voneinander getrennt werden.

**API-Format**

```http
GET /search/namespaces?schema.name={SCHEMA}
GET /search/namespaces?schema.name={SCHEMA}&s={SEARCH_TERM}
```

| Parameter | Beschreibung |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Erforderlich)** Wobei {SCHEMA} den Schemaklasse-Wert darstellt, der mit den Suchobjekten verknüpft ist. Derzeit wird nur `_xdm.context.segmentdefinition` unterstützt. |
| `s={SEARCH_TERM}` | *(Optional)* Dabei stellt {SEARCH_TERM} eine Abfrage dar, die der Microsoft-Implementierung der [Suchsyntax von Lucene) ](https://docs.microsoft.com/de-DE/azure/search/query-lucene-syntax). Wenn kein Suchbegriff angegeben wird, werden alle mit `schema.name` verknüpften Datensätze zurückgegeben. Eine detailliertere Erklärung finden Sie im [Anhang](#appendix) dieses Dokuments. |

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

### Suchen nach einzelnen Entitäten

Dieser Suchendpunkt kann verwendet werden, um eine Liste aller Volltext-indizierten Objekte innerhalb des angegebenen Namespace abzurufen. Es können mehrere Parameter verwendet werden, die durch kaufmännische Und-Zeichen (&amp;) voneinander getrennt werden.

**API-Format**

```http
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&s={SEARCH_TERM}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| Parameter | Beschreibung |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Erforderlich)** Hierbei enthält {SCHEMA} den mit den Suchobjekten verknüpften Schemaklasse-Wert. Derzeit wird nur `_xdm.context.segmentdefinition` unterstützt. |
| `namespace={NAMESPACE}` | **(Erforderlich)** Wobei {NAMESPACE} den Namespace enthält, in dem gesucht werden soll. |
| `s={SEARCH_TERM}` | *(Optional)* Hierbei enthält {SEARCH_TERM} eine Abfrage, die der Microsoft-Implementierung der [Suchsyntax von Lucene](https://docs.microsoft.com/de-DE/azure/search/query-lucene-syntax) entspricht. Wenn kein Suchbegriff angegeben wird, werden alle mit `schema.name` verknüpften Datensätze zurückgegeben. Eine detailliertere Erklärung finden Sie im [Anhang](#appendix) dieses Dokuments. |
| `entityId={ENTITY_ID}` | *(Optional)* Schränkt die Suche auf den angegebenen Ordner ein, der mit {ENTITY_ID} angegeben ist. |
| `limit={LIMIT}` | *(Optional)* Dabei steht {LIMIT} für die Anzahl der zurückzugebenden Suchergebnisse. Der Standardwert lautet 50. |
| `page={PAGE}` | *(Optional)* Dabei entspricht {PAGE} der Seitenzahl, die für die Paginierung der Ergebnisse der durchsuchten Abfrage verwendet wird. Bitte beachten Sie, dass die Seitennummer bei **0** beginnt. |


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

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit Ergebnissen zurückgegeben, die mit der Suchanfrage übereinstimmen.

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

Dieser Suchendpunkt kann verwendet werden, um die Strukturinformationen zum angeforderten Suchobjekt abzurufen.

**API-Format**

```http
GET /search/taxonomy?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| Parameter | Beschreibung |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Erforderlich)** Hierbei enthält {SCHEMA} den mit den Suchobjekten verknüpften Schemaklasse-Wert. Derzeit wird nur `_xdm.context.segmentdefinition` unterstützt. |
| `namespace={NAMESPACE}` | **(Erforderlich)** Wobei {NAMESPACE} den Namespace enthält, in dem gesucht werden soll. |
| `entityId={ENTITY_ID}` | **(Erforderlich)** Die ID des Suchobjekts, zu dem Sie die Strukturinformationen abrufen möchten, angegeben mit {ENTITY_ID}. |

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

Eine erfolgreiche Antwort gibt den HTTP-Status-Code 200 mit detaillierten Strukturinformationen zum angeforderten Suchobjekt zurück.

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

Nach dem Lesen dieses Handbuchs wissen Sie jetzt besser, wie die Segmentsuche funktioniert.

## Anhang {#appendix}

Die folgenden Abschnitte enthalten zusätzliche Informationen zur Funktionsweise von Suchbegriffen. Suchabfragen werden wie folgt geschrieben: `s={FieldName}:{SearchExpression}`. Um beispielsweise nach einer Segmentdefinition mit dem Namen AAM oder [!DNL Platform] zu suchen, verwenden Sie die folgende Suchabfrage: `s=segmentName:AAM%20OR%20Platform`.

>[!NOTE]
>
>Als Best Practices sollte der Suchausdruck wie im Beispiel oben HTML-kodiert sein.

### Suchfelder {#search-fields}

In der folgenden Tabelle sind die Felder aufgeführt, die mit dem Abfrageparameter durchsucht werden können.

| Feldname | Beschreibung |
| ---------- | ----------- |
| folderId | Der Ordner oder die Ordner mit der Ordner-ID der angegebenen Suche. |
| folderLocation | Der Speicherort oder die Speicherorte, die den Ordnerspeicherort Ihrer angegebenen Suche haben. |
| parentFolderId | Die Segmentdefinition oder der Ordner, die bzw. der die übergeordnete Ordner-ID der angegebenen Suche aufweist. |
| segmentId | Die Segmentdefinition, die der Segment-ID Ihrer angegebenen Suche entspricht. |
| segmentName | Die Segmentdefinition, die dem Segmentnamen Ihrer angegebenen Suche entspricht. |
| segmentDescription | Die Segmentdefinition, die der Segmentbeschreibung der angegebenen Suche entspricht. |

### Suchausdruck {#search-expression}

In der folgenden Tabelle sind die Besonderheiten der Funktionsweise von Suchabfragen bei Verwendung der Segmentsuche-API aufgeführt.

>[!NOTE]
>
>Die folgenden Beispiele werden der besseren Übersichtlichkeit halber in einem nicht HTML-kodierten Format angezeigt. Bewährte Verfahren finden Sie, indem Sie Ihren Suchausdruck mit HTML kodieren.

| Beispielsuchausdruck | Beschreibung |
| ------------------------- | ----------- |
| treiben | Suchen Sie nach einem beliebigen Wort. Dies gibt Ergebnisse zurück, wenn das Wort „foo“ in einem der durchsuchbaren Felder gefunden wird. |
| Lebensmittel UND Bar | Eine boolesche Suche. Dies gibt Ergebnisse zurück **wenn** beide“ Wörter „foo“ und „bar“ in einem der durchsuchbaren Felder gefunden werden. |
| Fußleiste ODER | Eine boolesche Suche. Dies gibt Ergebnisse zurück **wenn entweder** Wort „foo“ oder das Wort „bar“ in einem der durchsuchbaren Felder gefunden wird. |
| Foo NOT bar | Eine boolesche Suche. Dies gibt Ergebnisse zurück, wenn das Wort „foo“ gefunden wird, aber das Wort „bar“ in keinem der durchsuchbaren Felder gefunden wird. |
| Name: foo AND bar | Eine boolesche Suche. Dies gibt Ergebnisse zurück **wenn** beide“ Wörter „foo“ und „bar“ im Feld „name“ gefunden werden. |
| Durchgang* | Eine Platzhaltersuche. Bei Verwendung eines Sternchens (*) besteht eine Übereinstimmung aus 0 oder mehr Zeichen, was bedeutet, dass Ergebnisse zurückgegeben werden, wenn der Inhalt eines der durchsuchbaren Felder ein Wort enthält, das mit „run“ beginnt. Dies liefert z. B. Ergebnisse, wenn die Wörter „running“, „running“, „runner“ oder „runt“ erscheinen. |
| Cam? | Eine Platzhaltersuche. Mit einem Fragezeichen (?) stimmt nur mit genau einem Zeichen überein, d. h. es werden Ergebnisse zurückgegeben, wenn der Inhalt eines der durchsuchbaren Felder mit „cam“ und einem zusätzlichen Buchstaben beginnt. Beispielsweise werden Ergebnisse zurückgegeben, wenn die Wörter „camp“ oder „cams“ angezeigt werden, jedoch keine Ergebnisse, wenn die Wörter „campaign“ oder „campfire“ zu sehen sind. |
| „Blauer Regenschirm“ | Eine Suche nach Phrasen. Daraufhin werden Ergebnisse zurückgegeben, wenn der Inhalt eines der durchsuchbaren Felder die vollständige Phrase „blue umbrella“ enthält. |
| blau\~ | Eine unscharfe Suche. Optional können Sie eine Zahl zwischen 0 und 2 nach der Tilde (~) einfügen, um den Bearbeitungsabstand festzulegen. „blue\~1“ würde beispielsweise „blue“, „blues“ oder „glue“ zurückgeben. Eine unscharfe Suche kann **nur** auf Begriffe und nicht auf Phrasen angewendet werden. Sie können jedoch Tilden an das Ende jedes Wortes in einer Phrase anhängen. So würde beispielsweise „camping\~ in\~ der\~ Sommer\~&quot; mit „camping im Sommer“ übereinstimmen. |
| „Hotelflughafen“\~5 | Eine Suche in der Nähe. Diese Art der Suche wird verwendet, um Begriffe zu finden, die in einem Dokument nahe beieinander liegen. Zum Beispiel findet die Phrase `"hotel airport"~5` die Begriffe „Hotel“ und „Flughafen“ innerhalb von 5 Wörtern voneinander in einem Dokument. |
| `/a[0-9]+b$/` | Suche nach regulären Ausdrücken. Diese Art der Suche findet eine Übereinstimmung basierend auf dem Inhalt zwischen Schrägstrichen &quot;/&quot;, wie in der RegExp-Klasse dokumentiert. Um beispielsweise Dokumente zu finden, die „motel“ oder „hotel“ enthalten, geben Sie `/[mh]otel/` an. Suchen nach regulären Ausdrücken werden mit einzelnen Wörtern abgeglichen. |

Eine detailliertere Dokumentation zur Abfragesyntax finden Sie in der [Dokumentation zur Lucene-Abfragesyntax](https://docs.microsoft.com/de-DE/azure/search/query-lucene-syntax).
