---
title: Erstellen einer Google Ads-Basisverbindung mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit Google Ads verbinden.
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: ce3dabe4ab08a41e581b97b74b3abad352e3267c
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 27%

---

# Erstellen einer Google Ads-Basisverbindung mithilfe der [!DNL Flow Service]-API

>[!WARNING]
>
>Die [!DNL Google Ads] ist vorübergehend nicht verfügbar. Adobe arbeitet daran, Probleme mit dieser Quelle zu beheben.

>[!NOTE]
>
>Die Google Ads-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Quellen finden Sie ](../../../../home.md#terms-and-conditions) „Quellen - Übersicht“ .

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für Google Ads mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um sich mithilfe der [!DNL Flow Service]-API erfolgreich mit Google Ads verbinden zu können.

### Sammeln erforderlicher Anmeldedaten

Damit [!DNL Flow Service] eine Verbindung mit Google Ads herstellen können, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `clientCustomerId` | Die Kunden-ID ist die Kontonummer, die dem Google Ads-Client-Konto entspricht, das Sie mit der Google Ads-API verwalten möchten. Diese ID folgt der Vorlage von `123-456-7890`. |
| `loginCustomerId` | Die Kunden-ID für die Anmeldung ist die Kontonummer, die Ihrem Google Ads Manager-Konto entspricht und zum Abrufen von Berichtsdaten von einem bestimmten aktiven Kunden verwendet wird. Weitere Informationen zur Anmelde-Kunden-ID finden Sie in der Dokumentation zur [Google Ads-API](https://developers.google.com/search-ads/reporting/concepts/login-customer-id). |
| `developerToken` | Mit dem Entwickler-Token können Sie auf die Google Ads-API zugreifen. Sie können dasselbe Entwickler-Token verwenden, um Anfragen an alle Ihre Google Ads-Konten zu richten. Rufen Sie Ihr Entwickler-Token ab[ indem Sie sich bei Ihrem Manager-Konto ](https://ads.google.com/home/tools/manager-accounts/) und dann zur [!DNL API Center] navigieren. |
| `refreshToken` | Das Aktualisierungs-Token ist Teil [!DNL OAuth2] Authentifizierung. Mit diesem Token können Sie Ihre Zugriffs-Token nach ihrem Ablauf neu generieren. |
| `clientId` | Die Client-ID wird zusammen mit dem Client-Geheimnis im Rahmen [!DNL OAuth2] Authentifizierung verwendet. Gemeinsam ermöglichen die Client-ID und das Client-Geheimnis, dass Ihre Anwendung im Namen Ihres Kontos betrieben wird, indem Sie Ihre Anwendung bei Google identifizieren. |
| `clientSecret` | Das Client-Geheimnis wird zusammen mit der Client-ID als Teil [!DNL OAuth2] Authentifizierung verwendet. Gemeinsam ermöglichen die Client-ID und das Client-Geheimnis, dass Ihre Anwendung im Namen Ihres Kontos betrieben wird, indem Sie Ihre Anwendung bei Google identifizieren. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für Google Ads lautet: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

Lesen Sie das Dokument zur API-Übersicht für [weitere Informationen zu den ersten Schritten mit Google Ads](https://developers.google.com/google-ads/api/docs/first-call/overview).

### Verwenden von Platform-APIs

Informationen zum Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungs-Anmeldedaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den `/connections`-Endpunkt und geben Sie dabei Ihre Google Ads-Authentifizierungsdaten als Teil der Anfrageparameter an.

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für Google Ads:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "name": "Google Ads base connection",
      "description": "Google Ads base connection",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "clientCustomerID": "{CLIENT_CUSTOMER_ID}",
              "loginCustomerID": "{LOGIN_CUSTOMER_ID}",
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
| `auth.params.clientCustomerID` | Die Kunden-ID Ihres Google Ads-Kontos. |
| `auth.params.loginCustomerID` | Die Kunden-ID für die Anmeldung, die Ihrem Google Ads Manager-Konto entspricht. |
| `auth.params.developerToken` | Das Entwickler-Token Ihres Google Ads-Kontos. |
| `auth.params.refreshToken` | Das Aktualisierungstoken Ihres Google Ads-Kontos. |
| `auth.params.clientID` | Die Client-ID Ihres Google Ads-Kontos. |
| `auth.params.clientSecret` | Das Client-Geheimnis Ihres Google Ads-Kontos. |
| `connectionSpec.id` | Die Google Ads-Verbindungsspezifikations-ID: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**Antwort**

Bei einer erfolgreichen Antwort werden Details zu der neu erstellten Basisverbindung zurückgegeben, einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist im nächsten Schritt erforderlich, um eine Quellverbindung zu erstellen.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine Google Ads-Basisverbindung mithilfe der [!DNL Flow Service]-API erstellt. Sie können diese Basisverbindungs-ID in den folgenden Tutorials verwenden:

* [Erkunden von Struktur und Inhalten Ihrer Datentabellen mithilfe der  [!DNL Flow Service] -API](../../explore/tabular.md)
* [Erstellen eines Datenflusses, um Werbedaten mithilfe der API  [!DNL Flow Service]  Platform zu übertragen](../../collect/advertising.md)
