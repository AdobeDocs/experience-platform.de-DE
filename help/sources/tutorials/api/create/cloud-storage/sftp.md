---
keywords: Experience Platform;Home;beliebte Themen;SFTP;sftp;Secure File Transfer Protocol;Secure File Transfer Protocol
solution: Experience Platform
title: Erstellen einer SFTP-Quellverbindung mit der Flow Service API
topic: Übersicht
type: Tutorial
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service API mit einem SFTP-Server (Secure File Transfer Protocol) verbinden.
translation-type: tm+mt
source-git-commit: b39426d768a0c6fdfa742ec74e4e0bed9c432269
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 21%

---


# Erstellen Sie eine SFTP-Quellverbindung mit der API [!DNL Flow Service]

>[!NOTE]
>
>Der SFTP-Anschluss befindet sich in der Betaphase. Die Funktionen und Dokumentation können sich ändern. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie unter [Sources overview](../../../../home.md#terms-and-conditions).

Dieses Lernprogramm verwendet die API [!DNL Flow Service], um Sie durch die Schritte zu führen, mit denen Sie die Experience Platform mit einem SFTP-Server (Secure File Transfer Protocol) verbinden.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Plattformdiensten zu strukturieren, zu kennzeichnen und zu verbessern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

>[!IMPORTANT]
>
>Es wird empfohlen, beim Einsetzen von JSON-Objekten mit einer SFTP-Quellverbindung Zeilenumbrüche oder Wagenrückgaben zu vermeiden. Um die Beschränkung zu umgehen, verwenden Sie ein einzelnes JSON-Objekt pro Zeile und verwenden Sie mehrere Zeilen für die anschließenden Dateien.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mit der API [!DNL Flow Service] erfolgreich eine Verbindung zu einem SFTP-Server herzustellen.

### Erforderliche Anmeldedaten sammeln

Damit [!DNL Flow Service] eine Verbindung zu SFTP herstellen kann, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `host` | Der Name oder die IP-Adresse, die mit Ihrem SFTP-Server verknüpft ist. |
| `username` | Der Benutzername mit Zugriff auf Ihren SFTP-Server. |
| `password` | Das Kennwort für Ihren SFTP-Server. |
| `privateKeyContent` | Der Base64-kodierte Inhalt mit privatem SSH-Schlüssel. Der Typ des OpenSSH-Schlüssels muss entweder als RSA oder als DSA klassifiziert werden. |
| `passPhrase` | Die Phrase oder das Kennwort zum Entschlüsseln des privaten Schlüssels, wenn die Schlüsseldatei oder der Schlüsselinhalt durch eine Phrase geschützt ist. Wenn PrivateKeyContent kennwortgeschützt ist, muss dieser Parameter mit der Passphrase von PrivateKeyContent als Wert verwendet werden. |

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

### Sammeln von Werten für erforderliche Kopfzeilen

Um Platform-APIs aufrufen zu können, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://www.adobe.com/go/platform-api-authentication-en) abschließen. Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform], einschließlich derjenigen, die zu [!DNL Flow Service] gehören, werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an [!DNL Platform]-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird in:

* `x-sandbox-name: {SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* `Content-Type: application/json`

## Verbindung erstellen

Eine Verbindung gibt eine Quelle an und enthält Ihre Anmeldeinformationen für diese Quelle. Es ist nur eine Verbindung erforderlich, da sie zur Erstellung mehrerer Datenflüsse verwendet werden kann, um verschiedene Daten einzubringen.

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

>[!IMPORTANT]
>
>Der SFTP-Connector unterstützt einen RSA- oder DSA-Typ OpenSSH-Schlüssel. Stellen Sie sicher, dass der Inhalt der Schlüsseldatei mit `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` und mit `"-----END [RSA/DSA] PRIVATE KEY-----"` endet. Wenn es sich bei der privaten Schlüsseldatei um eine PPK-Datei handelt, verwenden Sie das PuTTY-Tool, um das PPK in das OpenSSH-Format zu konvertieren.

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
| `auth.params.privateKeyContent` | Der Base64-kodierte Inhalt mit privatem SSH-Schlüssel. Der Typ des OpenSSH-Schlüssels muss entweder als RSA oder als DSA klassifiziert werden. |
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

In diesem Lernprogramm haben Sie eine SFTP-Verbindung mit der API [!DNL Flow Service] erstellt und den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese Verbindungs-ID verwenden, um Cloud-Datenspeicherung mithilfe der Flow Service API](../../explore/cloud-storage.md) oder [zu erfassen. Verwenden Sie dazu die Flussdienst-API](../../cloud-storage-parquet.md).[
