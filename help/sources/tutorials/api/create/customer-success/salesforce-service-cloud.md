---
title: Erstellen einer Salesforce Service Cloud Source-Verbindung mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit Salesforce Service Cloud verbinden.
exl-id: ed133bca-8e88-4c85-ae52-c3269b6bf3c9
source-git-commit: 7930a869627130a5db34780e64b809cda0c1e5f4
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 33%

---

# Erstellen einer [!DNL Salesforce Service Cloud]-Quellverbindung mit der [!DNL Flow Service]-API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

In diesem Tutorial erfahren Sie, wie Sie mit der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) eine Basisverbindung für [!DNL Salesforce Service Cloud] erstellen.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von [!DNL Platform]-Diensten zu strukturieren, zu beschriften und zu erweitern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform stellt virtuelle Sandboxes bereit, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen aufteilen, um die Entwicklung und Weiterentwicklung von Programmen für digitale Erlebnisse zu erleichtern.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service] -API erfolgreich eine Verbindung zu [!DNL Salesforce Service Cloud] herstellen zu können.

### Sammeln erforderlicher Anmeldeinformationen

Die Quelle [!DNL Salesforce Service Cloud] unterstützt grundlegende Authentifizierung und OAuth2 Client Credential.

>[!BEGINTABS]

>[!TAB Grundlegende Authentifizierung]

Um Ihr [!DNL Salesforce Service Cloud]-Konto mit [!DNL Flow Service] mittels einfacher Authentifizierung zu verbinden, geben Sie Werte für die folgenden Anmeldedaten an:

| Anmeldedaten | Beschreibung |
| --- | --- |
| `environmentUrl` | Die URL der Quellinstanz [!DNL Salesforce Service Cloud]. |
| `username` | Der Benutzername für das [!DNL Salesforce Service Cloud] -Benutzerkonto. |
| `password` | Das Kennwort für das [!DNL Salesforce Service Cloud] -Benutzerkonto. |
| `securityToken` | Das Sicherheits-Token für das [!DNL Salesforce Service Cloud] -Benutzerkonto. |
| `apiVersion` | (Optional) Die REST-API-Version der von Ihnen verwendeten [!DNL Salesforce Service Cloud]-Instanz. Der Wert für die API-Version muss mit einer Dezimalzahl formatiert sein. Wenn Sie beispielsweise die API-Version `52` verwenden, müssen Sie den Wert als `52.0` eingeben. Wenn dieses Feld leer gelassen wird, verwendet Experience Platform automatisch die neueste verfügbare Version. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Salesforce Service Cloud] ist: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Weitere Informationen zu den ersten Schritten finden Sie in [diesem Salesforce-Dokument](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

>[!TAB OAuth 2 Client Credential]

Geben Sie Werte für die folgenden Anmeldedaten an, um Ihr [!DNL Salesforce Service Cloud]-Konto mithilfe der OAuth 2-Client-Anmeldedaten mit [!DNL Flow Service] zu verbinden:

| Anmeldedaten | Beschreibung |
| --- | --- |
| `environmentUrl` | Die URL der Quellinstanz [!DNL Salesforce Service Cloud]. |
| `clientId` | Die Client-ID wird zusammen mit dem Client-Geheimnis als Teil der OAuth2-Authentifizierung verwendet. Gemeinsam ermöglichen es die Client-ID und das Client-Geheimnis Ihrer Anwendung, im Namen Ihres Kontos zu arbeiten, indem Sie Ihre Anwendung mit [!DNL Salesforce Service Cloud] identifizieren. |
| `clientSecret` | Das Client-Geheimnis wird zusammen mit der Client-ID als Teil der OAuth2-Authentifizierung verwendet. Gemeinsam ermöglichen es die Client-ID und das Client-Geheimnis Ihrer Anwendung, im Namen Ihres Kontos zu arbeiten, indem Sie Ihre Anwendung mit [!DNL Salesforce Service Cloud] identifizieren. |
| `apiVersion` | Die REST-API-Version der von Ihnen verwendeten [!DNL Salesforce Service Cloud]-Instanz. Der Wert für die API-Version muss mit einer Dezimalzahl formatiert sein. Wenn Sie beispielsweise die API-Version `52` verwenden, müssen Sie den Wert als `52.0` eingeben. Wenn dieses Feld leer gelassen wird, verwendet Experience Platform automatisch die neueste verfügbare Version. Dieser Wert ist für die Authentifizierung von OAuth2-Client-Anmeldedaten obligatorisch. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Salesforce Service Cloud] ist: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Weitere Informationen zur Verwendung von OAuth für [!DNL Salesforce Service Cloud] finden Sie im [[!DNL Salesforce Service Cloud] Handbuch zu OAuth-Autorisierungsflüssen](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

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

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Salesforce Service Cloud] mithilfe der einfachen Authentifizierung:

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
| `auth.params.username` | Der Benutzername, der Ihrem [!DNL Salesforce Service Cloud] -Konto zugeordnet ist. |
| `auth.params.password` | Das Ihrem [!DNL Salesforce Service Cloud]-Konto zugeordnete Kennwort. |
| `auth.params.securityToken` | Das Ihrem [!DNL Salesforce Service Cloud]-Konto zugeordnete Sicherheits-Token. |
| `connectionSpec.id` | Die [!DNL Salesforce Service Cloud]-Verbindungsspezifikations-ID: `cb66ab34-8619-49cb-96d1-39b37ede86ea` |

>[!TAB OAuth2 Client Credential]

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Salesforce Service Cloud] mithilfe von OAuth 2 Client Credential:

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
| `auth.params.clientId` | Die mit Ihrem [!DNL Salesforce Service Cloud]-Konto verknüpfte Client-ID. |
| `auth.params.clientSecret` | Das Client-Geheimnis, das Ihrem [!DNL Salesforce Service Cloud]-Konto zugeordnet ist. |
| `auth.params.apiVersion` | Die REST-API-Version der von Ihnen verwendeten [!DNL Salesforce Service Cloud]-Instanz. |
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
