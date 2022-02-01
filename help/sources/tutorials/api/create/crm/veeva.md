---
keywords: Experience Platform; Startseite; beliebte Themen; veeva crm; Veeva CRM; Veeva
solution: Experience Platform
title: Erstellen einer VEC CRM-Basisverbindung mit der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit dem VEC-CRM verbinden.
exl-id: e1aea5a2-a247-43eb-8252-2e2ed96b82a1
source-git-commit: 25cc0c5a1e6dcf01b82956ea1022663445315a27
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 10%

---

# Erstellen Sie eine [!DNL Veeva CRM] Basisverbindung mit [!DNL Flow Service] API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Veeva CRM] mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten zu strukturieren, zu beschriften und zu erweitern, indem Sie [!DNL Platform] Dienste.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um eine erfolgreiche Verbindung zu [!DNL Veeva CRM] mithilfe der [!DNL Flow Service] API.

### Erforderliche Anmeldedaten sammeln

Zur [!DNL Flow Service] zur Verbindung mit [!DNL Veeva CRM]müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `environmentUrl` | Die URL Ihrer [!DNL Veeva CRM] -Instanz. |
| `username` | Der Benutzername-Wert Ihres [!DNL Veeva CRM] -Konto. |
| `password` | Der Kennwortwert Ihrer [!DNL Veeva CRM] -Konto. |
| `securityToken` | Das Sicherheits-Token für Ihre [!DNL Veeva CRM] -Instanz. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Veeva CRM] ist: `fcad62f3-09b0-41d3-be11-449d5a621b69`. |

Weiterführende Informationen zu diesen Werten finden Sie in diesem Abschnitt [[!DNL Veeva CRM] Dokument](https://developer.veevacrm.com/api/#order-management-rest-api).

### Verwenden von Platform-APIs

Informationen zum erfolgreichen Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Basisverbindung erstellen

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an die `/connections` Endpunkt beim Bereitstellen [!DNL Veeva CRM] Authentifizierungsberechtigungen als Teil der Anfrageparameter.

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Veeva CRM]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json'
    -d '{
        "name": "Veeva CRM base connection",
        "description": "Base Connection for Veeva CRM",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "environmentUrl": "{ENVIRONMENT_URL}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "fcad62f3-09b0-41d3-be11-449d5a621b69",
            "version": "1.0"
        }
    }'
```

| Parameter | Beschreibung |
| --- | --- |
| `name` | Der Name Ihres [!DNL Veeva CRM] Basisverbindung. Sie können diesen Namen verwenden, um Ihre [!DNL Veeva CRM] Basisverbindung. |
| `description` | Eine optionale Beschreibung für Ihre [!DNL Veeva CRM] Basisverbindung. |
| `auth.specName` | Der Authentifizierungstyp, der für die Verbindung verwendet wird. |
| `auth.params.environmentUrl` | Die URL Ihrer [!DNL Veeva CRM] -Instanz. |
| `auth.params.username` | Der Benutzername-Wert Ihres [!DNL Veeva CRM] -Konto. |
| `auth.params.password` | Der Kennwortwert Ihrer [!DNL Veeva CRM] -Konto. |
| `auth.params.securityToken` | Das Sicherheits-Token für Ihre [!DNL Veeva CRM] -Instanz. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID für [!DNL Veeva CRM]: `fcad62f3-09b0-41d3-be11-449d5a621b69`. |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Basisverbindung zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist im nächsten Schritt erforderlich, um eine Quellverbindung zu erstellen.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Veeva CRM] Basisverbindung mit [!DNL Flow Service] API und haben den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese ID im nächsten Tutorial verwenden, während Sie lernen, wie Sie [Erkunden von CRM-Systemen mit der Flow Service-API](../../explore/crm.md).
