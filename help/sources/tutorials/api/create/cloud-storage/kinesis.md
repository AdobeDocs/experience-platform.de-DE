---
title: Erstellen einer Amazon Kinesis Source-Verbindung mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit einer Amazon Kinesis-Quelle verbinden.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 64da8894-12ac-45a0-b03e-fe9b6aa435d3
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 50%

---

# Erstellen einer [!DNL Amazon Kinesis]-Quellverbindung mithilfe der Flow Service-API

>[!IMPORTANT]
>
>Die [!DNL Amazon Kinesis] ist im Quellkatalog für Benutzende verfügbar, die Real-Time Customer Data Platform Ultimate erworben haben.

Dieses Tutorial führt Sie durch die Schritte zum Verbinden [!DNL Amazon Kinesis] (nachstehend „[!DNL Kinesis]“ genannt) mit Experience Platform mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Experience Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne [!DNL Experience Platform] in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um [!DNL Kinesis] mithilfe der [!DNL Flow Service]-API erfolgreich mit Experience Platform verbinden zu können.

### Sammeln erforderlicher Anmeldedaten

Damit [!DNL Flow Service] eine Verbindung mit Ihrem [!DNL Amazon Kinesis]-Konto herstellen können, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `accessKeyId` | Die Zugriffsschlüssel-ID entspricht der Hälfte des Zugriffsschlüsselpaars, das zum Authentifizieren Ihres [!DNL Kinesis]-Kontos bei Experience Platform verwendet wird. |
| `secretKey` | Der geheime Zugriffsschlüssel ist die andere Hälfte des Zugriffsschlüsselpaars, das zum Authentifizieren Ihres [!DNL Kinesis]-Kontos bei Experience Platform verwendet wird. |
| `region` | Die Region für Ihr [!DNL Kinesis]. Weitere Informationen zu Regionen [ Sie im Handbuch zum Hinzufügen von IP](../../../../ip-address-allow-list.md)Adressen zu Ihrer Zulassungsliste . |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Spezifikations-ID der [!DNL Kinesis]-Verbindung lautet: `86043421-563b-46ec-8e6c-e23184711bf6`. |

Weiterführende Informationen zu [!DNL Kinesis] Zugriffsschlüsseln und deren Generierung finden Sie in diesem [[!DNL AWS] Handbuch zum Verwalten von Zugriffsschlüsseln für IAM-Benutzer](https://docs.aws.amazon.com/de_de/IAM/latest/UserGuide/id_credentials_access-keys.html).

### Verwenden von Experience Platform-APIs

Informationen zum erfolgreichen Aufrufen von Experience Platform-APIs finden Sie im Handbuch unter [ mit Experience Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung

Der erste Schritt beim Erstellen einer Quellverbindung besteht darin, Ihre [!DNL Kinesis]-Quelle zu authentifizieren und eine Basisverbindungs-ID zu generieren. Mittels einer Basisverbindungs-ID können Sie Dateien aus Ihrer Quelle durchsuchen, zwischen Dateien innerhalb der Quelle navigieren und bestimmte Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu Datentypen und Formaten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den `/connections`-Endpunkt beim Bereitstellen der [!DNL Kinesis]-Authentifizierungs-Anmeldedaten als Teil der Anfrageparameter.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.accessKeyId` | Die Zugriffsschlüssel-ID für Ihr [!DNL Kinesis]. |
| `auth.params.secretKey` | Der geheime Zugriffsschlüssel für Ihr [!DNL Kinesis]. |
| `auth.params.region` | Die Region für Ihr [!DNL Kinesis]. |
| `connectionSpec.id` | Die [!DNL Kinesis]-Verbindungsspezifikations-ID: `86043421-563b-46ec-8e6c-e23184711bf6` |

**Antwort**

Bei einer erfolgreichen Antwort werden Details zu der neu erstellten Basisverbindung zurückgegeben, einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist im nächsten Schritt erforderlich, um eine Quellverbindung zu erstellen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Erstellen einer Quellverbindung {#source}

Eine Quellverbindung erstellt und verwaltet die Verbindung zu der externen Quelle, aus der Daten erfasst werden. Eine Quellverbindung besteht aus Informationen wie Datenquelle, Datenformat und der Quellverbindungs-ID, die zum Erstellen eines Datenflusses erforderlich sind. Eine Quellverbindungsinstanz ist für einen Mandanten und eine Organisation spezifisch.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `baseConnectionId` | Die ID der Basisverbindung Ihrer [!DNL Kinesis]-Quelle, die im vorhergehenden Schritt generiert wurde. |
| `connectionSpec.id` | Die feste Verbindungsspezifikations-ID für [!DNL Kinesis]. Diese ID lautet: `86043421-563b-46ec-8e6c-e23184711bf6` |
| `data.format` | Das Format der [!DNL Kinesis]-Daten, die Sie aufnehmen möchten. Derzeit wird nur das Datenformat `json` unterstützt. |
| `params.stream` | Der Name des Datenstroms, aus dem Datensätze abgerufen werden sollen. |
| `params.dataType` | Dieser Parameter definiert den Typ der aufgenommenen Daten. Zu den unterstützten Datentypen gehören: `raw` und `xdm`. |
| `params.reset` | Dieser Parameter definiert, wie die Daten gelesen werden. Verwenden Sie `latest` , um mit dem Lesen der neuesten Daten zu beginnen, und `earliest` , um mit dem Lesen der ersten verfügbaren Daten im Stream zu beginnen. |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Quellverbindung zurück. Diese ID ist im nächsten Tutorial zum Erstellen eines Datenflusses erforderlich.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

>[!NOTE]
>
>Nachdem Sie einen Streaming-Datenfluss erstellt oder aktualisiert haben, ist eine kurze 5-minütige Pause bei der Datenaufnahme erforderlich, um potenzielle Instanzen von Datenverlust oder Datenverlust zu verhindern.

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Kinesis]-Quellverbindung mithilfe der [!DNL Flow Service]-API erstellt. Sie können diese Quellverbindungs-ID im nächsten Tutorial verwenden, um [einen Streaming-Datenfluss mit der  [!DNL Flow Service] -API](../../collect/streaming.md) zu erstellen.
