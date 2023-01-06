---
keywords: Experience Platform;Startseite;beliebte Themen;Überwachen von Datenflüssen;Flow Service API;Flow Service
solution: Experience Platform
title: Überwachen von Datenflüssen mithilfe der Flow Service-API
type: Tutorial
description: In diesem Tutorial werden die Schritte zum Überwachen von Daten in Datenflüssen auf Vollständigkeit, Fehler und Metriken mithilfe der Flow Service-API beschrieben.
exl-id: c4b2db97-eba4-460d-8c00-c76c666ed70e
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 62%

---

# Überwachen von Datenflüssen mithilfe der Flow Service-API

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und zu verbessern. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken. Darüber hinaus ermöglicht Experience Platform die Aktivierung von Daten für externe Partner.

[!DNL Flow Service] wird verwendet, um Kundendaten aus verschiedenen Quellen innerhalb von Adobe Experience Platform zu sammeln und zu zentralisieren. Der Dienst bietet eine Benutzeroberfläche und eine RESTful-API, über die alle unterstützten Quellen und Ziele miteinander verbunden werden können.

In diesem Tutorial werden die Schritte zum Überwachen von Datenflüssen auf Vollständigkeit, Fehler und Metriken mithilfe der [[!DNL Flow Service API]](https://www.adobe.io/experience-platform-apis/references/flow-service/) beschrieben.

## Erste Schritte

Für dieses Tutorial benötigen Sie den ID-Wert eines Datenflusses. Wenn Sie keine gültige Datenfluss-ID haben, wählen Sie Ihren Connector aus der [Quellen - Übersicht](../../sources/home.md) oder [Ziele - Übersicht](../../destinations/catalog/overview.md) und führen Sie die Schritte aus, die vor dem Versuch dieses Tutorials beschrieben wurden.

Dieses Tutorial setzt außerdem ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Ziele](../../destinations/home.md): Ziele sind vordefinierte Integrationen mit häufig verwendeten Anwendungen, die die nahtlose Aktivierung von Daten aus Platform für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle ermöglichen.
- [Quellen](../../sources/home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

In den folgenden Abschnitten finden Sie zusätzliche Informationen, die Sie benötigen, um die Flussläufe mithilfe des [!DNL Flow Service] API.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform], einschließlich der Ressourcen, die zu [!DNL Flow Service] gehören, werden in bestimmten virtuellen Sandboxes isoliert. Bei allen Anfragen an [!DNL Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- `x-sandbox-name: {SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

- `Content-Type: application/json`

## Durchfluss überwachen

Nachdem Sie einen Datenfluss erstellt haben, führen Sie eine GET-Anfrage an die [!DNL Flow Service] API.

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
            "id": "65b7cfcc-6b2e-47c8-8194-13005b792752",
            "createdAt": 1607520228894,
            "updatedAt": 1607520276948,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "prod",
            "imsOrgId": "{ORG_ID}",
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
| `items` | Enthält eine einzige Payload von Metadaten, die mit Ihrer spezifischen Datenflussausführung verknüpft sind. |
| `metrics` | Die Eigenschaften der Daten im Fluss werden ausgeführt. |
| `activities` | Zeigt an, wie die Daten transformiert werden. |
| `durationSummary` | Die Start- und Endzeit des Flusslaufs. |
| `sizeSummary` | Die Datenmenge in Byte. |
| `recordSummary` | Die Datensatzanzahl der Daten. |
| `fileSummary` | Die Dateianzahl der Daten. |
| `fileSummary.extensions` | Enthält Informationen, die spezifisch für die Aktivität sind. Beispiel: `manifest` ist nur Teil der &quot;Promotion-Aktivität&quot;, daher ist sie in der `extensions` -Objekt. |
| `statusSummary` | Zeigt an, ob es sich bei der Flussausführung um einen Erfolg oder einen Fehler handelt. |

## Nächste Schritte

Mit diesem Tutorial haben Sie mithilfe der [!DNL Flow Service]-API Metriken und Fehlerinformationen zu Ihrem Datenfluss abgerufen. Sie können jetzt Ihren Datenfluss entsprechend Ihrem Datenaufnahme-Zeitplan überwachen, um dessen Status und Aufnahmeraten zu verfolgen. Informationen zum Überwachen von Datenflüssen auf Quellen finden Sie im Abschnitt [Überwachen von Datenflüssen für Quellen mithilfe der Benutzeroberfläche](../ui/monitor-sources.md) Tutorial. Weitere Informationen zum Überwachen von Datenflüssen für Ziele finden Sie im Abschnitt [Überwachen von Datenflüssen für Ziele mithilfe der Benutzeroberfläche](../ui/monitor-destinations.md) Tutorial.
