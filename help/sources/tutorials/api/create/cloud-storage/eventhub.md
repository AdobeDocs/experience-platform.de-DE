---
keywords: Experience Platform; Startseite; beliebte Themen; Ereignis-Hub; Azure-Ereignis-Hub; Event-Hub
solution: Experience Platform
title: Erstellen einer Azure Event Hub-Quellverbindung mithilfe der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit einem Azure Event Hub-Konto verbinden.
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 8%

---


# Erstellen Sie eine [!DNL Azure Event Hubs] Quellverbindung mithilfe der [!DNL Flow Service] API

Dieses Tutorial führt Sie durch die Schritte zum Verbinden [!DNL Azure Event Hubs] (nachstehend &quot;genannt)[!DNL Event Hubs]&quot;) zur Experience Platform mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten zu strukturieren, zu beschriften und zu erweitern, indem Sie [!DNL Platform] Dienste.
- [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um eine erfolgreiche Verbindung herzustellen [!DNL Event Hubs] zur Plattform mithilfe der [!DNL Flow Service] API.

### Erforderliche Anmeldedaten sammeln

Zur [!DNL Flow Service] , um eine Verbindung mit Ihrer [!DNL Event Hubs] -Konto angeben, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `sasKeyName` | Der Name der Autorisierungsregel, der auch als SAS-Schlüsselname bezeichnet wird. |
| `sasKey` | Der Primärschlüssel der [!DNL Event Hubs] Namespace. Die `sasPolicy` dass `sasKey` muss `manage` -Berechtigungen, die für die [!DNL Event Hubs] Liste auszufüllen. |
| `namespace` | Der Namespace des [!DNL Event Hubs] auf. Ein [!DNL Event Hubs] Der Namespace stellt einen eindeutigen Scoping-Container bereit, in dem Sie einen oder mehrere [!DNL Event Hubs]. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die [!DNL Event Hubs] Verbindungsspezifikations-ID lautet: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

Weitere Informationen zu diesen Werten finden Sie unter [Dieses Ereignis-Hubs-Dokument](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

### Verwenden von Platform-APIs

Informationen zum erfolgreichen Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Basisverbindung erstellen

Der erste Schritt beim Erstellen einer Quellverbindung besteht darin, Ihre [!DNL Event Hubs] -Quelle und generieren Sie eine Basis-Verbindungs-ID. Mit einer Basis-Verbindungs-ID können Sie Dateien aus Ihrer Quelle durchsuchen und durchsuchen und bestimmte Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an die `/connections` Endpunkt beim Bereitstellen [!DNL Event Hubs] Authentifizierungsberechtigungen als Teil der Anfrageparameter.

**API-Format**

```http
POST /connections
```

**Anfrage**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.namespace` | Der Namespace des [!DNL Event Hubs] auf. |
| `connectionSpec.id` | Die [!DNL Event Hubs] Verbindungsspezifikations-ID lautet: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Basisverbindung zurück, einschließlich der eindeutigen Kennung (`id`). Diese Verbindungs-ID ist im nächsten Schritt erforderlich, um eine Quellverbindung zu erstellen.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Quellverbindung erstellen

Eine Quellverbindung erstellt und verwaltet die Verbindung zur externen Quelle, von der aus Daten erfasst werden. Eine Quellverbindung besteht aus Informationen wie Datenquelle, Datenformat und einer Quell-Verbindungs-ID, die zum Erstellen eines Datenflusses erforderlich sind. Eine Quellverbindungsinstanz ist für einen Mandanten und eine IMS-Organisation spezifisch.

Um eine Quellverbindung zu erstellen, stellen Sie eine POST-Anfrage an die `/sourceConnections` Endpunkt der [!DNL Flow Service] API.

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
    -H 'x-gw-ims-org-id: {IMS_Org}' \
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
            "eventHubName": "{EVENTHUB_NAME}",
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
| `connectionSpec.id` | Die ID der Festnetzverbindungsspezifikation für [!DNL Event Hubs]. Diese ID lautet: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |
| `data.format` | Das Format der [!DNL Event Hubs] -Daten, die Sie erfassen möchten. Derzeit wird nur das Datenformat `json`. |
| `params.eventHubName` | Der Name für Ihre [!DNL Event Hubs] -Quelle. |
| `params.dataType` | Dieser Parameter definiert den Typ der aufgenommenen Daten. Zu den unterstützten Datentypen gehören: `raw` und `xdm`. |
| `params.reset` | Dieser Parameter definiert, wie die Daten gelesen werden. Verwendung `latest` , um mit dem Lesen der neuesten Daten zu beginnen, und verwenden Sie `earliest` , um mit dem Lesen der ersten verfügbaren Daten im Stream zu beginnen. Dieser Parameter ist optional und standardmäßig `earliest` wenn nicht angegeben. |
| `params.consumerGroup` | Der Veröffentlichungs- oder Abonnementmechanismus, der für [!DNL Event Hubs]. Dieser Parameter ist optional und standardmäßig `$Default` wenn nicht angegeben. Siehe hierzu [[!DNL Event Hubs] Handbuch für Ereignisnutzer](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers) für weitere Informationen. |

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Event Hubs] Quellverbindung mithilfe der [!DNL Flow Service] API. Sie können diese Quell-Verbindungs-ID im nächsten Tutorial zu [Erstellen Sie einen Streaming-Datenfluss mit dem [!DNL Flow Service] API](../../collect/streaming.md).
