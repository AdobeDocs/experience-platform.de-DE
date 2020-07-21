---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Entwicklerhandbuch für Query Service
topic: queries
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 34%

---


# Abfragen

## Beispiel-API-Aufrufe

The following sections walk through calls you can make using the `/queries` endpoint in the [!DNL Query Service] API. Jeder Aufruf enthält das allgemeine API-Format, eine Beispielanfrage mit den erforderlichen Kopfzeilen und eine Beispielantwort.

### Eine Liste von Abfragen abrufen

You can retrieve a list of all queries for your IMS Organization by making a GET request to the `/queries` endpoint.

**API-Format**

```http
GET /queries
GET /queries?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`: (*Optional*) Ergänzende Parameter für den Anfragepfad, die zur Konfiguration der in der Antwort zurückgegebenen Ergebnisse dienen. Die Angabe mehrere Parameter ist ebenfalls möglich. Trennen Sie sie dazu unter Verwendung des kaufmännischen Und-Zeichens (`&`) voneinander. Die verfügbaren Parameter sind unten aufgeführt.

**Abfrage**

Im Folgenden finden Sie eine Liste der verfügbaren Abfragen für die Auflistung von Abfragen. Alle diese Parameter sind optional. Wenn Sie diesen Endpunkt ohne Parameter aufrufen, werden alle für Ihr Unternehmen verfügbaren Abfragen abgerufen.

| Parameter | Beschreibung |
| --------- | ----------- |
| `orderby` | Gibt das Feld an, nach dem Ergebnisse sortiert werden sollen. Unterstützte Felder sind `created` und `updated`. `orderby=created` beispielsweise wird Ergebnisse in aufsteigender Reihenfolge sortieren. Durch Hinzufügen eines `-`-Zeichens vor „created“ (`orderby=-created`) werden Elemente in absteigender Reihenfolge sortiert. |
| `limit` | Gibt die Seitengrößenbeschränkung an, um die Anzahl der Ergebnisse zu steuern, die auf einer Seite enthalten sind. (*Standardwert: 20*) |
| `start` | Versetzt die Antwortliste mit einer nullbasierten Nummerierung. Beispielsweise gibt `start=2` eine Liste ab der dritten aufgeführten Abfrage zurück. (*Standardwert: 0*) |
| `property` | Filtern Sie Ergebnisse anhand von Feldern. Die Filter **müssen** HTML-Escape-Zeichen aufweisen. Kommas dienen dazu, um mehrere Filter zu kombinieren. The supported fields are `created`, `updated`, `state`, and `id`. Die Liste der unterstützten Operatoren ist `>` (größer als), `<` (kleiner als), `>=` (größer gleich), `<=` (kleiner gleich), `==` (gleich), `!=` (nicht gleich) und `~` (enthält). Gibt beispielsweise alle Abfragen mit der angegebenen ID zurück. `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` |
| `excludeSoftDeleted` | Gibt an, ob eine Abfrage, die weich gelöscht wurde, einbezogen werden soll. Beispielsweise `excludeSoftDeleted=false` werden **auch** gelöschte Abfragen einbezogen. (*Boolescher Wert, Standardwert: true*) |
| `excludeHidden` | Gibt an, ob nicht vom Benutzer gesteuerte Abfragen angezeigt werden sollen. Wenn dieser Wert auf &quot;false&quot;gesetzt ist, werden nicht vom Benutzer gesteuerte Abfragen wie CURSOR-Definitionen, FETCH- oder Metadaten-Abfragen **einbezogen** . (*Boolescher Wert, Standardwert: true*) |

**Anfrage**

Mit der folgenden Anforderung wird die neueste für Ihr IMS-Unternehmen erstellte Abfrage abgerufen.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries?limit=1 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit einer Liste von Abfragen für die angegebene IMS-Organisation als JSON zurück. Die folgende Antwort gibt die neueste Abfrage zurück, die für Ihr IMS-Unternehmen erstellt wurde.

```json
{
    "queries": [
        {
            "isInsertInto": false,
            "request": {
                "dbName": "prod:all",
                "sql": "SELECT *\nFROM\n  accounts\nLIMIT 10\n"
            },
            "state": "SUCCESS",
            "rowCount": 0,
            "errors": [],
            "isCTAS": false,
            "version": 1,
            "id": "9957bd7f-2244-4fd5-91bc-077d7df1d8e5",
            "elapsedTime": 28,
            "updated": "2019-12-06T22:00:17.390Z",
            "client": "Adobe Query Service UI",
            "userId": "{USER_ID}",
            "created": "2019-12-06T22:00:17.362Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/queries/9957bd7f-2244-4fd5-91bc-077d7df1d8e5",
                    "method": "GET"
                },
                "soft_delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/queries/9957bd7f-2244-4fd5-91bc-077d7df1d8e5",
                    "method": "PATCH",
                    "body": "{ \"op\": \"soft_delete\"}"
                },
                "referenced_datasets": [
                    {
                        "id": "5b2bdd32230d4401de87397c",
                        "href": "https://platform.adobe.io/data/foundation/catalog/dataSets/5b2bdd32230d4401de87397c"
                    }
                ]
            }
        }
    ],
    "_page": {
        "orderby": "-created",
        "start": "2019-12-06T22:00:17.362Z",
        "next": "2019-08-01T00:14:21.748Z",
        "count": 1
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/query/queries?orderby=-created&start=2019-08-01T00:14:21.748Z"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/query/queries?orderby=-created&start=2019-12-06T22:00:17.362Z&isPrevLink=true"
        }
    },
    "version": 1
}
```

### Eine Abfrage erstellen

You can create a new query by making a POST request to the `/queries` endpoint.

**API-Format**

```http
POST /queries
```

**Anfrage**

Mit der folgenden Anforderung wird eine neue Abfrage erstellt, die durch die in der Payload bereitgestellten Werte konfiguriert wird:

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/queries \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Query"
        "description": "Sample Description"
    }  
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `dbName` | Der Name der Datenbank, für die Sie eine SQL-Abfrage erstellen. |
| `sql` | Die SQL-Abfrage, die Sie erstellen möchten. |
| `name` | Der Name der SQL-Abfrage. |
| `description` | Die Beschreibung Ihrer SQL-Abfrage. |

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 202 (Akzeptiert) mit Details zu Ihrer neu erstellten Abfrage zurück. Sobald die Abfrage aktiviert ist und erfolgreich ausgeführt wurde, ändert sich der `state` Vorgang von `SUBMITTED` zu `SUCCESS`.

```json
{
    "isInsertInto": false,
    "request": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Query",
        "description": "Sample Description"
    },
    "state": "SUBMITTED",
    "rowCount": 0,
    "errors": [],
    "isCTAS": false,
    "version": 1,
    "id": "4d64cd49-cf8f-463a-a182-54bccb9954fc",
    "elapsedTime": 0,
    "updated": "2020-01-08T21:47:46.865Z",
    "client": "API",
    "userId": "{USER_ID}",
    "created": "2020-01-08T21:47:46.865Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "GET"
        },
        "soft_delete": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"soft_delete\"}"
        },
        "cancel": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\"}"
        }
    }
}
```

>[!NOTE]
>
>You can use the value of `_links.cancel` to [cancel your created query](#cancel-a-query).

### Abrufen einer Abfrage nach ID

You can retrieve detailed information about a specific query by making a GET request to the `/queries` endpoint and providing the query&#39;s `id` value in the request path.

**API-Format**

```http
GET /queries/{QUERY_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{QUERY_ID}` | The `id` value of the query you want to retrieve. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit detaillierten Informationen zur angegebenen Abfrage zurück.

```json
{
    "isInsertInto": false,
    "request": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Query",
        "description": "Sample Description"
    },
    "state": "SUBMITTED",
    "rowCount": 0,
    "errors": [],
    "isCTAS": false,
    "version": 1,
    "id": "4d64cd49-cf8f-463a-a182-54bccb9954fc",
    "elapsedTime": 0,
    "updated": "2020-01-08T21:47:46.865Z",
    "client": "API",
    "userId": "{USER_ID}",
    "created": "2020-01-08T21:47:46.865Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "GET"
        },
        "soft_delete": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"soft_delete\"}"
        },
        "cancel": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\"}"
        }
    }
}
```

>[!NOTE]
>
>You can use the value of `_links.cancel` to [cancel your created query](#cancel-a-query).

### Abfrage abbrechen

You can request to delete a specified query by making a PATCH request to the `/queries` endpoint and providing the query&#39;s `id` value in the request path.

**API-Format**

```http
PATCH /queries/{QUERY_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{QUERY_ID}` | The `id` value of the query you want to cancel. |


**Anfrage**

Diese API-Anfrage nutzt für die Payload die JSON Patch-Syntax. Weiterführende Informationen zur Funktionsweise von JSON Patch finden Sie im Dokument zu den API-Grundlagen.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json',
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
   "op": "cancel"  
 }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `op` | Um die Abfrage abzubrechen, müssen Sie den Parameter op mit dem Wert festlegen `cancel `. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 202 (Akzeptiert) mit der folgenden Meldung zurück:

```json
{
    "message": "Query cancel request received",
    "statusCode": 202
}
```
