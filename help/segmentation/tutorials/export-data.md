---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Daten mit APIs exportieren
topic: tutorial
translation-type: tm+mt
source-git-commit: d0b9223aebca0dc510a7457e5a5c65ac4a567933
workflow-type: tm+mt
source-wordcount: '1953'
ht-degree: 1%

---


# Exportieren von Profil-Daten mit APIs

Echtzeit-Kundendaten ermöglichen es Ihnen, eine Ansicht einzelner Kunden zu erstellen, indem Daten aus mehreren Quellen, einschließlich Attributdaten und Verhaltensdaten, zusammengeführt werden. Innerhalb von Profil verfügbare Daten können dann zur weiteren Verarbeitung in einen Datensatz exportiert werden. Dieses Lernprogramm enthält schrittweise Anweisungen zum Erstellen und Verwalten von Exportaufträgen mithilfe der [Segmentierungs-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml).

Neben der Erstellung eines Exportauftrags können Sie auch über die Profil Access API und Projektionen auf Profil-Daten zugreifen. Weitere Informationen zu diesen anderen Zugriffsmustern finden Sie im Tutorial [zur](../../profile/api/entities.md) Profil Access API oder im Tutorial zur [Konfiguration von Edge-Zielen und Projektionen](../../profile/api/edge-projections.md) .

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der verschiedenen Adobe Experience Platform-Dienste, die beim Arbeiten mit Profil-Daten erforderlich sind. Bevor Sie mit diesem Lernprogramm beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [Echtzeit-Profil](../../profile/home.md): Bietet ein einheitliches, kundenspezifisches Profil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.
- [Adobe Experience Platform Segmentation Service](../home.md): Ermöglicht Ihnen das Erstellen von Segmenten für Audiencen aus Echtzeitdaten zum Profil von Kunden.
- [Erlebnisdatenmodell (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem Plattform Kundenerlebnisdaten organisiert.
- [Sandboxen](../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Plattforminstanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

### Erforderliche Kopfzeilen

Für dieses Lernprogramm müssen Sie außerdem das [Authentifizierungstraining](../../tutorials/authentication.md) abgeschlossen haben, um Platform-APIs erfolgreich aufzurufen. Das Abschließen des Authentifizierungstreutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform API-Aufrufen bereit, wie unten dargestellt:

- Genehmigung: Träger `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in Experience Platform werden zu bestimmten virtuellen Sandboxen isoliert. Anforderungen an Plattform-APIs erfordern einen Header, der den Namen der Sandbox angibt, in der der Vorgang stattfindet:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Weitere Informationen zu Sandboxes in Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Für alle POST-, PUT- und PATCH-Anforderungen ist ein zusätzlicher Header erforderlich:

- Content-Type: application/json

## Erstellen eines Exportauftrags

Für das Exportieren von Profil-Daten muss zunächst ein Datensatz erstellt werden, in den die Daten exportiert werden, und dann ein neuer Exportauftrag initiiert werden. Beide Schritte können mit Experience Platform-APIs durchgeführt werden, wobei erstere die Catalog Service API und letztere die Real-time Customer Profil API verwenden. Detaillierte Anweisungen zum Abschluss der einzelnen Schritte finden Sie in den folgenden Abschnitten.

- [Zielgruppe-Datensatz](#create-a-target-dataset) erstellen - Erstellen Sie einen Datensatz, der exportierte Daten enthält.
- [Einen neuen Exportauftrag](#initiate-export-job) starten: Füllen Sie den Datensatz mit den Daten des individuellen XDM-Profils.

### Zielgruppen-Dataset erstellen

Beim Exportieren von Profil-Daten muss zunächst ein Zielgruppe-Datensatz erstellt werden. Es ist wichtig, dass der Datensatz korrekt konfiguriert wird, um sicherzustellen, dass der Export erfolgreich ist.

Eine der wichtigsten Überlegungen ist das Schema, auf dem der Datensatz basiert (`schemaRef.id` in der unten stehenden API-Musteranforderung). Um ein Segment zu exportieren, muss der Datensatz auf dem XDM Individual Profil Vereinigung Schema (`https://ns.adobe.com/xdm/context/profile__union`) basieren. Ein Vereinigung-Schema ist ein systemgeneriertes, schreibgeschütztes Schema, das die Felder von Schemas, die dieselbe Klasse besitzen, Aggregat gibt, in diesem Fall die XDM-Klasse Individuelles Profil. Weitere Informationen zu Schemas der Vereinigung Ansicht finden Sie im Abschnitt zum [Echtzeit-Kundenmanagement im Schema Registry-Entwicklerhandbuch](../../xdm/schema/composition.md#union).

In den folgenden Schritten wird beschrieben, wie Sie ein Dataset erstellen, das auf das Schema zur Vereinigung einzelner XDM-Profil mithilfe der Katalog-API verweist. Sie können auch die Benutzeroberfläche von Adobe Experience Platform verwenden, um einen Datensatz zu erstellen, der auf das Schema der Vereinigung verweist. Die Schritte zur Verwendung der Benutzeroberfläche werden in [diesem UI-Lernprogramm zum Exportieren von Segmenten](./create-dataset-export-segment.md) beschrieben, aber auch hier. Nach Abschluss können Sie zu diesem Lernprogramm zurückkehren, um mit den Schritten zum [Starten eines neuen Exportauftrags](#initiate-export-job)fortzufahren.

Wenn Sie bereits über einen kompatiblen Datensatz verfügen und dessen ID kennen, können Sie direkt mit dem Schritt zum [Initiieren eines neuen Exportauftrags](#initiate-export-job)fortfahren.

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

### Exportauftrag starten

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
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ],
      "segmentQualificationTime": {
            "startTime": "2019-09-01T00:00:00Z",
            "endTime": "2019-09-02T00:00:00Z"
        },
      "fromIngestTimestamp": "2018-10-25T13:22:04-07:00",
      "emptyProfiles": false
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
      "segmentPerBatch": true
    },
    "schema": {
      "name": "_xdm.context.profile"
    },
    "evaluationInfo": {
        "segmentation": true
    }
  }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `fields` | *(Optional)* Beschränkt die Datenfelder, die in den Export einbezogen werden sollen, auf die in diesem Parameter bereitgestellten Felder. Derselbe Parameter ist auch bei der Erstellung eines Segments verfügbar. Daher wurden die Felder im Segment möglicherweise bereits gefiltert. Wird dieser Wert nicht angegeben, werden alle Felder in die exportierten Daten einbezogen. |
| `mergePolicy` | *(Optional)* Gibt die Richtlinie zum Zusammenführen an, die für die exportierten Daten gilt. Schließen Sie diesen Parameter ein, wenn mehrere Segmente exportiert werden. Wird dieser Wert nicht angegeben, verwendet der Exportdienst die vom Segment bereitgestellte Mergerichtlinie. |
| `mergePolicy.id` | Die ID der Zusammenführungsrichtlinie. |
| `mergePolicy.version` | Die spezifische Version der zu verwendenden Mergerichtlinie. Wenn Sie diesen Wert auslassen, wird standardmäßig die neueste Version verwendet. |
| `filter` | *(Optional)* Gibt einen oder mehrere der folgenden Filter an, die vor dem Exportieren auf das Segment angewendet werden sollen. |
| `filter.segments` | *(Optional)* Gibt die zu exportierenden Segmente an. Wird dieser Wert nicht angegeben, werden alle Daten aus allen Profilen exportiert. Akzeptiert ein Array von Segmentobjekten, die jeweils die folgenden Felder enthalten:<ul><li>`segmentId`: **(Erforderlich bei Verwendung`segments`)** der Segment-ID für Profil, die exportiert werden sollen.</li><li>`segmentNs` *(Optional)* Segmentcode für den jeweiligen Namensraum `segmentID`.</li><li>`status` *(Optional)* Ein Array von Zeichenfolgen, das einen Statusfilter für die `segmentID`Zeichenfolge bereitstellt. Standardmäßig `status` wird der Wert `["realized", "existing"]` verwendet, der alle Profil darstellt, die zum aktuellen Zeitpunkt in das Segment fallen. Mögliche Werte sind: `"realized"`, `"existing"`und `"exited"`.</br></br>Weitere Informationen finden Sie im Lernprogramm zum [Erstellen von Segmenten](./create-a-segment.md).</li></ul> |
| `filter.segmentQualificationTime` | *(Optional)* Filtern Sie nach der Segmentqualifizierungszeit. Die Beginn- und/oder Endzeit können angegeben werden. |
| `filter.segmentQualificationTime.startTime` | *(Optional)* Segmentqualifizierungs-Beginn für eine Segment-ID für einen bestimmten Status. Es wurde nicht angegeben, es wird kein Filter für die Zeit des Beginns für eine Segment-ID-Qualifizierung angezeigt. Der Zeitstempel muss im [RFC 3339](https://tools.ietf.org/html/rfc3339) -Format angegeben werden. |
| `filter.segmentQualificationTime.endTime` | *(Optional)* Endzeit der Segmentqualifizierung für eine Segment-ID für einen bestimmten Status. Es wurde kein Filter für die Endzeit einer Segment-ID-Qualifizierung bereitgestellt. Der Zeitstempel muss im [RFC 3339](https://tools.ietf.org/html/rfc3339) -Format angegeben werden. |
| `filter.fromIngestTimestamp ` | *(Optional)* Beschränkt exportierte Profil auf diejenigen, die nach diesem Zeitstempel aktualisiert wurden. Der Zeitstempel muss im [RFC 3339](https://tools.ietf.org/html/rfc3339) -Format angegeben werden. <ul><li>`fromIngestTimestamp` für **Profile**, sofern vorhanden: Umfasst alle zusammengeführten Profil, bei denen der zusammengeführte aktualisierte Zeitstempel größer als der angegebene Zeitstempel ist. Unterstützt `greater_than` Operand.</li><li>`fromTimestamp` für **Ereignisse**: Alle nach diesem Zeitstempel erfassten Ereignis werden entsprechend dem resultierenden Profil exportiert. Dies ist nicht die Ereignis-Zeit selbst, sondern die Aufnahmezeit für die Ereignisse.</li> |
| `filter.emptyProfiles` | *(Optional)* Boolescher Wert. Profil können Profil-Datensätze, ExperienceEvent-Datensätze oder beides enthalten. Profil ohne Profil-Datensätze und nur ExperienceEvent-Datensätze werden als &quot;emptyProfiles&quot;bezeichnet. Um alle Profil im Profil-Store einschließlich &quot;emptyProfiles&quot;zu exportieren, setzen Sie den Wert `emptyProfiles` auf `true`. Wenn `emptyProfiles` dies auf `false`festgelegt ist, werden nur Profil mit Profil-Datensätzen im Store exportiert. Wenn `emptyProfiles` das Attribut nicht enthalten ist, werden standardmäßig nur Profil exportiert, die Profil-Datensätze enthalten. |
| `additionalFields.eventList` | *(Optional)* Steuert die Zeitreihen-Ereignis-Felder, die für untergeordnete oder zugehörige Objekte exportiert werden, indem eine oder mehrere der folgenden Einstellungen bereitgestellt werden:<ul><li>`eventList.fields`: Steuerung der zu exportierenden Felder.</li><li>`eventList.filter`: Gibt Kriterien an, die die Ergebnisse verknüpfter Objekte einschränken. Erwartet einen für den Export erforderlichen Mindestwert, normalerweise ein Datum.</li><li>`eventList.filter.fromIngestTimestamp`: Filter erhalten Zeitreihen-Ereignis zu denen, die nach dem bereitgestellten Zeitstempel erfasst wurden. Dies ist nicht die Ereignis-Zeit selbst, sondern die Aufnahmezeit für die Ereignisse.</li></ul> |
| `destination` | **(Erforderlich)** Zielinformationen für die exportierten Daten:<ul><li>`destination.datasetId`: **(Erforderlich)** Die ID des Datensatzes, in den Daten exportiert werden sollen.</li><li>`destination.segmentPerBatch`: *(Optional)* Ein boolescher Wert, der, falls nicht angegeben, standardmäßig `false`lautet. Beim Wert `false` werden alle Segment-IDs in eine einzige Stapel-ID exportiert. Ein Wert von `true` exportiert eine Segment-ID in eine Stapel-ID. Beachten Sie, dass die Einstellung des Werts sich auf die Exportleistung des Stapels auswirken `true` kann.</li></ul> |
| `schema.name` | **(Erforderlich)** Der Name des Schemas, das mit dem Datensatz verknüpft ist, in den Daten exportiert werden sollen. |
| `evaluationInfo.segmentation` | *(Optional)* Ein boolescher Wert, der, falls nicht angegeben, standardmäßig auf `false`. Der Wert `true` gibt an, dass die Segmentierung für den Exportauftrag durchgeführt werden muss. |

>[!NOTE] Um nur Profil-Daten zu exportieren und keine zugehörigen ExperienceEvent-Daten einzuschließen, entfernen Sie das Objekt &quot;additionalFields&quot;aus der Anforderung.

**Antwort**

Eine erfolgreiche Antwort gibt einen Datensatz zurück, der mit den in der Anforderung angegebenen Profil-Daten gefüllt ist.

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
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
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

Wenn `destination.segmentPerBatch` sie nicht in die Anforderung einbezogen wurde (falls sie nicht vorhanden ist, wird sie standardmäßig auf `false`) oder der Wert auf festgelegt wurde `false`, hätte das `destination` Objekt in der Antwort oben kein `batches` Array und würde stattdessen nur ein `batchId`wie unten dargestellt enthalten. Dieser einzelne Stapel würde alle Segment-IDs enthalten, während die obige Antwort eine einzelne Segment-ID pro Stapel-ID anzeigt.

```json
  "destination": {
    "datasetId": "5cf6bcf79ecc7c14530fe436",
    "segmentPerBatch": false,
    "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
  }
```

## Liste aller Exportaufträge

Sie können eine Liste aller Exportaufträge für eine bestimmte IMS-Organisation zurückgeben, indem Sie eine GET-Anforderung an den `export/jobs` Endpunkt ausführen. Die Anforderung unterstützt auch die Abfrage Parameter `limit` und `offset`, wie unten dargestellt.

**API-Format**

```http
GET /export/jobs
GET /export/jobs?limit=4
GET /export/jobs?offset=2
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `limit` | Geben Sie die Anzahl der zurückzugebenden Datensätze an. |
| `offset` | Versetzen Sie die Seite der Ergebnisse, die durch die angegebene Zahl zurückgegeben werden sollen. |

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
      "filter": {
          "segments": [
              {
                  "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff"
              }
          ]
      },
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

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | Der `id` Exportauftrag, auf den Sie zugreifen möchten. |

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
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
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
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
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

Mit Experience Platform können Sie einen vorhandenen Exportauftrag stornieren. Dies kann aus verschiedenen Gründen nützlich sein, z. B. wenn der Exportauftrag nicht abgeschlossen wurde oder in der Verarbeitungsstufe hängen geblieben ist. Um einen Exportauftrag abzubrechen, können Sie eine DELETE-Anforderung an den `/export/jobs` Endpunkt ausführen und die Angabe `id` des Exportauftrags, den Sie abbrechen möchten, in den Anforderungspfad einschließen.

**API-Format**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | Der `id` Exportauftrag, auf den Sie zugreifen möchten. |

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

Nach erfolgreichem Abschluss des Exports sind Ihre Daten in der Experience Platform &quot;Data Lake in Experience Platform&quot;verfügbar. Sie können dann mit der [Datenzugriff-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) auf die Daten zugreifen, indem Sie die mit dem Export verknüpfte `batchId` Datei verwenden. Je nach Größe des Exports können die Daten in Blöcken vorliegen und der Stapel kann aus mehreren Dateien bestehen.

Eine schrittweise Anleitung zum Zugriff auf und Herunterladen von Stapeldateien mit der Datenzugriff-API finden Sie im Lernprogramm [Datenzugriff](../../data-access/tutorials/dataset-data.md).

Sie können auch über den Adobe Experience Platform Abfrage Service auf erfolgreich exportierte Echtzeit-Kundendaten zugreifen. Mithilfe der Benutzeroberfläche oder RESTful-API können Sie mit dem Abfrage Service Abfragen für Daten im Data Lake schreiben, überprüfen und ausführen.

Weitere Informationen zur Abfrage von Audiencen finden Sie in der Dokumentation zum [Abfrage Service](../../query-service/home.md).