---
keywords: Experience Platform; Startseite; beliebte Themen; Query Service; API-Handbuch; Abfragen; Abfrage; Query Service
solution: Experience Platform
title: Query API Endpoint
topic-legacy: queries
description: In den folgenden Abschnitten werden die Aufrufe erläutert, die Sie mithilfe des /queries -Endpunkts in der Query Service-API ausführen können.
exl-id: d6273e82-ce9d-4132-8f2b-f376c6712882
source-git-commit: 536c2998f7d320dec0cb392465677dd30c8ea622
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 32%

---

# Abfrage-Endpunkt

## Beispiel-API-Aufrufe

In den folgenden Abschnitten werden die Aufrufe erläutert, die Sie mithilfe des Endpunkts `/queries` in der API [!DNL Query Service] tätigen können. Jeder Aufruf enthält das allgemeine API-Format, eine Beispielanfrage mit den erforderlichen Kopfzeilen und eine Beispielantwort.

### Abrufen einer Abfrageliste

Sie können eine Liste aller Abfragen für Ihre IMS-Organisation abrufen, indem Sie eine GET-Anfrage an den Endpunkt `/queries` stellen.

**API-Format**

```http
GET /queries
GET /queries?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`: (*Optional*) Dem Anfragepfad hinzugefügte Parameter, die die in der Antwort zurückgegebenen Ergebnisse konfigurieren. Es können mehrere Parameter eingeschlossen werden, die durch kaufmännische Und-Zeichen (`&`) voneinander getrennt werden. Die verfügbaren Parameter sind unten aufgeführt.

**Abfrageparameter**

Im Folgenden finden Sie eine Liste der verfügbaren Abfrageparameter zur Auflistung von Abfragen. Alle diese Parameter sind optional. Wenn Sie diesen Endpunkt ohne Parameter aufrufen, werden alle für Ihre Organisation verfügbaren Abfragen abgerufen.

| Parameter | Beschreibung |
| --------- | ----------- |
| `orderby` | Gibt das Feld an, nach dem Ergebnisse sortiert werden sollen. Die unterstützten Felder sind `created` und `updated`. `orderby=created` zum Beispiel sortiert Ergebnisse in aufsteigender Reihenfolge. Durch Hinzufügen eines `-`-Zeichens vor „created“ (`orderby=-created`) werden Elemente nach der Erstellung in absteigender Reihenfolge sortiert. |
| `limit` | Gibt die maximale Seitengröße an, um die Anzahl der Ergebnisse zu steuern, die auf einer Seite enthalten sind. (*Standardwert: 20*) |
| `start` | Versetzt die Antwortliste mit einer nullbasierten Nummerierung. Beispielsweise gibt `start=2` eine Liste zurück, die bei der dritten aufgelisteten Abfrage beginnt. (*Standardwert: 0*) |
| `property` | Filtern Sie Ergebnisse nach Feldern. Die Filter **müssen** mit HTML-Escape-Zeichen versehen sein. Kommas dienen dazu, mehrere Filter zu kombinieren. Die unterstützten Felder sind `created`, `updated`, `state` und `id`. Die Liste der unterstützten Operatoren ist `>` (größer als), `<` (kleiner als), `>=` (größer oder gleich), `<=` (kleiner oder gleich), `==` (gleich), `!=` (nicht gleich) und `~` (enthält). `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` gibt beispielsweise alle Abfragen mit der angegebenen ID zurück. |
| `excludeSoftDeleted` | Gibt an, ob eine Abfrage einbezogen werden soll, bei der eine weiche Löschung vorgenommen wurde. Zum Beispiel `excludeSoftDeleted=false` enthält **die** weichen gelöschten Abfragen. (*Boolesch, Standardwert: true*) |
| `excludeHidden` | Gibt an, ob benutzergesteuerte Abfragen angezeigt werden sollen. Wenn dieser Wert auf &quot;false&quot;gesetzt ist, enthält **auch** nicht vom Benutzer gesteuerte Abfragen wie CURSOR-Definitionen, FETCH- oder Metadaten-Abfragen. (*Boolesch, Standardwert: true*) |

**Anfrage**

Mit der folgenden Anfrage wird die neueste für Ihre IMS-Organisation erstellte Abfrage abgerufen.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries?limit=1 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit einer Liste von Abfragen für die angegebene IMS-Organisation als JSON zurück. Die folgende Antwort gibt die neueste für Ihre IMS-Organisation erstellte Abfrage zurück.

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

### Abfragen erstellen

Sie können eine neue Abfrage erstellen, indem Sie eine POST-Anfrage an den Endpunkt `/queries` senden.

**API-Format**

```http
POST /queries
```

**Anfrage**

Die folgende Anfrage erstellt eine neue Abfrage, die durch die in der Payload angegebenen Werte konfiguriert wird:

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
        "name": "Sample Query",
        "description": "Sample Description"
    }  
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `dbName` | Der Name der Datenbank, für die Sie eine SQL-Abfrage erstellen. |
| `sql` | Die SQL-Abfrage, die Sie erstellen möchten. |
| `name` | Der Name Ihrer SQL-Abfrage. |
| `description` | Die Beschreibung Ihrer SQL-Abfrage. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 202 (Akzeptiert) mit Details zu Ihrer neu erstellten Abfrage zurück. Nachdem die Abfrage aktiviert wurde und erfolgreich ausgeführt wurde, ändert sich `state` von `SUBMITTED` in `SUCCESS`.

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
>Sie können den Wert von `_links.cancel` bis [Ihre erstellte Abfrage abbrechen](#cancel-a-query).

### Abfrage nach ID abrufen

Sie können detaillierte Informationen zu einer bestimmten Abfrage abrufen, indem Sie eine GET-Anfrage an den Endpunkt `/queries` senden und im Anfragepfad den Wert `id` der Abfrage angeben.

**API-Format**

```http
GET /queries/{QUERY_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{QUERY_ID}` | Der `id` -Wert der Abfrage, die Sie abrufen möchten. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit detaillierten Informationen zur angegebenen Abfrage zurück.

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
>Sie können den Wert von `_links.cancel` bis [Ihre erstellte Abfrage abbrechen](#cancel-a-query).

### Abbrechen einer Abfrage

Sie können das Löschen einer bestimmten Abfrage anfordern, indem Sie eine PATCH-Anfrage an den Endpunkt `/queries` senden und im Anfragepfad den Wert `id` der Abfrage angeben.

**API-Format**

```http
PATCH /queries/{QUERY_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{QUERY_ID}` | Der `id` -Wert der Abfrage, die Sie abbrechen möchten. |


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
| `op` | Um die Abfrage abzubrechen, müssen Sie den Parameter op mit dem Wert `cancel ` festlegen. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 202 (Akzeptiert) mit der folgenden Meldung zurück:

```json
{
    "message": "Query cancel request received",
    "statusCode": 202
}
```
