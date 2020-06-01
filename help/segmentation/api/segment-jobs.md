---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Segmentaufträge
topic: developer guide
translation-type: tm+mt
source-git-commit: b0554d931718bb6a8dd7d4f971daf3652a19a2a8
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 3%

---


# Entwicklerhandbuch für Segmentaufträge

Ein Segmentauftrag ist ein asynchroner Vorgang, bei dem ein neues Audiencen-Segment erstellt wird. Er verweist auf eine Segmentdefinition sowie auf alle Zusammenführungsrichtlinien, die steuern, wie Echtzeit-Kundenattribute in Ihren Profil-Fragmenten überlappende Attribute zusammenführen. Nach erfolgreichem Abschluss eines Segmentauftrags können Sie verschiedene Segmentinformationen sammeln, z. B. Fehler, die während der Verarbeitung aufgetreten sind, und die endgültige Größe Ihrer Audience.

Dieses Handbuch enthält Informationen zum besseren Verständnis von Segmentaufträgen und enthält Beispiel-API-Aufrufe zum Ausführen grundlegender Aktionen mit der API.

## Erste Schritte

Die in diesem Handbuch verwendeten API-Endpunkte sind Teil der Segmentierungs-API. Bevor Sie fortfahren, lesen Sie bitte das Entwicklerhandbuch für die [Segmentierung](./getting-started.md).

Insbesondere enthält der [Abschnitt](./getting-started.md#getting-started) &quot;Erste Schritte&quot;des Segmentierungsentwicklerhandbuchs Links zu verwandten Themen, eine Anleitung zum Lesen der Beispiel-API-Aufrufe im Dokument und wichtige Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen einer Experience Platform-API erforderlich sind.

## Eine Liste von Segmentaufträgen abrufen

Sie können eine Liste aller Segmentaufträge für Ihre IMS-Organisation abrufen, indem Sie eine GET-Anforderung an den `/segment/jobs` Endpunkt senden.

**API-Format**

```http
GET /segment/jobs
GET /segment/jobs?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`: (*Optional*) Dem Anforderungspfad hinzugefügte Parameter, die die in der Antwort zurückgegebenen Ergebnisse konfigurieren. Es können mehrere Parameter eingeschlossen werden, die durch das kaufmännische Und (`&`) voneinander getrennt werden. Die verfügbaren Parameter sind unten aufgeführt.

**Abfrage**

Im Folgenden finden Sie eine Liste der verfügbaren Abfragen für die Auflistung von Segmentaufträgen. Alle diese Parameter sind optional. Wenn Sie diesen Endpunkt ohne Parameter aufrufen, werden alle für Ihr Unternehmen verfügbaren Segmentaufträge abgerufen.

| Parameter | Beschreibung |
| --------- | ----------- |
| `start` | Gibt den Startversatz für die zurückgegebenen Segmentaufträge an. |
| `limit` | Gibt die Anzahl der pro Seite zurückgegebenen Segmentaufträge an. |
| `status` | Die Ergebnisse werden auf der Grundlage des Status Filter. Die unterstützten Werte sind &quot;NEU&quot;, &quot;ABGESCHLOSSEN&quot;, &quot;VERARBEITUNG&quot;, &quot;ERFOLGT&quot;, &quot;FEHLGESCHLAGEN&quot;, &quot;ABGESCHLOSSEN&quot;, &quot;ABGESCHLOSSEN&quot; |
| `sort` | Die zurückgegebenen Segmentaufträge werden bestellt. Ist im Format geschrieben `[attributeName]:[desc|asc]`. |
| `property` | Filter segmentieren Aufträge und erhalten exakte Übereinstimmungen für den angegebenen Filter. Es kann in einem der folgenden Formate geschrieben werden: <ul><li>`[jsonObjectPath]==[value]` - Filtern nach dem Objektschlüssel</li><li>`[arrayTypeAttributeName]~[objectKey]==[value]` - Filtern innerhalb des Arrays</li></ul> |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs?status=SUCCEEDED \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit einer Liste von Segmentaufträgen für das angegebene IMS-Unternehmen als JSON zurück. Die folgende Antwort gibt eine Liste aller erfolgreichen Segmentaufträge für das IMS-Unternehmen zurück.

>[!NOTE] Die folgende Antwort wurde für Leerzeichen abgeschnitten und zeigt nur den ersten zurückgegebenen Auftrag an.

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

## Neuen Segmentauftrag erstellen

Sie können einen neuen Segmentauftrag erstellen, indem Sie eine POST-Anforderung an den `/segment/jobs` Endpunkt senden.

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
]
 '
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit Details zu Ihrem neu erstellten Segmentauftrag zurück.

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

## Abrufen eines bestimmten Segmentauftrags

Sie können detaillierte Informationen zu einem bestimmten Segmentauftrag abrufen, indem Sie eine GET-Anforderung an den `/segment/jobs` Endpunkt senden und den `id` Wert des Segmentauftrags im Anforderungspfad angeben.

**API-Format**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | Der `id` Wert des Segmentauftrags, den Sie abrufen möchten. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit detaillierten Informationen zum angegebenen Segmentauftrag zurück.

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

## Massenabruf von Segmentaufträgen

Sie können detaillierte Informationen zu mehreren angegebenen Segmentaufträgen abrufen, indem Sie eine POST-Anforderung an den `/segment/jobs/bulk-get` Endpunkt senden und die `id` Werte der Segmentaufträge im Anforderungstext angeben.

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

>[!NOTE] Die folgende Antwort wurde für Leerzeichen abgeschnitten und zeigt nur Teildetails der einzelnen Segmentaufträge an. Bei der vollständigen Antwort werden alle Details zu den angeforderten Segmentaufträgen Liste.

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

## Abbrechen oder Löschen eines bestimmten Segmentauftrags

Sie können einen bestimmten Segmentauftrag löschen, indem Sie eine DELETE-Anforderung an den `/segment/jobs` Endpunkt senden und den `id` Wert des Segmentauftrags im Anforderungspfad angeben.

**API-Format**

```http
DELETE /segment/jobs/{SEGMENT_JOB_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | Der `id` Wert des Segmentauftrags, den Sie löschen möchten. |

**Anfrage**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 204 mit den folgenden Informationen zurück.

```json
{
    "status": true,
    "message": "Segment job with id 'd3b4a50d-dfea-43eb-9fca-557ea53771fd' has been marked for cancelling"
}
```

## Nächste Schritte

Nach dem Lesen dieses Handbuchs haben Sie jetzt ein besseres Verständnis dafür, wie Segmentaufträge funktionieren. Weitere Informationen zur Segmentierung finden Sie in der [Segmentierungsübersicht](../home.md).