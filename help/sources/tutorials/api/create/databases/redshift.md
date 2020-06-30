---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Amazon Redshift-Connectors mithilfe der Flow Service API
topic: overview
translation-type: tm+mt
source-git-commit: fc5cdaa661c47e14ed5412868f3a54fd7bd2b451
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 1%

---


# Erstellen eines [!DNL Amazon Redshift] Connectors mit der [!DNL Flow Service] API

>[!NOTE]
>Der [!DNL Amazon Redshift] Anschluss befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../../../home.md#terms-and-conditions) Quellen.

[!DNL Flow Service] dient zur Erfassung und Zentralisierung von Kundendaten aus unterschiedlichen Quellen innerhalb der Adobe Experience Platform. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

Dieses Lernprogramm verwendet die [!DNL Flow Service] API, um Sie durch die Schritte zur Verbindung [!DNL Experience Platform] mit [!DNL Amazon Redshift] (nachfolgend &quot;[!DNL Redshift]&quot;) zu führen.

## Erste Schritte

Dieses Handbuch erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu verbessern.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um eine Verbindung mit [!DNL Redshift] der [!DNL Flow Service] API herstellen zu können.

### Erforderliche Berechtigungen erfassen

Damit eine Verbindung [!DNL Flow Service] mit [!DNL Redshift]hergestellt werden kann, müssen Sie die folgenden Verbindungseigenschaften angeben:

| **Berechtigung** | **Beschreibung** |
| -------------- | --------------- |
| `server` | Der mit Ihrem [!DNL Redshift] Konto verknüpfte Server. |
| `username` | Der mit Ihrem [!DNL Redshift] Konto verknüpfte Benutzername. |
| `password` | Das Ihrem [!DNL Redshift] Konto zugeordnete Kennwort. |
| `database` | Die [!DNL Redshift] Datenbank, auf die Sie zugreifen. |

Weitere Informationen zu den ersten Schritten finden Sie in [diesem Redshift-Dokument](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

### Lesen von Beispiel-API-Aufrufen

In diesem Lernprogramm finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur [!DNL Experience Platform] Fehlerbehebung.

### Werte für erforderliche Kopfzeilen sammeln

Um [!DNL Platform] APIs aufzurufen, müssen Sie zunächst das [Authentifizierungslehrgang](../../../../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungtutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen [!DNL Experience Platform] API-Aufrufen bereit, wie unten dargestellt:

* Genehmigung: Träger `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform]und auch die der [!DNL Flow Service], werden zu bestimmten virtuellen Sandboxen isoliert. Alle Anforderungen an [!DNL Platform] APIs erfordern einen Header, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

* x-sandbox-name: `{SANDBOX_NAME}`

Für alle Anforderungen, die eine Payload enthalten (POST, PUT, PATCH), ist ein zusätzlicher Medientyp-Header erforderlich:

* Content-Type: `application/json`

## Verbindungsspezifikationen nachschlagen

Um eine [!DNL Redshift] Verbindung zu erstellen, muss eine Reihe von [!DNL Redshift] Verbindungsspezifikationen innerhalb von vorhanden sein [!DNL Flow Service]. Der erste Schritt beim Verbinden [!DNL Platform] mit [!DNL Redshift] ist das Abrufen dieser Spezifikationen.

**API-Format**

Jede verfügbare Quelle verfügt über einen eigenen Satz von Verbindungsspezifikationen, um Verbindungseigenschaften wie Authentifizierungsanforderungen zu beschreiben. Sie können Verbindungsspezifikationen nachschlagen, [!DNL Redshift] indem Sie eine GET-Anforderung ausführen und Abfragen-Parameter verwenden.

Beim Senden einer GET-Anforderung ohne Abfrage-Parameter werden Verbindungsspezifikationen für alle verfügbaren Quellen zurückgegeben. Sie können die Abfrage einbeziehen, `property=name=="amazon-redshift"` um Informationen speziell für [!DNL Redshift]Sie zu erhalten.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="amazon-redshift"
```

**Anfrage**

Die folgende Anforderung ruft die Verbindungsspezifikationen für [!DNL Redshift]ab.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="amazon-redshift"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Verbindungsspezifikationen für [!DNL Redshift]einschließlich der eindeutigen Kennung (`id`) zurück. Diese ID ist im nächsten Schritt erforderlich, um eine Basisverbindung zu erstellen.

```json
{
    "items": [
        {
            "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
            "name": "amazon-redshift",
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
                            "server": {
                                "type": "string",
                                "description": "IP address or host name of the Amazon Redshift server"
                            },
                            "username": {
                                "type": "string",
                                "description": "Name of user who has access to the database"
                            },
                            "password": {
                                "type": "string",
                                "description": "Password for the user account",
                                "format": "password"
                            },
                            "database": {
                                "type": "string",
                                "description": "Name of the Amazon Redshift database"
                            }
                        },
                        "required": [
                            "server",
                            "username",
                            "password",
                            "database"
                        ]
                    }
                }
            ]
        }
    ]
}
```

## Basisverbindung erstellen

Eine Basisverbindung gibt eine Quelle an und enthält Ihre Anmeldeinformationen für diese Quelle. Pro [!DNL Redshift] Konto ist nur eine Basisverbindung erforderlich, da diese zum Erstellen mehrerer Quell-Connectors verwendet werden kann, um verschiedene Daten einzubringen.

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
        "name": "amazon-redshift base connection",
        "description": "base connection for amazon-redshift,
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "server": "{SERVER}",
                "database": "{DATABASE}",
                "password": "{PASSWORD}",
                "username": "{USERNAME}"
            }
        },
        "connectionSpec": {
            "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| ------------- | --------------- |
| `auth.params.server` | Ihr [!DNL Redshift] Server. |
| `auth.params.database` | Die mit Ihrem [!DNL Redshift] Konto verknüpfte Datenbank. |
| `auth.params.password` | Das Ihrem [!DNL Redshift] Konto zugeordnete Kennwort. |
| `auth.params.username` | Der mit Ihrem [!DNL Redshift] Konto verknüpfte Benutzername. |
| `connectionSpec.id` | Die Verbindungsspezifikation `id` Ihres [!DNL Redshift] Kontos, die im vorherigen Schritt abgerufen wurde. |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Basisverbindung einschließlich ihrer eindeutigen Kennung (`id`) zurück. Diese ID ist erforderlich, um Ihre Daten im nächsten Lernprogramm zu untersuchen.

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

## Nächste Schritte

In diesem Lernprogramm haben Sie eine [!DNL Redshift] Basisverbindung mit der [!DNL Flow Service] API erstellt und den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese Basis-Verbindungs-ID im nächsten Lernprogramm verwenden, um zu erfahren, wie Sie Datenbanken oder NoSQL-Systeme mit der Flow Service API [erkunden können](../../explore/database-nosql.md).
