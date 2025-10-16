---
title: Verbinden von Google Ads mit Experience Platform mithilfe von APIs
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit Google Ads verbinden.
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: a0977e98219797eda14dd8d7ddb6cf3f1410cef0
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 27%

---

# Verbinden von [!DNL Google Ads] mit Experience Platform mithilfe der [!DNL Flow Service]-API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Lesen Sie dieses Tutorial, um zu erfahren, wie Sie Ihr [!DNL Google Ads]-Konto mithilfe der [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/) mit Adobe Experience Platform verbinden.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Google Ads]-API eine Verbindung zu [!DNL Flow Service] herstellen zu können.

### Verwenden von Experience Platform-APIs

Informationen zum erfolgreichen Aufrufen von Experience Platform-APIs finden Sie im Handbuch unter [&#x200B; mit Experience Platform-APIs](../../../../../landing/api-guide.md).

### Sammeln erforderlicher Anmeldedaten

Informationen zur Authentifizierung finden Sie im Abschnitt [[!DNL Google Ads] Quellenübersicht](../../../../connectors/advertising/ads.md).

## Erstellen einer Basisverbindung

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Experience Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen ID der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

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
              "refreshToken": "{REFRESH_TOKEN}",
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}",
              "googleAdsApiVersion": "v19"

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
| `auth.params.clientCustomerID` | Die Kunden-ID Ihres [!DNL Google Ads] Kontos. |
| `auth.params.loginCustomerID` | Die Kunden-ID für die Anmeldung, die Ihrem [!DNL Google Ads] Manager-Konto entspricht. |
| `auth.params.developerToken` | Das Entwickler-Token Ihres [!DNL Google Ads]. |
| `auth.params.refreshToken` | Das Aktualisierungs-Token Ihres [!DNL Google Ads] Kontos. |
| `auth.params.clientID` | Die Client-ID Ihres [!DNL Google Ads]. |
| `auth.params.clientSecret` | Das Client-Geheimnis Ihres [!DNL Google Ads]. |
| `auth.params.googleAdsApiVersion` | Die [!DNL Google Ads] API-Version, die Sie verwenden. Experience Platform unterstützt derzeit Version `v19` und höher. Stellen Sie sicher, dass Sie eine dieser unterstützten Versionen verwenden, um die Kompatibilität sicherzustellen. |
| `connectionSpec.id` | Die Spezifikations-ID der [!DNL Google Ads]-Verbindung: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**Antwort**

Bei einer erfolgreichen Antwort werden Details zu der neu erstellten Basisverbindung zurückgegeben, einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist im nächsten Schritt erforderlich, um eine Quellverbindung zu erstellen.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Erstellen eines Datenflusses zum Aufnehmen von Werbedaten

In diesem Tutorial haben Sie eine [!DNL Google Ads]-Basisverbindung mithilfe der [!DNL Flow Service]-API erstellt und Ihr [!DNL Google Ads]-Konto mit Experience Platform verbunden. Sie können diese Basisverbindungs-ID in den folgenden Tutorials verwenden:

* [Erkunden von Struktur und Inhalten Ihrer Datentabellen mithilfe der  [!DNL Flow Service] -API](../../explore/tabular.md)
* [Erstellen eines Datenflusses, um Werbedaten mithilfe der API  [!DNL Flow Service]  Experience Platform zu übertragen](../../collect/advertising.md)
