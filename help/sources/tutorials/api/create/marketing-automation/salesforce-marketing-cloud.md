---
title: Erstellen einer Salesforce-Marketing Cloud-Basisverbindung mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie Ihr Salesforce-Marketing Cloud-Konto mithilfe der Flow Service-API gegen Experience Platform authentifizieren.
exl-id: fbf68d3a-f8b1-4618-bd56-160cc6e3346d
source-git-commit: 30f1e8a0424ee0f81d8e98fb24886ad1480b270c
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 58%

---

# Erstellen einer [!DNL Salesforce Marketing Cloud]-Basisverbindung mithilfe der [!DNL Flow Service]-API

>[!IMPORTANT]
>
>Die Erfassung benutzerdefinierter Objekte wird von der Quellintegration für [!DNL Salesforce Marketing Cloud] derzeit nicht unterstützt.

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Salesforce Marketing Cloud] mithilfe der [[!DNL Flow Service] -API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Verwenden von Platform-APIs

Informationen darüber, wie Sie Platform-APIs erfolgreich aufrufen können, finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

Im folgenden Abschnitt finden Sie weitere Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service] -API erfolgreich eine Verbindung zu [!DNL Salesforce Marketing Cloud] herstellen zu können.

### Sammeln erforderlicher Anmeldeinformationen

Damit [!DNL Flow Service] eine Verbindung zu [!DNL Salesforce Marketing Cloud] herstellen kann, müssen Sie die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `host` | Der Host-Server Ihrer Anwendung. Dies ist häufig Ihre Subdomäne. **Hinweis:** Bei der Eingabe Ihres `host` -Werts müssen Sie den `{subdomain}.rest.marketingcloudapis.com` angeben. Wenn Ihre Host-URL beispielsweise `https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/` ist, müssen Sie `acme-ab12c3d4e5fg6hijk7lmnop8qrst.rest.marketingcloudapis.com/` als Hostwert eingeben. |
| `clientId` | Die mit Ihrer [!DNL Salesforce Marketing Cloud] -Anwendung verknüpfte Client-ID. |
| `clientSecret` | Das Client-Geheimnis, das Ihrer [!DNL Salesforce Marketing Cloud]-Anwendung zugeordnet ist. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Salesforce Marketing Cloud] ist: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

Weitere Informationen zu den ersten Schritten finden Sie in diesem [[!DNL Salesforce Marketing Cloud] Dokument](<https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm>).

## Erstellen einer Basisverbindung

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den `/connections` -Endpunkt und geben Sie dabei Ihre [!DNL Salesforce Marketing Cloud]-Authentifizierungsdaten als Teil des Anfragetexts an.

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Salesforce Marketing Cloud]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Marketing Cloud base connection",
      "description": "Salesforce Marketing Cloud base connection",
      "auth": {
          "specName": "Client-Id-Secret Based Authentication",
          "params": {
              "host": "acme-ab12c3d4e5fg6hijk7lmnop8qrst"
              "clientId": "acme-salesforce-marketing-cloud",
              "clientSecret": "xxxx"
          }
      },
      "connectionSpec": {
          "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
          "version": "1.0"
      }
  }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.clientId` | Die mit Ihrer [!DNL Salesforce Marketing Cloud] -Anwendung verknüpfte Client-ID. |
| `auth.params.clientSecret` | Das Client-Geheimnis, das Ihrer [!DNL Salesforce Marketing Cloud]-Anwendung zugeordnet ist. |
| `connectionSpec.id` | Die [!DNL Salesforce Marketing Cloud] Verbindungsspezifikations-ID: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

**Antwort**

Eine erfolgreiche Antwort gibt die neu erstellte Verbindung zurück, einschließlich der eindeutigen Verbindungskennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Tutorial zu untersuchen.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Salesforce Marketing Cloud]-Basisverbindung mithilfe der [!DNL Flow Service]-API erstellt. Sie können diese Basisverbindungs-ID in den folgenden Tutorials verwenden:

* [Erkunden von Struktur und Inhalten Ihrer Datentabellen mithilfe der  [!DNL Flow Service] -API](../../explore/tabular.md)
* [Erstellen eines Datenflusses, um Daten zur Marketing-Automatisierung mithilfe der  [!DNL Flow Service] -API auf Platform zu übertragen](../../collect/marketing-automation.md)
