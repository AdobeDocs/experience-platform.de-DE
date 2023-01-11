---
keywords: Experience Platform; Startseite; beliebte Themen; Abfragedienst; Abfragevorlagen; API-Handbuch; Vorlagen; Query Service
solution: Experience Platform
title: API-Endpunkt für Abfragevorlagen
description: In diesem Handbuch werden die verschiedenen API-Aufrufe für Abfragevorlagen beschrieben, die Sie mit der Query Service-API ausführen können.
exl-id: 14cd7907-73d2-478f-8992-da3bdf08eacc
source-git-commit: ee6a54aeba4ddfeb98ee5e11283c299f00969a53
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 65%

---

# Endpunkt &quot;Abfragevorlagen&quot;

## Beispiel-API-Aufrufe

In den folgenden Abschnitten werden die verschiedenen API-Aufrufe beschrieben, die Sie mithilfe der [!DNL Query Service] API. Jeder Aufruf enthält das allgemeine API-Format, eine Beispielanfrage mit den erforderlichen Kopfzeilen und eine Beispielantwort.

Siehe [Dokumentation zu Benutzeroberflächenabfragevorlagen](../ui/query-templates.md) für Informationen zum Erstellen von Vorlagen über die Experience Platform-Benutzeroberfläche.

### Liste von Abfragevorlagen abrufen

Sie können eine Liste aller Abfragevorlagen für Ihre IMS-Organisation abrufen, indem Sie eine GET-Anfrage an den `/query-templates`-Endpunkt senden.

**API-Format**

```http
GET /query-templates
GET /query-templates?{QUERY_PARAMETERS}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Optional*) Dem Anfragepfad hinzugefügte Parameter, die die in der Antwort zurückgegebenen Ergebnisse konfigurieren. Es können mehrere Parameter eingeschlossen werden, die durch kaufmännische Und-Zeichen (`&`) voneinander getrennt werden. Die verfügbaren Parameter sind unten aufgeführt. |

**Abfrageparameter**

Im Folgenden finden Sie eine Liste der verfügbaren Abfrageparameter zum Auflisten von Abfragevorlagen. Alle diese Parameter sind optional. Wenn Sie diesen Endpunkt ohne Parameter aufrufen, werden alle für Ihre Organisation verfügbaren Abfragevorlagen abgerufen.

| Parameter | Beschreibung |
| --------- | ----------- |
| `orderby` | Gibt das Feld an, nach dem Ergebnisse sortiert werden sollen. Die unterstützten Felder sind `created` und `updated`. `orderby=created` zum Beispiel sortiert Ergebnisse in aufsteigender Reihenfolge. Durch Hinzufügen eines `-`-Zeichens vor „created“ (`orderby=-created`) werden Elemente nach der Erstellung in absteigender Reihenfolge sortiert. |
| `limit` | Gibt die maximale Seitengröße an, um die Anzahl der Ergebnisse zu steuern, die auf einer Seite enthalten sind. (*Standardwert: 20*) |
| `start` | Versetzt die Antwortliste mit einer nullbasierten Nummerierung. Beispielsweise gibt `start=2` eine Liste zurück, die bei der dritten aufgelisteten Abfrage beginnt. (*Standardwert: 0*) |
| `property` | Filtern Sie Ergebnisse nach Feldern. Die Filter **müssen** mit HTML-Escape-Zeichen versehen sein. Kommas dienen dazu, mehrere Filter zu kombinieren. Die unterstützten Felder sind `name` und `userId`. Der einzige unterstützte Operator ist `==` (gleich). Beispielsweise gibt `name==my_template` alle Abfragevorlagen mit dem Namen `my_template` zurück. |

**Anfrage**

Mit der folgenden Anfrage wird die neueste Abfragevorlage abgerufen, die für Ihre IMS-Organisation erstellt wurde.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit einer Liste von Abfragevorlagen für die angegebene IMS-Organisation zurück. Die folgende Antwort gibt die neueste Abfragevorlage zurück, die für Ihre IMS-Organisation erstellt wurde.

```json
{
    "templates": [
        {
            "sql": "SELECT *\nFROM\n  accounts\nLIMIT 10\n",
            "name": "Test",
            "id": "f7cb5155-29da-4b95-8131-8c5deadfbe7f",
            "updated": "2019-11-21T21:50:01.469Z",
            "userId": "{USER_ID}",
            "created": "2019-11-21T21:50:01.469Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/query-templates/f7cb5155-29da-4b95-8131-8c5deadfbe7f",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/query-templates/f7cb5155-29da-4b95-8131-8c5deadfbe7f",
                    "method": "DELETE"
                },
                "update": {
                    "href": "https://platform.adobe.io/data/foundation/query/query-templates/f7cb5155-29da-4b95-8131-8c5deadfbe7f",
                    "method": "PUT",
                    "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
                }
            }
        }
    ],
    "_page": {
        "orderby": "-created",
        "start": "2019-11-21T21:50:01.469Z",
        "next": "2019-11-21T21:50:01.469Z",
        "count": 1
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates?orderby=-created&start=2019-11-21T21:50:01.469Z"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates?orderby=-created&start=2019-11-21T21:50:01.469Z&isPrevLink=true"
        }
    },
    "version": 1
}
```

>[!NOTE]
>
>Sie können den Wert von `_links.delete` verwenden, um [Ihre Abfragevorlage zu löschen](#delete-a-specified-query-template).

### Abfragevorlage erstellen

Sie können eine Abfragevorlage erstellen, indem Sie eine POST-Anfrage an den `/query-templates`-Endpunkt senden.

**API-Format**

```http
POST /query-templates
```

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/query-templates
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
        "name": "Sample query template",
        "queryParameters": {
            user_id : {USER_ID}
            }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `sql` | Die SQL-Abfrage, die Sie erstellen möchten. Sie können entweder Standard-SQL oder eine Parameterersetzung verwenden. Um einen Parameteraustausch in der SQL zu verwenden, müssen Sie dem Parameterschlüssel eine `$`. Beispiel: `$key`und geben Sie die Parameter an, die in SQL als JSON-Schlüsselwertpaare im `queryParameters` -Feld. Die hier übergebenen Werte sind die Standardparameter, die in der Vorlage verwendet werden. Wenn Sie diese Parameter überschreiben möchten, müssen Sie sie in der POST-Anfrage überschreiben. |
| `name` | Der Name der Abfragevorlage. |
| `queryParameters` | Eine Schlüsselwertpaarung zum Ersetzen von parametrisierten Werten in der SQL-Anweisung. Dies ist nur erforderlich **if** Sie verwenden Parameterersetzungen innerhalb der von Ihnen bereitgestellten SQL. An diesen Schlüsselwertpaaren wird keine Wertüberprüfung durchgeführt. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 202 (Akzeptiert) mit Details zur neu erstellten Abfragevorlage zurück.

```json
{
    "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
    "name": "Sample query template",
    "id": "0094d000-9062-4e6a-8fdb-05606805f08f",
    "updated": "2020-01-09T00:20:09.670Z",
    "userId": "{USER_ID}",
    "created": "2020-01-09T00:20:09.670Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "DELETE"
        },
        "update": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "PUT",
            "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>Sie können den Wert von `_links.delete` verwenden, um [Ihre Abfragevorlage zu löschen](#delete-a-specified-query-template).

### Bestimmte Abfragevorlage abrufen

Sie können eine bestimmte Abfragevorlage abrufen, indem Sie eine GET-Anfrage an den `/query-templates/{TEMPLATE_ID}`-Endpunkt senden und im Anfragepfad die Kennung der Abfragevorlage angeben.

**API-Format**

```http
GET /query-templates/{TEMPLATE_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- | 
| `{TEMPLATE_ID}` | Der `id`-Wert der Abfragevorlage, die Sie abrufen möchten. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zur angegebenen Abfragevorlage zurück.

```json
{
    "sql": "SELECT * FROM accounts;",
    "name": "Sample query template",
    "id": "0094d000-9062-4e6a-8fdb-05606805f08f",
    "updated": "2020-01-09T00:20:09.670Z",
    "userId": "A5A562D15E1645480A495CE1@techacct.adobe.com",
    "created": "2020-01-09T00:20:09.670Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "DELETE"
        },
        "update": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "PUT",
            "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>Sie können den Wert von `_links.delete` verwenden, um [Ihre Abfragevorlage zu löschen](#delete-a-specified-query-template).

### Bestimmte Abfragevorlage aktualisieren

Sie können eine bestimmte Abfragevorlage aktualisieren, indem Sie eine PUT-Anfrage an den `/query-templates/{TEMPLATE_ID}`-Endpunkt senden und im Anfragepfad die Kennung der Abfragevorlage angeben.

**API-Format**

```http
PUT /query-templates/{TEMPLATE_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{TEMPLATE_ID}` | Der `id`-Wert der Abfragevorlage, die Sie abrufen möchten. |

**Anfrage**

>[!NOTE]
>
>Für die PUT-Anfrage müssen Sie sowohl das Feld „sql“ als auch das Feld „name“ ausfüllen. Dadurch wird der aktuelle Inhalt dieser Abfragevorlage **überschrieben**.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
    "name": "Sample query template",
    "queryParameters": {
            user_id : {USER_ID}
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `sql` | Die SQL-Abfrage, die Sie erstellen möchten. Sie können entweder Standard-SQL oder eine Parameterersetzung verwenden. Um einen Parameteraustausch in der SQL zu verwenden, müssen Sie dem Parameterschlüssel eine `$`. Beispiel: `$key`und geben Sie die Parameter an, die in SQL als JSON-Schlüsselwertpaare im `queryParameters` -Feld. Die hier übergebenen Werte sind die Standardparameter, die in der Vorlage verwendet werden. Wenn Sie diese Parameter überschreiben möchten, müssen Sie sie in der POST-Anfrage überschreiben. |
| `name` | Der Name der Abfragevorlage. |
| `queryParameters` | Eine Schlüsselwertpaarung zum Ersetzen von parametrisierten Werten in der SQL-Anweisung. Dies ist nur erforderlich **if** Sie verwenden Parameterersetzungen innerhalb der von Ihnen bereitgestellten SQL. An diesen Schlüsselwertpaaren wird keine Wertüberprüfung durchgeführt. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 202 (Akzeptiert) mit den aktualisierten Daten zur angegebenen Abfragevorlage zurück.

```json
{
    "sql": "SELECT * FROM accounts LIMIT 20;",
    "name": "Sample query template",
    "id": "0094d000-9062-4e6a-8fdb-05606805f08f",
    "updated": "2020-01-09T00:29:20.028Z",
    "lastUpdatedBy": "{USER_ID}",
    "userId": "{USER_ID}",
    "created": "2020-01-09T00:20:09.670Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/query_templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/query_templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "DELETE"
        },
        "update": {
            "href": "https://platform.adobe.io/data/foundation/query/query_templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "PUT",
            "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>Sie können den Wert von `_links.delete` verwenden, um [Ihre Abfragevorlage zu löschen](#delete-a-specified-query-template).

### Bestimmte Abfragevorlage löschen

Sie können eine bestimmte Abfragevorlage löschen, indem Sie eine DELETE-Anfrage an `/query-templates/{TEMPLATE_ID}` senden und im Anfragepfad die Kennung der Abfragevorlage angeben.

**API-Format**

```http
DELETE /query-templates/{TEMPLATE_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{TEMPLATE_ID}` | Der `id`-Wert der Abfragevorlage, die Sie abrufen möchten. |

**Anfrage**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 202 (Akzeptiert) mit der folgenden Meldung zurück.

```json
{
    "message": "Deleted",
    "statusCode": 202
}
```
