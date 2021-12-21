---
keywords: Experience Platform; Startseite; beliebte Themen; Greenplum; Greenplum
solution: Experience Platform
title: Erstellen einer GreenPlum-Basisverbindung mit der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Flow Service-API eine Verbindung von GreenPlum mit Adobe Experience Platform herstellen.
exl-id: c4ce452a-b4c5-46ab-83ab-61b296c271d0
source-git-commit: bdc9b78666c3f67cd8794d132515fda5698c81ac
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 10%

---

# Erstellen Sie eine [!DNL GreenPlum] Basisverbindung mit [!DNL Flow Service] API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL GreenPlum] mithilfe der [[!DNL Flow Service] API](https://docs.greenplum.org/6-7/security-guide/topics/Authenticate.html).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten zu strukturieren, zu beschriften und zu erweitern, indem Sie [!DNL Platform] Dienste.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um eine erfolgreiche Verbindung zu [!DNL GreenPlum] mithilfe der [!DNL Flow Service] API.

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `connectionString` | Die Verbindungszeichenfolge, über die die Verbindung zu Ihrem [!DNL GreenPlum] -Instanz. Das Verbindungszeichenfolgenmuster für [!DNL GreenPlum] is `HOST={SERVER};PORT={PORT};DB={DATABASE};UID={USERNAME};PWD={PASSWORD}` |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL GreenPlum] is `37b6bf40-d318-4655-90be-5cd6f65d334b`. |

Weitere Informationen zum Akquise einer Verbindungszeichenfolge finden Sie unter [dieses GreenPlum-Dokument](https://docs.greenplum.org/6-7/security-guide/topics/Authenticate.html).

### Verwenden von Platform-APIs

Informationen zum erfolgreichen Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Basisverbindung erstellen

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an die `/connections` Endpunkt beim Bereitstellen [!DNL GreenPlum] Authentifizierungsberechtigungen als Teil der Anfrageparameter.

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL GreenPlum]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "GreenPlum test connection",
        "description": "A test connection for a GreenPlum source",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "connectionString": "HOST={SERVER};PORT={PORT};DB={DATABASE};UID={USERNAME};PWD={PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "37b6bf40-d318-4655-90be-5cd6f65d334b",
            "version": "1.0"
        }
    }'
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `auth.params.connectionString` | Die Verbindungszeichenfolge, mit der eine Verbindung zu einem [!DNL GreenPlum] -Konto. Das Verbindungszeichenfolgenmuster lautet: `HOST={SERVER};PORT={PORT};DB={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | Die [!DNL GreenPlum] Verbindungsspezifikations-ID: `37b6bf40-d318-4655-90be-5cd6f65d334b`. |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Verbindung zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Tutorial zu untersuchen.

```json
{
    "id": "575abae5-c99a-452c-9aba-e5c99ac52c4d",
    "etag": "\"e5012c89-0000-0200-0000-5eaa036b0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL GreenPlum] Verbindung mithilfe der [!DNL Flow Service] API und haben den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese ID im nächsten Tutorial verwenden, während Sie lernen, wie Sie [Datenbanken mithilfe der Flow Service-API analysieren](../../explore/database-nosql.md).
