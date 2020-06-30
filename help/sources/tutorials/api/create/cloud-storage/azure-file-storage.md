---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen Sie einen Azurblase-Datenspeicherung-Connector mit der Flow-Dienst-API
topic: overview
translation-type: tm+mt
source-git-commit: 11431ffcfc2204931fe3e863bfadc7878a40b49c
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 2%

---


# Erstellen eines [!DNL Azure File Storage] Connectors mit der [!DNL Flow Service] API

>[!NOTE]
>Der [!DNL Azure File Storage] Anschluss befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../../../home.md#terms-and-conditions) Quellen.

[!DNL Flow Service] dient zur Erfassung und Zentralisierung von Kundendaten aus unterschiedlichen Quellen innerhalb der Adobe Experience Platform. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

Dieses Lernprogramm verwendet die [!DNL Flow Service] API, um Sie durch die Schritte zu führen, mit denen Sie eine Verbindung herstellen [!DNL Azure File Storage] können [!DNL Experience Platform].

## Erste Schritte

Dieses Handbuch erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu verbessern.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um eine Verbindung mit [!DNL Azure File Storage] der [!DNL Flow Service] API herstellen zu können.

### Erforderliche Berechtigungen erfassen

Damit eine Verbindung [!DNL Flow Service] zu [!DNL Azure File Storage]hergestellt werden kann, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `host` | Der Endpunkt der [!DNL Azure File Storag]Instanz, auf die Sie zugreifen. |
| `userId` | Der Benutzer mit ausreichendem Zugriff auf den [!DNL Azure File Storage] Endpunkt. |
| `password` | Das Kennwort für Ihre [!DNL Azure File Storage] Instanz |
| Verbindungs-ID | Die eindeutige Kennung, die zum Erstellen einer Verbindung erforderlich ist. Die Verbindungsspezifikations-ID für [!DNL Azure File Storage] lautet: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |

Weitere Informationen zu den ersten Schritten finden Sie in [diesem Dokument](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows)der Azurblauen Datei-Datenspeicherung.

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

## Verbindung herstellen

Eine Verbindung gibt eine Quelle an und enthält Ihre Anmeldeinformationen für diese Quelle. Für jedes Blue File Datenspeicherung-Konto ist nur eine Verbindung erforderlich, da sie zur Erstellung mehrerer Quellschnittstellen verwendet werden kann, um verschiedene Daten einzubringen.

**API-Format**

```http
POST /connections
```

**Anfrage**

Die folgende Anforderung erstellt eine neue [!DNL Azure File Storage] Verbindung, die von den in der Payload bereitgestellten Eigenschaften konfiguriert wird:


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
| `auth.params.host` | Der Endpunkt der [!DNL Azure File Storage] Instanz, auf die Sie zugreifen. |
| `auth.params.userId` | Der Benutzer mit ausreichendem Zugriff auf den [!DNL Azure File Storage] Endpunkt. |
| `auth.params.password` | Der [!DNL Azure File Storage] Zugriffsschlüssel. |
| `connectionSpec.id` | Die [!DNL Azure File Storage] Verbindungs-ID: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Verbindung zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Lernprogramm zu untersuchen.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## Nächste Schritte

In diesem Lernprogramm haben Sie eine [!DNL Azure File Storage] Verbindung mit der [!DNL Flow Service] API erstellt und den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese ID im nächsten Lernprogramm verwenden, um zu erfahren, wie Sie eine Cloud-Datenspeicherung von Drittanbietern mithilfe der Flow Service API [untersuchen](../../explore/cloud-storage.md).
