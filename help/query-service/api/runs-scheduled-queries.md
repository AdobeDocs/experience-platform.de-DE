---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Entwicklerhandbuch für Abfrage Service
topic: runs for scheduled queries
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 2%

---


# Wird für geplante Abfragen ausgeführt

## Beispiel-API-Aufrufe

Nachdem Sie wissen, welche Header verwendet werden sollen, können Sie mit dem Aufrufen der Abfrage Service API beginnen. In den folgenden Abschnitten werden die verschiedenen API-Aufrufe erläutert, die Sie mit der Abfrage Service API durchführen können. Jeder Aufruf enthält das allgemeine API-Format, eine Musteranforderung mit den erforderlichen Kopfzeilen und eine Beispielantwort.

### Eine Liste aller ausgeführten Vorgänge für eine bestimmte geplante Abfrage abrufen

Sie können eine Liste aller ausgeführten Vorgänge für eine bestimmte geplante Abfrage abrufen, unabhängig davon, ob sie aktuell ausgeführt werden oder bereits abgeschlossen sind. Dies geschieht durch eine GET-Anforderung an den `/schedules/{SCHEDULE_ID}/runs` Endpunkt, wobei `{SCHEDULE_ID}` der `id` Wert der geplanten Abfrage, deren Ausführung Sie abrufen möchten, ist.

**API-Format**

```http
GET /schedules/{SCHEDULE_ID}/runs
GET /schedules/{SCHEDULE_ID}/runs?{QUERY_PARAMETERS}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Der `id` Wert der geplanten Abfrage, die Sie abrufen möchten. |
| `{QUERY_PARAMETERS}` | (*Optional*) Dem Anforderungspfad hinzugefügte Parameter, die die in der Antwort zurückgegebenen Ergebnisse konfigurieren. Es können mehrere Parameter eingeschlossen werden, die durch das kaufmännische Und (`&`) voneinander getrennt werden. Die verfügbaren Parameter sind unten aufgeführt. |

**Abfrage**

Im Folgenden finden Sie eine Liste der verfügbaren Abfrage-Parameter für die Auflistung der Ausführung für eine angegebene geplante Abfrage. Alle diese Parameter sind optional. Wenn Sie diesen Endpunkt ohne Parameter aufrufen, werden alle für die angegebene geplante Abfrage verfügbaren Vorgänge abgerufen.

| Parameter | Beschreibung |
| --------- | ----------- |
| `orderby` | Gibt das Feld an, in dem die Ergebnisse sortiert werden sollen. Die unterstützten Felder sind `created` und `updated`. Die Ergebnisse `orderby=created` werden beispielsweise in aufsteigender Reihenfolge sortiert. Durch Hinzufügen eines `-` vor dem Erstellen (`orderby=-created`) werden Elemente in absteigender Reihenfolge sortiert. |
| `limit` | Gibt die maximale Seitengröße an, um die Anzahl der Ergebnisse zu steuern, die in einer Seite enthalten sind. (*Default value: 20*) |
| `start` | Verschiebt die Liste der Antwort mit einer nullbasierten Nummerierung. Beispielsweise `start=2` gibt eine Liste ab der dritten aufgelisteten Abfrage zurück. (*Default value: 0*) |
| `property` | Filtern Sie die Ergebnisse nach Feldern. Die Filter **müssen** HTML-Escape-Zeichen sein. Kommas werden verwendet, um mehrere Filter zu kombinieren. Die unterstützten Felder sind `created`, `state`und `externalTrigger`. Die Liste der unterstützten Operatoren ist `>` (größer als), `<` (kleiner als), `==` (gleich) und `!=` (nicht gleich). Beispielsweise `externalTrigger==true,state==SUCCESS,created>2019-04-20T13:37:00Z` werden alle nach dem 20. April 2019 manuell erstellten, erfolgreichen und erstellten Vorgänge zurückgegeben. |

**Anfrage**

Mit der folgenden Anforderung werden die letzten vier Ausführungen für die angegebene geplante Abfrage abgerufen.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs?limit=4
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort wird HTTP-Status 200 mit einer Liste der Ausführung für die angegebene geplante Abfrage als JSON zurückgegeben. Die folgende Antwort gibt die letzten vier Ausführungen für die angegebene geplante Abfrage zurück.

```json
{
    "runsSchedules": [
        {
            "state": "SUCCESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEyOjMwOjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T12:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEyOjMwOjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEyOjMwOjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        },
        {
            "state": "SUCCESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEzOjMwOjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T13:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEzOjMwOjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEzOjMwOjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        },
        {
            "state": "SUCCESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE0OjMwOjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T14:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE0OjMwOjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE0OjMwOjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        },
        {
            "state": "IN_PROGRESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE4OjQ1OjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T15:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE4OjQ1OjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE4OjQ1OjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        }
    ],
    "_page": {
        "orderby": "+created",
        "start": "2020-01-08T12:30:00Z",
        "count": 4
    },
    "_links": {},
    "version": 1
}
```

>[!NOTE]
>
>Sie können den Wert von verwenden, `_links.cancel` um eine Ausführung für eine bestimmte geplante Abfrage [zu](#immediately-stop-a-run-for-a-specific-scheduled-query)stoppen.

### Sofort einen Run für eine bestimmte geplante Abfrage auslösen

Sie können einen Run für eine angegebene geplante Abfrage sofort auslösen, indem Sie eine POST-Anforderung an den `/schedules/{SCHEDULE_ID}/runs` Endpunkt senden, wobei `{SCHEDULE_ID}` der `id` Wert der geplanten Abfrage ist, deren Ausführung Sie auslösen möchten.

**API-Format**

```http
POST /schedules/{SCHEDULE_ID}/runs
```

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 202 (Akzeptiert) mit der folgenden Meldung zurück.

```json
{
    "message": "Request to trigger run of a scheduled query accepted.",
    "statusCode": 202
}
```

### Abrufen von Details zu einer Ausführung für eine bestimmte geplante Abfrage

Sie können Details zu einer Ausführung für eine bestimmte geplante Abfrage abrufen, indem Sie eine GET-Anforderung an den `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` Endpunkt senden und sowohl die ID der geplanten Abfrage als auch die Ausführung im Anforderungspfad angeben.

**API-Format**

```http
GET /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Der `id` Wert der geplanten Abfrage, deren Ausführung Sie Details abrufen möchten. |
| `{RUN_ID}` | Der `id` Wert der Ausführung, die Sie abrufen möchten. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit Details zum angegebenen Ausführen zurück.

```json
{
    "state": "success",
    "taskStatusList": [
        {
            "duration": 303,
            "endDate": "2020-01-08T23:49:02.346318",
            "state": "SUCCESS",
            "message": "Processed Successfully",
            "startDate": "2020-01-08T23:43:58.936269",
            "taskId": "7Omob151BM"
        }
    ],
    "version": 1,
    "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw",
    "scheduleId": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
    "externalTrigger": "false",
    "created": "2020-01-08T20:45:00",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw",
            "method": "GET"
        },
        "cancel": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\" }"
        }
    }
}
```

### Beenden Sie einen Run für eine bestimmte geplante Abfrage sofort

Sie können einen Run für eine bestimmte geplante Abfrage sofort beenden, indem Sie eine PATCH-Anforderung an den `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` Endpunkt senden und sowohl die ID der geplanten Abfrage als auch die Ausführung im Anforderungspfad angeben.

**API-Format**

```http
PATCH /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Der `id` Wert der geplanten Abfrage, deren Ausführung Sie Details abrufen möchten. |
| `{RUN_ID}` | Der `id` Wert der Ausführung, die Sie abrufen möchten. |

**Anfrage**

Diese API-Anforderung verwendet die JSON Patch-Syntax für die Nutzlast. Weitere Informationen zur Funktionsweise von JSON Patch finden Sie im Dokument API-Grundlagen.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
     "op": "cancel"
 }'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 202 (Akzeptiert) mit der folgenden Meldung zurück.

```json
{
    "message": "Request to cancel run of a scheduled query accepted",
    "statusCode": 202
}
```
