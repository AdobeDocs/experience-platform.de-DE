---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Apache Cassandra-Connectors mithilfe der Flow Service API
topic: overview
translation-type: tm+mt
source-git-commit: accbb95234085c7c1969e9fecc4f5db52426c8b7
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 3%

---


# Erstellen eines Apache Cassandra-Connectors mithilfe der Flow Service API

Mit dem Flow-Dienst werden Kundendaten aus verschiedenen Quellen innerhalb der Adobe Experience Platform erfasst und zentralisiert. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

Dieses Lernprogramm verwendet die Flow Service API, um Sie durch die Schritte zu führen, die notwendig sind, um Apache Cassandra (im Folgenden &quot;Cassandra&quot; genannt) mit der Experience Platform zu verbinden.

## Erste Schritte

Dieses Handbuch erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

* [Quellen](../../../../home.md): Mit Experience Platform können Daten aus verschiedenen Quellen erfasst werden, während Sie gleichzeitig die Möglichkeit haben, eingehende Daten mithilfe von Plattformdiensten zu strukturieren, zu beschriften und zu verbessern.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Plattforminstanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mit der Flow Service API eine erfolgreiche Verbindung zu Cassandra herzustellen.

### Erforderliche Berechtigungen erfassen

Damit der Flow-Dienst eine Verbindung mit Cassandra herstellen kann, müssen Sie Werte für die folgenden Verbindungseigenschaften bereitstellen:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `host` | Die IP-Adresse oder der Hostname des Cassandra-Servers. |
| `port` | Der TCP-Anschluss, den der Cassandra-Server verwendet, um auf Clientverbindungen zu warten. Der Standard-Port ist `9042`. |
| `username` | Der Benutzername, mit dem eine Verbindung zum Cassandra-Server zur Authentifizierung hergestellt wird. |
| `password` | Das Kennwort zum Herstellen einer Verbindung zum Cassandra-Server zur Authentifizierung. |
| `connectionSpec.id` | Die eindeutige Kennung, die zum Erstellen einer Verbindung erforderlich ist. Die Verbindungs-ID für Cassandra ist `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

Weitere Informationen zum Einstieg finden Sie in [diesem Cassandra-Dokument](https://cassandra.apache.org/doc/latest/operating/security.html#authentication).

### Lesen von Beispiel-API-Aufrufen

In diesem Lernprogramm finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

### Werte für erforderliche Kopfzeilen sammeln

Um Aufrufe an Plattform-APIs durchzuführen, müssen Sie zunächst das [Authentifizierungstraining](../../../../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungstreutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform API-Aufrufen bereit, wie unten dargestellt:

* Genehmigung: Träger `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in Experience Platform, einschließlich der Ressourcen des Flow-Dienstes, werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an Plattform-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

* x-sandbox-name: `{SANDBOX_NAME}`

Für alle Anforderungen, die eine Payload enthalten (POST, PUT, PATCH), ist ein zusätzlicher Medientyp-Header erforderlich:

* Content-Type: `application/json`

## Verbindung herstellen

Eine Verbindung gibt eine Quelle an und enthält Ihre Anmeldeinformationen für diese Quelle. Pro Cassandra-Konto ist nur ein Connector erforderlich, da er zur Erstellung mehrerer Quell-Connectors verwendet werden kann, um verschiedene Daten einzubringen.

**API-Format**

```http
POST /connections
```

**Anfrage**

Um eine Cassandra-Verbindung zu erstellen, muss die eindeutige Verbindungs-ID als Teil der POST-Anforderung angegeben werden. Die Verbindungs-ID für Cassandra ist `a8f4d393-1a6b-43f3-931f-91a16ed857f4`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Cassandra test connection",
        "description": "A test connection for Cassandra",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST},
                    "port": "{PORT}",
                    "username": "{USERNAME}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "a8f4d393-1a6b-43f3-931f-91a16ed857f4",
            "version": "1.0"
        }
    }'
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `auth.params.host` | Die IP-Adresse oder der Hostname des Cassandra-Servers. |
| `auth.params.port` | Der TCP-Anschluss, den der Cassandra-Server verwendet, um auf Clientverbindungen zu warten. Der Standard-Port ist `9042`. |
| `auth.params.username` | Der Benutzername, mit dem eine Verbindung zum Cassandra-Server zur Authentifizierung hergestellt wird. |
| `auth.params.password` | Das Kennwort zum Herstellen einer Verbindung zum Cassandra-Server zur Authentifizierung. |
| `connectionSpec.id` | Die Cassandra-Verbindungsspezifikations-ID: `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Verbindung zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Lernprogramm zu untersuchen.

```json
{
    "id": "ce69aa89-1baa-4054-a9aa-891baa605425",
    "etag": "\"5a026e19-0000-0200-0000-5eac76d00000\""
}
```

## Nächste Schritte

In diesem Lernprogramm haben Sie eine Cassandra-Verbindung mit der Flow Service API erstellt und den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese ID im nächsten Lernprogramm verwenden, um zu erfahren, wie Sie Datenbanken mithilfe der Flow Service API [untersuchen](../../explore/database-nosql.md).
