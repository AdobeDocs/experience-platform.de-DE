---
keywords: Experience Platform;Startseite;beliebte Themen;Überwachen von Datenflüssen;Flow Service API;Flow Service
solution: Experience Platform
title: Überwachen von Datenflüssen zu Quellen mithilfe der Flow Service-API
topic-legacy: overview
type: Tutorial
description: In diesem Tutorial werden die Schritte zum Überwachen von Daten in Datenflüssen auf Vollständigkeit, Fehler und Metriken mithilfe der Flow Service-API beschrieben.
exl-id: 5b7d1aa4-5e6d-48f4-82bd-5348dc0e890d
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 96%

---

# Überwachen von Datenflüssen aus Quellen mithilfe der Flow Service-API

In diesem Tutorial werden die Schritte zum Überwachen von Datenflüssen auf Vollständigkeit, Fehler und Metriken mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) beschrieben.

>[!NOTE]
>
>Für dieses Tutorial benötigen Sie den ID-Wert eines Datenflusses. Wenn Sie keine gültige Datenfluss-ID haben, wählen Sie einen beliebigen Connector aus der [Quellen-Übersicht](../../home.md) und führen Sie die zum Erstellen eines Datenflusses beschriebenen Schritte aus, bevor Sie dieses Tutorial ausführen.

## Erste Schritte

Dieses Tutorial setzt außerdem ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Verwenden von Platform-APIs

Informationen zum Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../landing/api-guide.md).

## Überwachen von Datenflüssen

Um den Status Ihres Datenflusses anzuzeigen, stellen Sie eine GET-Anfrage an die [!DNL Flow Service]-API. Geben Sie dabei die entsprechende Fluss-ID Ihres Datenflusses an.

**API-Format**

```http
GET /runs?property=flowId=={FLOW_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{FLOW_ID}` | Der eindeutige `id`-Wert für den Datenfluss, den Sie überwachen möchten. |

**Anfrage**

Mit der folgenden Anfrage werden die Spezifikationen für einen vorhandenen Datenfluss abgerufen.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==c9cef9cb-c934-4467-8ef9-cbc934546741' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort werden Details zu Ihrem Flussvorgang angegeben, einschließlich Informationen zum Erstellungsdatum, zu den Quell- und Zielverbindungen sowie zur eindeutigen Kennung des Flussvorgangs (`id`).

```json
{
    "items": [
        {
            "createdAt": 1596656079576,
            "updatedAt": 1596656113526,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
            "sandboxName": "prod",
            "id": "9830305a-985f-47d0-b030-5a985fd7d004",
            "flowId": "c9cef9cb-c934-4467-8ef9-cbc934546741",
            "etag": "\"b8003af1-0000-0200-0000-5f2b09f10000\"",
            "metrics": {
                "durationSummary": {
                    "startedAtUTC": 1596656058198,
                    "completedAtUTC": 1596656113306
                },
                "sizeSummary": {
                    "inputBytes": 24012,
                    "outputBytes": 17128
                },
                "recordSummary": {
                    "inputRecordCount": 100,
                    "outputRecordCount": 99,
                    "failedRecordCount": 1
                },
                "fileSummary": {
                    "inputFileCount": 1,
                    "outputFileCount": 1,
                    "activityRefs": [
                        "promotionActivity"
                    ]
                },
                "statusSummary": {
                    "status": "success",
                    "errors": [
                        {
                            "code": "CONNECTOR-2001-500",
                            "message": "Error occurred at promotion activity."
                        }
                    ],
                    "activityRefs": [
                        "promotionActivity"
                    ]
                }
            },
            "activities": [
                {
                    "id": "copyActivity",
                    "updatedAtUTC": 1596656095088,
                    "durationSummary": {
                        "startedAtUTC": 1596656058198,
                        "completedAtUTC": 1596656089650,
                        "extensions": {
                            "windowStart": 1596653708000,
                            "windowEnd": 1596655508000
                        }
                    },
                    "sizeSummary": {
                        "inputBytes": 24012,
                        "outputBytes": 24012
                    },
                    "recordSummary": {},
                    "fileSummary": {
                        "inputFileCount": 1,
                        "outputFileCount": 1
                    },
                    "statusSummary": {
                        "status": "success",
                        "extensions": {
                            "type": "one-time"
                        }
                    },
                    "sourceInfo": [
                        {
                            "id": "c0e18602-f9ea-44f9-a186-02f9ea64f9ac",
                            "type": "SourceConnection",
                            "reference": {
                                "type": "AdfRunId",
                                "ids": [
                                    "8a8eb0cc-e283-4605-ac70-65a5adb1baef"
                                ]
                            }
                        }
                    ]
                },
                {
                    "id": "promotionActivity",
                    "updatedAtUTC": 1596656113485,
                    "durationSummary": {
                        "startedAtUTC": 1596656095333,
                        "completedAtUTC": 1596656113306
                    },
                    "sizeSummary": {
                        "inputBytes": 24012,
                        "outputBytes": 17128
                    },
                    "recordSummary": {
                        "inputRecordCount": 100,
                        "outputRecordCount": 99,
                        "failedRecordCount": 1
                    },
                    "fileSummary": {
                        "inputFileCount": 2,
                        "outputFileCount": 1,
                        "extensions": {
                            "manifest": {
                                "fileInfo": "https://platform.adobe.io/data/foundation/export/batches/01EF01X41KJD82Y9ZX6ET54PCZ/meta?path=input_files"
                            }
                        }
                    },
                    "statusSummary": {
                        "status": "success",
                        "errors": [
                            {
                                "code": "CONNECTOR-2001-500",
                                "message": "Error occurred at promotion activity."
                            }
                        ],
                        "extensions": {
                            "manifest": {
                                "failedRecords": "https://platform.adobe.io/data/foundation/export/batches/01EF01X41KJD82Y9ZX6ET54PCZ/meta?path=row_errors",
                                "sampleErrors": "https://platform.adobe.io/data/foundation/export/batches/01EF01X41KJD82Y9ZX6ET54PCZ/meta?path=row_error_samples.json"
                            },
                            "errors": [
                                {
                                    "code": "INGEST-1212-400",
                                    "message": "Encountered 1 errors in the data. Successfully ingested 99 rows. Review the associated diagnostic files for additional details."
                                },
                                {
                                    "code": "MAPPER-3700-400",
                                    "recordCount": 1,
                                    "message": "Mapper Transform Error"
                                }
                            ]
                        }
                    },
                    "targetInfo": [
                        {
                            "id": "47166b83-01c7-4b65-966b-8301c70b6562",
                            "type": "TargetConnection",
                            "reference": {
                                "type": "Batch",
                                "ids": [
                                    "01EF01X41KJD82Y9ZX6ET54PCZ"
                                ]
                            }
                        }
                    ]
                }
            ]
        }
    ],
    "_links": {}
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `items` | Enthält eine einzige Payload von Metadaten, die mit Ihrer spezifischen Datenflussausführung verknüpft sind. |
| `metrics` | Definiert die Eigenschaften der Daten in der Flussausführung. |
| `activities` | Definiert, wie die Daten transformiert werden. |
| `durationSummary` | Definiert die Start- und Endzeit des Durchlaufs. |
| `sizeSummary` | Definiert das Volumen der Daten in Byte. |
| `recordSummary` | Definiert die Anzahl der Datensätze. |
| `fileSummary` | Definiert die Dateianzahl der Daten. |
| `statusSummary` | Definiert, ob die Flussausführung erfolgreich oder fehlgeschlagen ist. |

## Nächste Schritte

Mit diesem Tutorial haben Sie mithilfe der [!DNL Flow Service]-API Metriken und Fehlerinformationen zu Ihrem Datenfluss abgerufen. Sie können jetzt Ihren Datenfluss entsprechend Ihrem Datenaufnahme-Zeitplan überwachen, um dessen Status und Aufnahmeraten zu verfolgen. Informationen dazu, wie Sie dieselben Aufgaben über die Benutzeroberfläche ausführen, finden Sie im Tutorial zum [Überwachen von Datenflüssen mithilfe der Benutzeroberfläche](../ui/monitor.md).
