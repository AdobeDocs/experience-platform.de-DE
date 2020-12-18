---
keywords: Experience Platform;home;popular topics;SFTP;sftp;Secure File Transfer Protocol;secure file transfer protocol
solution: Experience Platform
title: Erstellen eines SFTP-Connectors mit der Flow Service API
topic: overview
type: Tutorial
description: Dieses Lernprogramm verwendet die Flow Service API, um Sie durch die Schritte zum Herstellen einer Verbindung zwischen der Experience Platform und einem SFTP-Server (Secure File Transfer Protocol) zu führen.
translation-type: tm+mt
source-git-commit: 9092c3d672967d3f6f7bf7116c40466a42e6e7b1
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 24%

---


# Erstellen Sie einen SFTP-Connector mit der API [!DNL Flow Service]

>[!NOTE]
>
>Der SFTP-Anschluss befindet sich in der Betaphase. Die Funktionen und Dokumentation können sich ändern. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie unter [Sources overview](../../../../home.md#terms-and-conditions).

Dieses Lernprogramm verwendet die API [!DNL Flow Service], um Sie durch die Schritte zu führen, mit denen Sie die Experience Platform mit einem SFTP-Server (Secure File Transfer Protocol) verbinden.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Plattformdiensten zu strukturieren, zu kennzeichnen und zu verbessern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mit der API [!DNL Flow Service] erfolgreich eine Verbindung zu einem SFTP-Server herzustellen.

### Erforderliche Anmeldedaten sammeln

Damit [!DNL Flow Service] eine Verbindung zu SFTP herstellen kann, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `host` | Der Name oder die IP-Adresse, die mit Ihrem SFTP-Server verknüpft ist. |
| `username` | Der Benutzername mit Zugriff auf Ihren SFTP-Server. |
| `password` | Das Kennwort für Ihren SFTP-Server. |
| `privateKeyContent` | Der Base64-kodierte Inhalt mit privatem SSH-Schlüssel. Das Format des privaten SSH-Schlüssels OpenSSH (RSA/DSA). |
| `passPhrase` | Die Phrase oder das Kennwort zum Entschlüsseln des privaten Schlüssels, wenn die Schlüsseldatei oder der Schlüsselinhalt durch eine Phrase geschützt ist. Wenn PrivateKeyContent kennwortgeschützt ist, muss dieser Parameter mit der Passphrase von PrivateKeyContent als Wert verwendet werden. |

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](../../../../../tutorials/authentication.md) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform], einschließlich derjenigen, die zu [!DNL Flow Service] gehören, werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an [!DNL Platform]-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird in:

* `x-sandbox-name: {SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* `Content-Type: application/json`

## Verbindung erstellen

Eine Verbindung gibt eine Quelle an und enthält Ihre Anmeldeinformationen für diese Quelle. Pro SFTP-Konto ist nur eine Verbindung erforderlich, da sie zum Erstellen mehrerer Quell-Connectors verwendet werden kann, um verschiedene Daten einzubringen.

### Erstellen einer SFTP-Verbindung mit einfacher Authentifizierung

Um eine SFTP-Verbindung mit einfacher Authentifizierung zu erstellen, fordern Sie eine POST an die [!DNL Flow Service]-API an, während Sie Werte für `host`, `userName` und `password` angeben.

**API-Format**

```http
POST /connections
```

**Anfrage**

Um eine SFTP-Verbindung zu erstellen, muss die eindeutige Verbindungs-ID als Teil der POST-Anfrage angegeben werden. Die Verbindungs-Spezifikations-ID für SFTP ist `b7bf2577-4520-42c9-bae9-cad01560f7bc`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d  '{
        "name": "SFTP connector with password",
        "description": "SFTP connector password",
        "auth": {
            "specName": "Basic Authentication for sftp",
            "params": {
                "host": "{HOST}",
                "userName": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "b7bf2577-4520-42c9-bae9-cad01560f7bc",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.host` | Der Hostname des SFTP-Servers. |
| `auth.params.username` | Der mit Ihrem SFTP-Server verknüpfte Benutzername. |
| `auth.params.password` | Das Ihrem SFTP-Server zugeordnete Kennwort. |
| `connectionSpec.id` | Die SFTP-Server-Verbindungs-ID: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Verbindung zurück. Diese ID ist erforderlich, um Ihren SFTP-Server im nächsten Lernprogramm zu erkunden.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

### Erstellen einer SFTP-Verbindung mit einer SSH-Authentifizierung mit öffentlichem Schlüssel

Um eine SFTP-Verbindung mit der SSH-Authentifizierung mit öffentlichem Schlüssel zu erstellen, fordern Sie eine POST an die [!DNL Flow Service]-API an, während Sie Werte für `host`, `userName`, `privateKeyContent` und `passPhrase` angeben.

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
        "name": "SFTP connector with SSH authentication",
        "description": "SFTP connector with SSH authentication",
        "auth": {
            "specName": "SSH PublicKey Authentication for sftp",
            "params": {
                "host": "{HOST}",
                "userName": "{USERNAME}",
                "privateKeyContent": "{PRIVATE_KEY_CONTENT}",
                "passPhrase": "{PASSPHRASE}"
            }
        },
        "connectionSpec": {
            "id": "b7bf2577-4520-42c9-bae9-cad01560f7bc",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.host` | Der Hostname des SFTP-Servers. |
| `auth.params.username` | Der mit Ihrem SFTP-Server verknüpfte Benutzername. |
| `auth.params.privateKeyContent` | Der Base64-kodierte Inhalt mit privatem SSH-Schlüssel. Das Format des privaten SSH-Schlüssels OpenSSH (RSA/DSA). |
| `auth.params.passPhrase` | Die Phrase oder das Kennwort zum Entschlüsseln des privaten Schlüssels, wenn die Schlüsseldatei oder der Schlüsselinhalt durch eine Phrase geschützt ist. Wenn PrivateKeyContent kennwortgeschützt ist, muss dieser Parameter mit der Passphrase von PrivateKeyContent als Wert verwendet werden. |
| `connectionSpec.id` | Die SFTP-Server-Verbindungs-ID: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Verbindung zurück. Diese ID ist erforderlich, um Ihren SFTP-Server im nächsten Lernprogramm zu erkunden.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Nächste Schritte

In diesem Lernprogramm haben Sie eine SFTP-Verbindung mit der API [!DNL Flow Service] erstellt und den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese Verbindungs-ID verwenden, um Cloud-Datenspeicherung mithilfe der Flow Service API[ oder ](../../explore/cloud-storage.md)zu erfassen, indem Sie die Flussdienst-API[ verwenden.](../../cloud-storage-parquet.md)
