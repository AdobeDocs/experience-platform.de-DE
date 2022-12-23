---
keywords: Experience Platform;Startseite;beliebte Themen;Abfragedienst;Abfrage-Service;Warnhinweis;
title: API-Endpunkt für Warnhinweis-Abonnements
description: Dieses Handbuch enthält Beispiele für HTTP-Anfragen und -Antworten für die verschiedenen API-Aufrufe, die Sie mit der Abfrage-Service-API an den Endpunkt für Warnhinweis-Abonnements stellen können.
exl-id: 30ac587a-2286-4a52-9199-7a2a8acd5362
source-git-commit: a9887535b12b8c4aeb39bb5a6646da88db4f0308
workflow-type: ht
source-wordcount: '2289'
ht-degree: 100%

---

# API-Endpunkt für Warnhinweis-Abonnements

Mit dem Adobe Experience Platform-Abfrage-Service können Sie Warnhinweise für ungeplante und geplante Abfragen abonnieren. Warnhinweise können per E-Mail, über die Platform-Benutzeroberfläche oder über beide empfangen werden. Der Benachrichtigungsinhalt ist für Warnhinweise in Platform und für E-Mail-Warnungen identisch. Derzeit können Abfrage-Warnhinweise nur mithilfe der [Abfrage-Service-API](https://developer.adobe.com/experience-platform-apis/references/query-service/) abonniert werden.

>[!IMPORTANT]
>
>Um E-Mail-Warnungen zu erhalten, müssen Sie diese Einstellung zunächst in der Benutzeroberfläche aktivieren. Weitere Informationen finden Sie in der Dokumentation zu [Anweisungen zum Aktivieren von E-Mail-Warnhinweisen](../../observability/alerts/ui.md#enable-email-alerts).

In der folgenden Tabelle werden die unterstützten Warnhinweistypen für verschiedene Arten von Abfragen erläutert:

| Abfragetyp | Unterstützte Warnhinweistypen |
|---|---|
| Ad-hoc-Abfragen | `success` oder `failed` Ausführungen. |
| Geplante Abfragen | `start`, `success` oder `failed` Ausführungen. |

>[!NOTE]
>
>Alle Nicht-SELECT-Abfragen unterstützen Warnhinweis-Abonnements. Sie müssen nicht der Ersteller der Abfrage sein, um einen Warnhinweis zu abonnieren. Andere Benutzende können sich ebenfalls für Warnhinweise zu einer Abfrage anmelden, die sie nicht selbst erstellt haben.

Die folgenden Warnhinweise gelten ohne Warnhinweis-Abonnement:

* Wenn ein Batch-Abfrageauftrag abgeschlossen wird, erhalten Benutzer eine Benachrichtigung.
* Wenn die Dauer eines Batch-Abfrageauftrags einen Schwellenwert überschreitet, wird ein Warnhinweis für die Person ausgelöst, die die Abfrage geplant hat.

>[!NOTE]
>
>Für Tests verwendete Abfragen können aus diesen Warnhinweisen ausgeschlossen werden, wenn sie entsprechend konfiguriert sind.

## Beispiel-API-Aufrufe

In den folgenden Abschnitten werden die verschiedenen API-Aufrufe beschrieben, die Sie mithilfe der Query Service-API ausführen können. Jeder Aufruf enthält das allgemeine API-Format, eine Beispielanfrage mit den erforderlichen Kopfzeilen und eine Beispielantwort.

## Abrufen einer Liste aller Warnhinweise für eine Organisation und Sandbox {#get-list-of-org-alert-subs}

Rufen Sie eine Liste aller Warnhinweise für eine Organisations-Sandbox ab, indem Sie eine GET-Anfrage an den `/alert-subscriptions`-Endpunkt stellen.

**API-Format**

```http
GET /alert-subscriptions
```

**Anfrage**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 sowie das `alerts`-Array mit Informationen zu Paginierung und Version zurückgegeben. Das `alerts`-Array enthält Details zu allen Warnhinweisen für eine Organisation und eine bestimmte Sandbox. Pro Antwort stehen maximal drei Warnhinweise zur Verfügung. Im Antworttext ist ein Warnhinweis pro Warnhinweistyp enthalten.

>[!NOTE]
>
>Das `alerts._links`-Objekt im `alerts`-Array wurde zur Vereinfachung gekürzt. Ein vollständiges Beispiel für das `alerts._links`-Objekt finden Sie in der [Antwort auf die POST-Anfrage](#subscribe-users).

```json
{
    "alerts": [
        {
            "assetId": "0ca168f4-e46b-4f7f-be6a-bdc386271b4a",
            "id": "query_service_flow_run_start-dcf7b4be-ccd7-4c73-ae0c-a4bb34a40adada84",
            "status": "enabled",
            "alertType": "start",
            "_links":{
                "self": {…},
                "subscribe": {…},
                "patch_status": {…},
                "get_list_of_subscribers_by_alert_type": {…},
                "delete": {…}
            }
        },
        {
            "assetId": "0ca168f4-e46b-4f7f-be6a-bdc386271b4a",
            "id": "query_service_flow_run_success-dcf7b4be-ccd7-4c73-ae0c-a4bb34a40adada84",
            "status": "enabled",
            "alertType": "success",
            "_links":{
                "self": {…},
                "subscribe": {…},
                "patch_status": {…},
                "get_list_of_subscribers_by_alert_type": {…},
                "delete": {…}
            }
        },
        {
            "assetId": "700d43d9-3b99-4d4c-8dbb-29c911c0e0df",
            "id": "query_service_flow_run_start-75da972a-e859-47a5-934c-629904daa1ef",
            "status": "enabled",
            "alertType": "start",
            "_links":{
                "self": {…},
                "subscribe": {…},
                "patch_status": {…},
                "get_list_of_subscribers_by_alert_type": {…},
                "delete": {…}
            }
        }
    ], 
    "_page": {
        "orderby": "-created",
        "page": 1,
        "count": 26,
        "pageSize": 50
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=2"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=0"
        }
    },
    "version": 1
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `alerts.assetId` | Die Abfrage-ID, die den Warnhinweis mit einer bestimmten Abfrage verknüpft hat. |
| `alerts.id` | Der Name des Warnhinweises. Dieser Name wird vom Warnhinweis-Service generiert und im Warnhinweis-Dashboard verwendet. Der Name des Warnhinweises besteht aus dem Ordner, in dem der Warnhinweis gespeichert wird, dem `alertType` und der Fluss-ID. Informationen zu den verfügbaren Warnhinweisen finden Sie in der [Dokumentation zum Warnhinweis-Dashboard von Platform](../../observability/alerts/ui.md). |
| `alerts.status` | Der Warnhinweis weist vier Statuswerte auf: `enabled`, `enabling`, `disabled` und `disabling`. Ein Warnhinweis wartet entweder aktiv auf die Ereignisse, wird für die zukünftige Verwendung angehalten, wobei alle relevanten Abonnenten und Einstellungen beibehalten werden, oder wechselt zwischen diesen Zuständen. |
| `alerts.alertType` | Der Typ des Warnhinweises. Es gibt die folgenden drei möglichen Werte für einen Warnhinweis: <ul><li>`start`: Benachrichtigt Benutzende, wenn die Ausführung der Abfrage begonnen hat.</li><li>`success`: Benachrichtigt Benutzende, wenn die Abfrage abgeschlossen ist.</li><li>`failure`: Benachrichtigt Benutzende, wenn die Abfrage fehlschlägt.</li></ul> |
| `alerts._links` | Enthält Informationen zu den verfügbaren Methoden und Endpunkten, mit denen Informationen zu dieser Warnhinweis-ID abgerufen, aktualisiert, bearbeitet oder gelöscht werden können. |
| `_page` | Das Objekt enthält Eigenschaften zum Beschreiben der Reihenfolge, Größe, Gesamtanzahl der Seiten und der aktuellen Seite. |
| `_links` | Das Objekt enthält URI-Verweise, die zum Abrufen der nächsten oder vorherigen Seite von Ressourcen verwendet werden können. |

## Abrufen der Informationen zum Warnhinweis-Abonnement für eine bestimmte Abfrage- oder Zeitplan-ID {#retrieve-all-alert-subscriptions-by-id}

Rufen Sie die Informationen zum Warnhinweis-Abonnement für eine bestimmte Abfrage- oder Zeitplan-ID ab, indem Sie eine GET-Anfrage an den `/alert-subscriptions/{QUERY_ID}`- oder `/alert-subscriptions/{SCHEDULE_ID}`-Endpunkt stellen.

**API-Format**

```http
GET /alert-subscriptions/{QUERY_ID}
GET /alert-subscriptions/{SCHEDULE_ID}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{QUERY_ID}` | Die ID der Abfrage, für die die Abonnementinformationen zurückgegeben werden sollen. |
| `{SCHEDULE_ID}` | Die ID der geplanten Abfrage, für die die Abonnementinformationen zurückgegeben werden sollen. |

**Anfrage**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 sowie das `alerts`-Array zurückgegeben, das Abonnementinformationen für die angegebene Abfrage- oder Zeitplan-ID enthält.

```json
{
    "alerts": [
        {
            "assetId": "6df22232-f427-4250-a4e1-43cd30990641",
            "id": "query_service_flow_run_failure-5cdc3bbe-750a-4d80-9c43-96e5e09f1a96",
            "status": "enabled",
            "alertType": "failure",
            "subscriptions": {
                "emailNotifications": [
                    "rrunner@adobe.com",
                    "jsnow@adobe.com",
                    "keverdeen@adobe.com"
                ],
                "inContextNotifications": [
                    "rrunner@adobe.com",
                    "jsnow@adobe.com",
                    "keverdeen@adobe.com"
                ]
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        },
        {
            "assetId": "6df22232-f427-4250-a4e1-43cd30990641",
            "id": "query_service_flow_run_start-5cdc3bbe-750a-4d80-9c43-96e5e09f1a96",
            "status": "enabled",
            "alertType": "start",
            "subscriptions": {
                "emailNotifications": [
                    "rrunner@adobe.com"
                ],
                "inContextNotifications": [
                    "rrunner@adobe.com"
                ]
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        }
    ]
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `assetId` | Der Warnhinweis ist mit dieser ID verknüpft. Die ID kann entweder eine Abfrage- oder Zeitplan-ID sein. |
| `id` | Der Name des Warnhinweises. Dieser Name wird vom Warnhinweis-Service generiert und im Warnhinweis-Dashboard verwendet. Der Name des Warnhinweises besteht aus dem Ordner, in dem der Warnhinweis gespeichert wird, dem `alertType` und der Fluss-ID. Informationen zu den verfügbaren Warnhinweisen finden Sie in der [Dokumentation zum Warnhinweis-Dashboard von Platform](../../observability/alerts/ui.md). |
| `status` | Der Warnhinweis weist vier Statuswerte auf: `enabled`, `enabling`, `disabled` und `disabling`. Ein Warnhinweis wartet entweder aktiv auf die Ereignisse, wird für die zukünftige Verwendung angehalten, wobei alle relevanten Abonnenten und Einstellungen beibehalten werden, oder wechselt zwischen diesen Zuständen. |
| `alertType` | Jeder Warnhinweis kann drei verschiedene Arten von Warnhinweistypen aufweisen. Dabei handelt es sich um: <ul><li>`start`: Benachrichtigt Benutzende, wenn die Ausführung der Abfrage begonnen hat.</li><li>`success`: Benachrichtigt Benutzende, wenn die Abfrage abgeschlossen wurde.</li><li>`failure`: Benachrichtigt Benutzende, wenn die Abfrage fehlschlägt.</li></ul> |
| `subscriptions.emailNotifications` | Eine Reihe von bei Adobe registrierten E-Mail-Adressen von Benutzenden, die sich für den Erhalt von E-Mails für den Warnhinweis angemeldet haben. |
| `subscriptions.inContextNotifications` | Ein Array von Adobe-registrierten E-Mail-Adressen für Benutzende, die Benachrichtigungen der Benutzeroberfläche für den Warnhinweis abonniert haben. |

## Abrufen von Informationen zu Warnhinweis-Abonnements für eine bestimmte Abfrage- oder Zeitplan-ID und einen Warnhinweistyp {#get-alert-info-by-id-and-alert-type}

Rufen Sie Informationen zu Warnhinweis-Abonnements für eine bestimmte ID und einen bestimmten Warnhinweistyp ab, indem Sie eine GET-Anfrage an den `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}`-Endpunkt stellen. Dies gilt für die ID von Abfragen und geplanten Abfragen.

**API-Format**

```http
GET /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
GET /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `ALERT_TYPE` | Jeder Warnhinweis kann drei verschiedene Arten von Warnhinweistypen aufweisen. Dabei handelt es sich um: <ul><li>`start`: Benachrichtigt Benutzende, wenn die Ausführung der Abfrage begonnen hat.</li><li>`success`: Benachrichtigt Benutzende, wenn die Abfrage abgeschlossen wurde.</li><li>`failure`: Benachrichtigt Benutzende, wenn die Abfrage fehlschlägt.</li></ul> |
| `QUERY_ID` | Die eindeutige Kennung der zu aktualisierenden Abfrage. |
| `SCHEDULE_ID` | Die eindeutige Kennung der geplanten Abfrage, die aktualisiert werden soll. |

**Anfrage**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1/start'' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Antwort**

Bei einer erfolgreichen Antwort werden der HTTP-Status 200 sowie alle Warnhinweise zurückgegeben, die abonniert wurden. Dazu gehören die Warnhinweis-ID, der Typ des Warnhinweises, die Adobe-registrierten E-Mail-IDs des Abonnenten und der bevorzugte Benachrichtigungskanal.

```json
{
    "alerts": [
        {
            "assetId": "6df22232-f427-4250-a4e1-43cd30990641",
            "id": "query_service_flow_run_success-5cdc3bbe-750a-4d80-9c43-96e5e09f1a96",
            "status": "enabled",
            "alertType": "success",
            "subscriptions": {
                "emailNotifications": [
                    "rrunner@adobe.com",
                    "jsnow@adobe.com"
                ],
                "inContextNotifications": [
                    "jsnow@adobe.com"
                ]
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        }
    ]
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `assetId` | Die Abfrage-ID, die den Warnhinweis mit einer bestimmten Abfrage verknüpft hat. |
| `alertType` | Der Typ des Warnhinweises. Es gibt die folgenden drei möglichen Werte für einen Warnhinweis: <ul><li>`start`: Benachrichtigt Benutzende, wenn die Ausführung der Abfrage begonnen hat.</li><li>`success`: Benachrichtigt Benutzende, wenn die Abfrage abgeschlossen wurde.</li><li>`failure`: Benachrichtigt Benutzende, wenn die Abfrage fehlschlägt.</li></ul> |
| `subscriptions` | Ein Objekt, das verwendet wird, um die mit den Warnhinweisen verknüpften registrierten E-Mail-IDs von Adobe sowie die Kanäle zu übergeben, in denen die Benutzenden die Warnhinweise erhalten. |
| `subscriptions.inContextNotifications` | Ein Array von Adobe-registrierten E-Mail-Adressen für Benutzende, die Benachrichtigungen der Benutzeroberfläche für den Warnhinweis abonniert haben. |
| `subscriptions.emailNotifications` | Eine Reihe von bei Adobe registrierten E-Mail-Adressen von Benutzenden, die sich für den Erhalt von E-Mails für den Warnhinweis angemeldet haben. |

## Rufen Sie eine Liste aller Warnungen ab, die eine Person abonniert hat {#get-alert-subscription-list}

Rufen Sie eine Liste aller Warnhinweise ab, die eine Person abonniert hat, indem Sie eine GET-Anfrage an den `/alert-subscriptions/user-subscriptions/{EMAIL_ID}`-Endpunkt stellen. Die Antwort enthält den Namen des Warnhinweises, die IDs, den Status, den Typ des Warnhinweises und die Benachrichtigungskanäle.

**API-Format**

```http
GET /alert-subscriptions/user-subscriptions/{EMAIL_ID}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{EMAIL_ID}` | Eine E-Mail-Adresse, die für ein Adobe-Konto registriert ist, wird zur Identifizierung der Personen verwendet, die Warnhinweise abonniert haben. |

**Anfrage**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/user-subscriptions/rrunner@adobe.com' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 sowie das Array `items` mit den Details zu den Warnhinweisen zurückgegeben, die mit der angegebenen `emailId` abonniert wurden.

```json
{
    "items": [
        {
            "name": "query_service_flow_run_success-8f057161-b312-4274-b629-f346c7d15c1f",
            "assetId": "39e65373-e47a-4feb-9e5a-dffa2f677bca",
            "status": "enabled",
            "alertType": "success",
            "subscriptions": {
                "inContextNotification": true,
                "emailNotifications": true
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        },
        {
            "name": "query_service_flow_run_start-8f057161-b312-4274-b629-f346c7d15c1f",
            "assetId": "39e65373-e47a-4feb-9e5a-dffa2f677bca",
            "status": "enabled",
            "alertType": "start",
            "subscriptions": {
                "inContextNotification": true,
                "emailNotifications": true
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        }
    ], "_page": {
            "orderby": "-created",
            "page": 1,
            "count": 26,
            "pageSize": 50
        },
    "_links": {
        "next": {
            "href": "https://platform-int.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=2"
        },
        "prev": {
            "href": "https://platform-int.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=0"
        }
    },
    "version": 1
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `name` | Der Name des Warnhinweises. Dieser Name wird vom Warnhinweis-Service generiert und im Warnhinweis-Dashboard verwendet. Der Name des Warnhinweises besteht aus dem Ordner, in dem der Warnhinweis gespeichert wird, dem `alertType` und der Fluss-ID. Informationen zu den verfügbaren Warnhinweisen finden Sie in der [Dokumentation zum Warnhinweis-Dashboard von Platform](../../observability/alerts/ui.md). |
| `assetId` | Die Abfrage-ID, die den Warnhinweis mit einer bestimmten Abfrage verknüpft hat. |
| `status` | Der Warnhinweis weist vier Statuswerte auf: `enabled`, `enabling`, `disabled` und `disabling`. Ein Warnhinweis wartet entweder aktiv auf die Ereignisse, wird für die zukünftige Verwendung angehalten, wobei alle relevanten Abonnenten und Einstellungen beibehalten werden, oder wechselt zwischen diesen Zuständen. |
| `alertType` | Der Typ des Warnhinweises. Es gibt die folgenden drei möglichen Werte für einen Warnhinweis: <ul><li>`start`: Benachrichtigt Benutzende, wenn die Ausführung der Abfrage begonnen hat.</li><li>`success`: Benachrichtigt Benutzende, wenn die Abfrage abgeschlossen wurde.</li><li>`failure`: Benachrichtigt Benutzende, wenn die Abfrage fehlschlägt.</li></ul> |
| `subscriptions` | Ein Objekt, das verwendet wird, um die mit den Warnhinweisen verknüpften registrierten E-Mail-IDs von Adobe sowie die Kanäle zu übergeben, in denen die Benutzenden die Warnhinweise erhalten. |
| `subscriptions.inContextNotifications` | Ein boolescher Wert, der bestimmt, wie Benutzende Benachrichtigungen zu Warnhinweisen erhalten. Der Wert `true` bestätigt, dass Warnhinweise über die Benutzeroberfläche bereitgestellt werden sollten. Der Wert `false` stellt sicher, dass die Benutzenden nicht über diesen Kanal benachrichtigt werden. |
| `subscriptions.emailNotifications` | Ein boolescher Wert, der bestimmt, wie Benutzende Benachrichtigungen zu Warnhinweisen erhalten. Der Wert `true` bestätigt, dass Warnhinweise per E-Mail bereitgestellt werden sollten. Der Wert `false` stellt sicher, dass Benutzende nicht über diesen Kanal benachrichtigt werden. |

## Erstellen eines Warnhinweises und Abonnements von Benutzenden {#subscribe-users}

Um einen Warnhinweis zu erstellen und Benutzende für den Empfang anzumelden, stellen Sie eine `POST`-Anfrage an den `/alert-subscriptions`-Endpunkt. Diese Anfrage verknüpft eine Abfrage mithilfe einer `assetId`-Eigenschaft mit einem neu erstellten Warnhinweis und meldet Benutzende mithilfe von `emailIds` für diesen Warnhinweis an.

>[!IMPORTANT]
>
>Sie können in einer Anfrage bis zu fünf bei Adobe registrierte E-Mail-IDs übergeben. Um mehr als fünf Benutzende für einen Warnhinweis anzumelden, müssen weitere Anfragen gestellt werden.

**API-Format**

```http
POST /alert-subscriptions
```

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/alert-subscriptions
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '
    {
    "assetId": "a679dd0e-bcb2-4e69-a610-22d17ba98cac",
    "alertType": "failure",
    "subscriptions": {
        "emailIds": [
            "rrunner@adobe.com",
            "jsnow@adobe.com"
        ],
        "inContextNotifications": true,
        "emailNotifications": true
    }
}'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `assetId` | Der Warnhinweis ist mit dieser ID verknüpft. Die ID kann entweder eine Abfrage- oder Zeitplan-ID sein. |
| `alertType` | Der Typ des Warnhinweises. Es gibt die folgenden drei möglichen Werte für einen Warnhinweis: <ul><li>`start`: Benachrichtigt Benutzende, wenn die Ausführung der Abfrage begonnen hat.</li><li>`success`: Benachrichtigt Benutzende, wenn die Abfrage abgeschlossen ist.</li><li>`failure`: Benachrichtigt Benutzende, wenn die Abfrage fehlschlägt.</li></ul> |
| `subscriptions` | Ein Objekt, das verwendet wird, um die mit den Warnhinweisen verknüpften registrierten E-Mail-IDs von Adobe sowie die Kanäle zu übergeben, in denen die Benutzenden die Warnhinweise erhalten. |
| `subscriptions.emailIds` | Ein Array von E-Mail-Adressen zur Identifizierung der Benutzenden, die die Warnhinweise erhalten sollen. Die E-Mail-Adressen **müssen** bei einem Adobe-Konto registriert sein. |
| `subscriptions.inContextNotifications` | Ein boolescher Wert, der bestimmt, wie Benutzende Benachrichtigungen zu Warnhinweisen erhalten. Der Wert `true` bestätigt, dass Warnhinweise über die Benutzeroberfläche bereitgestellt werden sollten. Der Wert `false` stellt sicher, dass die Benutzenden nicht über diesen Kanal benachrichtigt werden. |
| `subscriptions.emailNotifications` | Ein boolescher Wert, der bestimmt, wie Benutzende Benachrichtigungen zu Warnhinweisen erhalten. Der Wert `true` bestätigt, dass Warnhinweise per E-Mail bereitgestellt werden sollten. Der Wert `false` stellt sicher, dass die Benutzenden nicht über diesen Kanal benachrichtigt werden. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 202 (Akzeptiert) mit Details zum neu erstellten Warnhinweis zurückgegeben.

```json
{
    "assetId": "c4f67291-1161-4943-bc29-8736469bb928",
    "id": "query_service_flow_run_failure-5f4cb942-b67c-4ea4-a90d-5b6245e60aca",
    "alertType": "failure",
    "subscriptions": {
        "emailIds": [
            "{USER_EMAIL_ID}"
        ],
        "inContextNotifications": false,
        "emailNotifications": true
    },
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
            "method": "GET"
        },
        "subscribe": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
            "method": "POST",
            "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
        },
        "patch_status": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
            "method": "PATCH",
            "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
        },
        "get_list_of_subscribers_by_alert_type": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
            "method": "DELETE"
        }
    }
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `id` | Der Name des Warnhinweises. Dieser Name wird vom Warnhinweis-Service generiert und im Warnhinweis-Dashboard verwendet. Der Name des Warnhinweises besteht aus dem Ordner, in dem der Warnhinweis gespeichert wird, dem `alertType` und der Fluss-ID. Informationen zu den verfügbaren Warnhinweisen finden Sie in der [Dokumentation zum Warnhinweis-Dashboard von Platform](../../observability/alerts/ui.md). |
| `_links` | Enthält Informationen zu den verfügbaren Methoden und Endpunkten, mit denen Informationen zu dieser Warnhinweis-ID abgerufen, aktualisiert, bearbeitet oder gelöscht werden können. |

## Aktivieren oder Deaktivieren eines Warnhinweises {#enable-or-disable-alert}

Diese Anfrage verweist unter Verwendung einer Abfrage- oder Zeitplan-ID sowie eines Warnhinweistyps auf einen bestimmten Warnhinweis und aktualisiert den Warnhinweisstatus mit dem Statuswert `enable` oder `disable`. Sie können den Status eines Warnhinweises aktualisieren, indem Sie eine `PATCH`-Anfrage an den `/alert-subscriptions/{queryId}/{alertType}`- oder `/alert-subscriptions/{scheduleId}/{alertType}`-Endpunkt stellen.

**API-Format**

```http
PATCH /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
PATCH /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `ALERT_TYPE` | Der Typ des Warnhinweises. Es gibt die folgenden drei möglichen Werte für einen Warnhinweis: <ul><li>`start`: Benachrichtigt Benutzende, wenn die Ausführung der Abfrage begonnen hat.</li><li>`success`: Benachrichtigt Benutzende, wenn die Abfrage abgeschlossen ist.</li><li>`failure`: Benachrichtigt Benutzende, wenn die Abfrage fehlschlägt.</li></ul>Sie müssen den aktuellen Warnhinweistyp im Endpunkt-Namespace angeben, um ihn zu ändern. |
| `QUERY_ID` | Die eindeutige Kennung der zu aktualisierenden Abfrage. |
| `SCHEDULE_ID` | Die eindeutige Kennung der geplanten Abfrage, die aktualisiert werden soll. |

**Anfrage**

```shell
curl -X PATCH 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1/start'' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
  -d '{
        "op": "replace",
        "path" : "/status",
        "value": "enable"
      }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `op` | Der auszuführende Vorgang. Derzeit ist der einzige akzeptierte Wert `replace`. |
| `path` | Dieser Wert bezieht sich auf den Namespace im Endpunkt. Derzeit ist der einzige akzeptierte Wert `/status`. |
| `value` | Bei einer erfolgreichen PATCH-Anfrage wird damit der `status`-Wert des Warnhinweises geändert. Derzeit lauten die zulässigen Werte `enable` oder `disable`. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit Details zum Warnhinweisstatus, zum Typ und zur ID sowie zur Abfrage zurückgegeben, auf die er sich bezieht.

```json
{
    "id" : "query_service_flow_run_success-4422fc69-eaa7-464e-945b-63cfd435d3d1",
    "assetId": "4422fc69-eaa7-464e-945b-63cfd435d3d1", 
    "alertType": "start",
    "status": "enabled"
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `id` | Der Name des Warnhinweises. Dieser Name wird vom Warnhinweis-Service generiert und im Warnhinweis-Dashboard verwendet. Der Name des Warnhinweises besteht aus dem Ordner, in dem der Warnhinweis gespeichert wird, dem `alertType` und der Fluss-ID. Informationen zu den verfügbaren Warnhinweisen finden Sie in der [Dokumentation zum Warnhinweis-Dashboard von Platform](../../observability/alerts/ui.md). |
| `assetId` | Der Warnhinweis ist mit dieser ID verknüpft. Die ID kann entweder eine Abfrage- oder Zeitplan-ID sein. |
| `alertType` | Jeder Warnhinweis kann drei verschiedene Arten von Warnhinweistypen aufweisen. Dabei handelt es sich um: <ul><li>`start`: Benachrichtigt Benutzende, wenn die Ausführung der Abfrage begonnen hat.</li><li>`success`: Benachrichtigt Benutzende, wenn die Abfrage abgeschlossen ist.</li><li>`failure`: Benachrichtigt Benutzende, wenn die Abfrage fehlschlägt.</li></ul> |
| `status` | Der Warnhinweis weist vier Statuswerte auf: `enabled`, `enabling`, `disabled` und `disabling`. Ein Warnhinweis wartet entweder aktiv auf die Ereignisse, wird für die zukünftige Verwendung angehalten, wobei alle relevanten Abonnenten und Einstellungen beibehalten werden, oder wechselt zwischen diesen Zuständen. |

## Löschen des Warnhinweises für eine bestimmte Abfrage und einen bestimmten Warnhinweistyp {#delete-alert-info-by-id-and-alert-type}

Löschen Sie einen Warnhinweis für eine bestimmte Abfrage- oder Zeitplan-ID und einen Warnhinweistyp, indem Sie eine DELETE-Anfrage an den Endpunkt `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` oder `/alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}` stellen.

```http
DELETE /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
DELETE /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `ALERT_TYPE` | Der Typ des Warnhinweises. Es gibt die folgenden drei möglichen Werte für einen Warnhinweis: <ul><li>`start`: Benachrichtigt Benutzende, wenn die Ausführung der Abfrage begonnen hat.</li><li>`success`: Benachrichtigt Benutzende, wenn die Abfrage abgeschlossen ist.</li><li>`failure`: Benachrichtigt Benutzende, wenn die Abfrage fehlschlägt.</li></ul> Die DELETE-Anfrage gilt nur für den jeweils angegebenen Warnhinweistyp. |
| `QUERY_ID` | Die eindeutige Kennung der zu aktualisierenden Abfrage. |
| `SCHEDULE_ID` | Die eindeutige Kennung der geplanten Abfrage, die aktualisiert werden soll. |

**Anfrage**

```shell
curl -X DELETE 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1/start' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 sowie eine Bestätigungsmeldung zurückgegeben, die die Asset-ID und den Warnhinweistyp des gelöschten Warnhinweises enthält.

```json
{
"message": "Alert Deleted Successfully for assetId: 6df22232-f427-4250-a4e1-43cd30990641 and alertType: success",
"statusCode": 200
}
```

## Nächste Schritte

In diesem Handbuch wurde die Verwendung des `/alert-subscriptions`-Endpunkts in der Abfrage-Service-API behandelt. Nachdem Sie dieses Handbuch gelesen haben, wissen Sie nun besser, wie Sie einen Warnhinweis für eine Abfrage erstellen, Benutzende für den Warnhinweis abonnieren, welche Arten von Warnhinweisen verfügbar sind und wie Sie Informationen zum Warnhinweis-Abonnement abrufen, aktualisieren und löschen können.

Weitere Informationen zu anderen verfügbaren Funktionen und Vorgängen finden Sie im [Handbuch zur Abfrage-Service-API](./getting-started.md).
