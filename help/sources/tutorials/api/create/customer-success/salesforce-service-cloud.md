---
title: Erstellen einer Salesforce Service Cloud-Quellverbindung mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit Salesforce Service Cloud verbinden.
exl-id: ed133bca-8e88-4c85-ae52-c3269b6bf3c9
source-git-commit: 7930a869627130a5db34780e64b809cda0c1e5f4
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 33%

---

# Erstellen Sie eine [!DNL Salesforce Service Cloud] Quellverbindung mithilfe der [!DNL Flow Service] API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

In diesem Tutorial erfahren Sie, wie Sie eine Basisverbindung für [!DNL Salesforce Service Cloud] mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten zu strukturieren, zu beschriften und zu erweitern, indem [!DNL Platform] Dienste.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform stellt virtuelle Sandboxes bereit, die eine [!DNL Platform] in separate virtuelle Umgebungen zu integrieren, um die Entwicklung und Weiterentwicklung von Programmen für digitale Erlebnisse zu unterstützen.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um eine erfolgreiche Verbindung zu [!DNL Salesforce Service Cloud] mithilfe der [!DNL Flow Service] API.

### Sammeln erforderlicher Anmeldeinformationen

Die [!DNL Salesforce Service Cloud] -Quelle unterstützt grundlegende Authentifizierung und OAuth2 Client Credential.

>[!BEGINTABS]

>[!TAB Grundlegende Authentifizierung]

Um eine Verbindung herzustellen [!DNL Salesforce Service Cloud] -Konto [!DNL Flow Service] Geben Sie mithilfe der einfachen Authentifizierung Werte für die folgenden Anmeldeinformationen an:

| Anmeldedaten | Beschreibung |
| --- | --- |
| `environmentUrl` | Die URL der [!DNL Salesforce Service Cloud] Quellinstanz. |
| `username` | Der Benutzername für die [!DNL Salesforce Service Cloud] Benutzerkonto. |
| `password` | Das Kennwort für die [!DNL Salesforce Service Cloud] Benutzerkonto. |
| `securityToken` | Das Sicherheits-Token für [!DNL Salesforce Service Cloud] Benutzerkonto. |
| `apiVersion` | (Optional) Die REST-API-Version der [!DNL Salesforce Service Cloud] -Instanz, die Sie verwenden. Der Wert für die API-Version muss mit einer Dezimalzahl formatiert sein. Wenn Sie beispielsweise die API-Version verwenden `52`eingeben, müssen Sie den Wert als `52.0`. Wenn dieses Feld leer gelassen wird, verwendet Experience Platform automatisch die neueste verfügbare Version. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Salesforce Service Cloud] ist: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Weitere Informationen zu den ersten Schritten finden Sie unter [Dieses Salesforce-Dokument](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

>[!TAB OAuth 2 Client Credential]

Um eine Verbindung herzustellen [!DNL Salesforce Service Cloud] -Konto [!DNL Flow Service] Geben Sie mithilfe von OAuth 2 Client Credential Werte für die folgenden Anmeldedaten an:

| Anmeldedaten | Beschreibung |
| --- | --- |
| `environmentUrl` | Die URL der [!DNL Salesforce Service Cloud] Quellinstanz. |
| `clientId` | Die Client-ID wird zusammen mit dem Client-Geheimnis als Teil der OAuth2-Authentifizierung verwendet. Gemeinsam ermöglichen es die Client-ID und das Client-Geheimnis Ihrer Anwendung, im Namen Ihres Kontos zu arbeiten, indem Sie Ihre Anwendung identifizieren auf [!DNL Salesforce Service Cloud]. |
| `clientSecret` | Das Client-Geheimnis wird zusammen mit der Client-ID als Teil der OAuth2-Authentifizierung verwendet. Gemeinsam ermöglichen es die Client-ID und das Client-Geheimnis Ihrer Anwendung, im Namen Ihres Kontos zu arbeiten, indem Sie Ihre Anwendung identifizieren auf [!DNL Salesforce Service Cloud]. |
| `apiVersion` | Die REST-API-Version der [!DNL Salesforce Service Cloud] -Instanz, die Sie verwenden. Der Wert für die API-Version muss mit einer Dezimalzahl formatiert sein. Wenn Sie beispielsweise die API-Version verwenden `52`eingeben, müssen Sie den Wert als `52.0`. Wenn dieses Feld leer gelassen wird, verwendet Experience Platform automatisch die neueste verfügbare Version. Dieser Wert ist für die Authentifizierung von OAuth2-Client-Anmeldedaten obligatorisch. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Salesforce Service Cloud] ist: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Weitere Informationen zur Verwendung von OAuth für [!DNL Salesforce Service Cloud], lesen Sie die [[!DNL Salesforce Service Cloud] Handbuch zu OAuth-Autorisierungsflüssen](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

### Verwenden von Platform-APIs

Informationen zum Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL Salesforce Service Cloud]-Authentifizierungsdaten als Teil der Anfrageparameter an.

**API-Format**

```http
POST /connections
```

**Anfrage**

>[!BEGINTABS]

>[!TAB Grundlegende Authentifizierung]

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Salesforce Service Cloud] einfache Authentifizierung verwenden:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Service Cloud account for ACME data (basic auth)",
      "description": "Salesforce Service Cloud account for ACME data (basic auth)",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
            "environmentUrl": "https://acme-enterprise-3126.my.salesforce.com",
            "username": "acme-salesforce-service-cloud",
            "password": "xxxx",
            "securityToken": "xxxx"
        }
      },
      "connectionSpec": {
          "id": "cb66ab34-8619-49cb-96d1-39b37ede86ea",
          "version": "1.0"
      }
  }'
```

| Parameter | Beschreibung |
| ---| --- |
| `auth.params.environmentUrl` | Die URL Ihrer [!DNL Salesforce Service Cloud] -Instanz. |
| `auth.params.username` | Der mit Ihrer [!DNL Salesforce Service Cloud] -Konto. |
| `auth.params.password` | Das Kennwort für Ihre [!DNL Salesforce Service Cloud] -Konto. |
| `auth.params.securityToken` | Das Ihrem [!DNL Salesforce Service Cloud] -Konto. |
| `connectionSpec.id` | Die [!DNL Salesforce Service Cloud]-Verbindungsspezifikations-ID: `cb66ab34-8619-49cb-96d1-39b37ede86ea` |

>[!TAB OAuth2 Client Credential]

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Salesforce Service Cloud] Verwendung von OAuth 2 Client Credential:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Service Cloud account for ACME data (OAuth2)",
      "description": "Salesforce Service Cloud account for ACME data (OAuth2)",
      "auth": {
          "specName": "OAuth2 Client Credential",
          "params":
            "environmentUrl": "https://acme-enterprise-3126.my.salesforce.com",
            "clientId": "xxxx",
            "clientSecret": "xxxx",
            "apiVersion": "60.0"
        }
      },
      "connectionSpec": {
          "id": "cb66ab34-8619-49cb-96d1-39b37ede86ea",
          "version": "1.0"
      }
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `auth.params.environmentUrl` | Die URL Ihrer [!DNL Salesforce Service Cloud] -Instanz. |
| `auth.params.clientId` | Die mit Ihrer [!DNL Salesforce Service Cloud] -Konto. |
| `auth.params.clientSecret` | Das Client-Geheimnis, das mit Ihrem [!DNL Salesforce Service Cloud] -Konto. |
| `auth.params.apiVersion` | Die REST-API-Version der [!DNL Salesforce Service Cloud] -Instanz, die Sie verwenden. |
| `connectionSpec.id` | Die [!DNL Salesforce Service Cloud] Verbindungsspezifikations-ID: `cb66ab34-8619-49cb-96d1-39b37ede86ea`. |

>[!ENDTABS]

**Antwort**

Bei einer erfolgreichen Antwort wird Ihre neu erstellte Basisverbindung zusammen mit der eindeutigen ID zurückgegeben.

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Salesforce Service Cloud]-Basisverbindung mithilfe der [!DNL Flow Service]-API erstellt. Sie können diese Basisverbindungs-ID in den folgenden Tutorials verwenden:

* [Erkunden von Struktur und Inhalten Ihrer Datentabellen mithilfe der  [!DNL Flow Service] -API](../../explore/tabular.md)
* [Erstellen eines Datenflusses, um Kundenerfolgsdaten mithilfe der  [!DNL Flow Service] -API zu Platform zu übertragen](../../collect/customer-success.md)
