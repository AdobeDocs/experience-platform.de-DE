---
keywords: Experience Platform;home;popular topics;Salesforce;salesforce
solution: Experience Platform
title: Erstellen eines Salesforce-Connectors mithilfe der Flow Service API
topic: overview
type: Tutorial
description: Dieses Lernprogramm verwendet die Flow Service API, um Sie durch die Schritte zu führen, mit denen Sie die Plattform mit einem Salesforce-Konto verbinden können, um CRM-Daten zu erfassen.
translation-type: tm+mt
source-git-commit: d332226541685108b58d88096146ed6048606774
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 23%

---


# Erstellen eines [!DNL Salesforce] Connectors mit der [!DNL Flow Service] API

Der Flow Service dient zur Erfassung und Zentralisierung von Kundendaten aus verschiedenen Quellen innerhalb von Adobe Experience Platform. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

Dieses Lernprogramm verwendet die [!DNL Flow Service] API, um Sie durch die Schritte zu führen, die notwendig sind, um eine Verbindung zu einem [!DNL Platform] [!DNL Salesforce] Konto zur Erfassung von CRM-Daten herzustellen.

Wenn Sie lieber die Benutzeroberfläche in verwenden möchten, [!DNL Experience Platform]bietet das [Salesforce-UI-Lernprogramm](../../../ui/create/crm/salesforce.md) schrittweise Anleitungen zum Durchführen ähnlicher Aktionen.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu verbessern.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

The following sections provide additional information that you will need to know in order to successfully connect [!DNL Platform] to a [!DNL Salesforce] account using the [!DNL Flow Service] API.

### Erforderliche Anmeldedaten sammeln

Damit eine Verbindung [!DNL Flow Service] zu [!DNL Salesforce]hergestellt werden kann, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `environmentUrl` | The URL of the [!DNL Salesforce] source instance. |
| `username` | Der Benutzername für das [!DNL Salesforce] Benutzerkonto. |
| `password` | Das Kennwort für das [!DNL Salesforce] Benutzerkonto. |
| `securityToken` | Das Sicherheits-Token für das [!DNL Salesforce] Benutzerkonto. |

Weitere Informationen zu den ersten Schritten finden Sie in [diesem Salesforce-Dokument](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](../../../../../tutorials/authentication.md) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to the [!DNL Flow Service], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* x-sandbox-name: `{SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* Content-Type: `application/json`

## Verbindungsspezifikationen nachschlagen

Bevor Sie eine Verbindung [!DNL Platform] zu einem [!DNL Salesforce] Konto herstellen, müssen Sie sicherstellen, dass die Verbindungsspezifikationen für dieses Konto vorhanden sind [!DNL Salesforce]. Wenn keine Verbindungsspezifikationen vorhanden sind, kann keine Verbindung hergestellt werden.

Jede verfügbare Quelle verfügt über einen eigenen Satz von Verbindungsspezifikationen, um Verbindungseigenschaften wie Authentifizierungsanforderungen zu beschreiben. Sie können Verbindungsspezifikationen nachschlagen, [!DNL Salesforce] indem Sie eine GET anfordern und Abfragen-Parameter verwenden.

**API-Format**

Beim Senden einer GET ohne Abfrage-Parameter werden Verbindungsspezifikationen für alle verfügbaren Quellen zurückgegeben. Sie können die Abfrage einbeziehen, `property=name=="salesforce"` um Informationen speziell für [!DNL Salesforce]Sie zu erhalten.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="salesforce"
```

**Anfrage**

Die folgende Anforderung ruft die Verbindungsspezifikationen für [!DNL Salesforce]ab.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name==%22salesforce%22' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Verbindungsspezifikationen für [!DNL Salesforce]einschließlich der eindeutigen Kennung (`id`) zurück. Diese ID ist im nächsten Schritt erforderlich, um eine Basisverbindung zu erstellen.

```json
{
    "items": [
        {
            "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
            "name": "salesforce",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "type": "Basic_Authentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params",
                        "properties": {
                            "environmentUrl": {
                                "type": "string",
                                "description": "URL of the source instance"
                            },
                            "username": {
                                "type": "string",
                                "description": "User name for the user account"
                            },
                            "password": {
                                "type": "string",
                                "description": "Password for the user account",
                                "format": "password"
                            },
                            "securityToken": {
                                "type": "string",
                                "description": "Security token for the user account",
                                "format": "password"
                            }
                        },
                        "required": [
                            "username",
                            "password",
                            "securityToken"
                        ]
                    }
                }
            ]
        }
    ]
}
```

## Verbindung für die API erstellen

Eine Verbindung für die API gibt eine Quelle an und enthält Ihre Anmeldeinformationen für diese Quelle. Pro [!DNL Salesforce] Konto ist nur eine Verbindung für die API erforderlich, da sie zum Erstellen mehrerer Quell-Connectors verwendet werden kann, um verschiedene Daten einzubringen.

**API-Format**

```http
POST /connections
```

**Anfrage**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Salesforce Base Connection",
        "description": "Base connection for Salesforce account",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.username` | Der mit Ihrem [!DNL Salesforce] Konto verknüpfte Benutzername. |
| `auth.params.password` | Das Ihrem [!DNL Salesforce] Konto zugeordnete Kennwort. |
| `auth.params.securityToken` | Das mit Ihrem [!DNL Salesforce] Konto verknüpfte Sicherheitstoken. |
| `connectionSpec.id` | Die Verbindungsspezifikation `id` Ihres [!DNL Salesforce] Kontos, die im vorherigen Schritt abgerufen wurde. |

**Antwort**

Eine erfolgreiche Antwort enthält die eindeutige Kennung der Basisverbindung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Lernprogramm zu untersuchen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung für Ihr [!DNL Salesforce] Konto mithilfe von APIs erstellt und eine eindeutige ID als Teil des Antwortkörpers erhalten. Sie können diese Verbindungs-ID im nächsten Lernprogramm verwenden, um zu erfahren, wie Sie CRM-Systeme mithilfe der Flow Service API [erkunden](../../explore/crm.md).