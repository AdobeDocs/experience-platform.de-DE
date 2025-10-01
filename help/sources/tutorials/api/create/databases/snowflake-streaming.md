---
title: Verbinden Ihres Snowflake-Streaming-Kontos mit Adobe Experience Platform
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit Snowflake Streaming verbinden.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 3fc225a4-746c-4a91-aa77-bbeb091ec364
source-git-commit: a4a464f1f3b61311754a39f2a6e6a4ef21af3ab0
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 20%

---

# Streamen von [!DNL Snowflake] an Experience Platform mithilfe der [!DNL Flow Service]-API

>[!IMPORTANT]
>
>
> Die [!DNL Snowflake] Streaming-Quelle ist in der API für Benutzende verfügbar, die Real-Time Customer Data Platform Ultimate erworben haben.

In diesem Tutorial erfahren Sie, wie Sie mithilfe der -API Daten aus Ihrem [!DNL Snowflake]-Konto mit Adobe Experience Platform [[!DNL Flow Service]  und ](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Experience Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Experience Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Verwenden von Experience Platform-APIs

Informationen zum erfolgreichen Aufrufen von Experience Platform-APIs finden Sie im Handbuch unter [ mit Experience Platform-APIs](../../../../../landing/api-guide.md).

### Sammeln erforderlicher Anmeldedaten

Informationen zur Authentifizierung [[!DNL Snowflake]  Sie in ](../../../../connectors/databases/snowflake-streaming.md#prerequisites)Übersicht“.

## Erstellen einer Basisverbindung {#create-a-base-connection}

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Experience Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen ID der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den `/connections`-Endpunkt und geben Sie dabei Ihre [!DNL Snowflake] Authentifizierungsdaten als Teil des Anfragetexts an.

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Snowflake]:

>[!TIP]
>
>Der `auth.specName` muss genau wie im folgenden Beispiel eingegeben werden, einschließlich der Leerzeichen.

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
| `auth.params.account` | Der Name Ihres [!DNL Snowflake] Streaming-Kontos. |
| `auth.params.database` | Der Name der [!DNL Snowflake], aus der Daten abgerufen werden. |
| `auth.params.warehouse` | Der Name Ihres [!DNL Snowflake]. Das [!DNL Snowflake] Warehouse verwaltet den Abfrageausführungsprozess für das Programm. Jedes Warehouse ist unabhängig voneinander und muss beim Übermitteln von Daten an Experience Platform einzeln aufgerufen werden. |
| `auth.params.username` | Der Benutzername für Ihr [!DNL Snowflake] Streaming-Konto. |
| `auth.params.schema` | (Optional) Das mit Ihrem [!DNL Snowflake]-Streaming-Konto verknüpfte Datenbankschema. |
| `auth.params.password` | Das Passwort für Ihr [!DNL Snowflake] Streaming-Konto. |
| `auth.params.role` | (Optional) Die Rolle des Benutzers für diese [!DNL Snowflake]. Wenn kein Wert angegeben wird, ist dieser Standardwert `public`. |
| `connectionSpec.id` | Die Spezifikations-ID der [!DNL Snowflake]-Verbindung: `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

**Antwort**

Eine erfolgreiche Antwort gibt die neu erstellte Basisverbindung und das entsprechende eTag zurück.

```json
{
    "id": "1b614dc0-b76e-41e1-b25f-09f4a9d3f111",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## Erkunden von Datentabellen {#explore-your-data-tables}

Verwenden Sie als Nächstes die Basisverbindungs-ID, um die Datentabellen Ihrer Quelle zu durchsuchen und durch diese zu navigieren, indem Sie eine GET-Anfrage an den `/connections/{BASE_CONNECTION_ID}/explore?objectType=root`-Endpunkt stellen und dabei Ihre Basisverbindungs-ID als Parameter angeben.

**API-Format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parameter | Beschreibung |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Die Basisverbindungs-ID Ihrer [!DNL Snowflake]-Streaming-Quelle. |


**Anfrage**

Mit der folgenden Anfrage werden die Struktur und der Inhalt Ihres [!DNL Snowflake] Streaming-Kontos abgerufen.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/1b614dc0-b76e-41e1-b25f-09f4a9d3f111/explore?objectType=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Struktur und den Inhalt der Daten Ihrer Quelle auf der Stammebene zurück.

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

Eine Quellverbindung erstellt und verwaltet die Verbindung zur externen Quelle, aus der Daten aufgenommen werden.

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
| `baseConnectionId` | Die ID der authentifizierten Basisverbindung für Ihre [!DNL Snowflake] Streaming-Quelle. Diese ID wurde in einem früheren Schritt generiert. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID für die [!DNL Snowflake] Streaming-Quelle. |
| `params.tableName` | Der Name der Tabelle in Ihrer [!DNL Snowflake], die Sie an Experience Platform übermitteln möchten. |
| `params.timestampColumn` | Der Name der Zeitstempelspalte, die zum Abrufen inkrementeller Werte verwendet wird. |
| `params.backfill` | Ein boolesches Flag, das bestimmt, ob die Daten ab dem Anfang (Epochenzeit 0) oder ab dem Zeitpunkt abgerufen werden, zu dem die Quelle initiiert wird. Weitere Informationen zu diesem Wert finden Sie unter [[!DNL Snowflake] Übersicht über Streaming-Quellen](../../../../connectors/databases/snowflake-streaming.md). |
| `params.timezoneValue` | Der Wert für die Zeitzone gibt an, welche aktuelle Zeit für die Abfrage der [!DNL Snowflake]-Datenbank abgerufen werden soll. Dieser Parameter sollte bereitgestellt werden, wenn die Zeitstempelspalte in der Konfiguration auf `TIMESTAMP_NTZ` festgelegt ist. Wenn nicht angegeben, ist `timezoneValue` standardmäßig UTC. |

**Antwort**

Bei einer erfolgreichen Antwort werden Ihre Quellverbindungs-ID und das entsprechende eTag zurückgegeben. Die Quellverbindungs-ID wird in einem späteren Schritt zum Erstellen eines Datenflusses verwendet.

```json
{
    "id": "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## Erstellen eines Datenflusses

>[!NOTE]
>
>Nachdem Sie einen Streaming-Datenfluss erstellt oder aktualisiert haben, ist eine kurze 5-minütige Pause bei der Datenaufnahme erforderlich, um potenzielle Instanzen von Datenverlust oder Datenverlust zu verhindern.

Um einen Datenfluss zum Streamen von Daten aus Ihrem [!DNL Snowflake]-Konto an Experience Platform zu erstellen, müssen Sie eine POST-Anfrage an den `/flows`-Endpunkt senden und dabei die folgenden Werte angeben:

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

Mit der folgenden Anfrage wird ein Streaming-Datenfluss für Ihr [!DNL Snowflake]-Konto erstellt.

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
| `sourceConnectionIds` | Die Quellverbindungs-ID für Ihre [!DNL Snowflake] Streaming-Quelle. |
| `targetConnectionIds` | Die Zielverbindungs-ID für Ihre [!DNL Snowflake] Streaming-Quelle. |
| `flowSpec.id` | Die Flussspezifikations-ID zum Erstellen eines Datenflusses für eine [!DNL Snowflake] Streaming-Quelle. Mit dieser Flussspezifikations-ID können Sie einen Streaming-Datenfluss mit Zuordnungstransformationen erstellen. Diese ID ist fest und lautet: `c1a19761-d2c7-4702-b9fa-fe91f0613e81`. |
| `transformations.params.mappingId` | Die Zuordnungs-ID für Ihren Datenfluss. |

**Antwort**

Bei einer erfolgreichen Antwort werden Ihre Fluss-ID und das entsprechende eTag zurückgegeben.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"770029f8-0000-0200-0000-6019e7d40000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie einen Streaming-Datenfluss für Ihre [!DNL Snowflake] mithilfe der [!DNL Flow Service]-API erstellt. In der folgenden Dokumentation finden Sie weitere Informationen zu Adobe Experience Platform-Quellen:

* [Quellen – Übersicht](../../../../home.md)
* [Überwachen Ihres Datenflusses mithilfe von APIs](../../monitor.md)
