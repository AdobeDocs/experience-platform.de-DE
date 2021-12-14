---
keywords: Experience Platform;home;popular topics;Google PubSub;google pubsub
solution: Experience Platform
title: Erstellen einer Google PubSub-Quellverbindung mit der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit einem Google PubSub-Konto verbinden.
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 8%

---

# Erstellen Sie eine [!DNL Google PubSub] Quellverbindung mithilfe der Flow Service-API

>[!NOTE]
>
>Die [!DNL Google PubSub] -Connector befindet sich in der Beta-Phase. Siehe [Quellen - Übersicht](../../../../home.md#terms-and-conditions) Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectoren.

Dieses Tutorial führt Sie durch die Schritte zum Verbinden [!DNL Google PubSub] (nachstehend &quot;genannt)[!DNL PubSub]&quot;) zur Experience Platform mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Platform-Diensten zu strukturieren, zu beschriften und zu erweitern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um eine erfolgreiche Verbindung herzustellen [!DNL PubSub] zur Plattform mithilfe der [!DNL Flow Service] API.

### Erforderliche Anmeldedaten sammeln

Zur [!DNL Flow Service] zur Verbindung mit [!DNL PubSub]müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `projectId` | Die zum Authentifizieren erforderliche Projekt-ID [!DNL PubSub]. |
| `credentials` | Die zum Authentifizieren erforderliche Berechtigung oder der Schlüssel [!DNL PubSub]. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich Authentifizierungsspezifikationen im Zusammenhang mit der Erstellung der Basis- und Quell-Target-Verbindungen. Die [!DNL PubSub] Verbindungsspezifikations-ID lautet: `70116022-a743-464a-bbfe-e226a7f8210c`. |

Weitere Informationen zu diesen Werten finden Sie in diesem [[!DNL PubSub] Authentifizierung](https://cloud.google.com/pubsub/docs/authentication) Dokument. Informationen zur Verwendung der dienstkontenbasierten Authentifizierung finden Sie in diesem [[!DNL PubSub] Handbuch zum Erstellen von Dienstkonten](https://cloud.google.com/docs/authentication/production#create_service_account) für Schritte zum Generieren Ihrer Anmeldedaten.

>[!TIP]
>
>Wenn Sie auf Dienstkonten basierende Authentifizierung verwenden, stellen Sie sicher, dass Sie ausreichend Benutzerzugriff auf Ihr Dienstkonto gewährt haben und dass im JSON keine zusätzlichen Leerzeichen vorhanden sind, wenn Sie Ihre Anmeldeinformationen kopieren und einfügen.

### Verwenden von Platform-APIs

Informationen zum erfolgreichen Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Basisverbindung erstellen

Der erste Schritt beim Erstellen einer Quellverbindung besteht darin, Ihre [!DNL PubSub] -Quelle und generieren Sie eine Basis-Verbindungs-ID. Mit einer Basis-Verbindungs-ID können Sie Dateien aus Ihrer Quelle durchsuchen und durchsuchen und bestimmte Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an die `/connections` Endpunkt beim Bereitstellen [!DNL PubSub] Authentifizierungsberechtigungen als Teil der Anfrageparameter.

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
        "name": "Google PubSub connection",
        "description": "Google PubSub connection",
        "auth": {
            "specName": "Google PubSub authentication credentials",
            "params": {
                "projectId": "{PROJECT_ID}",
                "credentials": "{CREDENTIALS}"
            }
        },
        "connectionSpec": {
            "id": "70116022-a743-464a-bbfe-e226a7f8210c",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.projectId` | Die zum Authentifizieren erforderliche Projekt-ID [!DNL PubSub]. |
| `auth.params.credentials` | Die zum Authentifizieren erforderliche Berechtigung oder der Schlüssel [!DNL PubSub]. |
| `connectionSpec.id` | Die [!DNL PubSub] Verbindungsspezifikations-ID: `70116022-a743-464a-bbfe-e226a7f8210c`. |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Verbindung zurück, einschließlich der eindeutigen Kennung (`id`). Diese Basis-Verbindungs-ID ist im nächsten Schritt erforderlich, um eine Quellverbindung zu erstellen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Quellverbindung erstellen {#source}

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
        "name": "Google PubSub source connection",
        "description": "A source connection for Google PubSub",
        "baseConnectionId": "4cb0c374-d3bb-4557-b139-5712880adc55",
        "connectionSpec": {
            "id": "70116022-a743-464a-bbfe-e226a7f8210c",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "topicId": "{TOPIC_ID}",
            "subscriptionId": "{SUBSCRIPTION_ID}",
            "dataType": "raw"
        }
    }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name Ihrer Quellverbindung. Stellen Sie sicher, dass der Name Ihrer Quellverbindung beschreibend ist, da Sie damit Informationen zu Ihrer Quellverbindung nachschlagen können. |
| `description` | Ein optionaler Wert, den Sie angeben können, um weitere Informationen zu Ihrer Quellverbindung einzuschließen. |
| `baseConnectionId` | Die Kennung der Basisverbindung Ihrer [!DNL PubSub] -Quelle, die im vorherigen Schritt generiert wurde. |
| `connectionSpec.id` | Die ID der Festnetzverbindungsspezifikation für [!DNL PubSub]. Diese ID lautet: `70116022-a743-464a-bbfe-e226a7f8210c` |
| `data.format` | Das Format der [!DNL PubSub] -Daten, die Sie erfassen möchten. Derzeit wird nur das Datenformat `json`. |
| `params.topicId` | Die Themen-ID definiert die spezifische benannte Ressource, an die Nachrichten von Herausgebern gesendet werden |
| `params.subscriptionId` | Die Anmelde-ID definiert die spezifische benannte Ressource, die den Stream von Nachrichten aus einem bestimmten Thema darstellt, die an die abonnierende Anwendung gesendet werden sollen. |
| `params.dataType` | Dieser Parameter definiert den Typ der aufgenommenen Daten. Zu den unterstützten Datentypen gehören: `raw` und `xdm`. |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Quellverbindung. Diese ID ist im nächsten Tutorial zum Erstellen eines Datenflusses erforderlich.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL PubSub] Quellverbindung mithilfe der [!DNL Flow Service] API. Sie können diese Quell-Verbindungs-ID im nächsten Tutorial zu [Erstellen Sie einen Streaming-Datenfluss mit dem [!DNL Flow Service] API](../../collect/streaming.md).
