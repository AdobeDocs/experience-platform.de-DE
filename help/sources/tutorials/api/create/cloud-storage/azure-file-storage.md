---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen Sie einen Azurblase-Datenspeicherung-Connector mit der Flow-Dienst-API
topic: overview
translation-type: tm+mt
source-git-commit: c843ebb72ee3f1e8d2233dd2be4021403417813b
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 1%

---


# Erstellen Sie einen Azurblase-Datenspeicherung-Connector mit der Flow-Dienst-API

>[!NOTE]
>Der Azurblase File Datenspeicherung Stecker ist in Beta. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../../../home.md#terms-and-conditions) Quellen.

Mit dem Flow Service werden Kundendaten aus unterschiedlichen Quellen innerhalb der Adobe Experience Platform erfasst und zentralisiert. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

In diesem Lernprogramm wird die Flow Service API verwendet, um Sie durch die Schritte zu führen, um die Datenspeicherung der Azurblauen Datei mit der Experience Platform zu verbinden.

## Erste Schritte

Dieses Handbuch erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Platformen zu strukturieren, zu beschriften und zu verbessern.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxen, die eine Instanz einer Platform in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mit der Flow Service API eine Verbindung zur Azurblauen Datenspeicherung herzustellen.

### Erforderliche Berechtigungen erfassen

Damit der Flow-Dienst eine Verbindung mit der Azur-Datei-Datenspeicherung herstellen kann, müssen Sie Werte für die folgenden Verbindungseigenschaften bereitstellen:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `host` | Der Endpunkt der Azurblauen Dateiinstanz, auf die Sie zugreifen. |
| `userId` | Der Benutzer hat ausreichend Zugriff auf den Datenspeicherung-Endpunkt der Azurblauen Datei. |
| `password` | Das Kennwort für die Datenspeicherung der Azurblase-Datei |
| Verbindungs-ID | Die eindeutige Kennung, die zum Erstellen einer Verbindung erforderlich ist. Die Verbindungsspezifikations-ID für die Datenspeicherung von Azurblase-Dateien lautet: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |

Weitere Informationen zu den ersten Schritten finden Sie in [diesem Dokument](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows)der Azurblauen Datei-Datenspeicherung.

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

Eine Verbindung gibt eine Quelle an und enthält Ihre Anmeldeinformationen für diese Quelle. Für jedes Blue File Datenspeicherung-Konto ist nur eine Verbindung erforderlich, da sie zur Erstellung mehrerer Quellschnittstellen verwendet werden kann, um verschiedene Daten einzubringen.

**API-Format**

```http
POST /connections
```

**Anfrage**

Mit der folgenden Anforderung wird eine neue Azurblase-Datenspeicherung erstellt, die von den in der Payload bereitgestellten Eigenschaften konfiguriert wird:


```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
        -d '{
        "name": "Azure File Storage connection",
        "description": "An Azure File Storage test connection",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST}",
                    "userId": "{USER_ID}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| --------- | ----------- |
| `auth.params.host` | Der Endpunkt der Azurblauen Dateiinstanz, auf die Sie zugreifen... |
| `auth.params.userId` | Der Benutzer hat ausreichend Zugriff auf den Datenspeicherung-Endpunkt der Azurblauen Datei. |
| `auth.params.password` | Die Azurblase-Datenspeicherung-Zugriffsschlüssel. |
| `connectionSpec.id` | Verbindungsspezifikations-ID für die Datenspeicherung der Azurblu-Datei: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Verbindung zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Lernprogramm zu untersuchen.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie mit der Flow-Dienst-API eine Datenspeicherung für die &quot;Blaue Datei&quot;erstellt und den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese ID im nächsten Lernprogramm verwenden, um zu erfahren, wie Sie eine Cloud-Datenspeicherung von Drittanbietern mithilfe der Flow Service API [untersuchen](../../explore/cloud-storage.md).
