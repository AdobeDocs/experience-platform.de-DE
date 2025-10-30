---
keywords: Experience Platform;Startseite;beliebte Themen;Abfrage-Service;API-Handbuch;Abfragen;Abfrage;Abfrage-Service;
solution: Experience Platform
title: API-Endpunkt für Abfragen
description: In den folgenden Abschnitten werden Aufrufe beschrieben, die Sie mit dem /queries-Endpunkt in der Abfrage-Service-API ausführen können.
role: Developer
exl-id: d6273e82-ce9d-4132-8f2b-f376c6712882
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 20%

---

# Abfrageendpunkt

## Beispiel für API-Aufrufe

In den folgenden Abschnitten werden Aufrufe beschrieben, die Sie mit dem `/queries`-Endpunkt in der [!DNL Query Service]-API ausführen können. Jeder Aufruf enthält das allgemeine API-Format, eine Beispielanfrage mit den erforderlichen Kopfzeilen und eine Beispielantwort.

### Abrufen einer Liste von Abfragen

Sie können eine Liste aller Abfragen für Ihr Unternehmen abrufen, indem Sie eine GET-Anfrage an den `/queries`-Endpunkt senden.

**API-Format**

```http
GET /queries
GET /queries?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`: (*Optional*) Dem Anfragepfad hinzugefügte Parameter, die die in der Antwort zurückgegebenen Ergebnisse konfigurieren. Es können mehrere Parameter eingeschlossen werden, die durch kaufmännische Und-Zeichen (`&`) voneinander getrennt werden. Die verfügbaren Parameter sind unten aufgeführt.

**Abfrageparameter**

Im Folgenden finden Sie eine Liste der verfügbaren Abfrageparameter für die Auflistung von Abfragen. Alle diese Parameter sind optional. Wenn Sie diesen Endpunkt ohne Parameter aufrufen, werden alle für Ihre Organisation verfügbaren Abfragen abgerufen.

| Parameter | Beschreibung |
| --------- | ----------- |
| `orderby` | Gibt das Feld an, nach dem Ergebnisse sortiert werden sollen. Die unterstützten Felder sind `created` und `updated`. `orderby=created` zum Beispiel sortiert Ergebnisse in aufsteigender Reihenfolge. Durch Hinzufügen eines `-`-Zeichens vor „created“ (`orderby=-created`) werden Elemente nach der Erstellung in absteigender Reihenfolge sortiert. |
| `limit` | Gibt die maximale Seitengröße an, um die Anzahl der Ergebnisse zu steuern, die auf einer Seite enthalten sind. (*Standardwert: 20*) |
| `start` | Geben Sie einen Zeitstempel im ISO-Format an, um die Ergebnisse zu sortieren. Wenn kein Startdatum angegeben wird, gibt der API-Aufruf zuerst die älteste erstellte Abfrage zurück und listet dann weiterhin neuere Ergebnisse auf.<br> ISO-Zeitstempel ermöglichen verschiedene Granularitätsstufen in Datum und Uhrzeit. Die grundlegenden ISO-Zeitstempel haben das Format: `2020-09-07`, um das Datum 7. September 2020 auszudrücken. Ein komplexeres Beispiel würde als `2022-11-05T08:15:30-05:00` geschrieben und entspricht dem 5. November 2022, 8:15:30 Uhr, US Eastern Standard Time. Eine Zeitzone kann mit einem UTC-Offset versehen werden und wird durch das Suffix „Z“ (`2020-01-01T01:01:01Z`) gekennzeichnet. Wenn keine Zeitzone angegeben wird, wird standardmäßig null verwendet. |
| `property` | Filtern Sie Ergebnisse nach Feldern. Die Filter **müssen** mit HTML-Escape-Zeichen versehen sein. Kommas dienen dazu, mehrere Filter zu kombinieren. Die unterstützten Felder sind `created`, `updated`, `state` und `id`. Die Liste der unterstützten Operatoren ist `>` (größer als), `<` (kleiner als), `>=` (größer oder gleich), `<=` (kleiner oder gleich), `==` (gleich), `!=` (ungleich) und `~` (enthält). Beispielsweise gibt `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` alle Abfragen mit der angegebenen ID zurück. |
| `excludeSoftDeleted` | Gibt an, ob eine Abfrage, die vorläufig gelöscht wurde, einbezogen werden soll. `excludeSoftDeleted=false` werden beispielsweise Abfragen **einschließen** vorläufig gelöschte Abfragen. (*Boolesch, Standardwert: true*) |
| `excludeHidden` | Gibt an, ob nicht benutzergesteuerte Abfragen angezeigt werden sollen. Wenn dieser Wert auf „false“ gesetzt **,** nicht benutzergesteuerte Abfragen wie CURSOR-Definitionen, FETCH oder Metadatenabfragen. (*Boolesch, Standardwert: true*) |
| `isPrevLink` | Der `isPrevLink` Abfrageparameter wird für die Paginierung verwendet. Die Ergebnisse des API-Aufrufs werden anhand ihres `created` Zeitstempels und der `orderby`-Eigenschaft sortiert. Beim Navigieren durch die Ergebnisseiten wird `isPrevLink` auf „true“ gesetzt, wenn rückwärts gepaggt wird. Dadurch wird die Reihenfolge der Abfrage umgekehrt. Siehe die Links „Weiter“ und „Zurück“ als Beispiele. |

**Anfrage**

Mit der folgenden Anfrage wird die neueste für Ihre Organisation erstellte Abfrage abgerufen.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries?limit=1 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status-Code 200 mit einer Liste von Abfragen für die angegebene Organisation als JSON zurück. Die folgende Antwort gibt die neueste Abfrage zurück, die für Ihre Organisation erstellt wurde.

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

### Erstellen einer Abfrage

Sie können eine neue Abfrage erstellen, indem Sie eine POST-Anfrage an den `/queries`-Endpunkt senden.

**API-Format**

```http
POST /queries
```

**Anfrage**

Die folgende Anfrage erstellt eine neue Abfrage mit einer SQL-Anweisung in der Payload:

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/queries \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
        "dbName": "prod:all",
        "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
        "queryParameters": {
            user_id : {USER_ID}
            }
        "name": "Sample Query",
        "description": "Sample Description"
    }  
```

Im folgenden Anfragebeispiel wird eine neue Abfrage mit einer vorhandenen Abfragevorlagen-ID erstellt.

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/queries \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
        "dbName": "prod:all",
        "templateID": "f7cb5155-29da-4b95-8131-8c5deadfbe7f",
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
| `queryParameters` | Ein Schlüssel-Wert-Paar, das alle parametrisierten Werte in der SQL-Anweisung ersetzt. Dies ist nur erforderlich **wenn** Parameterersetzungen innerhalb der von Ihnen angegebenen SQL verwenden. Für diese Schlüssel-Wert-Paare wird keine Überprüfung des Werttyps durchgeführt. |
| `templateId` | Die eindeutige Kennung für eine bereits vorhandene Abfrage. Sie können dies anstelle einer SQL-Anweisung bereitstellen. |
| `insertIntoParameters` | (Optional) Wenn diese Eigenschaft definiert ist, wird diese Abfrage in eine INSERT INTO-Abfrage konvertiert. |
| `ctasParameters` | (Optional) Wenn diese Eigenschaft definiert ist, wird diese Abfrage in eine CTAS-Abfrage konvertiert. |

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 202 (Akzeptiert) mit Details zur neu erstellten Abfrage zurückgegeben. Sobald die Abfrage aktiviert wurde und erfolgreich ausgeführt wurde, ändert sich die `state` von `SUBMITTED` in `SUCCESS`.

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
>Sie können den Wert von `_links.cancel` verwenden, um [erstellte Abfrage abzubrechen](#cancel-a-query).

### Abfrage nach ID abrufen

Sie können detaillierte Informationen zu einer bestimmten Abfrage abrufen, indem Sie eine GET-Anfrage an den `/queries`-Endpunkt senden und den `id` der Abfrage im Anfragepfad angeben.

**API-Format**

```http
GET /queries/{QUERY_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{QUERY_ID}` | Der `id` der Abfrage, die Sie abrufen möchten. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status-Code 200 mit detaillierten Informationen zur angegebenen Abfrage zurück.

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
>Sie können den Wert von `_links.cancel` verwenden, um [erstellte Abfrage abzubrechen](#cancel-a-query).

### Abfrage abbrechen oder vorläufig löschen

Sie können einen Abbruch oder ein Soft Delete für eine bestimmte Abfrage anfordern, indem Sie eine PATCH-Anfrage an den `/queries`-Endpunkt senden und den `id` der Abfrage im Anfragepfad angeben.

**API-Format**

```http
PATCH /queries/{QUERY_ID}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{QUERY_ID}` | Der `id` der Abfrage, für die Sie den Vorgang ausführen möchten. |


**Anfrage**

Diese API-Anfrage nutzt für die Payload die JSON Patch-Syntax. Weiterführende Informationen zur Funktionsweise von JSON Patch finden Sie im Dokument zu den API-Grundlagen.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json',
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
   "op": "cancel"  
 }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `op` | Der Typ des Vorgangs, der mit der Ressource durchgeführt werden soll. Die zulässigen Werte sind `cancel` und `soft_delete`. Um die Abfrage abzubrechen, müssen Sie den Parameter op mit dem Wert `cancel` festlegen. Beachten Sie, dass der Soft Delete-Vorgang verhindert, dass die Abfrage bei GET-Anfragen zurückgegeben wird, sie jedoch nicht aus dem System löscht. |

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 202 (Akzeptiert) mit der folgenden Meldung zurückgegeben:

```json
{
    "message": "Query cancel request received",
    "statusCode": 202
}
```
