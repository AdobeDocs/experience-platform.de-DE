---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Endpunkt-Handbuch für Exportaufträge
topic: developer guide
translation-type: tm+mt
source-git-commit: 3e39333207ef6c94b6d792be33a4605f185ff5ab
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 16%

---


# Endpunkt-Handbuch für Exportaufträge

Exportaufträge sind asynchrone Prozesse, mit denen Segmentmitglieder der Audience zu Datensätzen beibehalten werden. Sie können den `/export/jobs` Endpunkt in der Adobe Experience Platform Segmentation API verwenden, mit dem Sie Exportaufträge programmgesteuert abrufen, erstellen und abbrechen können.

## Erste Schritte

The endpoints used in this guide are part of the [!DNL Adobe Experience Platform Segmentation Service] API. Before continuing, please review the [getting started guide](./getting-started.md) for important information that you need to know in order to successfully make calls to the API, including required headers and how to read example API calls.

## Liste mit Exportaufträgen abrufen {#retrieve-list}

Sie können eine Liste aller Exportaufträge für Ihre IMS-Organisation abrufen, indem Sie eine GET-Anfrage an den `/export/jobs`-Endpunkt senden.

**API-Format**

Der `/export/jobs` Endpunkt unterstützt mehrere Abfragen-Parameter, um die Ergebnisse zu filtern. Diese Parameter sind optional, ihre Verwendung wird jedoch dringend empfohlen, um den kostspieligen Aufwand zu reduzieren. Wenn Sie diesen Endpunkt ohne Parameter aufrufen, werden alle für Ihre Organisation verfügbaren Exportaufträge abgerufen. Es können mehrere Parameter eingeschlossen werden, getrennt durch das kaufmännische Und-Zeichen (`&`).

```http
GET /export/jobs
GET /export/jobs?limit={LIMIT}
GET /export/jobs?offset={OFFSET}
GET /export/jobs?status={STATUS}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{LIMIT}` | Gibt die Zahl der zurückgegebenen Exportaufträge an. |
| `{OFFSET}` | Gibt den Versatz der Ergebnisseiten an. |
| `{STATUS}` | Filtert die Ergebnisse auf der Grundlage des Status. Die unterstützten Werte sind &quot;NEW&quot;, &quot;SUCCEEDED&quot;und &quot;FAILED&quot;. |

**Anfrage**

Mit der folgenden Anforderung werden die letzten beiden Exportaufträge innerhalb Ihrer IMS-Organisation abgerufen.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Die folgende Antwort gibt HTTP-Status 200 mit einer Liste erfolgreich abgeschlossener Exportaufträge zurück, basierend auf dem im Anforderungspfad bereitgestellten Abfrage-Parameter.

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
                ]
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
                "totalExportedProfileCounter": 20,
                "exportedProfileByNamespaceCounter": {
                    "namespace1": 10,
                    "namespace2": 5
                }
            },
            "computeGatewayJobId": {
                "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94"
            },
            "creationTime": 1538615973895,
            "updateTime": 1538616233239,
            "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
        },
        {
            "profileInstanceId": "test_xdm_latest_profile_20_e2e_1538573005395",
            "errors": [
                {
                    "code": "0090000009",
                    "msg": "Error writing profiles to output path 'adl://va7devprofilesnapshot.azuredatalakestore.net/snapshot/722'",
                    "callStack": "com.adobe.aep.unifiedprofile.common.logging.Logger" 
                },
                {
                    "code": "unknown",
                    "msg": "Job aborted.",
                    "callStack": "org.apache.spark.SparkException: Job aborted."
                }
            ],
            "jobType": "BATCH",
            "filter": {
                "segments": [
                    {
                        "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                        "segmentNs": "AAM",
                        "status": ["realized", "existing"]
                    }
                ]
            },
            "id": 722,
            "schema": {
                "name": "_xdm.context.profile"
            },
            "mergePolicy": {
                "id": "7972e3d6-96ea-4ece-9627-cbfd62709c5d",
                "version": 1
            },
            "status": "FAILED",
            "requestId": "KbOAsV7HXmdg262lc4yZZhoml27UWXPZ",
            "computeGatewayJobId": {
                "exportJob": "15971e0f-317c-4390-9038-1a0498eb356f"
            },
            "metrics": {
                "totalTime": {
                    "startTimeInMs": 1538573416687,
                    "endTimeInMs": 1538573922551,
                    "totalTimeInMs": 505864
                },
                "profileExportTime": {
                    "startTimeInMs": 1538573872211,
                    "endTimeInMs": 1538573918809,
                    "totalTimeInMs": 46598
                }
            },
            "destination": {
                "datasetId": "5bb4c46757920712f924a3eb",
                "segmentPerBatch": false,
                "batchId": "IWEQ6920712f9475762D"
            },
            "updateTime": 1538573922551,
            "imsOrgId": "1BD6382559DF0C130A49422D@AdobeOrg",
            "creationTime": 1538573416687
        }
    ],
    "page":{
        "sortField": "createdTime",
        "sort": "desc",
        "pageOffset": "1540974701302_96",
        "pageSize": 2
    },
    "link":{
        "next": "/export/jobs/?limit=2&offset=1538573416687_722"
    }
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `destination` | Zielinformationen für die exportierten Daten:<ul><li>`datasetId`: Die ID des Datensatzes, in den Daten exportiert wurden.</li><li>`segmentPerBatch`: Ein boolescher Wert, der angibt, ob Segment-IDs konsolidiert sind. Der Wert &quot;false&quot;bedeutet, dass alle Segment-IDs in eine einzige Stapel-ID exportiert werden. Der Wert &quot;true&quot;bedeutet, dass eine Segment-ID in eine Stapel-ID exportiert wird. **Hinweis:** Das Festlegen des Werts auf &quot;true&quot;kann sich auf die Exportleistung des Stapels auswirken.</li></ul> |
| `fields` | Eine Liste der exportierten Felder, durch Kommas getrennt. |
| `schema.name` | Der Name des mit dem Datensatz verknüpften Schemas, in das Daten exportiert werden sollen. |
| `filter.segments` | Die Segmente, die exportiert werden. Die folgenden Felder sind enthalten:<ul><li>`segmentId`: Die Segment-ID, in die Profil exportiert werden.</li><li>`segmentNs`: Segment-Namensraum für die angegebene `segmentID`.</li><li>`status`: Ein Zeichenfolgen-Array, das einen Statusfilter für die `segmentID`Zeichenfolge bereitstellt. Standardmäßig `status` wird der Wert `["realized", "existing"]` verwendet, der alle Profil darstellt, die zum aktuellen Zeitpunkt in das Segment fallen. Mögliche Werte sind: &quot;realisiert&quot;, &quot;vorhanden&quot;und &quot;beendet&quot;.</li></ul> |
| `mergePolicy` | Richtlinieninformationen für die exportierten Daten zusammenführen |
| `metrics.totalTime` | Ein Feld, das die Gesamtdauer angibt, die der Exportauftrag gedauert hat. |
| `metrics.profileExportTime` | Ein Feld, das angibt, wie lange es gedauert hat, bis die Profil exportiert wurden. |
| `page` | Informationen zur Paginierung der angeforderten Exportaufträge. |
| `link.next` | Ein Link zur nächsten Seite der Exportaufträge. |

## Neuen Exportauftrag erstellen {#create}

Sie können einen neuen Exportauftrag erstellen, indem Sie eine POST-Anfrage an den `/export/jobs`-Endpunkt senden.

**API-Format**

```http
POST /export/jobs
```

**Anfrage**

Die folgende Anforderung erstellt einen neuen Exportauftrag, der durch die in der Payload bereitgestellten Parameter konfiguriert wird.

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
                "fromIngestTimestamp": "2018-01-01T00:00:00Z",
                "toIngestTimestamp": "2020-01-01T00:00:00Z"
            }
        }
    },
    "destination":{
        "datasetId": "5b7c86968f7b6501e21ba9df",
        "segmentPerBatch": false
    },
    "schema":{
        "name": "_xdm.context.profile"
    }
}'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `fields` | Eine Liste der exportierten Felder, durch Kommas getrennt. Wenn leer gelassen, werden alle Felder exportiert. |
| `mergePolicy` | Gibt die Richtlinie zum Zusammenführen der exportierten Daten an. Schließen Sie diesen Parameter ein, wenn mehrere Segmente exportiert werden. Wenn nicht angegeben, wird für den Export dieselbe Zusammenführungsrichtlinie wie für das angegebene Segment verwendet. |
| `filter` | Ein Objekt, das die Segmente angibt, die je nach ID, Qualifikationszeit oder Erfassungszeit in den Exportauftrag aufgenommen werden, und zwar je nach den unten aufgeführten Untereigenschaften. Wenn leer gelassen, werden alle Daten exportiert. |
| `filter.segments` | Gibt die zu exportierenden Segmente an. Wird dieser Wert nicht angegeben, werden alle Daten aus allen Profilen exportiert. Akzeptiert ein Array von Segmentobjekten, die jeweils die folgenden Felder enthalten:<ul><li>`segmentId`: **(Erforderlich bei Verwendung`segments`)** der Segment-ID für Profil, die exportiert werden sollen.</li><li>`segmentNs` *(Optional)* Segmentcode für den jeweiligen Namensraum `segmentID`.</li><li>`status` *(Optional)* Ein Array von Zeichenfolgen, das einen Statusfilter für die `segmentID`Zeichenfolge bereitstellt. Standardmäßig `status` wird der Wert `["realized", "existing"]` verwendet, der alle Profil darstellt, die zum aktuellen Zeitpunkt in das Segment fallen. Possible values include: `"realized"`, `"existing"`, and `"exited"`.</li></ul> |
| `filter.segmentQualificationTime` | Filtern Sie nach der Segmentqualifizierungszeit. Die Beginn- und/oder Endzeit können angegeben werden. |
| `filter.segmentQualificationTime.startTime` | Beginn des Segmentqualifizierungsstatus für eine Segment-ID für einen bestimmten Status. Es wurde nicht angegeben, es wird kein Filter für die Zeit des Beginns für eine Segment-ID-Qualifizierung angezeigt. Der Zeitstempel muss im [RFC 3339](https://tools.ietf.org/html/rfc3339) -Format angegeben werden. |
| `filter.segmentQualificationTime.endTime` | Endzeit der Segmentqualifizierung für eine Segment-ID für einen bestimmten Status. Es wurde kein Filter für die Endzeit einer Segment-ID-Qualifizierung bereitgestellt. Der Zeitstempel muss im [RFC 3339](https://tools.ietf.org/html/rfc3339) -Format angegeben werden. |
| `filter.fromIngestTimestamp ` | Beschränkt exportierte Profil auf nur diejenigen, die nach diesem Zeitstempel aktualisiert wurden. Der Zeitstempel muss im [RFC 3339](https://tools.ietf.org/html/rfc3339) -Format angegeben werden. <ul><li>`fromIngestTimestamp` für **Profile**, sofern vorhanden: Umfasst alle zusammengeführten Profil, bei denen der zusammengeführte aktualisierte Zeitstempel größer als der angegebene Zeitstempel ist. Unterstützt `greater_than` Operand.</li><li>`fromIngestTimestamp` für **Ereignisse**: Alle nach diesem Zeitstempel erfassten Ereignis werden entsprechend dem resultierenden Profil exportiert. Dies ist nicht die Ereignis-Zeit selbst, sondern die Aufnahmezeit für die Ereignisse.</li> |
| `filter.emptyProfiles` | Ein boolescher Wert, der angibt, ob nach leeren Profilen gefiltert werden soll. Profil können Profil-Datensätze, ExperienceEvent-Datensätze oder beides enthalten. Profil ohne Profil-Datensätze und nur ExperienceEvent-Datensätze werden als &quot;emptyProfiles&quot;bezeichnet. Um alle Profil im Profil-Store einschließlich &quot;emptyProfiles&quot;zu exportieren, setzen Sie den Wert `emptyProfiles` auf `true`. Wenn `emptyProfiles` dies auf `false`festgelegt ist, werden nur Profil mit Profil-Datensätzen im Store exportiert. Wenn `emptyProfiles` das Attribut nicht enthalten ist, werden standardmäßig nur Profil exportiert, die Profil-Datensätze enthalten. |
| `additionalFields.eventList` | Steuert die Zeitreihenfelder für Ereignisse, die für untergeordnete oder verknüpfte Objekte exportiert werden, indem eine oder mehrere der folgenden Einstellungen bereitgestellt werden:<ul><li>`fields`: Steuerung der zu exportierenden Felder.</li><li>`filter`: Gibt Kriterien an, die die Ergebnisse verknüpfter Objekte einschränken. Erwartet einen für den Export erforderlichen Mindestwert, normalerweise ein Datum.</li><li>`filter.fromIngestTimestamp`: Filter der Zeitreihen-Ereignis zu denen, die nach dem bereitgestellten Zeitstempel erfasst wurden. Dies ist nicht die Ereignis-Zeit selbst, sondern die Aufnahmezeit für die Ereignisse.</li><li>`filter.toIngestTimestamp`: Filter des Zeitstempels zu den Zeitstempeln, die vor dem angegebenen Zeitstempel erfasst wurden. Dies ist nicht die Ereignis-Zeit selbst, sondern die Aufnahmezeit für die Ereignisse.</li></ul> |
| `destination` | **(Erforderlich)** Informationen zu den exportierten Daten:<ul><li>`datasetId`: **(Erforderlich)** Die ID des Datensatzes, in den Daten exportiert werden sollen.</li><li>`segmentPerBatch`: *(Optional)* Ein boolescher Wert, der standardmäßig auf &quot;false&quot;gesetzt ist, wenn er nicht angegeben wird. Der Wert &quot;false&quot;exportiert alle Segment-IDs in eine einzelne Stapel-ID. Der Wert &quot;true&quot;exportiert eine Segment-ID in eine Stapel-ID. Beachten Sie, dass die Einstellung des Werts auf &quot;true&quot;die Exportleistung des Stapels beeinträchtigen kann.</li></ul> |
| `schema.name` | **(Erforderlich)** Der Name des Schemas, das mit dem Datensatz verknüpft ist, in den Daten exportiert werden sollen. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zu Ihrem neu erstellten Exportauftrag zurück.

```json
{
    "id": 100,
    "jobType": "BATCH",
    "destination": {
        "datasetId": "5b7c86968f7b6501e21ba9df",
        "segmentPerBatch": false,
        "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "fields": "identities.id,personalEmail.address",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "imsOrgId": "{IMS_ORG}",
    "status": "NEW",
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
            "fields": "_id, _experience",
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
    "metrics": {
        "totalTime": {
            "startTimeInMs": 123456789000,
        }
    },
    "computeGatewayJobId": {
        "exportJob": ""    
    },
    "creationTime": 1538615973895,
    "updateTime": 1538616233239,
    "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `id` | Ein vom System generierter schreibgeschützter Wert, der den soeben erstellten Exportauftrag identifiziert. |

Wenn Sie `destination.segmentPerBatch` stattdessen `true`den Wert für das `destination` obige Objekt festgelegt hätten, würde es ein `batches` Array haben, wie unten dargestellt:

```json
    "destination": {
        "dataSetId" : "{DATASET_ID}",
        "segmentPerBatch": true,
        "batches" : [
            {
                "segmentId": "segment1",
                "segmentNs": "ups",
                "status": ["realized"],
                "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
            },
            {
                "segmentId": "segment2",
                "segmentNs": "AdCloud",
                "status": "exited",
                "batchId": "df4gssdfb93a09f7e37fa53ad52"
            }
        ]
    }
```

## Bestimmten Exportauftrag abrufen {#get}

You can retrieve detailed information about a specific export job by making a GET request to the `/export/jobs` endpoint and providing the ID of the export job you wish to retrieve in the request path.

**API-Format**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | The `id` of the export job you want to access. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/11037 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit genauen Informationen zum angegebenen Exportauftrag zurück.

```json
{
    "id": 11037,
    "jobType": "BATCH",
    "destination": {
        "datasetId": "5b7c86968f7b6501e21ba9df",
        "segmentPerBatch": false,
        "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "fields": "identities.id,personalEmail.address",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "imsOrgId": "{IMS_ORG}",
    "status": "SUCCEEDED",
    "filter": {
        "segments": [
            {
                "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                "segmentNs": "ups",
                "status":[
                    "realized"
                ]
            }
        ]
    },
    "mergePolicy": {
        "id": "timestampOrdered-none-mp",
        "version": 1
    },
    "profileInstanceId": "ups",
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
        "totalExportedProfileCounter": 20,
        "exportedProfileByNamespaceCounter": {
            "namespace1": 10,
            "namespace2": 5
        }
    },
    "computeGatewayJobId": {
        "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94"
    },
    "creationTime": 1538615973895,
    "updateTime": 1538616233239,
    "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `destination` | Zielinformationen für die exportierten Daten:<ul><li>`datasetId`: Die ID des Datensatzes, in den die Daten exportiert wurden.</li><li>`segmentPerBatch`: Ein boolescher Wert, der angibt, ob Segment-IDs konsolidiert sind. Ein Wert von `false` bedeutet, dass alle Segment-IDs in einer einzelnen Stapel-ID enthalten waren. Der Wert `true` bedeutet, dass eine Segment-ID in eine Stapel-ID exportiert wird.</li></ul> |
| `fields` | Eine Liste der exportierten Felder, durch Kommas getrennt. |
| `schema.name` | Der Name des mit dem Datensatz verknüpften Schemas, in das Daten exportiert werden sollen. |
| `filter.segments` | Die Segmente, die exportiert werden. Die folgenden Felder sind enthalten:<ul><li>`segmentId`: Segment-ID für zu exportierende Profil.</li><li>`segmentNs`: Segment-Namensraum für die angegebene `segmentID`.</li><li>`status`: Ein Zeichenfolgen-Array, das einen Statusfilter für die `segmentID`Zeichenfolge bereitstellt. Standardmäßig `status` wird der Wert `["realized", "existing"]` verwendet, der alle Profil darstellt, die zum aktuellen Zeitpunkt in das Segment fallen. Mögliche Werte sind: &quot;realisiert&quot;, &quot;vorhanden&quot;und &quot;beendet&quot;.</li></ul> |
| `mergePolicy` | Richtlinieninformationen für die exportierten Daten zusammenführen |
| `metrics.totalTime` | Ein Feld, das die Gesamtdauer angibt, die der Exportauftrag gedauert hat. |
| `metrics.profileExportTime` | Ein Feld, das angibt, wie lange es gedauert hat, bis die Profil exportiert wurden. |
| `totalExportedProfileCounter` | Die Gesamtanzahl der Profile, die für alle Stapel exportiert wurden. |

## Bestimmten Exportauftrag abbrechen oder löschen {#delete}

Sie können den angegebenen Exportauftrag löschen, indem Sie eine DELETE-Anforderung an den `/export/jobs` Endpunkt senden und die ID des Exportauftrags angeben, den Sie im Anforderungspfad löschen möchten.

**API-Format**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | The `id` of the export job you want to delete. |

**Anfrage**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/export/jobs/{EXPORT_JOB_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 mit der folgenden Meldung zurück:

```json
{
  "status": true,
  "message": "Export job has been marked for cancelling"
}
```

## Nächste Schritte

Nach dem Lesen dieses Handbuchs haben Sie jetzt ein besseres Verständnis dafür, wie Exportaufträge funktionieren.