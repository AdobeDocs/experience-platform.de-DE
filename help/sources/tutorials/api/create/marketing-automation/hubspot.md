---
keywords: Experience Platform; Startseite; beliebte Themen; Hotspot; Hubspot
solution: Experience Platform
title: Erstellen einer HubSpot-Basisverbindung mit der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit HubSpot verbinden.
exl-id: a3e64215-a82d-4aa7-8e6a-48c84c056201
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 9%

---

# Erstellen einer [!DNL HubSpot]-Basisverbindung mithilfe der [!DNL Flow Service]-API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL HubSpot] mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md):  [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von  [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu erweitern.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service]-API erfolgreich eine Verbindung zu [!DNL HubSpot] herstellen zu können.

### Erforderliche Anmeldedaten sammeln

Damit [!DNL Flow Service] eine Verbindung mit [!DNL HubSpot] herstellen kann, müssen Sie die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `clientId` | Die Client-ID, die Ihrer [!DNL HubSpot]-Anwendung zugeordnet ist. |
| `clientSecret` | Das Client-Geheimnis, das Ihrer [!DNL HubSpot]-Anwendung zugeordnet ist. |
| `accessToken` | Das Zugriffstoken, das beim erstmaligen Authentifizieren Ihrer OAuth-Integration erhalten wurde. |
| `refreshToken` | Das Aktualisierungstoken, das beim erstmaligen Authentifizieren Ihrer OAuth-Integration erhalten wurde. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL HubSpot] lautet: `cc6a4487-9e91-433e-a3a3-9cf6626c1806`. |

Weitere Informationen zu den ersten Schritten finden Sie in diesem [HubSpot-Dokument](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

### Verwenden von Platform-APIs

Informationen dazu, wie Sie erfolgreich Aufrufe an Platform-APIs durchführen können, finden Sie im Handbuch [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Basisverbindung erstellen

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL HubSpot]-Authentifizierungsdaten als Teil der Anfrageparameter an.

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL HubSpot]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "connection for HubSpot",
        "description": "connection for HubSpot",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "version": "1.0"
        }
    }
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.clientId` | Die Client-ID, die Ihrer [!DNL HubSpot]-Anwendung zugeordnet ist. |
| `auth.params.clientSecret` | Das Client-Geheimnis, das Ihrer [!DNL HubSpot]-Anwendung zugeordnet ist. |
| `auth.params.accessToken` | Das Zugriffstoken, das beim erstmaligen Authentifizieren Ihrer OAuth-Integration erhalten wurde. |
| `auth.params.refreshToken` | Das Aktualisierungstoken, das beim erstmaligen Authentifizieren Ihrer OAuth-Integration erhalten wurde. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID [!DNL HubSpot]: `cc6a4487-9e91-433e-a3a3-9cf6626c1806`. |

**Antwort**

Eine erfolgreiche Antwort gibt die neu erstellte Verbindung zurück, einschließlich der eindeutigen Verbindungskennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Tutorial zu untersuchen.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

In diesem Tutorial haben Sie eine [!DNL HubSpot]-Verbindung mit der [!DNL Flow Service]-API erstellt und den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese Verbindungs-ID im nächsten Tutorial verwenden, wenn Sie erfahren, wie Sie [Marketing-Automatisierungssysteme mithilfe der Flow Service-API](../../explore/marketing-automation.md) untersuchen.
