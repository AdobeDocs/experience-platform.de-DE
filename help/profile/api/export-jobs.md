---
keywords: Experience Platform;Profil;Echtzeit-Kundenprofil;Fehlerbehebung;API;
title: API-Endpunkt für Profilexportvorgänge
type: Documentation
description: Mit dem Echtzeit-Kundenprofil können Sie in Adobe Experience Platform eine zentrale Ansicht einzelner Kunden erstellen, indem Sie Daten aus verschiedenen Quellen zusammenführen, einschließlich Attributdaten und Verhaltensdaten. Profildaten können dann zur weiteren Verarbeitung in einen Datensatz exportiert werden.
role: Developer
exl-id: d51b1d1c-ae17-4945-b045-4001e4942b67
source-git-commit: fd5042bee9b09182ac643bcc69482a0a2b3f8faa
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 9%

---

# Endpunkt für Profilexportvorgänge

[!DNL Real-Time Customer Profile] können Sie eine einzige Ansicht einzelner Kunden erstellen, indem Sie Daten aus mehreren Quellen zusammenführen, einschließlich Attributdaten und Verhaltensdaten. Profildaten können dann zur weiteren Verarbeitung in einen Datensatz exportiert werden. Beispielsweise können [!DNL Profile] Daten zur Aktivierung exportiert werden, indem Zielgruppen erstellt werden, und Profilattribute können für das Reporting exportiert werden.

Dieses Dokument enthält schrittweise Anweisungen zum Erstellen und Verwalten von Exportvorgängen mithilfe der [Profil-API](https://www.adobe.com/go/profile-apis-en).

>[!NOTE]
>
>In diesem Handbuch wird die Verwendung von Exportvorgängen in der [!DNL Profile API] behandelt. Informationen zum Verwalten von Exportvorgängen für den Segmentierungs-Service von Adobe Experience Platform finden Sie im Handbuch [Exportvorgänge in der Segmentierungs-API](../../profile/api/export-jobs.md).

Zusätzlich zum Erstellen eines Exportvorgangs können Sie auch über den `/entities`-Endpunkt, auch &quot;[!DNL Profile Access]&quot; genannt, auf [!DNL Profile] zugreifen. Weitere Informationen finden Sie [Handbuch für Entitäten](./entities.md)Endpunkte). Anweisungen zum Zugriff auf [!DNL Profile] Daten über die Benutzeroberfläche finden Sie im [Benutzerhandbuch](../ui/user-guide.md).

## Erste Schritte

Die in diesem Handbuch verwendeten API-Endpunkte sind Teil der [!DNL Real-Time Customer Profile]-API. Bevor Sie fortfahren, werfen Sie im Handbuch [Erste Schritte](getting-started.md) einen Blick auf die Informationen zu Links zu entsprechenden Dokumentationen, den Leitfaden zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtige Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen einer [!DNL Experience Platform]-API erforderlich sind.

## Erstellen von Exportvorgängen

Der Export [!DNL Profile] Daten erfordert zunächst das Erstellen eines Datensatzes, in den die Daten exportiert werden, und dann das Initiieren eines neuen Exportvorgangs. Beide Schritte können mithilfe von Experience Platform-APIs durchgeführt werden, wobei Erstere die Catalog Service-API und Letztere die Echtzeit-Kundenprofil-API verwenden. Detaillierte Anweisungen zum Durchführen der einzelnen Schritte finden Sie in den folgenden Abschnitten.

### Erstellen eines Zieldatensatzes

Beim Exportieren [!DNL Profile] Daten muss zunächst ein Zieldatensatz erstellt werden. Es ist wichtig, dass der Datensatz korrekt konfiguriert ist, um sicherzustellen, dass der Export erfolgreich war.

Eine der wichtigsten Überlegungen betrifft das Schema, auf dem der Datensatz basiert (`schemaRef.id` in der unten stehenden API-Beispielanfrage). Um Profildaten zu exportieren, muss der Datensatz auf dem [!DNL XDM Individual Profile] Vereinigungsschema (`https://ns.adobe.com/xdm/context/profile__union`) basieren. Ein Vereinigungsschema ist ein systemgeneriertes, schreibgeschütztes Schema, das die Felder von Schemas aggregiert, die dieselbe Klasse haben. In diesem Fall ist dies die [!DNL XDM Individual Profile]. Weitere Informationen zu Vereinigungsansichtsschemata finden Sie im Abschnitt [Vereinigung“ im Handbuch mit den Grundlagen der Schemakomposition](../../xdm/schema/composition.md#union).

In den Schritten, die in diesem Tutorial folgen, wird beschrieben, wie Sie mithilfe der [!DNL Catalog]-API einen Datensatz erstellen, der auf das [!DNL XDM Individual Profile]-Vereinigungsschema verweist. Sie können auch die [!DNL Platform]-Benutzeroberfläche verwenden, um einen Datensatz zu erstellen, der auf das Vereinigungsschema verweist. Die Schritte zur Verwendung der Benutzeroberfläche werden in [diesem Benutzeroberflächen-Tutorial zum Exportieren von ](../../segmentation/tutorials/create-dataset-export-segment.md) beschrieben, können aber auch hier angewendet werden. Nach Abschluss des Vorgangs können Sie zu diesem Tutorial zurückkehren, um mit den Schritten zum [ eines neuen Exportvorgangs ](#initiate).

Wenn Sie bereits über einen kompatiblen Datensatz verfügen und dessen ID kennen, können Sie direkt mit dem Schritt zum [ eines neuen Exportvorgangs ](#initiate).

**API-Format**

```http
POST /dataSets
```

**Anfrage**

Die folgende Anfrage erstellt einen neuen Datensatz, der Konfigurationsparameter in der Payload bereitstellt.

```shell
curl -X POST https://platform.adobe.io/data/foundation/catalog/dataSets \
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

Eine erfolgreiche Antwort gibt ein -Array zurück, das die schreibgeschützte, systemgenerierte, eindeutige ID des neu erstellten Datensatzes enthält. Eine ordnungsgemäß konfigurierte Datensatz-ID ist erforderlich, um Profildaten erfolgreich zu exportieren.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Exportvorgang starten {#initiate}

Sobald Sie über einen Vereinigungs-persistierten Datensatz verfügen, können Sie einen Exportvorgang erstellen, um die Profildaten im Datensatz zu persistieren, indem Sie eine POST-Anfrage an den `/export/jobs`-Endpunkt in der Echtzeit-Kundenprofil-API stellen und im Hauptteil der Anfrage die Details der Daten angeben, die Sie exportieren möchten.

**API-Format**

```http
POST /export/jobs
```

**Anfrage**

Die folgende Anfrage erstellt einen neuen Exportvorgang und gibt Konfigurationsparameter in der Payload an.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/export/jobs \
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
    },
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
| `fields` | *(Optional)* Begrenzt die Datenfelder, die in den Export einbezogen werden sollen, auf die in diesem Parameter angegebenen Felder. Wenn Sie diesen Wert weglassen, werden alle Felder in die exportierten Daten aufgenommen. |
| `mergePolicy` | *(Optional)* Gibt die Zusammenführungsrichtlinie an, die für die exportierten Daten gelten soll. Schließen Sie diesen Parameter ein, wenn mehrere Zielgruppen exportiert werden. |
| `mergePolicy.id` | Die ID der Zusammenführungsrichtlinie. |
| `mergePolicy.version` | Die spezifische Version der zu verwendenden Zusammenführungsrichtlinie. Wenn Sie diesen Wert weglassen, wird standardmäßig die neueste Version verwendet. |
| `additionalFields.eventList` | *(Optional)* Steuert die Zeitreihen-Ereignisfelder, die für untergeordnete oder zugehörige Objekte exportiert werden, indem eine oder mehrere der folgenden Einstellungen bereitgestellt werden:<ul><li>`eventList.fields`: Steuern der zu exportierenden Felder.</li><li>`eventList.filter`: Gibt Kriterien an, die die Ergebnisse der zugeordneten Objekte einschränken. Erwartet einen für den Export erforderlichen Mindestwert, in der Regel ein Datum.</li><li>`eventList.filter.fromIngestTimestamp`: Filtert Zeitreihenereignisse nach denen, die nach dem angegebenen Zeitstempel aufgenommen wurden. Dies ist nicht die Ereigniszeit selbst, sondern die Aufnahmezeit für die Ereignisse.</li></ul> |
| `destination` | **(Erforderlich** Zielinformationen für die exportierten Daten:<ul><li>`destination.datasetId`: **(Erforderlich)** Die ID des Datensatzes, in den Daten exportiert werden sollen.</li><li>`destination.segmentPerBatch`: *(Optional)* Ein boolescher Wert, der, wenn er nicht angegeben wird, standardmäßig auf `false` festgelegt wird. Beim Wert `false` werden alle Segmentdefinitions-IDs in eine einzige Batch-ID exportiert. Beim Wert `true` wird eine Segmentdefinitions-ID in eine Batch-ID exportiert. Beachten Sie, dass sich die Einstellung des `true` Werts auf die Stapelexportleistung auswirken kann.</li></ul> |
| `schema.name` | **(Erforderlich)** Der Name des Schemas, das mit dem Datensatz verknüpft ist, in den Daten exportiert werden sollen. |

>[!NOTE]
>
>Um nur Profildaten zu exportieren und keine zugehörigen Zeitreihendaten einzuschließen, entfernen Sie das Objekt „additionalFields“ aus der Anfrage.

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

## Auflisten aller Exportvorgänge

Sie können eine Liste aller Exportvorgänge für eine bestimmte Organisation zurückgeben, indem Sie eine GET-Anfrage an den `export/jobs`-Endpunkt senden. Die Anfrage unterstützt auch die Abfrageparameter `limit` und `offset`, wie unten dargestellt.

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
| `sort` | Sortieren Sie die Ergebnisse nach einem bestimmten Feld in aufsteigender ( **`asc`** ) oder absteigender ( **`desc`** ) Reihenfolge. Der Sortierparameter funktioniert nicht, wenn mehrere Ergebnisseiten zurückgegeben werden. Beispiel: `sort=updateTime:asc` |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Antwort**

Die Antwort enthält ein `records`-Objekt, das die von Ihrer Organisation erstellten Exportaufträge enthält.

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

## Überwachen des Exportfortschritts

Um die Details eines bestimmten Exportvorgangs anzuzeigen oder dessen Status während der Verarbeitung zu überwachen, können Sie eine GET-Anfrage an den `/export/jobs`-Endpunkt senden und die `id` des Exportvorgangs in den Pfad aufnehmen. Der Exportvorgang ist abgeschlossen, sobald das `status` den Wert „SUCCEEDED“ zurückgibt.

**API-Format**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | Die `id` des Exportvorgangs, auf den Sie zugreifen möchten. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/24115 \
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
| `batchId` | Die Kennung der Stapel, die bei einem erfolgreichen Export erstellt wurden und zu Suchzwecken beim Lesen von Profildaten verwendet werden sollen. |

## Abbrechen von Exportvorgängen

Beim Experience Platform können Sie einen vorhandenen Exportvorgang abbrechen. Dies kann aus verschiedenen Gründen nützlich sein, z. B. wenn der Exportvorgang nicht abgeschlossen wurde oder in der Verarbeitungsstufe hängen geblieben ist. Um einen Exportvorgang abzubrechen, können Sie eine DELETE-Anfrage an den `/export/jobs`-Endpunkt senden und die `id` des Exportvorgangs, den Sie abbrechen möchten, in den Anfragepfad aufnehmen.

**API-Format**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | Die `id` des Exportvorgangs, auf den Sie zugreifen möchten. |

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/export/jobs/726 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Löschanfrage gibt den HTTP-Status 204 (Kein Inhalt) und einen leeren Antworttext zurück, was anzeigt, dass der Abbruchsvorgang erfolgreich war.

## Nächste Schritte

Sobald der Export erfolgreich abgeschlossen wurde, sind Ihre Daten im Data Lake als Experience Platform verfügbar. Anschließend können Sie die [Datenzugriffs-API](https://www.adobe.io/experience-platform-apis/references/data-access/) verwenden, um mithilfe der mit dem Export verknüpften `batchId` auf die Daten zuzugreifen. Je nach Größe des Exports können die Daten in Blöcken vorliegen und der Batch kann aus mehreren Dateien bestehen.

Eine schrittweise Anleitung zum Zugreifen auf und Herunterladen von Batch-Dateien mit der Datenzugriffs-API finden Sie im [Datenzugriffs-Tutorial](../../data-access/tutorials/dataset-data.md).

Sie können über den Abfrage-Service von Adobe Experience Platform auch auf erfolgreich exportierte Echtzeit-Kundenprofildaten zugreifen. Mit der Benutzeroberfläche oder der RESTful-API können Sie mit dem Abfrage-Service Abfragen für Daten im Data Lake schreiben, validieren und ausführen.

Weitere Informationen zum Abfragen von Zielgruppendaten finden Sie in der [Dokumentation zum Abfrage-Service](../../query-service/home.md).

## Anhang

Der folgende Abschnitt enthält zusätzliche Informationen zu Exportvorgängen in der Profil-API.

### Beispiele für zusätzliche Export-Payloads

Der Beispiel-API-Aufruf im Abschnitt [Initiieren eines Exportvorgangs](#initiate) erstellt einen Auftrag, der sowohl Profil- (Datensatz-) als auch Ereignis- (Zeitreihen-) Daten enthält. Dieser Abschnitt enthält zusätzliche Beispiele für Anfrage-Payloads, um den Export auf den einen oder den anderen Datentyp zu beschränken.

Die folgende Payload erstellt einen Exportvorgang, der nur Profildaten (keine Ereignisse) enthält:

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

Um einen Exportvorgang zu erstellen, der nur Ereignisdaten (keine Profilattribute) enthält, sieht die Payload möglicherweise wie folgt aus:

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

Sie können auch den Endpunkt für Exportvorgänge verwenden, um Zielgruppen anstelle von [!DNL Profile] zu exportieren. Weitere Informationen finden Sie [ Handbuch zu Exportvorgängen in ](../../segmentation/api/export-jobs.md) Segmentierungs-API .
