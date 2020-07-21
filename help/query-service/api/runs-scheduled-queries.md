---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Entwicklerhandbuch für Query Service
topic: runs for scheduled queries
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 94%

---


# Ausführungen für geplante Abfragen

## Beispiel-API-Aufrufe

Now that you understand what headers to use, you are ready to begin making calls to the [!DNL Query Service] API. The following sections walk through the various API calls you can make using the [!DNL Query Service] API. Jeder Aufruf enthält das allgemeine API-Format, eine Musteranfrage mit den erforderlichen Kopfzeilen und eine Beispielantwort.

### Liste aller ausgeführten Vorgänge für eine bestimmte geplante Abfrage abrufen

Sie können für eine bestimmte geplante Abfrage eine Liste aller ausgeführten Vorgänge abrufen, unabhängig davon, ob diese aktuell ausgeführt werden oder bereits abgeschlossen wurden. Dies ist durch eine GET-Anfrage an den `/schedules/{SCHEDULE_ID}/runs`-Endpunkt möglich, wobei `{SCHEDULE_ID}` der `id`-Wert der geplanten Abfrage ist, deren Ausführungen Sie abrufen möchten.

**API-Format**

```http
GET /schedules/{SCHEDULE_ID}/runs
GET /schedules/{SCHEDULE_ID}/runs?{QUERY_PARAMETERS}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Der `id`-Wert der geplanten Abfrage, die Sie abrufen möchten. |
| `{QUERY_PARAMETERS}` | (*Optional*) Dem Anfragepfad hinzugefügte Parameter, die die in der Antwort zurückgegebenen Ergebnisse konfigurieren. Es können mehrere Parameter eingeschlossen werden, getrennt durch das kaufmännische Und-Zeichen (`&`). Die verfügbaren Parameter sind unten aufgeführt. |

**Abfrage**

Im Folgenden finden Sie eine Liste der verfügbaren Abfrageparameter für die Auflistung der Ausführungen einer angegebenen geplanten Abfrage. Alle diese Parameter sind optional. Wenn Sie diesen Endpunkt ohne Parameter aufrufen, werden alle für die angegebene geplante Abfrage verfügbaren Ausführungen abgerufen.

| Parameter | Beschreibung |
| --------- | ----------- |
| `orderby` | Gibt das Feld an, nach dem Ergebnisse sortiert werden sollen. Unterstützte Felder sind `created` und `updated`. `orderby=created` beispielsweise wird Ergebnisse in aufsteigender Reihenfolge sortieren. Durch Hinzufügen eines `-`-Zeichens vor „created“ (`orderby=-created`) werden Elemente in absteigender Reihenfolge sortiert. |
| `limit` | Gibt die Seitengrößenbeschränkung an, um die Anzahl der Ergebnisse zu steuern, die auf einer Seite enthalten sind. (*Standardwert: 20*) |
| `start` | Versetzt die Antwortliste mit einer nullbasierten Nummerierung. Beispielsweise gibt `start=2` eine Liste ab der dritten aufgeführten Abfrage zurück. (*Standardwert: 0*) |
| `property` | Filtern Sie Ergebnisse anhand von Feldern. Die Filter **müssen** HTML-Escape-Zeichen aufweisen. Kommas dienen dazu, um mehrere Filter zu kombinieren. Unterstützte Felder sind `created`, `state` und `externalTrigger`. Die Liste der unterstützten Operatoren umfasst `>` (größer als), `<` (kleiner als), `==` (gleich) und `!=` (ungleich). Beispielsweise gibt `externalTrigger==true,state==SUCCESS,created>2019-04-20T13:37:00Z` alle manuell erstellten, erfolgreichen und nach dem 20. April 2019 erstellten Ausführungen zurück. |

**Anfrage**

Mit der folgenden Anfrage werden für die angegebene geplante Abfrage die letzten vier Ausführungen abgerufen.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs?limit=4
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort wird für die angegebene geplante Abfrage der HTTP-Status 200 mit einer Liste der Ausführungen als JSON zurückgegeben. Folgende Antwort gibt die letzten vier Ausführungen für die angegebene geplante Abfrage zurück.

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
>Sie können den Wert von `_links.cancel` nutzen, um [eine Ausführung für eine bestimmte geplante Abfrage zu stoppen](#immediately-stop-a-run-for-a-specific-scheduled-query).

### Sofort eine Ausführung für eine bestimmte geplante Abfrage auslösen

Sie können eine Ausführung für eine angegebene geplante Abfrage sofort auslösen, indem Sie eine POST-Anfrage an den `/schedules/{SCHEDULE_ID}/runs`-Endpunkt senden, wobei `{SCHEDULE_ID}` der `id`-Wert der geplanten Abfrage ist, deren Ausführung Sie auslösen möchten.

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

Eine erfolgreiche Antwort gibt den HTTP-Status 202 (Akzeptiert) mit der folgenden Meldung zurück.

```json
{
    "message": "Request to trigger run of a scheduled query accepted.",
    "statusCode": 202
}
```

### Details zu einer Ausführung für eine bestimmte geplante Abfrage abrufen

Sie können Details über die Ausführung für eine bestimmte geplante Abfrage abrufen, indem Sie eine GET-Anfrage an den `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}`-Endpunkt senden und sowohl die Kennung der geplanten Abfrage als auch die Ausführung im Anfragepfad angeben.

**API-Format**

```http
GET /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Der `id`-Wert der geplanten Abfrage, für deren Ausführung Sie Details abrufen möchten. |
| `{RUN_ID}` | Der `id`-Wert der Ausführung, die Sie abrufen möchten. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zur angegebenen Ausführung zurück.

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

### Ausführung für eine bestimmte geplante Abfrage sofort anhalten

Sie können eine Ausführung für eine bestimmte geplante Abfrage sofort anhalten, indem Sie eine PATCH-Anfrage an den `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}`-Endpunkt senden und sowohl die Kennung der geplanten Abfrage als auch die Ausführung im Anfragepfad angeben.

**API-Format**

```http
PATCH /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Der `id`-Wert der geplanten Abfrage, für deren Ausführung Sie Details abrufen möchten. |
| `{RUN_ID}` | Der `id`-Wert der Ausführung, die Sie abrufen möchten. |

**Anfrage**

Diese API-Anfrage nutzt für die Payload die JSON Patch-Syntax. Weiterführende Informationen zur Funktionsweise von JSON Patch finden Sie im Dokument zu den API-Grundlagen.

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

Eine erfolgreiche Antwort gibt den HTTP-Status 202 (Akzeptiert) mit der folgenden Meldung zurück.

```json
{
    "message": "Request to cancel run of a scheduled query accepted",
    "statusCode": 202
}
```
