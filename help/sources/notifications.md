---
keywords: Experience Platform;Startseite;beliebte Themen;Benachrichtigungen
description: Durch das Abonnieren von Adobe I/O Events können Sie Webhooks verwenden, um Benachrichtigungen über den Flussausführungsstatus Ihrer Quellverbindungen zu erhalten. Diese Benachrichtigungen enthalten Informationen zum Erfolg Ihrer Flussausführung oder zu Fehlern, die zum Fehlschlagen einer Ausführung beigetragen haben.
solution: Experience Platform
title: Benachrichtigungen zur Flussausführung
exl-id: 0f1cde97-3030-4b8e-be08-21f64e78b794
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 16%

---

# Flusslaufbenachrichtigungen

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Experience Platform]-Services zu strukturieren, zu kennzeichnen und zu verbessern. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) wird verwendet, um Kundendaten aus verschiedenen Quellen innerhalb von [!DNL Experience Platform] zu sammeln und zu zentralisieren. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

Mit Adobe I/O Events können Sie Ereignisse abonnieren und Webhooks verwenden, um Benachrichtigungen zum Status Ihrer Flussausführungen zu erhalten. Diese Benachrichtigungen enthalten Informationen zum Erfolg Ihrer Flussausführung oder zu Fehlern, die zum Fehlschlagen einer Ausführung beigetragen haben.

In diesem Dokument wird beschrieben, wie Sie Ereignisse abonnieren, Webhooks registrieren und Benachrichtigungen mit Informationen zum Status Ihrer Flussausführungen erhalten.

## Erste Schritte

In diesem Tutorial wird davon ausgegangen, dass Sie bereits mindestens eine Quellverbindung erstellt haben, deren Flussausführungen Sie überwachen möchten. Wenn Sie noch keine Quellverbindung konfiguriert haben, konsultieren Sie zunächst die [Quellenübersicht](./home.md), um die Quelle Ihrer Wahl zu konfigurieren, bevor Sie zu dieser Anleitung zurückkehren.

Dieses Dokument setzt auch ein Verständnis von Webhooks voraus. Außerdem erfahren Sie, wie Sie einen Webhook von einer Anwendung zu einer anderen verbinden. Eine Einführung in Webhooks finden Sie in der [[!DNL I/O Events] Dokumentation](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md).

## Registrieren eines Webhooks für Benachrichtigungen zu Flussausführungen

Um Flussausführungsbenachrichtigungen zu erhalten, müssen Sie Adobe Developer Console verwenden, um einen Webhook zu Ihrer [!DNL Experience Platform]-Integration zu registrieren.

Im Tutorial zum [ von [!DNL I/O Event]-Benachrichtigungen ](../observability/alerts/subscribe.md) Sie ausführliche Schritte, wie Sie dies tun können.

>[!IMPORTANT]
>
>Achten Sie während des Abonnementvorgangs darauf, dass Sie **[!UICONTROL Platform-Benachrichtigungen]** als Ereignisanbieter auswählen und die folgenden Ereignisabonnements auswählen:
>
>* Flussausführung von **[!UICONTROL Experience Platform Source war erfolgreich]**
>* Die Flussausführung von **[!UICONTROL Experience Platform Source ist fehlgeschlagen]**

## Benachrichtigungen zur Flussausführung empfangen

Wenn Ihr Webhook verbunden und Ihr Ereignisabonnement abgeschlossen ist, können Sie damit beginnen, Flussausführungsbenachrichtigungen über das Webhook-Dashboard zu erhalten.

Eine Benachrichtigung gibt Informationen wie die Anzahl der ausgeführten Aufnahmevorgänge, die Dateigröße und Fehler zurück. Eine Benachrichtigung gibt auch eine Payload zurück, die mit Ihrer Flussausführung im JSON-Format verknüpft ist. Die Antwort-Payload kann entweder als `sources_flow_run_success` oder `sources_flow_run_failure` klassifiziert werden.

>[!IMPORTANT]
>
>Wenn die partielle Aufnahme während des Flusserstellungsprozesses aktiviert ist, wird ein Fluss, der sowohl erfolgreiche als auch fehlgeschlagene Aufnahmen enthält, nur dann als `sources_flow_run_success` markiert, wenn die Anzahl der Fehler unterhalb des Fehlerschwellenwerts liegt, der während des Flusserstellungsprozesses festgelegt wurde. Wenn eine erfolgreiche Flussausführung Fehler enthält, werden diese Fehler weiterhin als Teil der zurückgegebenen Payload einbezogen.

### Erfolgreich

Eine erfolgreiche Antwort gibt einen Satz von `metrics` zurück, die die Eigenschaften einer bestimmten Flussausführung definieren und `activities`, die beschreiben, wie Daten transformiert werden.

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
    "imsOrgId": "{ORG_ID}",
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
        "imsOrgId": "{ORG_ID}",
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
| `metrics` | Definiert die Eigenschaften der Daten in der Flussausführung. |
| `activities` | Definiert die verschiedenen Schritte und Aktivitäten, die zum Transformieren der Daten ausgeführt werden. |
| `durationSummary` | Definiert die Start- und Endzeit des Durchlaufs. |
| `sizeSummary` | Definiert das Volumen der Daten in Byte. |
| `recordSummary` | Definiert die Anzahl der Datensätze. |
| `fileSummary` | Definiert die Dateianzahl der Daten. |
| `fileInfo` | Eine URL, die zu einem Überblick über die erfolgreich aufgenommenen Dateien führt. |
| `statusSummary` | Definiert, ob die Flussausführung erfolgreich oder fehlgeschlagen ist. |

### Fehlgeschlagen

Die folgende Antwort ist ein Beispiel für eine fehlgeschlagene Flussausführung, bei der bei der Verarbeitung der kopierten Daten ein Fehler auftritt. Fehler können auch auftreten, während Daten aus der Quelle kopiert werden. Ein fehlgeschlagener Flussdurchgang enthält Informationen zu den Fehlern, die zum Fehlschlagen des Durchgangs beigetragen haben, einschließlich des Fehlers und der Beschreibung.

```json
[
  {
    "messages": [
      {
        "msgType": "eventNotification",
        "version": "1.0",
        "timestamp": 1597434157622,
        "imsOrgId": "{ORG_ID}",
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
          "imsOrgId": "{ORG_ID}",
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
| `fileInfo` | Eine URL, die zu einem Überblick über die Dateien führt, die sowohl erfolgreich als auch nicht erfolgreich erfasst wurden. |

>[!NOTE]
>
>Siehe [Anhang](#errors) für weitere Informationen zu Fehlermeldungen.

## Nächste Schritte

Sie können jetzt Ereignisse abonnieren, mit denen Sie Echtzeitbenachrichtigungen zum Status Ihrer Flussausführungen erhalten können. Weitere Informationen zu Flussausführungen und Quellen finden Sie unter [Quellen - Übersicht](./home.md).

## Anhang

Die folgenden Abschnitte enthalten zusätzliche Informationen zum Arbeiten mit Flussausführungsbenachrichtigungen.

### Fehlermeldungen verstehen {#errors}

Aufnahmefehler können auftreten, wenn Daten aus der Quelle kopiert werden oder wenn die kopierten Daten zu [!DNL Experience Platform] verarbeitet werden. Weitere Informationen zu bestimmten Fehlern finden Sie in der folgenden Tabelle.

| Fehler | Beschreibung |
| ---------- | ----------- |
| `CONNECTOR-1001-500` | Fehler beim Kopieren von Daten aus einer Quelle. |
| `CONNECTOR-2001-500` | Fehler beim Verarbeiten der kopierten Daten in [!DNL Experience Platform]. Dieser Fehler kann beim Analysieren, Validieren oder Transformieren auftreten. |
