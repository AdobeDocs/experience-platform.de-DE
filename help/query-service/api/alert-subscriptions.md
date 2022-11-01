---
keywords: Experience Platform; Startseite; beliebte Themen; Abfragedienst; Query Service; Warnhinweis;
title: API-Endpunkt für Warnhinweis-Abonnements
description: Dieses Handbuch enthält Beispiel-HTTP-Anfragen und -Antworten für die verschiedenen API-Aufrufe, die Sie mit der Query Service-API an den Endpunkt für Warnhinweise-Abonnements senden können.
source-git-commit: 4f85f38e4870f0c2429a3a2a50bd7f95075c6be4
workflow-type: tm+mt
source-wordcount: '2289'
ht-degree: 7%

---

# API-Endpunkt für Warnhinweis-Abonnements

Mit dem Adobe Experience Platform-Abfrage-Service können Sie Warnhinweise für ungeplante und geplante Abfragen abonnieren. Warnhinweise können per E-Mail, über die Platform-Benutzeroberfläche oder über beide empfangen werden. Der Benachrichtigungsinhalt ist für Warnhinweise in der Plattform und für E-Mail-Warnungen identisch. Zurzeit können Abfrage-Warnhinweise nur mit der [Abfrage-Service-API](https://developer.adobe.com/experience-platform-apis/references/query-service/) abonniert werden.

>[!IMPORTANT]
>
>Um E-Mail-Warnungen zu erhalten, müssen Sie diese Einstellung zunächst in der Benutzeroberfläche aktivieren. Weitere Informationen finden Sie in der Dokumentation für [Anweisungen zum Aktivieren von E-Mail-Warnungen](../../observability/alerts/ui.md#enable-email-alerts).

In der folgenden Tabelle werden die unterstützten Warnhinweistypen für verschiedene Arten von Abfragen erläutert:

| Abfragetyp | Unterstützte Warnhinweistypen |
|---|---|
| Ad-hoc-Abfragen | `success` oder `failed` Ausführungen. |
| Geplante Abfragen | `start`, `success`oder `failed` Ausführungen. |

>[!NOTE]
>
>Alle Nicht-SELECT-Abfragen unterstützen Warnungen-Abonnements und Sie müssen nicht der Ersteller der Abfrage sein, um eine Warnung zu abonnieren. Andere Benutzer können sich auch für Warnhinweise bei einer Abfrage registrieren, die sie nicht erstellt haben.

Die folgenden Warnhinweise gelten ohne Warnhinweis-Abonnement:

* Wenn ein Batch-Abfrageauftrag abgeschlossen ist, erhalten Benutzer eine Benachrichtigung.
* Wenn die Dauer eines Batch-Abfrageauftrags einen Schwellenwert überschreitet, wird ein Warnhinweis für die Person ausgelöst, die die Abfrage geplant hat.

>[!NOTE]
>
>Für Tests verwendete Abfragen können aus diesen Warnhinweisen ausgeschlossen werden, wenn sie entsprechend konfiguriert sind.

## Beispiel-API-Aufrufe

In den folgenden Abschnitten werden die verschiedenen API-Aufrufe beschrieben, die Sie mithilfe der Query Service-API ausführen können. Jeder Aufruf enthält das allgemeine API-Format, eine Beispielanfrage mit den erforderlichen Kopfzeilen und eine Beispielantwort.

## Liste aller Warnhinweise für eine Organisation und eine Sandbox abrufen {#get-list-of-org-alert-subs}

Rufen Sie eine Liste aller Warnhinweise für eine Organisations-Sandbox ab, indem Sie eine GET-Anfrage an die `/alert-subscriptions` -Endpunkt.

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

Eine erfolgreiche Antwort gibt den HTTP-200-Status zurück und die `alerts` -Array mit Paginierung und Versionsinformationen. Die `alerts` -Array enthält Details zu allen Warnhinweisen für eine Organisation und eine bestimmte Sandbox. Pro Antwort stehen maximal drei Warnhinweise zur Verfügung. Jeder Warnhinweis ist im Antworttext enthalten.

>[!NOTE]
>
>Die `alerts._links` -Objekt im `alerts` -Array wurde aus Gründen der Kürze abgeschnitten. Ein vollständiges Beispiel für die `alerts._links` -Objekt finden Sie im [Antwort auf die POST-Anfrage](#subscribe-users).

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
| `alerts.id` | Der Name des Warnhinweises. Dieser Name wird vom Warnhinweisdienst generiert und im Dashboard &quot;Warnungen&quot;verwendet. Der Warnungsname besteht aus dem Ordner, in dem der Warnhinweis gespeichert wird, und der `alertType`und die Fluss-ID. Informationen zu den verfügbaren Warnhinweisen finden Sie im [Dokumentation zum Platform-Warnhinweis-Dashboard](../../observability/alerts/ui.md). |
| `alerts.status` | Der Warnhinweis weist vier Statuswerte auf: `enabled`, `enabling`, `disabled`und `disabling`. Ein Warnhinweis wartet entweder aktiv auf die Ereignisse, hält sie für die zukünftige Verwendung an, behält dabei alle relevanten Abonnenten und Einstellungen bei oder wechselt zwischen diesen Status. |
| `alerts.alertType` | Die Art des Warnhinweises. Es gibt drei mögliche Werte für eine Warnung: <ul><li>`start`: Benachrichtigt einen Benutzer, wenn die Ausführung der Abfrage begonnen hat.</li><li>`success`: Benachrichtigt den Benutzer bei Abschluss der Abfrage.</li><li>`failure`: Benachrichtigt den Benutzer, wenn die Abfrage fehlschlägt.</li></ul> |
| `alerts._links` | Enthält Informationen zu den verfügbaren Methoden und Endpunkten, mit denen Informationen zu dieser Warnhinweis-ID abgerufen, aktualisiert, bearbeitet oder gelöscht werden können. |
| `_page` | Das Objekt enthält Eigenschaften zum Beschreiben der Reihenfolge, Größe, Gesamtanzahl der Seiten und der aktuellen Seite. |
| `_links` | Das Objekt enthält URI-Referenzen, die zum Abrufen der nächsten oder vorherigen Seite von Ressourcen verwendet werden können. |

## Abrufen der Informationen zum Warnhinweis-Abonnement für eine bestimmte Abfrage oder Zeitplan-ID {#retrieve-all-alert-subscriptions-by-id}

Rufen Sie die Informationen zum Warnhinweis-Abonnement für eine bestimmte Abfrage-ID oder Zeitplan-ID ab, indem Sie eine GET-Anfrage an die `/alert-subscriptions/{QUERY_ID}` oder `/alert-subscriptions/{SCHEDULE_ID}` -Endpunkt.

**API-Format**

```http
GET /alert-subscriptions/{QUERY_ID}
GET /alert-subscriptions/{SCHEDULE_ID}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{QUERY_ID}` | Die Kennung der Abfrage, für die Sie die Abonnementinformationen zurückgeben möchten. |
| `{SCHEDULE_ID}` | Die ID der geplanten Abfrage, für die Sie die Abonnementinformationen zurückgeben möchten. |

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

Eine erfolgreiche Antwort gibt den HTTP-Status 200 zurück und die `alerts` -Array, das Abonnementinformationen für die angegebene Abfrage- oder Zeitplan-ID enthält.

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
| `assetId` | Der Warnhinweis ist mit dieser ID verknüpft. Die ID kann entweder eine Abfrage-ID oder eine Zeitplan-ID sein. |
| `id` | Der Name des Warnhinweises. Dieser Name wird vom Warnhinweisdienst generiert und im Dashboard &quot;Warnungen&quot;verwendet. Der Warnungsname besteht aus dem Ordner, in dem der Warnhinweis gespeichert wird, und der `alertType`und die Fluss-ID. Informationen zu den verfügbaren Warnhinweisen finden Sie im [Dokumentation zum Platform-Warnhinweis-Dashboard](../../observability/alerts/ui.md). |
| `status` | Der Warnhinweis weist vier Statuswerte auf: `enabled`, `enabling`, `disabled`und `disabling`. Ein Warnhinweis wartet entweder aktiv auf die Ereignisse, hält sie für die zukünftige Verwendung an, behält dabei alle relevanten Abonnenten und Einstellungen bei oder wechselt zwischen diesen Status. |
| `alertType` | Jeder Warnhinweis kann drei verschiedene Arten von Warnhinweisen aufweisen. Sie sind: <ul><li>`start`: Benachrichtigt einen Benutzer, wenn die Ausführung der Abfrage begonnen hat.</li><li>`success`: Benachrichtigt den Benutzer bei Abschluss der Abfrage.</li><li>`failure`: Benachrichtigt den Benutzer, wenn die Abfrage fehlschlägt.</li></ul> |
| `subscriptions.emailNotifications` | Eine Reihe von Adobe registrierten E-Mail-Adressen für Benutzer, die sich für den Erhalt von E-Mails für den Warnhinweis angemeldet haben. |
| `subscriptions.inContextNotifications` | Eine Reihe von E-Mail-Adressen, die von Adoben registriert wurden, um Benutzer zu erreichen, die Benachrichtigungen der Benutzeroberfläche für den Warnhinweis abonniert haben. |

## Abrufen von Warnhinweisinformationen für eine bestimmte Abfrage- oder Zeitplan-ID und einen Warnhinweistyp {#get-alert-info-by-id-and-alert-type}

Rufen Sie die Informationen zum Warnhinweis-Abonnement für eine bestimmte ID und einen bestimmten Warnhinweistyp ab, indem Sie eine GET-Anfrage an die `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` -Endpunkt. Dies gilt sowohl für Abfrage- als auch für geplante Abfrage-IDs.

**API-Format**

```http
GET /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
GET /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `ALERT_TYPE` | Jeder Warnhinweis kann drei verschiedene Arten von Warnhinweisen aufweisen. Sie sind: <ul><li>`start`: Benachrichtigt einen Benutzer, wenn die Ausführung der Abfrage begonnen hat.</li><li>`success`: Benachrichtigt den Benutzer bei Abschluss der Abfrage.</li><li>`failure`: Benachrichtigt den Benutzer, wenn die Abfrage fehlschlägt.</li></ul> |
| `QUERY_ID` | Die eindeutige Kennung für die zu aktualisierende Abfrage. |
| `SCHEDULE_ID` | Die eindeutige Kennung für die geplante Abfrage, die aktualisiert werden soll. |

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

Eine erfolgreiche Antwort gibt den HTTP-Status 200 und alle Warnhinweise zurück, die abonniert wurden. Dazu gehören die Warnhinweis-ID, der Typ des Warnhinweises, die für die Adobe registrierten E-Mail-IDs des Abonnenten und der bevorzugte Benachrichtigungskanal.

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
| `alertType` | Die Art des Warnhinweises. Es gibt drei mögliche Werte für eine Warnung: <ul><li>`start`: Benachrichtigt einen Benutzer, wenn die Ausführung der Abfrage begonnen hat.</li><li>`success`: Benachrichtigt den Benutzer bei Abschluss der Abfrage.</li><li>`failure`: Benachrichtigt den Benutzer, wenn die Abfrage fehlschlägt.</li></ul> |
| `subscriptions` | Ein Objekt, das verwendet wird, um die mit den Warnhinweisen verknüpften registrierten E-Mail-IDs der Adobe sowie die Kanäle zu übergeben, in denen die Benutzer die Warnhinweise erhalten. |
| `subscriptions.inContextNotifications` | Eine Reihe von E-Mail-Adressen, die von Adoben registriert wurden, um Benutzer zu erreichen, die Benachrichtigungen der Benutzeroberfläche für den Warnhinweis abonniert haben. |
| `subscriptions.emailNotifications` | Eine Reihe von Adobe registrierten E-Mail-Adressen für Benutzer, die sich für den Erhalt von E-Mails für den Warnhinweis angemeldet haben. |

## Rufen Sie eine Liste aller Warnungen ab, die ein Benutzer abonniert hat {#get-alert-subscription-list}

Rufen Sie eine Liste aller Warnhinweise ab, die ein Benutzer abonniert hat, indem Sie eine GET-Anfrage an die `/alert-subscriptions/user-subscriptions/{EMAIL_ID}` -Endpunkt. Die Antwort enthält den Warnungsnamen, die Kennungen, den Status, den Warnungstyp und die Benachrichtigungskanäle.

**API-Format**

```http
GET /alert-subscriptions/user-subscriptions/{EMAIL_ID}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{EMAIL_ID}` | Eine E-Mail-Adresse, die für ein Adobe-Konto registriert ist, wird verwendet, um die Benutzer zu identifizieren, die Warnhinweise abonniert haben. |

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

Eine erfolgreiche Antwort gibt den HTTP-Status 200 zurück und die `items` Array mit Details zu den von der `emailId` bereitgestellt.

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
| `name` | Der Name des Warnhinweises. Dieser Name wird vom Warnhinweisdienst generiert und im Dashboard &quot;Warnungen&quot;verwendet. Der Warnungsname besteht aus dem Ordner, in dem der Warnhinweis gespeichert wird, und der `alertType`und die Fluss-ID. Informationen zu den verfügbaren Warnhinweisen finden Sie im [Dokumentation zum Platform-Warnhinweis-Dashboard](../../observability/alerts/ui.md). |
| `assetId` | Die Abfrage-ID, die den Warnhinweis mit einer bestimmten Abfrage verknüpft hat. |
| `status` | Der Warnhinweis weist vier Statuswerte auf: `enabled`, `enabling`, `disabled`und `disabling`. Ein Warnhinweis wartet entweder aktiv auf die Ereignisse, hält sie für die zukünftige Verwendung an, behält dabei alle relevanten Abonnenten und Einstellungen bei oder wechselt zwischen diesen Status. |
| `alertType` | Die Art des Warnhinweises. Es gibt drei mögliche Werte für eine Warnung: <ul><li>`start`: Benachrichtigt einen Benutzer, wenn die Ausführung der Abfrage begonnen hat.</li><li>`success`: Benachrichtigt den Benutzer bei Abschluss der Abfrage.</li><li>`failure`: Benachrichtigt den Benutzer, wenn die Abfrage fehlschlägt.</li></ul> |
| `subscriptions` | Ein Objekt, das verwendet wird, um die mit den Warnhinweisen verknüpften registrierten E-Mail-IDs der Adobe sowie die Kanäle zu übergeben, in denen die Benutzer die Warnhinweise erhalten. |
| `subscriptions.inContextNotifications` | Ein boolean -Wert, der bestimmt, wie Benutzer Warnhinweise erhalten. A `true` -Wert bestätigt, dass Warnhinweise über die Benutzeroberfläche bereitgestellt werden sollten. A `false` -Wert stellt sicher, dass die Benutzer nicht über diesen Kanal benachrichtigt werden. |
| `subscriptions.emailNotifications` | Ein boolean -Wert, der bestimmt, wie Benutzer Warnhinweise erhalten. A `true` -Wert bestätigt, dass Warnhinweise per E-Mail bereitgestellt werden sollten. A `false` -Wert stellt sicher, dass die Benutzer nicht über diesen Kanal benachrichtigt werden. |

## Warnhinweis erstellen und Benutzer abonnieren {#subscribe-users}

Um einen Warnhinweis zu erstellen und einen Benutzer für den Empfang anzumelden, erstellen Sie eine `POST` Anfrage an `/alert-subscriptions` -Endpunkt. Diese Anfrage verknüpft eine Abfrage mit einem neu erstellten Warnhinweis, indem eine `assetId` -Eigenschaft und abonniert Benutzer über die Verwendung von `emailIds`.

>[!IMPORTANT]
>
>Sie können in einer Anfrage bis zu fünf Adoben registrierte E-Mail-IDs übergeben. Um mehr als fünf Benutzer für einen Warnhinweis anzumelden, müssen nachfolgende Anfragen gestellt werden.

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
| `assetId` | Der Warnhinweis ist mit dieser ID verknüpft. Die ID kann entweder eine Abfrage-ID oder eine Zeitplan-ID sein. |
| `alertType` | Die Art des Warnhinweises. Es gibt drei mögliche Werte für eine Warnung: <ul><li>`start`: Benachrichtigt einen Benutzer, wenn die Ausführung der Abfrage begonnen hat.</li><li>`success`: Benachrichtigt den Benutzer bei Abschluss der Abfrage.</li><li>`failure`: Benachrichtigt den Benutzer, wenn die Abfrage fehlschlägt.</li></ul> |
| `subscriptions` | Ein Objekt, das verwendet wird, um die mit den Warnhinweisen verknüpften registrierten E-Mail-IDs der Adobe sowie die Kanäle zu übergeben, in denen die Benutzer die Warnhinweise erhalten. |
| `subscriptions.emailIds` | Ein Array von E-Mail-Adressen zur Identifizierung der Benutzer, die die Warnungen erhalten sollen. Die E-Mail-Adressen **must** bei einem Adobe-Konto registriert sein. |
| `subscriptions.inContextNotifications` | Ein boolean -Wert, der bestimmt, wie Benutzer Warnhinweise erhalten. A `true` -Wert bestätigt, dass Warnhinweise über die Benutzeroberfläche bereitgestellt werden sollten. A `false` -Wert stellt sicher, dass die Benutzer nicht über diesen Kanal benachrichtigt werden. |
| `subscriptions.emailNotifications` | Ein boolean -Wert, der bestimmt, wie Benutzer Warnhinweise erhalten. A `true` -Wert bestätigt, dass Warnhinweise per E-Mail bereitgestellt werden sollten. A `false` -Wert stellt sicher, dass die Benutzer nicht über diesen Kanal benachrichtigt werden. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 202 (Akzeptiert) mit Details zu Ihrem neu erstellten Warnhinweis zurück.

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
| `id` | Der Name des Warnhinweises. Dieser Name wird vom Warnhinweisdienst generiert und im Dashboard &quot;Warnungen&quot;verwendet. Der Warnungsname besteht aus dem Ordner, in dem der Warnhinweis gespeichert wird, und der `alertType`und die Fluss-ID. Informationen zu den verfügbaren Warnhinweisen finden Sie im [Dokumentation zum Platform-Warnhinweis-Dashboard](../../observability/alerts/ui.md). |
| `_links` | Enthält Informationen zu den verfügbaren Methoden und Endpunkten, mit denen Informationen zu dieser Warnhinweis-ID abgerufen, aktualisiert, bearbeitet oder gelöscht werden können. |

## Warnhinweis aktivieren oder deaktivieren {#enable-or-disable-alert}

Diese Anfrage verweist auf einen bestimmten Warnhinweis, der eine Abfrage- oder Zeitplan-ID sowie einen Warnhinweistyp verwendet, und aktualisiert den Warnhinweisstatus auf `enable` oder `disable`. Sie können den Status eines Warnhinweises aktualisieren, indem Sie eine `PATCH` Anfrage an `/alert-subscriptions/{queryId}/{alertType}` oder `/alert-subscriptions/{scheduleId}/{alertType}` -Endpunkt.

**API-Format**

```http
PATCH /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
PATCH /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `ALERT_TYPE` | Die Art des Warnhinweises. Es gibt drei mögliche Werte für eine Warnung: <ul><li>`start`: Benachrichtigt einen Benutzer, wenn die Ausführung der Abfrage begonnen hat.</li><li>`success`: Benachrichtigt den Benutzer bei Abschluss der Abfrage.</li><li>`failure`: Benachrichtigt den Benutzer, wenn die Abfrage fehlschlägt.</li></ul>Sie müssen den aktuellen Warnhinweistyp im Endpunkt-Namespace angeben, um ihn zu ändern. |
| `QUERY_ID` | Die eindeutige Kennung für die zu aktualisierende Abfrage. |
| `SCHEDULE_ID` | Die eindeutige Kennung für die geplante Abfrage, die aktualisiert werden soll. |

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
| `path` | Dieser Wert bezieht sich auf den Namespace im -Endpunkt. Derzeit ist der einzige akzeptierte Wert `/status`. |
| `value` | Bei einer erfolgreichen PATCH-Anfrage ändert dies die `status` Wert des Warnhinweises. Derzeit sind die zulässigen Werte `enable` oder `disable`. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zum Warnhinweisstatus, zum Typ und zur ID sowie zur Abfrage zurück, auf die sie sich bezieht.

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
| `id` | Der Name des Warnhinweises. Dieser Name wird vom Warnhinweisdienst generiert und im Dashboard &quot;Warnungen&quot;verwendet. Der Warnungsname besteht aus dem Ordner, in dem der Warnhinweis gespeichert wird, und der `alertType`und die Fluss-ID. Informationen zu den verfügbaren Warnhinweisen finden Sie im [Dokumentation zum Platform-Warnhinweis-Dashboard](../../observability/alerts/ui.md). |
| `assetId` | Der Warnhinweis ist mit dieser ID verknüpft. Die ID kann entweder eine Abfrage-ID oder eine Zeitplan-ID sein. |
| `alertType` | Jeder Warnhinweis kann drei verschiedene Arten von Warnhinweisen aufweisen. Sie sind: <ul><li>`start`: Benachrichtigt einen Benutzer, wenn die Ausführung der Abfrage begonnen hat.</li><li>`success`: Benachrichtigt den Benutzer bei Abschluss der Abfrage.</li><li>`failure`: Benachrichtigt den Benutzer, wenn die Abfrage fehlschlägt.</li></ul> |
| `status` | Der Warnhinweis weist vier Statuswerte auf: `enabled`, `enabling`, `disabled`und `disabling`. Ein Warnhinweis wartet entweder aktiv auf die Ereignisse, hält sie für die zukünftige Verwendung an, behält dabei alle relevanten Abonnenten und Einstellungen bei oder wechselt zwischen diesen Status. |

## Warnhinweis für eine bestimmte Abfrage und einen bestimmten Warnhinweistyp löschen {#delete-alert-info-by-id-and-alert-type}

Löschen Sie einen Warnhinweis für eine bestimmte Abfrage oder Zeitplan-ID und einen Warnhinweistyp, indem Sie eine DELETE-Anfrage an die `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` oder `/alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}` -Endpunkt.

```http
DELETE /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
DELETE /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `ALERT_TYPE` | Die Art des Warnhinweises. Es gibt drei mögliche Werte für eine Warnung: <ul><li>`start`: Benachrichtigt einen Benutzer, wenn die Ausführung der Abfrage begonnen hat.</li><li>`success`: Benachrichtigt den Benutzer bei Abschluss der Abfrage.</li><li>`failure`: Benachrichtigt den Benutzer, wenn die Abfrage fehlschlägt.</li></ul> Die DELETE-Anfrage gilt nur für den jeweiligen Warnhinweistyp. |
| `QUERY_ID` | Die eindeutige Kennung für die zu aktualisierende Abfrage. |
| `SCHEDULE_ID` | Die eindeutige Kennung für die geplante Abfrage, die aktualisiert werden soll. |

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

Eine erfolgreiche Antwort gibt den HTTP-200-Status und eine Bestätigungsmeldung zurück, die die Asset-ID und den Warnhinweistyp des gelöschten Warnhinweises enthält.

```json
{
"message": "Alert Deleted Successfully for assetId: 6df22232-f427-4250-a4e1-43cd30990641 and alertType: success",
"statusCode": 200
}
```

## Nächste Schritte

In diesem Handbuch wurde die Verwendung der `/alert-subscriptions` -Endpunkt in der Query Service-API. Nachdem Sie dieses Handbuch gelesen haben, können Sie nun besser verstehen, wie Sie einen Warnhinweis für eine Abfrage erstellen, Benutzer für den Warnhinweis abonnieren, welche Arten von Warnhinweisen verfügbar sind und wie Informationen zum Warnhinweis-Abonnement abgerufen, aktualisiert und gelöscht werden können.

Siehe [Handbuch zur Query Service-API](./getting-started.md) , um mehr über andere verfügbare Funktionen und Vorgänge zu erfahren.
