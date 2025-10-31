---
solution: Experience Platform
title: API-Endpunkt für Segmentaufträge
description: Mit dem Segmentauftrags-Endpunkt in der Segmentierungs-Service-API von Adobe Experience Platform können Sie Segmentaufträge für Ihr Unternehmen programmgesteuert verwalten.
role: Developer
exl-id: 105481c2-1c25-4f0e-8fb0-c6577a4616b3
source-git-commit: 83a249daddbee1ec264b6e505517325c76ac9b09
workflow-type: tm+mt
source-wordcount: '1232'
ht-degree: 18%

---

# Segmentauftrags-Endpunkt

Ein Segmentauftrag ist ein asynchroner Prozess, der bei Bedarf ein Zielgruppensegment erstellt. Es verweist auf [Segmentdefinition](./segment-definitions.md) sowie auf alle [Zusammenführungsrichtlinien](../../profile/api/merge-policies.md) die steuern, wie [!DNL Real-Time Customer Profile] überlappende Attribute über Ihre Profilfragmente hinweg zusammenführt. Nach erfolgreichem Abschluss eines Segmentauftrags können Sie verschiedene Informationen über das Segment sammeln, z. B. Fehler, die bei der Verarbeitung aufgetreten sind, oder die endgültige Größe Ihrer Zielgruppe.

Dieses Handbuch enthält Informationen zum besseren Verständnis von Segmentaufträgen und umfasst Beispiel-API-Aufrufe zum Ausführen grundlegender Aktionen mit der API.

## Erste Schritte

Die in diesem Handbuch verwendeten Endpunkte sind Teil der [!DNL Adobe Experience Platform Segmentation Service]-API. Bevor Sie fortfahren, lesen Sie den Abschnitt [Erste Schritte](./getting-started.md). Dort erhalten Sie wichtige Informationen darüber, wie Sie die API aufrufen und die erforderlichen Kopfzeilen sowie Beispiele für API-Aufrufe lesen können.

## Liste mit Segmentaufträgen abrufen {#retrieve-list}

Sie können eine Liste aller Segmentaufträge für Ihr Unternehmen abrufen, indem Sie eine GET-Anfrage an den `/segment/jobs`-Endpunkt senden.

**API-Format**

Der `/segment/jobs`-Endpunkt unterstützt verschiedene Abfrageparameter, mit denen Sie Ihre Ergebnisse filtern können. Obwohl diese Parameter optional sind, wird ihre Verwendung dringend empfohlen, um kostspieligen Aufwand zu reduzieren. Wenn Sie diesen Endpunkt ohne Parameter aufrufen, werden alle für Ihre Organisation verfügbaren Exportaufträge abgerufen. Es können mehrere Parameter eingeschlossen werden, die durch kaufmännische Und-Zeichen (`&`) voneinander getrennt werden.

```http
GET /segment/jobs
GET /segment/jobs?{QUERY_PARAMETERS}
```

**Abfrageparameter**

+++ Eine Liste der verfügbaren Abfrageparameter.

| Parameter | Beschreibung | Beispiel |
| --------- | ----------- | ------- |
| `start` | Gibt den Startversatz für die zurückgegebenen Segmentaufträge an. | `start=1` |
| `limit` | Gibt die Anzahl der pro Seite zurückgegebenen Segmentaufträge an. | `limit=20` |
| `status` | Filtert die Ergebnisse anhand ihres Status. Unterstützte Werte sind „NEW“ (neu), „QUEUED“ (in Warteschlange), „PROCESSING“ (Verarbeitung läuft), „SUCCEEDED“ (erfolgreich abgeschlossen), „FAILED“ (fehlgeschlagen), „CANCELLING“ (wird abgebrochen) und „CANCELLED“ (abgebrochen). | `status=NEW` |
| `sort` | Bestellt die zurückgegebenen Segmentaufträge. | Wird im Format `[attributeName]:[desc\|asc]` geschrieben. `sort=creationTime:desc` |
| `property` | Filtert Segmentaufträge und erhält genaue Übereinstimmungen für den angegebenen Filter. Das kann in einem der folgenden Formate geschrieben sein: <ul><li>`[jsonObjectPath]==[value]` – Filtern nach dem Objektschlüssel</li><li>`[arrayTypeAttributeName]~[objectKey]==[value]` – Filtern innerhalb des Arrays</li></ul> | `property=segments~segmentId==workInUS` |

+++

**Anfrage**

+++ Eine Beispielanfrage zum Anzeigen einer Liste von Segmentvorgängen.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs?status=SUCCEEDED \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status-Code 200 mit einer Liste von Segmentvorgängen für die angegebene Organisation als JSON zurück. Eine vollständige Liste aller Segmentdefinitionen wird innerhalb des `children.segments` angezeigt.

>[!NOTE]
>
>Die folgende Antwort wurde aus Platzgründen gekürzt und zeigt nur den ersten zurückgegebenen Auftrag an.

+++ Eine Beispielantwort beim Abrufen einer Liste von Segmentvorgängen. 

```json
{
    "_page": {
        "totalCount": 14,
        "pageSize": 14
    },
    "children": [
        {
            "id": "b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "profileInstanceId": "ups",
            "source": "scheduler",
            "status": "SUCCEEDED",
            "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
            "computeJobId": 8811,
            "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
            "segments": [
                {
                    "segmentId": "30230300-ccf1-48ad-8012-c5563a007069",
                    "segment": {
                        "id": "30230300-ccf1-48ad-8012-c5563a007069",
                        "expression": {
                            "type": "PQL",
                            "format": "pql/json",
                            "value": "{PQL_EXPRESSION}"
                        },
                        "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                        "mergePolicy": {
                            "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                            "version": 1
                        }
                    }
                }
            ],
            "metrics": {
                "totalTime": {
                    "startTimeInMs": 1573203617195,
                    "endTimeInMs": 1573204395655,
                    "totalTimeInMs": 778460
                },
                "profileSegmentationTime": {
                    "startTimeInMs": 1573204266727,
                    "endTimeInMs": 1573204395655,
                    "totalTimeInMs": 128928
                },
                "totalProfiles":13146432,
                "segmentedProfileCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":1033
                },
                "segmentedProfileByNamespaceCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":{
                        "tenantiduserobjid":1033,
                        "campaign_profile_mscom_mkt_prod2":1033
                    }
                },
                "segmentedProfileByStatusCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":{
                        "exited":144646,
                        "realized":2056
                    }
                },
                "totalProfilesByMergePolicy":{
                    "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
                }
            },
            "requestId": "4e538382-dbd8-449e-988a-4ac639ebe72b-1573203600264",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "properties": {
                "scheduleId": "4e538382-dbd8-449e-988a-4ac639ebe72b",
                "runId": "e6c1308d-0d4b-4246-b2eb-43697b50a149"
            },
            "_links": {
                "cancel": {
                    "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
                    "method": "DELETE"
                },
                "checkStatus": {
                    "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
                    "method": "GET"
                }
            },
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        }
    ],
    "_links": {
        "next": {}
    }
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `id` | Eine systemgenerierte schreibgeschützte Kennung für den Segmentauftrag. |
| `status` | Der aktuelle Status für den Segmentauftrag. Zu den möglichen Statuswerten gehören „NEU“, „VERARBEITUNG LÄUFT“, „ABBRUCH“, „ABGEBROCHEN“, „FEHLGESCHLAGEN“ und „ERFOLGREICH“. |
| `segments` | Ein -Objekt, das Informationen zu den Segmentdefinitionen enthält, die im Segmentauftrag zurückgegeben werden. |
| `segments.segment.id` | Die ID der Segmentdefinition. |
| `segments.segment.expression` | Ein -Objekt, das Informationen zum Ausdruck der Segmentdefinition enthält, der in PQL geschrieben wurde. |
| `metrics` | Ein Objekt, das Diagnoseinformationen zum Segmentauftrag enthält. |
| `metrics.totalTime` | Ein -Objekt, das Informationen zu den Zeiten enthält, zu denen der Segmentierungsauftrag gestartet und beendet wurde, sowie zur insgesamt benötigten Zeit. |
| `metrics.profileSegmentationTime` | Ein -Objekt, das Informationen zu den Zeiten enthält, zu denen die Segmentierungsauswertung begonnen und beendet hat, sowie zur insgesamt benötigten Zeit. |
| `metrics.segmentProfileCounter` | Die Anzahl der qualifizierten Profile auf Segmentbasis. |
| `metrics.segmentedProfileByNamespaceCounter` | Die Anzahl der Profile, die für jeden Identity-Namespace auf Basis einer Segmentdefinition qualifiziert sind. |
| `metrics.segmentProfileByStatusCounter` | Die Anzahl der Profile für jeden Status. Die folgenden drei Status werden unterstützt: <ul><li>„realized“ - die Anzahl der Profile, die für die Segmentdefinition qualifiziert sind.</li><li>„exited“ : Die Anzahl der Profile, die nicht mehr in der Segmentdefinition vorhanden sind.</li></ul> |
| `metrics.totalProfilesByMergePolicy` | Die Gesamtzahl der zusammengeführten Profile pro Zusammenführungsrichtlinie. |

+++

## Neuen Segmentauftrag erstellen {#create}

Sie können einen neuen Segmentauftrag erstellen, indem Sie eine POST-Anfrage an den `/segment/jobs`-Endpunkt senden und die IDs der Segmentdefinition in den Anfragetext aufnehmen.

**API-Format**

```http
POST /segment/jobs
```

**Anfrage**

+++Beispielanfrage zum Erstellen eines neuen Segmentauftrags

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '[
    {
        "segmentId": "7863c010-e092-41c8-ae5e-9e533186752e"
    },
    {
        "segmentId": "07d39471-05d1-4083-a310-d96978fd7c85"
    }
 ]'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `segmentId` | Die ID der Segmentdefinition, die Sie auswerten möchten. Diese Segmentdefinitionen können zu verschiedenen Zusammenführungsrichtlinien gehören. Weitere Informationen zu Segmentdefinitionen finden Sie im [Handbuch zum Segmentdefinitionenendpunkt](./segment-definitions.md). |

+++

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit Informationen zu Ihrem neu erstellten Segmentauftrag zurückgegeben.

+++ Eine Beispielantwort beim Erstellen eines neuen Segmentauftrags.

```json
{
    "id": "b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
    "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "scheduler",
    "status": "PROCESSING",
    "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
    "computeJobId": 8811,
    "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
    "segments": [
        {
            "segmentId": "7863c010-e092-41c8-ae5e-9e533186752e",
            "segment": {
                "id": "7863c010-e092-41c8-ae5e-9e533186752e",
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                "mergePolicy": {
                    "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                    "version": 1
                }
            }
        },
        {
            "segmentId": "07d39471-05d1-4083-a310-d96978fd7c85",
            "segment": {
                "id": "07d39471-05d1-4083-a310-d96978fd7c85",
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                "mergePolicy": {
                    "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                    "version": 1
                }
            }
        }
    ],
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1573203617195,
            "endTimeInMs": 1573204395655,
            "totalTimeInMs": 778460
        },
        "profileSegmentationTime": {
            "startTimeInMs": 1573204266727,
            "endTimeInMs": 1573204395655,
            "totalTimeInMs": 128928
        },
        "segmentedProfileCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":1033
        },
        "segmentedProfileByNamespaceCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "tenantiduserobjid":1033,
                "campaign_profile_mscom_mkt_prod2":1033
            }
        },
        "segmentedProfileByStatusCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "exited":144646,
                "realized":2056
            }
        },
        "totalProfiles":13146432,
        "totalProfilesByMergePolicy":{
            "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
        }
    },
    "requestId": "4e538382-dbd8-449e-988a-4ac639ebe72b-1573203600264",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "properties": {
        "scheduleId": "4e538382-dbd8-449e-988a-4ac639ebe72b",
        "runId": "e6c1308d-0d4b-4246-b2eb-43697b50a149"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "method": "GET"
        }
    },
    "updateTime": 1573204395000,
    "creationTime": 1573203600535,
    "updateEpoch": 1573204395
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `id` | Eine systemgenerierte schreibgeschützte Kennung für den neu erstellten Segmentauftrag. |
| `status` | Der aktuelle Status für den Segmentauftrag. Da der Segmentvorgang neu erstellt wurde, ist der Status immer „NEU“. |
| `segments` | Ein -Objekt, das Informationen zu den Segmentdefinitionen enthält, für die dieser Segmentauftrag ausgeführt wird. |
| `segments.segment.id` | Die ID der von Ihnen angegebenen Segmentdefinition. |
| `segments.segment.expression` | Ein -Objekt, das Informationen zum Ausdruck der Segmentdefinition enthält, der in PQL geschrieben wurde. |

+++

## Bestimmten Segmentauftrag abrufen {#get}

Sie können detaillierte Informationen zu einem bestimmten Segmentauftrag abrufen, indem Sie eine GET-Anfrage an den `/segment/jobs`-Endpunkt senden und im Anfragepfad die ID des Segmentauftrags angeben, den Sie abrufen möchten.

**API-Format**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | Der `id`-Wert des Segmentauftrags, den Sie abrufen möchten. |

**Anfrage**

+++ Eine Beispielanfrage zum Abrufen eines Segmentauftrags.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status-Code 200 mit detaillierten Informationen zum angegebenen Segmentauftrag zurück. Eine vollständige Liste aller Segmentdefinitionen wird innerhalb des `children.segments` angezeigt.

+++ Eine Beispielantwort zum Abrufen eines Segmentauftrags.

```json
{
    "id": "d3b4a50d-dfea-43eb-9fca-557ea53771fd",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "api",
    "status": "SUCCEEDED",
    "batchId": "651fc109-3963-48d2-aa98-9e3cc2003bac",
    "computeJobId": 39312,
    "computeGatewayJobId": "a0099ab6-11ab-4c2b-a0ea-6162e16806bd",
    "segments": [
        {
            "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
            "segment": {
                "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                "mergePolicy": {
                    "id": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                    "version": 1
                }
            }
        }
    ],
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1579304313411
        },
        "profileSegmentationTime": {}
    },
    "requestId": "Hw1jdAHeuWHVKVxcAPFrLCbbjkriDl9v",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "GET"
        }
    },
    "updateTime": 1579304339000,
    "creationTime": 1579304260897,
    "updateEpoch": 1579304339
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `id` | Eine systemgenerierte schreibgeschützte Kennung für den Segmentauftrag. |
| `status` | Der aktuelle Status für den Segmentauftrag. Zu den möglichen Statuswerten gehören „NEU“, „VERARBEITUNG LÄUFT“, „ABBRUCH“, „ABGEBROCHEN“, „FEHLGESCHLAGEN“ und „ERFOLGREICH“. |
| `segments` | Ein -Objekt, das Informationen zu den Segmentdefinitionen enthält, die im Segmentauftrag zurückgegeben werden. |
| `segments.segment.id` | Die ID der Segmentdefinition. |
| `segments.segment.expression` | Ein -Objekt, das Informationen zum Ausdruck der Segmentdefinition enthält, der in PQL geschrieben wurde. |
| `metrics` | Ein Objekt, das Diagnoseinformationen zum Segmentauftrag enthält. |

+++

>[!ENDTABS]

## Massenabruf von Segmentaufträgen {#bulk-get}

Sie können detaillierte Informationen zu mehreren Segmentvorgängen abrufen, indem Sie eine POST-Anfrage an den `/segment/jobs/bulk-get`-Endpunkt senden und die `id` Werte der Segmentvorgänge im Anfragetext angeben.

**API-Format**

```http
POST /segment/jobs/bulk-get
```

**Anfrage**

+++ Eine Beispielanfrage für die Verwendung des Massenabruf-Endpunkts.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "ids": [
            {
                "id": "cc3419d3-0389-47f1-b174-fead6b3c830d"
            },
            {
                "id": "c527dc3f-07fe-4b96-be4e-23f38e734ff8"
            }
        ]
    }'
```

+++

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 207 mit den angeforderten Segmentvorgängen zurückgegeben.

>[!NOTE]
>
>Die folgende Antwort wurde aus Platzgründen gekürzt und zeigt nur teilweise Details zu jedem Segmentvorgang an. In der vollständigen Antwort werden die vollständigen Details für die angeforderten Segmentvorgänge aufgelistet.

+++ Eine Beispielantwort bei Verwendung der Massen-GET-Antwort.

```json
{
    "results": {
        "cc3419d3-0389-47f1-b174-fead6b3c830d": {
            "id": "cc3419d3-0389-47f1-b174-fead6b3c830d",
            "imsOrgId": "{ORG_ID}",
            "status": "SUCCEEDED",
            "segments": [
                {
                    "segmentId": "30230300-ccf1-48ad-8012-c5563a007069",
                    "segment": {
                        "id": "30230300-ccf1-48ad-8012-c5563a007069",
                        "expression": {
                            "type": "PQL",
                            "format": "pql/json",
                            "value": "{PQL_EXPRESSION}"
                        },
                        "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                        "mergePolicy": {
                            "id": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                            "version": 1
                        }
                    }
                }
            ],
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        },
        "c527dc3f-07fe-4b96-be4e-23f38e734ff8": {
            "id": "c527dc3f-07fe-4b96-be4e-23f38e734ff8",
            "imsOrgId": "{ORG_ID}",
            "status": "SUCCEEDED",
            "segments": [
                {
                    "segmentId": "30230300-d78c-48ad-8012-c5563a007069",
                    "segment": {
                        "id": "30230300-d78c-48ad-8012-c5563a007069",
                        "expression": {
                            "type": "PQL",
                            "format": "pql/json",
                            "value": "{PQL_EXPRESSION}"
                        },
                        "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                        "mergePolicy": {
                            "id": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                            "version": 1
                        }
                    }
                }
            ],
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        }
    }
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `id` | Eine systemgenerierte schreibgeschützte Kennung für den Segmentauftrag. |
| `status` | Der aktuelle Status für den Segmentauftrag. Zu den möglichen Statuswerten gehören „NEU“, „VERARBEITUNG LÄUFT“, „ABBRUCH“, „ABGEBROCHEN“, „FEHLGESCHLAGEN“ und „ERFOLGREICH“. |
| `segments` | Ein -Objekt, das Informationen zu den Segmentdefinitionen enthält, die im Segmentauftrag zurückgegeben werden. |
| `segments.segment.id` | Die ID der Segmentdefinition. |
| `segments.segment.expression` | Ein -Objekt, das Informationen zum Ausdruck der Segmentdefinition enthält, der in PQL geschrieben wurde. |

+++

## Bestimmten Segmentauftrag abbrechen oder löschen {#delete}

Sie können einen bestimmten Segmentauftrag löschen, indem Sie eine DELETE-Anfrage an den `/segment/jobs`-Endpunkt senden und im Anfragepfad die ID des Segmentauftrags angeben, den Sie löschen möchten.

>[!NOTE]
>
>Die API reagiert sofort auf die Löschanfrage. Das tatsächliche Löschen des Segmentauftrags erfolgt jedoch asynchron. Mit anderen Worten: Es besteht ein Zeitunterschied zwischen dem Zeitpunkt, zu dem die Löschanfrage an den Segmentauftrag gestellt wird, und dem Zeitpunkt, zu dem sie angewendet wird.

**API-Format**

```http
DELETE /segment/jobs/{SEGMENT_JOB_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | Der `id`-Wert des Segmentauftrags, den Sie löschen möchten. |

**Anfrage**

+++ Eine Beispielanfrage zum Löschen eines Segmentauftrags.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 mit einem leeren Antworttext zurück.

## Nächste Schritte

Nach dem Lesen dieses Handbuchs wissen Sie jetzt besser, wie Segmentvorgänge funktionieren.
