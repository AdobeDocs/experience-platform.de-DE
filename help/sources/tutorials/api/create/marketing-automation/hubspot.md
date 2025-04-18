---
keywords: Experience Platform;Startseite;beliebte Themen;hubspot;hubspot
solution: Experience Platform
title: Erstellen einer HubSpot-Basisverbindung mithilfe der Flow Service-API
type: Tutorial
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit HubSpot verbinden.
exl-id: a3e64215-a82d-4aa7-8e6a-48c84c056201
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 50%

---

# Erstellen einer [!DNL HubSpot]-Basisverbindung mithilfe der [!DNL Flow Service]-API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL HubSpot] mithilfe der [[!DNL Flow Service] -API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Experience Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Experience Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service]-API eine Verbindung zu [!DNL HubSpot] herstellen zu können.

### Sammeln erforderlicher Anmeldedaten

Damit [!DNL Flow Service] eine Verbindung mit [!DNL HubSpot] herstellen kann, müssen Sie die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `clientId` | Die mit Ihrem [!DNL HubSpot] Programm verknüpfte Client-ID. |
| `clientSecret` | Das mit Ihrer [!DNL HubSpot]-Anwendung verknüpfte Client-Geheimnis. |
| `accessToken` | Das Zugriffstoken, das beim ersten Authentifizieren Ihrer OAuth-Integration abgerufen wurde. |
| `refreshToken` | Das Aktualisierungstoken, das beim ersten Authentifizieren Ihrer OAuth-Integration abgerufen wurde. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL HubSpot] ist: `cc6a4487-9e91-433e-a3a3-9cf6626c1806`. |

Weitere Informationen zu den ersten Schritten finden Sie in diesem [HubSpot-Dokument](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

### Verwenden von Experience Platform-APIs

Informationen zum erfolgreichen Aufrufen von Experience Platform-APIs finden Sie im Handbuch unter [ mit Experience Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Experience Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen ID der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL HubSpot]-Authentifizierungs-Anmeldedaten als Teil der Anfrageparameter an.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.clientId` | Die mit Ihrem [!DNL HubSpot] Programm verknüpfte Client-ID. |
| `auth.params.clientSecret` | Das mit Ihrer [!DNL HubSpot]-Anwendung verknüpfte Client-Geheimnis. |
| `auth.params.accessToken` | Das Zugriffstoken, das beim ersten Authentifizieren Ihrer OAuth-Integration abgerufen wurde. |
| `auth.params.refreshToken` | Das Aktualisierungstoken, das beim ersten Authentifizieren Ihrer OAuth-Integration abgerufen wurde. |
| `connectionSpec.id` | Die Spezifikations-ID der [!DNL HubSpot]-Verbindung: `cc6a4487-9e91-433e-a3a3-9cf6626c1806`. |

**Antwort**

Eine erfolgreiche Antwort gibt die neu erstellte Verbindung zurück, einschließlich ihrer eindeutigen Verbindungskennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Tutorial zu untersuchen.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL HubSpot]-Basisverbindung mithilfe der [!DNL Flow Service]-API erstellt. Sie können diese Basisverbindungs-ID in den folgenden Tutorials verwenden:

* [Erkunden von Struktur und Inhalten Ihrer Datentabellen mithilfe der  [!DNL Flow Service] -API](../../explore/tabular.md)
* [Erstellen eines Datenflusses, um Daten zur Marketing-Automatisierung mithilfe der API  [!DNL Flow Service]  Experience Platform zu übertragen](../../collect/marketing-automation.md)
