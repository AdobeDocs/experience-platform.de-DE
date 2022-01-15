---
keywords: Experience Platform; Startseite; beliebte Themen; Abfragedienst; Query Service; geplante Abfragen; geplante Abfrage;
solution: Experience Platform
title: API-Endpunkt für geplante Abfragen
topic-legacy: scheduled queries
description: In den folgenden Abschnitten werden die verschiedenen API-Aufrufe erläutert, die Sie für geplante Abfragen mit der Query Service-API ausführen können.
exl-id: f57dbda5-da50-4812-a924-c8571349f1cd
source-git-commit: f1b982e5f788282a8cf2a9c4523370c520b82d0e
workflow-type: tm+mt
source-wordcount: '1113'
ht-degree: 35%

---

# Endpunkt für geplante Abfragen

## Beispiel-API-Aufrufe

Nachdem Sie nun wissen, welche Header verwendet werden sollen, können Sie mit den Aufrufen an die [!DNL Query Service] API. In den folgenden Abschnitten werden die verschiedenen API-Aufrufe erläutert, die Sie mithilfe der [!DNL Query Service] API. Jeder Aufruf enthält das allgemeine API-Format, eine Beispielanfrage mit den erforderlichen Kopfzeilen und eine Beispielantwort.

### Liste geplanter Abfragen abrufen

Sie können eine Liste aller geplanten Abfragen für Ihre IMS-Organisation abrufen, indem Sie eine GET-Anfrage an die `/schedules` -Endpunkt.

**API-Format**

```http
GET /schedules
GET /schedules?{QUERY_PARAMETERS}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Optional*) Dem Anfragepfad hinzugefügte Parameter, die die in der Antwort zurückgegebenen Ergebnisse konfigurieren. Es können mehrere Parameter eingeschlossen werden, die durch kaufmännische Und-Zeichen (`&`) voneinander getrennt werden. Die verfügbaren Parameter sind unten aufgeführt. |

**Abfrageparameter**

Im Folgenden finden Sie eine Liste der verfügbaren Abfrageparameter für die Auflistung geplanter Abfragen. Alle diese Parameter sind optional. Wenn Sie diesen Endpunkt ohne Parameter aufrufen, werden alle für Ihre Organisation verfügbaren geplanten Abfragen abgerufen.

| Parameter | Beschreibung |
| --------- | ----------- |
| `orderby` | Gibt das Feld an, nach dem Ergebnisse sortiert werden sollen. Die unterstützten Felder sind `created` und `updated`. `orderby=created` zum Beispiel sortiert Ergebnisse in aufsteigender Reihenfolge. Durch Hinzufügen eines `-`-Zeichens vor „created“ (`orderby=-created`) werden Elemente nach der Erstellung in absteigender Reihenfolge sortiert. |
| `limit` | Gibt die maximale Seitengröße an, um die Anzahl der Ergebnisse zu steuern, die auf einer Seite enthalten sind. (*Standardwert: 20*) |
| `start` | Versetzt die Antwortliste mit einer nullbasierten Nummerierung. Beispielsweise gibt `start=2` eine Liste zurück, die bei der dritten aufgelisteten Abfrage beginnt. (*Standardwert: 0*) |
| `property` | Filtern Sie Ergebnisse nach Feldern. Die Filter **müssen** mit HTML-Escape-Zeichen versehen sein. Kommas dienen dazu, mehrere Filter zu kombinieren. Unterstützte Felder sind `created`, `templateId` und `userId`. Die Liste der unterstützten Operatoren finden Sie unter `>` (größer als), `<` (kleiner als) und `==` (gleich). Beispiel: `userId==6ebd9c2d-494d-425a-aa91-24033f3abeec` gibt alle geplanten Abfragen zurück, bei denen die Benutzer-ID wie angegeben ist. |

**Anfrage**

Mit der folgenden Anfrage wird die neueste geplante Abfrage abgerufen, die für Ihre IMS-Organisation erstellt wurde.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit einer Liste geplanter Abfragen für die angegebene IMS-Organisation zurück. Die folgende Antwort gibt die neueste geplante Abfrage zurück, die für Ihre IMS-Organisation erstellt wurde.

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

Sie können eine neue geplante Abfrage erstellen, indem Sie eine POST-Anfrage an die `/schedules` -Endpunkt. Wenn Sie eine geplante Abfrage in der API erstellen, wird sie auch im Abfrage-Editor angezeigt. Weitere Informationen zu geplanten Abfragen in der Benutzeroberfläche finden Sie im Abschnitt [Dokumentation zum Abfrage-Editor](../ui/user-guide.md#scheduled-queries).

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
| `query.dbName` | Der Name der Datenbank, für die Sie eine geplante Abfrage erstellen. |
| `query.sql` | Die SQL-Abfrage, die Sie erstellen möchten. |
| `query.name` | Der Name der geplanten Abfrage. |
| `schedule.schedule` | Der Cron-Zeitplan für die Abfrage. Weitere Informationen zu Cron-Zeitplänen finden Sie in der Dokumentation zum [Format von Cron-Ausdrücken](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html). In diesem Beispiel bedeutet &quot;30 * * * *&quot;, dass die Abfrage stündlich mit der 30-Minuten-Markierung ausgeführt wird.<br><br>Alternativ können Sie die folgenden Kurzausdrücke verwenden:<ul><li>`@once`: Die Abfrage wird nur einmal ausgeführt.</li><li>`@hourly`: Die Abfrage wird stündlich zu Beginn der Stunde ausgeführt. Dies entspricht dem Cron-Ausdruck `0 * * * *`.</li><li>`@daily`: Die Abfrage wird einmal täglich um Mitternacht ausgeführt. Dies entspricht dem Cron-Ausdruck `0 0 * * *`.</li><li>`@weekly`: Die Abfrage läuft einmal pro Woche, am Sonntag um Mitternacht. Dies entspricht dem Cron-Ausdruck `0 0 * * 0`.</li><li>`@monthly`: Die Abfrage wird einmal im Monat am ersten Tag des Monats um Mitternacht ausgeführt. Dies entspricht dem Cron-Ausdruck `0 0 1 * *`.</li><li>`@yearly`: Die Abfrage wird einmal jährlich am 1. Januar um Mitternacht ausgeführt. Dies entspricht dem Cron-Ausdruck `1 0 0 1 1 *`. |
| `schedule.startDate` | Das Startdatum für Ihre geplante Abfrage, geschrieben als UTC-Zeitstempel. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 202 (Akzeptiert) mit Details zu Ihrer neu erstellten geplanten Abfrage zurück. Sobald die geplante Abfrage aktiviert wurde, wird die `state` ändert sich von `REGISTERING` nach `ENABLED`.

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
>Sie können den Wert von `_links.delete` nach [Löschen der erstellten geplanten Abfrage](#delete-a-specified-scheduled-query).

### Anforderungsdetails einer angegebenen geplanten Abfrage

Sie können Informationen zu einer bestimmten geplanten Abfrage abrufen, indem Sie eine GET-Anfrage an die `/schedules` -Endpunkt und geben die Kennung im Anfragepfad ein.

**API-Format**

```http
GET /schedules/{SCHEDULE_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Der `id`-Wert der geplanten Abfrage, die Sie abrufen möchten. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zur angegebenen geplanten Abfrage zurück.

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
>Sie können den Wert von `_links.delete` nach [Löschen der erstellten geplanten Abfrage](#delete-a-specified-scheduled-query).

### Aktualisieren der Details einer angegebenen geplanten Abfrage

Sie können die Details für eine bestimmte geplante Abfrage aktualisieren, indem Sie eine PATCH-Anfrage an die `/schedules` -Endpunkt und durch Angabe seiner ID im Anfragepfad.

Für die PATCH-Anfrage werden zwei Pfade unterstützt: `/state` und `/schedule/schedule`.

### Aktualisierung des geplanten Abfragestatus

Sie können `/state` um den Status der ausgewählten geplanten Abfrage zu aktualisieren - AKTIVIERT oder DEAKTIVIERT. Geben Sie zur Aktualisierung des Status den Wert `enable` oder `disable` an.

**API-Format**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Die `id` -Wert der geplanten Abfrage, die Sie PATCH möchten. |


**Anfrage**

Diese API-Anfrage nutzt für die Payload die JSON Patch-Syntax. Weiterführende Informationen zur Funktionsweise von JSON Patch finden Sie im Dokument zu den API-Grundlagen.

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
| `path` | Der Pfad des Werts, den Sie ändern möchten. Da Sie in diesem Fall den Status der geplanten Abfrage aktualisieren, müssen Sie den Wert von `path` nach `/state`. |
| `value` | Der aktualisierte Wert von `/state`. Dieser Wert kann entweder als `enable` oder `disable` , um die geplante Abfrage zu aktivieren oder zu deaktivieren. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 202 (Akzeptiert) mit der folgenden Meldung zurück.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Geplanten Abfragezeitplan aktualisieren

Sie können `/schedule/schedule` , um den Cron-Zeitplan der geplanten Abfrage zu aktualisieren. Weitere Informationen zu Cron-Zeitplänen finden Sie in der Dokumentation zum [Format von Cron-Ausdrücken](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html).

**API-Format**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Die `id` -Wert der geplanten Abfrage, die Sie PATCH möchten. |

**Anfrage**

Diese API-Anfrage nutzt für die Payload die JSON Patch-Syntax. Weiterführende Informationen zur Funktionsweise von JSON Patch finden Sie im Dokument zu den API-Grundlagen.

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
| `path` | Der Pfad des Werts, den Sie ändern möchten. Da Sie in diesem Fall den Zeitplan der geplanten Abfrage aktualisieren, müssen Sie den Wert von `path` nach `/schedule/schedule`. |
| `value` | Der aktualisierte Wert von `/schedule`. Dieser Wert muss in Form eines Cron-Zeitplans angegeben werden. In diesem Beispiel wird die geplante Abfrage also stündlich mit der 45-Minuten-Markierung ausgeführt. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 202 (Akzeptiert) mit der folgenden Meldung zurück.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Bestimmte geplante Abfrage löschen

Sie können eine bestimmte geplante Abfrage löschen, indem Sie eine DELETE-Anfrage an die `/schedules` -Endpunkt und geben Sie die Kennung der geplanten Abfrage an, die Sie im Anfragepfad löschen möchten.

>[!NOTE]
>
>Zeitplan **must** vor dem Löschen deaktiviert werden.

**API-Format**

```http
DELETE /schedules/{SCHEDULE_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Die `id` -Wert der geplanten Abfrage, die Sie DELETE möchten. |

**Anfrage**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 202 (Akzeptiert) mit der folgenden Meldung zurück.

```json
{
    "message": "Schedule deleted successfully",
    "statusCode": 202
}
```
