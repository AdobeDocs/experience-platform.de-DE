---
keywords: Experience Platform;home;beliebte Themen;Zoho CRM;zoho crm;Zoho;Zoho
solution: Experience Platform
title: Erstellen einer Zoho CRM-Basisverbindung mithilfe der Flow Service API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service API mit Zoho CRM verbinden.
source-git-commit: 7a15090d8ed2c1016d7dc4d7d3d0656640c4785c
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 8%

---

# (Beta) Erstellen Sie eine [!DNL Zoho CRM] Basisverbindung mit [!DNL Flow Service] API

>[!NOTE]
>
>Die [!DNL Zoho CRM] Quelle befindet sich in der Beta-Version. Siehe [Quellübersicht](../../../../home.md#terms-and-conditions) für weitere Informationen zur Verwendung von Beta-gekennzeichneten Steckverbindern.

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Zoho CRM] mit [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten zu strukturieren, zu kennzeichnen und zu verbessern, indem Sie [!DNL Platform] Dienstleistungen.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um erfolgreich eine Verbindung zu [!DNL Zoho CRM] mit [!DNL Flow Service] API.

### Erforderliche Anmeldedaten sammeln

In der Reihenfolge [!DNL Flow Service] Verbindung herstellen mit [!DNL Zoho CRM], müssen Sie Werte für die folgenden Verbindungseigenschaften bereitstellen:

| Anmeldedaten | Beschreibung |
| --- | --- |
| `endpoint` | Der Endpunkt des [!DNL Zoho CRM] Server, an den Sie Ihre Anforderung senden. |
| `accountsUrl` | Die Konto-URL wird verwendet, um Ihren Zugriff zu generieren und Token zu aktualisieren. Die URL muss domänenspezifisch sein. |
| `clientId` | Die Client-ID, die Ihrer [!DNL Zoho CRM] Benutzerkonto. |
| `clientSecret` | Das Client-Geheimnis, das Ihrem [!DNL Zoho CRM] Benutzerkonto. |
| `accessToken` | Das Zugriffstoken autorisiert Ihren sicheren und temporären Zugriff auf Ihre [!DNL Zoho CRM] Konto. |
| `refreshToken` | Ein Aktualisierungstoken ist ein Token, das verwendet wird, um ein neues Zugriffstoken zu generieren, sobald Ihr Zugriffstoken abgelaufen ist. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Verbindungseigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für das Erstellen der Basis- und Quellverbindungen. Verbindungsspezifikations-ID für [!DNL Zoho CRM] ist: `929e4450-0237-4ed2-9404-b7e1e0a00309`. |

Weitere Informationen zu diesen Anmeldedaten finden Sie in der Dokumentation zu [[!DNL Zoho CRM] Authentifizierung](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

### Verwenden von Plattform-APIs

Informationen dazu, wie Sie erfolgreich Aufrufe von Plattform-APIs durchführen, finden Sie im Handbuch zu [Erste Schritte mit Plattform-APIs](../../../../../landing/api-guide.md).

## Basisverbindung erstellen

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Plattform gespeichert, einschließlich der Authentifizierungsinformationen Ihrer Quelle, des aktuellen Zustands der Verbindung und Ihrer eindeutigen Basis-Verbindungs-ID. Die Basis-Verbindungs-ID ermöglicht es Ihnen, Dateien von der Quelle aus zu erkunden und zu navigieren und die spezifischen Elemente zu identifizieren, die Sie aufnehmen möchten, einschließlich Informationen zu den Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST an `/connections` Endpunkt beim Bereitstellen von [!DNL Zoho CRM] Authentifizierungsdaten als Teil der Anforderungsparameter.

**API-Format**

```https
POST /connections
```

**Anfrage**

>[!TIP]
>
>Die URL-Domäne Ihrer Konten muss Ihrem entsprechenden Domänenstandort entsprechen. Die folgenden Domänen und die zugehörigen Konto-URLs sind angegeben:<ul><li>Vereinigte Staaten: https://accounts.zoho.com</li><li>Australien: https://accounts.zoho.com.au</li><li>Europa: https://accounts.zoho.eu</li><li>Indien: https://accounts.zoho.in</li><li>China: https://accounts.zoho.com.cn</li></ul>

Die folgende Anforderung erstellt eine Basisverbindung für [!DNL Zoho CRM]:

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
| `name` | Der Name Ihrer [!DNL Zoho CRM] Basisverbindung. Sie können diesen Namen verwenden, um Ihre [!DNL Zoho CRM] Basisverbindung. |
| `description` | Eine optionale Beschreibung für Ihre [!DNL Zoho CRM] Basisverbindung. |
| `auth.specName` | Der für die Verbindung verwendete Authentifizierungstyp. |
| `auth.params.endpoint` | Der Endpunkt des [!DNL Zoho CRM] Server, an den Sie Ihre Anforderung senden. |
| `auth.params.accountsUrl` | Die Konto-URL wird verwendet, um Ihren Zugriff zu generieren und Token zu aktualisieren. Die URL muss domänenspezifisch sein. |
| `auth.params.clientId` | Die Client-ID, die Ihrer [!DNL Zoho CRM] Benutzerkonto. |
| `auth.params.clientSecret` | Das Client-Geheimnis, das Ihrem [!DNL Zoho CRM] Benutzerkonto. |
| `auth.params.accessToken` | Das Zugriffstoken autorisiert Ihren sicheren und temporären Zugriff auf Ihre [!DNL Zoho CRM] Konto. |
| `auth.params.refreshToken` | Ein Aktualisierungstoken ist ein Token, das verwendet wird, um ein neues Zugriffstoken zu generieren, sobald Ihr Zugriffstoken abgelaufen ist. |
| `connectionSpec.id` | Verbindungsspezifikations-ID für [!DNL Zoho CRM]: `929e4450-0237-4ed2-9404-b7e1e0a00309`. |

**Antwort**

Eine erfolgreiche Antwort gibt Details der neu erstellten Basisverbindung einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist im nächsten Schritt zum Erstellen einer Quellverbindung erforderlich.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Zoho CRM] Basisverbindung mit [!DNL Flow Service] API und haben den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese ID im nächsten Tutorial verwenden, während Sie lernen, wie Sie diese ID verwenden können. [CRM-Systeme mithilfe der Flow Service-API erkunden](../../explore/crm.md).
