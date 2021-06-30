---
keywords: Experience Platform; Startseite; beliebte Themen; SFTP; SFTP; Secure File Transfer Protocol; Secure File Transfer Protocol
solution: Experience Platform
title: Erstellen einer SFTP-Basisverbindung mit der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mit der Flow Service-API eine Verbindung zwischen Adobe Experience Platform und einem SFTP-Server (Secure File Transfer Protocol) herstellen.
exl-id: b965b4bf-0b55-43df-bb79-c89609a9a488
source-git-commit: 59a8e2aa86508e53f181ac796f7c03f9fcd76158
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 8%

---

# Erstellen einer SFTP-Basisverbindung mit der [!DNL Flow Service]-API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL SFTP] (Secure File Transfer Protocol) mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Platform-Diensten zu strukturieren, zu beschriften und zu erweitern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

>[!IMPORTANT]
>
>Es wird empfohlen, beim Erfassen von JSON-Objekten mit einer [!DNL SFTP]-Quellverbindung Zeilenumbrüche oder Zeilenumbrüche zu vermeiden. Um die Beschränkung zu umgehen, verwenden Sie ein einzelnes JSON-Objekt pro Zeile und verwenden mehrere Zeilen für die darauf folgenden Dateien.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service]-API erfolgreich eine Verbindung zu einem [!DNL SFTP]-Server herstellen zu können.

### Erforderliche Anmeldedaten sammeln

Damit [!DNL Flow Service] eine Verbindung zu [!DNL SFTP] herstellen kann, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `host` | Der Name oder die IP-Adresse, die mit Ihrem [!DNL SFTP]-Server verknüpft ist. |
| `username` | Der Benutzername mit Zugriff auf Ihren [!DNL SFTP]-Server. |
| `password` | Das Kennwort für Ihren [!DNL SFTP]-Server. |
| `privateKeyContent` | Der Base64-kodierte Inhalt mit privatem SSH-Schlüssel. Der Typ des OpenSSH-Schlüssels muss entweder als RSA oder als DSA klassifiziert werden. |
| `passPhrase` | Der Ausdruck oder das Kennwort zum Entschlüsseln des privaten Schlüssels, wenn die Schlüsseldatei oder der Schlüsselinhalt durch einen Pass-Satz geschützt ist. Wenn `privateKeyContent` kennwortgeschützt ist, muss dieser Parameter mit der Passphrase des privaten Schlüsselinhalts als Wert verwendet werden. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL SFTP] lautet: `b7bf2577-4520-42c9-bae9-cad01560f7bc`. |

### Verwenden von Platform-APIs

Informationen dazu, wie Sie erfolgreich Aufrufe an Platform-APIs durchführen können, finden Sie im Handbuch [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Basisverbindung erstellen

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL SFTP]-Authentifizierungsdaten als Teil der Anfrageparameter an.

### Erstellen einer [!DNL SFTP]-Verbindung mithilfe einer einfachen Authentifizierung

Um eine [!DNL SFTP]-Basisverbindung mit Standardauthentifizierung zu erstellen, stellen Sie eine POST-Anfrage an die [!DNL Flow Service]-API und geben Sie dabei Werte für `host`, `userName` und `password` an.

**API-Format**

```http
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL SFTP] mithilfe der einfachen Authentifizierung:

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
| `auth.params.host` | Der Hostname Ihres SFTP-Servers. |
| `auth.params.username` | Der Benutzername, der Ihrem SFTP-Server zugeordnet ist. |
| `auth.params.password` | Das Ihrem SFTP-Server zugeordnete Kennwort. |
| `connectionSpec.id` | Die Spezifikations-ID der SFTP-Server-Verbindung: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Verbindung zurück. Diese ID ist erforderlich, um Ihren SFTP-Server im nächsten Tutorial zu untersuchen.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

### Erstellen einer Verbindung [!DNL SFTP] mithilfe der Authentifizierung mit einem öffentlichen SSH-Schlüssel

Um eine [!DNL SFTP]-Basisverbindung mit der Authentifizierung mit öffentlichen SSH-Schlüsseln zu erstellen, stellen Sie eine POST-Anfrage an die [!DNL Flow Service]-API und geben Sie dabei Werte für `host`, `userName`, `privateKeyContent` und `passPhrase` an.

>[!IMPORTANT]
>
>Der Connector [!DNL SFTP] unterstützt einen OpenSSH-Schlüssel vom Typ RSA oder DSA. Stellen Sie sicher, dass der Inhalt Ihrer Schlüsseldatei mit `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` beginnt und mit `"-----END [RSA/DSA] PRIVATE KEY-----"` endet. Wenn es sich bei der privaten Schlüsseldatei um eine PPK-Datei handelt, verwenden Sie das PuTTY-Tool, um von PPK in das OpenSSH-Format zu konvertieren.

**API-Format**

```http
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL SFTP] mithilfe der Authentifizierung mit dem öffentlichen SSH-Schlüssel:

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
| `auth.params.host` | Der Hostname Ihres [!DNL SFTP]-Servers. |
| `auth.params.username` | Der Benutzername, der Ihrem [!DNL SFTP]-Server zugeordnet ist. |
| `auth.params.privateKeyContent` | Der Base64-kodierte Inhalt mit privatem SSH-Schlüssel. Der Typ des OpenSSH-Schlüssels muss entweder als RSA oder als DSA klassifiziert werden. |
| `auth.params.passPhrase` | Der Ausdruck oder das Kennwort zum Entschlüsseln des privaten Schlüssels, wenn die Schlüsseldatei oder der Schlüsselinhalt durch einen Pass-Satz geschützt ist. Wenn PrivateKeyContent kennwortgeschützt ist, muss dieser Parameter mit der Passphrase von PrivateKeyContent als Wert verwendet werden. |
| `connectionSpec.id` | Die Kennung der Serververbindungsspezifikation [!DNL SFTP]: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Verbindung zurück. Diese ID ist erforderlich, um Ihren [!DNL SFTP]-Server im nächsten Tutorial zu untersuchen.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL SFTP]-Verbindung mit der [!DNL Flow Service]-API erstellt und den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese Verbindungs-ID verwenden, um [Cloud-Speicher mithilfe der Flow Service-API](../../explore/cloud-storage.md) oder [Ermitteln von Parquet-Daten mithilfe der Flow Service-API](../../cloud-storage-parquet.md) zu untersuchen.
