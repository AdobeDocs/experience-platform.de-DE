---
keywords: Experience Platform;Profil;Echtzeit-Kundenprofil;Fehlerbehebung;API;
title: API-Endpunkt für Profilsystemaufträge
type: Documentation
description: Mit Adobe Experience Platform können Sie einen Datensatz oder Batch aus dem Profilspeicher löschen, um nicht mehr benötigte oder irrtümlich hinzugefügte Echtzeit-Kundenprofildaten zu entfernen. Dies erfordert die Verwendung der Profil-API zum Erstellen eines Profil-Systemauftrags oder einer Löschanfrage.
role: Developer
exl-id: 75ddbf2f-9a54-424d-8569-d6737e9a590e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2022'
ht-degree: 35%

---

# Auftrags-Endpunkt des Profilsystems (Löschanfragen)

>[!IMPORTANT]
>
>Die folgenden Endpunkte können je nach Implementierung von Adobe Experience Platform auf Microsoft Azure und Amazon Web Services (AWS) unterschiedlich sein. Experience Platform, das auf AWS ausgeführt wird, steht derzeit einer begrenzten Anzahl von Kunden zur Verfügung. Weitere Informationen zur unterstützten Experience Platform-Infrastruktur finden Sie in der Übersicht zur [Experience Platform Multi-Cloud](https://experienceleague.adobe.com/de/docs/experience-platform/landing/multi-cloud).

Mit Adobe Experience Platform können Sie Daten aus verschiedenen Quellen erfassen und zuverlässige Profile für einzelne Kunden einrichten. In [!DNL Experience Platform] aufgenommene Daten werden im [!DNL Data Lake] gespeichert. Wenn die Datensätze für das Profil aktiviert wurden, werden diese Daten auch im [!DNL Real-Time Customer Profile] Datenspeicher gespeichert. Gelegentlich kann es erforderlich sein, mit einem Datensatz verknüpfte Profildaten aus dem Profilspeicher zu löschen, um nicht mehr benötigte oder irrtümlich hinzugefügte Daten zu entfernen. Dies erfordert die Verwendung der [!DNL Real-Time Customer Profile]-API zum Erstellen eines [!DNL Profile] Systemauftrags oder „Löschanfrage“.

>[!NOTE]
>
>Wenn Sie versuchen, Datensätze oder Batches aus der [!DNL Data Lake] zu löschen, besuchen Sie die [Übersicht über den Katalog-Service](../../catalog/home.md), um weitere Informationen zu erhalten.

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil von [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Bevor Sie fortfahren, lesen Sie das Handbuch [Erste Schritte](getting-started.md) mit Links zur zugehörigen Dokumentation, einer Anleitung zum Lesen der API-Beispielaufrufe in diesem Dokument und wichtigen Informationen zu den erforderlichen Kopfzeilen, die für die erfolgreiche Ausführung von Aufrufen an eine Experience Platform-API erforderlich sind.

## Löschanfragen anzeigen {#view}

Bei einer Löschanfrage handelt es sich um einen langwierigen, asynchronen Prozess, d. h., Ihre Organisation führt möglicherweise mehrere Löschanfragen gleichzeitig aus. Um alle derzeit in Ihrer Organisation ausgeführten Löschanfragen anzuzeigen, können Sie eine GET-Anfrage an den `/system/jobs`-Endpunkt stellen.

Außerdem können Sie optionale Abfrageparameter verwenden, um die Liste der in der Antwort zurückgegebenen Löschanfragen zu filtern. Um mehrere Parameter zu verwenden, trennen Sie die einzelnen Parameter durch ein kaufmännisches Und-Zeichen (`&`).

**API-Format**

>[!AVAILABILITY]
>
>Die folgenden Abfrageparameter sind **verfügbar** wenn Sie Experience Platform auf Microsoft Azure verwenden.
>
>Bei Verwendung dieses Endpunkts auf AWS werden die ersten 100 Systemaufträge in absteigender Reihenfolge und basierend auf ihrem Erstellungsdatum zurückgegeben.

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| Parameter | Beschreibung | Beispiel |
| --------- | ----------- | ------- |
| `start` | Versetzt die zurückgegebene Ergebnisseite entsprechend der Erstellungszeit der Anfrage. | `start=4` |
| `limit` | Anzahl der zurückgegebenen Ergebnisse begrenzen. | `limit=10` |
| `page` | Gibt eine bestimmte Ergebnisseite zurück, je nach Erstellungszeit der Anfrage. | `page=2` |
| `sort` | Sortiert Ergebnisse nach einem bestimmten Feld in aufsteigender (`asc`) oder absteigender (`desc`) Reihenfolge. Der Sortierparameter funktioniert nicht, wenn mehrere Ergebnisseiten zurückgegeben werden. | `sort=batchId:asc` |

**Anfrage**

>[!IMPORTANT]
>
>Die folgende Anfrage unterscheidet sich zwischen der Azure- und der AWS-Instanz.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

+++ Eine Beispielanfrage zum Anzeigen Ihrer Systemaufträge.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

>[!TAB Amazon Web Services (AWS)]

>[!IMPORTANT]
>
>Sie **müssen** bei der Verwendung dieses Endpunkts mit AWS den `x-sandbox-id`-Anfrage-Header anstelle des `x-sandbox-name`-Anfrage-Headers verwenden.

+++ Eine Beispielanfrage zum Anzeigen Ihrer Systemaufträge.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
```

+++

>[!ENDTABS]

**Antwort**

>[!IMPORTANT]
>
>Die folgende Antwort unterscheidet sich zwischen der Azure- und der AWS-Instanz.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

Eine erfolgreiche Antwort enthält ein Array „children“ mit einem Objekt für jede Löschanfrage, das die Details dieser Anfrage enthält.

+++ Eine erfolgreiche Antwort zur Anzeige der Löschanfragen

```json
{
  "_page": {
    "count": 100,
    "next": "K1JJRDpFaWc5QUwyZFgtMEpBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQVFBQWZBQUg0Ly9yL25PcmpmZndEZUR3QT0="
  },
  "children": [
    {
      "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
      "imsOrgId": "{ORG_ID}",
      "batchId": "8d075b5a178e48389126b9289dcfd0ac",
      "jobType": "DELETE",
      "status": "COMPLETED",
      "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
      "createEpoch": 1559026134,
      "updateEpoch": 1559026137
    },
    {
      "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
      "imsOrgId": "{ORG_ID}",
      "dataSetId": "5c802d3cd83fc114b741c4b5",
      "jobType": "DELETE",
      "status": "PROCESSING",
      "metrics": "{\"recordsProcessed\":0,\"timeTakenInSec\":15}",
      "createEpoch": 1559025404,
      "updateEpoch": 1559025406
    }
  ]
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `_page.count` | Die Gesamtanzahl der Anfragen. Diese Antwort wurde aus Platzgründen abgeschnitten. |
| `_page.next` | Wenn eine zusätzliche Ergebnisseite vorhanden ist, zeigen Sie die nächste Ergebnisseite an, indem Sie den ID-Wert in einer [Suchanfrage](#view-a-specific-delete-request) durch den angegebenen `"next"`-Wert ersetzen. |
| `jobType` | Der Typ des zu erstellenden Auftrags. In diesem Fall wird immer `"DELETE"` zurückgegeben. |
| `status` | Der Status der Löschanfrage. Zu den möglichen Werten gehören `"NEW"`, `"PROCESSING"`, `"COMPLETED"` und `"ERROR"`. |
| `metrics` | Ein -Objekt, das die Anzahl der Datensätze enthält, die verarbeitet wurden (`"recordsProcessed"`), und die Zeit in Sekunden, die die Anfrage verarbeitet wurde oder wie lange die Anfrage dauerte (`"timeTakenInSec"`). |

+++

>[!TAB Amazon Web Services (AWS)]

Eine erfolgreiche Antwort gibt ein -Array zurück, das ein -Objekt für jede der Systemanforderungen enthält.

+++ Eine erfolgreiche Antwort zur Anzeige der Systemanforderungen

```json
{
    [
        {
            "requestId": "80a9405a-21ca-4278-aedf-99367f90c055",
            "requestType": "DELETE_EE_BATCH",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxName": "prod",
                "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
            },
            "status": "SUCCESS",
            "properties": {
                "batchId": "01JFSYFDFW9JAAEKHX672JMPSB",
                "datasetId": "66a92c5910df2d1767de13f3"
            },
            "createdAt": "2024-12-22T19:44:50.250006Z",
            "updatedAt": "2024-12-22T19:52:13.380706Z"
        },
        {
            "requestId": "38a835eb-b491-4864-902b-be07fa4d6a6d",
            "requestType": "TRUNCATE_DATASET",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxName": "prod",
                "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
            },
            "status": "SUCCESS",
            "properties": {
                "datasetId": "66a92c5910df2d1767de13f3"
            },
            "createdAt": "2024-12-22T19:44:50.250006Z",
            "updatedAt": "2024-12-22T19:52:13.380706Z"
        }        
    ]
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `requestId` | Die ID des Systemvorgangs. |
| `requestType` | Der Typ des Systemvorgangs. Zu den möglichen Werten gehören `BACKFILL_TTL`, `DELETE_EE_BATCH` und `TRUNCATE_DATASET`. |
| `status` | Der Status des Systemvorgangs. Zu den möglichen Werten gehören `NEW`, `SUCCESS`, `ERROR`, `FAILED` und `IN-PROGRESS`. |
| `properties` | Ein Objekt, das Batch- und/oder Datensatz-IDs des Systemauftrags enthält. |

+++

>[!ENDTABS]

## Erstellen einer Löschanfrage {#create-a-delete-request}

Die Initiierung einer neuen Löschanfrage erfolgt über eine POST-Anfrage an den `/systems/jobs`-Endpunkt, wobei die Kennung des zu löschenden Datensatzes oder Batches im Text der Anfrage angegeben wird.

### Löschen eines Datensatzes und der zugehörigen Profildaten

Um einen Datensatz und alle mit dem Datensatz verknüpften Profildaten aus dem Profilspeicher zu löschen, muss die Datensatz-ID im Hauptteil der POST-Anfrage enthalten sein. Durch diese Aktion werden ALLE Daten für einen bestimmten Datensatz gelöscht. Mit [!DNL Experience Platform] können Sie Datensätze löschen, die sowohl auf Datensatz- als auch auf Zeitreihenschemata basieren.

**API-Format**

```http
POST /system/jobs
```

**Anfrage**

>[!IMPORTANT]
>
>Die folgende Anfrage unterscheidet sich zwischen der Azure- und der AWS-Instanz.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

+++ Eine Beispielanfrage zum Löschen eines Datensatzes.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "dataSetId": "5c802d3cd83fc114b741c4b5"
      }'
```

+++

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `dataSetId` | Die ID des Datensatzes, den Sie löschen möchten. |

>[!TAB Amazon Web Services (AWS)]

>[!IMPORTANT]
>
>Sie **müssen** bei der Verwendung dieses Endpunkts mit AWS den `x-sandbox-id`-Anfrage-Header anstelle des `x-sandbox-name`-Anfrage-Headers verwenden.

+++ Eine Beispielanfrage zum Löschen eines Datensatzes.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
  -d '{
        "dataSetId": "5c802d3cd83fc114b741c4b5"
      }'
```

+++

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `dataSetId` | Die ID des Datensatzes, den Sie löschen möchten. |

>[!ENDTABS]

**Antwort**

>[!IMPORTANT]
>
>Die folgende Antwort unterscheidet sich zwischen der Azure- und der AWS-Instanz.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

Eine erfolgreiche Antwort gibt die Details der neu erstellten Löschanfrage zurück, einschließlich einer eindeutigen, vom System generierten und schreibgeschützten Kennung für die Anfrage. Diese kann zum Nachschlagen der Anfrage und Überprüfen ihres Status verwendet werden. Der `status` (Status) der Anfrage lautet zum Zeitpunkt der Erstellung `"NEW"`, und zwar solange, bis die Verarbeitung beginnt. Die `dataSetId` in der Antwort sollte mit der in der Anfrage gesendeten `dataSetId` übereinstimmen.

+++ Eine erfolgreiche Antwort zum Erstellen einer DELETE-Anfrage.

```json
{
    "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
    "imsOrgId": "{ORG_ID}",
    "dataSetId": "5c802d3cd83fc114b741c4b5",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559025404,
    "updateEpoch": 1559025406
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `id` | Die eindeutige, vom System generierte und schreibgeschützte Kennung der Löschanfrage. |
| `dataSetId` | Die Kennung des Datensatzes, wie in der POST-Anfrage angegeben. |

+++

>[!TAB Amazon Web Services (AWS)]

Eine erfolgreiche Antwort gibt die Details der neu erstellten Systemanfrage zurück.

+++ Eine erfolgreiche Antwort zum Erstellen einer DELETE-Anfrage.

```json
{
    "requestId": "80a9405a-21ca-4278-aedf-99367f90c055",
    "requestType": "DELETE_EE_BATCH",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxName": "prod",
        "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
    },
    "status": "SUCCESS",
    "properties": {
        "batchId": "01JFSYFDFW9JAAEKHX672JMPSB",
        "datasetId": "66a92c5910df2d1767de13f3"
    },
    "createdAt": "2024-12-22T19:44:50.250006Z",
    "updatedAt": "2024-12-22T19:52:13.380706Z"
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `requestId` | Die ID des Systemvorgangs. |
| `requestType` | Der Typ des Systemvorgangs. Zu den möglichen Werten gehören `BACKFILL_TTL`, `DELETE_EE_BATCH` und `TRUNCATE_DATASET`. |
| `status` | Der Status des Systemvorgangs. Zu den möglichen Werten gehören `NEW`, `SUCCESS`, `ERROR`, `FAILED` und `IN-PROGRESS`. |
| `properties` | Ein Objekt, das Batch- und/oder Datensatz-IDs des Systemauftrags enthält. |

+++

>[!ENDTABS]

### Batch löschen

Um einen Batch zu löschen, muss die Batch-Kennung im Text der POST-Anfrage enthalten sein. Beachten Sie, dass Sie Batches für Datensätze, die auf Datensatzschemata basieren, nicht löschen können. Nur Batches für Datensätze, die auf Zeitreihenschemata basieren, können gelöscht werden.

>[!NOTE]
>
> Batches für Datensätze, die auf Datensatzschemata basieren, lassen sich nicht löschen, weil Datensatz-Batches vom Typ Datensatz frühere Datensätze überschreiben und daher nicht „rückgängig gemacht“ oder gelöscht werden können. Die einzige Möglichkeit, die Auswirkungen fehlerhafter Batches auf Datensätze zu entfernen, die auf Datensatzschemata basieren, besteht darin, den Batch mit den richtigen Daten erneut aufzunehmen, um die falschen Datensätze zu überschreiben.

Weitere Informationen zum Datensatz- und Zeitreihenverhalten finden Sie im [Abschnitt zu XDM-Datenverhalten](../../xdm/home.md#data-behaviors) in der [!DNL XDM System].

**API-Format**

```http
POST /system/jobs
```

**Anfrage**

>[!IMPORTANT]
>
>Die folgende Anfrage unterscheidet sich zwischen der Azure- und der AWS-Instanz.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

+++ Eine Beispielanfrage zum Löschen eines Batches.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "datasetId": "66a92c5910df2d1767de13f3",
        "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

+++

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `datasetId` | Die ID des Datensatzes für den Batch, den Sie löschen möchten. |
| `batchId` | Die ID des Stapels, den Sie löschen möchten. |

>[!TAB Amazon Web Services (AWS)]

>[!IMPORTANT]
>
>Sie **müssen** bei der Verwendung dieses Endpunkts mit AWS den `x-sandbox-id`-Anfrage-Header anstelle des `x-sandbox-name`-Anfrage-Headers verwenden.

+++ Eine Beispielanfrage zum Löschen eines Batches.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
  -d '{
        "datasetId": "66a92c5910df2d1767de13f3",
        "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

+++

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `datasetId` | Die ID des Datensatzes für den Batch, den Sie löschen möchten. |
| `batchId` | Die ID des Stapels, den Sie löschen möchten. |

>[!ENDTABS]

**Antwort**

>[!IMPORTANT]
>
>Die folgende Antwort unterscheidet sich zwischen der Azure- und der AWS-Instanz.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

Eine erfolgreiche Antwort gibt die Details der neu erstellten Löschanfrage zurück, einschließlich einer eindeutigen, vom System generierten und schreibgeschützten Kennung für die Anfrage. Diese kann zum Nachschlagen der Anfrage und Überprüfen ihres Status verwendet werden. Der `"status"` (Status) der Anfrage lautet zum Zeitpunkt der Erstellung `"NEW"`, und zwar solange, bis die Verarbeitung beginnt. Der `"batchId"` Wert in der Antwort sollte mit dem in der Anfrage gesendeten `"batchId"` übereinstimmen.

+++ Eine erfolgreiche Antwort zum Erstellen einer DELETE-Anfrage.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{ORG_ID}",
    "datasetId": "66a92c5910df2d1767de13f3",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559026131,
    "updateEpoch": 1559026132
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `id` | Die eindeutige, vom System generierte und schreibgeschützte Kennung der Löschanfrage. |
| `datasetId` | Die ID des angegebenen Datensatzes. |
| `batchId` | Die Kennung des Batches, wie in der POST-Anfrage angegeben. |

+++

>[!TAB Amazon Web Services (AWS)]

Eine erfolgreiche Antwort gibt die Details der neu erstellten Systemanfrage zurück.

+++ Eine erfolgreiche Antwort zum Erstellen einer DELETE-Anfrage.

```json
{
    "requestId": "80a9405a-21ca-4278-aedf-99367f90c055",
    "requestType": "DELETE_EE_BATCH",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxName": "prod",
        "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
    },
    "status": "SUCCESS",
    "properties": {
        "batchId": "01JFSYFDFW9JAAEKHX672JMPSB",
        "datasetId": "66a92c5910df2d1767de13f3"
    },
    "createdAt": "2024-12-22T19:44:50.250006Z",
    "updatedAt": "2024-12-22T19:52:13.380706Z"
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `requestId` | Die ID des Systemvorgangs. |
| `requestType` | Der Typ des Systemvorgangs. Zu den möglichen Werten gehören `BACKFILL_TTL`, `DELETE_EE_BATCH` und `TRUNCATE_DATASET`. |
| `status` | Der Status des Systemvorgangs. Zu den möglichen Werten gehören `NEW`, `SUCCESS`, `ERROR`, `FAILED` und `IN-PROGRESS`. |
| `properties` | Ein Objekt, das Batch- und/oder Datensatz-IDs des Systemauftrags enthält. |

+++

>[!ENDTABS]

>[!AVAILABILITY]
>
>Die folgende Funktion ist **verfügbar** wenn Experience Platform auf Microsoft Azure verwendet wird.

Wenn Sie versuchen, eine Löschanfrage für einen Datensatz-Batch vom Typ Datensatz zu initiieren, tritt ein 400-Fehler auf, der in etwa wie folgt aussieht:

```json
{
    "requestId": "bc4eb29f-63a8-4653-9133-71238884bb81",
    "errors": {
        "400": [
            {
                "code": "500",
                "message": "Batch can only be specified for EE type 'a294e36d382649dab2cc6ad64a41b674'"
            }
        ]
    }
}
```

## Anzeigen einer bestimmten Löschanfrage {#view-a-specific-delete-request}

Zur Ansicht einer bestimmten Löschanfrage, einschließlich Details wie dem Status, können Sie eine GET-Anfrage (zum Nachschlagen) an den `/system/jobs`-Endpunkt stellen und die Kennung der Löschanfrage in den Pfad einschließen.

**API-Format**

```http
GET /system/jobs/{DELETE_REQUEST_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{DELETE_REQUEST_ID}` | Die ID der Löschanfrage, die Sie anzeigen möchten. |

**Anfrage**

>[!IMPORTANT]
>
>Die folgende Anfrage unterscheidet sich zwischen der Azure- und der AWS-Instanz.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

+++ Beispielanfrage zum Anzeigen eines Profilauftrags.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

>[!TAB Amazon Web Services (AWS)]

>[!IMPORTANT]
>
>Sie **müssen** bei der Verwendung dieses Endpunkts mit AWS den `x-sandbox-id`-Anfrage-Header anstelle des `x-sandbox-name`-Anfrage-Headers verwenden.

+++ Beispielanfrage zum Anzeigen eines Profilauftrags.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

+++

>[!ENDTABS]


**Antwort**

>[!IMPORTANT]
>
>Die folgende Antwort unterscheidet sich zwischen der Azure- und der AWS-Instanz.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

Die Antwort enthält die Details der Löschanfrage, einschließlich ihres aktualisierten Status. Die ID der Löschanfrage in der Antwort (der `"id"`) sollte mit der im Anfragepfad gesendeten ID übereinstimmen.

+++ Eine erfolgreiche Antwort für die Anzeige einer Löschanfrage.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{ORG_ID}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "COMPLETED",
    "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
    "createEpoch": 1559026134,
    "updateEpoch": 1559026137
}
```

| Eigenschaften | Beschreibung |
| ---------- | ----------- |
| `jobType` | Der Typ des erstellten Auftrags. In diesem Fall wird immer `"DELETE"` zurückgegeben. |
| `status` | Der Status der Löschanfrage. Zu den möglichen Werten gehören `NEW`, `PROCESSING`, `COMPLETED` und `ERROR`. |
| `metrics` | Ein Array, das die Anzahl der verarbeiteten Datensätze (`"recordsProcessed"`) und die Zeit in Sekunden enthält, die die Anfrage verarbeitet wurde, oder die Dauer der Anfrage (`"timeTakenInSec"`). |

+++

>[!TAB Amazon Web Services (AWS)]

Eine erfolgreiche Antwort gibt die Details der angegebenen Systemanfrage zurück.

+++ Eine erfolgreiche Antwort für die Anzeige einer Löschanfrage.

```json
{
    "requestId": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "requestType": "DELETE_EE_BATCH",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxName": "prod",
        "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
    },
    "status": "SUCCESS",
    "properties": {
        "batchId": "01JFSYFDFW9JAAEKHX672JMPSB",
        "datasetId": "66a92c5910df2d1767de13f3"
    },
    "createdAt": "2024-12-22T19:44:50.250006Z",
    "updatedAt": "2024-12-22T19:52:13.380706Z"
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `requestId` | Die ID des Systemvorgangs. |
| `requestType` | Der Typ des Systemvorgangs. Zu den möglichen Werten gehören `BACKFILL_TTL`, `DELETE_EE_BATCH` und `TRUNCATE_DATASET`. |
| `status` | Der Status des Systemvorgangs. Zu den möglichen Werten gehören `NEW`, `SUCCESS`, `ERROR`, `FAILED` und `IN-PROGRESS`. |
| `properties` | Ein Objekt, das Batch- und/oder Datensatz-IDs des Systemauftrags enthält. |

+++

>[!ENDTABS]

Sobald der Status der Löschanfrage `"COMPLETED"` ist, können Sie bestätigen, dass die Daten gelöscht wurden, indem Sie versuchen, über die Datenzugriffs-API auf die gelöschten Daten zuzugreifen. Anweisungen zum Zugreifen auf Datensätze und Batches mit der Data Access-API finden Sie in der [Dokumentation zu Data Access](../../data-access/home.md).

## Löschanfrage entfernen

>[!AVAILABILITY]
>
>Dieser Endpunkt wird **nur** in der Azure-Instanz von Adobe Experience Platform unterstützt und **nicht** in der AWS-Instanz unterstützt.

[!DNL Experience Platform] können Sie eine frühere Anfrage löschen. Dies kann aus verschiedenen Gründen nützlich sein, z. B. wenn der Löschvorgang nicht abgeschlossen wurde oder in der Verarbeitungsstufe hängen geblieben ist. Um eine Löschanfrage zu entfernen, können Sie eine Löschanfrage an den `/system/jobs`-Endpunkt stellen und die Kennung der Löschanfrage, die Sie entfernen möchten, in den Anfragepfad einschließen.

**API-Format**

```http
DELETE /system/jobs/{DELETE_REQUEST_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| {DELETE_REQUEST_ID} | Die Kennung der Löschanfrage, die Sie entfernen möchten. |

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei erfolgreicher Löschanfrage werden der HTTP-Status 200 (OK) und ein leerer Antworttext zurückgegeben. Sie können prüfen, ob die Anfrage gelöscht wurde, indem Sie eine GET-Anfrage ausführen, um die Löschanfrage mittels ihrer Kennung anzuzeigen. Nun sollte ein HTTP-Status 404 (Nicht gefunden) zurückgegeben werden, was bedeutet, dass die Löschanfrage entfernt wurde.

## Nächste Schritte

Nachdem Sie nun die Schritte kennen, die beim Löschen von Datensätzen und Batches aus dem [!DNL Profile store] in [!DNL Experience Platform] erforderlich sind, können Sie Daten, die fälschlicherweise hinzugefügt wurden oder die Ihr Unternehmen nicht mehr benötigt, sicher löschen. Beachten Sie, dass Löschanfragen nicht rückgängig gemacht werden können. Daher sollten Sie Daten nur dann löschen, wenn Sie sicher sind, dass Sie sie jetzt und in Zukunft nicht mehr benötigen werden.
