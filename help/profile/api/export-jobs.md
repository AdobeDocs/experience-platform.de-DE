---
keywords: Experience Platform;Profil;Echtzeit-Kundenprofil;Fehlerbehebung;API;
title: Profil-Export-Auftrags-API-Endpunkt
type: Documentation
description: Das Echtzeit-Kundenprofil ermöglicht es Ihnen, innerhalb von Adobe Experience Platform eine zentrale Ansicht einzelner Kunden zu erstellen, indem es Daten aus verschiedenen Quellen zusammenführt, einschließlich Attributdaten und Verhaltensdaten. Profildaten können dann zur weiteren Verarbeitung in einen Datensatz exportiert werden.
role: Developer
exl-id: d51b1d1c-ae17-4945-b045-4001e4942b67
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 9%

---

# Endpunkt der Profilexport-Aufträge

[!DNL Real-Time Customer Profile] ermöglicht Ihnen, eine zentrale Ansicht einzelner Kunden zu erstellen, indem Sie Daten aus verschiedenen Quellen zusammenführen, einschließlich Attributdaten und Verhaltensdaten. Profildaten können dann zur weiteren Verarbeitung in einen Datensatz exportiert werden. Beispiel: [!DNL Profile] -Daten können zur Aktivierung exportiert werden, indem Zielgruppen erstellt werden, und Profilattribute können zur Berichterstellung exportiert werden.

Dieses Dokument enthält eine schrittweise Anleitung zum Erstellen und Verwalten von Exportvorgängen mit dem [Profil-API](https://www.adobe.com/go/profile-apis-en).

>[!NOTE]
>
>In diesem Handbuch wird die Verwendung von Exportvorgängen im [!DNL Profile API]. Informationen zum Verwalten von Exportaufträgen für den Segmentierungsdienst von Adobe Experience Platform finden Sie im Handbuch zu [Exportaufträge in der Segmentation-API](../../profile/api/export-jobs.md).

Zusätzlich zur Erstellung eines Exportauftrags können Sie auch auf [!DNL Profile] Daten, die `/entities` -Endpunkt, auch als &quot;[!DNL Profile Access]&quot;. Siehe [Endpunktleitfaden für Entitäten](./entities.md) für weitere Informationen. Anweisungen zum Zugriff auf [!DNL Profile] Daten über die Benutzeroberfläche, siehe [Benutzerhandbuch](../ui/user-guide.md).

## Erste Schritte

Die in diesem Handbuch verwendeten API-Endpunkte sind Teil der [!DNL Real-Time Customer Profile] API. Bevor Sie fortfahren, werfen Sie im Handbuch [Erste Schritte](getting-started.md) einen Blick auf die Informationen zu Links zu entsprechenden Dokumentationen, den Leitfaden zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtige Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen einer [!DNL Experience Platform]-API erforderlich sind.

## Erstellen eines Exportvorgangs

Exportieren [!DNL Profile] -Daten erfordert zunächst die Erstellung eines Datensatzes, in den die Daten exportiert werden, und dann die Initiierung eines neuen Exportvorgangs. Beide Schritte können mit Experience Platform-APIs durchgeführt werden, wobei erstere die Catalog Service-API und letztere die Echtzeit-Kundenprofil-API verwenden. Detaillierte Anweisungen zum Abschließen der einzelnen Schritte finden Sie in den folgenden Abschnitten.

### Erstellen eines Zieldatensatzes

Beim Exportieren [!DNL Profile] -Daten, muss zunächst ein Zieldatensatz erstellt werden. Es ist wichtig, dass der Datensatz korrekt konfiguriert ist, um sicherzustellen, dass der Export erfolgreich ist.

Eine der wichtigsten Überlegungen ist das Schema, auf dem der Datensatz basiert (`schemaRef.id` in der API-Beispielanfrage unten). Um Profildaten zu exportieren, muss der Datensatz auf der [!DNL XDM Individual Profile] Vereinigungsschema (`https://ns.adobe.com/xdm/context/profile__union`). Ein Vereinigungsschema ist ein systemgeneriertes, schreibgeschütztes Schema, das die Felder von Schemas aggregiert, die dieselbe Klasse aufweisen. In diesem Fall ist dies die [!DNL XDM Individual Profile] -Klasse. Weitere Informationen zu Vereinigungsansichtsschemas finden Sie im [Vereinigungsabschnitt im Handbuch zu den Grundlagen der Schemakomposition](../../xdm/schema/composition.md#union).

In den in diesem Tutorial beschriebenen Schritten wird beschrieben, wie Sie einen Datensatz erstellen, der auf die [!DNL XDM Individual Profile] Vereinigungsschema mit [!DNL Catalog] API. Sie können auch die [!DNL Platform] -Benutzeroberfläche zum Erstellen eines Datensatzes, der auf das Vereinigungsschema verweist. Die Schritte zur Verwendung der Benutzeroberfläche werden im Abschnitt [Dieses UI-Tutorial zum Exportieren von Zielgruppen](../../segmentation/tutorials/create-dataset-export-segment.md) aber auch hier anwendbar sind. Nach Abschluss können Sie zu diesem Tutorial zurückkehren, um mit den Schritten für [Starten eines neuen Exportvorgangs](#initiate).

Wenn Sie bereits über einen kompatiblen Datensatz verfügen und dessen Kennung kennen, können Sie direkt mit dem Schritt für [Starten eines neuen Exportvorgangs](#initiate).

**API-Format**

```http
POST /dataSets
```

**Anfrage**

Die folgende Anfrage erstellt einen neuen Datensatz und stellt Konfigurationsparameter in der Payload bereit.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Profile Data Export",
        "schemaRef": {
          "id": "https://ns.adobe.com/xdm/context/profile__union",
          "contentType": "application/vnd.adobe.xed+json;version=1"
        }
      }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `name` | Ein beschreibender Name für den Datensatz. |
| `schemaRef.id` | Die ID der Vereinigungsansicht (Schema), mit der der Datensatz verknüpft wird. |

**Antwort**

Eine erfolgreiche Antwort gibt ein Array zurück, das die schreibgeschützte, systemgenerierte eindeutige ID des neu erstellten Datensatzes enthält. Eine ordnungsgemäß konfigurierte Datensatz-ID ist erforderlich, um Profildaten erfolgreich exportieren zu können.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Exportauftrag initiieren {#initiate}

Sobald Sie über einen Datensatz mit Vereinigungspersistenz verfügen, können Sie einen Exportauftrag erstellen, um die Profildaten in dem Datensatz zu speichern, indem Sie eine POST-Anfrage an die `/export/jobs` -Endpunkt in der Echtzeit-Kundenprofil-API verwenden und die Details der Daten angeben, die Sie im Text der Anfrage exportieren möchten.

**API-Format**

```http
POST /export/jobs
```

**Anfrage**

Die folgende Anfrage erstellt einen neuen Exportauftrag, der Konfigurationsparameter in der Payload bereitstellt.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "additionalFields": {
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
| `fields` | *(Optional)* Beschränkt die im Export einzuschließenden Datenfelder auf die in diesem Parameter angegebenen Felder. Wird dieser Wert nicht angegeben, werden alle Felder in die exportierten Daten aufgenommen. |
| `mergePolicy` | *(Optional)* Gibt die Zusammenführungsrichtlinie an, die für die exportierten Daten gelten soll. Schließen Sie diesen Parameter ein, wenn mehrere Zielgruppen exportiert werden. |
| `mergePolicy.id` | Die Kennung der Zusammenführungsrichtlinie. |
| `mergePolicy.version` | Die spezifische Version der zu verwendenden Zusammenführungsrichtlinie. Wird dieser Wert nicht angegeben, wird standardmäßig die neueste Version verwendet. |
| `additionalFields.eventList` | *(Optional)* Steuert die Zeitreihen-Ereignisfelder, die für untergeordnete oder verknüpfte Objekte exportiert werden, indem eine oder mehrere der folgenden Einstellungen bereitgestellt werden:<ul><li>`eventList.fields`: Kontrollieren Sie die zu exportierenden Felder.</li><li>`eventList.filter`: Gibt Kriterien an, die die Ergebnisse begrenzen, die aus den verknüpften Objekten enthalten sind. Erwartet einen für den Export erforderlichen Mindestwert, normalerweise ein Datum.</li><li>`eventList.filter.fromIngestTimestamp`: Filtert Zeitreihenereignisse nach denjenigen, die nach dem angegebenen Zeitstempel erfasst wurden. Dies ist nicht die Ereigniszeit selbst, sondern die Erfassungszeit für die Ereignisse.</li></ul> |
| `destination` | **(Erforderlich)** Zielinformationen für die exportierten Daten:<ul><li>`destination.datasetId`: **(Erforderlich)** Die ID des Datensatzes, in den Daten exportiert werden sollen.</li><li>`destination.segmentPerBatch`: *(Optional)* Ein boolescher Wert, der standardmäßig auf `false`. Ein Wert von `false` exportiert alle Segmentdefinitions-IDs in eine Batch-Kennung. Ein Wert von `true` exportiert eine Segmentdefinitions-ID in eine Batch-Kennung. Beachten Sie, dass die Einstellung von `true` kann sich auf die Batch-Exportleistung auswirken.</li></ul> |
| `schema.name` | **(Erforderlich)** Der Name des Schemas, das mit dem Datensatz verknüpft ist, in den Daten exportiert werden sollen. |

>[!NOTE]
>
>Um nur Profildaten zu exportieren und keine zugehörigen Zeitreihendaten zu enthalten, entfernen Sie das Objekt &quot;additionalFields&quot;aus der Anfrage.

**Antwort**

Eine erfolgreiche Antwort gibt einen Datensatz zurück, der mit Profildaten gefüllt ist, wie in der Anfrage angegeben.

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
      "dataSetId": "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": false,
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{ORG_ID}",
    "creationTime": 1559674261657
}
```

## Alle Exportaufträge auflisten

Sie können eine Liste aller Exportaufträge für eine bestimmte Organisation zurückgeben, indem Sie eine GET-Anfrage an die `export/jobs` -Endpunkt. Die Anfrage unterstützt auch die Abfrageparameter `limit` und `offset`, wie unten dargestellt.

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
| `sort` | Sortieren Sie die Ergebnisse nach einem bestimmten Feld in aufsteigender Reihenfolge ( **`asc`** ) oder absteigend ( **`desc`** ). Der Sortierparameter funktioniert nicht, wenn mehrere Ergebnisseiten zurückgegeben werden. Beispiel: `sort=updateTime:asc` |

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Antwort**

Die Antwort enthält eine `records` -Objekt, das die von Ihrem Unternehmen erstellten Exportaufträge enthält.

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
      "imsOrgId": "{ORG_ID}",
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
      "imsOrgId": "{ORG_ID}",
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

## Fortschritt des Exports überwachen

Um die Details eines bestimmten Exportauftrags anzuzeigen oder dessen Status bei der Verarbeitung zu überwachen, können Sie eine GET-Anfrage an die `/export/jobs` -Endpunkt und schließen Sie die `id` des Exportauftrags im Pfad. Der Exportvorgang ist abgeschlossen, sobald die `status` gibt den Wert &quot;SUCCEEDED&quot;zurück.

**API-Format**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | Die `id` des Exportauftrags, auf den Sie zugreifen möchten. |

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/24115 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
      "dataSetId": "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": false,
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{ORG_ID}",
    "creationTime": 1559674261657
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `batchId` | Die Kennung der Batches, die aus einem erfolgreichen Export erstellt wurden und zum Nachschlagen beim Lesen von Profildaten verwendet werden sollen. |

## Abbrechen eines Exportvorgangs

Mit Experience Platform können Sie einen vorhandenen Exportauftrag abbrechen, was aus verschiedenen Gründen nützlich sein kann, z. B. wenn der Exportauftrag nicht abgeschlossen wurde oder in der Verarbeitungsstufe hängengeblieben ist. Um einen Exportauftrag abzubrechen, können Sie eine DELETE-Anfrage an die `/export/jobs` -Endpunkt und schließen Sie die `id` des Exportauftrags, den Sie zum Anfragepfad abbrechen möchten.

**API-Format**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | Die `id` des Exportauftrags, auf den Sie zugreifen möchten. |

**Anfrage**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs/726 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Löschanfrage gibt den HTTP-Status 204 (Kein Inhalt) und einen leeren Antworttext zurück, der angibt, dass der Abbrechen-Vorgang erfolgreich war.

## Nächste Schritte

Nach erfolgreichem Abschluss des Exports sind Ihre Daten im Data Lake im Experience Platform verfügbar. Anschließend können Sie die [Data Access API](https://www.adobe.io/experience-platform-apis/references/data-access/) , um auf die Daten mithilfe der `batchId` mit dem Export verknüpft ist. Je nach Größe des Exports können die Daten in Blöcken vorliegen und der Batch kann aus mehreren Dateien bestehen.

Eine schrittweise Anleitung zum Verwenden der Data Access-API für den Zugriff auf und den Download von Batch-Dateien finden Sie im Abschnitt [Tutorial zum Datenzugriff](../../data-access/tutorials/dataset-data.md).

Sie können auch mithilfe von Adobe Experience Platform Query Service auf erfolgreich exportierte Echtzeit-Kundenprofildaten zugreifen. Mithilfe der Benutzeroberfläche oder der RESTful-API können Sie mit Query Service Abfragen zu Daten im Data Lake schreiben, validieren und ausführen.

Weiterführende Informationen zur Abfrage von Zielgruppendaten finden Sie im Abschnitt [Dokumentation zu Query Service](../../query-service/home.md).

## Anhang

Der folgende Abschnitt enthält zusätzliche Informationen zu Exportvorgängen in der Profil-API.

### Beispiele für zusätzliche Exportnutzdaten

Der Beispiel-API-Aufruf, der im Abschnitt [Initiieren eines Exportvorgangs](#initiate) erstellt einen Auftrag, der sowohl Profil- (Datensatz-) als auch Ereignis- (Zeitreihendaten) enthält. In diesem Abschnitt finden Sie zusätzliche Beispiele für Anfrage-Payload, mit denen Sie Ihren Export auf einen Datentyp beschränken können.

Die folgende Payload erstellt einen Exportauftrag, der nur Profildaten (keine Ereignisse) enthält:

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

Um einen Exportauftrag zu erstellen, der nur Ereignisdaten (keine Profilattribute) enthält, kann die Payload wie folgt aussehen:

```json
{
    "fields": "identityMap",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "additionalFields": {
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

### Audiences exportieren

Sie können auch den Endpunkt &quot;Exportaufträge&quot;verwenden, um Zielgruppen anstelle von zu exportieren [!DNL Profile] Daten. Siehe Handbuch unter [Exportaufträge in der Segmentation-API](../../segmentation/api/export-jobs.md) für weitere Informationen.
