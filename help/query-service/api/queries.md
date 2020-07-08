---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Entwicklerhandbuch für Abfrage Service
topic: queries
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 2%

---


# Abfragen

## Beispiel-API-Aufrufe

In den folgenden Abschnitten werden die Aufrufe erläutert, die Sie mithilfe des `/queries` Endpunkts in der Abfrage Service API durchführen können. Jeder Aufruf enthält das allgemeine API-Format, eine Musteranforderung mit den erforderlichen Kopfzeilen und eine Beispielantwort.

### Eine Liste von Abfragen abrufen

Sie können eine Liste aller Abfragen für Ihre IMS-Organisation abrufen, indem Sie eine GET-Anforderung an den `/queries` Endpunkt senden.

**API-Format**

```http
GET /queries
GET /queries?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`: (*Optional*) Dem Anforderungspfad hinzugefügte Parameter, die die in der Antwort zurückgegebenen Ergebnisse konfigurieren. Es können mehrere Parameter eingeschlossen werden, die durch das kaufmännische Und (`&`) voneinander getrennt werden. Die verfügbaren Parameter sind unten aufgeführt.

**Abfrage**

Im Folgenden finden Sie eine Liste der verfügbaren Abfragen für die Auflistung von Abfragen. Alle diese Parameter sind optional. Wenn Sie diesen Endpunkt ohne Parameter aufrufen, werden alle für Ihr Unternehmen verfügbaren Abfragen abgerufen.

| Parameter | Beschreibung |
| --------- | ----------- |
| `orderby` | Gibt das Feld an, in dem die Ergebnisse sortiert werden sollen. Die unterstützten Felder sind `created` und `updated`. Die Ergebnisse `orderby=created` werden beispielsweise in aufsteigender Reihenfolge sortiert. Durch Hinzufügen eines `-` vor dem Erstellen (`orderby=-created`) werden Elemente in absteigender Reihenfolge sortiert. |
| `limit` | Gibt die maximale Seitengröße an, um die Anzahl der Ergebnisse zu steuern, die in einer Seite enthalten sind. (*Default value: 20*) |
| `start` | Verschiebt die Liste der Antwort mit einer nullbasierten Nummerierung. Beispielsweise `start=2` gibt eine Liste ab der dritten aufgelisteten Abfrage zurück. (*Default value: 0*) |
| `property` | Filtern Sie die Ergebnisse nach Feldern. Die Filter **müssen** HTML-Escape-Zeichen sein. Kommas werden verwendet, um mehrere Filter zu kombinieren. Die unterstützten Felder sind `created`, `updated`, `state`und `id`. Die Liste der unterstützten Operatoren ist `>` (größer als), `<` (kleiner als), `>=` (größer gleich), `<=` (kleiner gleich), `==` (gleich), `!=` (nicht gleich) und `~` (enthält). Gibt beispielsweise alle Abfragen mit der angegebenen ID zurück. `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` |
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

Sie können eine neue Abfrage erstellen, indem Sie eine POST-Anforderung an den `/queries` Endpunkt senden.

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
>Mit dem Wert von können Sie Ihre erstellte Abfrage `_links.cancel`[abbrechen](#cancel-a-query).

### Abrufen einer Abfrage nach ID

Sie können detaillierte Informationen zu einer bestimmten Abfrage abrufen, indem Sie eine GET-Anforderung an den `/queries` Endpunkt senden und den `id` Wert der Abfrage im Anforderungspfad angeben.

**API-Format**

```http
GET /queries/{QUERY_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{QUERY_ID}` | Der `id` Wert der Abfrage, die Sie abrufen möchten. |

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
>Mit dem Wert von können Sie Ihre erstellte Abfrage `_links.cancel`[abbrechen](#cancel-a-query).

### Abfrage abbrechen

Sie können das Löschen einer bestimmten Abfrage anfordern, indem Sie eine PATCH-Anforderung an den `/queries` Endpunkt senden und den `id` Wert der Abfrage im Anforderungspfad angeben.

**API-Format**

```http
PATCH /queries/{QUERY_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{QUERY_ID}` | Der `id` Wert der Abfrage, die Sie abbrechen möchten. |


**Anfrage**

Diese API-Anforderung verwendet die JSON Patch-Syntax für die Nutzlast. Weitere Informationen zur Funktionsweise von JSON Patch finden Sie im Dokument API-Grundlagen.

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

Bei einer erfolgreichen Antwort wird der HTTP-Status 202 (Akzeptiert) mit der folgenden Meldung zurückgegeben:

```json
{
    "message": "Query cancel request received",
    "statusCode": 202
}
```
