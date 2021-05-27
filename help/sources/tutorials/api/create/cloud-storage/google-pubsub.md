---
keywords: Experience Platform; Homepage; beliebte Themen; Google PubSub; Google Publisub
solution: Experience Platform
title: Erstellen einer Google PubSub-Quellverbindung mithilfe der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mit der Flow Service-API Adobe Experience Platform mit einem Google PubSub-Konto verbinden.
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: f13afbd70db18e5faa1a101300f3dc7ec944baa3
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 9%

---

# Erstellen einer [!DNL Google PubSub] Quellverbindung mithilfe der Flow Service-API

>[!NOTE]
>
>Der Connector [!DNL Google PubSub] befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectoren finden Sie unter [Quellen - Übersicht](../../../../home.md#terms-and-conditions) .

Dieses Tutorial führt Sie durch die Schritte, die erforderlich sind, um [!DNL Google PubSub] (im Folgenden &quot;a1/>&quot;) mit der -Experience Platform zu verbinden, indem Sie die [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) verwenden.[!DNL PubSub]

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Platform-Diensten zu strukturieren, zu beschriften und zu erweitern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um [!DNL PubSub] mithilfe der [!DNL Flow Service]-API erfolgreich mit Platform zu verbinden.

### Erforderliche Anmeldedaten sammeln

Damit [!DNL Flow Service] eine Verbindung zu [!DNL PubSub] herstellen kann, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `projectId` | Die Projekt-ID, die zum Authentifizieren von [!DNL PubSub] erforderlich ist. |
| `credentials` | Die zum Authentifizieren von [!DNL PubSub] erforderlichen Anmeldedaten oder Schlüssel. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich Authentifizierungsspezifikationen im Zusammenhang mit der Erstellung der Basis- und Quell-Target-Verbindungen. Die Verbindungsspezifikations-ID [!DNL PubSub] lautet: `70116022-a743-464a-bbfe-e226a7f8210c`. |

Weitere Informationen zu diesen Werten finden Sie in diesem Dokument [[!DNL PubSub] authentication](https://cloud.google.com/pubsub/docs/authentication) . Informationen zum Verwenden der dienstkontenbasierten Authentifizierung finden Sie in diesem [[!DNL PubSub] Handbuch zum Erstellen von Dienstkonten](https://cloud.google.com/docs/authentication/production#create_service_account) für Schritte zum Generieren Ihrer Anmeldedaten.

>[!TIP]
>
>Wenn Sie auf Dienstkonten basierende Authentifizierung verwenden, stellen Sie sicher, dass Sie ausreichend Benutzerzugriff auf Ihr Dienstkonto gewährt haben und dass im JSON keine zusätzlichen Leerzeichen vorhanden sind, wenn Sie Ihre Anmeldeinformationen kopieren und einfügen.

### Verwenden von Platform-APIs

Informationen dazu, wie Sie erfolgreich Aufrufe an Platform-APIs durchführen können, finden Sie im Handbuch [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Basisverbindung erstellen

Der erste Schritt beim Erstellen einer Quellverbindung besteht darin, Ihre [!DNL PubSub]-Quelle zu authentifizieren und eine Basis-Verbindungs-ID zu generieren. Mit einer Basis-Verbindungs-ID können Sie Dateien aus Ihrer Quelle durchsuchen und durchsuchen und bestimmte Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL PubSub]-Authentifizierungsdaten als Teil der Anfrageparameter an.

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
| `auth.params.projectId` | Die Projekt-ID, die zum Authentifizieren von [!DNL PubSub] erforderlich ist. |
| `auth.params.credentials` | Die zum Authentifizieren von [!DNL PubSub] erforderlichen Anmeldedaten oder Schlüssel. |
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
| `baseConnectionId` | Die Basis-Verbindungs-ID Ihrer [!DNL PubSub]-Quelle, die im vorherigen Schritt generiert wurde. |
| `connectionSpec.id` | Die ID der festen Verbindungsspezifikation für [!DNL PubSub]. Diese ID lautet : `70116022-a743-464a-bbfe-e226a7f8210c` |
| `data.format` | Das Format der [!DNL PubSub]-Daten, die Sie erfassen möchten. Derzeit ist das einzige unterstützte Datenformat `json`. |
| `params.topicId` | Die Themen-ID definiert die spezifische benannte Ressource, an die Nachrichten von Herausgebern gesendet werden |
| `params.subscriptionId` | Die Anmelde-ID definiert die spezifische benannte Ressource, die den Stream von Nachrichten aus einem bestimmten Thema darstellt, die an die abonnierende Anwendung gesendet werden sollen. |
| `params.dataType` | Dieser Parameter definiert den Typ der aufgenommenen Daten. Zu den unterstützten Datentypen gehören: `raw` und `xdm`. |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Quellverbindung zurück. Diese ID ist im nächsten Tutorial zum Erstellen eines Datenflusses erforderlich.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL PubSub]-Quellverbindung mit der [!DNL Flow Service]-API erstellt. Sie können diese Quell-Verbindungs-ID im nächsten Tutorial zu [Erstellen eines Streaming-Datenflusses mit der  [!DNL Flow Service] API](../../collect/streaming.md) verwenden.
