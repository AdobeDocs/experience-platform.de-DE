---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Exportaufträge
topic: developer guide
translation-type: tm+mt
source-git-commit: 16ebff522c5b08e4c100f5d2f972ef4db64656a7
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 4%

---


# Exportaufträge

intro

- Eine Liste von Exportaufträgen abrufen
- Neuen Exportauftrag erstellen
- Abrufen eines bestimmten Exportauftrags
- Abbrechen oder Löschen eines bestimmten Exportauftrags

## Erste Schritte

Die in diesem Handbuch verwendeten API-Endpunkte sind Teil der Segmentierungs-API. Bevor Sie fortfahren, lesen Sie bitte das Entwicklerhandbuch für die [Segmentierung](./getting-started.md).

Insbesondere enthält der [Abschnitt](./getting-started.md#getting-started) &quot;Erste Schritte&quot;des Segmentierungsentwicklerhandbuchs Links zu verwandten Themen, eine Anleitung zum Lesen der Beispiel-API-Aufrufe im Dokument und wichtige Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen einer Experience Platform-API erforderlich sind.

## Eine Liste von Exportaufträgen abrufen

Sie können eine Liste aller Exportaufträge für Ihre IMS-Organisation abrufen, indem Sie eine GET-Anforderung an den `/export/jobs` Endpunkt senden.

**API-Format**

```http
GET /export/jobs
GET /export/jobs?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`: (*Optional*) Dem Anforderungspfad hinzugefügte Parameter, die die in der Antwort zurückgegebenen Ergebnisse konfigurieren. Es können mehrere Parameter eingeschlossen werden, die durch das kaufmännische Und (`&`) voneinander getrennt werden. Die verfügbaren Parameter sind unten aufgeführt.

**Abfrage**

Im Folgenden finden Sie eine Liste der verfügbaren Abfragen für die Auflistung von Exportaufträgen. Alle diese Parameter sind optional. Wenn Sie diesen Endpunkt ohne Parameter aufrufen, werden alle für Ihr Unternehmen verfügbaren Exportaufträge abgerufen.

| Parameter | Beschreibung |
| --------- | ----------- |
| `limit` | Gibt die Anzahl der zurückgegebenen Exportaufträge an. |
| `offset` | Gibt den Versatz der Ergebnisseiten an. |
| `status` | Die Ergebnisse werden auf der Grundlage des Status Filter. Die unterstützten Werte sind `NEW`, `SUCCEEDED`und `FAILED`. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs?status=SUCCEEDED \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit einer Liste von Exportaufträgen für das angegebene IMS-Unternehmen als JSON zurück. Die folgende Antwort gibt eine Liste aller erfolgreichen Exportaufträge für das IMS-Unternehmen zurück.

```json
{
  "records": [
    {
      "id": 100,
      "jobType": "BATCH",
      "destination": {
        "datasetId": "5b7c86968f7b6501e21ba9df",
        "segmentPerBatch": false,
        "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52",
        "batches": {
          "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
          "segmentNs": "ups",
          "status": [
            "realized"
          ],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        }
      },
      "fields": "identities.id,personalEmail.address",
      "schema": {
        "name": "_xdm.context.profile"
      },
      "imsOrgId": "1BD6382559DF0C130A49422D@AdobeOrg",
      "status": "SUCCEEDED",
      "filter": {
        "segments": [
          {
            "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
            "segmentNs": "ups",
            "status": [
              "realized"
            ]
          }
        ],
        "segmentQualificationTime": {
          "startTime": "2018-01-01T00:00:00Z",
          "endTime": "2018-02-01T00:00:00Z"
        },
        "fromIngestTimestamp": "2018-01-01T00:00:00Z",
        "emptyProfiles": true
      },
      "additionalFields": {
        "eventList": {
          "fields": "string",
          "filter": {
            "fromIngestTimestamp": "2018-01-01T00:00:00Z"
          }
        }
      },
      "mergePolicy": {
        "id": "timestampOrdered-none-mp",
        "version": 1
      },
      "profileInstanceId": "ups",
      "errors": [
        {
          "code": "0100000003",
          "msg": "Error in Export Job",
          "callStack": "com.adobe.aep.unifiedprofile.common.logging.Logger"
        }
      ],
      "metrics": {
        "totalTime": {
          "startTimeInMs": 123456789000,
          "endTimeInMs": 123456799000,
          "totalTimeInMs": 10000
        },
        "profileExportTime": {
          "startTimeInMs": 123456789000,
          "endTimeInMs": 123456799000,
          "totalTimeInMs": 10000
        },
        "aCPDatasetWriteTime": {
          "startTimeInMs": 123456789000,
          "endTimeInMs": 123456799000,
          "totalTimeInMs": 10000
        }
      },
      "computeGatewayJobId": {
        "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
        "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
      },
      "creationTime": 1538615973895,
      "updateTime": 1538616233239,
      "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
    }
  ],
  "page": {
    "sortField": "createdTime",
    "sort": "desc",
    "pageOffset": "1540974701302_96",
    "pageSize": 10
  },
  "link": {
    "next": "string"
  }
}
```

## Neuen Exportauftrag erstellen

Sie können einen neuen Exportauftrag erstellen, indem Sie eine POST-Anforderung an den `/export/jobs` Endpunkt senden.

**API-Format**

```http
POST /export/jobs
```

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/export/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
  "fields": "identities.id,personalEmail.address",
  "mergePolicy": {
    "id": "timestampOrdered-none-mp",
    "version": 1
  },
  "filter": {
    "segments": [
      {
        "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
        "segmentNs": "ups",
        "status": [
          "realized"
        ]
      }
    ],
    "segmentQualificationTime": {
      "startTime": "2018-01-01T00:00:00Z",
      "endTime": "2018-02-01T00:00:00Z"
    },
    "fromIngestTimestamp": "2018-01-01T00:00:00Z",
    "emptyProfiles": true
  },
  "additionalFields": {
    "eventList": {
      "fields": "string",
      "filter": {
        "fromIngestTimestamp": "2018-01-01T00:00:00Z"
      }
    }
  },
  "destination": {
    "datasetId": "5b7c86968f7b6501e21ba9df"
  },
  "schema": {
    "name": "_xdm.context.profile"
  }
 }'
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `fields` | Optional. Eine Liste der exportierten Felder, durch Kommas getrennt. Wenn Sie das Feld leer lassen, werden alle Felder exportiert. |
| `mergePolicy` | Optional. Ist dies nicht der Fall, wird für den Export dieselbe Merge-Richtlinie wie für das angegebene Segment verwendet. |
| `filter` | Optional. Wenn Sie das Feld leer lassen, werden alle Daten exportiert. |
| `filter.segments` | Optional. Die Filter des Segments für den Exportauftrag. |
| `filter.segmentQualificationTime` | Optional. Ein Filter für die Zeit der Segmentqualifizierung. Der Beginn und/oder die Endzeit können angegeben werden. |
| `filter.fromIngestTimestamp` | Optional. Ein RFC-3339 formatierter Zeitstempel. |
| `destination.datasetId` | Erforderlich. Der `id` Wert des Datensatzes, in den die Daten exportiert werden. |
| `segments.segmentId` | Erforderlich. Der `id` Wert des Segments, das exportiert wird. |
| `segments.sgementNs` | Optional. Die `namespace` für das jeweilige Segment. |



**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit Details zu Ihrem neu erstellten Exportauftrag zurück.

```json
{
  "id": 100,
  "jobType": "BATCH",
  "destination": {
    "datasetId": "5b7c86968f7b6501e21ba9df",
    "segmentPerBatch": false,
    "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52",
    "batches": {
      "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
      "segmentNs": "ups",
      "status": [
        "realized"
      ],
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    }
  },
  "fields": "identities.id,personalEmail.address",
  "schema": {
    "name": "_xdm.context.profile"
  },
  "imsOrgId": "1BD6382559DF0C130A49422D@AdobeOrg",
  "status": "SUCCEEDED",
  "filter": {
    "segments": [
      {
        "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
        "segmentNs": "ups",
        "status": [
          "realized"
        ]
      }
    ],
    "segmentQualificationTime": {
      "startTime": "2018-01-01T00:00:00Z",
      "endTime": "2018-02-01T00:00:00Z"
    },
    "fromIngestTimestamp": "2018-01-01T00:00:00Z",
    "emptyProfiles": true
  },
  "additionalFields": {
    "eventList": {
      "fields": "string",
      "filter": {
        "fromIngestTimestamp": "2018-01-01T00:00:00Z"
      }
    }
  },
  "mergePolicy": {
    "id": "timestampOrdered-none-mp",
    "version": 1
  },
  "profileInstanceId": "ups",
  "errors": [
    {
      "code": "0100000003",
      "msg": "Error in Export Job",
      "callStack": "com.adobe.aep.unifiedprofile.common.logging.Logger"
    }
  ],
  "metrics": {
    "totalTime": {
      "startTimeInMs": 123456789000,
      "endTimeInMs": 123456799000,
      "totalTimeInMs": 10000
    },
    "profileExportTime": {
      "startTimeInMs": 123456789000,
      "endTimeInMs": 123456799000,
      "totalTimeInMs": 10000
    },
    "aCPDatasetWriteTime": {
      "startTimeInMs": 123456789000,
      "endTimeInMs": 123456799000,
      "totalTimeInMs": 10000
    }
  },
  "computeGatewayJobId": {
    "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
    "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
  },
  "creationTime": 1538615973895,
  "updateTime": 1538616233239,
  "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
}
```

## Abrufen eines bestimmten Exportauftrags

Sie können detaillierte Informationen zu einem bestimmten Exportauftrag abrufen, indem Sie eine GET-Anforderung an den `/export/jobs` Endpunkt senden und den `id` Wert des Exportauftrags im Anforderungspfad angeben.

**API-Format**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

- `{EXPORT_JOB_ID}`: Der `id` Wert des Exportauftrags, den Sie abrufen möchten.

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/{EXPORT_JOB_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit detaillierten Informationen zum angegebenen Exportauftrag zurück.

```json
{
  "id": 100,
  "jobType": "BATCH",
  "destination": {
    "datasetId": "5b7c86968f7b6501e21ba9df",
    "segmentPerBatch": false,
    "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52",
    "batches": {
      "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
      "segmentNs": "ups",
      "status": [
        "realized"
      ],
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    }
  },
  "fields": "identities.id,personalEmail.address",
  "schema": {
    "name": "_xdm.context.profile"
  },
  "imsOrgId": "1BD6382559DF0C130A49422D@AdobeOrg",
  "status": "SUCCEEDED",
  "filter": {
    "segments": [
      {
        "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
        "segmentNs": "ups",
        "status": [
          "realized"
        ]
      }
    ],
    "segmentQualificationTime": {
      "startTime": "2018-01-01T00:00:00Z",
      "endTime": "2018-02-01T00:00:00Z"
    },
    "fromIngestTimestamp": "2018-01-01T00:00:00Z",
    "emptyProfiles": true
  },
  "additionalFields": {
    "eventList": {
      "fields": "string",
      "filter": {
        "fromIngestTimestamp": "2018-01-01T00:00:00Z"
      }
    }
  },
  "mergePolicy": {
    "id": "timestampOrdered-none-mp",
    "version": 1
  },
  "profileInstanceId": "ups",
  "errors": [
    {
      "code": "0100000003",
      "msg": "Error in Export Job",
      "callStack": "com.adobe.aep.unifiedprofile.common.logging.Logger"
    }
  ],
  "metrics": {
    "totalTime": {
      "startTimeInMs": 123456789000,
      "endTimeInMs": 123456799000,
      "totalTimeInMs": 10000
    },
    "profileExportTime": {
      "startTimeInMs": 123456789000,
      "endTimeInMs": 123456799000,
      "totalTimeInMs": 10000
    },
    "aCPDatasetWriteTime": {
      "startTimeInMs": 123456789000,
      "endTimeInMs": 123456799000,
      "totalTimeInMs": 10000
    }
  },
  "computeGatewayJobId": {
    "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
    "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
  },
  "creationTime": 1538615973895,
  "updateTime": 1538616233239,
  "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
}
```

## Abbrechen oder Löschen eines bestimmten Exportauftrags

Sie können anfordern, einen angegebenen Exportauftrag zu löschen, indem Sie eine DELETE-Anforderung an den `/export/jobs` Endpunkt senden und den `id` Wert des Exportauftrags im Anforderungspfad angeben.

**API-Format**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

- `{EXPORT_JOB_ID}`: Der `id` Wert des Exportauftrags, den Sie löschen möchten.

**Anfrage**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/export/jobs/{EXPORT_JOB_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit der folgenden Meldung zurück:

```json
{
  "status": true,
  "message": "Export job has been marked for cancelling"
}
```

## Nächste Schritte
