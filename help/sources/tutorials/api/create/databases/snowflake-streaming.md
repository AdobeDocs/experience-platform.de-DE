---
title: Snowflake-Streaming-Konto mit Adobe Experience Platform verbinden
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit Snowflake-Streaming verbinden.
badgeBeta: label="Beta" type="Informative"
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 3fc225a4-746c-4a91-aa77-bbeb091ec364
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 26%

---

# [!DNL Snowflake]-Daten mithilfe der [!DNL Flow Service]-API an Experience Platform streamen

>[!IMPORTANT]
>
>* Die Streaming-Quelle [!DNL Snowflake] befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta-beschrifteten Quellen finden Sie in der [Quellen - Übersicht](../../../../home.md#terms-and-conditions) .
>* Die Streaming-Quelle [!DNL Snowflake] steht in der API Benutzern zur Verfügung, die Real-time Customer Data Platform Ultimate erworben haben.

In diesem Tutorial erfahren Sie, wie Sie mithilfe der [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>) Daten von Ihrem [!DNL Snowflake]-Konto mit Adobe Experience Platform verbinden und streamen können.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Für die erforderliche Einrichtung und Informationen zur Streaming-Quelle [!DNL Snowflake]. Lesen Sie die [[!DNL Snowflake] Streaming-Quellübersicht](../../../../connectors/databases/snowflake-streaming.md).

### Verwenden von Platform-APIs

Informationen zum Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung {#create-a-base-connection}

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den `/connections` -Endpunkt und geben Sie dabei Ihre [!DNL Snowflake]-Authentifizierungsdaten als Teil des Anfragetexts an.

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Snowflake]:

>[!TIP]
>
>Der Wert `auth.specName` muss genau wie im folgenden Beispiel eingegeben werden, einschließlich der Leerzeichen.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection",
      "description": "Snowflake base connection",
      "auth": {
          "specName": "Basic Authentication for Snowflake",
          "params": {
              "account": "wixnnnd-ui60793.snowflakecomputing.com",
              "database": "ACME_DB",
              "warehouse": "ACME_WH",
              "username": "nikola15",
              "schema": "PUBLIC",
              "password": "xxxx",
              "role": "ACCOUNTADMIN"
          }
      },
      "connectionSpec": {
          "id": "51ae16c2-bdad-42fd-9fce-8d5dfddaf140",
          "version": "1.0"
      }
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `auth.params.account` | Der Name Ihres [!DNL Snowflake]-Streaming-Kontos. |
| `auth.params.database` | Der Name Ihrer [!DNL Snowflake]-Datenbank, aus der Daten abgerufen werden. |
| `auth.params.warehouse` | Der Name Ihres [!DNL Snowflake] Warehouse. Das [!DNL Snowflake]-Warehouse verwaltet den Abfrageausführungsprozess für die Anwendung. Jedes Warehouse ist unabhängig voneinander und muss einzeln aufgerufen werden, wenn Daten an Platform übermittelt werden. |
| `auth.params.username` | Der Benutzername für Ihr [!DNL Snowflake]-Streaming-Konto. |
| `auth.params.schema` | (Optional) Das Datenbankschema, das mit Ihrem [!DNL Snowflake]-Streaming-Konto verknüpft ist. |
| `auth.params.password` | Das Kennwort für Ihr [!DNL Snowflake]-Streaming-Konto. |
| `auth.params.role` | (Optional) Die Rolle des Benutzers für diese [!DNL Snowflake]-Verbindung. Wenn dieser Wert nicht angegeben wird, wird standardmäßig `public` verwendet. |
| `connectionSpec.id` | Die [!DNL Snowflake] Verbindungsspezifikations-ID: `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

**Antwort**

Eine erfolgreiche Antwort gibt die neu erstellte Basisverbindung und das zugehörige eTag zurück.

```json
{
    "id": "1b614dc0-b76e-41e1-b25f-09f4a9d3f111",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## Datentabellen durchsuchen {#explore-your-data-tables}

Verwenden Sie als Nächstes die Basis-Verbindungs-ID, um die Datentabellen Ihrer Quelle zu untersuchen und durch sie zu navigieren, indem Sie eine GET-Anfrage an den `/connections/{BASE_CONNECTION_ID}/explore?objectType=root` -Endpunkt senden und dabei Ihre Basis-Verbindungs-ID als Parameter angeben.

**API-Format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parameter | Beschreibung |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Die Kennung der Basisverbindung Ihrer [!DNL Snowflake]-Streaming-Quelle. |


**Anfrage**

Die folgende Anfrage ruft die Struktur und den Inhalt Ihres [!DNL Snowflake]-Streaming-Kontos ab.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/1b614dc0-b76e-41e1-b25f-09f4a9d3f111/explore?objectType=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Struktur und den Inhalt der Quelldaten auf der Stammebene zurück.

```json
{
    "items": [
        {
            "type": "table",
            "name": "ACME"
        }
    ]
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `items.type` | Der Typ der Tabelle. |
| `items.names` | Der Name der Tabelle. |

## Erstellen einer Quellverbindung {#create-a-source-connection}

Eine Quellverbindung erstellt und verwaltet die Verbindung zur externen Quelle, von der aus Daten erfasst werden.

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
      "name": "Snowflake Streaming Source Connection",
      "description": "A source connection for Snowflake Streaming data",
      "baseConnectionId": "1b614dc0-b76e-41e1-b25f-09f4a9d3f111",
      "connectionSpec": {
          "id": "51ae16c2-bdad-42fd-9fce-8d5dfddaf140",
          "version": "1.0"
      },
      "params": {
          "tableName": "ACME",
          "timestampColumn": "dOb",
          "backfill": "true",
          "timezoneValue": "PST"
      }
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `baseConnectionId` | Die authentifizierte Basis-Verbindungs-ID für Ihre [!DNL Snowflake]-Streaming-Quelle. Diese ID wurde in einem früheren Schritt generiert. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID für die [!DNL Snowflake]-Streaming-Quelle. |
| `params.tableName` | Der Name der Tabelle in Ihrer [!DNL Snowflake]-Datenbank, die Sie in Platform laden möchten. |
| `params.timestampColumn` | Der Name der Zeitstempelspalte, die zum Abrufen inkrementeller Werte verwendet wird. |
| `params.backfill` | Eine boolesche Kennzeichnung, die bestimmt, ob Daten vom Anfang (0 Epochenzeit) oder von dem Zeitpunkt an abgerufen werden, zu dem die Quelle initiiert wird. Weitere Informationen zu diesem Wert finden Sie in der [[!DNL Snowflake] Streaming-Quellübersicht](../../../../connectors/databases/snowflake-streaming.md). |
| `params.timezoneValue` | Der Zeitzonenwert gibt an, welche Zeitzone bei der Abfrage der [!DNL Snowflake] -Datenbank zur aktuellen Zeit abgerufen werden soll. Dieser Parameter sollte angegeben werden, wenn die Spalte mit dem Zeitstempel in der Konfiguration auf `TIMESTAMP_NTZ` gesetzt ist. Wenn nichts angegeben ist, wird standardmäßig UTC verwendet.`timezoneValue` |

**Antwort**

Bei einer erfolgreichen Antwort werden Ihre Kennung der Quellverbindung und das zugehörige eTag zurückgegeben. Die Kennung der Quellverbindung wird in einem späteren Schritt zum Erstellen eines Datenflusses verwendet.

```json
{
    "id": "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## Erstellen eines Datenflusses

Um einen Datenfluss zum Streamen von Daten aus dem Tour [!DNL Snowflake] -Konto an Platform zu erstellen, müssen Sie eine POST-Anfrage an den `/flows` -Endpunkt senden und dabei die folgenden Werte angeben:

>[!TIP]
>
>Folgen Sie den unten stehenden Links, um schrittweise Anleitungen zum Abrufen der folgenden IDs zu erhalten.

* [Quellverbindungs-ID](#create-a-source-connection)
* [Zielverbindungs-ID](../../collect/database-nosql.md#create-a-target-connection)
* [Flussspezifikations-ID](../../collect/database-nosql.md#retrieve-dataflow-specifications)
* [Zuordnungs-ID](../../collect/database-nosql.md#create-a-mapping)

**API-Format**

```http
POST /flows
```

**Anfrage**

Die folgende Anfrage erstellt einen Streaming-Datenfluss für Ihr [!DNL Snowflake] -Konto.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake Streaming Dataflow",
      "description": "A dataflow for Snowflake streaming data",
      "sourceConnectionIds": [
        "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6"
      ],
      "targetConnectionIds": [
        "78f41c31-3652-4a5e-b264-74331226dcf3"
      ],
      "flowSpec": {
        "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
        "version": "1.0"
      },
      "transformations": [
        {
          "name": "Mapping",
          "params": {
            "mappingId": "44d42ed27c46499a80eb0c0705c38cbd",
            "mappingVersion": 0
          }
        }
      ]
    }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `sourceConnectionIds` | Die Kennung der Quellverbindung für Ihre [!DNL Snowflake]-Streaming-Quelle. |
| `targetConnectionIds` | Die Zielverbindungs-ID für Ihre [!DNL Snowflake]-Streaming-Quelle. |
| `flowSpec.id` | Die Flussspezifikations-ID zum Erstellen eines Datenflusses für eine [!DNL Snowflake]-Streaming-Quelle. Mit dieser Flussspezifikations-ID können Sie einen Streaming-Datenfluss mit Zuordnungstransformationen erstellen. Diese ID ist fest und lautet: `c1a19761-d2c7-4702-b9fa-fe91f0613e81`. |
| `transformations.params.mappingId` | Die Zuordnungs-ID für Ihren Datenfluss. |

**Antwort**

Bei einer erfolgreichen Antwort werden Ihre Fluss-ID und das zugehörige eTag zurückgegeben.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"770029f8-0000-0200-0000-6019e7d40000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie einen Streaming-Datenfluss für Ihre [!DNL Snowflake] -Daten mithilfe der [!DNL Flow Service] -API erstellt. Weitere Informationen zu Adobe Experience Platform-Quellen finden Sie in der folgenden Dokumentation:

* [Quellen – Übersicht](../../../../home.md)
* [Überwachen Ihres Datenflusses mithilfe von APIs](../../monitor.md)
