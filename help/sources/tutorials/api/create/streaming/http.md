---
keywords: Experience Platform;Startseite;beliebte Themen;Streaming-Verbindung;Streaming-Verbindung erstellen;API-Handbuch;Tutorial;Erstellen einer Streaming-Verbindung;Streaming-Aufnahme;Aufnahme;
title: Erstellen einer HTTP-API-Streaming-Verbindung mithilfe der Flow Service-API
description: In diesem Tutorial erfahren Sie, wie Sie eine Streaming-Verbindung mithilfe der HTTP-API-Quelle für Roh- und XDM-Daten mithilfe der Flow Service-API erstellen
exl-id: 9f7fbda9-4cd3-4db5-92ff-6598702adc34
source-git-commit: bad1e0a9d86dcce68f1a591060989560435070c5
workflow-type: tm+mt
source-wordcount: '1684'
ht-degree: 28%

---


# Erstellen einer HTTP-API-Streaming-Verbindung mithilfe der [!DNL Flow Service]-API

Flow Service wird verwendet, um Kundendaten aus verschiedenen Quellen innerhalb von Adobe Experience Platform zu sammeln und zu zentralisieren. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

In diesem Tutorial wird die [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) verwendet, um Sie durch die Schritte zum Erstellen einer Streaming-Verbindung mithilfe der [!DNL Flow Service]-API zu führen.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Erlebnisdaten organisiert.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Kundenprofil in Echtzeit, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Darüber hinaus benötigen Sie zum Erstellen einer Streaming-Verbindung ein Ziel-XDM-Schema und einen Datensatz. Um zu erfahren, wie Sie diese erstellen, lesen Sie das Tutorial [Streaming von Datensatzdaten](../../../../../ingestion/tutorials/streaming-record-data.md) oder das Tutorial [Streaming von Zeitreihendaten](../../../../../ingestion/tutorials/streaming-time-series-data.md).

### Verwenden von Experience Platform-APIs

Informationen zum erfolgreichen Aufrufen von Experience Platform-APIs finden Sie im Handbuch unter [ mit Experience Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung

Eine Basisverbindung gibt die Quelle an und enthält die Informationen, die erforderlich sind, um den Fluss mit Streaming-Aufnahme-APIs kompatibel zu machen. Beim Erstellen einer Basisverbindung haben Sie die Möglichkeit, eine nicht authentifizierte und eine authentifizierte Verbindung zu erstellen.

### Nicht authentifizierte Verbindung

Nicht authentifizierte Verbindungen sind die Standard-Streaming-Verbindung, die Sie erstellen können, wenn Sie Daten in Experience Platform streamen möchten.

Um eine nicht authentifizierte Basisverbindung zu erstellen, stellen Sie eine POST-Anfrage an den `/connections`-Endpunkt und geben Sie dabei einen Namen für Ihre Verbindung, den Datentyp und die HTTP-API-Verbindungsspezifikations-ID an. Diese ID ist `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

**API-Format**

```http
POST /flowservice/connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für die HTTP-API.

>[!BEGINTABS]

>[!TAB XDM]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "name": "ACME Streaming Connection XDM Data",
    "description": "ACME streaming connection for customer data",
    "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
    },
    "auth": {
      "specName": "Streaming Connection",
      "params": {
        "dataType": "xdm"
      }
    }
  }'
```

>[!TAB Rohdaten]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "name": "ACME Streaming Connection Raw Data",
    "description": "ACME streaming connection for customer data",
    "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
    },
    "auth": {
      "specName": "Streaming Connection",
      "params": {
        "dataType": "raw"
      }
    }
  }'
```

>[!ENDTABS]

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name Ihrer Basisverbindung. Stellen Sie sicher, dass der Name beschreibend ist, da Sie damit Informationen zu Ihrer Basisverbindung nachschlagen können. |
| `description` | (Optional) Eine Eigenschaft, die Sie einbeziehen können, um weitere Informationen zu Ihrer Basisverbindung bereitzustellen. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID, die der HTTP-API entspricht. Diese ID ist `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`. |
| `auth.params.dataType` | Der Datentyp für die Streaming-Verbindung. Folgende Werte werden unterstützt: `xdm` und `raw`. |
| `auth.params.name` | Der Name der Streaming-Verbindung, die Sie erstellen möchten. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 mit Details zur neu erstellten Verbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`).

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `id` | Die `id` der neu erstellten Basisverbindung. |
| `etag` | Eine Kennung, die der Verbindung zugewiesen ist und die Version der Basisverbindung angibt. |

### Authentifizierte Verbindung

Authentifizierte Verbindungen sollten verwendet werden, wenn Sie zwischen Datensätzen aus vertrauenswürdigen und nicht vertrauenswürdigen Quellen unterscheiden müssen. Benutzende, die Informationen mit personenbezogenen Daten (PII) senden möchten, sollten beim Streaming von Informationen an Experience Platform eine authentifizierte Verbindung herstellen.

Um eine authentifizierte Basisverbindung zu erstellen, müssen Sie den `authenticationRequired`-Parameter in Ihre Anfrage einbeziehen und seinen Wert als `true` angeben. In diesem Schritt können Sie auch eine Quell-ID für Ihre authentifizierte Basisverbindung angeben. Dieser Parameter ist optional und verwendet denselben Wert wie das `name`-Attribut, wenn er nicht angegeben wird.


**API-Format**

```http
POST /flowservice/connections
```

**Anfrage**

Die folgende Anfrage erstellt eine authentifizierte Basisverbindung für die HTTP-API.

>[!BEGINTABS]

>[!TAB XDM]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "ACME Streaming Connection XDM Data Authenticated",
     "description": "ACME streaming connection for customer data",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Authenticated XDM streaming connection",
             "dataType": "xdm",
             "name": "Authenticated XDM streaming connection",
             "authenticationRequired": true
         }
     }
 }
```

>[!TAB Rohdaten]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "ACME Streaming Connection Raw Data Authenticated",
     "description": "ACME streaming connection for customer data",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Authenticated raw streaming connection",
             "dataType": "raw",
             "name": "Authenticated raw streaming connection",
             "authenticationRequired": true
         }
     }
 }
```

>[!ENDTABS]

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.sourceId` | Eine zusätzliche Kennung, die beim Erstellen einer authentifizierten Basisverbindung verwendet werden kann. Dieser Parameter ist optional und verwendet denselben Wert wie das `name`-Attribut, wenn er nicht angegeben wird. |
| `auth.params.authenticationRequired` | Dieser Parameter gibt an, ob die Streaming-Verbindung eine Authentifizierung erfordert oder nicht. Wenn `authenticationRequired` auf `true` gesetzt ist, muss eine Authentifizierung für die Streaming-Verbindung bereitgestellt werden. Wenn `authenticationRequired` auf `false` gesetzt ist, ist keine Authentifizierung erforderlich. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 mit Details zur neu erstellten Verbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`).

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

## Streaming-Endpunkt-URL abrufen

Nachdem die Basisverbindung erstellt wurde, können Sie jetzt Ihre Streaming-Endpunkt-URL abrufen.

**API-Format**

```http
GET /flowservice/connections/{BASE_CONNECTION_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | Der `id`-Wert der zuvor von Ihnen erstellten Verbindung. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit detaillierten Informationen zur angeforderten Verbindung zurück. Die Streaming-Endpunkt-URL wird automatisch mit der Verbindung erstellt und kann mit dem `inletUrl` abgerufen werden.

```json
{
  "items": [
    {
      "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
      "createdAt": 1669238699119,
      "updatedAt": 1669238699119,
      "createdBy": "acme@AdobeID",
      "updatedBy": "acme@AdobeID",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_ID}",
      "name": "ACME Streaming Connection XDM Data",
      "description": "ACME streaming connection for customer data",
      "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "Streaming Connection",
        "params": {
          "sourceId": "ACME Streaming Connection XDM Data",
          "inletUrl": "https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec",
          "authenticationRequired": false,
          "inletId": "667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec",
          "dataType": "xdm",
          "name": "ACME Streaming Connection XDM Data"
        }
      },
      "version": "\"f50185ed-0000-0200-0000-637e8fad0000\"",
      "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
    }
  ]
}
```

## Erstellen einer Quellverbindung {#source}

Um eine Quellverbindung zu erstellen, stellen Sie eine POST-Anfrage an den `/sourceConnections`-Endpunkt, während Sie Ihre Basisverbindungs-ID angeben.

**API-Format**

```http
POST /flowservice/sourceConnections
```

**Anfrage**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Streaming Source Connection for Customer Data",
      "description": "A streaming source connection for ACME XDM Customer Data",
      "baseConnectionId": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
      "connectionSpec": {
          "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
          "version": "1.0"
      }
    }'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 mit Details zur neu erstellten Quellverbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`).

```json
{
  "id": "34ece231-294d-416c-ad2a-5a5dfb2bc69f",
  "etag": "\"d505125b-0000-0200-0000-637eb7790000\""
}
```

## Erstellen eines XDM-Zielschemas {#target-schema}

Damit die Quelldaten in Experience Platform verwendet werden können, muss ein Zielschema erstellt werden, das die Quelldaten entsprechend Ihren Anforderungen strukturiert. Das Zielschema wird dann verwendet, um einen Experience Platform-Datensatz zu erstellen, in dem die Quelldaten enthalten sind.

Ein Ziel-XDM-Schema kann erstellt werden, indem eine POST-Anfrage an die [Schema-Registrierungs-API](https://www.adobe.io/experience-platform-apis/references/schema-registry/) durchgeführt wird.

Ausführliche Schritte zum Erstellen eines XDM-Zielschemas finden Sie im Tutorial zum [Erstellen eines Schemas mithilfe der API](../../../../../xdm/api/schemas.md).

### Erstellen eines Zieldatensatzes {#target-dataset}

Ein Zieldatensatz kann erstellt werden, indem eine POST-Anfrage an die [Catalog Service API](https://developer.adobe.com/experience-platform-apis/references/catalog/) durchgeführt wird, wodurch die ID des Zielschemas in der Payload angegeben wird.

Ausführliche Anweisungen zum Erstellen eines Zieldatensatzes finden Sie im Tutorial zu [Erstellen eines Datensatzes mithilfe der API](../../../../../catalog/api/create-dataset.md).

## Erstellen einer Zielverbindung {#target}

Eine Zielverbindung stellt die Verbindung zum Ziel dar, in das die aufgenommenen Daten übernommen werden. Um eine Zielverbindung zu erstellen, stellen Sie eine POST-Anfrage an `/targetConnections` und geben Sie dabei IDs für Ihren Zieldatensatz und das XDM-Zielschema an. In diesem Schritt müssen Sie auch die Data-Lake-Verbindungsspezifikations-ID angeben. Diese ID ist `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

**API-Format**

```http
POST /flowservice/targetConnections
```

**Anfrage**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Streaming Target Connection",
      "description": "ACME Streaming Target Connection",
      "data": {
          "schema": {
              "id": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
              "version": "application/vnd.adobe.xed-full+json;version=1.0"
          }
      },
      "params": {
          "dataSetId": "637eb7fadc8a211b6312b65b"
      },
          "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
  }'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 mit Details zur neu erstellten Zielverbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`).

```json
{
  "id": "07f2f6ff-1da5-4704-916a-c615b873cba9",
  "etag": "\"340680f7-0000-0200-0000-637eb8730000\""
}
```

## Erstellen einer Zuordnung {#mapping}

Damit die Quelldaten in einen Zieldatensatz aufgenommen werden können, müssen sie zunächst dem Zielschema zugeordnet werden, zu dem der Zieldatensatz gehört.

Um einen Zuordnungssatz zu erstellen, senden Sie eine POST-Anfrage an den `mappingSets`-Endpunkt der [[!DNL Data Prep] API](https://developer.adobe.com/experience-platform-apis/references/data-prep/), wobei Sie das Ziel-XDM-Schema `$id` und die Details der Zuordnungssätze, die Sie erstellen möchten, angeben.

**API-Format**

```http
POST /mappingSets
```

**Anfrage**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "version": 0,
      "xdmSchema": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
      "xdmVersion": "1.0",
      "mappings": [
          {
              "destinationXdmPath": "person.name.firstName",
              "sourceAttribute": "firstName",
              "identity": false,
              "version": 0
          },
          {
              "destinationXdmPath": "person.name.lastName",
              "sourceAttribute": "lastName",
              "identity": false,
              "version": 0
          }
      ]
  }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `xdmSchema` | `$id` des XDM-Zielschemas. |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Zuordnung zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist in einem späteren Schritt erforderlich, um einen Datenfluss zu erstellen.

```json
{
  "id": "79a623960d3f4969835c9e00dc90c8df",
  "version": 0,
  "createdDate": 1669249214031,
  "modifiedDate": 1669249214031,
  "createdBy": "acme@AdobeID",
  "modifiedBy": "acme@AdobeID"
}
```

## Erstellen eines Datenflusses

>[!NOTE]
>
>Nachdem Sie einen Streaming-Datenfluss erstellt oder aktualisiert haben, ist eine kurze 5-minütige Pause bei der Datenaufnahme erforderlich, um potenzielle Instanzen von Datenverlust oder Datenverlust zu verhindern.

Nachdem Sie Ihre Quell- und Zielverbindungen erstellt haben, können Sie jetzt einen Datenfluss erstellen. Der Datenfluss ist für die Planung und Erfassung von Daten aus einer Quelle verantwortlich. Sie können einen Datenfluss erstellen, indem Sie eine POST-Anfrage an den `/flows`-Endpunkt senden.

**API-Format**

```http
POST /flows
```

**Anfrage**

>[!BEGINTABS]

>[!TAB XDM]

Die folgende Anfrage erstellt einen Streaming-Datenfluss für XDM-Daten.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Streaming Dataflow",
      "description": "ACME streaming dataflow for customer data",
      "flowSpec": {
        "id": "d8a6f005-7eaf-4153-983e-e8574508b877",
        "version": "1.0"
      },
      "sourceConnectionIds": [
        "34ece231-294d-416c-ad2a-5a5dfb2bc69f"
      ],
      "targetConnectionIds": [
        "07f2f6ff-1da5-4704-916a-c615b873cba9"
      ]
    }'
```

>[!TAB RAW]

Die folgenden Anfragen erstellen einen Streaming-Datenfluss für Rohdaten.

Beim Erstellen eines Datenflusses mit Transformationen kann der `name` Parameter nicht geändert werden. Dieser Wert muss immer auf `Mapping` festgelegt werden.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "<name>",
      "description": "<description>",
      "flowSpec": {
        "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
        "version": "1.0"
      },
      "sourceConnectionIds": [
        "34ece231-294d-416c-ad2a-5a5dfb2bc69f"
      ],
      "targetConnectionIds": [
        "07f2f6ff-1da5-4704-916a-c615b873cba9"
      ],
      "transformations": [
        {
          "name": "Mapping",
          "params": {
            "mappingId": "79a623960d3f4969835c9e00dc90c8df",
            "mappingVersion": 0
          }
        }
      ]
    }'
```

>[!ENDTABS]

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name Ihres Datenflusses. Stellen Sie sicher, dass der Name Ihres Datenflusses beschreibend ist, da Sie damit Informationen zu Ihrem Datenfluss suchen können. |
| `description` | (Optional) Eine Eigenschaft, die Sie einfügen können, um weitere Informationen zu Ihrem Datenfluss bereitzustellen. |
| `flowSpec.id` | Die Flussspezifikations-ID für [!DNL HTTP API]. Um einen Datenfluss mit Transformationen zu erstellen, müssen Sie `c1a19761-d2c7-4702-b9fa-fe91f0613e81` verwenden. Um einen Datenfluss ohne Umwandlungen zu erstellen, verwenden Sie `d8a6f005-7eaf-4153-983e-e8574508b877`. |
| `sourceConnectionIds` | Die [Quellverbindungs-ID](#source), die in einem früheren Schritt abgerufen wurde. |
| `targetConnectionIds` | Die [Zielverbindungs-ID](#target), die in einem früheren Schritt abgerufen wurde. |
| `transformations.params.mappingId` | Die [Zuordnungs-ID](#mapping), die in einem früheren Schritt abgerufen wurde. |

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 201 mit Details zu Ihrem neu erstellten Datenfluss zurückgegeben, einschließlich der eindeutigen Kennung (`id`).

```json
{
  "id": "f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2",
  "etag": "\"dc0459ae-0000-0200-0000-637ebaec0000\""
}
```

## In Experience Platform aufzunehmende Daten posten {#ingest-data}

>[!NOTE]
>
>Sie müssen zwischen der Erstellung eines Datenflusses und der Aufnahme von Streaming-Daten eine Verzögerung von mindestens ca. 5 Minuten hinzufügen. Dadurch kann der Datenfluss vollständig aktiviert werden, bevor Daten aufgenommen werden.

Nachdem Sie Ihren Fluss erstellt haben, können Sie Ihre JSON-Nachricht an den Streaming-Endpunkt senden, den Sie zuvor erstellt haben.

**API-Format**

```http
POST /collection/{INLET_URL}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{INLET_URL}` | Ihre Streaming-Endpunkt-URL. Sie können diese URL abrufen, indem Sie eine GET-Anfrage an den `/connections`-Endpunkt stellen und dabei Ihre Basisverbindungs-ID angeben. |
| `{FLOW_ID}` | Die ID Ihres HTTP-API-Streaming-Datenflusses. Diese ID ist für XDM- und Rohdaten erforderlich. |

**Anfrage**

>[!BEGINTABS]

>[!TAB Senden von XDM-Daten]

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec \
  -H 'Content-Type: application/json' \
  -d '{
        "header": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
          },
          "flowId": "f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2",
          "datasetId": "604a18a3bae67d18db6d258c"
        },
        "body": {
          "xdmMeta": {
            "schemaRef": {
              "id": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
              "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
            }
          },
          "xdmEntity": {
            "_id": "http-source-connector-acme-01",
            "person": {
              "name": {
                "firstName": "suman",
                "lastName": "nolan"
              }
            },
            "workEmail": {
              "primary": true,
              "address": "suman@acme.com",
              "type": "work",
              "status": "active"
            }
          }
        }
      }'
```

>[!TAB Senden von Rohdaten mit Fluss-ID als HTTP-Kopfzeile]

Beim Senden von Rohdaten können Sie Ihre Fluss-ID entweder als Abfrageparameter oder als Teil Ihrer HTTP-Kopfzeile angeben. Im folgenden Beispiel wird die Fluss-ID als HTTP-Kopfzeile angegeben.

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec \
  -H 'Content-Type: application/json' 
  -H 'x-adobe-flow-id=f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2' \
  -d '{
      "name": "Johnson Smith",
      "location": {
          "city": "Seattle",
          "country": "United State of America",
          "address": "3692 Main Street"
      },
      "gender": "Male",
      "birthday": {
          "year": 1984,
          "month": 6,
          "day": 9
      }
  }'
```

>[!TAB Senden von Rohdaten mit Fluss-ID als Abfrageparameter]

Beim Senden von Rohdaten können Sie Ihre Fluss-ID entweder als Abfrageparameter oder als HTTP-Kopfzeile angeben. Im folgenden Beispiel wird die Fluss-ID als Abfrageparameter angegeben.

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec?x-adobe-flow-id=f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2 \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Johnson Smith",
      "location": {
          "city": "Seattle",
          "country": "United State of America",
          "address": "3692 Main Street"
      },
      "gender": "Male",
      "birthday": {
          "year": 1984,
          "month": 6,
          "day": 9
      }
  }'
```

>[!ENDTABS]

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status-Code 200 mit Details zu den neu aufgenommenen Informationen zurück.

```json
{
    "inletId": "{BASE_CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{BASE_CONNECTION_ID}` | Die Kennung der zuvor erstellten Streaming-Verbindung. |
| `xactionId` | Eine eindeutige Kennung, die für den soeben gesendeten Datensatz Server-seitig generiert wurde. Diese Kennung hilft Adobe bei der Verfolgung des Lebenszyklus dieses Datensatzes in verschiedenen Systemen sowie beim Debugging. |
| `receivedTimeMs` | Ein Zeitstempel (Epoche in Millisekunden), der anzeigt, wann die Anfrage empfangen wurde. |


## Nächste Schritte

In diesem Tutorial haben Sie eine Streaming-HTTP-Verbindung erstellt, mit der Sie den Streaming-Endpunkt verwenden können, um Daten in Experience Platform aufzunehmen. Anweisungen zum Erstellen einer Streaming-Verbindung in der Benutzeroberfläche finden Sie im Tutorial [Erstellen einer Streaming-Verbindung](../../../ui/create/streaming/http.md).

Um zu erfahren, wie Sie Daten an Experience Platform streamen, lesen Sie entweder das Tutorial [Streaming von Zeitreihendaten](../../../../../ingestion/tutorials/streaming-time-series-data.md) oder das Tutorial [Streaming von Datensatzdaten](../../../../../ingestion/tutorials/streaming-record-data.md).

## Anhang

Dieser Abschnitt enthält zusätzliche Informationen zum Erstellen von Streaming-Verbindungen mithilfe der API.

### Senden von Nachrichten an eine authentifizierte Streaming-Verbindung

Wenn für eine Streaming-Verbindung die Authentifizierung aktiviert ist, muss der Client die `Authorization`-Kopfzeile zu seiner Anfrage hinzufügen.

Wenn die `Authorization`-Kopfzeile nicht vorhanden ist oder ein ungültiges/abgelaufenes Zugriffstoken gesendet wird, wird eine HTTP 401 Unerlaubt-Antwort zurückgegeben, mit einer ähnlichen Antwort wie folgt:

**Antwort**

```json
{
    "type": "https://ns.adobe.com/adobecloud/problem/data-collection-service-authorization",
    "status": "401",
    "title": "Authorization",
    "report": {
        "message": "[id] Ims service token is empty"
    }
}
```

