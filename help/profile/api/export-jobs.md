---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Exportaufträge - Echtzeit-Client-Profil-API
topic: guide
translation-type: tm+mt
source-git-commit: 2c0466bf0534d09e3cad54caef213def122d948b
workflow-type: tm+mt
source-wordcount: '1494'
ht-degree: 7%

---


# Endpunkt für Exportaufträge

[!DNL Real-time Customer Profile] ermöglicht Ihnen die Erstellung einer einzelnen Ansicht einzelner Kunden durch Zusammenführen von Daten aus mehreren Quellen, einschließlich Attributdaten und Verhaltensdaten. Daten, die innerhalb des Datenbestands verfügbar sind, [!DNL Profile] können dann zur weiteren Verarbeitung in einen Datensatz exportiert werden. So können z. B. Audiencen aus [!DNL Profile] Daten zur Aktivierung exportiert und Profil-Attribute zum Berichte exportiert werden.

Dieses Dokument enthält schrittweise Anweisungen zum Erstellen und Verwalten von Exportaufträgen mit der [Profil-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml).

>[!NOTE]
>
>Dieses Handbuch behandelt die Verwendung von Exportaufträgen in der [!DNL Profile API]. Informationen zum Verwalten von Exportaufträgen für den Segmentierungsdienst für Adobe Experience Platformen finden Sie im Handbuch zu [Exportaufträgen in der Segmentierungs-API](../../profile/api/export-jobs.md).

Neben der Erstellung eines Exportauftrags können Sie auch über den [!DNL Profile] Endpunkt, auch als &quot; `/entities` &quot;bezeichnet, auf[!DNL Profile Access]Daten zugreifen. See the [entities endpoint guide](./entities.md) for more information. Anweisungen zum Zugriff auf [!DNL Profile] Daten mithilfe der Benutzeroberfläche finden Sie im [Benutzerhandbuch](../ui/user-guide.md).

## Erste Schritte

The API endpoints used in this guide are part of the [!DNL Real-time Customer Profile] API. Bevor Sie fortfahren, lesen Sie bitte die [Anleitung](getting-started.md) zu den ersten Schritten für Links zur zugehörigen Dokumentation, eine Anleitung zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtige Informationen zu den erforderlichen Kopfzeilen, die zum erfolgreichen Aufrufen einer beliebigen [!DNL Experience Platform] API erforderlich sind.

## Erstellen eines Exportauftrags

Exporting [!DNL Profile] data requires first creating a dataset into which the data will be exported, then initiating a new export job. Beide Schritte können mit Experience Platform-APIs durchgeführt werden, wobei erstere die Katalogdienst-API und letztere die Echtzeit-Customer-Profil-API verwenden. Detaillierte Anweisungen zum Abschluss der einzelnen Schritte finden Sie in den folgenden Abschnitten.

### Zielgruppen-Dataset erstellen

Beim Exportieren von [!DNL Profile] Daten muss zunächst ein Zielgruppe-Datensatz erstellt werden. Es ist wichtig, dass der Datensatz korrekt konfiguriert wird, um sicherzustellen, dass der Export erfolgreich ist.

Eine der wichtigsten Überlegungen ist das Schema, auf dem der Datensatz basiert (`schemaRef.id` in der unten stehenden API-Musteranforderung). Um Profil-Daten zu exportieren, muss der Datensatz auf dem Schema &quot; [!DNL XDM Individual Profile] Vereinigung&quot;(`https://ns.adobe.com/xdm/context/profile__union`) basieren. Ein Vereinigung-Schema ist ein systemgeneriertes, schreibgeschütztes Schema, das die Felder von Schemas, die dieselbe Klasse gemeinsam haben, Aggregat. In diesem Fall ist das die [!DNL XDM Individual Profile] Klasse. Weitere Informationen zu Schemas zur Ansicht der Vereinigung finden Sie im Abschnitt &quot; [Vereinigung&quot;im Handbuch](../../xdm/schema/composition.md#union)&quot;Grundlagen der Erstellung von Schemas&quot;.

In den folgenden Schritten wird beschrieben, wie Sie einen Datensatz erstellen, der auf das Schema &quot; [!DNL XDM Individual Profile] Vereinigung&quot;mithilfe der [!DNL Catalog] API verweist. Sie können auch die [!DNL Platform] Benutzeroberfläche verwenden, um einen Datensatz zu erstellen, der auf das Schema &quot;Vereinigung&quot;verweist. Die Schritte zur Verwendung der Benutzeroberfläche werden in [diesem UI-Lernprogramm zum Exportieren von Segmenten](../../segmentation/tutorials/create-dataset-export-segment.md) beschrieben, aber auch hier. Nach Abschluss können Sie zu diesem Lernprogramm zurückkehren, um mit den Schritten zum [Starten eines neuen Exportauftrags](#initiate)fortzufahren.

Wenn Sie bereits über einen kompatiblen Datensatz verfügen und dessen ID kennen, können Sie direkt mit dem Schritt zum [Initiieren eines neuen Exportauftrags](#initiate)fortfahren.

**API-Format**

```http
POST /dataSets
```

**Anfrage**

Mit der folgenden Anforderung wird ein neuer Datensatz erstellt, der Konfigurationsparameter in der Nutzlast bereitstellt.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Profile Data Export",
        "schemaRef": {
          "id": "https://ns.adobe.com/xdm/context/profile__union",
          "contentType": "application/vnd.adobe.xed+json;version=1"
        },
        "fileDescription": {
          "persisted": true,
          "containerFormat": "parquet",
          "format": "parquet"
        }
      }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `name` | Ein beschreibender Name für den Datensatz. |
| `schemaRef.id` | Die ID der Vereinigung-Ansicht (Schema), der der Datensatz zugeordnet werden soll. |
| `fileDescription.persisted` | Ein boolescher Wert, der bei Festlegung auf `true`die Persistenz des Datensatzes in der Ansicht &quot;Vereinigung&quot;ermöglicht. |

**Antwort**

Eine erfolgreiche Antwort gibt ein Array zurück, das die schreibgeschützte, systemgenerierte eindeutige ID des neu erstellten Datensatzes enthält. Für den erfolgreichen Export von Profil-Daten ist eine ordnungsgemäß konfigurierte Dataset-ID erforderlich.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Exportauftrag starten {#initiate}

Sobald Sie über einen Datensatz mit Vereinigung-Speicherung verfügen, können Sie einen Exportauftrag erstellen, um die Profil-Daten an den Datensatz zu erhalten, indem Sie eine POST-Anforderung an den `/export/jobs` Endpunkt in der Echtzeit-Client-Profil-API senden und die Details der Daten angeben, die Sie im Hauptteil der Anforderung exportieren möchten.

**API-Format**

```http
POST /export/jobs
```

**Anfrage**

Mit der folgenden Anforderung wird ein neuer Exportauftrag erstellt, der Konfigurationsparameter in der Nutzlast bereitstellt.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "additionalFields" : {
      "eventList": {
        "fields": "environment.browserDetails.name,environment.browserDetails.version",
        "filter": {
          "fromIngestTimestamp": "2018-10-25T13:22:04-07:00"
        }
      }
    }
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": false
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }' 
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `fields` | *(Optional)* Beschränkt die Datenfelder, die in den Export einbezogen werden sollen, auf die in diesem Parameter bereitgestellten Felder. Wird dieser Wert nicht angegeben, werden alle Felder in die exportierten Daten einbezogen. |
| `mergePolicy` | *(Optional)* Gibt die Richtlinie zum Zusammenführen an, die für die exportierten Daten gilt. Schließen Sie diesen Parameter ein, wenn mehrere Segmente exportiert werden. |
| `mergePolicy.id` | Die ID der Zusammenführungsrichtlinie. |
| `mergePolicy.version` | Die spezifische Version der zu verwendenden Mergerichtlinie. Wenn Sie diesen Wert auslassen, wird standardmäßig die neueste Version verwendet. |
| `additionalFields.eventList` | *(Optional)* Steuert die Zeitreihen-Ereignis-Felder, die für untergeordnete oder verknüpfte Objekte exportiert werden, indem eine oder mehrere der folgenden Einstellungen bereitgestellt werden:<ul><li>`eventList.fields`: Steuerung der zu exportierenden Felder.</li><li>`eventList.filter`: Gibt Kriterien an, die die Ergebnisse verknüpfter Objekte einschränken. Erwartet einen für den Export erforderlichen Mindestwert, normalerweise ein Datum.</li><li>`eventList.filter.fromIngestTimestamp`: Filter der Zeitreihen-Ereignis zu denen, die nach dem bereitgestellten Zeitstempel erfasst wurden. Dies ist nicht die Ereignis-Zeit selbst, sondern die Aufnahmezeit für die Ereignisse.</li></ul> |
| `destination` | **(Erforderlich)** Zielinformationen für die exportierten Daten:<ul><li>`destination.datasetId`: **(Erforderlich)** Die ID des Datensatzes, in den Daten exportiert werden sollen.</li><li>`destination.segmentPerBatch`: *(Optional)* Ein boolescher Wert, der, falls nicht angegeben, standardmäßig `false`lautet. Beim Wert `false` werden alle Segment-IDs in eine einzige Stapel-ID exportiert. Ein Wert von `true` exportiert eine Segment-ID in eine Stapel-ID. Beachten Sie, dass die Einstellung des Werts sich auf die Exportleistung des Stapels auswirken `true` kann.</li></ul> |
| `schema.name` | **(Erforderlich)** Der Name des Schemas, das mit dem Datensatz verknüpft ist, in den Daten exportiert werden sollen. |

>[!NOTE] Um nur Profil-Daten zu exportieren und keine zugehörigen Zeitreihendaten einzubeziehen, entfernen Sie das Objekt &quot;additionalFields&quot;aus der Anforderung.

**Antwort**

Eine erfolgreiche Antwort gibt einen Datensatz zurück, der mit den in der Anforderung angegebenen Profil-Daten gefüllt ist.

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "NEW",
    "requestId": "IwkVcD4RupdSmX376OBVORvcvTdA4ypN",
    "computeGatewayJobId": {},
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1559674261657
        }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": false,
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

## Liste aller Exportaufträge

You can return a list of all export jobs for a particular IMS Organization by performing a GET request to the `export/jobs` endpoint. Die Anforderung unterstützt auch die Abfrage Parameter `limit` und `offset`, wie unten dargestellt.

**API-Format**

```http
GET /export/jobs
GET /export/jobs?{QUERY_PARAMETERS}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `start` | Versatz der Seite mit den zurückgegebenen Ergebnissen, unter Berücksichtigung der Erstellungszeit der Anfrage. Beispiel: `start=4` |
| `limit` | Schränkt die Anzahl der zurückgegebenen Ergebnisse ein. Beispiel: `limit=10` |
| `page` | Gibt eine bestimmte Seite mit Ergebnissen zurück, unter Berücksichtigung der Erstellungszeit der Anfrage. Beispiel: `page=2` |
| `sort` | Sortiert Ergebnisse nach einem bestimmten Feld in aufsteigender (**`asc`**) oder absteigender (**`desc`**) Reihenfolge. Der Sortierparameter funktioniert nicht, wenn mehrere Ergebnisseiten zurückgegeben werden. Beispiel: `sort=updateTime:asc` |

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Antwort**

Die Antwort enthält ein `records` Objekt, das die von Ihrer IMS-Organisation erstellten Exportaufträge enthält.

```json
{
  "records": [
    {
      "profileInstanceId": "ups",
      "jobType": "BATCH",
      "id": 726,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "timestampOrdered-none-mp",
          "version": 1
      },
      "status": "SUCCEEDED",
      "requestId": "d995479c-8a08-4240-903b-af469c67be1f",
      "computeGatewayJobId": {
          "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
          "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538615973895,
              "endTimeInMs": 1538616233239,
              "totalTimeInMs": 259344
          },
          "profileExportTime": {
              "startTimeInMs": 1538616067445,
              "endTimeInMs": 1538616139576,
              "totalTimeInMs": 72131
          },
          "aCPDatasetWriteTime": {
              "startTimeInMs": 1538616195172,
              "endTimeInMs": 1538616195715,
              "totalTimeInMs": 543
          }
      },
      "destination": {
          "datasetId": "5b7c86968f7b6501e21ba9df",
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
      },
      "updateTime": 1538616233239,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538615973895
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
                "segmentId": "7a93d2ff-a220-4bae-9a4e-5f3c35032be3"
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
          "batchId": ""
      },
      "updateTime": 1538573922551,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538573416687
    }
  ],
  "page": {
      "sortField": "createdTime",
      "sort": "desc",
      "pageOffset": "1538573416687_722",
      "pageSize": 2
  },
  "link": {
      "next": "/export/jobs/?limit=2&offset=1538573416687_722"
  }
}
```

## Überwachung des Exportfortschritts

Um die Details eines bestimmten Exportauftrags Ansicht oder dessen Status während der Verarbeitung zu überwachen, können Sie eine GET-Anforderung an den `/export/jobs` Endpunkt senden und die Angabe `id` des Exportauftrags in den Pfad einschließen. Der Exportauftrag ist abgeschlossen, sobald das `status` Feld den Wert &quot;SUCCEEDED&quot;zurückgibt.

**API-Format**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | The `id` of the export job you want to access. |

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/24115 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "SUCCEEDED",
    "requestId": "YwMt1H8QbVlGT2pzyxgwFHTwzpMbHrTq",
    "computeGatewayJobId": {
      "exportJob": "305a2e5c-2cf3-4746-9b3d-3c5af0437754",
      "pushJob": "963f275e-91a3-4fa1-8417-d2ca00b16a8a"
    },
    "metrics": {
      "totalTime": {
        "startTimeInMs": 1547053539564,
        "endTimeInMs": 1547054743929,
        "totalTimeInMs": 1204365
      },
      "profileExportTime": {
        "startTimeInMs": 1547053667591,
        "endTimeInMs": 1547053778195,
        "totalTimeInMs": 110604
      },
      "aCPDatasetWriteTime": {
        "startTimeInMs": 1547054660416,
        "endTimeInMs": 1547054698918,
        "totalTimeInMs": 38502
      }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": false,
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `batchId` | Die Kennung der Stapel, die aus einem erfolgreichen Export erstellt wurden und für Nachschlagezwecke beim Lesen von Profil-Daten verwendet werden. |

## Abbrechen eines Exportauftrags

Mit der Experience Platform können Sie einen vorhandenen Exportauftrag stornieren. Dies kann aus verschiedenen Gründen nützlich sein, z. B. wenn der Exportauftrag nicht abgeschlossen wurde oder in der Verarbeitungsstufe hängen geblieben ist. In order to cancel an export job, you can perform a DELETE request to the `/export/jobs` endpoint and include the `id` of the export job that you wish to cancel to the request path.

**API-Format**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | The `id` of the export job you want to access. |

**Anfrage**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs/726 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Löschanforderung werden HTTP-Status 204 (Kein Inhalt) und ein leerer Antworttext zurückgegeben, der angibt, dass der Vorgang &quot;Abbrechen&quot;erfolgreich war.

## Nächste Schritte

Nach erfolgreichem Abschluss des Exports sind Ihre Daten im Data Lake in der Experience Platform verfügbar. Sie können dann mit der [Datenzugriff-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) auf die Daten zugreifen, indem Sie die mit dem Export verknüpfte `batchId` Datei verwenden. Je nach Größe des Exports können die Daten in Blöcken vorliegen und der Stapel kann aus mehreren Dateien bestehen.

Eine schrittweise Anleitung zum Zugriff auf und Herunterladen von Stapeldateien mit der Datenzugriff-API finden Sie im Lernprogramm [Datenzugriff](../../data-access/tutorials/dataset-data.md).

Sie können auch über den Adobe Experience Platform Abfrage Service auf erfolgreich exportierte Echtzeit-Kundendaten zugreifen. Mithilfe der Benutzeroberfläche oder RESTful-API können Sie mit dem Abfrage Service Abfragen für Daten im Data Lake schreiben, überprüfen und ausführen.

Weitere Informationen zur Abfrage von Audiencen finden Sie in der Dokumentation zum [Abfrage Service](../../query-service/home.md).

## Anhang

Im folgenden Abschnitt finden Sie weitere Informationen zu Exportaufträgen in der Profil-API.

### Zusätzliche Beispiele für die Exportnutzlast

Der API-Beispielaufruf, der im Abschnitt zum [Initiieren eines Exportauftrags](#initiate) angezeigt wird, erstellt einen Auftrag, der sowohl Profil- (Datensatz-) als auch Ereignis- (Zeitreihendaten) enthält. Dieser Abschnitt enthält zusätzliche Anforderungs-Nutzlastbeispiele, um den Export auf den einen Datentyp oder den anderen zu beschränken.

Die folgende Nutzlast erstellt einen Exportauftrag, der nur Profil-Daten (keine Ereignis) enthält:

```json
{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": false
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }
```

Um einen Exportauftrag zu erstellen, der nur Ereignis-Daten enthält (keine Profil-Attribute), sieht die Nutzlast möglicherweise wie folgt aus:

```json
{
    "fields": "identityMap",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "additionalFields" : {
      "eventList": {
        "fields": "environment.browserDetails.name,environment.browserDetails.version",
        "filter": {
          "fromIngestTimestamp": "2018-10-25T13:22:04-07:00"
        }
      }
    },
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": false
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }
```

### Exportieren von Segmenten

Sie können den Endpunkt &quot;Exportaufträge&quot;auch verwenden, um Audiencen- statt [!DNL Profile] Daten-Segmente zu exportieren. Weitere Informationen finden Sie im Handbuch zu [Exportaufträgen in der Segmentierungs-API](../../segmentation/api/export-jobs.md) .