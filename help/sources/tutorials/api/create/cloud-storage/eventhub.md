---
keywords: Experience Platform; Startseite; beliebte Themen; Ereignis-Hub; Azure-Ereignis-Hub; Event-Hub
solution: Experience Platform
title: Erstellen einer Azure Event Hub-Quellverbindung mithilfe der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit einem Azure Event Hub-Konto verbinden.
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 8%

---


# Erstellen einer [!DNL Azure Event Hubs]-Quellverbindung mithilfe der [!DNL Flow Service]-API

Dieses Tutorial führt Sie durch die Schritte, die erforderlich sind, um [!DNL Azure Event Hubs] (im Folgenden &quot;a1/>&quot;) mit der -Experience Platform zu verbinden, indem Sie die [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) verwenden.[!DNL Event Hubs]

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Quellen](../../../../home.md):  [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von  [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu erweitern.
- [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um [!DNL Event Hubs] mithilfe der [!DNL Flow Service]-API erfolgreich mit Platform zu verbinden.

### Erforderliche Anmeldedaten sammeln

Damit [!DNL Flow Service] eine Verbindung zu Ihrem [!DNL Event Hubs]-Konto herstellen kann, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `sasKeyName` | Der Name der Autorisierungsregel, der auch als SAS-Schlüsselname bezeichnet wird. |
| `sasKey` | Die generierte Signatur für den freigegebenen Zugriff. |
| `namespace` | Der Namespace des [!DNL Event Hubs], auf den Sie zugreifen. Ein [!DNL Event Hubs]-Namespace stellt einen eindeutigen Scoping-Container bereit, in dem Sie einen oder mehrere [!DNL Event Hubs] erstellen können. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID [!DNL Event Hubs] lautet: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

Weitere Informationen zu diesen Werten finden Sie in [diesem Ereignis-Hubs-Dokument](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

### Verwenden von Platform-APIs

Informationen dazu, wie Sie erfolgreich Aufrufe an Platform-APIs durchführen können, finden Sie im Handbuch [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Basisverbindung erstellen

Der erste Schritt beim Erstellen einer Quellverbindung besteht darin, Ihre [!DNL Event Hubs]-Quelle zu authentifizieren und eine Basis-Verbindungs-ID zu generieren. Mit einer Basis-Verbindungs-ID können Sie Dateien aus Ihrer Quelle durchsuchen und durchsuchen und bestimmte Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL Event Hubs]-Authentifizierungsdaten als Teil der Anfrageparameter an.

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
| `auth.params.namespace` | Der Namespace des [!DNL Event Hubs], auf den Sie zugreifen. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID [!DNL Event Hubs] lautet: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

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
| `baseConnectionId` | Die Verbindungs-ID Ihrer [!DNL Event Hubs]-Quelle, die im vorherigen Schritt generiert wurde. |
| `connectionSpec.id` | Die ID der festen Verbindungsspezifikation für [!DNL Event Hubs]. Diese ID lautet : `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |
| `data.format` | Das Format der [!DNL Event Hubs]-Daten, die Sie erfassen möchten. Derzeit ist das einzige unterstützte Datenformat `json`. |
| `params.eventHubName` | Der Name für Ihre [!DNL Event Hubs]-Quelle. |
| `params.dataType` | Dieser Parameter definiert den Typ der aufgenommenen Daten. Zu den unterstützten Datentypen gehören: `raw` und `xdm`. |
| `params.reset` | Dieser Parameter definiert, wie die Daten gelesen werden. Verwenden Sie `latest`, um mit dem Lesen der neuesten Daten zu beginnen, und verwenden Sie `earliest`, um mit dem Lesen der ersten verfügbaren Daten im Stream zu beginnen. Dieser Parameter ist optional und wird standardmäßig auf `earliest` gesetzt, falls nicht angegeben. |
| `params.consumerGroup` | Der Veröffentlichungs- oder Abonnementmechanismus, der für [!DNL Event Hubs] verwendet werden soll. Dieser Parameter ist optional und wird standardmäßig auf `$Default` gesetzt, falls nicht angegeben. Weitere Informationen finden Sie in diesem [[!DNL Event Hubs] Handbuch zu Ereigniskonsumenten](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers) . |

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Event Hubs]-Quellverbindung mit der [!DNL Flow Service]-API erstellt. Sie können diese Quell-Verbindungs-ID im nächsten Tutorial zu [Erstellen eines Streaming-Datenflusses mit der  [!DNL Flow Service] API](../../collect/streaming.md) verwenden.
