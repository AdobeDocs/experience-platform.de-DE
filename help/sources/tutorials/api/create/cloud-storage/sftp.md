---
title: Erstellen einer SFTP-Basisverbindung mit der Flow Service-API
description: Erfahren Sie, wie Sie mit der Flow Service-API eine Verbindung zwischen Adobe Experience Platform und einem SFTP-Server (Secure File Transfer Protocol) herstellen.
exl-id: b965b4bf-0b55-43df-bb79-c89609a9a488
source-git-commit: f6d1cc811378f2f37968bf0a42b428249e52efd8
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 28%

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

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um eine erfolgreiche Verbindung zu einer [!DNL SFTP] -Server, der [!DNL Flow Service] API.

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
| `maxConcurrentConnections` | Mit diesem Parameter können Sie eine maximale Anzahl gleichzeitiger Verbindungen festlegen, die Platform beim Herstellen einer Verbindung zu Ihrem SFTP-Server erstellt. Sie müssen festlegen, dass dieser Wert kleiner als der von SFTP festgelegte Grenzwert ist. **Hinweis**: Wenn diese Einstellung für ein vorhandenes SFTP-Konto aktiviert ist, betrifft sie nur zukünftige Datenflüsse und nicht vorhandene Datenflüsse. |
| `folderPath` | Der Pfad zu dem Ordner, auf den Sie Zugriff gewähren möchten. [!DNL SFTP] -Quelle können Sie den Ordnerpfad angeben, um den Benutzerzugriff auf den Unterordner Ihrer Wahl anzugeben. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL SFTP] ist: `b7bf2577-4520-42c9-bae9-cad01560f7bc`. |

### Verwenden von Platform-APIs

Informationen zum Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung

>[!TIP]
>
>Nach der Erstellung können Sie den Authentifizierungstyp eines [!DNL SFTP] Basisverbindung. Um den Authentifizierungstyp zu ändern, müssen Sie eine neue Basisverbindung erstellen.

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Die [!DNL SFTP] -Quelle unterstützt sowohl einfache Authentifizierung als auch Authentifizierung über einen öffentlichen SSH-Schlüssel. Während dieses Schritts können Sie auch den Pfad zum Unterordner angeben, auf den Sie Zugriff gewähren möchten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den `/connections`-Endpunkt beim Bereitstellen der [!DNL SFTP]-Authentifizierungsberechtigungsdaten als Teil der Anfrageparameter.

>[!IMPORTANT]
>
>Die [!DNL SFTP] Connector unterstützt einen OpenSSH-Schlüssel vom Typ RSA oder DSA. Stellen Sie sicher, dass der Inhalt Ihrer Schlüsseldatei mit `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` und endet mit `"-----END [RSA/DSA] PRIVATE KEY-----"`. Wenn es sich bei der privaten Schlüsseldatei um eine PPK-Datei handelt, verwenden Sie das PuTTY-Tool, um von PPK in das OpenSSH-Format zu konvertieren.

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
              "folderPath": "acme/business/customers/holidaySales"
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
| `auth.params.port` | Der Port des SFTP-Servers. Dieser ganzzahlige Wert ist standardmäßig auf 22 festgelegt. |
| `auth.params.username` | Der Benutzername, der Ihrem SFTP-Server zugeordnet ist. |
| `auth.params.password` | Das Ihrem SFTP-Server zugeordnete Kennwort. |
| `auth.params.maxConcurrentConnections` | Die maximale Anzahl gleichzeitiger Verbindungen, die beim Verbinden von Platform mit SFTP angegeben wird. Wenn diese Option aktiviert ist, muss dieser Wert auf mindestens 1 gesetzt werden. |
| `auth.params.folderPath` | Der Pfad zu dem Ordner, auf den Sie Zugriff gewähren möchten. |
| `connectionSpec.id` | Die Spezifikations-ID der SFTP-Server-Verbindung: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

+++

+++Antwort

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Verbindung. Diese ID ist erforderlich, um Ihren SFTP-Server im nächsten Tutorial zu untersuchen.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

+++

>[!TAB Authentifizierung mit öffentlichen SSH-Schlüsseln]

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
              "folderPath": "acme/business/customers/holidaySales"
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
| `auth.params.port` | Der Port des SFTP-Servers. Dieser ganzzahlige Wert ist standardmäßig auf 22 festgelegt. |
| `auth.params.username` | Der mit Ihrer [!DNL SFTP] Server. |
| `auth.params.privateKeyContent` | Der Base64-kodierte Inhalt mit privatem SSH-Schlüssel. Der Typ des OpenSSH-Schlüssels muss entweder als RSA oder als DSA klassifiziert werden. |
| `auth.params.passPhrase` | Der Ausdruck oder das Kennwort zum Entschlüsseln des privaten Schlüssels, wenn die Schlüsseldatei oder der Schlüsselinhalt durch einen Pass-Satz geschützt ist. Wenn PrivateKeyContent kennwortgeschützt ist, muss dieser Parameter mit der Passphrase von PrivateKeyContent als Wert verwendet werden. |
| `auth.params.maxConcurrentConnections` | Die maximale Anzahl gleichzeitiger Verbindungen, die beim Verbinden von Platform mit SFTP angegeben wird. Wenn diese Option aktiviert ist, muss dieser Wert auf mindestens 1 gesetzt werden. |
| `auth.params.folderPath` | Der Pfad zu dem Ordner, auf den Sie Zugriff gewähren möchten. |
| `connectionSpec.id` | Die [!DNL SFTP] Spezifikations-ID der Serververbindung: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

+++

+++Antwort

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Verbindung. Diese ID ist erforderlich, um Ihren SFTP-Server im nächsten Tutorial zu untersuchen.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

+++

>[!ENDTABS]

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL SFTP] Verbindung mithilfe der [!DNL Flow Service] API verwenden und den eindeutigen ID-Wert der Verbindung erhalten haben. Sie können diese Verbindungs-ID verwenden, um [Erkunden von Cloud-Speichern mithilfe der Flow Service-API](../../explore/cloud-storage.md).
