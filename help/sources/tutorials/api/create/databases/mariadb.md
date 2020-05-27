---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines MariaDB-Connectors mit der Flow Service API
topic: overview
translation-type: tm+mt
source-git-commit: 0a2247a9267d4da481b3f3a5dfddf45d49016e61
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 2%

---


# Erstellen eines MariaDB-Connectors mit der Flow Service API

>[!NOTE]
>Der MariaDB-Anschluss befindet sich in der Betaphase. Die Funktionen und Dokumentation können sich ändern.

Mit dem Flow-Dienst werden Kundendaten aus verschiedenen Quellen innerhalb der Adobe Experience Platform erfasst und zentralisiert. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

In diesem Lernprogramm wird die Flow Service API verwendet, um Sie durch die Schritte zur Verbindung von Experience Platform mit MariaDB zu führen.

## Erste Schritte

Dieses Handbuch erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

* [Quellen](../../../../home.md): Mit Experience Platform können Daten aus verschiedenen Quellen erfasst werden, während Sie gleichzeitig die Möglichkeit haben, eingehende Daten mithilfe von Plattformdiensten zu strukturieren, zu beschriften und zu verbessern.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Plattforminstanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der Flow Service API eine erfolgreiche Verbindung zu MariaDB herzustellen.

### Erforderliche Berechtigungen erfassen

Damit der Flow-Dienst eine Verbindung zu MariaDB herstellen kann, müssen Sie die folgende Verbindungseigenschaft angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `connectionString` | Die mit Ihrer MariaDB-Authentifizierung verknüpfte Verbindungszeichenfolge. Das Muster für die MariaDB-Verbindungszeichenfolge lautet: `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | Die ID, mit der eine Verbindung generiert wird. Die feste Verbindungs-spec-ID für MariaDB ist `3000eb99-cd47-43f3-827c-43caf170f015`. |

Weitere Informationen zum Abrufen einer Verbindungszeichenfolge finden Sie in [diesem MariaDB-Dokument](https://mariadb.com/kb/en/about-mariadb-connector-odbc/).

### Lesen von Beispiel-API-Aufrufen

In diesem Lernprogramm finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

### Werte für erforderliche Kopfzeilen sammeln

Um Aufrufe an Plattform-APIs durchführen zu können, müssen Sie zunächst das [Authentifizierungslehrgang](../../../../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungstreutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform API-Aufrufen bereit, wie unten dargestellt:

* Genehmigung: Träger `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in Experience Platform, einschließlich der Ressourcen des Flow-Dienstes, werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an Plattform-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

* x-sandbox-name: `{SANDBOX_NAME}`

Für alle Anforderungen, die eine Payload enthalten (POST, PUT, PATCH), ist ein zusätzlicher Medientyp-Header erforderlich:

* Content-Type: `application/json`

## Verbindung herstellen

Eine Verbindung gibt eine Quelle an und enthält Ihre Anmeldeinformationen für diese Quelle. Pro MariaDB-Konto ist nur eine Verbindung erforderlich, da sie zum Erstellen mehrerer Quell-Connectors verwendet werden kann, um verschiedene Daten einzubringen.

**API-Format**

```http
POST /connections
```

**Anfrage**

Um eine MariaDB-Verbindung zu erstellen, muss die eindeutige Verbindungs-Spec-ID als Teil der POST-Anforderung angegeben werden. Die Verbindungsspezifikations-ID für MariaDB ist `3000eb99-cd47-43f3-827c-43caf170f015`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Test connection for maria-db",
        "description": "Test connection for maria-db",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "3000eb99-cd47-43f3-827c-43caf170f015",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.connectionString` | Die mit Ihrer MariaDB-Authentifizierung verknüpfte Verbindungszeichenfolge. Das Muster für die MariaDB-Verbindungszeichenfolge lautet: `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | Die MariaDB-Verbindungs-spec-ID lautet: `3000eb99-cd47-43f3-827c-43caf170f015`. |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Basisverbindung einschließlich ihrer eindeutigen Kennung (`id`) zurück. Diese ID ist erforderlich, um Ihre Datenbank im nächsten Schritt zu untersuchen.

```json
{
    "id": "be3a2d71-1fb6-4fea-ba2d-711fb61fea50",
    "etag": "\"02002624-0000-0200-0000-5e41f7040000\""
}
```

## Nächste Schritte

In diesem Lernprogramm haben Sie eine MariaDB-Verbindung mit der Flow Service API erstellt und den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese Verbindungs-ID im nächsten Lernprogramm verwenden, um zu erfahren, wie Sie Datenbanken oder NoSQL-Systeme mit der Flow Service API [erkunden können](../../explore/database-nosql.md).
