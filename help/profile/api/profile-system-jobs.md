---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Profil-Systemaufträge - Echtzeit-Profil-API
topic: guide
translation-type: tm+mt
source-git-commit: f910351d49de9c4a18a444b99b7f102f4ce3ed5b
workflow-type: tm+mt
source-wordcount: '1420'
ht-degree: 68%

---


# Endpunkt &quot;Systemaufträge&quot;(Anforderungen löschen)

Mit Adobe Experience Platform können Sie Daten aus verschiedenen Quellen erfassen und zuverlässige Profile für einzelne Kunden einrichten. Daten, die in [!DNL Platform] aufgenommen werden, werden im [!DNL Data Lake] sowie im [!DNL Real-time Customer Profile] Datenspeicher gespeichert. Gelegentlich kann es erforderlich sein, einen Datensatz oder Stapel aus dem Profil Store zu löschen, um Daten zu entfernen, die nicht mehr benötigt werden oder fehlerhaft hinzugefügt wurden. This requires using the [!DNL Real-time Customer Profile] API to create a [!DNL Profile] system job, also known as a &quot;[!DNL delete request]&quot;, that can also be modified, monitored, or removed if required.

>[!NOTE]
>If you are trying to delete datasets or batches from the [!DNL Data Lake], please visit the [Catalog Service overview](../../catalog/home.md) for instructions.

## Erste Schritte

The API endpoint used in this guide is part of the [!DNL Real-time Customer Profile API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml). Bevor Sie fortfahren, lesen Sie bitte die [Anleitung](getting-started.md) zu den ersten Schritten für Links zur zugehörigen Dokumentation, eine Anleitung zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtige Informationen zu den erforderlichen Kopfzeilen, die zum erfolgreichen Aufrufen einer beliebigen [!DNL Experience Platform] API erforderlich sind.

## Löschanfragen anzeigen

Bei einer Löschanfrage handelt es sich um einen langwierigen, asynchronen Prozess, d. h., Ihre Organisation führt möglicherweise mehrere Löschanfragen gleichzeitig aus. Um alle derzeit in Ihrer Organisation ausgeführten Löschanfragen anzuzeigen, können Sie eine GET-Anfrage an den `/system/jobs`-Endpunkt stellen.

Außerdem können Sie optionale Abfrageparameter verwenden, um die Liste der in der Antwort zurückgegebenen Löschanfragen zu filtern. Wenn Sie mehrere Parameter verwenden möchten, trennen Sie die einzelnen Parameter durch ein kaufmännisches Und-Zeichen (&amp;).

**API-Format**

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| Parameter | Beschreibung |
|---|---|
| `start` | Versatz der Seite mit den zurückgegebenen Ergebnissen, unter Berücksichtigung der Erstellungszeit der Anfrage. Beispiel: *`start=4`* |
| `limit` | Schränkt die Anzahl der zurückgegebenen Ergebnisse ein. Beispiel: *`limit=10`* |
| `page` | Gibt eine bestimmte Seite mit Ergebnissen zurück, unter Berücksichtigung der Erstellungszeit der Anfrage. Beispiel: ***`page=2`*** |
| `sort` | Sortiert Ergebnisse nach einem bestimmten Feld in aufsteigender (*`asc`*) oder absteigender (**`desc`**) Reihenfolge. Der Sortierparameter funktioniert nicht, wenn mehrere Ergebnisseiten zurückgegeben werden. Beispiel: `sort=batchId:asc` |

**Anfrage**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Die Antwort enthält ein „untergeordnetes“ Array mit einem Objekt für jede Löschanfrage, das die Details dieser Anfrage enthält.

```json
{
  "_page": {
    "count": 100,
    "next": "K1JJRDpFaWc5QUwyZFgtMEpBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQVFBQWZBQUg0Ly9yL25PcmpmZndEZUR3QT0="
  },
  "children": [
    {
      "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
      "imsOrgId": "{IMS_ORG}",
      "batchId": "8d075b5a178e48389126b9289dcfd0ac",
      "jobType": "DELETE",
      "status": "COMPLETED",
      "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
      "createEpoch": 1559026134,
      "updateEpoch": 1559026137
    },
    {
      "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
      "imsOrgId": "{IMS_ORG}",
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
|---|---|
| `_page.count` | Die Gesamtanzahl der Anfragen. Diese Antwort wurde aus Platzgründen abgeschnitten. |
| `_page.next` | If an additional page of results exists, view the next page of results by replacing the ID value in a [lookup request](#view-a-specific-delete-request) with the `"next"` value provided. |
| `jobType` | Der Typ des zu erstellenden Auftrags. In this case, it will always return `"DELETE"`. |
| `status` | Der Status der Löschanfrage. Mögliche Werte `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`. |
| `metrics` | An object that includes the number of records that have been processed (`"recordsProcessed"`) and the time in seconds that the request has been processing, or how long the request took to complete (`"timeTakenInSec"`). |

## Löschanfrage erstellen {#create-a-delete-request}

Die Initiierung einer neuen Löschanfrage erfolgt über eine POST-Anfrage an den `/systems/jobs`-Endpunkt, wobei die Kennung des zu löschenden Datensatzes oder Batches im Text der Anfrage angegeben wird.

### Datensatz löschen

Um einen Datensatz zu löschen, muss die Datensatzkennung im Text der POST-Anfrage enthalten sein. Durch diese Aktion werden ALLE Daten für einen bestimmten Datensatz gelöscht. [!DNL Experience Platform]Mit können Sie Datensätze basierend auf Datensatz- und Zeitreihenschemas löschen.

>[!CAUTION]
> When attempting to delete a [!DNL Profile]-enabled dataset using the [!DNL Experience Platform] UI, the dataset is disabled for ingestion but will not be deleted until a delete request is created using the API. Weiterführende Informationen finden Sie im [Anhang](#appendix) zu diesem Dokument.

**API-Format**

```http
POST /system/jobs
```

**Anfrage**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "dataSetId": "5c802d3cd83fc114b741c4b5"
      }'
```

| Eigenschaft | Beschreibung |
|---|---|
| `dataSetId` | **(Erforderlich)** Die Kennung des Datensatzes, den Sie löschen möchten. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu erstellten Löschanfrage zurück, einschließlich einer eindeutigen, vom System generierten und schreibgeschützten Kennung für die Anfrage. Diese kann zum Nachschlagen der Anfrage und Überprüfen ihres Status verwendet werden. Der **`status`** (Status) der Anfrage lautet zum Zeitpunkt der Erstellung *`"NEW"`*, und zwar solange, bis die Verarbeitung beginnt. Die **`dataSetId`** in der Antwort sollte mit der in der Anfrage gesendeten ***`dataSetId`*** übereinstimmen.

```json
{
    "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
    "imsOrgId": "{IMS_ORG}",
    "dataSetId": "5c802d3cd83fc114b741c4b5",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559025404,
    "updateEpoch": 1559025406
}
```

| Eigenschaft | Beschreibung |
|---|---|
| `id` | Die eindeutige, vom System generierte und schreibgeschützte Kennung der Löschanfrage. |
| `dataSetId` | Die Kennung des Datensatzes, wie in der POST-Anfrage angegeben. |

### Batch löschen

Um einen Batch zu löschen, muss die Batch-Kennung im Text der POST-Anfrage enthalten sein. Beachten Sie, dass Sie Batches für Datensätze, die auf Datensatzschemas basieren, nicht löschen können. Nur Batches für Datensätze, die auf Zeitreihenschemas basieren, können gelöscht werden.

>[!NOTE]
> Batches für Datensätze, die auf Datensatzschemas basieren, lassen sich nicht löschen, weil Datensatz-Batches vom Typ Datensatz frühere Datensätze überschreiben und daher nicht „rückgängig gemacht“ oder gelöscht werden können. Die einzige Möglichkeit, die Auswirkungen fehlerhafter Stapel für Datensätze zu entfernen, die auf Datensatzdaten basieren, besteht darin, den Stapel mit den richtigen Daten erneut zu erfassen, um die falschen Schema zu überschreiben.

Weiterführende Informationen zum Verhalten von Datensätzen und Zeitreihen finden Sie im Abschnitt [XDM-Datenverhalten](../../xdm/home.md#data-behaviors) in der Übersicht zu [!DNL XDM System]

**API-Format**

```http
POST /system/jobs
```

**Anfrage**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

| Eigenschaft | Beschreibung |
|---|---|
| `batchId` | **(Erforderlich)** Die Kennung des Batches, den Sie löschen möchten. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu erstellten Löschanfrage zurück, einschließlich einer eindeutigen, vom System generierten und schreibgeschützten Kennung für die Anfrage. Diese kann zum Nachschlagen der Anfrage und Überprüfen ihres Status verwendet werden. Der `"status"` (Status) der Anfrage lautet zum Zeitpunkt der Erstellung `"NEW"`, und zwar solange, bis die Verarbeitung beginnt. Die `"batchId"` in der Antwort sollte mit der in der Anfrage gesendeten `"batchId"` übereinstimmen.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{IMS_ORG}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559026131,
    "updateEpoch": 1559026132
}
```

| Eigenschaft | Beschreibung |
|---|---|
| `id` | Die eindeutige, vom System generierte und schreibgeschützte Kennung der Löschanfrage. |
| `batchId` | Die Kennung des Batches, wie in der POST-Anfrage angegeben. |

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

## Bestimmte Löschanfrage anzeigen {#view-a-specific-delete-request}

Zur Ansicht einer bestimmten Löschanfrage, einschließlich Details wie dem Status, können Sie eine GET-Anfrage (zum Nachschlagen) an den `/system/jobs`-Endpunkt stellen und die Kennung der Löschanfrage in den Pfad einschließen.

**API-Format**

```http
GET /system/jobs/{DELETE_REQUEST_ID}
```

| Parameter | Beschreibung |
|---|---|
| `{DELETE_REQUEST_ID}` | **(Erforderlich)** Die Kennung der Löschanfrage, die Sie anzeigen möchten. |

**Anfrage**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Die Antwort enthält die Details der Löschanfrage, einschließlich ihres aktualisierten Status. Die Kennung der Löschanfrage in der Antwort sollte mit der Kennung übereinstimmen, die im Anfragepfad gesendet wird.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{IMS_ORG}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "COMPLETED",
    "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
    "createEpoch": 1559026134,
    "updateEpoch": 1559026137
}
```

| Eigenschaften | Beschreibung |
|---|---|
| `jobType` | The type of job being created, in this case it will always return `"DELETE"`. |
| `status` | Der Status der Löschanfrage. Mögliche Werte: `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`. |
| `metrics` | An array that includes the number of records that have been processed (`"recordsProcessed"`) and the time in seconds that the request has been processing, or how long the request took to complete (`"timeTakenInSec"`). |

Once the delete request status is `"COMPLETED"` you can confirm that the data has been deleted by attempting to access the deleted data using the Data Access API. Anweisungen zum Zugreifen auf Datensätze und Batches mit der Data Access-API finden Sie in der [Dokumentation zu Data Access](../../data-access/home.md).

## Löschanfrage entfernen

[!DNL Experience Platform]Mit können Sie eine frühere Anfrage löschen. Dies kann aus verschiedenen Gründen nützlich sein, z. B. wenn der Löschauftrag nicht abgeschlossen wurde oder in der Verarbeitungsstufe hängengeblieben ist. Um eine Löschanfrage zu entfernen, können Sie eine Löschanfrage an den `/system/jobs`-Endpunkt stellen und die Kennung der Löschanfrage, die Sie entfernen möchten, in den Anfragepfad einschließen.

**API-Format**

```http
DELETE /system/jobs/{DELETE_REQUEST_ID}
```

| Parameter | Beschreibung |
|---|---|
| {DELETE_REQUEST_ID} | Die Kennung der Löschanfrage, die Sie entfernen möchten. |

**Anfrage**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Eine erfolgreiche Löschanfrage gibt den HTTP-Status 200 (OK) und einen leeren Antworttext zurück. Sie können prüfen, ob die Anfrage gelöscht wurde, indem Sie eine GET-Anfrage ausführen, um die Löschanfrage mittels ihrer Kennung anzuzeigen. Nun sollte ein HTTP-Status 404 (Nicht gefunden) zurückgegeben werden, was bedeutet, dass die Löschanfrage entfernt wurde.

## Nächste Schritte

Now that you know the steps involved in deleting datasets and batches from the [!DNL Profile Store] within [!DNL Experience Platform], you can safely delete data that has been added erroneously or that your organization no longer needs. Beachten Sie, dass Löschanfragen nicht rückgängig gemacht werden können. Daher sollten Sie Daten nur dann löschen, wenn Sie sicher sind, dass Sie sie jetzt und in Zukunft nicht mehr benötigen werden.

## Anhang {#appendix}

The following information is supplemental to the act of deleting a dataset from the [!DNL Profile Store].

### Deleting a dataset using the [!DNL Experience Platform] UI

When using the [!DNL Experience Platform] user interface to delete a dataset that has been enabled for [!DNL Profile], a dialog opens asking, &quot;Are you sure you want to delete this dataset from the [!DNL Experience Data Lake]? Verwenden Sie die &quot;p[!DNL rofile systems jobs]&quot;-API, um diesen Datensatz aus dem [!DNL Profile Service]zu löschen.&quot;

Wenn Sie in der Benutzeroberfläche auf **[!UICONTROL Löschen]** klicken, wird der Datensatz für die Erfassung deaktiviert. Er wird jedoch NICHT automatisch aus dem Backend gelöscht. Um den Datensatz dauerhaft zu löschen, müssen Sie mithilfe der Schritte in diesem Handbuch zum [Erstellen einer Löschanfrage](#create-a-delete-request) manuell eine Löschanfrage erstellen.

The following image shows the warning when attempting to delete a [!DNL Profile]-enabled dataset using the UI.

![](../images/delete-profile-dataset.png)

Weiterführende Informationen zum Arbeiten mit Datensätzen finden Sie in der [Datensatzübersicht](../../catalog/datasets/overview.md).