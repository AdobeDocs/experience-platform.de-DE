---
keywords: Experience Platform;home;popular topics; File Transfer Protocol; file transfer protocol
solution: Experience Platform
title: Erstellen eines FTP-Connectors mit der Flow Service API
topic: overview
type: Tutorial
description: Dieses Lernprogramm verwendet die Flow Service API, um Sie durch die Schritte zum Herstellen einer Verbindung zwischen Experience Platform und FTP-Server (File Transfer Protocol) zu führen.
translation-type: tm+mt
source-git-commit: 807b3110606daa6b8d42d2f9048668f7c121c8f4
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 28%

---


# Erstellen eines FTP-Connectors mit der [!DNL Flow Service] API

>[!NOTE]
>
>Der FTP-Anschluss befindet sich in der Betaphase. Die Funktionen und Dokumentation können sich ändern. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../../../home.md#terms-and-conditions) Quellen.

Dieses Lernprogramm verwendet die [!DNL Flow Service] API, um Sie durch die Schritte zur Verbindung mit einem FTP-Server (File Transfer Protocol) [!DNL Experience Platform] zu führen.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu verbessern.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

The following sections provide additional information that you will need to know in order to successfully connect to an FTP server using the [!DNL Flow Service] API.

### Erforderliche Anmeldedaten sammeln

Damit eine Verbindung [!DNL Flow Service] zu FTP hergestellt werden kann, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `host` | Der Name oder die IP-Adresse, die mit Ihrem FTP-Server verknüpft ist. |
| `username` | Der Benutzername mit Zugriff auf Ihren FTP-Server. |
| `password` | Das Kennwort für Ihren FTP-Server. |

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](../../../../../tutorials/authentication.md) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to the [!DNL Flow Service], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* `x-sandbox-name: {SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* `Content-Type: application/json`

## Verbindung erstellen

Eine Verbindung gibt eine Quelle an und enthält Ihre Anmeldeinformationen für diese Quelle. Pro FTP-Konto ist nur eine Verbindung erforderlich, da sie zum Erstellen mehrerer Quell-Connectors verwendet werden kann, um verschiedene Daten einzubringen.

### Erstellen einer FTP-Verbindung mit einfacher Authentifizierung

Wenn Sie eine FTP-Verbindung mit einfacher Authentifizierung erstellen möchten, fordern Sie eine POST bei der [!DNL Flow Service] API an, während Sie Werte für die Verbindung `host`, `userName`und `password`angeben.

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
        "name": "FTP connector with password",
        "description": "FTP connector password",
        "auth": {
            "specName": "Basic Authentication for FTP",
            "params": {
                "host": "{HOST}",
                "userName": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.host` | Der Hostname des FTP-Servers. |
| `auth.params.username` | Der mit Ihrem FTP-Server verknüpfte Benutzername. |
| `auth.params.password` | Das Ihrem FTP-Server zugeordnete Kennwort. |
| `connectionSpec.id` | Die FTP-Server-Verbindungs-ID: `fb2e94c9-c031-467d-8103-6bd6e0a432f2` |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Verbindung zurück. Diese ID ist erforderlich, um Ihren FTP-Server im nächsten Lernprogramm zu untersuchen.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Nächste Schritte

In diesem Lernprogramm haben Sie eine FTP-Verbindung mit der [!DNL Flow Service] API erstellt und den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese Verbindungs-ID verwenden, um Cloud-Datenspeicherung mithilfe der Flow Service API [zu](../../explore/cloud-storage.md) untersuchen oder Parkettdaten mithilfe der Flow Service API [zu erfassen](../../cloud-storage-parquet.md).
