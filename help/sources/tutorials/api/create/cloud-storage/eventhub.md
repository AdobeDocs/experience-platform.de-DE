---
title: Erstellen einer Source-Verbindung mit Azure Event Hubs mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit einem Azure Event Hubs-Konto verbinden.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1496'
ht-degree: 30%

---

# Erstellen einer [!DNL Azure Event Hubs]-Quellverbindung mithilfe der [!DNL Flow Service]-API

>[!IMPORTANT]
>
>Die [!DNL Azure Event Hubs] ist im Quellkatalog für Benutzende verfügbar, die Real-Time Customer Data Platform Ultimate erworben haben.

Lesen Sie dieses Tutorial, um zu erfahren, wie Sie [!DNL Azure Event Hubs] (im Folgenden als &quot;[!DNL Event Hubs]&quot; bezeichnet) mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) mit Experience Platform verbinden.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Experience Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
- [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Experience Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um [!DNL Event Hubs] mithilfe der [!DNL Flow Service]-API erfolgreich mit Experience Platform verbinden zu können.

### Sammeln erforderlicher Anmeldedaten

Damit [!DNL Flow Service] eine Verbindung mit Ihrem [!DNL Event Hubs]-Konto herstellen können, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

>[!BEGINTABS]

>[!TAB Standardauthentifizierung]

| Anmeldedaten | Beschreibung |
| --- | --- |
| `sasKeyName` | Der Name der Autorisierungsregel, die auch als SAS-Schlüsselname bezeichnet wird. |
| `sasKey` | Der Primärschlüssel des [!DNL Event Hubs] Namespace. Für die `sasPolicy`, der die `sasKey` entspricht, müssen `manage` konfiguriert sein, damit die [!DNL Event Hubs] ausgefüllt werden kann. |
| `namespace` | Der Namespace der [!DNL Event Hub], auf die Sie zugreifen. Ein [!DNL Event Hub] Namespace bietet einen eindeutigen Container für die Berechnung des Umfangs, in dem Sie einen oder mehrere [!DNL Event Hubs] erstellen können. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Spezifikations-ID der [!DNL Event Hubs]-Verbindung lautet: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

>[!TAB SAS-Authentifizierung]

| Anmeldedaten | Beschreibung |
| --- | --- |
| `sasKeyName` | Der Name der Autorisierungsregel, die auch als SAS-Schlüsselname bezeichnet wird. |
| `sasKey` | Der Primärschlüssel des [!DNL Event Hubs] Namespace. Für die `sasPolicy`, der die `sasKey` entspricht, müssen `manage` konfiguriert sein, damit die [!DNL Event Hubs] ausgefüllt werden kann. |
| `namespace` | Der Namespace der [!DNL Event Hub], auf die Sie zugreifen. Ein [!DNL Event Hub] Namespace bietet einen eindeutigen Container für die Berechnung des Umfangs, in dem Sie einen oder mehrere [!DNL Event Hubs] erstellen können. |
| `eventHubName` | Geben Sie Ihren [!DNL Azure Event Hub] ein. Microsoft Weitere Informationen zu [&#128279;](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) finden Sie in der Dokumentation zu [!DNL Event Hub]. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Spezifikations-ID der [!DNL Event Hubs]-Verbindung lautet: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

Weitere Informationen zur SAS-Authentifizierung (Shared Access Signatures) für [!DNL Event Hubs] finden Sie im [[!DNL Azure] Handbuch zur Verwendung von SAS](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

>[!TAB Event Hub Azure Active Directory-Authentifizierung]

| Anmeldedaten | Beschreibung |
| --- | --- |
| `tenantId` | Die Mandanten-ID, von der Sie die Berechtigung anfordern möchten. Ihre Mandanten-ID kann als GUID oder benutzerfreundlicher Name formatiert sein. **Hinweis**: Die Mandanten-ID wird in der [!DNL Microsoft Azure] als „Verzeichnis-ID“ bezeichnet. |
| `clientId` | Die Ihrer App zugewiesene Anwendungs-ID. Sie können diese ID vom [!DNL Microsoft Entra ID] abrufen, in dem Sie Ihre [!DNL Azure Active Directory] registriert haben. |
| `clientSecretValue` | Das Client-Geheimnis, das zusammen mit der Client-ID zur Authentifizierung Ihrer App verwendet wird. Sie können Ihr Client-Geheimnis über das [!DNL Microsoft Entra ID]-Portal abrufen, in dem Sie Ihre [!DNL Azure Active Directory] registriert haben. |
| `namespace` | Der Namespace der [!DNL Event Hub], auf die Sie zugreifen. Ein [!DNL Event Hub] Namespace bietet einen eindeutigen Container für die Berechnung des Umfangs, in dem Sie einen oder mehrere [!DNL Event Hubs] erstellen können. |

Weitere Informationen zu [!DNL Azure Active Directory] finden Sie im [Azure-Handbuch zur Verwendung der Microsoft Entra ID](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application).

>[!TAB Authentifizierung für Azure Active Directory im Ereignis-Hub]

| Anmeldedaten | Beschreibung |
| --- | --- |
| `tenantId` | Die Mandanten-ID, von der Sie die Berechtigung anfordern möchten. Ihre Mandanten-ID kann als GUID oder benutzerfreundlicher Name formatiert sein. **Hinweis**: Die Mandanten-ID wird in der [!DNL Microsoft Azure] als „Verzeichnis-ID“ bezeichnet. |
| `clientId` | Die Ihrer App zugewiesene Anwendungs-ID. Sie können diese ID vom [!DNL Microsoft Entra ID] abrufen, in dem Sie Ihre [!DNL Azure Active Directory] registriert haben. |
| `clientSecretValue` | Das Client-Geheimnis, das zusammen mit der Client-ID zur Authentifizierung Ihrer App verwendet wird. Sie können Ihr Client-Geheimnis über das [!DNL Microsoft Entra ID]-Portal abrufen, in dem Sie Ihre [!DNL Azure Active Directory] registriert haben. |
| `namespace` | Der Namespace der [!DNL Event Hub], auf die Sie zugreifen. Ein [!DNL Event Hub] Namespace bietet einen eindeutigen Container für die Berechnung des Umfangs, in dem Sie einen oder mehrere [!DNL Event Hubs] erstellen können. |
| `eventHubName` | Geben Sie Ihren [!DNL Azure Event Hub] ein. Microsoft Weitere Informationen zu [&#128279;](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) finden Sie in der Dokumentation zu [!DNL Event Hub]. |

>[!ENDTABS]

Weitere Informationen zu diesen Werten finden Sie in [diesem Dokument zu Event Hubs](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

### Verwenden von Experience Platform-APIs

Informationen zum erfolgreichen Aufrufen von Experience Platform-APIs finden Sie im Handbuch unter [ mit Experience Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung

>[!TIP]
>
>Nach der Erstellung können Sie den Authentifizierungstyp einer [!DNL Event Hubs] Basisverbindung nicht mehr ändern. Um den Authentifizierungstyp zu ändern, müssen Sie eine neue Basisverbindung erstellen.

Der erste Schritt beim Erstellen einer Quellverbindung besteht darin, Ihre [!DNL Event Hubs]-Quelle zu authentifizieren und eine Basisverbindungs-ID zu generieren. Mittels einer Basisverbindungs-ID können Sie Dateien aus Ihrer Quelle durchsuchen, zwischen Dateien innerhalb der Quelle navigieren und bestimmte Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu Datentypen und Formaten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den `/connections`-Endpunkt beim Bereitstellen der [!DNL Event Hubs]-Authentifizierungs-Anmeldedaten als Teil der Anfrageparameter.

**API-Format**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Standardauthentifizierung]

Um ein Konto mit Standardauthentifizierung zu erstellen, stellen Sie eine POST-Anfrage an den `/connections`-Endpunkt und geben Sie dabei Werte für Ihre `sasKeyName`, `sasKey` und `namespace` an.

+++Anfrage

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Azure Event Hubs connection",
      "description": "Connector for Azure Event Hubs",
      "auth": {
          "specName": "Azure EventHub authentication credentials",
          "params": {
              "sasKeyName": "{SAS_KEY_NAME}",
              "sasKey": "{SAS_KEY}",
              "namespace": "{NAMESPACE}"
          }
      },
      "connectionSpec": {
          "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
          "version": "1.0"
      }
  }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.sasKeyName` | Der Name der Autorisierungsregel, die auch als SAS-Schlüsselname bezeichnet wird. |
| `auth.params.sasKey` | Die generierte Shared Access-Signatur. |
| `auth.params.namespace` | Der Namespace der [!DNL Event Hubs], auf die Sie zugreifen. |
| `connectionSpec.id` | Die Spezifikations-ID der [!DNL Event Hubs] ist: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++Antwort

Bei einer erfolgreichen Antwort werden Details zu der neu erstellten Basisverbindung zurückgegeben, einschließlich ihrer eindeutigen Kennung (`id`). Diese Verbindungs-ID ist im nächsten Schritt erforderlich, um eine Quellverbindung zu erstellen.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!TAB SAS-Authentifizierung]

Um ein Konto mit SAS-Authentifizierung zu erstellen, stellen Sie eine POST-Anfrage an den `/connections`-Endpunkt und geben Sie dabei Werte für Ihre `sasKeyName`, `sasKey`, `namespace` und `eventHubName` an.

+++Anfrage

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Azure Event Hubs connection",
      "description": "Connector for Azure Event Hubs",
      "auth": {
          "specName": "Azure EventHub authentication credentials",
          "params": {
              "sasKeyName": "{SAS_KEY_NAME}",
              "sasKey": "{SAS_KEY}",
              "namespace": "{NAMESPACE}",
              "eventHubName": "{EVENT_HUB_NAME} 
          }
      },
      "connectionSpec": {
          "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
          "version": "1.0"
      }
  }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.sasKeyName` | Der Name der Autorisierungsregel, die auch als SAS-Schlüsselname bezeichnet wird. |
| `auth.params.sasKey` | Die generierte Shared Access-Signatur. |
| `auth.params.namespace` | Der Namespace der [!DNL Event Hubs], auf die Sie zugreifen. |
| `params.eventHubName` | Der Name Ihrer [!DNL Event Hubs]. |
| `connectionSpec.id` | Die Spezifikations-ID der [!DNL Event Hubs] ist: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++Antwort

Bei einer erfolgreichen Antwort werden Details zu der neu erstellten Basisverbindung zurückgegeben, einschließlich ihrer eindeutigen Kennung (`id`). Diese Verbindungs-ID ist im nächsten Schritt erforderlich, um eine Quellverbindung zu erstellen.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!TAB Event Hub Azure Active Directory-Authentifizierung]

Um ein Konto mit Azure Active Directory-Authentifizierung zu erstellen, stellen Sie eine POST-Anfrage an den `/connections`-Endpunkt und geben Sie dabei Werte für Ihre `tenantId`, `clientId`, `clientSecretValue` und `namespace` an.

+++Anfrage

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Azure Event Hubs connection",
      "description": "Connector for Azure Event Hubs",
      "auth": {
          "specName": "Event Hub Azure Active Directory Auth",
          "params": {
              "tenantId": "{TENANT_ID}",
              "clientId": "{CLIENT_ID}",
              "clientSecretValue": "{CLIENT_SECRET_VALUE}",
              "namespace": "{NAMESPACE}" 
          }
      },
      "connectionSpec": {
          "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
          "version": "1.0"
      }
  }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.tenantId` | Die Mandanten-ID Ihrer Anwendung. **Hinweis**: Die Mandanten-ID wird in der [!DNL Microsoft Azure] als „Verzeichnis-ID“ bezeichnet. |
| `auth.params.clientId` | Die Client-ID Ihrer Organisation. |
| `auth.params.clientSecretValue` | Der Client-Geheimniswert Ihrer Organisation. |
| `auth.params.namespace` | Der Namespace der [!DNL Event Hubs], auf die Sie zugreifen. |
| `connectionSpec.id` | Die Spezifikations-ID der [!DNL Event Hubs] ist: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++Antwort

Bei einer erfolgreichen Antwort werden Details zu der neu erstellten Basisverbindung zurückgegeben, einschließlich ihrer eindeutigen Kennung (`id`). Diese Verbindungs-ID ist im nächsten Schritt erforderlich, um eine Quellverbindung zu erstellen.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!TAB Authentifizierung für Azure Active Directory im Ereignis-Hub]

Um ein Konto mit Azure Active Directory-Authentifizierung zu erstellen, stellen Sie eine POST-Anfrage an den `/connections`-Endpunkt und geben Sie dabei Werte für Ihre `tenantId`, `clientId`, `clientSecretValue`, `namespace` und `eventHubName` an.

+++Anfrage

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Azure Event Hubs connection",
      "description": "Connector for Azure Event Hubs",
      "auth": {
          "specName": "Event Hub Scoped Azure Active Directory Auth",
          "params": {
              "tenantId": "{TENANT_ID}",
              "clientId": "{CLIENT_ID}",
              "clientSecretValue": "{CLIENT_SECRET_VALUE}",
              "namespace": "{NAMESPACE}",
              "eventHubName": "{EVENT_HUB_NAME}" 
          }
      },
      "connectionSpec": {
          "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
          "version": "1.0"
      }
  }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.tenantId` | Die Mandanten-ID Ihrer Anwendung. **Hinweis**: Die Mandanten-ID wird in der [!DNL Microsoft Azure] als „Verzeichnis-ID“ bezeichnet. |
| `auth.params.clientId` | Die Client-ID Ihrer Organisation. |
| `auth.params.clientSecretValue` | Der Client-Geheimniswert Ihrer Organisation. |
| `auth.params.namespace` | Der Namespace der [!DNL Event Hubs], auf die Sie zugreifen. |
| `auth.params.eventHubName` | Der Name Ihrer [!DNL Event Hubs]. |
| `connectionSpec.id` | Die Spezifikations-ID der [!DNL Event Hubs] ist: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++Antwort

Bei einer erfolgreichen Antwort werden Details zu der neu erstellten Basisverbindung zurückgegeben, einschließlich ihrer eindeutigen Kennung (`id`). Diese Verbindungs-ID ist im nächsten Schritt erforderlich, um eine Quellverbindung zu erstellen.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!ENDTABS]

## Erstellen einer Quellverbindung

>[!TIP]
>
>Eine [!DNL Event Hubs] Verbrauchergruppe kann jeweils nur für einen einzigen Fluss verwendet werden.

Eine Quellverbindung erstellt und verwaltet die Verbindung zu der externen Quelle, aus der Daten erfasst werden. Eine Quellverbindung besteht aus Informationen wie Datenquelle, Datenformat und einer Quell-Verbindungs-ID, die zum Erzeugen eines Datenflusses erforderlich sind. Eine Quellverbindungsinstanz ist für einen Mandanten und eine Organisation spezifisch.

Um eine Quellverbindung zu erstellen, stellen Sie eine POST-Anfrage an den `/sourceConnections`-Endpunkt der [!DNL Flow Service]-API.

**API-Format**

```http
POST /sourceConnections
```

**Anfrage**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "Azure Event Hubs source connection",
      "description": "A source connection for Azure Event Hubs",
      "baseConnectionId": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
      "connectionSpec": {
          "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "eventHubName": "{EVENT_HUB_NAME}",
          "dataType": "raw",
          "reset": "latest",
          "consumerGroup": "{CONSUMER_GROUP}"
      }
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name Ihrer Quellverbindung. Stellen Sie sicher, dass der Name Ihrer Quellverbindung beschreibend ist, da Sie damit Informationen zu Ihrer Quellverbindung nachschlagen können. |
| `description` | Ein optionaler Wert, den Sie angeben können, um weitere Informationen zu Ihrer Quellverbindung einzuschließen. |
| `baseConnectionId` | Die Verbindungs-ID Ihrer [!DNL Event Hubs], die im vorherigen Schritt generiert wurde. |
| `connectionSpec.id` | Die feste Verbindungsspezifikations-ID für [!DNL Event Hubs]. Diese ID lautet: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |
| `data.format` | Das Format der [!DNL Event Hubs]-Daten, die Sie aufnehmen möchten. Derzeit wird nur das Datenformat `json` unterstützt. |
| `params.eventHubName` | Der Name Ihrer [!DNL Event Hubs]. |
| `params.dataType` | Dieser Parameter definiert den Typ der aufgenommenen Daten. Zu den unterstützten Datentypen gehören: `raw` und `xdm`. |
| `params.reset` | Dieser Parameter definiert, wie die Daten gelesen werden. Verwenden Sie `latest` , um mit dem Lesen der neuesten Daten zu beginnen, und `earliest` , um mit dem Lesen der ersten verfügbaren Daten im Stream zu beginnen. Dieser Parameter ist optional und auf `earliest` gesetzt, wenn er nicht angegeben wurde. |
| `params.consumerGroup` | Der Veröffentlichungs- oder Abonnementmechanismus, der für die [!DNL Event Hubs] verwendet werden soll. Dieser Parameter ist optional und auf `$Default` gesetzt, wenn er nicht angegeben wurde. Weitere Informationen finden Sie [[!DNL Event Hubs]  diesem Handbuch ](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers) Event-Verbraucher . **Hinweis**: Eine [!DNL Event Hubs] Verbrauchergruppe kann jeweils nur für einen einzigen Fluss verwendet werden. |

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Event Hubs]-Quellverbindung mithilfe der [!DNL Flow Service]-API erstellt. Sie können diese Quellverbindungs-ID im nächsten Tutorial verwenden, um [einen Streaming-Datenfluss mit der  [!DNL Flow Service] -API](../../collect/streaming.md) zu erstellen.
