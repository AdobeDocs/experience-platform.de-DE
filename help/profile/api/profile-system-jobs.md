---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Entwicklerhandbuch für Customer Profil-API in Echtzeit
topic: guide
translation-type: tm+mt
source-git-commit: d0ccaa5511375253a2eca8f1235c2f953b734709
workflow-type: tm+mt
source-wordcount: '1506'
ht-degree: 2%

---


# Profil-Systemaufträge (Anforderungen löschen)

Mit der Adobe Experience Platform können Sie Daten aus mehreren Quellen erfassen und stabile Profil für einzelne Kunden erstellen. Daten, die in Platform aufgenommen werden, werden im Data Lake sowie im Echtzeit-Kundendatenspeicher gespeichert. Gelegentlich kann es erforderlich sein, einen Datensatz oder Stapel aus dem Profil-Store zu löschen, um Daten zu entfernen, die nicht mehr benötigt werden oder fehlerhaft hinzugefügt wurden. Dies erfordert die Verwendung der Echtzeit-Client-Profil-API zum Erstellen eines Profil-Systemauftrags (auch als &quot;Löschanforderung&quot;bezeichnet), der bei Bedarf auch modifiziert, überwacht oder entfernt werden kann.

>[!NOTE]
>Wenn Sie versuchen, Datasets oder Stapel aus dem Data Lake zu löschen, finden Sie Anweisungen in der Übersicht über den [Katalogdienst](../../catalog/home.md) .

## Erste Schritte

Die in diesem Handbuch verwendeten API-Endpunkte sind Teil der Real-time Customer Profil API. Bevor Sie fortfahren, lesen Sie bitte das Entwicklerhandbuch [zur](getting-started.md)Echtzeit-Customer Profil API. Insbesondere enthält der [Abschnitt](getting-started.md#getting-started) &quot;Erste Schritte&quot;des Profil-Entwicklerhandbuchs Links zu verwandten Themen, eine Anleitung zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtige Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen von Experience Platform-APIs benötigt werden.

## Ansichten löschen

Bei einer Löschanforderung handelt es sich um einen langwierigen, asynchronen Prozess, d. h., Ihr Unternehmen führt möglicherweise mehrere Löschanforderungen gleichzeitig aus. Um alle derzeit in Ihrem Unternehmen ausgeführten Löschanforderungen Ansicht, können Sie eine GET-Anforderung an den `/system/jobs` Endpunkt durchführen.

Sie können auch optionale Parameter für die Abfrage verwenden, um die Liste der in der Antwort zurückgegebenen Löschanforderungen zu filtern. Wenn Sie mehrere Parameter verwenden möchten, trennen Sie jeden Parameter mit einem kaufmännischen Und (&amp;).

**API-Format**

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| Parameter | Beschreibung |
|---|---|
| `start` | Versetzen Sie die Seite der zurückgegebenen Ergebnisse gemäß der Erstellungszeit der Anforderung. Beispiel: `start=4` |
| `limit` | Schränken Sie die Anzahl der zurückgegebenen Ergebnisse ein. Beispiel: `limit=10` |
| `page` | Gibt eine bestimmte Ergebnisseite gemäß der Erstellungszeit der Anforderung zurück. Beispiel: `page=2` |
| `sort` | Sortieren Sie die Ergebnisse nach einem bestimmten Feld in aufsteigender (`asc`) oder absteigender (`desc`) Reihenfolge. Der Sortierparameter funktioniert nicht, wenn mehrere Ergebnisseiten zurückgegeben werden. Beispiel: `sort=batchId:asc` |

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

Die Antwort enthält ein Array mit den untergeordneten Elementen mit einem Objekt für jede Löschanforderung, das die Details dieser Anforderung enthält.

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
| _page.count | Die Gesamtanzahl der Anforderungen. Diese Antwort wurde für den Weltraum abgeschnitten. |
| _page.next | Wenn eine zusätzliche Ergebnisseite vorhanden ist, wird die nächste Ergebnisseite Ansicht, indem der ID-Wert in einer [Suchanfrage](#view-a-specific-delete-request) durch den bereitgestellten Wert &quot;next&quot;ersetzt wird. |
| jobType | Der Typ des zu erstellenden Auftrags. In diesem Fall wird immer &quot;LÖSCHEN&quot;zurückgegeben. |
| status | Der Status der Löschanforderung. Mögliche Werte sind &quot;NEW&quot;, &quot;PROCESSING&quot;, &quot;COMPLETED&quot;, &quot;ERROR&quot;. |
| Metriken | Ein Objekt, das die Anzahl der verarbeiteten Datensätze (&quot;recordsProcessing&quot;) und die Zeit in Sekunden, die die Anforderung verarbeitet wurde, oder die Dauer der Anforderung (&quot;timeTakenInSec&quot;) enthält. |

## Create a delete request {#create-a-delete-request}

Die Initiierung einer neuen Löschanforderung erfolgt über eine POST-Anforderung an den `/systems/jobs` Endpunkt, wobei die ID des zu löschenden Datensatzes oder Stapels im Hauptteil der Anforderung angegeben wird.

### Löschen eines Datensatzes

Um einen Datensatz zu löschen, muss die DataSet-ID im Hauptteil der POST-Anforderung enthalten sein. Durch diese Aktion werden ALLE Daten für einen bestimmten Datensatz gelöscht. Mit Experience Platform können Sie Datensätze basierend auf Schemas aus Datensatz- und Zeitreihen löschen.

>[!CAUTION]
> Beim Versuch, einen Profil-aktivierten Datensatz mithilfe der Experience Platform-Benutzeroberfläche zu löschen, ist der Datensatz für die Erfassung deaktiviert, wird jedoch erst gelöscht, wenn mit der API eine Löschanforderung erstellt wurde. Weitere Informationen finden Sie im [Anhang](#appendix) zu diesem Dokument.

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
| dataSetId | **(Erforderlich)** Die ID des Datensatzes, den Sie löschen möchten. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu erstellten Löschanforderung zurück, einschließlich einer eindeutigen, systemgenerierten schreibgeschützten ID für die Anforderung. Dies kann zum Nachschlagen der Anforderung und zum Überprüfen ihres Status verwendet werden. Die `status` Anforderung wird zum Zeitpunkt der Erstellung `"NEW"` bis zur Verarbeitung ausgeführt. Die `dataSetId` in der Antwort sollte mit der in der Anforderung gesendeten `dataSetId` übereinstimmen.

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
| id | Die eindeutige, systemgenerierte schreibgeschützte ID der Löschanforderung. |
| dataSetId | Die ID des Datensatzes, wie in der POST-Anforderung angegeben. |

### Stapel löschen

Um einen Stapel zu löschen, muss die Stapel-ID im Hauptteil der POST-Anforderung enthalten sein. Es wird darauf hingewiesen, dass Sie keine Stapel für Datensätze löschen können, die auf Schemas basieren. Nur Stapel für Datensätze, die auf Zeitreihen-Schemas basieren, können gelöscht werden.

>[!NOTE]
> Stapel für Datensätze, die auf Datensatztypen basieren, können nicht gelöscht werden, weil Datensatztypen vorherige Datensätze überschreiben und daher nicht rückgängig gemacht oder gelöscht werden können. Die einzige Möglichkeit, die Auswirkungen fehlerhafter Stapel für Datensätze zu entfernen, die auf Datensatzdaten basieren, besteht darin, den Stapel mit den richtigen Daten zu erfassen, um die falschen Schema zu überschreiben.

Weitere Informationen zum Verhalten von Datensätzen und Zeitreihen finden Sie im [Abschnitt zu XDM-Datenverhalten](../../xdm/home.md#data-behaviors) in der XDM-Systemübersicht.

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
| batchId | **(Erforderlich)** Die ID des Stapels, den Sie löschen möchten. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu erstellten Löschanforderung zurück, einschließlich einer eindeutigen, systemgenerierten schreibgeschützten ID für die Anforderung. Dies kann zum Nachschlagen der Anforderung und zum Überprüfen ihres Status verwendet werden. Der &quot;Status&quot;für die Anforderung zum Zeitpunkt der Erstellung lautet &quot;NEU&quot;, bis die Verarbeitung beginnt. Die &quot;batchId&quot;in der Antwort sollte mit der &quot;batchId&quot;übereinstimmen, die in der Anforderung gesendet wurde.

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
| id | Die eindeutige, systemgenerierte schreibgeschützte ID der Löschanforderung. |
| batchId | Die ID des Stapels, wie in der POST-Anforderung angegeben. |

Wenn Sie versuchen, eine Löschanforderung für einen Datensatzdataset-Stapel zu starten, tritt ein Fehler auf 400-Ebene auf, ähnlich dem Folgenden:

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

## Ansicht einer bestimmten Löschanforderung {#view-a-specific-delete-request}

Zur Ansicht einer bestimmten Löschanforderung, einschließlich Details wie dem Status, können Sie eine GET-Anforderung (Lookup) an den `/system/jobs` Endpunkt ausführen und die ID der Löschanforderung in den Pfad einschließen.

**API-Format**

```http
GET /system/jobs/{DELETE_REQUEST_ID}
```

| Parameter | Beschreibung |
|---|---|
| {DELETE_REQUEST_ID} | **(Erforderlich)** Die ID der zu Ansicht Löschanforderung. |

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

Die Antwort enthält die Details der Löschanforderung, einschließlich des aktualisierten Status. Die ID der Löschanforderung in der Antwort sollte mit der ID übereinstimmen, die im Anforderungspfad gesendet wird.

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
| jobType | Der Typ des zu erstellenden Auftrags, in diesem Fall wird immer &quot;LÖSCHEN&quot;zurückgegeben. |
| status | Der Status der Löschanforderung. Mögliche Werte: &quot;NEW&quot;, &quot;PROCESSING&quot;, &quot;COMPLETED&quot;, &quot;FEHLER&quot;. |
| Metriken | Ein Array, das die Anzahl der verarbeiteten Datensätze (&quot;recordsProcessing&quot;) und die Zeit in Sekunden, in der die Anforderung verarbeitet wurde, oder die Dauer der Anforderung (&quot;timeTakenInSec&quot;) enthält. |

Sobald der Löschanforderungsstatus &quot;ABGESCHLOSSEN&quot;ist, können Sie bestätigen, dass die Daten gelöscht wurden, indem Sie versuchen, mithilfe der Datenzugriff-API auf die gelöschten Daten zuzugreifen. Anweisungen zum Zugriff auf Datensätze und Stapel mit der Datenzugriff-API finden Sie in der Dokumentation zum [Datenzugriff](../../data-access/home.md).

## Löschen einer Anforderung

Mit Experience Platform können Sie eine vorherige Anforderung löschen. Dies kann aus verschiedenen Gründen nützlich sein, z. B. wenn der Löschauftrag nicht abgeschlossen wurde oder in der Verarbeitungsstufe hängen geblieben ist. Um eine Löschanforderung zu entfernen, können Sie eine DELETE-Anforderung an den `/system/jobs` Endpunkt ausführen und die ID der Löschanforderung einschließen, die Sie in den Anforderungspfad entfernen möchten.

**API-Format**

```http
DELETE /system/jobs/{DELETE_REQUEST_ID}
```

| Parameter | Beschreibung |
|---|---|
| {DELETE_REQUEST_ID} | Die ID der Löschanforderung, die Sie entfernen möchten. |

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

Bei einer erfolgreichen Löschanforderung werden HTTP-Status 200 (OK) und ein leerer Antworttext zurückgegeben. Sie können bestätigen, dass die Anforderung gelöscht wurde, indem Sie eine GET-Anforderung ausführen, um die Löschanforderung mit ihrer ID Ansicht. Dadurch sollte ein HTTP-Status 404 (Nicht gefunden) zurückgegeben werden, der angibt, dass die Löschanforderung entfernt wurde.

## Nächste Schritte

Da Sie nun wissen, wie Sie Datasets und Stapel aus dem Profil Store in Experience Platform löschen, können Sie Daten, die irrtümlicherweise hinzugefügt wurden oder die Ihr Unternehmen nicht mehr benötigt, problemlos löschen. Bitte beachten Sie, dass eine Löschanforderung nicht rückgängig gemacht werden kann. Daher sollten Sie nur Daten löschen, die Sie sicher sind, dass Sie jetzt nicht mehr benötigen und in Zukunft nicht mehr benötigen.

## Anhang {#appendix}

Die folgenden Informationen ergänzen den Vorgang des Löschens eines Datensatzes aus dem Profil-Store.

### Löschen eines Datensatzes mithilfe der Benutzeroberfläche der Experience Platform

Wenn Sie mit der Benutzeroberfläche von Experience Platform einen zum Profil aktivierten Datensatz löschen, wird ein Dialogfeld mit der Frage angezeigt: &quot;Sind Sie sicher, dass Sie diesen Datensatz aus dem Experience Data Lake löschen möchten? Verwenden Sie die API &quot;Profil systems jobs&quot;, um diesen Datensatz aus dem Profil Service zu löschen.&quot;

Wenn Sie in der Benutzeroberfläche auf &quot; **Löschen** &quot;klicken, wird der Datensatz zur Erfassung deaktiviert. Der Datensatz wird jedoch NICHT automatisch im Backend gelöscht. Um den Datensatz dauerhaft zu löschen, muss eine Löschanforderung manuell mithilfe der Schritte in diesem Handbuch zum [Erstellen einer Löschanforderung](#create-a-delete-request)erstellt werden.

Die folgende Abbildung zeigt die Warnung, wenn versucht wird, einen Profil-aktivierten Datensatz mithilfe der Benutzeroberfläche zu löschen.

![](../images/delete-profile-dataset.png)

Weitere Informationen zum Arbeiten mit Datensätzen erhalten Sie zunächst in der Übersicht über die [Datensätze](../../catalog/datasets/overview.md).