---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Entwicklerhandbuch für Abfrage Service
topic: query templates
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 3%

---


# Abfrage-Vorlagen

## Beispiel-API-Aufrufe

Nachdem Sie wissen, welche Header verwendet werden sollen, können Sie mit dem Aufrufen der Abfrage Service API beginnen. In den folgenden Abschnitten werden die verschiedenen API-Aufrufe erläutert, die Sie mit der Abfrage Service API durchführen können. Jeder Aufruf enthält das allgemeine API-Format, eine Musteranforderung mit den erforderlichen Kopfzeilen und eine Beispielantwort.

### Abrufen einer Liste von Vorlagen für Abfragen

Sie können eine Liste aller Vorlagen für Abfragen für Ihre IMS-Organisation abrufen, indem Sie eine GET-Anforderung an den `/query-templates` Endpunkt senden.

**API-Format**

```http
GET /query-templates
GET /query-templates?{QUERY_PARAMETERS}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Optional*) Dem Anforderungspfad hinzugefügte Parameter, die die in der Antwort zurückgegebenen Ergebnisse konfigurieren. Es können mehrere Parameter eingeschlossen werden, die durch das kaufmännische Und (`&`) voneinander getrennt werden. Die verfügbaren Parameter sind unten aufgeführt. |

**Abfrage**

Im Folgenden finden Sie eine Liste der verfügbaren Abfragen zur Auflistung von Vorlagen für Abfragen. Alle diese Parameter sind optional. Wenn Sie diesen Endpunkt ohne Parameter aufrufen, werden alle für Ihr Unternehmen verfügbaren Vorlagen zur Abfrage abgerufen.

| Parameter | Beschreibung |
| --------- | ----------- |
| `orderby` | Gibt das Feld an, in dem die Ergebnisse sortiert werden sollen. Die unterstützten Felder sind `created` und `updated`. Die Ergebnisse `orderby=created` werden beispielsweise in aufsteigender Reihenfolge sortiert. Durch Hinzufügen eines `-` vor dem Erstellen (`orderby=-created`) werden Elemente in absteigender Reihenfolge sortiert. |
| `limit` | Gibt die maximale Seitengröße an, um die Anzahl der Ergebnisse zu steuern, die in einer Seite enthalten sind. (*Default value: 20*) |
| `start` | Verschiebt die Liste der Antwort mit einer nullbasierten Nummerierung. Beispielsweise `start=2` gibt eine Liste ab der dritten aufgelisteten Abfrage zurück. (*Default value: 0*) |
| `property` | Filtern Sie die Ergebnisse nach Feldern. Die Filter **müssen** HTML-Escape-Zeichen sein. Kommas werden verwendet, um mehrere Filter zu kombinieren. Die unterstützten Felder sind `name` und `userId`. Der einzige unterstützte Operator ist `==` (gleich). Beispielsweise `name==my_template` werden alle Abfragen-Vorlagen mit dem Namen zurückgegeben `my_template`. |

**Anfrage**

Mit der folgenden Anforderung wird die neueste Vorlage für die Abfrage abgerufen, die für Ihr IMS-Unternehmen erstellt wurde.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit einer Liste von Abfragen-Vorlagen für die angegebene IMS-Organisation zurück. Die folgende Antwort gibt die neueste Vorlage für die Abfrage zurück, die für Ihr IMS-Unternehmen erstellt wurde.

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
                    "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
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

>[!NOTE] Sie können den Wert von verwenden, `_links.delete` um die Vorlage [Ihrer Abfrage zu](#delete-a-specified-query-template)löschen.

### Erstellen einer Vorlage für eine Abfrage

Sie können eine Vorlage für die Abfrage erstellen, indem Sie eine POST-Anforderung an den `/query-templates` Endpunkt senden.

**API-Format**

```http
POST /query-templates
```

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/query-templates
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "sql": "SELECT * FROM accounts;",
        "name": "Sample query template"
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `sql` | Die SQL-Abfrage, die Sie erstellen möchten. |
| `name` | Der Name der Vorlage &quot;Abfrage&quot;. |

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 202 (Akzeptiert) mit Details zur neu erstellten Vorlage für die Abfrage zurück.

```json
{
    "sql": "SELECT * FROM accounts;",
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
            "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
        }
    }
}
```

>[!NOTE] Sie können den Wert von verwenden, `_links.delete` um die Vorlage [Ihrer Abfrage zu](#delete-a-specified-query-template)löschen.

### Abrufen einer angegebenen Vorlage für Abfragen

Sie können eine bestimmte Vorlage für die Abfrage abrufen, indem Sie eine GET-Anforderung an den `/query-templates/{TEMPLATE_ID}` Endpunkt senden und die ID der Vorlage für die Abfrage im Anforderungspfad angeben.

**API-Format**

```http
GET /query-templates/{TEMPLATE_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- | 
| `{TEMPLATE_ID}` | Der `id` Wert der Abfrage-Vorlage, die Sie abrufen möchten. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit Details zur Vorlage der angegebenen Abfrage zurück.

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
            "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
        }
    }
}
```

>[!NOTE] Sie können den Wert von verwenden, `_links.delete` um die Vorlage [Ihrer Abfrage zu](#delete-a-specified-query-template)löschen.

### Aktualisieren einer bestimmten Vorlage für eine Abfrage

Sie können eine bestimmte Vorlage für Abfragen aktualisieren, indem Sie eine PUT-Anforderung an den `/query-templates/{TEMPLATE_ID}` Endpunkt senden und die ID der Vorlage für die Abfrage im Anforderungspfad angeben.

**API-Format**

```http
PUT /query-templates/{TEMPLATE_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{TEMPLATE_ID}` | Der `id` Wert der Abfrage-Vorlage, die Sie abrufen möchten. |

**Anfrage**

>[!NOTE] Für die PUT-Anforderung müssen sowohl das Feld &quot;sql&quot;als auch das Feld &quot;name&quot;ausgefüllt werden. Der aktuelle Inhalt dieser Abfrage-Vorlage wird **überschrieben** .

```shell
curl -X PUT https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "sql": "SELECT * FROM accounts LIMIT 20;",
    "name": "Sample query template"
 }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `sql` | Die SQL-Abfrage, die Sie aktualisieren möchten. |
| `name` | Der Name der geplanten Abfrage. |

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 202 (Akzeptiert) mit den aktualisierten Informationen für die Vorlage der angegebenen Abfrage zurück.

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
            "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
        }
    }
}
```

>[!NOTE] Sie können den Wert von verwenden, `_links.delete` um die Vorlage [Ihrer Abfrage zu](#delete-a-specified-query-template)löschen.

### Eine angegebene Vorlage für eine Abfrage löschen

Sie können eine bestimmte Vorlage für Abfragen löschen, indem Sie eine DELETE-Anforderung an die Adresse senden `/query-templates/{TEMPLATE_ID}` und die ID der Vorlage für die Abfrage im Anforderungspfad angeben.

**API-Format**

```http
DELETE /query-templates/{TEMPLATE_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{TEMPLATE_ID}` | Der `id` Wert der Abfrage-Vorlage, die Sie abrufen möchten. |

**Anfrage**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 202 (Akzeptiert) mit der folgenden Meldung zurück.

```json
{
    "message": "Deleted",
    "statusCode": 202
}
```
