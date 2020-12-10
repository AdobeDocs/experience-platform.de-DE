---
keywords: Experience Platform;home;popular topics;monitor dataflows;flow service api;Flow Service
solution: Experience Platform
title: Überwachen von Flüssen und Ausgängen
topic: overview
type: Tutorial
description: In diesem Lernprogramm werden die Schritte zur Überwachung von Flusslaufdaten auf Vollständigkeit, Fehler und Metriken mithilfe der Flow Service API beschrieben.
translation-type: tm+mt
source-git-commit: 3fb5879ea636d4059a6b42e2f98742ff7df0397c
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 20%

---


# Überwachen von Datenflüssen mithilfe der Flow Service API

Adobe Experience Platform allows data to be ingested from external sources while providing you with the ability to structure, label, and enhance incoming data using [!DNL Platform] services. Daten können aus verschiedensten Quellen erfasst werden, darunter etwa Adobe-Anwendungen, Cloud-basierte Datenspeicher und Datenbanken. Darüber hinaus ermöglicht die Experience Platform die Aktivierung von Daten an externe Partner.

[!DNL Flow Service] wird zur Erfassung und Zentralisierung von Kundendaten aus unterschiedlichen Quellen innerhalb von Adobe Experience Platform verwendet. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen und Ziele verbunden werden können.

In diesem Lernprogramm werden die Schritte zum Überwachen von Flusslaufdaten auf Vollständigkeit, Fehler und Metriken mit dem [[!DNL Flow Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)Operator beschrieben.

## Erste Schritte

Für dieses Lernprogramm müssen Sie über den ID-Wert eines gültigen Datenflusses verfügen. Wenn Sie über keine gültige DataFlow-ID verfügen, wählen Sie den gewünschten Connector aus der Übersicht über die [Quellen](../../sources/home.md) oder [Ziele aus und befolgen Sie die Schritte, die vor dem Versuch dieses Lernprogramms beschrieben werden](../../destinations/catalog/overview.md) .

Für dieses Lernprogramm müssen Sie außerdem die folgenden Komponenten von Adobe Experience Platform kennen:

- [Ziele](../../destinations/home.md): Ziele sind vorgefertigte Integrationen mit häufig verwendeten Anwendungen, die die nahtlose Aktivierung von Daten von Platform für Cross-Kanal-Marketing-Kampagnen, E-Mail-Kampagnen, gezielte Werbung und viele andere Anwendungsfälle ermöglichen.
- [Quellen](../../sources/home.md): [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu verbessern.
- [Sandboxen](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

The following sections provide additional information that you will need to know in order to successfully monitor flow runs using the [!DNL Flow Service] API.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](../../tutorials/authentication.md) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to [!DNL Flow Service], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

- `x-sandbox-name: {SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

- `Content-Type: application/json`

## Monitorfluss

Nachdem Sie einen Datenflug durchgeführt haben, führen Sie eine GET an die [!DNL Flow Service] API durch.

**API-Format**

```http
GET /runs?property=flowId=={FLOW_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{FLOW_ID}` | Der eindeutige `id` Wert des zu überwachenden Datenflusses. |

**Anfrage**

Die folgende Anforderung ruft die Spezifikationen für einen vorhandenen Datendurchlauf ab.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==c9cef9cb-c934-4467-8ef9-cbc934546741' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt Details zu Ihrem Flusslauf zurück, einschließlich Informationen zum Erstellungsdatum, zu Quell- und Zielgruppe-Verbindungen sowie zur eindeutigen Kennung des Flusslaufs (`id`).

```json
{
    "items": [
        {
            "id": "65b7cfcc-6b2e-47c8-8194-13005b792752",
            "createdAt": 1607520228894,
            "updatedAt": 1607520276948,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "prod",
            "imsOrgId": "{IMS_ORG_ID}",
            "flowId": "f00c8762-df2f-432b-a7d7-38999fef5e8e",
            "etag": "\"560266dc-0000-0200-0000-5fd0d0140000\"",
            "metrics": {
                "durationSummary": {
                    "startedAtUTC": 1607520205922,
                    "completedAtUTC": 1607520262413
                },
                "sizeSummary": {
                    "inputBytes": 87885,
                    "outputBytes": 56730
                },
                "recordSummary": {
                    "inputRecordCount": 26758,
                    "outputRecordCount": 26758,
                    "failedRecordCount": 0
                },
                "fileSummary": {
                    "inputFileCount": 11,
                    "outputFileCount": 11,
                    "activityRefs": [
                        "37b34f84-1ada-11eb-adc1-0242ac120002"
                    ]
                },
                "statusSummary": {
                    "status": "success"
                }
            },
            "activities": [
                {
                    "id": "4f008a00-3a04-11eb-adc1-0242ac120002",
                    "name": "Copy Activity",
                    "updatedAtUTC": 0,
                    "durationSummary": {
                        "startedAtUTC": 1607520205922,
                        "completedAtUTC": 1607520236968
                    },
                    "sizeSummary": {
                        "inputBytes": 87885,
                        "outputBytes": 87885
                    },
                    "recordSummary": {
                        "inputRecordCount": 26758,
                        "outputRecordCount": 26758
                    },
                    "fileSummary": {
                        "inputFileCount": 11,
                        "outputFileCount": 11
                    },
                    "statusSummary": {
                        "status": "success"
                    }
                },
                {
                    "id": "37b34f84-1ada-11eb-adc1-0242ac120002",
                    "name": "Promotion Activity",
                    "updatedAtUTC": 0,
                    "durationSummary": {
                        "startedAtUTC": 1607520244985,
                        "completedAtUTC": 1607520262413
                    },
                    "sizeSummary": {
                        "inputBytes": 26758,
                        "outputBytes": 56730
                    },
                    "recordSummary": {
                        "inputRecordCount": 26758,
                        "outputRecordCount": 26758,
                        "failedRecordCount": 0
                    },
                    "fileSummary": {
                        "inputFileCount": 11,
                        "outputFileCount": 2,
                        "extensions": {
                            "manifest": {
                                "fileInfo": "https://platform.adobe.io/data/foundation/export/batches/01ES3TRN69E9W2DZ770XCGYAH1/meta?path=input_files",
                                "pathPrefix": "bucket1/csv_test/"
                            }
                        }
                    },
                    "statusSummary": {
                        "status": "success"
                    }
                }
            ]
        }
    ]
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `items` | Enthält eine einzige Nutzlast von Metadaten, die mit Ihrer spezifischen Flussausführung verknüpft sind. |
| `metrics` | Die Eigenschaften der Daten im Fluss werden ausgeführt. |
| `activities` | Zeigt, wie die Daten transformiert werden. |
| `durationSummary` | Beginn und Endzeit des Flusses. |
| `sizeSummary` | Die Datenmenge in Byte. |
| `recordSummary` | Die Datensatzzählung der Daten. |
| `fileSummary` | Die Datei zählt die Daten. |
| `fileSummary.extensions` | Enthält Informationen, die für die Aktivität spezifisch sind. Beispielsweise `manifest` ist sie nur Teil der &quot;Promotion-Aktivität&quot;und wird daher in das `extensions` Objekt einbezogen. |
| `statusSummary` | Zeigt an, ob es sich bei der Ausführung des Flusses um einen Erfolg oder einen Fehler handelt. |

## Nächste Schritte

In diesem Lernprogramm haben Sie mithilfe der [!DNL Flow Service] API Metriken und Fehlerinformationen zu Ihrem Datendurchlauf abgerufen. Sie können jetzt Ihren Datenflug abhängig von Ihrem Aufnahmeplan weiter überwachen, um dessen Status und die Erfassungsraten zu verfolgen. Informationen zum Überwachen von Datenflüssen auf Quellen finden Sie in den [Überwachungsdatenflüssen für Quellen, die Sie mithilfe des Lernprogramms &quot;Benutzeroberfläche](../ui/monitor-sources.md) &quot;verwenden. Weitere Informationen zum Überwachen von Datenflüssen nach Zielen finden Sie in den [Überwachen von Datenflüssen für Ziele im Lernprogramm der Benutzeroberfläche](../ui/monitor-destinations.md) .