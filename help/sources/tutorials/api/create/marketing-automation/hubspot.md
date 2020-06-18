---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines HubSpot-Connectors mit der Flow Service API
topic: overview
translation-type: tm+mt
source-git-commit: 7328226b8349ffcdddadbd27b74fc54328b78dc5
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 1%

---


# Erstellen eines HubSpot-Connectors mit der Flow Service API

>[!NOTE]
>Der HubSpot-Anschluss befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../../../home.md#terms-and-conditions) Quellen.

Mit dem Flow Service werden Kundendaten aus unterschiedlichen Quellen innerhalb der Adobe Experience Platform erfasst und zentralisiert. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

Dieses Lernprogramm verwendet die Flow Service API, um Sie durch die Schritte zu führen, mit denen Sie die Experience Platform mit HubSpot verbinden.

## Erste Schritte

Dieses Handbuch erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Platformen zu strukturieren, zu beschriften und zu verbessern.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxen, die eine Instanz einer Platform in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der Flow Service API eine erfolgreiche Verbindung zu HubSpot herzustellen.

### Erforderliche Berechtigungen erfassen

Damit der Flow-Dienst eine Verbindung mit HubSpot herstellen kann, müssen Sie die folgenden Verbindungseigenschaften bereitstellen:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| Client-ID | Die mit Ihrer HubSpot-Anwendung verknüpfte Client-ID. |
| geheimer Clientschlüssel | Das mit Ihrer HubSpot-Anwendung verknüpfte Client-Geheimnis. |
| Zugriffstoken | Das Zugriffstoken, das beim erstmaligen Authentifizieren der OAuth-Integration erhalten wurde. |
| Token aktualisieren | Das Aktualisierungstoken, das beim erstmaligen Authentifizieren der OAuth-Integration erhalten wurde. |
| Verbindungs-ID | Die eindeutige Kennung, die zum Erstellen einer Verbindung erforderlich ist. Die Verbindungsspezifikations-ID für HubSpot lautet: `cc6a4487-9e91-433e-a3a3-9cf6626c1806` |

Weitere Informationen zum Einstieg finden Sie in diesem [HubSpot-Dokument](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

### Lesen von Beispiel-API-Aufrufen

In diesem Lernprogramm finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt [zum Lesen von Beispiel-API-Aufrufen](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung bei Experience Platformen.

### Werte für erforderliche Kopfzeilen sammeln

Um Platformen-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungslehrgang](../../../../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungtutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform API-Aufrufen bereit, wie unten dargestellt:

* Genehmigung: Träger `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle in der Experience Platform vorhandenen Ressourcen, einschließlich der Ressourcen des Flow-Dienstes, werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an Platform-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

* x-sandbox-name: `{SANDBOX_NAME}`

Für alle Anforderungen, die eine Payload enthalten (POST, PUT, PATCH), ist ein zusätzlicher Medientyp-Header erforderlich:

* Content-Type: `application/json`

## Verbindung herstellen

Eine Verbindung gibt eine Quelle an und enthält Ihre Anmeldeinformationen für diese Quelle. Pro HubSpot-Konto ist nur eine Verbindung erforderlich, da sie zum Erstellen mehrerer Quell-Connectors verwendet werden kann, um verschiedene Daten einzubringen.

**API-Format**

```https
POST /connections
```

**Anfrage**

Um eine HubSpot-Verbindung zu erstellen, muss die eindeutige Verbindungs-ID als Teil der POST-Anforderung angegeben werden. Die Verbindungs-ID für HubSpot ist `cc6a4487-9e91-433e-a3a3-9cf6626c1806`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "connection for hubspot",
        "description": "connection for hubspot",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "version": "1.0"
        }
    }
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.clientId` | Die mit Ihrer HubSpot-Anwendung verknüpfte Client-ID. |
| `auth.params.clientSecret` | Das mit Ihrer HubSpot-Anwendung verknüpfte Client-Geheimnis. |
| `auth.params.accessToken` | Das Zugriffstoken, das beim erstmaligen Authentifizieren der OAuth-Integration erhalten wurde. |
| `auth.params.refreshToken` | Das Aktualisierungstoken, das beim erstmaligen Authentifizieren der OAuth-Integration erhalten wurde. |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Verbindung für die API zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Lernprogramm zu untersuchen.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

In diesem Lernprogramm haben Sie eine HubSpot-Verbindung mit der Flow Service API erstellt und den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese Verbindungs-ID im nächsten Lernprogramm verwenden, um zu erfahren, wie Sie Marketingautomatisierungssysteme mithilfe der Flow Service API [untersuchen](../../explore/marketing-automation.md).