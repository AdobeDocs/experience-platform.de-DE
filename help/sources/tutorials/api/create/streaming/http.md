---
keywords: Experience Platform; Startseite; beliebte Themen; Streaming-Verbindung; Streaming-Verbindung erstellen; API-Handbuch; Tutorial; Erstellen einer Streaming-Verbindung; Streaming-Erfassung; Erfassung;
title: Erstellen einer HTTP-API-Streaming-Verbindung mithilfe der Flow Service-API
description: In diesem Tutorial erfahren Sie, wie Sie mithilfe der Flow Service-API eine Streaming-Verbindung mithilfe der HTTP-API-Quelle für Roh- und XDM-Daten erstellen
exl-id: 9f7fbda9-4cd3-4db5-92ff-6598702adc34
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1472'
ht-degree: 40%

---


# Erstellen Sie eine HTTP-API-Streaming-Verbindung mithilfe der [!DNL Flow Service] API

Mit Flow Service können Kundendaten aus verschiedenen Quellen in Adobe Experience Platform erfasst und zentralisiert werden. Der Dienst bietet eine Benutzeroberfläche und eine RESTful-API, über die alle unterstützten Quellen verbunden werden können.

In diesem Tutorial wird die [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) um Sie durch die Schritte zum Erstellen einer Streaming-Verbindung mit dem [!DNL Flow Service] API.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md): Der standardisierte Rahmen, durch den [!DNL Platform] organisiert Erlebnisdaten.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Verbraucherprofil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.

Zum Erstellen einer Streaming-Verbindung müssen Sie außerdem über ein Ziel-XDM-Schema und einen Datensatz verfügen. Um zu erfahren, wie Sie diese erstellen, lesen Sie bitte das Tutorial zu [Streaming von Datensatzdaten](../../../../../ingestion/tutorials/streaming-record-data.md) oder das Tutorial zu [Streaming von Zeitreihendaten](../../../../../ingestion/tutorials/streaming-time-series-data.md).

### Verwenden von Platform-APIs

Informationen zum Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung

Eine Basisverbindung gibt die Quelle an und enthält die Informationen, die erforderlich sind, um den Fluss mit Streaming-Aufnahme-APIs kompatibel zu machen. Beim Erstellen einer Basisverbindung haben Sie die Möglichkeit, eine nicht authentifizierte und eine authentifizierte Verbindung zu erstellen.

### Nicht authentifizierte Verbindung

Nicht authentifizierte Verbindungen sind die Standard-Streaming-Verbindung, die Sie erstellen können, wenn Sie Daten an Platform streamen möchten.

Um eine nicht authentifizierte Basisverbindung zu erstellen, stellen Sie eine POST-Anfrage an die `/connections` -Endpunkt hinzugefügt, während Sie einen Namen für Ihre Verbindung, den Datentyp und die HTTP-API-Verbindungsspezifikations-ID angeben. Diese ID lautet `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

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
| `connectionSpec.id` | Die Verbindungsspezifikations-ID, die der HTTP-API entspricht. Diese ID lautet `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`. |
| `auth.params.dataType` | Der Datentyp für die Streaming-Verbindung. Zu den unterstützten Werten gehören: `xdm` und `raw`. |
| `auth.params.name` | Der Name der Streaming-Verbindung, die Sie erstellen möchten. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 mit Details zur neu erstellten Verbindung zurück, einschließlich der eindeutigen Kennung (`id`).

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `id` | Die `id` der neu erstellten Basisverbindung. |
| `etag` | Eine der Verbindung zugewiesene Kennung, die die Version der Basisverbindung angibt. |

### Authentifizierte Verbindung

Authentifizierte Verbindungen sollten verwendet werden, wenn Sie zwischen Datensätzen aus vertrauenswürdigen und nicht vertrauenswürdigen Quellen unterscheiden müssen. Benutzer, die Informationen mit personenbezogenen Daten (PII) senden möchten, sollten beim Streaming von Informationen an Platform eine authentifizierte Verbindung erstellen.

Um eine authentifizierte Basisverbindung zu erstellen, müssen Sie die `authenticationRequired` -Parameter in Ihrer Anforderung ein und geben Sie seinen Wert als `true`. In diesem Schritt können Sie auch eine Quell-ID für Ihre authentifizierte Basisverbindung angeben. Dieser Parameter ist optional und verwendet denselben Wert wie die `name` -Attribut, wenn es nicht angegeben wird.


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
| `auth.params.sourceId` | Eine zusätzliche Kennung, die beim Erstellen einer authentifizierten Basisverbindung verwendet werden kann. Dieser Parameter ist optional und verwendet denselben Wert wie die `name` -Attribut, wenn es nicht angegeben wird. |
| `auth.params.authenticationRequired` | Der Parameter, der angibt, dass die erstellte Streaming-Verbindung hergestellt wurde |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 mit Details zur neu erstellten Verbindung zurück, einschließlich der eindeutigen Kennung (`id`).

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

## Abrufen der Streaming-Endpunkt-URL

Mit der erstellten Basisverbindung können Sie jetzt Ihre Streaming-Endpunkt-URL abrufen.

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

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit detaillierten Informationen zur angeforderten Verbindung zurück. Die Streaming-Endpunkt-URL wird automatisch mit der Verbindung erstellt und kann mithilfe der `inletUrl` -Wert.

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

Um eine Quellverbindung zu erstellen, stellen Sie eine POST-Anfrage an die `/sourceConnections` -Endpunkt bei der Bereitstellung Ihrer Basis-Verbindungs-ID.

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

Eine erfolgreiche Antwort gibt den HTTP-Status 201 mit detaillierten Informationen zur neu erstellten Quellverbindung zurück, einschließlich der eindeutigen Kennung (`id`).

```json
{
  "id": "34ece231-294d-416c-ad2a-5a5dfb2bc69f",
  "etag": "\"d505125b-0000-0200-0000-637eb7790000\""
}
```

## Erstellen eines XDM-Zielschemas {#target-schema}

Damit die Quelldaten in Platform verwendet werden können, muss ein Zielschema erstellt werden, das die Quelldaten entsprechend Ihren Anforderungen strukturiert. Das Zielschema wird dann verwendet, um einen Platform-Datensatz zu erstellen, in dem die Quelldaten enthalten sind.

Ein Ziel-XDM-Schema kann erstellt werden, indem eine POST-Anfrage an die [Schema-Registrierungs-API](https://www.adobe.io/experience-platform-apis/references/schema-registry/) durchgeführt wird.

Ausführliche Schritte zum Erstellen eines XDM-Zielschemas finden Sie im Tutorial zum [Erstellen eines Schemas mithilfe der API](../../../../../xdm/api/schemas.md).

### Erstellen eines Zieldatensatzes {#target-dataset}

Ein Zieldatensatz kann erstellt werden, indem eine POST-Anfrage an die [Catalog Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) durchgeführt wird, wodurch die ID des Zielschemas in der Payload angegeben wird.

Ausführliche Anweisungen zum Erstellen eines Zieldatensatzes finden Sie im Tutorial zu [Erstellen eines Datensatzes mithilfe der API](../../../../../catalog/api/create-dataset.md).

## Erstellen einer Zielverbindung {#target}

Eine Zielverbindung stellt die Verbindung zum Ziel dar, in das die aufgenommenen Daten übernommen werden. Um eine Zielverbindung zu erstellen, stellen Sie eine POST-Anfrage an `/targetConnections` , während Sie IDs für Ihren Zieldatensatz und Ihr Ziel-XDM-Schema angeben. In diesem Schritt müssen Sie auch die Spezifikations-ID für die Verbindung mit Data Lake angeben. Diese ID lautet `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

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

Eine erfolgreiche Antwort gibt den HTTP-Status 201 mit Details zur neu erstellten Zielverbindung zurück, einschließlich der eindeutigen Kennung (`id`).

```json
{
  "id": "07f2f6ff-1da5-4704-916a-c615b873cba9",
  "etag": "\"340680f7-0000-0200-0000-637eb8730000\""
}
```

## Erstellen einer Zuordnung {#mapping}

Damit die Quelldaten in einen Zieldatensatz aufgenommen werden können, müssen sie zunächst dem Zielschema zugeordnet werden, zu dem der Zieldatensatz gehört.

Um einen Zuordnungssatz zu erstellen, senden Sie eine POST-Anfrage an den `mappingSets`-Endpunkt der [[!DNL Data Prep] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-prep.yaml), wobei Sie das Ziel-XDM-Schema `$id` und die Details der Zuordnungssätze, die Sie erstellen möchten, angeben.

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

| Eigenschaft | Beschreibung |
| --- | --- |

## Erstellen eines Datenflusses

Nachdem Sie Ihre Quell- und Zielverbindungen erstellt haben, können Sie jetzt einen Datenfluss erstellen. Der Datenfluss ist für die Planung und Erfassung von Daten aus einer Quelle zuständig. Sie können einen Datenfluss erstellen, indem Sie eine POST-Anfrage an die `/flows` -Endpunkt.

**API-Format**

```http
POST /flows
```

**Anfrage**

>[!BEGINTABS]

>[!TAB Ohne Umwandlungen]

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

>[!TAB Mit Umwandlungen]

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
| `flowSpec.id` | Die Flussspezifikations-ID für [!DNL HTTP API]. Um einen Datenfluss mit Transformationen zu erstellen, müssen Sie  `c1a19761-d2c7-4702-b9fa-fe91f0613e81`. Um einen Datenfluss ohne Transformationen zu erstellen, verwenden Sie `d8a6f005-7eaf-4153-983e-e8574508b877`. |
| `sourceConnectionIds` | Die [Quellverbindungs-ID](#source), die in einem früheren Schritt abgerufen wurde. |
| `targetConnectionIds` | Die [Zielverbindungs-ID](#target), die in einem früheren Schritt abgerufen wurde. |
| `transformations.params.mappingId` | Die [Zuordnungs-ID](#mapping), die in einem früheren Schritt abgerufen wurde. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 mit Details zum neu erstellten Datenfluss zurück, einschließlich der eindeutigen Kennung (`id`).

```json
{
  "id": "f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2",
  "etag": "\"dc0459ae-0000-0200-0000-637ebaec0000\""
}
```


## Beitragsdaten zur Aufnahme in Platform {#ingest-data}

Nachdem Sie Ihren Fluss erstellt haben, können Sie Ihre JSON-Nachricht an den zuvor erstellten Streaming-Endpunkt senden.

**API-Format**

```http
POST /collection/{INLET_URL}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{INLET_URL}` | Ihre Streaming-Endpunkt-URL. Sie können diese URL abrufen, indem Sie eine GET-Anfrage an die `/connections` -Endpunkt bei der Bereitstellung Ihrer Basis-Verbindungs-ID. |

**Anfrage**

>[!BEGINTABS]

>[!TAB XDM]

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2' \
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

>[!TAB Rohdaten]

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: 1f086c23-2ea8-4d06-886c-232ea8bd061d' \
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

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zu den neu erfassten Informationen zurück.

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
| `receivedTimeMs` | Ein Zeitstempel (Epoche in Millisekunden), der angibt, wann die Anfrage empfangen wurde. |


## Nächste Schritte

In diesem Tutorial haben Sie eine Streaming-HTTP-Verbindung erstellt, über die Sie den Streaming-Endpunkt verwenden können, um Daten in Platform aufzunehmen. Anweisungen zum Erstellen einer Streaming-Verbindung in der Benutzeroberfläche finden Sie in der [Tutorial zum Erstellen einer Streaming-Verbindung](../../../ui/create/streaming/http.md).

Informationen zum Streamen von Daten an Platform finden Sie im Tutorial zu [Streaming von Zeitreihendaten](../../../../../ingestion/tutorials/streaming-time-series-data.md) oder das Tutorial zu [Streaming von Datensatzdaten](../../../../../ingestion/tutorials/streaming-record-data.md).

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
