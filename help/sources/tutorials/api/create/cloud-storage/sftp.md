---
keywords: Experience Platform;home;beliebte Themen;SFTP;sftp;Secure File Transfer Protocol;Secure File Transfer Protocol
solution: Experience Platform
title: Erstellen Sie eine SFTP-Basisverbindung mithilfe der Flow Service API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service API mit einem SFTP-Server (Secure File Transfer Protocol) verbinden.
exl-id: b965b4bf-0b55-43df-bb79-c89609a9a488
source-git-commit: 13bd1254dfe89004465174a7532b4f6aaef54c09
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 7%

---

# Erstellen Sie eine SFTP-Basisverbindung mit [!DNL Flow Service] API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL SFTP] (Secure File Transfer Protocol) mit [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Plattformdiensten zu strukturieren, zu kennzeichnen und zu verbessern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

>[!IMPORTANT]
>
>Es wird empfohlen, beim Erfassen von JSON-Objekten mit einer [!DNL SFTP] Quellverbindung. Um die Beschränkung zu umgehen, verwenden Sie ein einzelnes JSON-Objekt pro Zeile und verwenden mehrere Zeilen, um Dateien zu hinterlassen.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um erfolgreich eine Verbindung zu einer [!DNL SFTP] Server, der [!DNL Flow Service] API.

### Erforderliche Anmeldedaten sammeln

In der Reihenfolge [!DNL Flow Service] Verbindung herstellen zu [!DNL SFTP], müssen Sie Werte für die folgenden Verbindungseigenschaften bereitstellen:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `host` | Der Name oder die IP-Adresse, die Ihrer/Ihrem [!DNL SFTP] Server. |
| `port` | Der SFTP-Serveranschluss, mit dem Sie eine Verbindung herstellen. Wenn nicht angegeben, wird der Wert standardmäßig auf `22`. |
| `username` | Der Benutzername mit Zugriff auf Ihre [!DNL SFTP] Server. |
| `password` | Das Kennwort für Ihre [!DNL SFTP] Server. |
| `privateKeyContent` | Der Base64-kodierte Inhalt mit privatem SSH-Schlüssel. Der Typ des OpenSSH-Schlüssels muss als RSA oder DSA klassifiziert werden. |
| `passPhrase` | Der Ausdruck oder das Kennwort &quot;Kennwort übergeben&quot;, um den privaten Schlüssel zu entschlüsseln, wenn die Schlüsseldatei oder der Schlüsselinhalt durch einen Passphrase geschützt ist. Wenn `privateKeyContent` kennwortgeschützt ist, muss dieser Parameter mit der Passphrase des privaten Schlüssels als Wert verwendet werden. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Verbindungseigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für das Erstellen der Basis- und Quellverbindungen. Verbindungsspezifikations-ID für [!DNL SFTP] ist: `b7bf2577-4520-42c9-bae9-cad01560f7bc`. |

### Verwenden von Plattform-APIs

Informationen dazu, wie Sie erfolgreich Aufrufe von Plattform-APIs durchführen, finden Sie im Handbuch zu [Erste Schritte mit Plattform-APIs](../../../../../landing/api-guide.md).

## Basisverbindung erstellen

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Plattform gespeichert, einschließlich der Authentifizierungsinformationen Ihrer Quelle, des aktuellen Zustands der Verbindung und Ihrer eindeutigen Basis-Verbindungs-ID. Die Basis-Verbindungs-ID ermöglicht es Ihnen, Dateien von der Quelle aus zu erkunden und zu navigieren und die spezifischen Elemente zu identifizieren, die Sie aufnehmen möchten, einschließlich Informationen zu den Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST an `/connections` Endpunkt beim Bereitstellen von [!DNL SFTP] Authentifizierungsdaten als Teil der Anforderungsparameter.

### Erstellen Sie eine [!DNL SFTP] Basisverbindung mit einfacher Authentifizierung

So erstellen Sie [!DNL SFTP] Basisverbindung mit einfacher Authentifizierung, stellen Sie eine POST an [!DNL Flow Service] API bei Angabe von Werten für die `host`, `userName`und `password`.

**API-Format**

```http
POST /connections
```

**Anfrage**

Die folgende Anforderung erstellt eine Basisverbindung für [!DNL SFTP] einfache Authentifizierung verwenden:

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
| `auth.params.username` | Der Ihrem SFTP-Server zugeordnete Benutzername. |
| `auth.params.password` | Das mit Ihrem SFTP-Server verknüpfte Kennwort. |
| `connectionSpec.id` | Spezifikations-ID für die SFTP-Serververbindung: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung zurück (`id`) der neu erstellten Verbindung. Diese ID ist erforderlich, um Ihren SFTP-Server im nächsten Tutorial zu erkunden.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

### Erstellen Sie eine [!DNL SFTP] Basisverbindung mit Authentifizierung mit öffentlichem SSH-Schlüssel

So erstellen Sie [!DNL SFTP] Basisverbindung mit Authentifizierung mit öffentlichem SSH-Schlüssel erstellen Sie eine POST an [!DNL Flow Service] API bei Angabe von Werten für die `host`, `userName`, `privateKeyContent`und `passPhrase`.

>[!IMPORTANT]
>
>Die [!DNL SFTP] Connector unterstützt einen RSA- oder DSA-Schlüssel vom Typ OpenSSH. Stellen Sie sicher, dass Ihre Schlüsseldateiinhalte Beginn mit `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` und endet mit `"-----END [RSA/DSA] PRIVATE KEY-----"`. Wenn es sich bei der Datei mit privatem Schlüssel um eine PPK-Datei handelt, verwenden Sie das PuTTY-Tool, um von PPK in das OpenSSH-Format zu konvertieren.

**API-Format**

```http
POST /connections
```

**Anfrage**

Die folgende Anforderung erstellt eine Basisverbindung für [!DNL SFTP] Authentifizierung mit öffentlichem SSH-Schlüssel verwenden:

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
| `auth.params.host` | Der Hostname von [!DNL SFTP] Server. |
| `auth.params.username` | Der Ihrem/r [!DNL SFTP] Server. |
| `auth.params.privateKeyContent` | Der Base64-kodierte Inhalt mit privatem SSH-Schlüssel. Der Typ des OpenSSH-Schlüssels muss als RSA oder DSA klassifiziert werden. |
| `auth.params.passPhrase` | Der Ausdruck oder das Kennwort &quot;Kennwort übergeben&quot;, um den privaten Schlüssel zu entschlüsseln, wenn die Schlüsseldatei oder der Schlüsselinhalt durch einen Passphrase geschützt ist. Wenn PrivateKeyContent kennwortgeschützt ist, muss dieser Parameter mit der Passphrase von PrivateKeyContent als Wert verwendet werden. |
| `connectionSpec.id` | Die [!DNL SFTP] Spezifikations-ID der Serververbindung: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung zurück (`id`) der neu erstellten Verbindung. Diese ID ist erforderlich, um Ihre [!DNL SFTP] Server im nächsten Tutorial.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL SFTP] Verbindung mit [!DNL Flow Service] API und den eindeutigen ID-Wert der Verbindung erhalten haben. Sie können diese Verbindungs-ID verwenden, um [Cloud-Datenspeicherung mithilfe der Flow Service API erkunden](../../explore/cloud-storage.md).
