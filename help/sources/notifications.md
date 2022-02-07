---
keywords: Experience Platform; Homepage; beliebte Themen Benachrichtigungen
description: Durch Abonnieren von Adobe I/O-Ereignissen können Sie Webhooks verwenden, um Benachrichtigungen über die Flusslaufstatus Ihrer Quellverbindungen zu erhalten. Diese Benachrichtigungen enthalten Informationen zum Erfolg Ihrer Flussausführung oder zu Fehlern, die zum Fehler einer Ausführung beigetragen haben.
solution: Experience Platform
title: Flusslaufbenachrichtigungen
topic-legacy: overview
exl-id: 0f1cde97-3030-4b8e-be08-21f64e78b794
source-git-commit: a51c878bbfd3004cb597ce9244a9ed2f2318604b
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 7%

---

# Flusslaufbenachrichtigungen

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten zu strukturieren, zu beschriften und zu erweitern mithilfe von [!DNL Platform] Dienste. Daten können aus verschiedensten Quellen erfasst werden, darunter etwa Adobe-Anwendungen, Cloud-basierte Datenspeicher und Datenbanken.

[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) dient zur Erfassung und Zentralisierung von Kundendaten aus verschiedenen Quellen innerhalb von [!DNL Platform]. Der Dienst bietet eine Benutzeroberfläche und eine RESTful-API, über die alle unterstützten Quellen verbunden werden können.

Mit Adobe I/O Events können Sie  abonnieren und Webhooks verwenden, um Benachrichtigungen über den Ausführungsstatus zu erhalten. Diese Benachrichtigungen enthalten Informationen zum Erfolg Ihrer Flussausführung oder zu Fehlern, die zum Fehler einer Ausführung beigetragen haben.

In diesem Dokument erfahren Sie, wie Sie Ereignisse abonnieren, Webhooks registrieren und Benachrichtigungen mit Informationen zum Status Ihrer Workflow-Ausführungen erhalten.

## Erste Schritte

In diesem Tutorial wird davon ausgegangen, dass Sie bereits mindestens eine Quellverbindung erstellt haben, deren Fluss überwacht werden soll. Wenn Sie noch keine Quellverbindung konfiguriert haben, besuchen Sie zunächst das [Quellen - Übersicht](./home.md) um die Quelle Ihrer Wahl zu konfigurieren, bevor Sie zu diesem Handbuch zurückkehren.

Dieses Dokument setzt auch ein Verständnis der Webhooks voraus und wie ein Webhook von einer Anwendung zur anderen verbunden werden kann. Eine Einführung in Webhooks finden Sie in der [[!DNL I/O Events] Dokumentation](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md).

## Webhook für Fluss-Ausführungsbenachrichtigungen registrieren

Um Benachrichtigungen über Flusslaufvorgänge zu erhalten, müssen Sie die Adobe Developer Console verwenden, um einen Webhook bei Ihrem [!DNL Experience Platform] Integration.

Folgen Sie dem Tutorial zu [Abonnieren von [!DNL I/O Event]-Benachrichtigungen](../observability/alerts/subscribe.md) für detaillierte Schritte, wie Sie dies erreichen können.

>[!IMPORTANT]
>
>Stellen Sie während des Abonnementprozesses sicher, dass Sie **[!UICONTROL Plattformbenachrichtigungen]** als Ereignisanbieter und wählen Sie die folgenden Ereignisanmeldungen aus:
>
>* **[!UICONTROL Flusslauf der Experience Platform Source erfolgreich]**
>* **[!UICONTROL Experience Platform Source&#39;s Flow Run Failed]**


## Flusslaufbenachrichtigungen empfangen

Wenn Ihr Webhook verbunden ist und Ihr Ereignisabonnement abgeschlossen ist, können Sie über das Webhook-Dashboard mit dem Empfang von Benachrichtigungen zu Flüssen beginnen.

Eine Benachrichtigung gibt Informationen wie die Anzahl der ausgeführten Aufnahmeaufträge, die Dateigröße und Fehler zurück. Eine Benachrichtigung gibt auch eine Payload zurück, die mit Ihrer Flow-Ausführung im JSON-Format verknüpft ist. Die Antwort-Payload kann entweder als `sources_flow_run_success` oder `sources_flow_run_failure`.

>[!IMPORTANT]
>
>Wenn die partielle Erfassung während der Flusserstellung aktiviert ist, wird ein Fluss, der sowohl erfolgreiche als auch fehlgeschlagene Aufnahmen enthält, als `sources_flow_run_success` nur dann, wenn die Fehleranzahl unter dem Fehlerschwellenprozentsatz liegt, der während der Flusserstellung festgelegt wurde. Wenn eine erfolgreiche Flussausführung Fehler enthält, werden diese Fehler weiterhin als Teil der Rückgabe-Payload einbezogen.

### Erfolgreich

Eine erfolgreiche Antwort gibt eine Reihe von `metrics` die Eigenschaften eines bestimmten Flusslaufs definieren und `activities` wird beschrieben, wie Daten transformiert werden.

```json
{
  "event_id": "aec55616-1715-487f-8044-ba648cc8ffee",
  "event": {
    "createdAt": 1597213529158,
    "updatedAt": 1597213530760,
    "createdBy": "{CREATED_BY}",
    "updatedBy": "{UPDATED_BY}",
    "createdClient": "{CREATED_CLIENT}",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "7127a4f0-def8-11e9-83ce-e79494b1c2a5",
    "sandboxName": "prod",
    "imsOrgId": "{IMS_ORG}",
    "id": "933cf9f4-cf01-4d75-bcf9-f4cf010d750a",
    "flowId": "1c6f1047-dcaf-48fe-af10-47dcaf08feaf",
    "providerRefId": "test1234",
    "etag": "\"5100ec97-0000-0200-0000-5f338b5b0000\"",
    "metrics": {
      "durationSummary": {
        "startedAtUTC": 1590512053,
        "completedAtUTC": 1590512053
      },
      "sizeSummary": {
        "inputBytes": 2048,
        "outputBytes": 1024
      },
      "recordSummary": {
        "inputRecordCount": 100,
        "outputRecordCount": 70
      },
      "fileSummary": {
        "inputFileCount": 10,
        "outputFileCount": 10
      },
      "statusSummary": {
        "status": "success"
      }
    },
    "activities": [
      {
        "id": "copyActivity",
        "updatedAtUTC": 87473822,
        "durationSummary": {
          "startedAtUTC": 1590512053,
          "completedAtUTC": 1590512053
        },
        "sizeSummary": {
          "inputBytes": 2048,
          "outputBytes": 1098
        },
        "recordSummary": {
          "inputRecordCount": 100,
          "outputRecordCount": 100
        },
        "fileSummary": {
          "inputFileCount": 10,
          "outputFileCount": 10
        },
        "statusSummary": {
          "status": "success",
          "extensions": {
            "adf/pipeline/id": "abcd",
            "adf/run/id": "1234"
          }
        },
        "sourceInfo": [
          {
            "id": "sourceConnectionId1",
            "type": "SourceConnection",
            "reference": {
              "type": "AdfRunId"
            }
          }
        ]
      },
      {
        "id": "promotionActivity",
        "updatedAtUTC": 87473822,
        "durationSummary": {
          "completedAtUTC": 1590512053
        },
        "sizeSummary": {
          "inputBytes": 1098,
          "outputBytes": 1024
        },
        "recordSummary": {},
        "fileSummary": {
          "inputFileCount": 10,
          "outputFileCount": 10,
          "extensions": {
            "manifest": {
              "fileInfo": "https://platform.adobe.io/data/foundation/export/batches/01E4TSJNM2H5M74J0XB8MFWDHK/meta?path=input_files"
            }
          }
        },
        "statusSummary": {
          "status": "success",
          "extensions": {
            "batchId": "b1",
            "acp_request_id": "1234"
          }
        },
        "targetInfo": [
          {
            "id": "targetConnectionId1",
            "type": "TargetConnection",
            "reference": {
              "type": "batch"
            }
          }
        ]
      }
    ],
    "slaCreatedAt": 1597213531124,
    "processStartTime": 1597213531213,
    "header": {
      "_adobeio": {
        "imsOrgId": "{IMS_ORG}",
        "providerMetadata": "platform_notifications",
        "eventCode": "sources_flow_run_success"
      }
    },
    "transformedTime": 1597213531214
  }
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `metrics` | Definiert die Eigenschaften der Daten im Durchfluss. |
| `activities` | Definiert die verschiedenen Schritte und Aktivitäten, die zur Transformation der Daten durchgeführt werden. |
| `durationSummary` | Definiert die Start- und Endzeit des Durchlaufs. |
| `sizeSummary` | Definiert das Volumen der Daten in Byte. |
| `recordSummary` | Definiert die Datensatzanzahl der Daten. |
| `fileSummary` | Definiert die Dateianzahl der Daten. |
| `fileInfo` | Eine URL, die zu einem Überblick über die erfolgreich aufgenommenen Dateien führt. |
| `statusSummary` | Definiert, ob die Flussausführung ein Erfolg oder ein Fehler ist. |

### Fehlgeschlagen

Die folgende Antwort ist ein Beispiel für einen fehlgeschlagenen Fluss, bei dem bei der Verarbeitung der kopierten Daten ein Fehler auftritt. Fehler können auch auftreten, wenn Daten aus der Quelle kopiert werden. Eine fehlgeschlagene Ausführung von Flüssen enthält Informationen zu den Fehlern, die zum Fehler der Ausführung beigetragen haben, einschließlich Fehler und Beschreibung.

```json
[
  {
    "messages": [
      {
        "msgType": "eventNotification",
        "version": "1.0",
        "timestamp": 1597434157622,
        "imsOrgId": "{IMS_ORG}",
        "schema": {
          "name": "run-notification",
          "version": "1.0"
        },
        "provider": "FlowService",
        "_eventNotificationMeta": {
          "category": "Platform Notifications",
          "type": "sources_flow_run_failed"
        },
        "value": {
          "createdAt": 1597434147259,
          "updatedAt": 1597434157567,
          "createdBy": "{CREATED_BY}",
          "updatedBy": "{UPDATED_BY}",
          "createdClient": "{CREATED_CLIENT}",
          "updatedClient": "{UPDATED_CLIENT}",
          "sandboxId": "e49ebb00-d0fa-11e9-b164-ed6a398c8b35",
          "sandboxName": "prod",
          "imsOrgId": "{IMS_ORG}",
          "id": "d9024c32-2174-4271-824c-322174627101",
          "flowId": "cf4fce79-8822-456d-8fce-798822556dc6",
          "etag": "\"0c003dbf-0000-0200-0000-5f36e92d0000\"",
          "metrics": {
            "durationSummary": {
              "startedAtUTC": 1597434147190
            },
            "sizeSummary": {
              "inputBytes": -1
            },
            "fileSummary": {
              "inputFileCount": -1
            },
            "statusSummary": {
              "status": "failed",
              "errors": [
                {
                  "code": "CONNECTOR-2001-500",
                  "message": "Error in processing (parsing, validation or transformation) the copied data."
                }
              ]
            }
          },
          "activities": [
            {
              "id": "promotionActivity",
              "updatedAtUTC": 1597434157529,
              "durationSummary": {
                "startedAtUTC": 1597434147190,
                "completedAtUTC": 1597434157212
              },
              "sizeSummary": {
                "inputBytes": -1
              },
              "recordSummary": {},
              "fileSummary": {
                "inputFileCount": -1,
                "extensions": {
                  "manifest": {
                    "fileInfo": "https://platform-stage.adobe.io/data/foundation/export/batches/6f6a900f-e40d-4f0e-9bb9-b614436c3465/meta?path=input_files"
                  }
                }
              },
              "statusSummary": {
                "status": "failed",
                "errors": [
                  {
                    "code": "CONNECTOR-2001-500",
                    "message": "Error in processing (parsing, validation or transformation) the copied data."
                  }
                ],
                "extensions": {
                  "errors": [
                    {
                      "code": "133",
                      "message": "We are unable to locate any files uploaded for this batch. Please upload files to ingest."
                    }
                  ]
                }
              },
              "targetInfo": [
                {
                  "id": "e88737aa-27b8-4795-8737-aa27b8f7959e",
                  "type": "TargetConnection",
                  "reference": {
                    "type": "Batch",
                    "ids": [
                      "6f6a900f-e40d-4f0e-9bb9-b614436c3465"
                    ]
                  }
                }
              ]
            }
          ]
        }
      }
    ]
  }
]
```

| Eigenschaft | Beschreibung |
| ---------- | ----------- |
| `fileInfo` | Eine URL, die zu einem Überblick über die Dateien führt, die erfolgreich und nicht erfolgreich erfasst wurden. |

>[!NOTE]
>
>Siehe [Anhang](#errors) für weitere Informationen zu Fehlermeldungen.

## Nächste Schritte

Sie können jetzt Ereignisse abonnieren, mit denen Sie Echtzeit-Benachrichtigungen zu Ihren Flusslaufstatus erhalten. Weitere Informationen zu Fluss-Läufen und -Quellen finden Sie unter [Quellen - Übersicht](./home.md).

## Anhang

Die folgenden Abschnitte enthalten zusätzliche Informationen für die Arbeit mit Benachrichtigungen über Fluss-Ausführungsvorgänge.

### Grundlagen zu Fehlermeldungen {#errors}

Aufnahmefehler können auftreten, wenn Daten aus der Quelle kopiert oder die kopierten Daten verarbeitet werden [!DNL Platform]. Weitere Informationen zu bestimmten Fehlern finden Sie in der unten stehenden Tabelle.

| Fehler | Beschreibung |
| ---------- | ----------- |
| `CONNECTOR-1001-500` | Beim Kopieren von Daten aus einer Quelle ist ein Fehler aufgetreten. |
| `CONNECTOR-2001-500` | Beim Verarbeiten der kopierten Daten in ist ein Fehler aufgetreten. [!DNL Platform]. Dieser Fehler kann beim Analysieren, Validieren oder Transformieren auftreten. |
