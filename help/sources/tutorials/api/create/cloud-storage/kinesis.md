---
keywords: Experience Platform; Startseite; beliebte Themen; Kinesis; Kinese; Amazon Kinesis; Amazon-Kinesis
solution: Experience Platform
title: Erstellen einer Amazon Kinesis-Quellverbindung mithilfe der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mit der Flow Service-API eine Verbindung zwischen Adobe Experience Platform und einer Amazon Kinesis-Quelle herstellen.
exl-id: 64da8894-12ac-45a0-b03e-fe9b6aa435d3
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 8%

---

# Erstellen einer [!DNL Amazon Kinesis]-Quellverbindung mithilfe der Flow Service-API

Dieses Tutorial führt Sie durch die Schritte, die erforderlich sind, um [!DNL Amazon Kinesis] (im Folgenden &quot;a1/>&quot;) mit der -Experience Platform zu verbinden, indem Sie die [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) verwenden.[!DNL Kinesis]

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von  [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu erweitern.
* [Sandboxes](../../../../../sandboxes/home.md)[!DNL Platform]: Experience bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um [!DNL Kinesis] mithilfe der [!DNL Flow Service]-API erfolgreich mit Platform zu verbinden.

### Erforderliche Anmeldedaten sammeln

Damit [!DNL Flow Service] eine Verbindung zu Ihrem [!DNL Amazon Kinesis]-Konto herstellen kann, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `accessKeyId` | Die Zugriffsschlüssel-ID entspricht der Hälfte des Zugriffsschlüsselpaars, das zum Authentifizieren Ihres [!DNL Kinesis]-Kontos bei Platform verwendet wird. |
| `secretKey` | Der geheime Zugriffsschlüssel ist die andere Hälfte des Zugriffsschlüsselpaars, das zum Authentifizieren Ihres [!DNL Kinesis]-Kontos bei Platform verwendet wird. |
| `region` | Die Region für Ihr [!DNL Kinesis]-Konto. Weitere Informationen zu Regionen finden Sie im Handbuch zum Hinzufügen von IP-Adressen zu Ihrer Zulassungsliste](../../../../ip-address-allow-list.md).[ |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID [!DNL Kinesis] lautet: `86043421-563b-46ec-8e6c-e23184711bf6`. |

Weitere Informationen zu [!DNL Kinesis]-Zugriffsschlüsseln und deren Erstellung finden Sie in diesem [[!DNL AWS] Handbuch zum Verwalten von Zugriffsschlüsseln für IAM-Benutzer](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### Verwenden von Platform-APIs

Informationen dazu, wie Sie erfolgreich Aufrufe an Platform-APIs durchführen können, finden Sie im Handbuch [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Basisverbindung erstellen

Der erste Schritt beim Erstellen einer Quellverbindung besteht darin, Ihre [!DNL Kinesis]-Quelle zu authentifizieren und eine Basis-Verbindungs-ID zu generieren. Mit einer Basis-Verbindungs-ID können Sie Dateien aus Ihrer Quelle durchsuchen und durchsuchen und bestimmte Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL Kinesis]-Authentifizierungsdaten als Teil der Anfrageparameter an.

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
        "name": "Amazon Kinesis connection",
        "description": "Connector for Amazon Kinesis",
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "auth": {
            "specName": "Aws Kinesis authentication credentials",
            "params": {
                "accessKeyId": "{ACCESS_KEY_ID}",
                "secretKey": "{SECRET_KEY}",
                "region": "{REGION}"
            }
        },
        "connectionSpec": {
            "id": "86043421-563b-46ec-8e6c-e23184711bf6",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.accessKeyId` | Die Zugriffsschlüssel-ID für Ihr [!DNL Kinesis]-Konto. |
| `auth.params.secretKey` | Der geheime Zugriffsschlüssel für Ihr [!DNL Kinesis]-Konto. |
| `auth.params.region` | Die Region für Ihr [!DNL Kinesis]-Konto. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID [!DNL Kinesis]: `86043421-563b-46ec-8e6c-e23184711bf6` |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Basisverbindung zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist im nächsten Schritt erforderlich, um eine Quellverbindung zu erstellen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Quellverbindung erstellen {#source}

Eine Quellverbindung erstellt und verwaltet die Verbindung zur externen Quelle, von der aus Daten erfasst werden. Eine Quellverbindung besteht aus Informationen wie der Datenquelle, dem Datenformat und der Kennung der Quellverbindung, die zum Erstellen eines Datenflusses erforderlich ist. Eine Quellverbindungsinstanz ist für einen Mandanten und eine IMS-Organisation spezifisch.

Um eine Quellverbindung zu erstellen, stellen Sie eine POST-Anfrage an den `/sourceConnections`-Endpunkt der [!DNL Flow Service]-API.

**API-Format**

```http
POST /sourceConnections
```

**Anfrage**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "AWS Kinesis source connection",
        "description": "A source connection for AWS Kinesis",
        "baseConnectionId": "4cb0c374-d3bb-4557-b139-5712880adc55",
        "connectionSpec": {
            "id": "86043421-563b-46ec-8e6c-e23184711bf6",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "stream": "{STREAM}",
            "dataType": "raw",
            "reset": "latest"
        }
    }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name Ihrer Quellverbindung. Stellen Sie sicher, dass der Name Ihrer Quellverbindung beschreibend ist, da Sie damit Informationen zu Ihrer Quellverbindung nachschlagen können. |
| `description` | Ein optionaler Wert, den Sie angeben können, um weitere Informationen zu Ihrer Quellverbindung einzuschließen. |
| `baseConnectionId` | Die Basis-Verbindungs-ID Ihrer [!DNL Kinesis]-Quelle, die im vorherigen Schritt generiert wurde. |
| `connectionSpec.id` | Die ID der festen Verbindungsspezifikation für [!DNL Kinesis]. Diese ID lautet : `86043421-563b-46ec-8e6c-e23184711bf6` |
| `data.format` | Das Format der [!DNL Kinesis]-Daten, die Sie erfassen möchten. Derzeit ist das einzige unterstützte Datenformat `json`. |
| `params.stream` | Der Name des Datenstreams, aus dem Datensätze abgerufen werden sollen. |
| `params.dataType` | Dieser Parameter definiert den Typ der aufgenommenen Daten. Zu den unterstützten Datentypen gehören: `raw` und `xdm`. |
| `params.reset` | Dieser Parameter definiert, wie die Daten gelesen werden. Verwenden Sie `latest`, um mit dem Lesen der neuesten Daten zu beginnen, und verwenden Sie `earliest`, um mit dem Lesen der ersten verfügbaren Daten im Stream zu beginnen. |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Quellverbindung zurück. Diese ID ist im nächsten Tutorial zum Erstellen eines Datenflusses erforderlich.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Kinesis]-Quellverbindung mit der [!DNL Flow Service]-API erstellt. Sie können diese Quell-Verbindungs-ID im nächsten Tutorial zu [Erstellen eines Streaming-Datenflusses mit der  [!DNL Flow Service] API](../../collect/streaming.md) verwenden.
