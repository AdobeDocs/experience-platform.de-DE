---
keywords: Experience Platform; Profil; Echtzeit-Kundenprofil; Fehlerbehebung; API
title: API-Endpunkt für Profilsystemaufträge
type: Documentation
description: Mit Adobe Experience Platform können Sie einen Datensatz oder Batch aus dem Profilspeicher löschen, um Echtzeit-Kundenprofildaten zu entfernen, die nicht mehr benötigt werden oder fehlerhaft hinzugefügt wurden. Dazu muss die Profil-API zum Erstellen eines Profilsystemauftrags oder einer Löschanfrage verwendet werden.
exl-id: 75ddbf2f-9a54-424d-8569-d6737e9a590e
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1316'
ht-degree: 70%

---

# Endpunkt für Profilsystemaufträge (Löschanfragen)

Mit Adobe Experience Platform können Sie Daten aus verschiedenen Quellen erfassen und zuverlässige Profile für einzelne Kunden einrichten. Daten, die in erfasst werden [!DNL Platform] wird im [!DNL Data Lake]und wenn die Datensätze für Profil aktiviert wurden, werden diese Daten im [!DNL Real-Time Customer Profile] auch Datenspeicher. Gelegentlich kann es erforderlich sein, Datensätze oder Batches aus dem Profilspeicher zu löschen, um Daten zu entfernen, die nicht mehr benötigt werden oder irrtümlich hinzugefügt wurden. Dazu muss die [!DNL Real-Time Customer Profile] API zum Erstellen einer [!DNL Profile] Systemauftrag oder `delete request`, die bei Bedarf auch geändert, überwacht oder entfernt werden können.

>[!NOTE]
>
>Wenn Sie versuchen, Datensätze oder Batches aus dem [!DNL Data Lake], besuchen Sie bitte die [Catalog Service - Übersicht](../../catalog/home.md) für weitere Informationen.

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil von [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Bevor Sie fortfahren, lesen Sie das Handbuch [Erste Schritte](getting-started.md) mit Links zur zugehörigen Dokumentation, einer Anleitung zum Lesen der API-Beispielaufrufe in diesem Dokument und wichtigen Informationen zu den erforderlichen Kopfzeilen, die für die erfolgreiche Ausführung von Aufrufen an eine Experience Platform-API erforderlich sind.

## Löschanfragen anzeigen

Bei einer Löschanfrage handelt es sich um einen langwierigen, asynchronen Prozess, d. h., Ihre Organisation führt möglicherweise mehrere Löschanfragen gleichzeitig aus. Um alle derzeit in Ihrer Organisation ausgeführten Löschanfragen anzuzeigen, können Sie eine GET-Anfrage an den `/system/jobs`-Endpunkt stellen.

Außerdem können Sie optionale Abfrageparameter verwenden, um die Liste der in der Antwort zurückgegebenen Löschanfragen zu filtern. Wenn Sie mehrere Parameter verwenden möchten, trennen Sie die einzelnen Parameter durch ein kaufmännisches Und-Zeichen (`&`).

**API-Format**

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| Parameter | Beschreibung |
|---|---|
| `start` | Versatz der Seite mit den zurückgegebenen Ergebnissen, unter Berücksichtigung der Erstellungszeit der Anfrage. Beispiel: `start=4` |
| `limit` | Schränkt die Anzahl der zurückgegebenen Ergebnisse ein. Beispiel: `limit=10` |
| `page` | Gibt eine bestimmte Seite mit Ergebnissen zurück, unter Berücksichtigung der Erstellungszeit der Anfrage. Beispiel: `page=2` |
| `sort` | Sortiert Ergebnisse nach einem bestimmten Feld in aufsteigender (`asc`) oder absteigender (`desc`) Reihenfolge. Der Sortierparameter funktioniert nicht, wenn mehrere Ergebnisseiten zurückgegeben werden. Beispiel: `sort=batchId:asc` |

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
|---|---|
| `_page.count` | Die Gesamtanzahl der Anfragen. Diese Antwort wurde aus Platzgründen abgeschnitten. |
| `_page.next` | Wenn eine zusätzliche Ergebnisseite vorhanden ist, zeigen Sie die nächste Ergebnisseite an, indem Sie den ID-Wert in einer [Suchanfrage](#view-a-specific-delete-request) mit dem `"next"` bereitgestellter Wert. |
| `jobType` | Der Typ des zu erstellenden Auftrags. In diesem Fall wird immer `"DELETE"`. |
| `status` | Der Status der Löschanfrage. Mögliche Werte sind `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`. |
| `metrics` | Ein Objekt, das die Anzahl der verarbeiteten Datensätze enthält (`"recordsProcessed"`) und die Zeit in Sekunden, die die Anfrage verarbeitet wurde oder wie lange die Anfrage gedauert hat (`"timeTakenInSec"`). |

## Löschanfrage erstellen {#create-a-delete-request}

Die Initiierung einer neuen Löschanfrage erfolgt über eine POST-Anfrage an den `/systems/jobs`-Endpunkt, wobei die Kennung des zu löschenden Datensatzes oder Batches im Text der Anfrage angegeben wird.

### Datensatz löschen

Um einen Datensatz aus dem Profilspeicher zu löschen, muss die Datensatz-ID im Hauptteil der POST-Anfrage enthalten sein. Durch diese Aktion werden ALLE Daten für einen bestimmten Datensatz gelöscht. [!DNL Experience Platform]Mit können Sie Datensätze basierend auf Datensatz- und Zeitreihenschemas löschen.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "dataSetId": "5c802d3cd83fc114b741c4b5"
      }'
```

| Eigenschaft | Beschreibung |
|---|---|
| `dataSetId` | **(Erforderlich)** Die Kennung des Datensatzes, den Sie löschen möchten. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu erstellten Löschanfrage zurück, einschließlich einer eindeutigen, vom System generierten und schreibgeschützten Kennung für die Anfrage. Diese kann zum Nachschlagen der Anfrage und Überprüfen ihres Status verwendet werden. Der `status` (Status) der Anfrage lautet zum Zeitpunkt der Erstellung `"NEW"`, und zwar solange, bis die Verarbeitung beginnt. Die `dataSetId` in der Antwort sollte mit der in der Anfrage gesendeten `dataSetId` übereinstimmen.

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
|---|---|
| `id` | Die eindeutige, vom System generierte und schreibgeschützte Kennung der Löschanfrage. |
| `dataSetId` | Die Kennung des Datensatzes, wie in der POST-Anfrage angegeben. |

### Batch löschen

Um einen Batch zu löschen, muss die Batch-Kennung im Text der POST-Anfrage enthalten sein. Beachten Sie, dass Sie Batches für Datensätze, die auf Datensatzschemas basieren, nicht löschen können. Nur Batches für Datensätze, die auf Zeitreihenschemas basieren, können gelöscht werden.

>[!NOTE]
>
> Batches für Datensätze, die auf Datensatzschemas basieren, lassen sich nicht löschen, weil Datensatz-Batches vom Typ Datensatz frühere Datensätze überschreiben und daher nicht „rückgängig gemacht“ oder gelöscht werden können. Die einzige Möglichkeit, die Auswirkungen fehlerhafter Batches für Datensätze zu entfernen, die auf Datensatzschemas basieren, besteht darin, den Batch mit den richtigen Daten neu zu erfassen, um die falschen Datensätze zu überschreiben.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

| Eigenschaft | Beschreibung |
|---|---|
| `batchId` | **(Erforderlich)** Die Kennung des Batches, den Sie löschen möchten. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu erstellten Löschanfrage zurück, einschließlich einer eindeutigen, vom System generierten und schreibgeschützten Kennung für die Anfrage. Diese kann zum Nachschlagen der Anfrage und Überprüfen ihres Status verwendet werden. Der `"status"` (Status) der Anfrage lautet zum Zeitpunkt der Erstellung `"NEW"`, und zwar solange, bis die Verarbeitung beginnt. Die `"batchId"` -Wert in der Antwort sollte mit dem `"batchId"` -Wert, der in der Anfrage gesendet wird.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{ORG_ID}",
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
curl -X GET \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Die Antwort enthält die Details der Löschanfrage, einschließlich ihres aktualisierten Status. Die Kennung der Löschanfrage in der Antwort (die `"id"` -Wert) mit der im Anfragepfad gesendeten ID übereinstimmen.

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
|---|---|
| `jobType` | Der Typ des zu erstellenden Auftrags, in diesem Fall wird immer `"DELETE"`. |
| `status` | Der Status der Löschanfrage. Mögliche Werte: `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`. |
| `metrics` | Ein Array, das die Anzahl der verarbeiteten Datensätze enthält (`"recordsProcessed"`) und die Zeit in Sekunden, die die Anfrage verarbeitet wurde oder wie lange die Anfrage gedauert hat (`"timeTakenInSec"`). |

Sobald der Löschanfragestatus `"COMPLETED"` Sie können bestätigen, dass die Daten gelöscht wurden, indem Sie versuchen, mithilfe der Data Access API auf die gelöschten Daten zuzugreifen. Anweisungen zum Zugreifen auf Datensätze und Batches mit der Data Access-API finden Sie in der [Dokumentation zu Data Access](../../data-access/home.md).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Bei erfolgreicher Löschanfrage werden der HTTP-Status 200 (OK) und ein leerer Antworttext zurückgegeben. Sie können prüfen, ob die Anfrage gelöscht wurde, indem Sie eine GET-Anfrage ausführen, um die Löschanfrage mittels ihrer Kennung anzuzeigen. Nun sollte ein HTTP-Status 404 (Nicht gefunden) zurückgegeben werden, was bedeutet, dass die Löschanfrage entfernt wurde.

## Nächste Schritte

Jetzt wissen Sie, welche Schritte beim Löschen von Datensätzen und Batches aus der [!DNL Profile Store] Innerhalb [!DNL Experience Platform]können Sie Daten löschen, die irrtümlich hinzugefügt wurden oder die Ihre Organisation nicht mehr benötigt. Beachten Sie, dass Löschanfragen nicht rückgängig gemacht werden können. Daher sollten Sie Daten nur dann löschen, wenn Sie sicher sind, dass Sie sie jetzt und in Zukunft nicht mehr benötigen werden.
