---
keywords: Experience Platform;Home;beliebte Themen;Segmentierung;Segmentierung;Segmentierungsdienst;Segmentaufträge;Segmentauftrag;API;API;
solution: Experience Platform
title: API-Endpunkt für Segmentaufträge
topic-legacy: developer guide
description: Mit dem Segmentauftragsendpunkt in der Adobe Experience Platform Segmentation Service API können Sie Segmentaufträge programmgesteuert für Ihr Unternehmen verwalten.
exl-id: 105481c2-1c25-4f0e-8fb0-c6577a4616b3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 32%

---

# Endpunkt für Segmentaufträge

Ein Segmentauftrag ist ein asynchroner Vorgang, bei dem ein neues Zielgruppensegment erstellt wird. Er verweist auf eine [Segmentdefinition](./segment-definitions.md) sowie alle [Mergerichtlinien](../../profile/api/merge-policies.md), die steuern, wie [!DNL Real-time Customer Profile] überlappende Profil-Fragmente zusammenführt. Nach erfolgreichem Abschluss eines Segmentauftrags können Sie verschiedene Informationen über das Segment sammeln, z. B. Fehler, die bei der Verarbeitung aufgetreten sind, oder die endgültige Größe Ihrer Zielgruppe.

Dieses Handbuch enthält Informationen zum besseren Verständnis von Segmentaufträgen und umfasst Beispiel-API-Aufrufe zum Ausführen grundlegender Aktionen mit der API.

## Erste Schritte

Die in diesem Handbuch verwendeten Endpunkte sind Teil der API [!DNL Adobe Experience Platform Segmentation Service]. Bevor Sie fortfahren, lesen Sie bitte im Handbuch [Erste Schritte](./getting-started.md) nach wichtigen Informationen, die Sie kennen müssen, um die API erfolgreich aufzurufen, einschließlich erforderlicher Kopfzeilen und Anleitungen zum Lesen von Beispiel-API-Aufrufen.

## Liste mit Segmentaufträgen abrufen {#retrieve-list}

Sie können eine Liste aller Segmentaufträge für Ihre IMS-Organisation abrufen, indem Sie eine GET-Anfrage an den `/segment/jobs`-Endpunkt richten.

**API-Format**

Der `/segment/jobs`-Endpunkt unterstützt mehrere Abfragen-Parameter, um die Ergebnisse zu filtern. Diese Parameter sind optional, ihre Verwendung wird jedoch dringend empfohlen, um den kostspieligen Aufwand zu reduzieren. Wenn Sie diesen Endpunkt ohne Parameter aufrufen, werden alle für Ihre Organisation verfügbaren Exportaufträge abgerufen. Es können mehrere Parameter eingeschlossen werden, die durch kaufmännische Und-Zeichen (`&`) voneinander getrennt werden.

```http
GET /segment/jobs
GET /segment/jobs?{QUERY_PARAMETERS}
```

**Abfrageparameter**

| Parameter | Beschreibung | Beispiel |
| --------- | ----------- | ------- |
| `start` | Gibt den Startversatz für die zurückgegebenen Segmentaufträge an. | `start=1` |
| `limit` | Gibt die Anzahl der pro Seite zurückgegebenen Segmentaufträge an. | `limit=20` |
| `status` | Filtert die Ergebnisse anhand ihres Status. Unterstützte Werte sind „NEW“ (neu), „QUEUED“ (in Warteschlange), „PROCESSING“ (in Bearbeitung), „SUCCEEDED“ (erfolgreich abgeschlossen), „FAILED“ (fehlgeschlagen), „CANCELLING“ (wird abgebrochen) und „CANCELLED“ (abgebrochen). | `status=NEW` |
| `sort` | Ordnet die zurückgegebenen Segmentaufträge. Ist im Format `[attributeName]:[desc|asc]` geschrieben. | `sort=creationTime:desc` |
| `property` | Filtert Segmentaufträge und erhält genaue Übereinstimmungen für den angegebenen Filter. Das kann in einem der folgenden Formate geschrieben sein: <ul><li>`[jsonObjectPath]==[value]` – Filtern nach dem Objektschlüssel</li><li>`[arrayTypeAttributeName]~[objectKey]==[value]` – Filtern innerhalb des Arrays</li></ul> | `property=segments~segmentId==workInUS` |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs?status=SUCCEEDED \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit einer Liste von Segmentaufträgen für die angegebene IMS-Organisation als JSON zurück. Die folgende Antwort gibt eine Liste aller erfolgreichen Segmentaufträge für die IMS-Organisation zurück.

>[!NOTE]
>
>Die folgende Antwort wurde aus Platzgründen abgeschnitten und zeigt nur den ersten zurückgegebenen Auftrag.

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
                        "existing":10,
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
| `id` | Ein vom System generierter schreibgeschützter Bezeichner für den Segmentauftrag. |
| `status` | Der aktuelle Status für den Segmentauftrag. Mögliche Werte für den Status sind &quot;NEW&quot;, &quot;PROCESSING&quot;, &quot;CANCELING&quot;, &quot;CANCELLED&quot;, &quot;FAILED&quot;und &quot;SUCCEEDED&quot;. |
| `segments` | Ein Objekt, das Informationen zu den Segmentdefinitionen enthält, die im Segmentauftrag zurückgegeben werden. |
| `segments.segment.id` | Die ID der Segmentdefinition. |
| `segments.segment.expression` | Ein Objekt, das Informationen zum Ausdruck der Segmentdefinition enthält, geschrieben in PQL. |
| `metrics` | Ein Objekt, das diagnostische Informationen zum Segmentauftrag enthält. |
| `metrics.totalTime` | Ein Objekt, das Informationen über den Start und das Ende des Segmentierungsauftrags sowie die gesamte benötigte Zeit enthält. |
| `metrics.profileSegmentationTime` | Ein Objekt, das Informationen über den Beginn und das Ende der Segmentierungsauswertung sowie die gesamte benötigte Zeit enthält. |
| `metrics.segmentProfileCounter` | Die Anzahl der pro Segment qualifizierten Profil. |
| `metrics.segmentedProfileByNamespaceCounter` | Die Anzahl der Profil, die für jeden Identitäts-Namensraum auf Segmentbasis qualifiziert sind. |
| `metrics.segmentProfileByStatusCounter` | Die Anzahl der Profil für jeden Status. Die folgenden drei Status werden unterstützt: <ul><li>&quot;realisiert&quot;- Die Anzahl der neuen Profil, die in das Segment eingegeben wurden.</li><li>&quot;existing&quot; - Die Anzahl der Profil, die weiterhin im Segment vorhanden sind.</li><li>&quot;Exited&quot;- Die Anzahl der Segmentsegmente, die im Profil nicht mehr vorhanden sind.</li></ul> |
| `metrics.totalProfilesByMergePolicy` | Die Gesamtzahl der zusammengeführten Profil auf der Grundlage der Zusammenführungsrichtlinien. |

## Neuen Segmentauftrag erstellen {#create}

Sie können einen neuen Segmentauftrag erstellen, indem Sie eine POST an den Endpunkt `/segment/jobs` anfordern und die ID der Segmentdefinition einschließen, aus der Sie eine neue Audience erstellen möchten.

**API-Format**

```http
POST /segment/jobs
```

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
[
  {
    "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
  }
]'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `segmentId` | Die ID der Segmentdefinition, für die Sie einen Segmentauftrag erstellen möchten. Diese Segmentdefinitionen können zu verschiedenen Zusammenführungsrichtlinien gehören. Weitere Informationen zu Segmentdefinitionen finden Sie im [Segmentdefinitionsendpunkt-Handbuch](./segment-definitions.md). |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zu Ihrem neu erstellten Segmentauftrag zurück.

```json
{
    "id": "d3b4a50d-dfea-43eb-9fca-557ea53771fd",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "api",
    "status": "NEW",
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
    "updateTime": 1579304260000,
    "creationTime": 1579304260897,
    "updateEpoch": 1579304260
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `id` | Ein vom System generierter schreibgeschützter Bezeichner für den neu erstellten Segmentauftrag. |
| `status` | Der aktuelle Status für den Segmentauftrag. Da der Segmentauftrag neu erstellt wurde, lautet der Status immer &quot;NEU&quot;. |
| `segments` | Ein Objekt, das Informationen zu den Segmentdefinitionen enthält, für die dieser Segmentauftrag ausgeführt wird. |
| `segments.segment.id` | Die ID der von Ihnen angegebenen Segmentdefinition. |
| `segments.segment.expression` | Ein Objekt, das Informationen zum Ausdruck der Segmentdefinition enthält, geschrieben in PQL. |

## Bestimmten Segmentauftrag abrufen {#get}

Sie können detaillierte Informationen zu einem bestimmten Segmentauftrag abrufen, indem Sie eine GET an den Endpunkt `/segment/jobs` anfordern und die ID des Segmentauftrags angeben, den Sie im Anforderungspfad abrufen möchten.

**API-Format**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | Der `id`-Wert des Segmentauftrags, den Sie abrufen möchten. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit genauen Informationen zum angegebenen Segmentauftrag zurück.

```json
{
    "id": "d3b4a50d-dfea-43eb-9fca-557ea53771fd",
    "imsOrgId": "{IMS_ORG}",
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
| `id` | Ein vom System generierter schreibgeschützter Bezeichner für den Segmentauftrag. |
| `status` | Der aktuelle Status für den Segmentauftrag. Mögliche Werte für den Status sind &quot;NEW&quot;, &quot;PROCESSING&quot;, &quot;CANCELING&quot;, &quot;CANCELLED&quot;, &quot;FAILED&quot;und &quot;SUCCEEDED&quot;. |
| `segments` | Ein Objekt, das Informationen zu den Segmentdefinitionen enthält, die im Segmentauftrag zurückgegeben werden. |
| `segments.segment.id` | Die ID der Segmentdefinition. |
| `segments.segment.expression` | Ein Objekt, das Informationen zum Ausdruck der Segmentdefinition enthält, geschrieben in PQL. |
| `metrics` | Ein Objekt, das diagnostische Informationen zum Segmentauftrag enthält. |

## Massenabruf von Segmentaufträgen {#bulk-get}

Sie können detaillierte Informationen zu mehreren Segmentaufträgen abrufen, indem Sie eine POST an den `/segment/jobs/bulk-get`-Endpunkt anfordern und die `id`-Werte der Segmentaufträge im Anforderungstext angeben.

**API-Format**

```http
POST /segment/jobs/bulk-get
```

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 207 mit den angeforderten Segmentaufträgen zurück.

>[!NOTE]
>
>Die folgende Antwort wurde für Leerzeichen abgeschnitten und zeigt nur Teildetails der einzelnen Segmentaufträge an. Bei der vollständigen Antwort werden alle Details zu den angeforderten Segmentaufträgen Liste.

```json
{
    "results": {
        "cc3419d3-0389-47f1-b174-fead6b3c830d": {
            "id": "cc3419d3-0389-47f1-b174-fead6b3c830d",
            "imsOrgId": "{IMS_ORG}",
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
            "imsOrgId": "{IMS_ORG}",
            "status": "SUCCEEDED",
            "segments": [
                {
                    "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
                    "segment": {
                        "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
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
| `id` | Ein vom System generierter schreibgeschützter Bezeichner für den Segmentauftrag. |
| `status` | Der aktuelle Status für den Segmentauftrag. Mögliche Werte für den Status sind &quot;NEW&quot;, &quot;PROCESSING&quot;, &quot;CANCELING&quot;, &quot;CANCELLED&quot;, &quot;FAILED&quot;und &quot;SUCCEEDED&quot;. |
| `segments` | Ein Objekt, das Informationen zu den Segmentdefinitionen enthält, die im Segmentauftrag zurückgegeben werden. |
| `segments.segment.id` | Die ID der Segmentdefinition. |
| `segments.segment.expression` | Ein Objekt, das Informationen zum Ausdruck der Segmentdefinition enthält, geschrieben in PQL. |

## Bestimmten Segmentauftrag abbrechen oder löschen {#delete}

Sie können einen bestimmten Segmentauftrag löschen, indem Sie eine DELETE-Anforderung an den Endpunkt `/segment/jobs` stellen und die ID des Segmentauftrags angeben, der im Anforderungspfad gelöscht werden soll.

>[!NOTE]
>
>Die API-Antwort auf die Löschanforderung erfolgt sofort. Der eigentliche Löschvorgang des Segmentauftrags ist jedoch asynchron. Mit anderen Worten, es gibt einen zeitlichen Unterschied zwischen dem Zeitpunkt, zu dem die Anforderung zum Löschen des Segmentauftrags ausgeführt wird, und dem Zeitpunkt, zu dem er angewendet wird.

**API-Format**

```http
DELETE /segment/jobs/{SEGMENT_JOB_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | Der `id`-Wert des Segmentauftrags, den Sie löschen möchten. |

**Anfrage**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 mit folgenden Informationen zurück.

```json
{
    "status": true,
    "message": "Segment job with id 'd3b4a50d-dfea-43eb-9fca-557ea53771fd' has been marked for cancelling"
}
```

## Nächste Schritte

Nach dem Lesen dieses Handbuchs verstehen Sie nun besser, wie Segmentaufträge funktionieren.
