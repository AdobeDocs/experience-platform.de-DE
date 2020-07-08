---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Entwicklerhandbuch für Abfrage Service
topic: scheduled queries
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 3%

---


# Geplante Abfragen

## Beispiel-API-Aufrufe

Nachdem Sie wissen, welche Header verwendet werden sollen, können Sie mit dem Aufrufen der Abfrage Service API beginnen. In den folgenden Abschnitten werden die verschiedenen API-Aufrufe erläutert, die Sie mit der Abfrage Service API durchführen können. Jeder Aufruf enthält das allgemeine API-Format, eine Musteranforderung mit den erforderlichen Kopfzeilen und eine Beispielantwort.

### Liste der geplanten Abfragen abrufen

Sie können eine Liste aller geplanten Abfragen für Ihre IMS-Organisation abrufen, indem Sie eine GET-Anforderung an den `/schedules` Endpunkt senden.

**API-Format**

```http
GET /schedules
GET /schedules?{QUERY_PARAMETERS}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Optional*) Dem Anforderungspfad hinzugefügte Parameter, die die in der Antwort zurückgegebenen Ergebnisse konfigurieren. Es können mehrere Parameter eingeschlossen werden, die durch das kaufmännische Und (`&`) voneinander getrennt werden. Die verfügbaren Parameter sind unten aufgeführt. |

**Abfrage**

Im Folgenden finden Sie eine Liste der verfügbaren Abfrage-Parameter für die Auflistung geplanter Abfragen. Alle diese Parameter sind optional. Wenn Sie diesen Endpunkt ohne Parameter aufrufen, werden alle für Ihr Unternehmen verfügbaren geplanten Abfragen abgerufen.

| Parameter | Beschreibung |
| --------- | ----------- |
| `orderby` | Gibt das Feld an, in dem die Ergebnisse sortiert werden sollen. Die unterstützten Felder sind `created` und `updated`. Die Ergebnisse `orderby=created` werden beispielsweise in aufsteigender Reihenfolge sortiert. Durch Hinzufügen eines `-` vor dem Erstellen (`orderby=-created`) werden Elemente in absteigender Reihenfolge sortiert. |
| `limit` | Gibt die maximale Seitengröße an, um die Anzahl der Ergebnisse zu steuern, die in einer Seite enthalten sind. (*Default value: 20*) |
| `start` | Verschiebt die Liste der Antwort mit einer nullbasierten Nummerierung. Beispielsweise `start=2` gibt eine Liste ab der dritten aufgelisteten Abfrage zurück. (*Default value: 0*) |
| `property` | Filtern Sie die Ergebnisse nach Feldern. Die Filter **müssen** HTML-Escape-Zeichen sein. Kommas werden verwendet, um mehrere Filter zu kombinieren. Die unterstützten Felder sind `created`, `templateId`und `userId`. Die Liste der unterstützten Operatoren ist `>` (größer als), `<` (kleiner als) und `==` (gleich). Gibt beispielsweise alle geplanten Abfragen zurück, bei denen die Benutzer-ID wie angegeben angegeben ist. `userId==6ebd9c2d-494d-425a-aa91-24033f3abeec` |

**Anfrage**

Mit der folgenden Anforderung wird die neueste geplante Abfrage abgerufen, die für Ihr IMS-Unternehmen erstellt wurde.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit einer Liste geplanter Abfragen für die angegebene IMS-Organisation zurück. Die folgende Antwort gibt die neueste geplante Abfrage zurück, die für Ihr IMS-Unternehmen erstellt wurde.

```json
{
    "schedules": [
        {
            "state": "ENABLED",
            "query": {
                "dbName": "prod:all",
                "sql": "SELECT * FROM accounts;",
                "name": "Sample Scheduled Query",
                "description": "A sample of a scheduled query."
            },
            "updatedUserId": "{USER_ID}",
            "version": 2,
            "id": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "updated": "1578523458919",
            "schedule": {
                "schedule": "30 * * * *",
                "startDate": "2020-01-08T12:30:00.000Z",
                "maxActiveRuns": 1
            },
            "userId": "{USER_ID}",
            "created": "1578523458919",
            "_links": {
                "enable": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "PATCH",
                    "body": "{ \"op\": \"enable\" }"
                },
                "runs": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
                    "method": "GET"
                },
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "DELETE"
                },
                "disable": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "PATCH",
                    "body": "{ \"op\": \"disable\" }"
                },
                "trigger": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
                    "method": "POST"
                }
            }
        }
    ],
    "_page": {
        "orderby": "+created",
        "start": "2020-01-08T22:44:18.919Z",
        "count": 1
    },
    "_links": {},
    "version": 2
}
```

### Neue geplante Abfrage erstellen

Sie können eine neue geplante Abfrage erstellen, indem Sie eine POST-Anforderung an den `/schedules` Endpunkt senden.

**API-Format**

```http
POST /schedules
```

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
     "query": {
         "dbName": "prod:all",
         "sql": "SELECT * FROM accounts;",
         "name": "Sample Scheduled Query",
         "description": "A sample of a scheduled query."
     }, 
     "schedule": {
         "schedule": "30 * * * *",
         "startDate": "2020-01-08T12:30:00.000Z"
     }
 }
 '
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `query.dbName` | Der Datenbankname, für den Sie eine geplante Abfrage erstellen. |
| `query.sql` | Die SQL-Abfrage, die Sie erstellen möchten. |
| `query.name` | Der Name der geplanten Abfrage. |
| `schedule.schedule` | Der Cron-Zeitplan für die Abfrage. Weitere Informationen zu Cron-Zeitplänen finden Sie in der Dokumentation zum [Cron-Ausdruck](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) . In diesem Beispiel bedeutet &quot;30 * * * *&quot;, dass die Abfrage stündlich mit 30 Minuten ausgeführt wird. |
| `schedule.startDate` | Das Datum des Beginns für Ihre geplante Abfrage, geschrieben als UTC-Zeitstempel. |

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 202 (Akzeptiert) mit Details zu Ihrer neu erstellten geplanten Abfrage zurück. Nach der Aktivierung der geplanten Abfrage ändert sich die `state` Einstellung von `REGISTERING` zu `ENABLED`.

```json
{
    "state": "REGISTERING",
    "query": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Scheduled Query",
        "description": "A sample of a scheduled query."
    },
    "updatedUserId": "{USER_ID}",
    "version": 2,
    "id": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
    "schedule": {
        "schedule": "30 * * * *",
        "startDate": "2020-01-08T12:30:00.000Z",
        "maxActiveRuns": 1
    },
    "userId": "{USER_ID}",
    "_links": {
        "enable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"enable\" }"
        },
        "runs": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "GET"
        },
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "DELETE"
        },
        "disable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"disable\" }"
        },
        "trigger": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "POST"
        }
    }
}
```

>[!NOTE]
>
>Sie können den Wert von verwenden, `_links.delete` um Ihre erstellte geplante Abfrage [zu](#delete-a-specified-scheduled-query)löschen.

### Details zu einer bestimmten geplanten Abfrage anfordern

Sie können Informationen zu einer bestimmten geplanten Abfrage abrufen, indem Sie eine GET-Anforderung an den `/schedules` Endpunkt senden und dessen ID im Anforderungspfad angeben.

**API-Format**

```http
GET /schedules/{SCHEDULE_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Der `id` Wert der geplanten Abfrage, die Sie abrufen möchten. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit Details zur angegebenen geplanten Abfrage zurück.

```json
{
    "state": "ENABLED",
    "query": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Scheduled Query",
        "description": "A sample of a scheduled query."
    },
    "updatedUserId": "{USER_ID}",
    "version": 2,
    "id": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
    "updated": "1578523458919",
    "schedule": {
        "schedule": "30 * * * *",
        "startDate": "2020-01-08T12:30:00.000Z",
        "maxActiveRuns": 1
    },
    "userId": "{USER_ID}",
    "created": "1578523458919",
    "_links": {
        "enable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"enable\" }"
        },
        "runs": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "GET"
        },
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "DELETE"
        },
        "disable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"disable\" }"
        },
        "trigger": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "POST"
        }
    }
}
```

>[!NOTE]
>
>Sie können den Wert von verwenden, `_links.delete` um Ihre erstellte geplante Abfrage [zu](#delete-a-specified-scheduled-query)löschen.

### Details zu einer bestimmten geplanten Abfrage aktualisieren

Sie können die Details einer bestimmten geplanten Abfrage aktualisieren, indem Sie eine PATCH-Anforderung an den `/schedules` Endpunkt senden und dessen ID im Anforderungspfad angeben.

Die PATCH-Anforderung unterstützt zwei verschiedene Pfade: `/state` und `/schedule/schedule`.

### Status der geplanten Abfrage aktualisieren

Sie können den Status der ausgewählten geplanten Abfrage aktualisieren - AKTIVIERT oder DEAKTIVIERT. `/state` Um den Status zu aktualisieren, müssen Sie den Wert als `enable` oder `disable`festlegen.

**API-Format**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Der `id` Wert der geplanten Abfrage, die Sie abrufen möchten. |


**Anfrage**

Diese API-Anforderung verwendet die JSON Patch-Syntax für die Nutzlast. Weitere Informationen zur Funktionsweise von JSON Patch finden Sie im Dokument API-Grundlagen.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
     "body": [
         {
             "op": "replace",
             "path": "/state",
             "value": "disable"
         }
     ]
 }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `path` | Der Pfad des Werts, den Sie patchen möchten. In diesem Fall müssen Sie, da Sie den Status der geplanten Abfrage aktualisieren, den Wert `path` auf `/state`setzen. |
| `value` | Der aktualisierte Wert der `/state`. Dieser Wert kann entweder als `enable` oder `disable` zur Aktivierung oder Deaktivierung der geplanten Abfrage eingestellt werden. |

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 202 (Akzeptiert) mit der folgenden Meldung zurück.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Zeitplan für geplante Abfragen aktualisieren

Sie können den Cron-Zeitplan der geplanten Abfrage `/schedule/schedule` aktualisieren. Weitere Informationen zu Cron-Zeitplänen finden Sie in der Dokumentation zum [Cron-Ausdruck](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) .

**API-Format**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Der `id` Wert der geplanten Abfrage, die Sie abrufen möchten. |

**Anfrage**

Diese API-Anforderung verwendet die JSON Patch-Syntax für die Nutzlast. Weitere Informationen zur Funktionsweise von JSON Patch finden Sie im Dokument API-Grundlagen.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
     "body": [
         {
             "op": "replace",
             "path": "/schedule/schedule",
             "value": "45 * * * *"
         }
     ]
 }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `path` | Der Pfad des Werts, den Sie patchen möchten. In diesem Fall müssen Sie, da Sie den Zeitplan der geplanten Abfrage aktualisieren, den Wert `path` auf `/schedule/schedule`einstellen. |
| `value` | Der aktualisierte Wert der `/schedule`. Dieser Wert muss in Form eines Cron-Plans vorliegen. In diesem Beispiel wird die geplante Abfrage stündlich mit 45 Minuten ausgeführt. |

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 202 (Akzeptiert) mit der folgenden Meldung zurück.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Eine angegebene geplante Abfrage löschen

Sie können eine angegebene geplante Abfrage löschen, indem Sie eine DELETE-Anforderung an den `/schedules` Endpunkt senden und die ID der geplanten Abfrage angeben, die Sie im Anforderungspfad löschen möchten.

>[!NOTE]
>
>Der Zeitplan **muss** vor dem Löschen deaktiviert werden.

**API-Format**

```http
DELETE /schedules/{SCHEDULE_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Der `id` Wert der geplanten Abfrage, die Sie abrufen möchten. |

**Anfrage**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 202 (Akzeptiert) mit der folgenden Meldung zurück.

```json
{
    "message": "Schedule deleted successfully",
    "statusCode": 202
}
```
