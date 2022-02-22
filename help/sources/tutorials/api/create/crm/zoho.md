---
keywords: Experience Platform; Startseite; beliebte Themen; Zoho CRM; Zoho crm; Zoho; Zoho
solution: Experience Platform
title: Erstellen einer Zoho CRM-Basisverbindung mit der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Flow Service-API Adobe Experience Platform mit dem Zoho-CRM verbinden.
exl-id: 33995927-8f5e-44c5-b809-4db8706bbd34
source-git-commit: 46b2fd6bc715bf1d8ccfeed576a2a2d193f92edd
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 8%

---

# Erstellen Sie eine [!DNL Zoho CRM] Basisverbindung mit [!DNL Flow Service] API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Zoho CRM] mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten zu strukturieren, zu beschriften und zu erweitern, indem Sie [!DNL Platform] Dienste.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um eine erfolgreiche Verbindung zu [!DNL Zoho CRM] mithilfe der [!DNL Flow Service] API.

### Erforderliche Anmeldedaten sammeln

Zur [!DNL Flow Service] zur Verbindung mit [!DNL Zoho CRM]müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| --- | --- |
| `endpoint` | Der Endpunkt der [!DNL Zoho CRM] -Server, an den Sie Ihre Anforderung senden. |
| `accountsUrl` | Die Konto-URL wird verwendet, um Ihre Zugriffs- und Aktualisierungstoken zu generieren. Die URL muss domänenspezifisch sein. |
| `clientId` | Die Client-ID, die Ihrer [!DNL Zoho CRM] Benutzerkonto. |
| `clientSecret` | Das Client-Geheimnis, das Ihrem [!DNL Zoho CRM] Benutzerkonto. |
| `accessToken` | Das Zugriffstoken autorisiert Ihren sicheren und temporären Zugriff auf Ihre [!DNL Zoho CRM] -Konto. |
| `refreshToken` | Ein Aktualisierungstoken ist ein Token, mit dem ein neues Zugriffstoken generiert wird, sobald Ihr Zugriffstoken abgelaufen ist. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Zoho CRM] ist: `929e4450-0237-4ed2-9404-b7e1e0a00309`. |

Weitere Informationen zu diesen Anmeldedaten finden Sie in der Dokumentation unter [[!DNL Zoho CRM] Authentifizierung](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

### Verwenden von Platform-APIs

Informationen zum erfolgreichen Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Basisverbindung erstellen

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an die `/connections` Endpunkt beim Bereitstellen [!DNL Zoho CRM] Authentifizierungsberechtigungen als Teil der Anfrageparameter.

**API-Format**

```https
POST /connections
```

**Anfrage**

>[!TIP]
>
>Ihre Konto-URL-Domäne muss mit Ihrem entsprechenden Domänen-Speicherort übereinstimmen. Im Folgenden finden Sie die verschiedenen Domänen und die zugehörigen Konto-URLs:<ul><li>Vereinigte Staaten: https://accounts.zoho.com</li><li>Australien: https://accounts.zoho.com.au</li><li>Europa: https://accounts.zoho.eu</li><li>Indien: https://accounts.zoho.in</li><li>China: https://accounts.zoho.com.cn</li></ul>

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Zoho CRM]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json'
    -d '{
        "name": "Zoho CRM base connection",
        "description": "Base Connection for Zoho CRM",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "endpoint": "{ENDPOINT}",
                "accountsUrl": "{ACCOUNTS_URL}",
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "929e4450-0237-4ed2-9404-b7e1e0a00309",
            "version": "1.0"
        }
    }'
```

| Parameter | Beschreibung |
| --- | --- |
| `name` | Der Name Ihres [!DNL Zoho CRM] Basisverbindung. Sie können diesen Namen verwenden, um Ihre [!DNL Zoho CRM] Basisverbindung. |
| `description` | Eine optionale Beschreibung für Ihre [!DNL Zoho CRM] Basisverbindung. |
| `auth.specName` | Der Authentifizierungstyp, der für die Verbindung verwendet wird. |
| `auth.params.endpoint` | Der Endpunkt der [!DNL Zoho CRM] -Server, an den Sie Ihre Anforderung senden. |
| `auth.params.accountsUrl` | Die Konto-URL wird verwendet, um Ihre Zugriffs- und Aktualisierungstoken zu generieren. Die URL muss domänenspezifisch sein. |
| `auth.params.clientId` | Die Client-ID, die Ihrer [!DNL Zoho CRM] Benutzerkonto. |
| `auth.params.clientSecret` | Das Client-Geheimnis, das Ihrem [!DNL Zoho CRM] Benutzerkonto. |
| `auth.params.accessToken` | Das Zugriffstoken autorisiert Ihren sicheren und temporären Zugriff auf Ihre [!DNL Zoho CRM] -Konto. |
| `auth.params.refreshToken` | Ein Aktualisierungstoken ist ein Token, mit dem ein neues Zugriffstoken generiert wird, sobald Ihr Zugriffstoken abgelaufen ist. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID für [!DNL Zoho CRM]: `929e4450-0237-4ed2-9404-b7e1e0a00309`. |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Basisverbindung zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist im nächsten Schritt erforderlich, um eine Quellverbindung zu erstellen.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Zoho CRM] Basisverbindung mit [!DNL Flow Service] API und haben den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese ID im nächsten Tutorial verwenden, während Sie lernen, wie Sie [Erkunden von CRM-Systemen mit der Flow Service-API](../../explore/crm.md).
