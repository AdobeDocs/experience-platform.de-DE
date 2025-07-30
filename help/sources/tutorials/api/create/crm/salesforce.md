---
title: Verbinden von Salesforce mit Experience Platform mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit einem Salesforce-Konto verbinden.
exl-id: 43dd9ee5-4b87-4c8a-ac76-01b83c1226f6
source-git-commit: 56307d8457ba6d0046ad80a7c97405220aa6161c
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 17%

---

# Verbinden von [!DNL Salesforce] mit Experience Platform mithilfe der [!DNL Flow Service]-API

Lesen Sie dieses Handbuch, um zu erfahren, wie Sie Ihr [!DNL Salesforce]-Quellkonto mithilfe der [[!DNL Flow Service] API) mit Adobe Experience Platform ](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Experience Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Experience Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Verwenden von Experience Platform-APIs

Informationen zum erfolgreichen Aufrufen von Experience Platform-APIs finden Sie im Handbuch unter [ mit Experience Platform-APIs](../../../../../landing/api-guide.md).

## Verbinden von [!DNL Salesforce] mit Experience Platform auf [!DNL Azure] {#azure}

Lesen Sie die folgenden Schritte, um Informationen zum Verbinden Ihrer [!DNL Salesforce] mit Experience Platform auf [!DNL Azure] zu erhalten.

### Sammeln erforderlicher Anmeldedaten

>[!WARNING]
>
>Die Standardauthentifizierung für die [!DNL Salesforce] wird im Januar 2026 eingestellt. Sie müssen zur Authentifizierung mit Client-Anmeldeinformationen für OAuth 2 wechseln, um weiterhin die -Quelle verwenden und Daten von Ihrem [!DNL Salesforce]-Konto in Experience Platform aufnehmen zu können.

Die [!DNL Salesforce]-Quelle unterstützt die Standardauthentifizierung sowie OAuth2-Client-Anmeldeinformationen.

>[!BEGINTABS]

>[!TAB Einfache Authentifizierung]

Um Ihr [!DNL Salesforce]-Konto mit [!DNL Flow Service] über die Standardauthentifizierung zu verbinden, geben Sie Werte für die folgenden Anmeldeinformationen an:

| Anmeldedaten | Beschreibung |
| --- | --- |
| `environmentUrl` | Die URL der [!DNL Salesforce] Quellinstanz. Das Format für `environmentUrl` ist `https://[domain].my.salesforce.com`. |
| `username` | Der Benutzername für das [!DNL Salesforce] Benutzerkonto. |
| `password` | Das Kennwort für das [!DNL Salesforce] Benutzerkonto. |
| `securityToken` | Das Sicherheits-Token für das [!DNL Salesforce] Benutzerkonto. |
| `apiVersion` | (Optional) Die REST-API-Version der von Ihnen verwendeten [!DNL Salesforce]. Der Wert für die API-Version muss mit einer Dezimalzahl formatiert sein. Wenn Sie beispielsweise die API-Version `52` verwenden, müssen Sie den Wert als `52.0` eingeben. Wenn dieses Feld leer gelassen wird, verwendet Experience Platform automatisch die neueste verfügbare Version. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Salesforce] ist: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Weitere Informationen zu den ersten Schritten finden Sie [diesem Salesforce-Dokument](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

>[!TAB OAuth 2 Client-Anmeldedaten]

Um Ihr [!DNL Salesforce]-Konto mit [!DNL Flow Service] über Anmeldeinformationen für den OAuth 2-Client zu verbinden, geben Sie Werte für die folgenden Anmeldeinformationen an:

| Anmeldedaten | Beschreibung |
| --- | --- |
| `environmentUrl` | Die URL der [!DNL Salesforce] Quellinstanz. Das Format für `environmentUrl` ist `https://[domain].my.salesforce.com` |
| `clientId` | Die Client-ID wird im Rahmen der OAuth2-Authentifizierung zusammen mit dem Client-Geheimnis verwendet. Zusammen ermöglichen die Client-ID und das Client-Geheimnis, dass Ihre Anwendung im Namen Ihres Kontos betrieben wird, indem Sie Ihre Anwendung für die [!DNL Salesforce] identifizieren. |
| `clientSecret` | Das Client-Geheimnis wird zusammen mit der Client-ID als Teil der OAuth2-Authentifizierung verwendet. Zusammen ermöglichen die Client-ID und das Client-Geheimnis, dass Ihre Anwendung im Namen Ihres Kontos betrieben wird, indem Sie Ihre Anwendung für die [!DNL Salesforce] identifizieren. |
| `apiVersion` | Die REST-API-Version der von Ihnen verwendeten [!DNL Salesforce]. Der Wert für die API-Version muss mit einer Dezimalzahl formatiert sein. Wenn Sie beispielsweise die API-Version `52` verwenden, müssen Sie den Wert als `52.0` eingeben. Wenn dieses Feld leer gelassen wird, verwendet Experience Platform automatisch die neueste verfügbare Version. Dieser Wert ist für die Authentifizierung mit Client-Anmeldeinformationen für OAuth2 obligatorisch. |
| `includeDeletedObjects` | Ein boolescher Wert, der bestimmt, ob vorläufig gelöschte Datensätze einbezogen werden sollen. Wenn auf „true“ gesetzt, können vorläufig gelöschte Datensätze in Ihre [!DNL Salesforce]-Abfrage aufgenommen und von Ihrem -Konto in Experience Platform aufgenommen werden. Wenn Sie Ihre Konfiguration nicht angeben, ist dieser Wert standardmäßig auf `false` festgelegt. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Salesforce] ist: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Weitere Informationen zur Verwendung von OAuth für [!DNL Salesforce] finden Sie im [[!DNL Salesforce] Handbuch zu OAuth-Autorisierungsflüssen](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&type=5).

>[!ENDTABS]

### Erstellen einer Basisverbindung für [!DNL Salesforce] in Experience Platform auf [!DNL Azure]

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Experience Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen ID der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basisverbindung zu erstellen und Ihr [!DNL Salesforce]-Konto mit Experience Platform on [!DNL Azure] zu verbinden, stellen Sie eine POST-Anfrage an den `/connections`-Endpunkt und geben Sie im Anfragetext Ihre Anmeldeinformationen zur [!DNL Salesforce]-Authentifizierung an.

**API-Format**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Einfache Authentifizierung]

+++Anfrage

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Salesforce] mit einfacher Authentifizierung:

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
| `auth.params.environmentUrl` | Die URL Ihrer [!DNL Salesforce]. |
| `auth.params.username` | Der Benutzername, der Ihrem [!DNL Salesforce]-Konto zugeordnet ist. |
| `auth.params.password` | Das mit Ihrem [!DNL Salesforce]-Konto verknüpfte Kennwort. |
| `auth.params.securityToken` | Das Ihrem [!DNL Salesforce]-Konto zugeordnete Sicherheits-Token. |
| `connectionSpec.id` | Die Spezifikations-ID der [!DNL Salesforce]-Verbindung: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

+++

+++Antwort

Bei einer erfolgreichen Antwort wird Ihre neu erstellte Basisverbindung zusammen mit der eindeutigen ID zurückgegeben.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

+++

>[!TAB OAuth 2 Client-Anmeldedaten]

+++Anfrage

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Salesforce] mit OAuth 2-Client-Anmeldedaten:

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
            "apiVersion": "60.0",
            "includeDeletedObjects": true
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
| `auth.params.environmentUrl` | Die URL Ihrer [!DNL Salesforce]. |
| `auth.params.clientId` | Die mit Ihrem [!DNL Salesforce]-Konto verknüpfte Client-ID. |
| `auth.params.clientSecret` | Das mit Ihrem [!DNL Salesforce]-Konto verknüpfte Client-Geheimnis. |
| `auth.params.apiVersion` | Die REST-API-Version der von Ihnen verwendeten [!DNL Salesforce]. |
| `auth.params.includeDeletedObjects` | Ein boolescher Wert, der bestimmt, ob vorläufig gelöschte Datensätze einbezogen werden sollen. |
| `connectionSpec.id` | Die Spezifikations-ID der [!DNL Salesforce]-Verbindung: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

+++


+++Antwort

Bei einer erfolgreichen Antwort wird Ihre neu erstellte Basisverbindung zusammen mit der eindeutigen ID zurückgegeben.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

+++

>[!ENDTABS]

## Verbinden von [!DNL Salesforce] mit Experience Platform auf Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Dieser Abschnitt gilt für Implementierungen von Experience Platform, die auf Amazon Web Services (AWS) ausgeführt werden. Experience Platform, das auf AWS ausgeführt wird, steht derzeit einer begrenzten Anzahl von Kunden zur Verfügung. Weitere Informationen zur unterstützten Experience Platform-Infrastruktur finden Sie in der Übersicht zur [Experience Platform Multi-Cloud](../../../../../landing/multi-cloud.md).

Lesen Sie die folgenden Schritte, um Informationen zum Verbinden Ihrer [!DNL Salesforce] mit Experience Platform auf AWS zu erhalten.

### Voraussetzungen

Informationen zum Einrichten Ihres [!DNL Salesforce]-Kontos für die Verbindung zu Experience Platform auf AWS finden Sie in der [[!DNL Salesforce] Übersicht](../../../../connectors/crm/salesforce.md#aws).

### Erstellen einer Basisverbindung für [!DNL Salesforce] auf Experience Platform auf AWS

Um eine Basisverbindung zu erstellen und Ihr [!DNL Salesforce]-Konto mit Experience Platform auf AWS zu verbinden, stellen Sie eine POST-Anfrage an den `/connections`-Endpunkt und geben Sie die entsprechenden Werte für Ihre -Anmeldeinformationen an.

**API-Format**

```http
POST /connections
```

**Anfrage**

+++Auswählen, um die Anfrage anzuzeigen

Die folgende Anfrage erstellt eine Basisverbindung für die [!DNL Salesforce] in Experience Platform auf AWS.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Salesforce account on AWS",
      "description": "ACME Salesforce account on AWS",
      "auth": {
          "specName": "OAuth2 JWT Token Credential",
          "params":
            "jwtToken": "{JWT_TOKEN},
            "clientId": "xxxx",
            "clientSecret": "xxxx",
            "instanceUrl": "https://acme-enterprise-3126.my.salesforce.com"
        }
      },
      "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
      }
  }'
```

Informationen zum Abrufen Ihrer [!DNL Salesforce]-`jwtToken` finden Sie im Handbuch unter [Einrichten einer - [!DNL Salesforce]  für die Verbindung zu Experience Platform auf AWS](../../../../connectors/crm/salesforce.md#aws).

+++

**Antwort**

+++Auswählen, um die Antwort anzuzeigen

Bei einer erfolgreichen Antwort wird Ihre neu erstellte Basisverbindung zusammen mit der eindeutigen ID zurückgegeben.

```json
{
    "id": "3e908d3f-c390-482b-9f44-43d3d4f2eb82",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

+++

### Verbindungsstatus überprüfen

Um Ihren Verbindungsstatus zu überprüfen, stellen Sie eine GET-Anfrage an den `/connections`-Endpunkt und geben Sie die ID der Basisverbindung an, die im Erstellungsschritt generiert wurde.

**API-Format**

```http
GET /connections
```

**Anfrage**

+++Auswählen, um die Anfrage anzuzeigen

Die folgende Anfrage ruft Informationen zur Basisverbindungs-ID ab: `3e908d3f-c390-482b-9f44-43d3d4f2eb82`.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/3e908d3f-c390-482b-9f44-43d3d4f2eb82' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
```

+++

**Antwort**

>[!BEGINTABS]

>[!TAB Wird initialisiert]

+++Auswählen, um ein Beispiel für eine Antwort anzuzeigen

Die folgende Antwort zeigt Informationen zur Basisverbindungs-ID an: `3e908d3f-c390-482b-9f44-43d3d4f2eb82` im `initializing`.

```json
{
  "items": [
    {
      "id": "3e908d3f-c390-482b-9f44-43d3d4f2eb82",
      "createdAt": 1736506325115,
      "updatedAt": 1736506325717,
      "createdBy": "acme@techacct.adobe.com",
      "updatedBy": "acme@techacct.adobe.com",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_ID}",
      "name": "JWT Token Auth Authentication E2E-1736506322",
      "description": "Base Connection for salesforce E2E",
      "connectionSpec": {
        "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
        "version": "1.0"
      },
      "state": "initializing",
      "auth": {
        "specName": "OAuth2 JWT Token Credential",
        "params": {
          "jwtToken": "{JWT_TOKEN}",
          "clientId": "{CLIENT_ID}",
          "clientSecret": "{CLIENT_SECRET}",
          "instanceUrl": "https://acme-enterprise-3126.my.salesforce.com"
        }
      }
    }
  }
]
```

+++

>[!TAB Aktiviert]

+++Auswählen, um ein Beispiel für eine Antwort anzuzeigen

Die folgende Antwort zeigt Informationen zur Basisverbindungs-ID an: `3e908d3f-c390-482b-9f44-43d3d4f2eb82` im `enabled`.

```json
{
  "items": [
      {
        "id": "3e908d3f-c390-482b-9f44-43d3d4f2eb82",
        "createdAt": 1736506325115,
        "updatedAt": 1736506413299,
        "createdBy": "acme@techacct.adobe.com",
        "updatedBy": "acme@AdobeID",
        "createdClient": "{CREATED_CLIENT}",
        "updatedClient": "acme",
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "imsOrgId": "{ORG_ID}",
        "name": "JWT Token Auth Authentication E2E-1736506322",
        "description": "Base Connection for salesforce E2E",
        "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
        },
        "state": "enabled",
        "auth": {
          "specName": "OAuth2 JWT Token Credential",
          "params": {
            "jwtToken": "{JWT_TOKEN}",
            "clientId": "{CLIENT_ID}",
            "clientSecret": "{CLIENT_SECRET}",
            "instanceUrl": "https://adb8-dev-ed.develop.my.salesforce.com",
            "orgId": "00DdL000001iPRxUAM"
          }
        },
        "version": "\"6d27f305-40be-41c3-97d4-a701827c34df\"",
        "etag": "\"6d27f305-40be-41c3-97d4-a701827c34df\""
    }
  ]
}
```

+++

>[!ENDTABS]

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Salesforce]-Basisverbindung mithilfe der [!DNL Flow Service]-API erstellt. Sie können diese Basisverbindungs-ID in den folgenden Tutorials verwenden:

* [Erkunden von Struktur und Inhalten Ihrer Datentabellen mithilfe der  [!DNL Flow Service] -API](../../explore/tabular.md)
* [Erstellen eines Datenflusses, um CRM-Daten mithilfe der API  [!DNL Flow Service]  Experience Platform zu übertragen](../../collect/crm.md)
