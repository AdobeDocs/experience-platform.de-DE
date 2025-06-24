---
title: Erstellen einer SFTP-Basisverbindung mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit einem SFTP-Server (Secure File Transfer Protocol) verbinden.
exl-id: b965b4bf-0b55-43df-bb79-c89609a9a488
source-git-commit: 4816a6b627dc6551e351bfe3cdc4bc8c8ea8b17e
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 14%

---

# Erstellen einer SFTP-Basisverbindung mithilfe der [!DNL Flow Service]-API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL SFTP] (Secure File Transfer Protocol) mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

>[!IMPORTANT]
>
>Es wird empfohlen, bei der Aufnahme von JSON-Objekten mit einer [!DNL SFTP] Quellverbindung Zeilenumbrüche oder Zeilenumbrüche zu vermeiden. Um die Einschränkung zu umgehen, verwenden Sie ein einzelnes JSON-Objekt pro Zeile und verwenden Sie mehrere Zeilen für nachfolgende Dateien.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service]-API eine Verbindung zu einem [!DNL SFTP]-Server herstellen zu können.

### Sammeln erforderlicher Anmeldedaten

Lesen Sie [[!DNL SFTP] Authentifizierungshandbuch](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials), um ausführliche Schritte zum Abrufen Ihrer Authentifizierungsdaten zu erhalten.

### Verwenden von Experience Platform-APIs

Informationen zum erfolgreichen Aufrufen von Experience Platform-APIs finden Sie im Handbuch unter [ mit Experience Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung

>[!TIP]
>
>Nach der Erstellung können Sie den Authentifizierungstyp einer [!DNL SFTP] Basisverbindung nicht mehr ändern. Um den Authentifizierungstyp zu ändern, müssen Sie eine neue Basisverbindung erstellen.

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Experience Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen ID der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Die [!DNL SFTP]-Quelle unterstützt sowohl die einfache Authentifizierung als auch die Authentifizierung über einen öffentlichen SSH-Schlüssel. In diesem Schritt können Sie auch den Pfad zu dem Unterordner festlegen, auf den Sie Zugriff gewähren möchten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den `/connections`-Endpunkt beim Bereitstellen der [!DNL SFTP]-Authentifizierungs-Anmeldedaten als Teil der Anfrageparameter.

>[!IMPORTANT]
>
>Der [!DNL SFTP]-Connector unterstützt OpenSSH-Schlüssel vom Typ `ed25519`, `RSA` oder `DSA`. Stellen Sie sicher, dass Ihr Schlüsseldateiinhalt mit `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` beginnt und mit `"-----END [RSA/DSA] PRIVATE KEY-----"` endet. Wenn es sich bei der privaten Schlüsseldatei um eine Datei im PPK-Format handelt, verwenden Sie das PuTTY-Tool, um von PPK in das OpenSSH-Format zu konvertieren.

**API-Format**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Einfache Authentifizierung]

+++Anfrage

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
              "port": 22,
              "userName": "{USERNAME}",
              "password": "{PASSWORD}",
              "maxConcurrentConnections": 5,
              "folderPath": "acme/business/customers/holidaySales",
              "disableChunking": "true"
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
| `auth.params.host` | Der Host-Name Ihres SFTP-Servers. |
| `auth.params.port` | Der Port des SFTP-Servers Der Standardwert für diese Ganzzahl ist 22. |
| `auth.params.username` | Der Benutzername, der Ihrem SFTP-Server zugeordnet ist. |
| `auth.params.password` | Das mit Ihrem SFTP-Server verknüpfte Kennwort. |
| `auth.params.maxConcurrentConnections` | Die maximale Anzahl gleichzeitiger Verbindungen, die beim Verbinden von Experience Platform mit SFTP angegeben wird. Wenn dieser Wert aktiviert ist, muss er auf mindestens 1 gesetzt werden. |
| `auth.params.folderPath` | Der Pfad zum Ordner, auf den Sie Zugriff gewähren möchten. |
| `auth.params.disableChunking` | Ein boolescher Wert, der bestimmt, ob der SFTP-Server die Unterteilung unterstützt oder nicht. |
| `connectionSpec.id` | Die SFTP-Server-Verbindungsspezifikations-ID: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

+++

+++Antwort

Bei einer erfolgreichen Antwort wird die eindeutige Kennung (`id`) der neu erstellten Verbindung zurückgegeben. Diese ID ist erforderlich, um Ihren SFTP-Server im nächsten Tutorial zu untersuchen.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

+++

>[!TAB SSH-Authentifizierung mit öffentlichem Schlüssel]

+++Anfrage

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
              "port": 22,
              "userName": "{USERNAME}",
              "privateKeyContent": "{PRIVATE_KEY_CONTENT}",
              "passPhrase": "{PASSPHRASE}",
              "maxConcurrentConnections": 5,
              "folderPath": "acme/business/customers/holidaySales",
              "disableChunking": "true"
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
| `auth.params.host` | Der Hostname Ihres [!DNL SFTP]. |
| `auth.params.port` | Der Port des SFTP-Servers Der Standardwert für diese Ganzzahl ist 22. |
| `auth.params.username` | Der Benutzername, der Ihrem [!DNL SFTP]-Server zugeordnet ist. |
| `auth.params.privateKeyContent` | Der Base64-kodierte Inhalt des privaten SSH-Schlüssels. Die unterstützten OpenSSH-Schlüsseltypen sind `ed25519`, `RSA` und `DSA`. |
| `auth.params.passPhrase` | Die Passphrase oder das Passwort zum Entschlüsseln des privaten Schlüssels, wenn die Schlüsseldatei oder der Schlüsselinhalt durch eine Passphrase geschützt ist. Wenn PrivateKeyContent kennwortgeschützt ist, muss dieser Parameter mit der Passphrase von PrivateKeyContent als Wert verwendet werden. |
| `auth.params.maxConcurrentConnections` | Die maximale Anzahl gleichzeitiger Verbindungen, die beim Verbinden von Experience Platform mit SFTP angegeben wird. Wenn dieser Wert aktiviert ist, muss er auf mindestens 1 gesetzt werden. |
| `auth.params.folderPath` | Der Pfad zum Ordner, auf den Sie Zugriff gewähren möchten. |
| `auth.params.disableChunking` | Ein boolescher Wert, der bestimmt, ob der SFTP-Server die Unterteilung unterstützt oder nicht. |
| `connectionSpec.id` | Die Spezifikations-ID der [!DNL SFTP]-Server-Verbindung: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

+++

+++Antwort

Bei einer erfolgreichen Antwort wird die eindeutige Kennung (`id`) der neu erstellten Verbindung zurückgegeben. Diese ID ist erforderlich, um Ihren SFTP-Server im nächsten Tutorial zu untersuchen.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

+++

>[!ENDTABS]

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL SFTP] mithilfe der [!DNL Flow Service]-API erstellt und den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese Verbindungs-ID verwenden, um [Cloud-Speicher mithilfe der Flow Service-API zu ](../../explore/cloud-storage.md).
