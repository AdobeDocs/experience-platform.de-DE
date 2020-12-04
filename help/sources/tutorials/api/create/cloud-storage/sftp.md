---
keywords: Experience Platform;home;popular topics;SFTP;sftp;Secure File Transfer Protocol;secure file transfer protocol
solution: Experience Platform
title: Erstellen eines SFTP-Connectors mit der Flow Service API
topic: overview
type: Tutorial
description: Dieses Lernprogramm verwendet die Flow Service API, um Sie durch die Schritte zum Herstellen einer Verbindung zwischen der Experience Platform und einem SFTP-Server (Secure File Transfer Protocol) zu führen.
translation-type: tm+mt
source-git-commit: 71653681a0f4b31319bd352202bf55fb3947a455
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 21%

---


# Erstellen eines SFTP-Connectors mit der [!DNL Flow Service] API

>[!NOTE]
>
>Der SFTP-Anschluss befindet sich in der Betaphase. Die Funktionen und Dokumentation können sich ändern. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../../../home.md#terms-and-conditions) Quellen.

[!DNL Flow Service] wird zur Erfassung und Zentralisierung von Kundendaten aus unterschiedlichen Quellen innerhalb von Adobe Experience Platform verwendet. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

Dieses Lernprogramm verwendet die [!DNL Flow Service] API, um Sie durch die Schritte zur Verbindung mit einem SFTP-Server (Secure File Transfer Protocol) [!DNL Experience Platform] zu führen.

Wenn Sie lieber die Benutzeroberfläche in verwenden möchten, [!DNL Experience Platform]enthält das [UI-Lernprogramm](../../../ui/create/cloud-storage/ftp-sftp.md) eine schrittweise Anleitung zum Durchführen ähnlicher Aktionen.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu verbessern.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

The following sections provide additional information that you will need to know in order to successfully connect to an SFTP server using the [!DNL Flow Service] API.

### Erforderliche Anmeldedaten sammeln

Damit eine Verbindung [!DNL Flow Service] zu SFTP hergestellt werden kann, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

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

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to the [!DNL Flow Service], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* x-sandbox-name: `{SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* Content-Type: `application/json`

## Verbindung erstellen

Eine Verbindung gibt eine Quelle an und enthält Ihre Anmeldeinformationen für diese Quelle. Pro SFTP-Konto ist nur eine Verbindung erforderlich, da sie zum Erstellen mehrerer Quell-Connectors verwendet werden kann, um verschiedene Daten einzubringen.

### Erstellen einer SFTP-Verbindung mit einfacher Authentifizierung

Wenn Sie eine SFTP-Verbindung mit einfacher Authentifizierung erstellen möchten, fordern Sie eine POST bei der [!DNL Flow Service] API an, während Sie Werte für die Verbindungen `host`, `userName`und `password`angeben.

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

Um eine SFTP-Verbindung mit der SSH-Authentifizierung mit öffentlichem Schlüssel zu erstellen, fordern Sie eine POST bei der [!DNL Flow Service] API an und geben Sie Werte für die Verbindungen `host`, `userName`, `privateKeyContent`und `passPhrase`an.

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

In diesem Lernprogramm haben Sie eine SFTP-Verbindung mit der [!DNL Flow Service] API erstellt und den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese Verbindungs-ID verwenden, um Cloud-Datenspeicherung mithilfe der Flow Service API [zu](../../explore/cloud-storage.md) untersuchen oder Parkettdaten mithilfe der Flow Service API [zu erfassen](../../cloud-storage-parquet.md).
