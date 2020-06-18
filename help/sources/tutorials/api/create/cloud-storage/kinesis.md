---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Amazon Kinesis-Connectors mithilfe der Flow Service API
topic: overview
translation-type: tm+mt
source-git-commit: 855f543a1cef394d121502f03471a60b97eae256
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 2%

---


# Erstellen eines Amazon Kinesis-Connectors mithilfe der Flow Service API

>[!NOTE]
>Der Amazon Kineses Connector befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../../../home.md#terms-and-conditions) Quellen.

Mit dem Flow Service werden Kundendaten aus unterschiedlichen Quellen innerhalb der Adobe Experience Platform erfasst und zentralisiert. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

In diesem Lernprogramm wird die Flow Service API verwendet, um Sie durch die Schritte zu führen, mit denen Sie die Experience Platform mit einem Amazon Kinesis-Konto verbinden.

## Erste Schritte

Dieses Handbuch erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Platformen zu strukturieren, zu beschriften und zu verbessern.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxen, die eine Instanz einer Platform in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der Flow Service API eine erfolgreiche Verbindung zu einem Amazon Kinesis-Konto herzustellen.

### Erforderliche Berechtigungen erfassen

Damit der Flow-Dienst eine Verbindung zu Ihrem Amazon Kinesis-Konto herstellen kann, müssen Sie Werte für die folgenden Verbindungseigenschaften bereitstellen:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `accessKeyId` | Die Zugriffsschlüssel-ID für Ihr Kinesis-Konto. |
| `secretKey` | Der geheime Zugriffsschlüssel für Ihr Kinesis-Konto. |
| `region` |  | Die Region für Ihr Kinesis-Konto. |
| `connectionSpec.id` | Die Spezifikations-ID der Kinesis-Verbindung: `86043421-563b-46ec-8e6c-e23184711bf6` |

Weitere Informationen zu diesen Werten finden Sie in [diesem Kinesis Dokument](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html).

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

Eine Verbindung gibt eine Quelle an und enthält Ihre Anmeldeinformationen für diese Quelle. Pro Amazon Kinesis-Konto ist nur eine Verbindung erforderlich, da sie zum Erstellen mehrerer Quell-Connectors verwendet werden kann, um verschiedene Daten einzubringen.

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
        "name": "Amazon Kinesis connection",
        "description": "Connector for Amazon Kinesis",
        "auth": {
            "specName": "Basic Authentication for Kinesis",
            "params": {
                "accessKeyId": "accessKeyId",
                "secretKey": "secretKey"
            }
        },
        "connectionSpec": {
            "id": "86043421-563b-46ec-8e6c-e23184711bf6",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.accessKeyId` | Die Zugriffsschlüssel-ID für Ihr Kinesis-Konto. |
| `auth.params.secretKey` | Der geheime Zugriffsschlüssel für Ihr Kinesis-Konto. |
| `auth.params.region` | Die Region für Ihr Kinesis-Konto. |
| `connectionSpec.id` | Die Spezifikations-ID der Kinesis-Verbindung: `86043421-563b-46ec-8e6c-e23184711bf6` |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Verbindung zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihre Cloud-Datenspeicherung-Daten im nächsten Lernprogramm zu untersuchen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Nächste Schritte

In diesem Lernprogramm haben Sie eine Amazon-Kinesis-Verbindung mit APIs erstellt und eine eindeutige ID als Teil des Antwortkörpers erhalten. Mit dieser Verbindungs-ID können Sie Cloud-Datenspeicherung mithilfe der Flow Service API [untersuchen](../../explore/cloud-storage.md).