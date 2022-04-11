---
keywords: Experience Platform;Startseite;beliebte Themen;Zoho CRM;Zoho crm;Zoho;Zoho
solution: Experience Platform
title: Erstellen einer Zoho CRM-Basisverbindung mithilfe der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit dem Zoho-CRM verbinden.
exl-id: 33995927-8f5e-44c5-b809-4db8706bbd34
source-git-commit: 46b2fd6bc715bf1d8ccfeed576a2a2d193f92edd
workflow-type: ht
source-wordcount: '649'
ht-degree: 100%

---

# Erstellen einer [!DNL Zoho CRM]-Basisverbindung mithilfe der [!DNL Flow Service]-API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Zoho CRM] mithilfe der [[!DNL Flow Service] -API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie für eine erfolgreiche Verbindung mit [!DNL Zoho CRM] unter Verwendung der [!DNL Flow Service]-API benötigen.

### Sammeln erforderlicher Anmeldeinformationen

Damit [!DNL Flow Service] eine Verbindung mit [!DNL Zoho CRM] herstellen kann, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| --- | --- |
| `endpoint` | Der Endpunkt des [!DNL Zoho CRM]-Servers, an den Sie Ihre Anfrage stellen. |
| `accountsUrl` | Die Konto-URL wird verwendet, um Ihre Zugriffs- und Aktualisierungs-Token zu generieren. Die URL muss Domain-spezifisch sein. |
| `clientId` | Die Client-ID, die Ihrem [!DNL Zoho CRM]-Benutzerkonto entspricht. |
| `clientSecret` | Das Client-Geheimnis, das Ihrem [!DNL Zoho CRM]-Benutzerkonto entspricht. |
| `accessToken` | Das Zugriffs-Token autorisiert Ihren sicheren und temporären Zugriff auf Ihr [!DNL Zoho CRM]-Konto. |
| `refreshToken` | Ein Aktualisierungs-Token ist ein Token, mit dem ein neues Zugriffs-Token generiert wird, sobald Ihr Zugriffs-Token abgelaufen ist. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Zoho CRM] ist: `929e4450-0237-4ed2-9404-b7e1e0a00309`. |

Weitere Informationen zu diesen Anmeldeinformationen finden Sie in der Dokumentation unter [[!DNL Zoho CRM] Authentifizierung](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

### Verwenden von Platform-APIs

Weitere Informationen zum erfolgreichen Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL Zoho CRM]-Authentifizierungsdaten als Teil der Anfrageparameter an.

**API-Format**

```https
POST /connections
```

**Anfrage**

>[!TIP]
>
>Ihre Konto-URL-Domain muss mit Ihrem entsprechenden Domain-Speicherort übereinstimmen. Im Folgenden finden Sie die verschiedenen Domains und die zugehörigen Konto-URLs:<ul><li>Vereinigte Staaten: https://accounts.zoho.com</li><li>Australien: https://accounts.zoho.com.au</li><li>Europa: https://accounts.zoho.eu</li><li>Indien: https://accounts.zoho.in</li><li>China: https://accounts.zoho.com.cn</li></ul>

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
| `name` | Der Name Ihrer [!DNL Zoho CRM]-Basisverbindung. Sie können diesen Namen verwenden, um Ihre [!DNL Zoho CRM]-Basisverbindung zu suchen. |
| `description` | Eine optionale Beschreibung für Ihre [!DNL Zoho CRM]-Basisverbindung. |
| `auth.specName` | Der Authentifizierungstyp, der für die Verbindung verwendet wird. |
| `auth.params.endpoint` | Der Endpunkt des [!DNL Zoho CRM]-Servers, an den Sie Ihre Anfrage stellen. |
| `auth.params.accountsUrl` | Die Konto-URL wird verwendet, um Ihre Zugriffs- und Aktualisierungs-Token zu generieren. Die URL muss Domain-spezifisch sein. |
| `auth.params.clientId` | Die Client-ID, die Ihrem [!DNL Zoho CRM]-Benutzerkonto entspricht. |
| `auth.params.clientSecret` | Das Client-Geheimnis, das Ihrem [!DNL Zoho CRM]-Benutzerkonto entspricht. |
| `auth.params.accessToken` | Das Zugriffs-Token autorisiert den sicheren und temporären Zugriff auf Ihr [!DNL Zoho CRM]-Konto. |
| `auth.params.refreshToken` | Ein Aktualisierungs-Token ist ein Token, mit dem ein neues Zugriffs-Token generiert wird, sobald Ihr Zugriffs-Token abgelaufen ist. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID für [!DNL Zoho CRM]: `929e4450-0237-4ed2-9404-b7e1e0a00309`. |

**Antwort**

Bei einer erfolgreichen Antwort werden Details zu der neu erstellten Basisverbindung zurückgegeben, einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist im nächsten Schritt erforderlich, um eine Quellverbindung zu erstellen.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Zoho CRM]-Basisverbindung mithilfe der [!DNL Flow Service]-API erstellt und den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese ID im nächsten Tutorial verwenden, in dem Sie das [Erkunden von CRM-Systemen mit der Flow Service-API](../../explore/crm.md) lernen.
