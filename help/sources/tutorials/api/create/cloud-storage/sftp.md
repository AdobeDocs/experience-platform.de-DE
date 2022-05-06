---
keywords: Experience Platform; Startseite; beliebte Themen; SFTP; SFTP; Secure File Transfer Protocol; Secure File Transfer Protocol
solution: Experience Platform
title: Erstellen einer SFTP-Basisverbindung mit der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit einem SFTP-Server (Secure File Transfer Protocol) verbinden.
exl-id: b965b4bf-0b55-43df-bb79-c89609a9a488
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 32%

---

# Erstellen Sie eine SFTP-Basisverbindung mit der [!DNL Flow Service] API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL SFTP] (Secure File Transfer Protocol) unter Verwendung des [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

>[!IMPORTANT]
>
>Es wird empfohlen, beim Erfassen von JSON-Objekten mit einer [!DNL SFTP] Quellverbindung. Um die Beschränkung zu umgehen, verwenden Sie ein einzelnes JSON-Objekt pro Zeile und verwenden mehrere Zeilen für die darauf folgenden Dateien.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um eine erfolgreiche Verbindung zu einer [!DNL SFTP] Server, der [!DNL Flow Service] API.

### Sammeln erforderlicher Anmeldeinformationen

Um [!DNL Flow Service] mit [!DNL SFTP] zu verbinden, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `host` | Der Name oder die IP-Adresse, die mit Ihrer [!DNL SFTP] Server. |
| `port` | Der SFTP-Server-Port, mit dem Sie eine Verbindung herstellen. Wenn der Wert nicht angegeben wird, wird standardmäßig `22`. |
| `username` | Der Benutzername mit Zugriff auf Ihre [!DNL SFTP] Server. |
| `password` | Das Kennwort für Ihre [!DNL SFTP] Server. |
| `privateKeyContent` | Der Base64-kodierte Inhalt mit privatem SSH-Schlüssel. Der Typ des OpenSSH-Schlüssels muss entweder als RSA oder als DSA klassifiziert werden. |
| `passPhrase` | Der Ausdruck oder das Kennwort zum Entschlüsseln des privaten Schlüssels, wenn die Schlüsseldatei oder der Schlüsselinhalt durch einen Pass-Satz geschützt ist. Wenn die Variable `privateKeyContent` kennwortgeschützt ist, muss dieser Parameter mit der Passphrase des privaten Schlüsselinhalts als Wert verwendet werden. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL SFTP] ist: `b7bf2577-4520-42c9-bae9-cad01560f7bc`. |

### Verwenden von Platform-APIs

Informationen zum Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL SFTP]-Authentifizierungsdaten als Teil der Anfrageparameter an.

### Erstellen Sie eine [!DNL SFTP] Basisverbindung mit einfacher Authentifizierung

So erstellen Sie eine [!DNL SFTP] Basisverbindung mit einfacher Authentifizierung, stellen Sie eine POST-Anfrage an die [!DNL Flow Service] API beim Bereitstellen von Werten für die `host`, `userName`und `password`.

**API-Format**

```http
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL SFTP] einfache Authentifizierung verwenden:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.host` | Der Hostname Ihres SFTP-Servers. |
| `auth.params.username` | Der Benutzername, der Ihrem SFTP-Server zugeordnet ist. |
| `auth.params.password` | Das Ihrem SFTP-Server zugeordnete Kennwort. |
| `connectionSpec.id` | Die Spezifikations-ID der SFTP-Server-Verbindung: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Verbindung. Diese ID ist erforderlich, um Ihren SFTP-Server im nächsten Tutorial zu untersuchen.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

### Erstellen Sie eine [!DNL SFTP] Basisverbindung mit SSH-Authentifizierung für öffentlichen Schlüssel

So erstellen Sie eine [!DNL SFTP] Basisverbindung mit Authentifizierung mit dem öffentlichen SSH-Schlüssel, stellen Sie eine POST-Anfrage an die [!DNL Flow Service] API beim Bereitstellen von Werten für die `host`, `userName`, `privateKeyContent`und `passPhrase`.

>[!IMPORTANT]
>
>Die [!DNL SFTP] Connector unterstützt einen OpenSSH-Schlüssel vom Typ RSA oder DSA. Stellen Sie sicher, dass der Inhalt Ihrer Schlüsseldatei mit `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` und endet mit `"-----END [RSA/DSA] PRIVATE KEY-----"`. Wenn es sich bei der privaten Schlüsseldatei um eine PPK-Datei handelt, verwenden Sie das PuTTY-Tool, um von PPK in das OpenSSH-Format zu konvertieren.

**API-Format**

```http
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL SFTP] Verwenden der Authentifizierung mit dem öffentlichen SSH-Schlüssel:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.host` | Der Hostname Ihres [!DNL SFTP] Server. |
| `auth.params.username` | Der Benutzername, der mit Ihrer [!DNL SFTP] Server. |
| `auth.params.privateKeyContent` | Der Base64-kodierte Inhalt mit privatem SSH-Schlüssel. Der Typ des OpenSSH-Schlüssels muss entweder als RSA oder als DSA klassifiziert werden. |
| `auth.params.passPhrase` | Der Ausdruck oder das Kennwort zum Entschlüsseln des privaten Schlüssels, wenn die Schlüsseldatei oder der Schlüsselinhalt durch einen Pass-Satz geschützt ist. Wenn PrivateKeyContent kennwortgeschützt ist, muss dieser Parameter mit der Passphrase von PrivateKeyContent als Wert verwendet werden. |
| `connectionSpec.id` | Die [!DNL SFTP] Spezifikations-ID der Serververbindung: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Verbindung. Diese ID ist erforderlich, um Ihre [!DNL SFTP] -Server im nächsten Tutorial.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL SFTP] Verbindung mithilfe der [!DNL Flow Service] API verwenden und den eindeutigen ID-Wert der Verbindung erhalten haben. Sie können diese Verbindungs-ID verwenden, um [Erkunden von Cloud-Speichern mithilfe der Flow Service-API](../../explore/cloud-storage.md).
