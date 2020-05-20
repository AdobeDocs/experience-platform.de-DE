---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Entwicklerhandbuch für Customer Profil-API in Echtzeit
topic: guide
translation-type: tm+mt
source-git-commit: 95e002c60389ca7e4c1dcf32bbcf6f552cd55d95
workflow-type: tm+mt
source-wordcount: '1078'
ht-degree: 1%

---


# Profil-Suche

Mit der Profil-Suche können konfigurierbare Felder, die in verschiedenen Datenquellen enthalten sind, gesucht und indexiert werden und in Echtzeit zurückgegeben werden.

Dieses Handbuch enthält Informationen zum besseren Verständnis der Suche nach Profilen sowie Beispiele für API-Aufrufe zur Durchführung grundlegender Aktionen mit der API.

## Erste Schritte

Die in diesem Handbuch verwendeten API-Endpunkte sind Teil der Real-time Customer Profil API. Bevor Sie fortfahren, lesen Sie sich bitte das Entwicklerhandbuch für [Echtzeit-Profil durch](getting-started.md).

Insbesondere enthält der [Abschnitt](getting-started.md) &quot;Erste Schritte&quot;des Profil-Entwicklerhandbuchs Links zu verwandten Themen, eine Anleitung zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtige Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen von Experience Platform-APIs benötigt werden.

### Suchergebnisse abrufen

Der Suchendpunkt kann verwendet werden, um Suchergebnisse basierend auf den Werten des erforderlichen `schema.name` Parameters und zusätzlichen optionalen Parametern für die Abfrage zu erhalten. Es können mehrere Parameter verwendet werden, die durch das kaufmännische Und (&amp;) getrennt werden.

**API-Format**

```http
GET /search?{QUERY_PARAMETERS}
```

| Parameter | Beschreibung |
|---|---|
| `schema.name` | **Erforderlich.** Der Name der Schema-Klasse, die den zu durchsuchenden Inhalt enthält und in Punkt-Notation geschrieben ist. Derzeit wird nur `schema.name=_xdm.context.segmentdefinition` unterstützt. |
| `limit` | Die Anzahl der zurückzugebenden Suchergebnisse. Der Standardwert lautet 50. |
| `page` | Die Seitenzahl, die für die Paginierung der Ergebnisse der gesuchten Abfrage verwendet wird. |
| `s` | Eine Abfrage, die der Implementierung der Suchsyntax von [Lucene durch Microsoft entspricht](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). Wenn kein Suchbegriff angegeben ist, werden alle damit verbundenen Datensätze zurückgegeben `schema.name` . Eine ausführlichere Erläuterung finden Sie im Abschnitt [Suchparameter](#search-parameters) dieses Dokuments. |
| `namespace` | Identifiziert die tatsächlichen Daten, die nach der im `schema.name` Parameter angegebenen Schema-Klasse gesucht werden sollen. |
| `organization.type` | Bestimmt den Inhalt der Antwort. Das Format des zurückgegebenen Inhalts hängt von den in verwendeten Werten ab `schema.name`. Die gültigen Werte `_xdm.context.segmentdefinition`sind beispielsweise `hierarchy` oder `hierarchyinfo`. |
| `organization.id` | **Erforderlich, wenn`organization.type`angegeben.** Gibt die Hierarchie der angegebenen Organisation an, wenn sie mit dem `organization.type` von verwendet wird. |

**Anfrage**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search?schema.name=_xdm.context.segmentdefinition \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt ein Array von Objekten zurück, die Ihre Suchkriterien erfüllen. In diesem Beispiel wird eine Liste von Segmentdefinitionen zurückgegeben, da der `schema.name` Parameter `_xdm.context.segmentdefinition`angegeben wurde.

```json
{
  "aam-hierarchy": {
    "_xdm.context.segmentdefinition": [
      {
        "isFolder": true,
        "id": "100023",
        "name": "Segment Definition 1",
        "description": "Sample description.",
        "parentFolderId": "99970"
      },
      {
        "isFolder": false,
        "id": "1000028",
        "name": "Segment Definition 2",
        "description": "Sample description.",
        "parentFolderId": "103584"
      }
    ]
  },
  "page": {
    "totalCount": 2,
    "totalPages": 1,
    "pageOffset": "1",
    "pageSize": 2,
    "limit": 2
  }
}
```

### Bereitstellungsanforderungen erstellen

Sie können Bereitstellungsanforderungen erstellen, um die Suche nach Profilen auf Schemas zu aktivieren, indem Sie eine POST-Anforderung an den `/search/provisioning/component/init` Endpunkt senden.

**Anfrage**

>[!CAUTION]
>Diese POST-Anforderung enthält keine Payload und erfordert daher keinen Content-Type-Header. Außerdem gibt es keinen Sandbox-Header, da alle Daten in eine globale Sandbox gesendet werden.

```shell
curl -X POST \
    https://platform.adobe.io/data/core/ups/search/provisioning/component/init \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' 
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 201 (Erstellt) und folgende Meldung zurück:

```plaintext
The request has been fulfilled and resulted in a new resource being created.
```

### Konfigurationsanforderungen bearbeiten

Der Konfigurationsendpunkt kann verwendet werden, um die richtigen Indizes, Indizes und Datenquellenverbindungen für eine neue IMS-Organisation einzurichten. Zur Bearbeitung von Konfigurationsanforderungen sind zwei Eigenschaften erforderlich: `databaseName` und `containerName`.

`databaseName` der Name der Profil-Datenbank für die zu konfigurierende Organisation.

`containerName` steht für den Namen des Containers, der von einem Data Connector ausgefüllt wird, was während der Konfiguration gelesen wird. Es gibt zwei Werte für `containerName`die eine oder beide können in der POST-Anforderung verwendet werden:
- `_xdm.content.segmentdefinition`
- `_experience.audiencemanager.segmentfolder`

### Erstellen einer Konfigurationsanforderung

Der folgende API-Aufruf generiert die erforderliche Datenquelle, den Indexer und den Index basierend auf den Parametern, die in der Anforderungsnutzlast angegeben sind.

**API-Format**

```http
POST /search/configure
```

**Anfrage**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/search/configure \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "databaseName": {DATABASE_NAME},
    "containerName": "_xdm.context.segmentdefinition" "_experience.audiencemanager.segmentfolder"
  }'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 202 (Akzeptiert) und eine Klartext-Meldung zurück.

```plaintext
The request has been accepted for processing, but the processing has not been completed.
```

### Eine Konfigurationsanforderung löschen

Der folgende API-Aufruf entfernt übereinstimmende Indexeinträge und löscht den Indexer und die Datenquelle anhand der in der Anforderungsnutzlast bereitgestellten Parameter.

>[!NOTE]
>Der Index selbst wird nicht gelöscht, da er eine freigegebene Ressource ist.

**API-Format**

```http
DELETE /search/configure
```

**Anfrage**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/search/configure \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "databaseName": {DATABASE_NAME},
    "containerName": "_xdm.context.segmentdefinition" "_experience.audiencemanager.segmentfolder"
  }'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 202 (Akzeptiert) und eine Klartext-Meldung zurück.

```plaintext
The request has been accepted for processing, but the processing has not been completed.
```

## Nächste Schritte

Nach dem Lesen dieses Handbuchs haben Sie nun ein besseres Verständnis dafür, wie die Echtzeit-Suche nach Kunden-Profilen funktioniert. Weitere Informationen zum Echtzeit-Customer-Profil finden Sie in der Übersicht zum [Echtzeit-Customer-Profil](../home.md). Weitere Informationen zur Segmentierung finden Sie in der [Segmentierungsübersicht](../../segmentation/home.md).

## Anhang {#appendix}

### Suchparameter {#search-parameters}

In der folgenden Tabelle werden die Details zur Funktionsweise des Suchparameters bei Verwendung der Such-API Liste.

| Abfrage suchen | Beschreibung |
|------------ | -----------|
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

Weitere Informationen zur Syntax der Abfrage finden Sie in der [Lucene-Abfrage-Syntaxdokumentation](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax).
