---
keywords: Experience Platform; Startseite; beliebte Themen; Google AdWords; Google AdWords; Adwords
solution: Experience Platform
title: Erstellen einer Google AdWords-Basisverbindung mit der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mit der Flow Service-API Adobe Experience Platform mit Google AdWords verbinden.
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: 17055f76800deadacf435970a691cec79c9f1d17
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 54%

---

# Erstellen einer [!DNL Google AdWords]-Basisverbindung mithilfe der [!DNL Flow Service]-API

>[!NOTE]
>
>Die [!DNL Google AdWords] -Connector befindet sich in der Beta-Phase. Siehe [Quellen - Übersicht](../../../../home.md#terms-and-conditions) Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectoren.

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Google AdWords] (nachstehend &quot;genannt)[!DNL AdWords]&quot;) mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um eine erfolgreiche Verbindung zu [!DNL AdWords] mithilfe der [!DNL Flow Service] API.

### Sammeln erforderlicher Anmeldeinformationen

Damit [!DNL Flow Service] eine Verbindung mit [!DNL AdWords] herstellen kann, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `clientCustomerId` | Die Client-Kunden-ID der [!DNL AdWords] -Konto. |
| `developerToken` | Das mit dem Manager-Konto verknüpfte Entwicklungstoken. |
| `refreshToken` | Das Aktualisierungstoken, das von [!DNL Google] zur Genehmigung des Zugriffs auf [!DNL AdWords]. |
| `clientId` | Die Client-ID der [!DNL Google] -Anwendung, die zum Erfassen des Aktualisierungstokens verwendet wird. |
| `clientSecret` | Das Client-Geheimnis der [!DNL Google] -Anwendung, die zum Erfassen des Aktualisierungstokens verwendet wird. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL AdWords] ist: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

Weiterführende Informationen zu diesen Werten finden Sie in diesem Abschnitt [Google AdWords-Dokument](https://developers.google.com/adwords/api/docs/guides/authentication).

### Verwenden von Platform-APIs

Informationen zum Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL AdWords]-Authentifizierungsdaten als Teil der Anfrageparameter an.

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL AdWords]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json'
    -d '{
        "name": "google-AdWords connection",
        "description": "Connection for google-AdWords",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientCustomerID": "{CLIENT_CUSTOMER_ID}",
                "developerToken": "{DEVELOPER_TOKEN}",
                "authenticationType": "{AUTHENTICATION_TYPE}"
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "d771e9c1-4f26-40dc-8617-ce58c4b53702",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| --------- | ----------- |
| `auth.params.clientCustomerID` | Die Kunden-ID Ihrer [!DNL AdWords] -Konto. |
| `auth.params.developerToken` | Das Entwicklungstoken Ihrer [!DNL AdWords] -Konto. |
| `auth.params.refreshToken` | Das Aktualisierungstoken Ihrer [!DNL AdWords] -Konto. |
| `auth.params.clientID` | Die Client-ID Ihrer [!DNL AdWords] -Konto. |
| `auth.params.clientSecret` | Das Client-Geheimnis Ihres [!DNL AdWords] -Konto. |
| `connectionSpec.id` | Die [!DNL Google AdWords] Verbindungsspezifikations-ID: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**Antwort**

Bei einer erfolgreichen Antwort werden Details zu der neu erstellten Basisverbindung zurückgegeben, einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist im nächsten Schritt erforderlich, um eine Quellverbindung zu erstellen.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Google AdWords] Basisverbindung mit [!DNL Flow Service] API. Sie können diese Basis-Verbindungs-ID in den folgenden Tutorials verwenden:

* [Struktur und Inhalt Ihrer Datentabellen mithilfe des [!DNL Flow Service] API](../../explore/tabular.md)
* [Erstellen Sie einen Datenfluss, um Werbedaten mithilfe der [!DNL Flow Service] API](../../collect/advertising.md)
