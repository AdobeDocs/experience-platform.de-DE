---
keywords: Experience Platform; Startseite; beliebte Themen; Quadrat; Quadrat
title: Erstellen einer quadratischen Basisverbindung mit der Flow Service-API
description: Erfahren Sie, wie Sie mithilfe der Flow Service-API eine Verbindung zwischen Square und Adobe Experience Platform herstellen.
exl-id: 82c1d513-3b06-4ce9-b637-2c5a268da506
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 46%

---

# Erstellen einer [!DNL Square]-Basisverbindung mithilfe der [!DNL Flow Service]-API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Square] mithilfe der [[!DNL Flow Service] -API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen aufteilen, um die Entwicklung und Weiterentwicklung von Programmen für digitale Erlebnisse zu erleichtern.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um eine erfolgreiche Verbindung zu [!DNL Square] mithilfe der [!DNL Flow Service] API.

### Sammeln erforderlicher Anmeldeinformationen

Damit [!DNL Flow Service] eine Verbindung mit [!DNL Square] herstellen kann, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| --- | --- |
| `host` | Die URL der [!DNL Square] -Instanz. |
| `clientId` | Die mit Ihrer [!DNL Square] -Konto. |
| `clientSecret` | Das Client-Geheimnis, das mit Ihrem [!DNL Square] -Konto. |
| `accessToken` | Das Zugriffstoken wird verwendet, um Ihre [!DNL Square] Konto mit OAuth 2.0-Authentifizierung. Das Zugriffstoken kann abgerufen werden über [!DNL Square]. |
| `refreshToken` | Das Aktualisierungstoken wird verwendet, um neue Zugriffstoken zu generieren, sobald Ihr aktuelles Zugriffstoken abläuft. Das Aktualisierungstoken kann abgerufen werden von [!DNL Square]. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Square] ist: `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5` |

Weitere Informationen zu diesen Anmeldedaten und zum Abrufen dieser Anmeldedaten finden Sie im Abschnitt [[!DNL Square] Dokumentation zu OAuth](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

### Verwenden von Platform-APIs

Informationen zum Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL Square]-Authentifizierungsdaten als Teil der Anfrageparameter an.

**API-Format**

```http
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Square]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Square Base Connection",
        "description": "Square Base Connection",
        "auth": {
        "specName": "OAuth2 Refresh Code",
        "params": {
            "host": "{HOST}",
            "clientId": "{CLIENT_ID}",
            "clientSecret": "{CLIENT_SECRET}"
            "accessToken": "{ACCESS_TOKEN}"
            "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "2acf109f-9b66-4d5e-bc18-ebb2adcff8d5",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| --------- | ----------- |
| `auth.params.host` | Die URL der [!DNL Square] -Instanz. |
| `auth.params.clientId` | Die mit Ihrer [!DNL Square] -Konto. |
| `auth.params.clientSecret` | Das Client-Geheimnis, das mit Ihrem [!DNL Square] -Konto. |
| `auth.params.accessToken` | Das Zugriffstoken wird verwendet, um Ihre [!DNL Square] Konto mit OAuth 2.0-Authentifizierung. Das Zugriffstoken kann abgerufen werden über [!DNL Square]. |
| `auth.params.refreshToken` | Das Aktualisierungstoken wird verwendet, um neue Zugriffstoken zu generieren, sobald Ihr aktuelles Zugriffstoken abläuft. Das Aktualisierungstoken kann abgerufen werden von [!DNL Square]. |
| `connectionSpec.id` | Die [!DNL Square] Verbindungsspezifikations-ID: `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5`. |

**Antwort**

Eine erfolgreiche Antwort gibt die neu erstellte Verbindung zurück, einschließlich der eindeutigen Verbindungskennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Tutorial zu untersuchen.

```json
{
    "id": "24151d58-ffa7-4960-951d-58ffa7396097",
    "etag": "\"65015e9d-0000-0200-0000-5e89162d0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Square] Verbindung mithilfe der [!DNL Flow Service] API und haben den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese ID im nächsten Tutorial verwenden, während Sie lernen, wie Sie [Durchsuchen der Zahlungsanwendung mit der Flow Service-API](../../explore/payments.md).
