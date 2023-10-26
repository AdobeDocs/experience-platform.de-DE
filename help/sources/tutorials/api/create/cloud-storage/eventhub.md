---
title: Erstellen einer Azure Event Hub-Quellverbindung mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit einem Azure Event Hub-Konto verbinden.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 46%

---

# Erstellen Sie eine [!DNL Azure Event Hubs] Quellverbindung mithilfe der [!DNL Flow Service] API

>[!IMPORTANT]
>
>Die [!DNL Azure Event Hubs] -Quelle ist im Quellkatalog für Benutzer verfügbar, die Real-time Customer Data Platform Ultimate erworben haben.

In diesem Tutorial werden Schritte zum Erstellen eines [!DNL Azure Event Hubs] (nachstehend &quot;genannt)[!DNL Event Hubs]&quot;) zu Experience Platform, unter Verwendung der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
- [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um [!DNL Event Hubs] mithilfe der [!DNL Flow Service]-API erfolgreich mit Platform verbinden zu können.

### Sammeln erforderlicher Anmeldeinformationen

Zur [!DNL Flow Service] , um eine Verbindung mit Ihrer [!DNL Event Hubs] -Konto angeben, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

>[!BEGINTABS]

>[!TAB Standardauthentifizierung]

| Anmeldedaten | Beschreibung |
| --- | --- |
| `sasKeyName` | Der Name der Autorisierungsregel, der auch als SAS-Schlüsselname bezeichnet wird. |
| `sasKey` | Der Primärschlüssel der [!DNL Event Hubs] Namespace. Die `sasPolicy` dass `sasKey` muss `manage` -Berechtigungen, die für die [!DNL Event Hubs] Liste auszufüllen. |
| `namespace` | Der Namespace des [!DNL Event Hubs] auf die Sie zugreifen. Ein [!DNL Event Hubs] Der Namespace stellt einen eindeutigen Scoping-Container bereit, in dem Sie einen oder mehrere [!DNL Event Hubs]. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Spezifikations-ID der [!DNL Event Hubs]-Verbindung lautet: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

>[!TAB SAS-Authentifizierung]

| Anmeldedaten | Beschreibung |
| --- | --- |
| `sasKeyName` | Der Name der Autorisierungsregel, der auch als SAS-Schlüsselname bezeichnet wird. |
| `sasKey` | Der Primärschlüssel der [!DNL Event Hubs] Namespace. Die `sasPolicy` dass `sasKey` muss `manage` -Berechtigungen, die für die [!DNL Event Hubs] Liste auszufüllen. |
| `namespace` | Der Namespace des [!DNL Event Hubs] auf die Sie zugreifen. Ein [!DNL Event Hubs] Der Namespace stellt einen eindeutigen Scoping-Container bereit, in dem Sie einen oder mehrere [!DNL Event Hubs]. |
| `eventHubName` | Der Name für Ihre [!DNL Event Hubs] -Quelle. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Spezifikations-ID der [!DNL Event Hubs]-Verbindung lautet: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

>[!ENDTABS]

Weitere Informationen zu diesen Werten finden Sie unter [Dieses Ereignis-Hubs-Dokument](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

### Verwenden von Platform-APIs

Informationen zum Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung

>[!TIP]
>
>Nach der Erstellung können Sie den Authentifizierungstyp eines [!DNL Event Hubs] Basisverbindung. Um den Authentifizierungstyp zu ändern, müssen Sie eine neue Basisverbindung erstellen.

Der erste Schritt beim Erstellen einer Quellverbindung besteht darin, Ihre [!DNL Event Hubs]-Quelle zu authentifizieren und eine Basisverbindungs-ID zu generieren. Mittels einer Basisverbindungs-ID können Sie Dateien aus Ihrer Quelle durchsuchen, zwischen Dateien innerhalb der Quelle navigieren und bestimmte Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu Datentypen und Formaten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den `/connections`-Endpunkt beim Bereitstellen der [!DNL Event Hubs]-Authentifizierungsberechtigungsdaten als Teil der Anfrageparameter.

**API-Format**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Standardauthentifizierung]

Um ein Konto mit Standardauthentifizierung zu erstellen, stellen Sie eine POST-Anfrage an die `/connections` Endpunkt beim Bereitstellen von Werten für Ihre `sasKeyName`, `sasKey`, und `namespace`.

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
| `auth.params.sasKeyName` | Der Name der Autorisierungsregel, der auch als SAS-Schlüsselname bezeichnet wird. |
| `auth.params.sasKey` | Die generierte Signatur für den freigegebenen Zugriff. |
| `auth.params.namespace` | Der Namespace des [!DNL Event Hubs] auf die Sie zugreifen. |
| `connectionSpec.id` | Die Spezifikations-ID der [!DNL Event Hubs]-Verbindung lautet: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

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

Um ein Konto mit SAS-Authentifizierung zu erstellen, stellen Sie eine POST-Anfrage an die `/connections` Endpunkt beim Bereitstellen von Werten für Ihre `sasKeyName`, `sasKey`,`namespace`, und `eventHubName`.

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
| `auth.params.sasKeyName` | Der Name der Autorisierungsregel, der auch als SAS-Schlüsselname bezeichnet wird. |
| `auth.params.sasKey` | Die generierte Signatur für den freigegebenen Zugriff. |
| `auth.params.namespace` | Der Namespace des [!DNL Event Hubs] auf die Sie zugreifen. |
| `params.eventHubName` | Der Name für Ihre [!DNL Event Hubs] -Quelle. |
| `connectionSpec.id` | Die Spezifikations-ID der [!DNL Event Hubs]-Verbindung lautet: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

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
>Ein [!DNL Event Hubs] Die Benutzergruppe kann nur für einen einzelnen Fluss gleichzeitig verwendet werden.

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
| `baseConnectionId` | Die Verbindungs-ID Ihrer [!DNL Event Hubs] -Quelle, die im vorherigen Schritt generiert wurde. |
| `connectionSpec.id` | Die feste Verbindungsspezifikations-ID für [!DNL Event Hubs]. Diese ID lautet: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |
| `data.format` | Das Format der [!DNL Event Hubs]-Daten, die Sie aufnehmen möchten. Derzeit wird nur das Datenformat `json` unterstützt. |
| `params.eventHubName` | Der Name für Ihre [!DNL Event Hubs] -Quelle. |
| `params.dataType` | Dieser Parameter definiert den Typ der aufgenommenen Daten. Zu den unterstützten Datentypen gehören: `raw` und `xdm`. |
| `params.reset` | Dieser Parameter definiert, wie die Daten gelesen werden. Verwendung `latest` , um mit dem Lesen der neuesten Daten zu beginnen, und verwenden Sie `earliest` , um mit dem Lesen der ersten verfügbaren Daten im Stream zu beginnen. Dieser Parameter ist optional und standardmäßig `earliest` wenn nicht angegeben. |
| `params.consumerGroup` | Der Veröffentlichungs- oder Abonnementmechanismus, der für [!DNL Event Hubs]. Dieser Parameter ist optional und standardmäßig `$Default` wenn nicht angegeben. Siehe hierzu [[!DNL Event Hubs] Handbuch für Ereignisnutzer](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers) für weitere Informationen. **Hinweis**: ein [!DNL Event Hubs] Die Benutzergruppe kann nur für einen einzelnen Fluss gleichzeitig verwendet werden. |

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Event Hubs] Quellverbindung mithilfe der [!DNL Flow Service] API. Sie können diese Quellverbindungs-ID im nächsten Tutorial verwenden, um [einen Streaming-Datenfluss mit der  [!DNL Flow Service] -API](../../collect/streaming.md) zu erstellen.
