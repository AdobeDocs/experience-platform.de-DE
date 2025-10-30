---
keywords: Experience Platform;Startseite;beliebte Themen;Abfrage-Service;Abfrage-Service;geplante Abfragen;geplante Abfrage;
solution: Experience Platform
title: Zeitpläne-Endpunkt
description: In den folgenden Abschnitten werden die verschiedenen API-Aufrufe beschrieben, die Sie für geplante Abfragen mit der Abfrage-Service-API ausführen können.
role: Developer
exl-id: f57dbda5-da50-4812-a924-c8571349f1cd
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1409'
ht-degree: 23%

---

# Zeitpläne-Endpunkt

Erfahren Sie mit detaillierten Informationen und Beispielen, wie Sie geplante Abfragen programmgesteuert mithilfe der Abfrage-Service-Zeitpläne-API erstellen, verwalten und überwachen.

## Anforderungen und Voraussetzungen

Sie können geplante Abfragen entweder mit einem technischen Konto (authentifiziert über OAuth Server-zu-Server-Anmeldeinformationen) oder einem persönlichen Benutzerkonto (Benutzer-Token) erstellen. Adobe empfiehlt jedoch dringend die Verwendung eines technischen Kontos, um die unterbrechungsfreie, sichere Ausführung geplanter Abfragen sicherzustellen - insbesondere für Langzeit- oder Produktionsarbeitslasten.

Mit einem persönlichen Benutzerkonto erstellte Abfragen schlagen fehl, wenn der Zugriff dieses Benutzers widerrufen oder sein Konto deaktiviert wird. Technische Konten bieten mehr Stabilität, da sie nicht an den Beschäftigungsstatus oder die Zugriffsrechte eines einzelnen Benutzers gebunden sind.

>[!IMPORTANT]
>
>Wichtige Überlegungen beim Verwalten geplanter Abfragen:<ul><li>Geplante Abfragen schlagen fehl, wenn das Konto (technisch oder benutzerseitig), mit dem sie erstellt wurden, Zugriff oder Berechtigungen verliert.</li><li>Geplante Abfragen müssen vor dem Löschen über die API oder die Benutzeroberfläche deaktiviert werden.</li><li>Eine Planung auf unbestimmte Zeit ohne Enddatum wird nicht unterstützt; ein Enddatum muss immer angegeben werden.</li></ul>

Ausführliche Anleitungen zu Kontoanforderungen, zur Einrichtung von Berechtigungen und zur Verwaltung geplanter Abfragen finden Sie in der [Dokumentation zu Abfragezeitplänen](../ui/query-schedules.md#technical-account-user-requirements). Schrittweise Anweisungen zum Erstellen und Konfigurieren eines technischen Kontos finden Sie unter [Developer Console-Setup](https://experienceleague.adobe.com/en/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/set-up-developer-console-and-postman) und [End-to-End-Einrichtung eines technischen Kontos](https://experienceleague.adobe.com/en/docs/platform-learn/tutorial-comprehensive-technical/setup).

## Beispiel-API-Aufrufe

Nachdem Sie die erforderlichen Authentifizierungskopfzeilen konfiguriert haben (siehe [API-Authentifizierungshandbuch](../../landing/api-authentication.md)), können Sie mit Aufrufen an die [!DNL Query Service]-API beginnen. In den folgenden Abschnitten werden verschiedene API-Aufrufe mit allgemeinen Formaten, Beispielanfragen einschließlich erforderlicher Kopfzeilen und Beispielantworten veranschaulicht.

### Abrufen einer Liste geplanter Abfragen

Sie können eine Liste aller geplanten Abfragen für Ihr Unternehmen abrufen, indem Sie eine GET-Anfrage an den `/schedules`-Endpunkt senden.

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
| `start` | Geben Sie einen Zeitstempel im ISO-Format an, um die Ergebnisse zu sortieren. Wenn kein Startdatum angegeben wird, gibt der API-Aufruf zuerst die älteste erstellte geplante Abfrage zurück und listet dann weiterhin neuere Ergebnisse auf.<br> ISO-Zeitstempel ermöglichen verschiedene Granularitätsstufen in Datum und Uhrzeit. Die grundlegenden ISO-Zeitstempel haben das Format: `2020-09-07`, um das Datum 7. September 2020 auszudrücken. Ein komplexeres Beispiel würde als `2022-11-05T08:15:30-05:00` geschrieben und entspricht dem 5. November 2022, 8:15:30 Uhr, US Eastern Standard Time. Eine Zeitzone kann mit einem UTC-Offset versehen werden und wird durch das Suffix „Z“ (`2020-01-01T01:01:01Z`) gekennzeichnet. Wenn keine Zeitzone angegeben wird, wird standardmäßig null verwendet. |
| `property` | Filtern Sie Ergebnisse nach Feldern. Die Filter **müssen** mit HTML-Escape-Zeichen versehen sein. Kommas dienen dazu, mehrere Filter zu kombinieren. Unterstützte Felder sind `created`, `templateId` und `userId`. Die Liste der unterstützten Operatoren ist `>` (größer als), `<` (kleiner als) und `==` (gleich). Beispielsweise gibt `userId==6ebd9c2d-494d-425a-aa91-24033f3abeec` alle geplanten Abfragen zurück, bei denen die Benutzer-ID wie angegeben ist. |

**Anfrage**

Die folgende Anfrage ruft die neueste geplante Abfrage ab, die für Ihre Organisation erstellt wurde.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status-Code 200 mit einer Liste geplanter Abfragen für die angegebene Organisation zurück. Die folgende Antwort gibt die neueste geplante Abfrage zurück, die für Ihre Organisation erstellt wurde.

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

Sie können eine neue geplante Abfrage erstellen, indem Sie eine POST-Anfrage an den `/schedules`-Endpunkt senden. Wenn Sie eine geplante Abfrage in der API erstellen, wird sie auch im Abfrage-Editor angezeigt. Weitere Informationen zu geplanten Abfragen in der Benutzeroberfläche finden Sie in der [Dokumentation zum Abfrage-Editor](../ui/user-guide.md#scheduled-queries).

**API-Format**

```http
POST /schedules
```

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `query.dbName` | Der Name der Datenbank, in der die geplante Abfrage ausgeführt wird. |
| `query.sql` | Die SQL-Abfrage, die nach dem definierten Zeitplan ausgeführt werden soll. |
| `query.name` | Der Name der geplanten Abfrage. |
| `query.description` | Eine optionale Beschreibung für die geplante Abfrage. |
| `schedule.schedule` | Der Cron-Zeitplan für die Abfrage. Unter [Crontab.guru](https://crontab.guru/) finden Sie eine interaktive Möglichkeit, Cron-Ausdrücke zu erstellen, zu validieren und zu verstehen. In diesem Beispiel bedeutet &quot;`30 * * * *`&quot;, dass die Abfrage jede Stunde mit der 30-Minuten-Marke ausgeführt wird.<br><br>Alternativ können Sie die folgenden kurzen Ausdrücke verwenden:<ul><li>`@once`: Die Abfrage wird nur einmal ausgeführt.</li><li>`@hourly`: Die Abfrage wird stündlich zu Beginn der Stunde ausgeführt. Dies entspricht dem Cron-Ausdruck `0 * * * *`.</li><li>`@daily`: Die Abfrage wird einmal täglich um Mitternacht ausgeführt. Dies entspricht dem Cron-Ausdruck `0 0 * * *`.</li><li>`@weekly`: Die Abfrage wird einmal pro Woche, am Sonntag um Mitternacht, ausgeführt. Dies entspricht dem Cron-Ausdruck `0 0 * * 0`.</li><li>`@monthly`: Die Abfrage wird einmal monatlich am ersten Tag des Monats um Mitternacht ausgeführt. Dies entspricht dem Cron-Ausdruck `0 0 1 * *`.</li><li>`@yearly`: Die Abfrage wird einmal jährlich am 1. Januar um Mitternacht ausgeführt. Dies entspricht dem Cron-Ausdruck `0 0 1 1 *`. |
| `schedule.startDate` | Das Startdatum für Ihre geplante Abfrage, geschrieben als UTC-Zeitstempel. |

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 202 (Akzeptiert) mit Details zur neu erstellten geplanten Abfrage zurückgegeben. Nachdem die geplante Abfrage aktiviert wurde, ändert sich die `state` von `REGISTERING` in `ENABLED`.

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
>Sie können den Wert von `_links.delete` verwenden, um [die erstellte geplante Abfrage zu löschen](#delete-a-specified-scheduled-query).

### Anfragedetails einer angegebenen geplanten Abfrage

Sie können Informationen zu einer bestimmten geplanten Abfrage abrufen, indem Sie eine GET-Anfrage an den `/schedules`-Endpunkt senden und im Anfragepfad die Kennung angeben.

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status-Code 200 mit Details zur angegebenen geplanten Abfrage zurück.

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
>Sie können den Wert von `_links.delete` verwenden, um [die erstellte geplante Abfrage zu löschen](#delete-a-specified-scheduled-query).

### Aktualisieren der Details einer angegebenen geplanten Abfrage

Sie können die Details für eine bestimmte geplante Abfrage aktualisieren, indem Sie eine PATCH-Anfrage an den `/schedules`-Endpunkt stellen und im Anfragepfad dessen ID angeben.

Für die PATCH-Anfrage werden zwei Pfade unterstützt: `/state` und `/schedule/schedule`.

### Status der geplanten Abfrage aktualisieren

Sie können den Status der ausgewählten geplanten Abfrage aktualisieren, indem Sie die `path`-Eigenschaft auf `/state` und die `value`-Eigenschaft `enable` oder `disable` festlegen.

**API-Format**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Der `id` der geplanten Abfrage, die Sie an PATCH senden möchten. |


**Anfrage**

Diese API-Anfrage nutzt für die Payload die JSON Patch-Syntax. Weiterführende Informationen zur Funktionsweise von JSON Patch finden Sie im Dokument zu den API-Grundlagen.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `op` | Der für den Abfragezeitplan auszuführende Vorgang. Der akzeptierte Wert ist `replace`. |
| `path` | Der Pfad des Werts, den Sie ändern möchten. Da Sie in diesem Fall den Status der geplanten Abfrage aktualisieren, müssen Sie den Wert von `path` auf `/state` festlegen. |
| `value` | Der aktualisierte Wert von `/state`. Dieser Wert kann entweder als `enable` oder `disable` festgelegt werden, um die geplante Abfrage zu aktivieren oder zu deaktivieren. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 202 (Akzeptiert) mit der folgenden Meldung zurück.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Zeitplan für geplante Abfragen aktualisieren

Sie können den Cron-Zeitplan der geplanten Abfrage aktualisieren, indem Sie die `path` Eigenschaft im Anfrageinhalt auf `/schedule/schedule` festlegen. Weitere Informationen zu Cron-Zeitplänen finden Sie in der Dokumentation zum [Format von Cron-Ausdrücken](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html).

**API-Format**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Der `id` der geplanten Abfrage, die Sie an PATCH senden möchten. |

**Anfrage**

Diese API-Anfrage nutzt für die Payload die JSON Patch-Syntax. Weiterführende Informationen zur Funktionsweise von JSON Patch finden Sie im Dokument zu den API-Grundlagen.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `op` | Der für den Abfragezeitplan auszuführende Vorgang. Der akzeptierte Wert ist `replace`. |
| `path` | Der Pfad des Werts, den Sie ändern möchten. Da Sie in diesem Fall den Zeitplan der geplanten Abfrage aktualisieren, müssen Sie den Wert von `path` auf `/schedule/schedule` festlegen. |
| `value` | Der aktualisierte Wert von `/schedule`. Dieser Wert muss in Form eines Cron-Zeitplans angegeben werden. In diesem Beispiel wird die geplante Abfrage also stündlich mit der Marke von 45 Minuten ausgeführt. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 202 (Akzeptiert) mit der folgenden Meldung zurück.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Löschen einer angegebenen geplanten Abfrage

Sie können eine bestimmte geplante Abfrage löschen, indem Sie eine DELETE-Anfrage an den `/schedules`-Endpunkt senden und im Anfragepfad die ID der geplanten Abfrage angeben, die Sie löschen möchten.

>[!NOTE]
>
>Der Zeitplan **muss** vor dem Löschen deaktiviert werden.

**API-Format**

```http
DELETE /schedules/{SCHEDULE_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Der `id` der geplanten Abfrage, die Sie an DELETE senden möchten. |

**Anfrage**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
