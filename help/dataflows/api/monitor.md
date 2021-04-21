---
keywords: Experience Platform;Home;beliebte Themen;Überwachen von Datenflüssen;Flussdienst-API;Flussdienst
solution: Experience Platform
title: Überwachen von Datenflüssen mit der Flussdienst-API
topic-legacy: overview
type: Tutorial
description: In diesem Lernprogramm werden die Schritte zur Überwachung von Flusslaufdaten auf Vollständigkeit, Fehler und Metriken mithilfe der Flow Service API beschrieben.
exl-id: c4b2db97-eba4-460d-8c00-c76c666ed70e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 20%

---

# Überwachen von Datenflüssen mithilfe der Flow Service API

Adobe Experience Platform ermöglicht die Erfassung von Daten aus externen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von [!DNL Platform]-Diensten zu strukturieren, zu beschriften und zu verbessern. Daten können aus verschiedensten Quellen erfasst werden, darunter etwa Adobe-Anwendungen, Cloud-basierte Datenspeicher und Datenbanken. Darüber hinaus ermöglicht die Experience Platform die Aktivierung von Daten an externe Partner.

[!DNL Flow Service] wird zur Erfassung und Zentralisierung von Kundendaten aus unterschiedlichen Quellen innerhalb von Adobe Experience Platform verwendet. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen und Ziele verbunden werden können.

In diesem Lernprogramm werden die Schritte zum Überwachen von Flusslaufdaten auf Vollständigkeit, Fehler und Metriken mit dem [[!DNL Flow Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) beschrieben.

## Erste Schritte

Für dieses Lernprogramm müssen Sie über den ID-Wert eines gültigen Datenflusses verfügen. Wenn Sie keine gültige DataFlow-ID haben, wählen Sie den gewünschten Connector aus dem [sources overview](../../sources/home.md) oder [destination overview](../../destinations/catalog/overview.md) und befolgen Sie die Schritte, die vor dem Versuch dieses Lernprogramms beschrieben werden.

Für dieses Lernprogramm müssen Sie außerdem die folgenden Komponenten von Adobe Experience Platform kennen:

- [Ziele](../../destinations/home.md): Ziele sind vorgefertigte Integrationen mit häufig verwendeten Anwendungen, die die nahtlose Aktivierung von Daten von Platform für Cross-Kanal-Marketing-Kampagnen, E-Mail-Kampagnen, gezielte Werbung und viele andere Anwendungsfälle ermöglichen.
- [Quellen](../../sources/home.md):  [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von  [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu verbessern.
- [Sandboxen](../../sandboxes/home.md):  [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne  [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie zur erfolgreichen Überwachung von Flussläufen mit der API [!DNL Flow Service] kennen müssen.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Fehlerbehebungshandbuch für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://www.adobe.com/go/platform-api-authentication-en) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform], einschließlich derjenigen, die zu [!DNL Flow Service] gehören, werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an [!DNL Platform]-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird in:

- `x-sandbox-name: {SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

- `Content-Type: application/json`

## Monitorfluss

Nachdem Sie einen Datenflug durchgeführt haben, führen Sie eine GET an die API [!DNL Flow Service] aus.

**API-Format**

```http
GET /runs?property=flowId=={FLOW_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{FLOW_ID}` | Der eindeutige Wert `id` für den Datendurchlauf, den Sie überwachen möchten. |

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
| `fileSummary.extensions` | Enthält Informationen, die für die Aktivität spezifisch sind. `manifest` ist beispielsweise nur Teil der &quot;Promotion-Aktivität&quot;und ist daher im `extensions`-Objekt enthalten. |
| `statusSummary` | Zeigt an, ob es sich bei der Ausführung des Flusses um einen Erfolg oder einen Fehler handelt. |

## Nächste Schritte

In diesem Lernprogramm haben Sie mithilfe der API [!DNL Flow Service] Metriken und Fehlerinformationen zu Ihrem Datendurchlauf abgerufen. Sie können jetzt Ihren Datenflug abhängig von Ihrem Aufnahmeplan weiter überwachen, um dessen Status und die Erfassungsraten zu verfolgen. Informationen zum Überwachen von Datenflüssen auf Quellen finden Sie im Lehrgang [Überwachungsdataflows für Quellen, das die Benutzeroberfläche](../ui/monitor-sources.md) verwendet. Weitere Informationen zum Überwachen von Datenflüssen nach Zielen finden Sie im Lehrgang [Überwachung von Datenflüssen für Ziele mithilfe der Benutzeroberfläche](../ui/monitor-destinations.md).
