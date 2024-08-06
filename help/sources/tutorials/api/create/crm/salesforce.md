---
title: Erstellen einer Salesforce-Basisverbindung mit der Flow Service-API
description: Erfahren Sie, wie Sie mithilfe der Flow Service-API Adobe Experience Platform mit einem Salesforce-Konto verbinden.
exl-id: 43dd9ee5-4b87-4c8a-ac76-01b83c1226f6
source-git-commit: 5951b0f549c2fd2723945f8f4089d12f73b92e6c
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 36%

---

# Erstellen einer [!DNL Salesforce]-Basisverbindung mithilfe der [!DNL Flow Service]-API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Salesforce] mithilfe der [[!DNL Flow Service] -API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um [!DNL Platform] mithilfe der [!DNL Flow Service] -API erfolgreich mit einem [!DNL Salesforce] -Konto zu verbinden.

### Sammeln erforderlicher Anmeldedaten

Die Quelle [!DNL Salesforce] unterstützt grundlegende Authentifizierung und OAuth2 Client Credential.

>[!BEGINTABS]

>[!TAB Grundlegende Authentifizierung]

Um Ihr [!DNL Salesforce]-Konto mit [!DNL Flow Service] mittels einfacher Authentifizierung zu verbinden, geben Sie Werte für die folgenden Anmeldedaten an:

| Anmeldedaten | Beschreibung |
| --- | --- |
| `environmentUrl` | Die URL der Quellinstanz [!DNL Salesforce]. Das Format für `environmentUrl` ist `https://[domain].my.salesforce.com`. |
| `username` | Der Benutzername für das [!DNL Salesforce] -Benutzerkonto. |
| `password` | Das Kennwort für das [!DNL Salesforce] -Benutzerkonto. |
| `securityToken` | Das Sicherheits-Token für das [!DNL Salesforce] -Benutzerkonto. |
| `apiVersion` | (Optional) Die REST-API-Version der von Ihnen verwendeten [!DNL Salesforce]-Instanz. Der Wert für die API-Version muss mit einer Dezimalzahl formatiert sein. Wenn Sie beispielsweise die API-Version `52` verwenden, müssen Sie den Wert als `52.0` eingeben. Wenn dieses Feld leer gelassen wird, verwendet Experience Platform automatisch die neueste verfügbare Version. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Salesforce] ist: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Weitere Informationen zu den ersten Schritten finden Sie in [diesem Salesforce-Dokument](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

>[!TAB OAuth 2 Client Credential]

Geben Sie Werte für die folgenden Anmeldedaten an, um Ihr [!DNL Salesforce]-Konto mithilfe der OAuth 2-Client-Anmeldedaten mit [!DNL Flow Service] zu verbinden:

| Anmeldedaten | Beschreibung |
| --- | --- |
| `environmentUrl` | Die URL der Quellinstanz [!DNL Salesforce]. Das Format für `environmentUrl` ist `https://[domain].my.salesforce.com` |
| `clientId` | Die Client-ID wird zusammen mit dem Client-Geheimnis als Teil der OAuth2-Authentifizierung verwendet. Gemeinsam ermöglichen es die Client-ID und das Client-Geheimnis Ihrer Anwendung, im Namen Ihres Kontos zu arbeiten, indem Sie Ihre Anwendung mit [!DNL Salesforce] identifizieren. |
| `clientSecret` | Das Client-Geheimnis wird zusammen mit der Client-ID als Teil der OAuth2-Authentifizierung verwendet. Gemeinsam ermöglichen es die Client-ID und das Client-Geheimnis Ihrer Anwendung, im Namen Ihres Kontos zu arbeiten, indem Sie Ihre Anwendung mit [!DNL Salesforce] identifizieren. |
| `apiVersion` | Die REST-API-Version der von Ihnen verwendeten [!DNL Salesforce]-Instanz. Der Wert für die API-Version muss mit einer Dezimalzahl formatiert sein. Wenn Sie beispielsweise die API-Version `52` verwenden, müssen Sie den Wert als `52.0` eingeben. Wenn dieses Feld leer gelassen wird, verwendet Experience Platform automatisch die neueste verfügbare Version. Dieser Wert ist für die Authentifizierung von OAuth2-Client-Anmeldedaten obligatorisch. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Salesforce] ist: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Weitere Informationen zur Verwendung von OAuth für [!DNL Salesforce] finden Sie im [[!DNL Salesforce] Handbuch zu OAuth-Autorisierungsflüssen](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

### Verwenden von Platform-APIs

Informationen zum Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungs-Anmeldedaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den `/connections`-Endpunkt und geben Sie Ihre [!DNL Salesforce]-Authentifizierungsdaten im Anfrageinhalt an.

**API-Format**

```http
POST /connections
```

**Anfrage**

>[!BEGINTABS]

>[!TAB Grundlegende Authentifizierung]

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Salesforce] mithilfe der einfachen Authentifizierung:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Salesforce account",
      "description": "Salesforce account using basic authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params":
            "environmentUrl": "https://acme-enterprise-3126.my.salesforce.com",
            "username": "acme-salesforce",
            "password": "xxxx",
            "securityToken": "xxxx"
        }
      },
      "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
      }
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `auth.params.environmentUrl` | Die URL Ihrer [!DNL Salesforce] -Instanz. |
| `auth.params.username` | Der Benutzername, der Ihrem [!DNL Salesforce] -Konto zugeordnet ist. |
| `auth.params.password` | Das Ihrem [!DNL Salesforce]-Konto zugeordnete Kennwort. |
| `auth.params.securityToken` | Das Ihrem [!DNL Salesforce]-Konto zugeordnete Sicherheits-Token. |
| `connectionSpec.id` | Die [!DNL Salesforce] Verbindungsspezifikations-ID: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

>[!TAB OAuth 2 Client Credential]

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Salesforce] mithilfe von OAuth 2 Client Credential:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Salesforce account",
      "description": "Salesforce account using OAuth 2",
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
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
      }
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `auth.params.environmentUrl` | Die URL Ihrer [!DNL Salesforce] -Instanz. |
| `auth.params.clientId` | Die mit Ihrem [!DNL Salesforce]-Konto verknüpfte Client-ID. |
| `auth.params.clientSecret` | Das Client-Geheimnis, das Ihrem [!DNL Salesforce]-Konto zugeordnet ist. |
| `auth.params.apiVersion` | Die REST-API-Version der von Ihnen verwendeten [!DNL Salesforce]-Instanz. |
| `connectionSpec.id` | Die [!DNL Salesforce] Verbindungsspezifikations-ID: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

>[!ENDTABS]

**Antwort**

Bei einer erfolgreichen Antwort wird Ihre neu erstellte Basisverbindung zusammen mit der eindeutigen ID zurückgegeben.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Salesforce]-Basisverbindung mithilfe der [!DNL Flow Service]-API erstellt. Sie können diese Basisverbindungs-ID in den folgenden Tutorials verwenden:

* [Erkunden von Struktur und Inhalten Ihrer Datentabellen mithilfe der  [!DNL Flow Service] -API](../../explore/tabular.md)
* [Erstellen Sie einen Datenfluss, um CRM-Daten mithilfe der [!DNL Flow Service] API an Platform zu übertragen.](../../collect/crm.md)
