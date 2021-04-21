---
keywords: Experience Platform;Home;beliebte Themen; Benachrichtigungen
description: Durch das Abonnieren von Adobe I/O-Ereignissen können Sie Webhooks verwenden, um Benachrichtigungen über den Status Ihrer Quellverbindungen zu erhalten. Diese Benachrichtigungen enthalten Informationen zum Erfolg Ihrer Flussausführung oder zu Fehlern, die zum Fehlschlagen einer Ausführung beigetragen haben.
solution: Experience Platform
title: Flusslaufbenachrichtigungen
topic-legacy: overview
exl-id: 0f1cde97-3030-4b8e-be08-21f64e78b794
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 5%

---

# Flusslaufbenachrichtigungen

Adobe Experience Platform ermöglicht die Erfassung von Daten aus externen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von [!DNL Platform]-Diensten zu strukturieren, zu beschriften und zu verbessern. Daten können aus verschiedensten Quellen erfasst werden, darunter etwa Adobe-Anwendungen, Cloud-basierte Datenspeicher und Datenbanken.

[[!DNL Adobe Experience Platform Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) dient zur Erfassung und Zentralisierung von Kundendaten aus verschiedenen unterschiedlichen Quellen innerhalb  [!DNL Platform]. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

Mit Adobe I/O-Ereignissen können Sie Ereignis abonnieren und Webhooks verwenden, um Benachrichtigungen über den Status Ihrer Flussläufe zu erhalten. Diese Benachrichtigungen enthalten Informationen zum Erfolg Ihrer Flussausführung oder zu Fehlern, die zum Fehlschlagen einer Ausführung beigetragen haben.

In diesem Dokument wird beschrieben, wie Sie Ereignis abonnieren, Webhooks registrieren und Benachrichtigungen mit Informationen zum Status Ihrer Flussläufe erhalten.

## Erste Schritte

In diesem Lernprogramm wird davon ausgegangen, dass Sie bereits mindestens eine Quellverbindung erstellt haben, deren Fluss überwacht werden soll. Wenn Sie noch keine Quellverbindung konfiguriert haben, verwenden Sie den Beginn [sources overview](./home.md), um die Quelldatei Ihrer Wahl zu konfigurieren, bevor Sie zu diesem Handbuch zurückkehren.

Dieses Dokument erfordert auch ein funktionierendes Verständnis von Webhooks und wie ein Webhaken von einer Anwendung zur anderen verbunden werden kann. Eine Einführung zu Webhooks finden Sie in der [[!DNL I/O Events] Dokumentation](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md).

## WebHook für Flusslaufbenachrichtigungen registrieren

Um Benachrichtigungen über Flusslaufvorgänge zu erhalten, müssen Sie Adobe Developer Console verwenden, um einen Webshaken bei Ihrer [!DNL Experience Platform]-Integration zu registrieren.

Folgen Sie dem Tutorial [Abonnieren von [!DNL I/O Event] Benachrichtigungen](../observability/notifications/subscribe.md), um detaillierte Schritte dazu zu erhalten.

>[!IMPORTANT]
>
>Stellen Sie während des Abonnements sicher, dass Sie **[!UICONTROL Plattformbenachrichtigungen]** als Ereignis-Provider auswählen und die folgenden Ereignis-Abonnement auswählen:
>
>* **[!UICONTROL Flusslauf der Experience Platform-Quelle erfolgreich ausgeführt]**
>* **[!UICONTROL Flusslauf der Experience Platform fehlgeschlagen]**


## Benachrichtigungen über Flusslaufvorgänge empfangen

Wenn Ihr WebHook angeschlossen ist und Ihr Ereignis-Abonnement abgeschlossen ist, können Sie Beginn, die Flusslaufbenachrichtigungen empfangen, über das WebHook-Dashboard ausführen.

Eine Benachrichtigung gibt Informationen wie die Anzahl der ausgeführten Erfassungsaufträge, die Dateigröße und Fehler zurück. Eine Benachrichtigung gibt auch eine Nutzlast zurück, die mit Ihrer Flussausführung im JSON-Format verknüpft ist. Die Antwortnutzlast kann entweder als `sources_flow_run_success` oder `sources_flow_run_failure` klassifiziert werden.

>[!IMPORTANT]
>
>Wenn die teilweise Erfassung während des Prozesses der Flusserstellung aktiviert ist, wird ein Fluss, der sowohl erfolgreiche als auch fehlgeschlagene Einträge enthält, nur dann als `sources_flow_run_success` markiert, wenn die Anzahl der Fehler unter dem Fehlerschwellenprozentsatz liegt, der während des Prozesses der Flusserstellung festgelegt wurde. Wenn eine erfolgreiche Flussausführung Fehler enthält, werden diese Fehler weiterhin als Teil der Rückgabeauslastung einbezogen.

### Erfolg

Eine erfolgreiche Antwort gibt einen Satz von `metrics` zurück, der die Eigenschaften eines bestimmten Flusslaufs definiert, und `activities`, in dem beschrieben wird, wie Daten transformiert werden.

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
              "fileInfo": "https://platform-int.adobe.io/data/foundation/export/batches/01E4TSJNM2H5M74J0XB8MFWDHK/meta?path=input_files"
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
| `metrics` | Definiert die Eigenschaften der Daten in der Ausführung des Datenflusses. |
| `activities` | Definiert die verschiedenen Schritte und Aktivitäten, die zur Transformation der Daten durchgeführt werden. |
| `durationSummary` | Definiert den Beginn und die Endzeit der Flussausführung. |
| `sizeSummary` | Definiert die Datenmenge in Byte. |
| `recordSummary` | Definiert die Datensatzzählung der Daten. |
| `fileSummary` | Definiert die Dateianzahl der Daten. |
| `fileInfo` | Eine URL, die zu einem Überblick über die erfolgreich erfassten Dateien führt. |
| `statusSummary` | Definiert, ob die Ausführung des Flusses ein Erfolg oder ein Fehler ist. |

### Fehlgeschlagen

Die folgende Antwort ist ein Beispiel für einen fehlgeschlagenen Fluss, bei dem ein Fehler auftritt, während die kopierten Daten verarbeitet werden. Fehler können auch auftreten, wenn Daten aus der Quelle kopiert werden. Ein ausgefallener Flusslauf enthält Informationen zu den Fehlern, die zum Fehlschlagen des Vorgangs beigetragen haben, einschließlich Fehler und Beschreibung.

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
| `fileInfo` | Eine URL, die zu einem Überblick über die Dateien führt, die sowohl erfolgreich als auch erfolglos aufgenommen wurden. |

>[!NOTE]
>
>Weitere Informationen zu Fehlermeldungen finden Sie unter [Anhang](#errors).

## Nächste Schritte

Sie können jetzt Ereignis abonnieren, mit denen Sie Echtzeitbenachrichtigungen zu den Status Ihrer Flusslaufvorgänge erhalten können. Weitere Informationen zu Flussläufen und -quellen finden Sie unter [Quellübersicht](./home.md).

## Anhang

Die folgenden Abschnitte enthalten zusätzliche Informationen zum Arbeiten mit Flusslaufbenachrichtigungen.

### Fehlermeldungen {#errors}

Ingestion-Fehler können auftreten, wenn Daten aus der Quelle kopiert werden oder wenn die kopierten Daten nach [!DNL Platform] verarbeitet werden. Weitere Informationen zu bestimmten Fehlern finden Sie in der unten stehenden Tabelle.

| Fehler | Beschreibung |
| ---------- | ----------- |
| `CONNECTOR-1001-500` | Beim Kopieren von Daten aus einer Quelle ist ein Fehler aufgetreten. |
| `CONNECTOR-2001-500` | Während der Verarbeitung kopierter Daten zu [!DNL Platform] ist ein Fehler aufgetreten. Dieser Fehler kann bei der Analyse, Validierung oder Transformation auftreten. |
