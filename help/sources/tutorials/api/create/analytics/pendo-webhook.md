---
title: Erstellen einer Source-Verbindung und eines Datenflusses für Pendo mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit Pendo verbinden.
badge: Beta
exl-id: 12b0295d-4b26-4eb7-a02a-a01d825d2a1e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1397'
ht-degree: 49%

---

# Erstellen einer Quellverbindung und eines Datenflusses für [!DNL Pendo] mithilfe der Flow Service-API

>[!NOTE]
>
>Die [!DNL Pendo]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Quellen finden Sie ](../../../../home.md#terms-and-conditions) „Quellen - Übersicht“.

Das folgende Tutorial führt Sie durch die Schritte zum Erstellen einer Quellverbindung und eines Datenflusses, um [[!DNL Pendo]](https://Pendo.com/) Ereignisdaten mithilfe der -API [[!DNL Flow Service]  Adobe Experience Platform ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte {#getting-started}

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Experience Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

## Verbinden von [!DNL Pendo] mit Experience Platform mithilfe der [!DNL Flow Service]-API {#connect-platform-to-flow-api}

Im Folgenden werden die Schritte beschrieben, die Sie ausführen müssen, um eine Quellverbindung und einen Datenfluss zu erstellen und Ihre [!DNL Pendo] Ereignisdaten an Experience Platform zu übertragen.

### Erstellen einer Quellverbindung {#source-connection}

Erstellen Sie eine Quellverbindung, indem Sie eine POST-Anfrage an die [!DNL Flow Service]-API stellen und dabei die Verbindungsspezifikations-ID Ihrer Quelle, Details wie Name und Beschreibung und das Format Ihrer Daten angeben.

**API-Format**

```https
POST /sourceConnections
```

**Anfrage**

Die folgende Anfrage erstellt eine Quellverbindung für [!DNL Pendo]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Source Connection for Pendo",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "description": "Streaming Source Connection for Pendo",
      "connectionSpec": {
          "id": "6ff5654f-19d5-427d-bd3e-c0ebc802389a",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      }
    }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name Ihrer Quellverbindung. Stellen Sie sicher, dass der Name Ihrer Quellverbindung beschreibend ist, da Sie damit Informationen zu Ihrer Quellverbindung nachschlagen können. |
| `description` | Ein optionaler Wert, den Sie angeben können, um weitere Informationen über Ihre Quellverbindung bereitzustellen. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID, die Ihrer Quelle entspricht. |
| `data.format` | Das Format der [!DNL Pendo]-Daten, die Sie aufnehmen möchten. Derzeit wird nur das Datenformat `json` unterstützt. |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Quellverbindung zurück. Diese ID ist in einem späteren Schritt erforderlich, um einen Datenfluss zu erstellen.

```json
{
    "id": "76b968ff-3ff0-4e98-98bb-f3205d4d370c",
    "etag": "\"0301c198-0000-0200-0000-63f32ba50000\""
}
```

### Erstellen eines XDM-Zielschemas {#target-schema}

Damit die Quelldaten in Experience Platform verwendet werden können, muss ein Zielschema erstellt werden, das die Quelldaten entsprechend Ihren Anforderungen strukturiert. Das Zielschema wird dann verwendet, um einen Experience Platform-Datensatz zu erstellen, in dem die Quelldaten enthalten sind.

Ein Ziel-XDM-Schema kann erstellt werden, indem eine POST-Anfrage an die [Schema-Registrierungs-API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/) durchgeführt wird.

Ausführliche Schritte zum Erstellen eines XDM-Zielschemas finden Sie im Tutorial zum [Erstellen eines Schemas mithilfe der API](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html?lang=de#create).

### Erstellen eines Zieldatensatzes {#target-dataset}

Ein Zieldatensatz kann erstellt werden, indem eine POST-Anfrage an die [Catalog Service API](https://developer.adobe.com/experience-platform-apis/references/catalog/) durchgeführt wird, wodurch die ID des Zielschemas in der Payload angegeben wird.

Ausführliche Anweisungen zum Erstellen eines Zieldatensatzes finden Sie im Tutorial zu [Erstellen eines Datensatzes mithilfe der API](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html?lang=de).

### Erstellen einer Zielverbindung {#target-connection}

Eine Zielverbindung stellt die Verbindung zum Ziel dar, an dem die aufgenommenen Daten gespeichert werden sollen. Um eine Zielverbindung zu erstellen, müssen Sie die feste Verbindungsspezifikations-ID angeben, die dem Data Lake entspricht. Diese ID lautet: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Sie verfügen jetzt über die eindeutigen Kennungen, ein Zielschema, einen Zieldatensatz und die Verbindungsspezifikations-ID zum Data Lake. Anhand dieser Kennungen können Sie mit der [!DNL Flow Service]-API eine Zielverbindung erstellen, um den Datensatz anzugeben, der die eingehenden Quelldaten enthalten wird.

**API-Format**

```https
POST /targetConnections
```

**Anfrage**

Die folgende Anfrage erstellt eine Zielverbindung für [!DNL Pendo]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Target Connection for Pendo",
      "description": "Streaming Target Connection for Pendo",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "json",
          "schema": {
              "id": "https://ns.adobe.com/extconndev/schemas/b48de0b204046e65a4c50232e7946401946b4c519fd7c172",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "63dca52231a6031c07280614"
      }
  }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `name` | Der Name Ihrer Zielverbindung. Stellen Sie sicher, dass der Name Ihrer Zielverbindung beschreibend ist, da Sie damit Informationen zu Ihrer Zielverbindung nachschlagen können. |
| `description` | Ein optionaler Wert, den Sie für weitere Informationen zu Ihrer Zielverbindung angeben können. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID, die dem Data Lake entspricht. Diese feste ID lautet: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | Das Format der [!DNL Pendo]-Daten, die Sie aufnehmen möchten. |
| `params.dataSetId` | Die Zieldatensatz-ID, die in einem vorherigen Schritt abgerufen wurde. |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung der neuen Zielverbindung an (`id`). Diese ID ist in späteren Schritten erforderlich.

```json
{
    "id": "c63978c1-df7e-4611-aa32-3657eab5704b",
    "etag": "\"7f0045f1-0000-0200-0000-63f32c9d0000\""
}
```

### Erstellen einer Zuordnung {#mapping}

Damit die Quelldaten in einen Zieldatensatz aufgenommen werden können, müssen sie zunächst dem Zielschema zugeordnet werden, zu dem der Zieldatensatz gehört. Dies wird durch eine POST-Anfrage an [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) mit Datenzuordnungen erreicht, die in der Anfrage-Payload definiert sind.

**API-Format**

```http
POST /conversion/mappingSets
```

**Anfrage**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "outputSchema": {
          "schemaRef": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/945546112b746524bfd9f1264b26c2b7d8e7f5b7fadb953a",
              "contentType": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
    "mappings": [
        {
            "destinationXdmPath": "_extconndev.accountid",
            "sourceAttribute": "accountId",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.uniqueid",
            "sourceAttribute": "uniqueId",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.name1",
            "sourceAttribute": "properties.guideProperties.name",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.timestamp1",
            "sourceAttribute": "timestamp",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.visitorid",
            "sourceAttribute": "visitorId",
            "identity": false,
            "version": 0
        }
    ]
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `outputSchema.schemaRef.id` | Die ID des [Ziel-XDM-Schema](#target-schema), die in einem früheren Schritt generiert wurde. |
| `mappings.sourceType` | Der Typ des Quellattributs, das zugeordnet wird. |
| `mappings.source` | Das Quellattribut, das einem Ziel-XDM-Pfad zugeordnet werden muss. |
| `mappings.destination` | Der Ziel-XDM-Pfad, dem das Quellattribut zugeordnet wird. |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Zuordnung an, einschließlich der eindeutigen Kennung (`id`). Dieser Wert ist in einem späteren Schritt zum Erstellen eines Datenflusses erforderlich.

```json
{
    "id": "a126ae1a1d134c4b82bd00c2d01a039e",
    "version": 0,
    "createdDate": 1676881164541,
    "modifiedDate": 1676881164541,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### Erstellen eines Flusses {#flow}

Der letzte Schritt, um Daten von [!DNL Pendo] an Experience Platform zu senden, besteht darin, einen Datenfluss zu erstellen. Bislang haben Sie die folgenden erforderlichen Werte vorbereitet:

* [Quellverbindungs-ID](#source-connection)
* [Zielverbindungs-ID](#target-connection)
* [Zuordnungs-ID](#mapping)

Ein Datenfluss ist für die Planung und Erfassung von Daten aus einer Quelle verantwortlich. Sie können einen Datenfluss erstellen, indem Sie eine POST-Anfrage ausführen und dabei die oben genannten Werte in der Payload angeben.

**API-Format**

```http
POST /flows
```

**Anfrage**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Dataflow for Pendo",
      "description": "Streaming Dataflow for Pendo",
      "flowSpec": {
          "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "339d60a5-9ff6-4eba-8197-e8887eeb3c08"
      ],
      "targetConnectionIds": [
          "df7c660e-3484-463b-b01a-1835e9b04ac9"
      ],
      "transformations": [
      {
        "name": "Mapping",
        "params": {
          "mappingId": "bae11501021646e58cecc1182451af22",
          "mappingVersion": 0
        }
      }
    ]
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name Ihres Datenflusses. Stellen Sie sicher, dass der Name Ihres Datenflusses beschreibend ist, da Sie damit Informationen zu Ihrem Datenfluss suchen können. |
| `description` | Ein optionaler Wert, den Sie angeben können, um weitere Informationen zu Ihrem Datenfluss bereitzustellen. |
| `flowSpec.id` | Die Flussspezifikations-ID, die zum Erstellen eines Datenflusses erforderlich ist. Diese feste ID lautet: `e77fde5a-22a8-11ed-861d-0242ac120002`. |
| `flowSpec.version` | Die entsprechende Version der Flussspezifikations-ID. Dieser Wert ist standardmäßig auf `1.0` festgelegt. |
| `sourceConnectionIds` | Die [Quellverbindungs-ID](#source-connection), die in einem früheren Schritt generiert wurde. |
| `targetConnectionIds` | Die [Zielverbindungs-ID](#target-connection), die in einem früheren Schritt generiert wurde. |
| `transformations` | Diese Eigenschaft enthält die verschiedenen Umwandlungen, die auf Ihre Daten angewendet werden müssen. Diese Eigenschaft ist erforderlich, wenn nicht-XDM-konforme Daten an Experience Platform übermittelt werden. |
| `transformations.name` | Der Name, der der Transformation zugewiesen wurde. |
| `transformations.params.mappingId` | Die [Zuordnungs-ID](#mapping), die in einem früheren Schritt generiert wurde. |
| `transformations.params.mappingVersion` | Die entsprechende Version der Zuordnungs-ID. Dieser Wert ist standardmäßig auf `0` festgelegt. |

**Antwort**

Bei einer erfolgreichen Antwort wird die ID (`id`) des neu erstellten Datenflusses angegeben. Mit dieser ID können Sie Ihren Datenfluss überwachen, aktualisieren oder löschen.

```json
{
    "id": "c341617b-e143-43d5-aff1-da02b3e028b6",
    "etag": "\"9c01173c-0000-0200-0000-63f32d7c0000\""
}
```

### Abrufen der Streaming-Endpunkt-URL {#get-streaming-url}

Nachdem Ihr Datenfluss erstellt wurde, können Sie jetzt Ihre Streaming-Endpunkt-URL abrufen. Mit dieser Endpunkt-URL abonnieren Sie Ihre Quelle für einen Webhook, sodass Ihre Quelle mit Experience Platform kommunizieren kann.

Um Ihre Streaming-Endpunkt-URL abzurufen, stellen Sie eine GET-Anfrage an den `/flows`-Endpunkt und geben Sie die ID Ihres Datenflusses an.

**API-Format**

```http
GET /flows/{FLOW_ID}
```

**Anfrage**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/4982698b-e6b3-48c2-8dcf-040e20121fd2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort werden Informationen zu Ihrem Datenfluss zurückgegeben, einschließlich Ihrer Endpunkt-URL, die als `inletUrl` markiert ist. Auf der Seite [Webhook einrichten](../../../ui/create/analytics/pendo-webhook.md#get-streaming-endpoint-url) können Sie den erforderlichen Wert abrufen.

```json
{
    "items": [
        {
            "id": "d947e6a9-ea53-42c4-985c-c9379265491f",
            "createdAt": 1676875325841,
            "updatedAt": 1676875331938,
            "createdBy": "acme@AdobeID",
            "updatedBy": "acme@AdobeID",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{ORG_ID}",
            "name": "Streaming Dataflow for Pendo",
            "description": "Streaming Dataflow for Pendo",
            "flowSpec": {
                "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"9801a366-0000-0200-0000-63f2f92c0000\"",
            "etag": "\"9801a366-0000-0200-0000-63f2f92c0000\"",
            "sourceConnectionIds": [
                "339d60a5-9ff6-4eba-8197-e8887eeb3c08"
            ],
            "targetConnectionIds": [
                "df7c660e-3484-463b-b01a-1835e9b04ac9"
            ],
            "inheritedAttributes": {
                "properties": {
                    "isSourceFlow": true
                },
                "sourceConnections": [
                    {
                        "id": "339d60a5-9ff6-4eba-8197-e8887eeb3c08",
                        "connectionSpec": {
                            "id": "6ff5654f-19d5-427d-bd3e-c0ebc802389a",
                            "version": "1.0"
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "df7c660e-3484-463b-b01a-1835e9b04ac9",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "options": {
                "inletUrl": "https://dcs.adobedc.net/collection/e389c18dbc7f5de8b95df07b1b89d76ddd9b1e88d5423abc71b6ac9161491373"
            },
            "transformations": [
                {
                    "name": "Mapping",
                    "params": {
                        "mappingId": "bae11501021646e58cecc1182451af22",
                        "mappingVersion": 0
                    }
                }
            ],
            "runs": "/runs?property=flowId==4d90b316-1c9b-469d-935f-5a27d5deefdf",
            "providerRefId": "19d9fb14-9cb9-42a5-bb8b-23dc545e766a",
            "lastOperation": {
                "started": 0,
                "updated": 0,
                "operation": "enable"
            },
            "lastRunDetails": {
                "id": "d6972216-2332-41f6-8ed3-2ac82e6550b7",
                "state": "partialSuccess",
                "startedAtUTC": 1676862000000,
                "completedAtUTC": 1676867880000
            }
        }
    ]
}
```

## Anhang {#appendix}

Im folgenden Abschnitt finden Sie Informationen zu den Schritten, die Sie zum Überwachen, Aktualisieren und Löschen Ihres Datenflusses durchführen können.

### Überwachen Ihres Datenflusses {#monitor-dataflow}

Nachdem Ihr Datenfluss erstellt wurde, können Sie die Datenaufnahme überwachen, um Informationen über die Datenflussausführungen, den Abschlussstatus und Fehler anzuzeigen. Vollständige API-Beispiele finden Sie im Handbuch unter [Überwachen Ihrer Quelldatenflüsse mithilfe der API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html?lang=de).

### Aktualisieren des Datenflusses {#update-dataflow}

Aktualisieren Sie die Details Ihres Datenflusses, z. B. seinen Namen und seine Beschreibung, sowie seinen Ausführungsplan und die zugehörigen Zuordnungssätze, indem Sie eine PATCH-Anfrage an den `/flows`-Endpunkt [!DNL Flow Service] -API stellen und dabei die ID Ihres Datenflusses angeben. Bei einer PATCH-Anfrage müssen Sie die eindeutige `etag` Ihres Datenflusses in der `If-Match`-Kopfzeile angeben. Vollständige API-Beispiele finden Sie im Handbuch unter [Aktualisieren von Quelldatenflüssen mithilfe der API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html?lang=de)

### Konto aktualisieren {#update-account}

Aktualisieren Sie den Namen, die Beschreibung und die Anmeldeinformationen Ihres Quellkontos, indem Sie eine PATCH-Anfrage an die [!DNL Flow Service]-API durchführen und dabei Ihre Basisverbindungs-ID als Abfrageparameter angeben. Bei einer PATCH-Anfrage müssen Sie die eindeutige `etag` Ihres Quellkontos in der `If-Match`-Kopfzeile angeben. Vollständige API-Beispiele finden Sie im Handbuch unter [Aktualisieren Ihres Quellkontos mithilfe der API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html?lang=de).

### Löschen des Datenflusses {#delete-dataflow}

Löschen Sie Ihren Datenfluss, indem Sie eine DELETE-Anfrage an die [!DNL Flow Service]-API stellen und dabei die ID des Datenflusses angeben, den Sie als Teil des Abfrageparameters löschen möchten. Vollständige API-Beispiele finden Sie im Handbuch unter [Löschen Ihrer Datenflüsse mithilfe der API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html?lang=de).

### Konto löschen {#delete-account}

Löschen Sie Ihr Konto, indem Sie eine DELETE-Anfrage an die [!DNL Flow Service]-API mit Angabe der Basisverbindungs-ID des Kontos ausführen, das Sie löschen möchten. Vollständige API-Beispiele finden Sie im Handbuch unter [Löschen Ihres Quellkontos mithilfe der API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html?lang=de).
