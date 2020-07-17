---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Segmentaufträge
topic: developer guide
translation-type: tm+mt
source-git-commit: 2327ce9a87647fb2416093d4a27eb7d4dc4aa4d7
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 38%

---


# Endpunkt-Handbuch für Segmentaufträge

Ein Segmentauftrag ist ein asynchroner Vorgang, bei dem ein neues Zielgruppensegment erstellt wird. It references a [segment definition](./segment-definitions.md), as well as any [merge policies](../../profile/api/merge-policies.md) controlling how [!DNL Real-time Customer Profile] merges overlapping attributes across your profile fragments. Nach erfolgreichem Abschluss eines Segmentauftrags können Sie verschiedene Informationen über das Segment sammeln, z. B. Fehler, die bei der Verarbeitung aufgetreten sind, oder die endgültige Größe Ihrer Zielgruppe.

Dieses Handbuch enthält Informationen zum besseren Verständnis von Segmentaufträgen und umfasst Beispiel-API-Aufrufe zum Ausführen grundlegender Aktionen mit der API.

## Erste Schritte

The endpoints used in this guide are part of the [!DNL Adobe Experience Platform Segmentation Service] API. Before continuing, please review the [getting started guide](./getting-started.md) for important information that you need to know in order to successfully make calls to the API, including required headers and how to read example API calls.

## Liste mit Segmentaufträgen abrufen {#retrieve-list}

Sie können eine Liste aller Segmentaufträge für Ihre IMS-Organisation abrufen, indem Sie eine GET-Anfrage an den `/segment/jobs`-Endpunkt richten.

**API-Format**

Der `/segment/jobs` Endpunkt unterstützt mehrere Abfragen-Parameter, um die Ergebnisse zu filtern. Diese Parameter sind optional, ihre Verwendung wird jedoch dringend empfohlen, um den kostspieligen Aufwand zu reduzieren. Wenn Sie diesen Endpunkt ohne Parameter aufrufen, werden alle für Ihre Organisation verfügbaren Exportaufträge abgerufen. Es können mehrere Parameter eingeschlossen werden, getrennt durch das kaufmännische Und-Zeichen (`&`).

```http
GET /segment/jobs
GET /segment/jobs?{QUERY_PARAMETERS}
```

**Abfrage**

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
                        "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                        "mergePolicy": {
                            "id": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
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
                "totalProfiles": 0,
                "segmentedProfileCounter": {
                    "30230300-ccf1-48ad-8012-c5563a007069": 0,
                    "ca763983-5572-4ea4-809c-b7dff7e0d79b": 0
                },
                "segmentedProfileByNamespaceCounter": {
                    "30230300-ccf1-48ad-8012-c5563a007069": {},
                    "ca763983-5572-4ea4-809c-b7dff7e0d79b": {}
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

## Neuen Segmentauftrag erstellen {#create}

Sie können einen neuen Segmentauftrag erstellen, indem Sie eine POST-Anforderung an den `/segment/jobs` Endpunkt senden und die ID der Segmentdefinition einschließen, aus der Sie eine neue Audience erstellen möchten.

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
| `segmentId` | Die ID der Segmentdefinition, für die Sie einen Segmentauftrag erstellen möchten. Weitere Informationen zu Segmentdefinitionen finden Sie im [Segmentdefinitionsendpunkt-Handbuch](./segment-definitions.md). |

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

You can retrieve detailed information about a specific segment job by making a GET request to the `/segment/jobs` endpoint and providing the ID of the segment job you wish to retrieve in the request path.

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

Sie können detaillierte Informationen zu mehreren Segmentaufträgen abrufen, indem Sie eine POST-Anforderung an den `/segment/jobs/bulk-get` Endpunkt senden und die `id` Werte der Segmentaufträge im Anforderungstext angeben.

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

Sie können einen bestimmten Segmentauftrag löschen, indem Sie eine DELETE-Anforderung an den `/segment/jobs` Endpunkt senden und die ID des Segmentauftrags angeben, den Sie im Anforderungspfad löschen möchten.

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