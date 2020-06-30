---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Salesforce Service Cloud-Connectors mit der Flow Service API
topic: overview
translation-type: tm+mt
source-git-commit: fc5cdaa661c47e14ed5412868f3a54fd7bd2b451
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 1%

---


# Erstellen eines [!DNL Salesforce Service Cloud] Connectors mit der [!DNL Flow Service] API

>[!NOTE]
>Der [!DNL Salesforce Service Cloud] Anschluss befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../../../home.md#terms-and-conditions) Quellen.

[!DNL Flow Service] dient zur Erfassung und Zentralisierung von Kundendaten aus unterschiedlichen Quellen innerhalb der Adobe Experience Platform. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

Dieses Lernprogramm verwendet die [!DNL Flow Service] API, um Sie durch die Schritte zur Verbindung [!DNL Experience Platform] mit [!DNL Salesforce Service Cloud] (nachfolgend &quot;SSC&quot; genannt) zu führen.

## Erste Schritte

Dieses Handbuch erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu verbessern.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um eine erfolgreiche Verbindung mit dem SSC mithilfe der [!DNL Flow Service] API herzustellen.

### Erforderliche Berechtigungen erfassen

Damit eine Verbindung [!DNL Flow Service] mit dem SSC hergestellt werden kann, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `username` | Der Benutzername für das Benutzerkonto. |
| `password` | Das Kennwort für das Benutzerkonto. |
| `securityToken` | Das Sicherheits-Token für das Benutzerkonto. |

Weitere Informationen zu den ersten Schritten finden Sie in [diesem Salesforce Service Cloud-Dokument](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm).

### Lesen von Beispiel-API-Aufrufen

In diesem Lernprogramm finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur [!DNL Experience Platform] Fehlerbehebung.

### Werte für erforderliche Kopfzeilen sammeln

Um [!DNL Platform] APIs aufzurufen, müssen Sie zunächst das [Authentifizierungslehrgang](../../../../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungtutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen [!DNL Experience Platform] API-Aufrufen bereit, wie unten dargestellt:

* Genehmigung: Träger `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Sämtliche Ressourcen in [!DNL Experience Platform]und auch die Ressourcen, die [!DNL Flow Service]gehören, werden zu bestimmten virtuellen Sandboxen isoliert. Alle Anforderungen an [!DNL Platform] APIs erfordern einen Header, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

* x-sandbox-name: `{SANDBOX_NAME}`

Für alle Anforderungen, die eine Payload enthalten (POST, PUT, PATCH), ist ein zusätzlicher Medientyp-Header erforderlich:

* Content-Type: `application/json`

## Verbindungsspezifikationen nachschlagen

Um eine SSC-Verbindung zu erstellen, muss ein Satz von SSC-Verbindungsspezifikationen innerhalb [!DNL Flow Service]vorhanden sein. Der erste Schritt beim Herstellen einer Verbindung [!DNL Platform] mit dem SSC besteht darin, diese Spezifikationen abzurufen.

**API-Format**

Jede verfügbare Quelle verfügt über einen eigenen Satz von Verbindungsspezifikationen, um Verbindungseigenschaften wie Authentifizierungsanforderungen zu beschreiben. Beim Senden einer GET-Anforderung an den `/connectionSpecs` Endpunkt werden Verbindungsspezifikationen für alle verfügbaren Quellen zurückgegeben. Sie können auch die Abfrage einschließen, Informationen speziell für SSC `property=name=="salesforce-service-cloud"` zu erhalten.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="salesforce-service-cloud"
```

**Anfrage**

Die folgende Anforderung ruft die Verbindungsspezifikation für SSC ab.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="mysql"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Verbindungsspezifikationen für den SSC einschließlich der eindeutigen Kennung (`id`) zurück. Diese ID ist im nächsten Schritt zum Erstellen einer Basisverbindung erforderlich.

```json
{
    "items": [
        {
            "id": "cb66ab34-8619-49cb-96d1-39b37ede86ea",
            "name": "salesforce-service-cloud",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "type": "BasicAuthentication",
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
            ],
        }
    ]
}
```

## Basisverbindung erstellen

Eine Basisverbindung gibt eine Quelle an und enthält Ihre Anmeldeinformationen für diese Quelle. Pro SSC-Konto ist nur eine Basisverbindung erforderlich, da diese zum Erstellen mehrerer Quellschnittstellen verwendet werden kann, um verschiedene Daten einzubringen.

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
        "name": "Base connection for salesforce service cloud",
        "description": "Base connection for salesforce service cloud",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "b66ab34-8619-49cb-96d1-39b37ede86ea",
            "version": "1.0"
        }
    }'
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `auth.params.username` | Der mit Ihrem SSC-Konto verknüpfte Benutzername. |
| `auth.params.password` | Das Ihrem SSC-Konto zugeordnete Kennwort. |
| `auth.params.securityToken` | Das mit Ihrem SSC-Konto verknüpfte Sicherheitstoken. |
| `connectionSpec.id` | Die Verbindungsspezifikation `id` Ihres SSC-Kontos, die im vorherigen Schritt abgerufen wurde. |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Basisverbindung einschließlich ihrer eindeutigen Kennung (`id`) zurück. Diese ID ist erforderlich, um Ihre Daten im nächsten Lernprogramm zu untersuchen.

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## Nächste Schritte

In diesem Lernprogramm haben Sie eine SSC-Basisverbindung mit der [!DNL Flow Service] API erstellt und den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese Basis-Verbindungs-ID im nächsten Lernprogramm verwenden, um zu erfahren, wie Sie mithilfe der Flow Service API [Erfolgssysteme von Kunden](../../explore/customer-success.md)untersuchen.
