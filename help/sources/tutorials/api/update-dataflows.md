---
title: Aktualisieren von Datenflüssen mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie einen Datenfluss, einschließlich Name, Beschreibung und Zeitplan, mithilfe der Flow Service-API erstellen.
exl-id: 367a3a9e-0980-4144-a669-e4cfa7a9c722
source-git-commit: 9e1edaa4183a8025b8391f58d480063adc834616
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 87%

---

# Aktualisieren von Datenflüssen mithilfe der Flow Service-API

In diesem Tutorial werden die Schritte zum Aktualisieren eines Datenflusses mit der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) beschrieben, einschließlich der grundlegenden Informationen, des Zeitplans und der Zuordnungssätze.

>[!TIP]
>
>Ihre Quellverbindung und Ihre Zielverbindung sollten einem einzigen Datenfluss zugeordnet sein. Sie sollten Ihre Quell- und Zielverbindungen nicht separat aktualisieren, da die Änderungen nicht im entsprechenden Datenfluss übernommen werden. Wenn Ihr Anwendungsfall eine Aktualisierung Ihrer Quell- und Zielverbindungen erfordert, müssen Sie ein neues Paar aus Quell- und Zielverbindungen sowie einen neuen Datenfluss erstellen.

## Erste Schritte

Für dieses Tutorial benötigen Sie eine gültige Fluss-ID. Wenn Sie keine gültige Fluss-ID haben, wählen Sie Ihren gewünschten Connector aus der [Quellen – Übersicht](../../home.md) und befolgen Sie die beschriebenen Schritte, bevor Sie dieses Tutorial beginnen.

Dieses Tutorial setzt außerdem ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Verwenden von Platform-APIs

Weitere Informationen zum erfolgreichen Aufrufen von Platform-APIs finden Sie im Handbuch [Erste Schritte mit Platform-APIs](../../../landing/api-guide.md).

## Nachschlagen von Datenflussdetails

Der erste Schritt bei der Aktualisierung Ihres Datenflusses besteht darin, Datenflussdetails mit Ihrer Fluss-ID abzurufen. Sie können die aktuellen Details eines vorhandenen Datenflusses anzeigen, indem Sie eine GET-Anfrage an den `/flows`-Endpunkt stellen.

**API-Format**

```http
GET /flows/{FLOW_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{FLOW_ID}` | Der eindeutige `id`-Wert für den Datenfluss, den Sie abrufen möchten. |

**Anfrage**

Mit der folgenden Anfrage werden aktualisierte Informationen zu Ihrer Fluss-ID abgerufen.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort werden die aktuellen Details Ihres Datenflusses zurückgegeben, einschließlich der Version, des Zeitplans und der eindeutigen Kennung (`id`).

```json
{
    "items": [
        {
            "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
            "createdAt": 1612310475905,
            "updatedAt": 1614122324830,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{ORG_ID}",
            "name": "Database dataflow using BigQuery",
            "description": "collecting test1.Mytable from Google BigQuery",
            "flowSpec": {
                "id": "14518937-270c-4525-bdec-c2ba7cce3860",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"5400d99c-0000-0200-0000-60358d540000\"",
            "etag": "\"5400d99c-0000-0200-0000-60358d540000\"",
            "sourceConnectionIds": [
                "b7581b59-c603-4df1-a689-d23d7ac440f3"
            ],
            "targetConnectionIds": [
                "320f119a-5ac1-4ab1-88ea-eb19e674ea2e"
            ],
            "inheritedAttributes": {
                "sourceConnections": [
                    {
                        "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
                        "connectionSpec": {
                            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
                            "version": "1.0"
                        },
                        "baseConnection": {
                            "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
                            "connectionSpec": {
                                "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
                                "version": "1.0"
                            }
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "320f119a-5ac1-4ab1-88ea-eb19e674ea2e",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "scheduleParams": {
                "startTime": "1612310466",
                "frequency": "week",
                "interval": "15",
                "backfill": "true"
            },
            "transformations": [
                {
                    "name": "Copy",
                    "params": {
                        "deltaColumn": {
                            "name": "Datefield",
                            "dateFormat": "YYYY-MM-DD",
                            "timezone": "UTC"
                        }
                    }
                },
                {
                    "name": "Mapping",
                    "params": {
                        "mappingId": "0b090130b58b4819afc78b6dc98b484d",
                        "mappingVersion": "0"
                    }
                }
            ],
            "runs": "/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c/runs",
            "lastOperation": {
                "started": 1614122316652,
                "updated": 1614122324830,
                "percentCompleted": 100.0,
                "status": {
                    "value": "completed",
                    "errors": []
                },
                "ops": [
                    {
                        "op": "replace",
                        "path": "/scheduleParams/frequency",
                        "value": "week"
                    }
                ],
                "operation": "update"
            },
            "lastRunDetails": {
                "id": "a10cc80b-fbea-4c6b-873e-d7fd32f4d12d",
                "state": "success",
                "startedAtUTC": 1613079975512,
                "completedAtUTC": 1613080027511
            }
        }
    ]
}
```

## Aktualisieren des Datenflusses

Stellen Sie eine PATCH-Anfrage an die [!DNL Flow Service]-API mit Angabe Ihrer Fluss-ID, Version und des neuen Zeitplans, den Sie verwenden möchten.

>[!IMPORTANT]
>
>Die `If-Match`-Kopfzeile ist bei einer PATCH-Anfrage erforderlich. Der Wert für diese Kopfzeile ist die eindeutige Version der Verbindung, die Sie aktualisieren möchten. Der eTag-Wert wird bei jeder erfolgreichen Aktualisierung eines Datenflusses aktualisiert.

**API-Format**

```http
PATCH /flows/{FLOW_ID}
```

**Anfrage**

Mit der folgenden Anfrage werden Ihr Ablaufplan für den Fluss sowie der Name und die Beschreibung Ihres Datenflusses aktualisiert.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
            {
                "op": "replace",
                "path": "/scheduleParams/frequency",
                "value": "day"
            },
            {
                "op": "replace",
                "path": "/name",
                "value": "Database Dataflow Feb2021"
            },
            {
                "op": "replace",
                "path": "/description",
                "value": "Database dataflow for testing update API"
            }
        ]'
```

| Eigenschaft | Beschreibung |
| --------- | ----------- |
| `op` | Der Operationsaufruf, der verwendet wird, um die Aktion zu definieren, die zur Aktualisierung des Datenflusses erforderlich ist. Die Operationen umfassen `add`, `replace` und `remove`. |
| `path` | Definiert den Teil des Flusses, der aktualisiert werden soll. |
| `value` | Der neue Wert, mit dem Sie Ihren Parameter aktualisieren möchten. |

**Antwort**

Bei einer erfolgreichen Antwort werden Ihre Fluss-ID und ein aktualisiertes eTag zurückgegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET-Anfrage an die [!DNL Flow Service]-API bei gleichzeitiger Angabe Ihrer Fluss-ID stellen.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Aktualisieren der Zuordnung

Sie können den Zuordnungssatz eines bestehenden Datenflusses aktualisieren, indem Sie eine PATCH-Anfrage an die [!DNL Flow Service]-API stellen und aktualisierte Werte für Ihre `mappingId` und `mappingVersion` angeben.

**API-Format**

```http
PATCH /flows/{FLOW_ID}
```

**Anfrage**

Die folgende Anfrage aktualisiert den Zuordnungssatz Ihres Datenflusses.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "50014cc8-0000-0200-0000-6036eb720000"' \
    -d '[
        {
            "op": "replace",
            "path": "/transformations/0",
            "value": {
                "name": "Mapping",
                "params": {
                    "mappingId": "c5f22f04e09f44498e528901546a83b1",
                    "mappingVersion": 2
                }
            }
        }
    ]'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `op` | Der Operationsaufruf, der verwendet wird, um die Aktion zu definieren, die zur Aktualisierung des Datenflusses erforderlich ist. Die Operationen umfassen `add`, `replace` und `remove`. |
| `path` | Definiert den Teil des Flusses, der aktualisiert werden soll. In diesem Beispiel wird `transformations` aktualisiert. |
| `value.name` | Der Name der Eigenschaft, die aktualisiert werden soll. |
| `value.params.mappingId` | Die neue Zuordnungs-ID, die zum Aktualisieren des Zuordnungssatzes des Datenflusses verwendet werden soll. |
| `value.params.mappingVersion` | Die neue Zuordnungsversion, die mit der aktualisierten Zuordnungs-ID verknüpft ist. |

**Antwort**

Bei einer erfolgreichen Antwort werden Ihre Fluss-ID und ein aktualisiertes eTag zurückgegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET-Anfrage an die [!DNL Flow Service]-API stellen und gleichzeitig Ihre Fluss-ID angeben.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"2c000802-0000-0200-0000-613976440000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie die grundlegenden Informationen, den Zeitplan und die Zuordnungssätze Ihres Datenflusses mithilfe der [!DNL Flow Service]-API aktualisiert. Weitere Informationen zur Verwendung von Quell-Connectoren finden Sie im Abschnitt [Quellen – Übersicht](../../home.md).
