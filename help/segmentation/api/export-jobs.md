---
keywords: Experience Platform;Startseite;beliebte Themen;Segmentierung;Segmentierung;Segmentierungsdienst;Exportaufträge;API
solution: Experience Platform
title: API-Endpunkt für Exportaufträge
topic-legacy: developer guide
description: Exportaufträge sind asynchrone Prozesse, mit denen Segmentmitglieder der Audience zu Datensätzen beibehalten werden. Sie können den Endpunkt "/export/jobs"in der Adobe Experience Platform Segmentation Service API verwenden, mit dem Sie Exportaufträge programmgesteuert abrufen, erstellen und abbrechen können.
exl-id: 5b504a4d-291a-4969-93df-c23ff5994553
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1680'
ht-degree: 14%

---

# Endpunkt für Exportaufträge

Exportaufträge sind asynchrone Prozesse, mit denen Segmentmitglieder der Audience zu Datensätzen beibehalten werden. Sie können den Endpunkt `/export/jobs` in der Adobe Experience Platform Segmentation API verwenden, mit dem Sie Exportaufträge programmgesteuert abrufen, erstellen und abbrechen können.

>[!NOTE]
>
>Dieses Handbuch behandelt die Verwendung von Exportaufträgen im [!DNL Segmentation API]. Informationen zum Verwalten von Exportaufträgen für [!DNL Real-time Customer Profile]-Daten finden Sie im Handbuch zu [Exportaufträgen in der Profil-API](../../profile/api/export-jobs.md)

## Erste Schritte

Die in diesem Handbuch verwendeten Endpunkte sind Teil der API [!DNL Adobe Experience Platform Segmentation Service]. Bevor Sie fortfahren, lesen Sie bitte im Handbuch [Erste Schritte](./getting-started.md) nach wichtigen Informationen, die Sie kennen müssen, um die API erfolgreich aufzurufen, einschließlich erforderlicher Kopfzeilen und Anleitungen zum Lesen von Beispiel-API-Aufrufen.

## Liste mit Exportaufträgen abrufen {#retrieve-list}

Sie können eine Liste aller Exportaufträge für Ihre IMS-Organisation abrufen, indem Sie eine GET-Anfrage an den `/export/jobs`-Endpunkt senden.

**API-Format**

Der `/export/jobs`-Endpunkt unterstützt mehrere Abfragen-Parameter, um die Ergebnisse zu filtern. Diese Parameter sind optional, ihre Verwendung wird jedoch dringend empfohlen, um den kostspieligen Aufwand zu reduzieren. Wenn Sie diesen Endpunkt ohne Parameter aufrufen, werden alle für Ihre Organisation verfügbaren Exportaufträge abgerufen. Es können mehrere Parameter eingeschlossen werden, die durch kaufmännische Und-Zeichen (`&`) voneinander getrennt werden.

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
| `{STATUS}` | Filtert die Ergebnisse anhand ihres Status. Die unterstützten Werte sind &quot;NEW&quot;, &quot;SUCCEEDED&quot;und &quot;FAILED&quot;. |

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
| `destination` | Zielinformationen für die exportierten Daten:<ul><li>`datasetId`: Die ID des Datensatzes, in den Daten exportiert wurden.</li><li>`segmentPerBatch`: Ein boolescher Wert, der angibt, ob Segment-IDs konsolidiert sind. Der Wert &quot;false&quot;bedeutet, dass alle Segment-IDs in eine einzige Stapel-ID exportiert werden. Der Wert &quot;true&quot;bedeutet, dass eine Segment-ID in eine Stapel-ID exportiert wird. **Hinweis:Die** Einstellung des Werts auf &quot;true&quot;kann sich auf die Exportleistung des Stapels auswirken.</li></ul> |
| `fields` | Eine Liste der exportierten Felder, durch Kommas getrennt. |
| `schema.name` | Der Name des mit dem Datensatz verknüpften Schemas, in das Daten exportiert werden sollen. |
| `filter.segments` | Die Segmente, die exportiert werden. Die folgenden Felder sind enthalten:<ul><li>`segmentId`: Die Segment-ID, in die Profil exportiert werden.</li><li>`segmentNs`: Segment-Namensraum für die angegebene  `segmentID`.</li><li>`status`: Ein Zeichenfolgen-Array, das einen Statusfilter für die  `segmentID`Zeichenfolge bereitstellt. Standardmäßig hat `status` den Wert `["realized", "existing"]`, der alle Profil darstellt, die zum aktuellen Zeitpunkt in das Segment fallen. Mögliche Werte sind: &quot;realisiert&quot;, &quot;vorhanden&quot;und &quot;beendet&quot;. Der Wert &quot;realisiert&quot;bedeutet, dass das Profil in das Segment eintritt. Der Wert &quot;vorhanden&quot;bedeutet, dass sich das Profil weiterhin im Segment befindet. Der Wert &quot;Beenden&quot;bedeutet, dass das Profil das Segment verlässt.</li></ul> |
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
    },
    "evaluationInfo": {
        "segmentation": true
    }
}'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `fields` | Eine Liste der exportierten Felder, durch Kommas getrennt. Wenn leer gelassen, werden alle Felder exportiert. |
| `mergePolicy` | Gibt die Richtlinie zum Zusammenführen der exportierten Daten an. Schließen Sie diesen Parameter ein, wenn mehrere Segmente exportiert werden. Wenn nicht angegeben, wird für den Export dieselbe Zusammenführungsrichtlinie wie für das angegebene Segment verwendet. |
| `filter` | Ein Objekt, das die Segmente angibt, die je nach ID, Qualifikationszeit oder Erfassungszeit in den Exportauftrag aufgenommen werden, und zwar je nach den unten aufgeführten Untereigenschaften. Wenn leer gelassen, werden alle Daten exportiert. |
| `filter.segments` | Gibt die zu exportierenden Segmente an. Wird dieser Wert nicht angegeben, werden alle Daten aus allen Profilen exportiert. Akzeptiert ein Array von Segmentobjekten, die jeweils die folgenden Felder enthalten:<ul><li>`segmentId`:  **(Erforderlich bei Verwendung  `segments`)** Segment-ID für Profil, die exportiert werden sollen.</li><li>`segmentNs` *(Optional)* Segmentcode für den jeweiligen Namensraum  `segmentID`.</li><li>`status` *(Optional)* Ein Array von Zeichenfolgen, das einen Statusfilter für die  `segmentID`Variable bereitstellt. Standardmäßig hat `status` den Wert `["realized", "existing"]`, der alle Profil darstellt, die zum aktuellen Zeitpunkt in das Segment fallen. Mögliche Werte sind: `"realized"`, `"existing"` und `"exited"`.  Der Wert &quot;realisiert&quot;bedeutet, dass das Profil in das Segment eintritt. Der Wert &quot;vorhanden&quot;bedeutet, dass sich das Profil weiterhin im Segment befindet. Der Wert &quot;Beenden&quot;bedeutet, dass das Profil das Segment verlässt.</li></ul> |
| `filter.segmentQualificationTime` | Filtern Sie nach der Segmentqualifizierungszeit. Die Beginn- und/oder Endzeit können angegeben werden. |
| `filter.segmentQualificationTime.startTime` | Beginn des Segmentqualifizierungsstatus für eine Segment-ID für einen bestimmten Status. Es wurde nicht angegeben, es wird kein Filter für die Zeit des Beginns für eine Segment-ID-Qualifizierung angezeigt. Der Zeitstempel muss im Format [RFC 3339](https://tools.ietf.org/html/rfc3339) angegeben werden. |
| `filter.segmentQualificationTime.endTime` | Endzeit der Segmentqualifizierung für eine Segment-ID für einen bestimmten Status. Es wurde kein Filter für die Endzeit einer Segment-ID-Qualifizierung bereitgestellt. Der Zeitstempel muss im Format [RFC 3339](https://tools.ietf.org/html/rfc3339) angegeben werden. |
| `filter.fromIngestTimestamp ` | Beschränkt exportierte Profil auf nur diejenigen, die nach diesem Zeitstempel aktualisiert wurden. Der Zeitstempel muss im Format [RFC 3339](https://tools.ietf.org/html/rfc3339) angegeben werden. <ul><li>`fromIngestTimestamp` für  **Profile**, sofern vorhanden: Umfasst alle zusammengeführten Profil, bei denen der zusammengeführte aktualisierte Zeitstempel größer als der angegebene Zeitstempel ist. Unterstützt den Operanden `greater_than`.</li><li>`fromIngestTimestamp` für  **Ereignisse**: Alle nach diesem Zeitstempel erfassten Ereignis werden entsprechend dem resultierenden Profil exportiert. Dies ist nicht die Ereignis-Zeit selbst, sondern die Aufnahmezeit für die Ereignisse.</li> |
| `filter.emptyProfiles` | Ein boolescher Wert, der angibt, ob nach leeren Profilen gefiltert werden soll. Profil können Profil-Datensätze, ExperienceEvent-Datensätze oder beides enthalten. Profil ohne Profil-Datensätze und nur ExperienceEvent-Datensätze werden als &quot;emptyProfiles&quot;bezeichnet. Um alle Profil im Profil-Store, einschließlich &quot;emptyProfiles&quot;, zu exportieren, setzen Sie den Wert von `emptyProfiles` auf `true`. Wenn `emptyProfiles` auf `false` eingestellt ist, werden nur Profil mit Profil-Datensätzen im Store exportiert. Wenn das Attribut `emptyProfiles` nicht enthalten ist, werden standardmäßig nur Profil exportiert, die Profil-Datensätze enthalten. |
| `additionalFields.eventList` | Steuert die Zeitreihenfelder für Ereignisse, die für untergeordnete oder verknüpfte Objekte exportiert werden, indem eine oder mehrere der folgenden Einstellungen bereitgestellt werden:<ul><li>`fields`: Steuerung der zu exportierenden Felder.</li><li>`filter`: Gibt Kriterien an, die die Ergebnisse verknüpfter Objekte einschränken. Erwartet einen für den Export erforderlichen Mindestwert, normalerweise ein Datum.</li><li>`filter.fromIngestTimestamp`: Filter der Zeitreihen-Ereignis zu denen, die nach dem bereitgestellten Zeitstempel erfasst wurden. Dies ist nicht die Ereignis-Zeit selbst, sondern die Aufnahmezeit für die Ereignisse.</li><li>`filter.toIngestTimestamp`: Filter des Zeitstempels zu den Zeitstempeln, die vor dem angegebenen Zeitstempel erfasst wurden. Dies ist nicht die Ereignis-Zeit selbst, sondern die Aufnahmezeit für die Ereignisse.</li></ul> |
| `destination` | **(Erforderlich)** Informationen zu den exportierten Daten:<ul><li>`datasetId`:  **(Erforderlich)** Die ID des Datensatzes, in den Daten exportiert werden sollen.</li><li>`segmentPerBatch`:  *(Optional)* Ein boolescher Wert, der standardmäßig auf &quot;false&quot;gesetzt ist, wenn er nicht angegeben wird. Der Wert &quot;false&quot;exportiert alle Segment-IDs in eine einzelne Stapel-ID. Der Wert &quot;true&quot;exportiert eine Segment-ID in eine Stapel-ID. Beachten Sie, dass die Einstellung des Werts auf &quot;true&quot;die Exportleistung des Stapels beeinträchtigen kann.</li></ul> |
| `schema.name` | **(Erforderlich)** Der Name des Schemas, das mit dem Datensatz verknüpft ist, in den Daten exportiert werden sollen. |
| `evaluationInfo.segmentation` | *(Optional)* Ein boolescher Wert, der standardmäßig auf  `false`gesetzt wird, wenn er nicht angegeben wird. Der Wert `true` gibt an, dass die Segmentierung für den Exportauftrag durchgeführt werden muss. |

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

Wenn `destination.segmentPerBatch` auf `true` eingestellt wäre, hätte das `destination`-Objekt ein `batches`-Array, wie unten dargestellt:

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

Sie können detaillierte Informationen zu einem bestimmten Exportauftrag abrufen, indem Sie eine GET an den Endpunkt `/export/jobs` anfordern und die ID des Exportauftrags angeben, den Sie im Anforderungspfad abrufen möchten.

**API-Format**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | Der `id` des Exportauftrags, auf den Sie zugreifen möchten. |

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
| `destination` | Zielinformationen für die exportierten Daten:<ul><li>`datasetId`: Die ID des Datensatzes, in den die Daten exportiert wurden.</li><li>`segmentPerBatch`: Ein boolescher Wert, der angibt, ob Segment-IDs konsolidiert sind. Der Wert `false` bedeutet, dass alle Segment-IDs in einer einzigen Stapel-ID enthalten waren. Der Wert `true` bedeutet, dass eine Segment-ID in eine Stapel-ID exportiert wird.</li></ul> |
| `fields` | Eine Liste der exportierten Felder, durch Kommas getrennt. |
| `schema.name` | Der Name des mit dem Datensatz verknüpften Schemas, in das Daten exportiert werden sollen. |
| `filter.segments` | Die Segmente, die exportiert werden. Die folgenden Felder sind enthalten:<ul><li>`segmentId`: Segment-ID für zu exportierende Profil.</li><li>`segmentNs`: Segment-Namensraum für die angegebene  `segmentID`.</li><li>`status`: Ein Zeichenfolgen-Array, das einen Statusfilter für die  `segmentID`Zeichenfolge bereitstellt. Standardmäßig hat `status` den Wert `["realized", "existing"]`, der alle Profil darstellt, die zum aktuellen Zeitpunkt in das Segment fallen. Mögliche Werte sind: &quot;realisiert&quot;, &quot;vorhanden&quot;und &quot;beendet&quot;.  Der Wert &quot;realisiert&quot;bedeutet, dass das Profil in das Segment eintritt. Der Wert &quot;vorhanden&quot;bedeutet, dass sich das Profil weiterhin im Segment befindet. Der Wert &quot;Beenden&quot;bedeutet, dass das Profil das Segment verlässt.</li></ul> |
| `mergePolicy` | Richtlinieninformationen für die exportierten Daten zusammenführen |
| `metrics.totalTime` | Ein Feld, das die Gesamtdauer angibt, die der Exportauftrag gedauert hat. |
| `metrics.profileExportTime` | Ein Feld, das angibt, wie lange es gedauert hat, bis die Profil exportiert wurden. |
| `totalExportedProfileCounter` | Die Gesamtanzahl der Profile, die für alle Stapel exportiert wurden. |

## Bestimmten Exportauftrag abbrechen oder löschen {#delete}

Sie können anfordern, den angegebenen Exportauftrag zu löschen, indem Sie eine DELETE-Anforderung an den Endpunkt `/export/jobs` stellen und die ID des Exportauftrags angeben, den Sie im Anforderungspfad löschen möchten.

**API-Format**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | Der `id` des Exportauftrags, den Sie löschen möchten. |

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
