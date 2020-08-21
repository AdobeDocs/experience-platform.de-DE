---
keywords: Experience Platform;home;popular topics; notifications
description: Mit den Adobe-I/O-Ereignissen können Sie Ereignis abonnieren und Webhooks verwenden, um Benachrichtigungen über den Status Ihrer Flussläufe zu erhalten. Diese Benachrichtigungen enthalten Informationen zum Erfolg Ihrer Flussausführung oder zu Fehlern, die zum Fehlschlagen einer Ausführung beigetragen haben.
solution: Experience Platform
title: Flusslaufbenachrichtigungen
topic: overview
translation-type: tm+mt
source-git-commit: b5b785d8415c15e3acb9e1155811a66c51477717
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 4%

---


# Flusslaufbenachrichtigungen

Adobe Experience Platform allows data to be ingested from external sources while providing you with the ability to structure, label, and enhance incoming data using [!DNL Platform] services. Daten können aus verschiedensten Quellen erfasst werden, darunter etwa Adobe-Anwendungen, Cloud-basierte Datenspeicher und Datenbanken.

[[!DNL Adobe Experience Platform Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) dient zur Erfassung und Zentralisierung von Kundendaten aus verschiedenen Quellen innerhalb [!DNL Platform]. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

Mit Adobe-I/O-Ereignissen können Sie Ereignis abonnieren und Webhooks verwenden, um Benachrichtigungen über den Status Ihrer Flussläufe zu erhalten. Diese Benachrichtigungen enthalten Informationen zum Erfolg Ihrer Flussausführung oder zu Fehlern, die zum Fehlschlagen einer Ausführung beigetragen haben.

In diesem Dokument wird beschrieben, wie Sie Ereignis abonnieren, Webhooks registrieren und Benachrichtigungen mit Informationen zum Status Ihrer Flussläufe erhalten.

## Erste Schritte

Dieses Dokument erfordert ein funktionierendes Verständnis der folgenden Komponenten von Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Experience Platform] organisiert werden.
* [[!DNL Echtzeit-Profil]](../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
* [[!DNL Adobe Experience Platform-Datenaufnahme]](../ingestion/home.md): [!DNL Data Ingestion] stellt die verschiedenen Methoden dar, mit denen Daten aus diesen Quellen [!DNL Platform] erfasst werden, sowie die Art und Weise, wie diese Daten innerhalb der [!DNL Data Lake] zur Verwendung durch nachgelagerte [!DNL Platform] Dienste beibehalten werden.

Dieses Dokument erfordert auch ein funktionierendes Verständnis von Webhooks und wie ein Webhaken von einer Anwendung zur anderen verbunden werden kann. Weitere Informationen zu Webhooks finden Sie in der folgenden [Dokumentation](https://requestbin.com/blog/working-with-webhooks/) .

## Registrieren Sie Ihren Webhaken

Um Benachrichtigungen über den Status Ihrer Flusslaufzeit zu erhalten, müssen Sie einen Webhaken registrieren, indem Sie eine eindeutige WebHook-URL als Teil Ihrer Ereignis-Registrierungsdetails angeben. Um eine Verbindung zu Ihrem [!DNL I/O Events] Abonnement herzustellen, besuchen Sie den [Webgehackdienst](https://webhook.site/) und kopieren Sie die angegebene eindeutige URL.

![Webhaken](./images/notifications/webhook-url.png)

## Ereignisse abonnieren

Nachdem Sie eine eindeutige Webshaken-URL erworben haben, gehen Sie zu den [Adobe-E/A-Ereignissen](https://www.adobe.io/apis/experienceplatform/events.html) und befolgen Sie die Schritte, die im Dokument mit [Dateneingabebenachrichtigungen](../ingestion/quality/subscribe-events.md) beschrieben sind, um Beginn zu kontaktieren, die Ereignis abonnieren.

>[!IMPORTANT]
>Stellen Sie während des Abonnements sicher, dass Sie Benachrichtigungen als Ereignis-Provider auswählen und die folgenden Ereignis-Abonnement auswählen: [!DNL Platform]
>
>* **[!UICONTROL Flusslauf der Experience Platform-Quelle erfolgreich]**
>* **[!UICONTROL Flusslauf der Experience Platform fehlgeschlagen]**

>
>
Wenn Sie aufgefordert werden, eine Webhook-Adresse anzugeben, verwenden Sie die zuvor erworbene WebHook-URL.

## Benachrichtigungen über Flusslaufvorgänge empfangen

Wenn Ihr WebHook angeschlossen ist und Ihr Ereignis-Abonnement abgeschlossen ist, können Sie Beginn, die Flusslaufbenachrichtigungen empfangen, über das WebHook-Dashboard ausführen.

Eine Benachrichtigung gibt Informationen wie die Anzahl der ausgeführten Erfassungsaufträge, die Dateigröße und Fehler zurück. Eine Benachrichtigung gibt auch eine Nutzlast zurück, die mit Ihrer Flussausführung im JSON-Format verknüpft ist. Die Antwortnutzlast kann entweder als `sources_flow_run_success` oder `sources_flow_run_failure`klassifiziert werden.

>[!IMPORTANT]
>Wenn die teilweise Erfassung während des Prozesses der Flusserstellung aktiviert ist, wird ein Fluss, der sowohl erfolgreiche als auch fehlgeschlagene Einträge enthält, `sources_flow_run_success` nur dann als markiert, wenn die Anzahl der Fehler unter dem Fehlerschwellenprozentsatz liegt, der während des Prozesses der Flusserstellung festgelegt wurde. Wenn eine erfolgreiche Flussausführung Fehler enthält, werden diese Fehler weiterhin als Teil der Rückgabeauslastung einbezogen.

### Erfolg

Eine erfolgreiche Antwort gibt eine Reihe von Antworten zurück, `metrics` die Eigenschaften eines bestimmten Flusslaufs definieren und `activities` die beschreiben, wie Daten transformiert werden.

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
| `metrics` | Definiert die Eigenschaften der Daten im Fluss. |
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
>Weitere Informationen zu Fehlermeldungen finden Sie im [Anhang](#errors) .

## Nächste Schritte

Sie können jetzt Ereignis abonnieren, mit denen Sie Echtzeitbenachrichtigungen zu den Status Ihrer Flusslaufvorgänge erhalten können. Weitere Informationen zu Flussläufen und -quellen finden Sie in der [Quellenübersicht](./home.md).

## Anhang

Die folgenden Abschnitte enthalten zusätzliche Informationen zum Arbeiten mit Flusslaufbenachrichtigungen.

### Fehlermeldungen {#errors}

Ingestion-Fehler können auftreten, wenn Daten aus der Quelle kopiert werden oder wenn die kopierten Daten verarbeitet werden zu [!DNL Platform]. Weitere Informationen zu bestimmten Fehlern finden Sie in der unten stehenden Tabelle.

| Fehler | Beschreibung |
| ---------- | ----------- |
| `CONNECTOR-1001-500` | Beim Kopieren von Daten aus einer Quelle ist ein Fehler aufgetreten. |
| `CONNECTOR-2001-500` | Während der Verarbeitung kopierter Daten zu [!DNL Platform]ist ein Fehler aufgetreten. Dieser Fehler kann bei der Analyse, Validierung oder Transformation auftreten. |
