---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Google Cloud-Datenspeicherung-Connectors mithilfe der Flow Service API
topic: overview
translation-type: tm+mt
source-git-commit: 7ffe560f455973da3a37ad102fbb8cc5969d5043
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 2%

---


# Erstellen eines Google Cloud-Datenspeicherung-Connectors mithilfe der Flow Service API

Mit dem Flow-Dienst werden Kundendaten aus verschiedenen Quellen innerhalb der Adobe Experience Platform erfasst und zentralisiert. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

In diesem Lernprogramm wird die Flow Service API verwendet, um Sie durch die Schritte zur Verbindung von Experience Platform mit einem Google Cloud-Datenspeicherung-Konto zu führen.

## Erste Schritte

Dieses Handbuch erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

* [Quellen](../../../../home.md): Mit Experience Platform können Daten aus verschiedenen Quellen erfasst werden, während Sie gleichzeitig die Möglichkeit haben, eingehende Daten mithilfe von Plattformdiensten zu strukturieren, zu beschriften und zu verbessern.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Plattforminstanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der Flow Service API eine Verbindung zu einem Google Cloud-Datenspeicherung-Konto herstellen zu können.

### Erforderliche Berechtigungen erfassen

Damit der Flow-Dienst eine Verbindung zu Ihrem Google Cloud-Datenspeicherung-Konto herstellen kann, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `accessKeyId` | Die Zugriffsschlüssel-ID für Ihr Google Cloud-Datenspeicherung-Konto. |
| `secretAccessKey` | Der geheime Zugriffsschlüssel für Ihr Google Cloud-Datenspeicherung-Konto. |

Informationen zum Einstieg finden Sie in [diesem Google Cloud-Dokument](https://cloud.google.com/docs/authentication).

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

Eine Verbindung gibt eine Quelle an und enthält Ihre Anmeldeinformationen für diese Quelle. Pro Google Cloud-Datenspeicherung-Konto ist nur eine Verbindung erforderlich, da sie zum Erstellen mehrerer Quell-Connectors verwendet werden kann, um verschiedene Daten einzubringen.

**API-Format**

```http
POST /connections
```

**Anfrage**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google Cloud Storage connection",
        "description": "Connector for Google Cloud Storage",
        "auth": {
            "specName": "Basic Authentication for google-cloud",
            "params": {
                "accessKeyId": "accessKeyId",
                "secretAccessKey": "secretAccessKey"
            }
        },
        "connectionSpec": {
            "id": "32e8f412-cdf7-464c-9885-78184cb113fd",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.accessKeyId` | Die Zugriffsschlüssel-ID, die mit Ihrem Google Cloud-Datenspeicherung-Konto verknüpft ist. |
| `auth.params.secretAccessKey` | Der geheime Zugriffsschlüssel, der mit Ihrem Google Cloud-Datenspeicherung-Konto verknüpft ist. |
| `connectionSpec.id` | Die Google Cloud-Datenspeicherung-Verbindungs-ID: `32e8f412-cdf7-464c-9885-78184cb113fd` |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Verbindung zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihre Cloud-Datenspeicherung-Daten im nächsten Lernprogramm zu untersuchen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Nächste Schritte

In diesem Lernprogramm haben Sie eine Google Cloud-Datenspeicherung-Verbindung mit APIs erstellt und eine eindeutige ID als Teil des Antwortkörpers erhalten. Sie können diese Verbindungs-ID verwenden, um Cloud-Datenspeicherung mithilfe der Flow Service API [zu](../../explore/cloud-storage.md) untersuchen oder Parkettdaten mithilfe der Flow Service API [zu erfassen](../../cloud-storage-parquet.md).