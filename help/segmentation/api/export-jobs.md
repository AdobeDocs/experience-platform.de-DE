---
solution: Experience Platform
title: API-Endpunkt für Segmentexportvorgänge
description: Exportvorgänge sind asynchrone Prozesse, mit denen Zielgruppensegmentmitglieder in Datensätzen persistiert werden. Sie können den Endpunkt /export/jobs in der Segmentierungs-Service-API von Adobe Experience Platform verwenden, mit der Sie Exportaufträge programmgesteuert abrufen, erstellen und abbrechen können.
role: Developer
exl-id: 5b504a4d-291a-4969-93df-c23ff5994553
source-git-commit: bf90e478b38463ec8219276efe71fcc1aab6b2aa
workflow-type: tm+mt
source-wordcount: '1678'
ht-degree: 11%

---

# Endpunkt für Segmentexportvorgänge

Exportvorgänge sind asynchrone Prozesse, mit denen Zielgruppensegmentmitglieder in Datensätzen persistiert werden. Sie können den `/export/jobs`-Endpunkt in der Adobe Experience Platform-Segmentierungs-API verwenden, mit der Sie Exportaufträge programmgesteuert abrufen, erstellen und abbrechen können.

>[!NOTE]
>
>In diesem Handbuch wird die Verwendung von Exportvorgängen in der [!DNL Segmentation API] behandelt. Informationen zum Verwalten von Exportvorgängen für [!DNL Real-Time Customer Profile]-Daten finden Sie im Handbuch [Exportvorgänge in der Profil-API](../../profile/api/export-jobs.md)

## Erste Schritte

Die in diesem Handbuch verwendeten Endpunkte sind Teil der [!DNL Adobe Experience Platform Segmentation Service]-API. Bevor Sie fortfahren, lesen Sie den Abschnitt [Erste Schritte](./getting-started.md). Dort erhalten Sie wichtige Informationen darüber, wie Sie die API aufrufen und die erforderlichen Kopfzeilen sowie Beispiele für API-Aufrufe lesen können.

## Liste mit Exportaufträgen abrufen {#retrieve-list}

Sie können eine Liste aller Exportvorgänge für Ihr Unternehmen abrufen, indem Sie eine GET-Anfrage an den `/export/jobs`-Endpunkt senden.

**API-Format**

Der `/export/jobs`-Endpunkt unterstützt verschiedene Abfrageparameter, mit denen Sie Ihre Ergebnisse filtern können. Obwohl diese Parameter optional sind, wird ihre Verwendung dringend empfohlen, um kostspieligen Aufwand zu reduzieren. Wenn Sie diesen Endpunkt ohne Parameter aufrufen, werden alle für Ihre Organisation verfügbaren Exportaufträge abgerufen. Es können mehrere Parameter eingeschlossen werden, die durch kaufmännische Und-Zeichen (`&`) voneinander getrennt werden.

```http
GET /export/jobs
GET /export/jobs?{QUERY_PARAMETERS}
```

**Abfrageparameter**

+++ Eine Liste der verfügbaren Abfrageparameter.

| Parameter | Beschreibung | Beispiel |
| --------- | ----------- | ------- |
| `limit` | Gibt die Zahl der zurückgegebenen Exportaufträge an. | `limit=10` |
| `offset` | Gibt den Versatz der Ergebnisseiten an. | `offset=1540974701302_96` |
| `status` | Filtert die Ergebnisse anhand ihres Status. Die unterstützten Werte sind „NEW“, „SUCCEEDED“ und „FAILED“. | `status=NEW` |

+++

**Anfrage**

Die folgende Anfrage ruft die letzten beiden Exportvorgänge innerhalb Ihrer Organisation ab.

+++ Eine Beispielanfrage zum Abrufen von Exportvorgängen.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Antwort**

Die folgende Antwort gibt den HTTP-Status-Code 200 mit einer Liste der erfolgreich abgeschlossenen Exportvorgänge zurück, basierend auf dem im Anfragepfad angegebenen Abfrageparameter.

+++ Eine Beispielantwort beim Abrufen von Exportvorgängen.

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
                        "status": ["realized"]
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
| `destination` | Zielinformationen für die exportierten Daten:<ul><li>`datasetId`: Die ID des Datensatzes, in den die Daten exportiert wurden.</li><li>`segmentPerBatch`: Ein boolescher Wert, der anzeigt, ob Segment-IDs konsolidiert werden oder nicht. Der Wert „false“ bedeutet, dass alle Segment-IDs in eine einzige Batch-ID exportiert werden. Der Wert „true“ bedeutet, dass eine Segment-ID in eine Batch-ID exportiert wird. **Hinweis** Wenn Sie für den Wert „true“ festlegen, kann sich dies auf die Leistung beim Batch-Export auswirken.</li></ul> |
| `fields` | Liste der exportierten Felder, durch Kommas getrennt |
| `schema.name` | Der Name des Schemas, das dem Datensatz zugeordnet ist, in den die Daten exportiert werden sollen. |
| `filter.segments` | Die exportierten Segmente. Die folgenden Felder sind enthalten:<ul><li>`segmentId`: Die Segment-ID, an die Profile exportiert werden.</li><li>`segmentNs`: Segment-Namespace für den angegebenen `segmentID`.</li><li>`status`: Ein Array von Zeichenfolgen, das einen Statusfilter für die `segmentID` bereitstellt. Standardmäßig haben `status` den Wert `["realized"]` , der alle Profile darstellt, die zum aktuellen Zeitpunkt in das Segment fallen. Mögliche Werte sind: `realized` und `exited`. Der Wert `realized` bedeutet, dass das Profil für das Segment qualifiziert ist. Der Wert `exiting` bedeutet, dass das Profil das Segment verlässt.</li></ul> |
| `mergePolicy` | Informationen zu Zusammenführungsrichtlinien für die exportierten Daten. |
| `metrics.totalTime` | Ein Feld, das die Gesamtzeit angibt, die für die Ausführung des Exportvorgangs benötigt wurde. |
| `metrics.profileExportTime` | Ein Feld, das die Zeit angibt, die für den Export der Profile benötigt wurde. |
| `page` | Informationen zur Paginierung der angeforderten Exportvorgänge. |
| `link.next` | Ein Link zur nächsten Seite mit Exportvorgängen. |

+++

## Neuen Exportauftrag erstellen {#create}

Sie können einen neuen Exportauftrag erstellen, indem Sie eine POST-Anfrage an den `/export/jobs`-Endpunkt senden.

**API-Format**

```http
POST /export/jobs
```

**Anfrage**

Die folgende Anfrage erstellt einen neuen Exportvorgang, der durch die in der Payload angegebenen Parameter konfiguriert wird.

+++ Beispielanfrage zum Erstellen eines Exportvorgangs.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/export/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `mergePolicy` | Gibt die Zusammenführungsrichtlinie für die exportierten Daten an. Schließen Sie diesen Parameter ein, wenn mehrere Segmente exportiert werden. Wenn nicht angegeben, wird für den Export dieselbe Zusammenführungsrichtlinie wie für das angegebene Segment verwendet. |
| `filter` | Ein -Objekt, das die Segmente angibt, die je nach ID, Qualifizierungszeit oder Aufnahmezeit in den Exportvorgang aufgenommen werden sollen, und zwar abhängig von den unten aufgeführten Untereigenschaften. Wenn leer gelassen, werden alle Daten exportiert. |
| `filter.segments` | Gibt die zu exportierenden Segmente an. Wenn Sie diesen Wert weglassen, werden alle Daten aus allen Profilen exportiert. Akzeptiert ein Array von Segmentobjekten, die jeweils die folgenden Felder enthalten:<ul><li>`segmentId`: **(erforderlich bei Verwendung von `segments`)** Segment-ID für zu exportierende Profile.</li><li>`segmentNs` *(Optional)* Segment-Namespace für den angegebenen `segmentID`.</li><li>`status` *(Optional)* Ein Array von Zeichenfolgen, das einen Statusfilter für die `segmentID` bereitstellt. Standardmäßig haben `status` den Wert `["realized"]` , der alle Profile darstellt, die zum aktuellen Zeitpunkt in das Segment fallen. Mögliche Werte sind: `realized` und `exited`.  Der Wert `realized` bedeutet, dass das Profil für das Segment qualifiziert ist. Der Wert `exiting` bedeutet, dass das Profil das Segment verlässt.</li></ul> |
| `filter.segmentQualificationTime` | Filtern Sie nach der Segmentqualifikationszeit. Die Start- und/oder Endzeit kann angegeben werden. |
| `filter.segmentQualificationTime.startTime` | Startzeit der Segmentqualifizierung für eine Segment-ID für einen bestimmten Status. Wenn dies nicht angegeben ist, gibt es keinen Filter zur Startzeit für eine Segment-ID-Qualifizierung. Der Zeitstempel muss im Format [RFC 3339](https://tools.ietf.org/html/rfc3339) angegeben werden. |
| `filter.segmentQualificationTime.endTime` | Endzeit der Segmentqualifizierung für eine Segment-ID für einen bestimmten Status. Ist dies nicht angegeben, gibt es keinen Filter zur Endzeit für eine Segment-ID-Qualifizierung. Der Zeitstempel muss im Format [RFC 3339](https://tools.ietf.org/html/rfc3339) angegeben werden. |
| `filter.fromIngestTimestamp ` | Beschränkt exportierte Profile auf diejenigen, die nach diesem Zeitstempel aktualisiert wurden. Der Zeitstempel muss im Format [RFC 3339](https://tools.ietf.org/html/rfc3339) angegeben werden. <ul><li>`fromIngestTimestamp` für **Profile**, falls angegeben: Umfasst alle zusammengeführten Profile, bei denen der aktualisierte zusammengeführte Zeitstempel größer als der angegebene Zeitstempel ist. Unterstützt `greater_than` Operanden.</li><li>`fromIngestTimestamp` für **Ereignisse**: Alle nach diesem Zeitstempel aufgenommenen Ereignisse werden entsprechend dem resultierenden Profilergebnis exportiert. Dies ist nicht die Ereigniszeit selbst, sondern die Aufnahmezeit für die Ereignisse.</li> |
| `filter.emptyProfiles` | Ein boolescher Wert, der angibt, ob nach leeren Profilen gefiltert werden soll. Profile können Profildatensätze, ExperienceEvent-Datensätze oder beides enthalten. Profile ohne Profildatensätze und nur ExperienceEvent-Datensätze werden als „emptyProfiles“ bezeichnet. Um alle Profile im Profilspeicher zu exportieren, einschließlich „emptyProfiles“, setzen Sie den Wert von `emptyProfiles` auf `true`. Wenn `emptyProfiles` auf `false` gesetzt ist, werden nur Profile mit Profildatensätzen im Speicher exportiert. Wenn `emptyProfiles` Attribut nicht enthalten ist, werden standardmäßig nur Profile exportiert, die Profildatensätze enthalten. |
| `additionalFields.eventList` | Steuert die Zeitreihen-Ereignisfelder, die für untergeordnete oder zugehörige Objekte exportiert werden, indem eine oder mehrere der folgenden Einstellungen bereitgestellt werden:<ul><li>`fields`: Steuern der zu exportierenden Felder.</li><li>`filter`: Gibt Kriterien an, die die Ergebnisse der zugeordneten Objekte einschränken. Erwartet einen für den Export erforderlichen Mindestwert, in der Regel ein Datum.</li><li>`filter.fromIngestTimestamp`: Filtert Zeitreihenereignisse nach denen, die nach dem angegebenen Zeitstempel aufgenommen wurden. Dies ist nicht die Ereigniszeit selbst, sondern die Aufnahmezeit für die Ereignisse.</li><li>`filter.toIngestTimestamp`: Filtert den Zeitstempel nach denen, die vor dem angegebenen Zeitstempel aufgenommen wurden. Dies ist nicht die Ereigniszeit selbst, sondern die Aufnahmezeit für die Ereignisse.</li></ul> |
| `destination` | **(Erforderlich)** Informationen zu den exportierten Daten:<ul><li>`datasetId`: **(Erforderlich)** Die ID des Datensatzes, in den Daten exportiert werden sollen.</li><li>`segmentPerBatch`: *(Optional)* Ein boolescher Wert, der, wenn er nicht angegeben wird, standardmäßig auf „false“ festgelegt wird. Mit dem Wert „false“ werden alle Segment-IDs in eine einzige Batch-ID exportiert. Beim Wert „true“ wird eine Segment-ID in eine Batch-ID exportiert. Beachten Sie, dass sich das Festlegen des Werts auf „true“ auf die Batch-Exportleistung auswirken kann.</li></ul> |
| `schema.name` | **(Erforderlich)** Der Name des Schemas, das mit dem Datensatz verknüpft ist, in den Daten exportiert werden sollen. |
| `evaluationInfo.segmentation` | *(Optional)* Ein boolescher Wert, der, falls nicht angegeben, standardmäßig auf `false` festgelegt wird. Der Wert `true` gibt an, dass für den Exportvorgang eine Segmentierung durchgeführt werden muss. |

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zu Ihrem neu erstellten Exportauftrag zurück.

+++ Beispielantwort beim Erstellen eines Exportvorgangs.

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
    "imsOrgId": "{ORG_ID}",
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
| `id` | Ein systemgenerierter schreibgeschützter Wert, der den soeben erstellten Exportvorgang identifiziert. |

Wenn `destination.segmentPerBatch` auf &quot;`true`&quot; festgelegt worden wäre, hätte das obige `destination` alternativ ein `batches`-Array, wie unten dargestellt:

```json
    "destination": {
        "dataSetId": "{DATASET_ID}",
        "segmentPerBatch": true,
        "batches": [
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

+++

## Bestimmten Exportauftrag abrufen {#get}

Sie können detaillierte Informationen zu einem bestimmten Exportvorgang abrufen, indem Sie eine GET-Anfrage an den `/export/jobs`-Endpunkt senden und im Anfragepfad die ID des Exportvorgangs angeben, den Sie abrufen möchten.

**API-Format**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | Die `id` des Exportvorgangs, auf den Sie zugreifen möchten. |

**Anfrage**

+++ Eine Beispielanfrage zum Abrufen eines Exportvorgangs.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/11037 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit genauen Informationen zum angegebenen Exportauftrag zurück.

+++ Beispielantwort beim Abrufen eines Exportvorgangs.

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
    "imsOrgId": "{ORG_ID}",
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
| `destination` | Zielinformationen für die exportierten Daten:<ul><li>`datasetId`: Die ID des Datensatzes, in den die Daten exportiert wurden.</li><li>`segmentPerBatch`: Ein boolescher Wert, der anzeigt, ob Segment-IDs konsolidiert werden oder nicht. Der Wert `false` bedeutet, dass alle Segment-IDs in einer einzigen Batch-ID zusammengefasst wurden. Der Wert `true` bedeutet, dass eine Segment-ID in eine Batch-ID exportiert wird.</li></ul> |
| `fields` | Liste der exportierten Felder, durch Kommas getrennt |
| `schema.name` | Der Name des Schemas, das dem Datensatz zugeordnet ist, in den die Daten exportiert werden sollen. |
| `filter.segments` | Die exportierten Segmente. Die folgenden Felder sind enthalten:<ul><li>`segmentId`: Segment-ID für zu exportierende Profile.</li><li>`segmentNs`: Segment-Namespace für den angegebenen `segmentID`.</li><li>`status`: Ein Array von Zeichenfolgen, das einen Statusfilter für die `segmentID` bereitstellt. Standardmäßig haben `status` den Wert `["realized"]` , der alle Profile darstellt, die zum aktuellen Zeitpunkt in das Segment fallen. Mögliche Werte sind: `realized` und `exited`.  Der Wert `realized` bedeutet, dass das Profil für das Segment qualifiziert ist. Der Wert `exiting` bedeutet, dass das Profil das Segment verlässt.</li></ul> |
| `mergePolicy` | Informationen zu Zusammenführungsrichtlinien für die exportierten Daten. |
| `metrics.totalTime` | Ein Feld, das die Gesamtzeit angibt, die für die Ausführung des Exportvorgangs benötigt wurde. |
| `metrics.profileExportTime` | Ein Feld, das die Zeit angibt, die für den Export der Profile benötigt wurde. |
| `totalExportedProfileCounter` | Die Gesamtzahl der exportierten Profile in allen Stapeln. |

+++

## Bestimmten Exportauftrag abbrechen oder löschen {#delete}

Sie können das Löschen des angegebenen Exportvorgangs anfordern, indem Sie eine DELETE-Anfrage an den `/export/jobs`-Endpunkt senden und im Anfragepfad die ID des Exportvorgangs angeben, den Sie löschen möchten.

**API-Format**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | Die `id` des Exportvorgangs, den Sie löschen möchten. |

**Anfrage**

+++ Eine Beispielanfrage zum Löschen eines Exportvorgangs.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/export/jobs/{EXPORT_JOB_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 mit der folgenden Meldung zurück:

```json
{
  "status": true,
  "message": "Export job has been marked for cancelling"
}
```

## Nächste Schritte

Nach dem Lesen dieses Handbuchs wissen Sie jetzt besser, wie Exportvorgänge funktionieren.
