---
keywords: Experience Platform;Startseite;beliebte Themen;Square;Square
title: Erstellen einer quadratischen Basisverbindung mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie Square mithilfe der Flow Service-API mit Adobe Experience Platform verbinden.
exl-id: 82c1d513-3b06-4ce9-b637-2c5a268da506
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 35%

---

# Erstellen einer [!DNL Square]-Basisverbindung mithilfe der [!DNL Flow Service]-API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Square] mithilfe der [[!DNL Flow Service] -API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Experience Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service]-API eine Verbindung zu [!DNL Square] herstellen zu können.

### Sammeln erforderlicher Anmeldedaten

Damit [!DNL Flow Service] eine Verbindung mit [!DNL Square] herstellen kann, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| --- | --- |
| `host` | Die URL der [!DNL Square]. |
| `clientId` | Die mit Ihrem [!DNL Square]-Konto verknüpfte Client-ID. |
| `clientSecret` | Das mit Ihrem [!DNL Square]-Konto verknüpfte Client-Geheimnis. |
| `accessToken` | Das Zugriffstoken wird verwendet, um Ihr [!DNL Square]-Konto mit OAuth 2.0-Authentifizierung zu authentifizieren. Das Zugriffstoken kann von [!DNL Square] abgerufen werden. |
| `refreshToken` | Das Aktualisierungs-Token wird verwendet, um neue Zugriffs-Token zu generieren, sobald Ihr aktuelles Zugriffs-Token abläuft. Das Aktualisierungstoken kann von [!DNL Square] abgerufen werden. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Square] lautet: `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5` |

Weitere Informationen zu diesen Anmeldeinformationen und deren Abruf finden Sie unter [[!DNL Square] Dokumentation zu OAuth](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

### Verwenden von Experience Platform-APIs

Informationen zum erfolgreichen Aufrufen von Experience Platform-APIs finden Sie im Handbuch unter [&#x200B; mit Experience Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Experience Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen ID der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL Square]-Authentifizierungs-Anmeldedaten als Teil der Anfrageparameter an.

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
| `auth.params.host` | Die URL der [!DNL Square]. |
| `auth.params.clientId` | Die mit Ihrem [!DNL Square]-Konto verknüpfte Client-ID. |
| `auth.params.clientSecret` | Das mit Ihrem [!DNL Square]-Konto verknüpfte Client-Geheimnis. |
| `auth.params.accessToken` | Das Zugriffstoken wird verwendet, um Ihr [!DNL Square]-Konto mit OAuth 2.0-Authentifizierung zu authentifizieren. Das Zugriffstoken kann von [!DNL Square] abgerufen werden. |
| `auth.params.refreshToken` | Das Aktualisierungs-Token wird verwendet, um neue Zugriffs-Token zu generieren, sobald Ihr aktuelles Zugriffs-Token abläuft. Das Aktualisierungstoken kann von [!DNL Square] abgerufen werden. |
| `connectionSpec.id` | Die Spezifikations-ID der [!DNL Square]-Verbindung: `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5`. |

**Antwort**

Eine erfolgreiche Antwort gibt die neu erstellte Verbindung zurück, einschließlich ihrer eindeutigen Verbindungskennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Tutorial zu untersuchen.

```json
{
    "id": "24151d58-ffa7-4960-951d-58ffa7396097",
    "etag": "\"65015e9d-0000-0200-0000-5e89162d0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Square] mithilfe der [!DNL Flow Service]-API erstellt und den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese ID im nächsten Tutorial verwenden, in dem Sie lernen, wie Sie [Zahlungsanwendung mithilfe der Flow Service-API erkunden](../../explore/payments.md).
