---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;preview;sample
solution: Adobe Experience Platform
title: Profil-Vorschau - Echtzeit-Client-Profil-API
description: Adobe Experience Platform enables you to ingest customer data from multiple sources in order to build robust unified profiles for individual customers. As data enabled for Real-time Customer Profile is ingested into Platform, it is stored within the Profile data store. As the number of records in the Profile store increases or decreases, a sample job is run that includes information regarding how many profile fragments and merged profiles are in the data store. Using the Profile API you can preview the latest successful sample, as well as list profile distribution by dataset and by identity namespace.
topic: guide
translation-type: tm+mt
source-git-commit: 75a07abd27f74bcaa2c7348fcf43820245b02334
workflow-type: tm+mt
source-wordcount: '1442'
ht-degree: 6%

---


# Preview sample status endpoint (Profile preview)

Mit Adobe Experience Platform können Sie Kundendaten aus verschiedenen Quellen erfassen, um stabile einheitliche Profil für einzelne Kunden zu erstellen. As data enabled for Real-time Customer Profile is ingested into [!DNL Platform], it is stored within the Profile data store.

When the ingestion of records into the Profile store increases or decreases the total profile count by more than 5%, a job is triggered to update the count. For streaming data workflows, a check is done on an hourly basis to determine if the 5% increase or decrease threshold has been met. If it has, a job is automatically triggered to update the count. For batch ingestion, within 15 minutes of successfully ingesting a batch into the Profile store, if the 5% increase or decrease threshold is met, a job is run to update the count. Using the Profile API you can preview the latest successful sample job, as well as list profile distribution by dataset and by identity namespace.

These metrics are also available within the [!UICONTROL Profiles] section of the Experience Platform UI. For information on how to access Profile data using the UI, please visit the [[!DNL Profile] user guide](../ui/user-guide.md).

## Erste Schritte

The API endpoint used in this guide is part of the [[!DNL Real-time Customer Profile] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml). Before continuing, please review the [getting started guide](getting-started.md) for links to related documentation, a guide to reading the sample API calls in this document, and important information regarding required headers that are needed to successfully make calls to any [!DNL Experience Platform] API.

## Letzter Musterstatus der Ansicht {#view-last-sample-status}

Sie können eine GET an den `/previewsamplestatus` Endpunkt senden, um die Details zum letzten erfolgreichen Musterauftrag, der für Ihre IMS-Organisation ausgeführt wurde, Ansicht. Dies umfasst die Gesamtzahl der Profil im Beispiel sowie die Metrik zur Anzahl der Profil oder die Gesamtzahl der Profil, die Ihr Unternehmen innerhalb der Experience Platform hat. Die Profil-Anzahl wird nach dem Zusammenführen von Profil-Fragmenten generiert, um für jeden einzelnen Kunden ein Profil zu bilden. Mit anderen Worten: Ihre Organisation hat möglicherweise verschiedene Profilfragmente, die sich auf einen einzelnen Kunden beziehen, der mit Ihrer Marke über unterschiedliche Kanäle interagiert. Diese Fragmente würden jedoch zusammengeführt (gemäß der standardmäßigen Zusammenführungsrichtlinie) und eine Anzahl von „1“ zurückgeben, da sie alle mit derselben Person verbunden sind.

Die Profil-Anzahl umfasst auch Profil mit Attributen (Datensatzdaten) sowie Profil, die nur Zeitreihendaten (Ereignis) enthalten, wie z. B. Adobe Analytics-Profil. Der Musterauftrag wird regelmäßig aktualisiert, wenn Profil-Daten erfasst werden, um eine aktuelle Gesamtanzahl von Profilen innerhalb der Plattform bereitzustellen.

**API-Format**

```http
GET /previewsamplestatus
```

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Die Antwort enthält die Details zum letzten erfolgreichen Musterauftrag, der für das IMS-Unternehmen ausgeführt wurde.

>[!NOTE]
>
>In diesem Beispiel antworten `numRowsToRead` und `totalRows` sind gleich. Je nachdem, wie viele Profile Ihr Unternehmen in der Experience Platform hat, kann dies der Fall sein. Im Allgemeinen unterscheiden sich diese beiden Zahlen jedoch, wobei `numRowsToRead` die kleinere Zahl die Stichprobe als Untergruppe der Gesamtanzahl der Profil darstellt (`totalRows`).

```json
{
  "numRowsToRead": "41003",
  "cosmosDocCount": "\"300803\"",
  "totalFragmentCount": 47429,
  "lastSuccessfulBatchTimestamp": "\"null\"",
  "streamingDriven": "\"false\"",
  "totalRows": "41003",
  "lastBatchId": "\"null\"",
  "status": "TASK_FINISHED",
  "samplingRatio": 1.0,
  "mergeStrategy": "timestampOrdered_auto",
  "lastSampledTimestamp": "2020-08-01 17:57:57.0"
}
```

| Eigenschaft | Beschreibung |
|---|---|
| `numRowsToRead` | Die Gesamtzahl der zusammengeführten Profil im Beispiel. |
| `cosmosDocCount` | Gesamtanzahl der Dokumente in Kosmos. |
| `totalFragmentCount` | Gesamtanzahl der Profil-Fragmente im Profil Store. |
| `lastSuccessfulBatchTimestamp` | Letzter erfolgreicher Zeitstempel für die Stapelverarbeitung. |
| `streamingDriven` | *Dieses Feld ist veraltet und enthält keine Bedeutung für die Antwort.* |
| `totalRows` | Gesamtanzahl der zusammengeführten Profil in der Experience-Plattform, auch als &quot;Profil-Anzahl&quot;bezeichnet. |
| `lastBatchId` | Letzte Batch-Erfassungskennung. |
| `status` | Status des letzten Beispiels. |
| `samplingRatio` | Verhältnis der beprobten (`numRowsToRead`) zusammengeführten Profil zu den zusammengeführten (`totalRows`) Profilen insgesamt, ausgedrückt als Prozentsatz im Dezimalformat. |
| `mergeStrategy` | In der Stichprobe verwendete Merge-Strategie. |
| `lastSampledTimestamp` | Letzter erfolgreicher Beispiel-Zeitstempel. |

## Verteilung von Liste-Profil nach Datensatz

To see the distribution of profiles by dataset, you can perform a GET request to the `/previewsamplestatus/report/dataset` endpoint.

**API-Format**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| Parameter | Beschreibung |
|---|---|
| `date` | Geben Sie das Datum des zurückzugebenden Berichts an. Wenn am Datum mehrere Berichte ausgeführt wurden, wird der letzte Bericht für dieses Datum zurückgegeben. Wenn für das angegebene Datum kein Bericht vorhanden ist, wird der Fehler &quot;404&quot;zurückgegeben. Wenn kein Datum angegeben ist, wird der letzte Bericht zurückgegeben. Format: JJJJ-MM-TT. Beispiel: `date=2024-12-31` |

**Anfrage**

Die folgende Anforderung verwendet den `date` Parameter, um den letzten Bericht für das angegebene Datum zurückzugeben.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Die Antwort enthält ein `data` Array mit einer Liste von DataSet-Objekten. Die angezeigte Antwort wurde abgeschnitten und zeigt drei Datensätze an.

>[!NOTE]
>
>Wenn mehrere Berichte für das Datum vorhanden waren, wird nur der letzte zurückgegeben. Wenn für das bereitgestellte Datum kein Datensatzbericht vorhanden war, wird HTTP-Status 404 (Nicht gefunden) zurückgegeben.

```json
{
  "data": [
    {
      "sampleCount": 12577,
      "samplePercentage": 0.306734,
      "fullIDsCount": 20988,
      "fullIDsPercentage": 0.511865,
      "name": "CRM Profiles",
      "description": "Profiles from the CRM.",
      "value": "5f160106be34361915754b9c",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697",
    },
    {
      "sampleCount": 12938,
      "samplePercentage": 0.315538,
      "fullIDsCount": 21796,
      "fullIDsPercentage": 0.531571,
      "name": "AAM Authenticated Profiles",
      "description": "This data set contains AAM authenticated profiles.",
      "value": "5dc77ec6eed47f18a796ca90",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697"
    },
    {
      "sampleCount": 22725,
      "samplePercentage": 0.554228,
      "fullIDsCount": 41003,
      "fullIDsPercentage": 1.0,
      "name": "Loyalty Program Members",
      "description": "Members of the loyalty program at all levels.",
      "value": "5d0fda92274e55144d4de620",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697"
    }
  ],
  "reportTimestamp": "2020-08-01T17:57:58.697"
}
```

| Eigenschaft | Beschreibung |
|---|---|
| `sampleCount` | Die Gesamtzahl der zusammengeführten Profil mit dieser Datensatzkennung, die als Stichprobe erfasst wurden. |
| `samplePercentage` | Der `sampleCount` als Prozentsatz der Gesamtzahl der zusammengeführten Profil der Stichprobe (der `numRowsToRead` im [letzten Stichprobenstatus](#view-last-sample-status)zurückgegebene Wert), ausgedrückt als Dezimalformat. |
| `fullIDsCount` | Die Gesamtanzahl der zusammengeführten Profil mit dieser DataSet-ID. |
| `fullIDsPercentage` | Der `fullIDsCount` als Prozentsatz der Gesamtzahl der zusammengeführten Profil (der `totalRows` im [letzten Musterstatus](#view-last-sample-status)zurückgegebene Wert), ausgedrückt als Dezimalformat. |
| `name` | Der Name des Datensatzes, wie er bei der Erstellung des Datensatzes angegeben wird. |
| `description` | Die Beschreibung des Datensatzes, wie bei der Erstellung des Datensatzes angegeben. |
| `value` | Die ID des Datensatzes. |
| `streamingIngestionEnabled` | Ob der Datensatz für die Streaming-Erfassung aktiviert ist. |
| `createdUser` | Die Benutzer-ID des Benutzers, der den Datensatz erstellt hat. |
| `reportTimestamp` | Der Zeitstempel des Berichts. Wenn während der Anforderung ein `date` Parameter angegeben wurde, gilt der zurückgegebene Bericht für das angegebene Datum. If no `date` parameter is provided, the most recent report is returned. |



## Verteilung von Liste-Profil nach Namensraum

Sie können eine GET-Anforderung an den `/previewsamplestatus/report/namespace` Endpunkt ausführen, um die Aufschlüsselung nach Identitäts-Namensraum für alle zusammengeführten Profil in Ihrem Profil Store Ansicht. Identity Namensräume sind eine wichtige Komponente des Adobe Experience Platform Identity Service, die als Indikatoren für den Kontext dient, auf den sich Kundendaten beziehen. To learn more, visit the [identity namespace overview](../../identity-service/namespaces.md).

>[!NOTE]
>
>Die Gesamtanzahl der Profil nach Namensraum (addieren Sie die für jeden Namensraum angezeigten Werte) ist immer höher als die Metrik für die Anzahl der Profil, da ein Profil mit mehreren Namensräumen verknüpft werden könnte. Wenn ein Kunde beispielsweise auf mehr als einem Kanal mit Ihrer Marke interagiert, werden mehrere Namensraum mit diesem Kunden verknüpft.

**API-Format**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| Parameter | Beschreibung |
|---|---|
| `date` | Specify the date of the report to be returned. If multiple reports were run on the date, the most recent report for that date will be returned. If a report does not exist for the specified date, a 404 error will be returned. If no date is specified, the most recent report will be returned. Format: YYYY-MM-DD. Beispiel: `date=2024-12-31` |

**Anfrage**

The following request does not specify a `date` parameter and will therefore return the most recent report.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

The response includes a `data` array, with individual objects containing the details for each namespace. The response shown has been truncated to show four namespaces.

```json
{
  "data": [
    {
      "sampleCount": 12148,
      "samplePercentage": 0.296271,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 13141,
      "fullIDsCount": 12631,
      "fullIDsPercentage": 0.308051,
      "code": "Email",
      "value": "6"
    },
    {
      "sampleCount": 6989,
      "samplePercentage": 0.170451,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 7543,
      "fullIDsCount": 7042,
      "fullIDsPercentage": 0.171744,
      "code": "ECID",
      "value": "4"
    },
    {
      "sampleCount": 888,
      "samplePercentage": 0.021657,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 3801,
      "fullIDsCount": 3206,
      "fullIDsPercentage": 0.078189,
      "code": "AAID",
      "value": "10"
    },
    {
      "sampleCount": 21809,
      "samplePercentage": 0.531888,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 27023,
      "fullIDsCount": 21936,
      "fullIDsPercentage": 0.534985,
      "code": "Phone",
      "value": "7"
    }
  ],
  "reportTimestamp": "2020-08-01T17:57:58.697"
}
```

| Eigenschaft | Beschreibung |
|---|---|
| `sampleCount` | The total number of sampled merged profiles in the namespace. |
| `samplePercentage` | The `sampleCount` as a percentage of sampled merged profiles (the `numRowsToRead` value as returned in the [last sample status](#view-last-sample-status)), expressed in decimal format. |
| `reportTimestamp` | Der Zeitstempel des Berichts. If a `date` parameter was provided during the request, the report returned is for the date provided. Wenn kein `date` Parameter angegeben ist, wird der letzte Bericht zurückgegeben. |
| `fullIDsFragmentCount` | The total number of profile fragments in the namespace. |
| `fullIDsCount` | Die Gesamtzahl der zusammengeführten Profil im Namensraum. |
| `fullIDsPercentage` | Der `fullIDsCount` als Prozentsatz der zusammengeführten Profil insgesamt (der `totalRows` im [letzten Musterstatus](#view-last-sample-status)zurückgegebene Wert), ausgedrückt als Dezimalformat. |
| `code` | Die `code` für den Namensraum. Dies kann bei der Arbeit mit Namensräumen mithilfe der [Adobe Experience Platform Identity Service API](../../identity-service/api/list-namespaces.md) gefunden werden und wird auch als [!UICONTROL Identitätssymbol] in der Benutzeroberfläche der Experience Platform bezeichnet. To learn more, visit the [identity namespace overview](../../identity-service/namespaces.md). |
| `value` | Der `id` Wert für den Namensraum. Dies kann bei der Arbeit mit Namensräumen mithilfe der [Identitätsdienst-API](../../identity-service/api/list-namespaces.md)gefunden werden. |

## Nächste Schritte

Sie können auch ähnliche Schätzungen und Vorschauen für Informationen auf Zusammenfassungsebene der Ansicht zu Ihren Segmentdefinitionen verwenden, um sicherzustellen, dass Sie die erwartete Audience isolieren. Detaillierte Anweisungen zum Arbeiten mit Segmentansätzen und -schätzungen mithilfe der [!DNL Adobe Experience Platform Segmentation Service] API finden Sie im Handbuch [zu](../../segmentation/api/previews-and-estimates.md)Vorschauen und [!DNL Segmentation] Vorschauen und zu den Abschätzungsendpunkten, das Teil des API-Entwicklerhandbuchs ist.

