---
keywords: Experience Platform;Profil;Echtzeit-Kundenprofil;Fehlerbehebung;API;Vorschau;Beispiel
title: API-Endpunkt für Musterstatus der Vorschau (Profilvorschau)
description: Der Endpunkt für den Vorschaubeispielstatus der Echtzeit-Kundenprofil-API ermöglicht Ihnen die Vorschau des neuesten erfolgreichen Beispiels Ihrer Profildaten, die Auflistung der Profilverteilung nach Datensatz und Identität und die Erstellung von Berichten mit Datensatzüberschneidungen, Identitätsüberschneidungen und nicht zugeordneten Profilen.
role: Developer
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
source-git-commit: bb2cfb479031f9e204006ba489281b389e6c6c04
workflow-type: tm+mt
source-wordcount: '2306'
ht-degree: 6%

---

# Musterstatus-Endpunkt für Vorschau (Profilvorschau)

Mit Adobe Experience Platform können Sie Kundendaten aus verschiedenen Quellen aufnehmen, um ein robustes, einheitliches Profil für jeden einzelnen Ihrer Kunden zu erstellen. Bei der Aufnahme von Daten in Experience Platform wird ein Beispielvorgang ausgeführt, um die Profilanzahl und andere Metriken zu aktualisieren, die sich auf Echtzeit-Kundenprofildaten beziehen.

Die Ergebnisse dieses Beispielauftrags können mit dem `/previewsamplestatus`-Endpunkt, der Teil der Echtzeit-Kundenprofil-API ist, angezeigt werden. Dieser Endpunkt kann auch verwendet werden, um Profilverteilungen sowohl nach Datensatz als auch nach Identity-Namespace aufzulisten und mehrere Berichte zu generieren, um einen Einblick in die Zusammensetzung des Profilspeichers Ihres Unternehmens zu erhalten. Dieses Handbuch führt Sie durch die Schritte, die zum Anzeigen dieser Metriken mithilfe des `/previewsamplestatus`-API-Endpunkts erforderlich sind.

>[!NOTE]
>
>Als Teil der Segmentierungs-Service-API von Adobe Experience Platform stehen Schätzungs- und Vorschau-Endpunkte zur Verfügung, mit denen Sie Informationen auf Zusammenfassungsebene zu Segmentdefinitionen anzeigen können, um sicherzustellen, dass Sie die erwartete Zielgruppe isolieren. Ausführliche Schritte zum Arbeiten mit Vorschau- und Schätzendpunkten finden Sie im [Handbuch zu Vorschauen und &#x200B;](../../segmentation/api/previews-and-estimates.md)-Endpunkten, das Teil des [!DNL Segmentation]-API-Entwicklerhandbuchs ist.

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil der [[!DNL Real-Time Customer Profile] API](https://www.adobe.com/go/profile-apis-en). Bevor Sie fortfahren, lesen Sie im Handbuch [Erste Schritte](getting-started.md) die Links zu entsprechenden Dokumentationen, den Leitfaden zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtige Informationen zu Kopfzeilen, die für das erfolgreiche Aufrufen einer [!DNL Experience Platform]-API erforderlich sind.

## Profilfragmente im Vergleich zu zusammengeführten Profilen

Dieses Handbuch verweist sowohl auf „Profilfragmente“ als auch auf „zusammengeführte Profile“. Es ist wichtig, den Unterschied zwischen diesen Begriffen zu verstehen, bevor Sie fortfahren.

Jedes einzelne Kundenprofil besteht aus mehreren Profilfragmenten, die zu einer einzigen Ansicht dieses Kunden zusammengeführt wurden. Wenn ein Kunde beispielsweise über mehrere Kanäle mit Ihrer Marke interagiert, verfügt Ihr Unternehmen wahrscheinlich über mehrere Profilfragmente, die sich auf diesen einzelnen Kunden beziehen und in mehreren Datensätzen enthalten sind.

Wenn Profilfragmente in Experience Platform aufgenommen werden, werden sie zusammengeführt (auf der Grundlage einer Zusammenführungsrichtlinie), um ein einziges Profil für diesen Kunden zu erstellen. Daher ist die Gesamtzahl der Profilfragmente wahrscheinlich immer höher als die Gesamtzahl der zusammengeführten Profile, da jedes Profil aus mehreren Fragmenten besteht.

Um mehr über Profile und ihre Rolle in Experience Platform zu erfahren, lesen Sie zunächst die [Übersicht über das Echtzeit-Kundenprofil](../home.md).

## Wie der Beispielvorgang ausgelöst wird

Wenn Daten, die für das Echtzeit-Kundenprofil aktiviert sind, in [!DNL Experience Platform] aufgenommen werden, werden sie im Profildatenspeicher gespeichert. Wenn die Aufnahme von Datensätzen in den Profilspeicher die Gesamtprofilanzahl um mehr als 3 % erhöht oder verringert, wird ein Sampling-Auftrag ausgelöst, um die Anzahl zu aktualisieren. Die Art und Weise, wie die Stichprobe ausgelöst wird, hängt von der Art der Aufnahme ab, die verwendet wird:

* Bei **Streaming-Daten** Workflows wird stündlich überprüft, ob der Schwellenwert von 3 % für die Erhöhung oder Verringerung erreicht wurde. Ist dies der Fall, wird automatisch ein Beispielvorgang ausgelöst, um die Anzahl zu aktualisieren.
* Bei **Batch-Aufnahme** wird innerhalb von 15 Minuten nach der erfolgreichen Aufnahme eines Batches in den Profilspeicher ein Auftrag ausgeführt, um die Anzahl zu aktualisieren, wenn der Schwellenwert von 3 % für Erhöhung oder Verringerung erreicht ist. Mit der Profil-API können Sie den neuesten erfolgreichen Beispielvorgang in der Vorschau anzeigen sowie die Profilverteilung nach Datensatz und Identity-Namespace auflisten.

Die Metriken Profilanzahl und Profile nach Namespace sind auch im Abschnitt [!UICONTROL Profiles] der Experience Platform-Benutzeroberfläche verfügbar. Informationen zum Zugriff auf Profildaten über die Benutzeroberfläche finden Sie im [[!DNL Profile] UI-Handbuch](../ui/user-guide.md).

## Status der letzten Stichprobe anzeigen {#view-last-sample-status}

Sie können die Details des letzten erfolgreichen Beispielauftrags anzeigen, der für Ihr Unternehmen ausgeführt wurde, indem Sie eine GET-Anfrage an den `/previewsamplestatus`-Endpunkt stellen. Dieser Bericht enthält die Gesamtzahl der Profile in der Stichprobe sowie die Metrik zur Profilanzahl oder die Gesamtzahl der Profile, die Ihr Unternehmen in Experience Platform hat.

Die Profilanzahl wird nach dem Zusammenführen von Profilfragmenten generiert, um für jeden einzelnen Kunden ein einziges Profil zu bilden. Mit anderen Worten: Wenn Profilfragmente zusammengeführt werden, geben sie die Anzahl „1“ des Profils zurück, da sie alle mit derselben Person verbunden sind.

Die Profilanzahl umfasst auch Profile mit Attributen (Datensatzdaten) sowie Profile, die nur Zeitreihen-(Ereignis-)Daten enthalten, z. B. Adobe Analytics-Profile. Der Beispielvorgang wird regelmäßig aktualisiert, während Profildaten aufgenommen werden, um eine aktuelle Gesamtzahl von Profilen in Experience Platform bereitzustellen.

**API-Format**

```http
GET /previewsamplestatus
```

**Anfrage**

+++ Eine Beispielanfrage zur Anzeige des letzten Beispielstatus.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status-Code 200 zurück und enthält die Details für den letzten erfolgreichen Beispielvorgang, der für die Organisation ausgeführt wurde.

+++ Eine Beispielantwort, die den letzten Beispielstatus enthält.

>[!NOTE]
>
>In dieser Beispielantwort sind `numRowsToRead` und `totalRows` identisch. Je nach der Anzahl der Profile in Experience Platform kann dies der Fall sein. Im Allgemeinen sind diese beiden Zahlen jedoch unterschiedlich, wobei `numRowsToRead` die kleinere Zahl ist, da sie die Stichprobe als Teilmenge der Gesamtzahl der Profile darstellt (`totalRows`).

```json
{
  "numRowsToRead": "41003",
  "sampleJobRunning": {
    "status": true,
    "submissionTimestamp": "2020-08-01 17:57:57.0"
  },
  "docCount": "\"300803\"",
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
| -------- | ----------- |
| `numRowsToRead` | Die Gesamtzahl der zusammengeführten Profile in der Stichprobe. |
| `sampleJobRunning` | Ein boolescher Wert, der `true` zurückgibt, wenn ein Beispielvorgang ausgeführt wird. Bietet Transparenz bezüglich der Latenz, die beim Hochladen einer Batch-Datei auftritt, bis zum Zeitpunkt des tatsächlichen Hinzufügens zur Profilspeicherung. |
| `docCount` | Gesamtanzahl der Dokumente in der Datenbank. |
| `totalFragmentCount` | Gesamtzahl der Profilfragmente im Profilspeicher. |
| `lastSuccessfulBatchTimestamp` | Zeitstempel der letzten erfolgreichen Batch-Aufnahme. |
| `streamingDriven` | *Dieses Feld wird nicht mehr unterstützt und hat keine Bedeutung für die Antwort.* |
| `totalRows` | Die Gesamtzahl der zusammengeführten Profile in Experience Platform, auch als Profilanzahl bezeichnet. |
| `lastBatchId` | ID der letzten Batch-Aufnahme. |
| `status` | Status der letzten Stichprobe. |
| `samplingRatio` | Verhältnis der abgefragten zusammengeführten Profile (`numRowsToRead`) zu den gesamten zusammengeführten Profilen (`totalRows`), ausgedrückt als Prozentsatz im Dezimalformat. |
| `mergeStrategy` | Im Beispiel verwendete Zusammenführungsstrategie. |
| `lastSampledTimestamp` | Letzter erfolgreicher Beispiel-Zeitstempel. |

+++

## Auflisten der Profilverteilung nach Datensatz

Sie können die Profilverteilung nach Datensatz anzeigen, indem Sie eine GET-Anfrage an den `/previewsamplestatus/report/dataset`-Endpunkt senden.

**API-Format**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| Abfrageparameter | Beschreibung | Beispiel |
| --------------- | ----------- | ------- |
| `date` | Geben Sie das Datum des zurückzugebenden Berichts an. Wenn am Datum mehrere Berichte ausgeführt wurden, wird der aktuelle Bericht für dieses Datum zurückgegeben. Wenn für das angegebene Datum kein Bericht vorhanden ist, wird der Fehler 404 (Nicht gefunden) zurückgegeben. Wenn kein Datum angegeben wird, wird der letzte Bericht zurückgegeben. Format: JJJJ-MM-TT. | `date=2024-12-31` |

**Anfrage**

Die folgende Anfrage verwendet den `date`-Parameter, um den letzten Bericht für das angegebene Datum zurückzugeben.

+++ Eine Beispielanfrage zum Abrufen der Profilverteilung nach Datensatz.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**Antwort**

>[!NOTE]
>
>Wenn für das Datum mehrere Berichte vorhanden sind, wird nur der neueste Bericht zurückgegeben. Wenn für das angegebene Datum kein Datensatzbericht vorhanden ist, wird der HTTP-Status 404 (Nicht gefunden) zurückgegeben.

Eine erfolgreiche Antwort gibt den HTTP-Status-Code 200 zurück und enthält ein `data`-Array, das eine Liste der Datensatzobjekte enthält.

+++ Eine Beispielantwort, die die neuesten Datensatzobjekte enthält.

>[!NOTE]
>
>Die folgende angezeigte Antwort wurde gekürzt, um drei Datensätze anzuzeigen.

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
| -------- | ----------- |
| `sampleCount` | Die Gesamtzahl der stichprobenweise erfassten zusammengeführten Profile mit dieser Datensatz-ID. |
| `samplePercentage` | Der `sampleCount` als Prozentsatz der Gesamtzahl der abgefragten zusammengeführten Profile (der `numRowsToRead` Wert, wie er im [letzten Beispielstatus) zurückgegeben wurde](#view-last-sample-status) ausgedrückt im Dezimalformat. |
| `fullIDsCount` | Die Gesamtzahl der zusammengeführten Profile mit dieser Datensatz-ID. |
| `fullIDsPercentage` | Der `fullIDsCount` als Prozentsatz der Gesamtzahl der zusammengeführten Profile (der `totalRows`, wie im [letzten Beispielstatus) &#x200B;](#view-last-sample-status) Dezimalformat zurückgegeben. |
| `name` | Der Name des Datensatzes, wie er bei der Erstellung des Datensatzes angegeben wurde. |
| `description` | Die Beschreibung des Datensatzes, die bei der Erstellung des Datensatzes angegeben wurde. |
| `value` | Die ID des Datensatzes. |
| `streamingIngestionEnabled` | Ob der Datensatz für die Streaming-Aufnahme aktiviert ist. |
| `createdUser` | Die Benutzer-ID des Benutzers, der den Datensatz erstellt hat. |
| `reportTimestamp` | Der Zeitstempel des Berichts. Wenn während der Anfrage ein `date` angegeben wurde, wird der Bericht für das angegebene Datum zurückgegeben. Wenn kein `date` angegeben wird, wird der neueste Bericht zurückgegeben. |

+++

## Auflisten der Profilverteilung nach Identity-Namespace

Sie können eine GET-Anfrage an den `/previewsamplestatus/report/namespace`-Endpunkt ausführen, um die Aufschlüsselung nach Identity-Namespace für alle zusammengeführten Profile in Ihrem Profilspeicher anzuzeigen. Dazu gehören sowohl die von Adobe bereitgestellten Standardidentitäten als auch die von Ihrem Unternehmen definierten benutzerdefinierten Identitäten.

Identity-Namespaces sind eine wichtige Komponente von Adobe Experience Platform Identity Service, die als Indikatoren für den Kontext dienen, auf den sich Kundendaten beziehen. Um mehr darüber zu erfahren, lesen Sie zunächst den Abschnitt [Übersicht über Identitäts-Namespaces](../../identity-service/features/namespaces.md).

>[!NOTE]
>
>Die Gesamtzahl der Profile nach Namespace (die Summe der für jeden Namespace angezeigten Werte) kann höher sein als die Profilzählungsmetrik, da ein Profil mit mehreren Namespaces verknüpft sein kann. Wenn beispielsweise ein Kunde mit Ihrer Marke auf mehr als einem Kanal interagiert, werden diesem einzelnen Kunden mehrere Namespaces zugeordnet.

**API-Format**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| Abfrageparameter | Beschreibung | Beispiel |
| --------------- | ----------- | ------- |
| `date` | Gibt das Datum des zurückzugebenden Berichts an. Wenn am Datum mehrere Berichte ausgeführt wurden, wird der aktuelle Bericht für dieses Datum zurückgegeben. Wenn für das angegebene Datum kein Bericht vorhanden ist, wird der Fehler 404 (Nicht gefunden) zurückgegeben. Wenn kein Datum angegeben wird, wird der neueste Bericht zurückgegeben. Format: `YYYY-MM-DD`. | `date=2025-6-20` |

**Anfrage**

Die folgende Anfrage gibt keinen `date` an und gibt den neuesten Bericht zurück.

+++ Eine Beispielanfrage, um den letzten Bericht für die Profilverteilung nach Namespace zurückzugeben. 

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 zurück und enthält ein `data`-Array mit einzelnen Objekten, die die Details für jeden Namespace enthalten. Die angezeigte Antwort wurde abgeschnitten, sodass vier Namespaces angezeigt werden.

+++ Eine Beispielantwort enthält Informationen zur Profilverteilung nach Namespace.

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
| -------- | ----------- |
| `sampleCount` | Die Gesamtzahl der abgefragten zusammengeführten Profile im Namespace. |
| `samplePercentage` | Der `sampleCount` als Prozentsatz der abgefragten zusammengeführten Profile (der im `numRowsToRead`letzten Beispielstatus) zurückgegebene [-Wert &#x200B;](#view-last-sample-status) Dezimalformat. |
| `reportTimestamp` | Der Zeitstempel des Berichts. Wenn während der Anfrage ein `date` angegeben wurde, wird der Bericht für das angegebene Datum zurückgegeben. Wenn kein `date` angegeben wird, wird der neueste Bericht zurückgegeben. |
| `fullIDsFragmentCount` | Die Gesamtzahl der Profilfragmente im Namespace. |
| `fullIDsCount` | Die Gesamtzahl der zusammengeführten Profile im Namespace. |
| `fullIDsPercentage` | Der `fullIDsCount` als Prozentsatz der gesamten zusammengeführten Profile (der `totalRows` wie im [letzten Beispielstatus) &#x200B;](#view-last-sample-status) Dezimalformat angegeben. |
| `code` | Die `code` für den Namespace. Dies ist beim Arbeiten mit Namespaces mithilfe der [Adobe Experience Platform Identity Service-API &#x200B;](../../identity-service/api/list-namespaces.md) und wird in der Experience Platform-Benutzeroberfläche auch als [!UICONTROL Identity symbol] bezeichnet. Weitere Informationen finden Sie unter [Übersicht über Identity-Namespaces](../../identity-service/features/namespaces.md). |
| `value` | Der `id` für den Namespace. Dies können Sie beim Arbeiten mit Namespaces mithilfe der [Identity Service-API](../../identity-service/api/list-namespaces.md) feststellen. |

+++

## Auflisten der Datensatzstatistiken {#dataset-stats}

Sie können einen Bericht generieren, der Statistiken zum Datensatz enthält, indem Sie eine GET-Anfrage an den `/previewsamplestatus/report/dataset_stats`-Endpunkt senden.

**API-Format**

```http
GET /previewsamplestatus/report/dataset_stats
```

**Anfrage**

+++ Eine Beispielanfrage zum Generieren des Datensatzstatistikberichts.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset_stats \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status-Code 200 mit Informationen zu den Statistiken des Datensatzes zurück.

+++ Eine Beispielantwort, die Informationen zu den Statistiken des Datensatzes enthält.

>[!NOTE]
>
>Die folgende Antwort wurde gekürzt, um drei Datensätze anzuzeigen.

```json
{
    "data": [
        {
            "120days": 4,
            "14days": 4,
            "30days": 4,
            "365days": 4,
            "60days": 4,
            "7days": 4,
            "90days": 4,
            "datasetId": "{DATASET_ID}",
            "datasetType": "ExperienceEvents",
            "percentEvents": 0.0,
            "percentProfiles": 0.0,
            "profileFragments": 1,
            "records": 4,
            "totalProfiles": 1
        },
        {
            "120days": 155435837,
            "14days": 32888631,
            "30days": 66496282,
            "365days": 155435837,
            "60days": 116433804,
            "7days": 18202004,
            "90days": 155435837,
            "datasetId": "{DATASET_ID}",
            "datasetType": "ExperienceEvents",
            "percentEvents": 16.0,
            "percentProfiles": 0.0,
            "profileFragments": 5410745,
            "records": 155435837,
            "totalProfiles": 4524723
        },
        {
            "120days": 0,
            "14days": 0,
            "30days": 0,
            "365days": 0,
            "60days": 0,
            "7days": 0,
            "90days": 0,
            "datasetId": "{DATASET_ID}",
            "datasetType": "Profiles",
            "percentEvents": 0.0,
            "percentProfiles": 0.0,
            "profileFragments": 3589,
            "records": 3589,
            "totalProfiles": 3589
        }
    ],
    "reportTimestamp": "2025-10-29T16:20:18.956"
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `120days` | Die Anzahl der Datensätze, die nach einem Datenablauf von 120 Tagen im Datensatz verbleiben. |
| `14days` | Die Anzahl der Datensätze, die nach einem Datenablauf von 14 Tagen im Datensatz verbleiben. |
| `30days` | Die Anzahl der Datensätze, die nach einem Datenablauf von 30 Tagen im Datensatz verbleiben. |
| `365days` | Die Anzahl der Datensätze, die nach einem Datenablauf von 365 Tagen im Datensatz verbleiben. |
| `60days` | Die Anzahl der Datensätze, die nach einem Datenablauf von 60 Tagen im Datensatz verbleiben. |
| `7days` | Die Anzahl der Datensätze, die nach einem Datenablauf von 7 Tagen im Datensatz verbleiben. |
| `90days` | Die Anzahl der Datensätze, die nach einem Datenablauf von 90 Tagen im Datensatz verbleiben. |
| `datasetId` | Die ID des Datensatzes. |
| `datasetType` | Der Datensatztyp. Dieser Wert kann entweder `Profiles` oder `ExperienceEvents` sein. |
| `percentEvents` | Der Prozentsatz der Erlebnisereignis-Datensätze, die sich im Datensatz befinden. |
| `percentProfiles` | Der Prozentsatz der Profildatensätze, die sich im Datensatz befinden. |
| `profileFragments` | Die Gesamtzahl der Profilfragmente, die im Datensatz vorhanden sind. |
| `records` | Die Gesamtzahl der in den Datensatz aufgenommenen Profildatensätze. |
| `totalProfiles` | Die Gesamtzahl der in den Datensatz aufgenommenen Profile. |

+++

## Abrufen der Datensatzgröße {#character-count}

Mit diesem Endpunkt können Sie die Größe des Datensatzes in Byte wöchentlich abrufen.

**API-Format**

```http
GET /previewsamplestatus/report/character_count
```

**Anfrage**

+++Eine Beispielanfrage zum Generieren des Berichts zur Zeichenanzahl.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/character_count \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit Informationen zur Größe des Datensatzes im Laufe der Wochen zurückgegeben.

+++ Eine Beispielantwort, die Informationen zur Größe des Datensatzes nach Ablauf der Daten enthält.

>[!NOTE]
>
>Die folgende Antwort wurde gekürzt, um drei Datensätze anzuzeigen.

```json
{
    "data": [
        {
            "datasetIds": [
                {
                    "datasetId": "67aba91a453f7d298cd2a643",
                    "recordType": "keyvalue",
                    "weeks": [
                        {
                            "size": 107773533894,
                            "week": "2025-10-26"
                        }
                    ]
                },
                {
                    "datasetId": "67aa6c867c3110298b017f0e",
                    "recordType": "timeseries",
                    "weeks": [
                        {
                            "size": 242902062440,
                            "week": "2025-10-26"
                        },
                        {
                            "size": 837539413062,
                            "week": "2025-10-19"
                        },
                        {
                            "size": 479253986484,
                            "week": "2025-10-12"
                        },
                        {
                            "size": 358911988990,
                            "week": "2025-10-05"
                        },
                        {
                            "size": 349701073042,
                            "week": "2025-09-28"
                        }
                    ]
                },
                {
                    "datasetId": "680c043667c0d7298c9ea275",
                    "recordType": "keyvalue",
                    "weeks": [
                        {
                            "size": 18392459832,
                            "week": "2025-10-26"
                        }
                    ]
                }
            ],
            "modelName": "_xdm.context.profile",
            "reportTimestamp": "2025-10-30T00:28:30.069Z"
        }
    ],
    "reportTimestamp": "2025-10-30T00:28:30.069Z"
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `datasetId` | Die ID des Datensatzes. |
| `recordType` | Der Datentyp im Datensatz. Der Datensatztyp wirkt sich auf den Wert der `weeks` aus. Zu den unterstützten Werten gehören `keyvalue` und `timeseries`. |
| `weeks` | Ein Array, das die Größeninformationen zum Datensatz enthält. Bei Datensätzen des Datensatztyps `keyvalue` enthält dies die neueste Woche sowie die Gesamtgröße des Datensatzes in Byte. Bei Datensätzen des Datensatztyps `timeseries` enthält dies jede Woche von der Aufnahme des Datensatzes bis zur letzten Woche und die Gesamtgröße des Datensatzes in Byte für jede dieser Wochen. |
| `modelName` | Der Name des Modells für den Datensatz. Mögliche Werte sind `_xdm.context.profile` und `_xdm.context.experienceevent`. |
| `reportTimestamp` | Datum und Uhrzeit der Berichterstellung. |

+++

## Nächste Schritte

Nachdem Sie nun wissen, wie Sie eine Vorschau von Beispieldaten im Profilspeicher anzeigen und mehrere Berichte zu den Daten ausführen, können Sie auch die Endpunkte „Schätzung“ und „Vorschau“ der Segmentierungs-Service-API verwenden, um Informationen auf Zusammenfassungsebene zu Ihren Segmentdefinitionen anzuzeigen. Diese Informationen helfen sicherzustellen, dass Sie Ihre erwartete Zielgruppe isolieren. Weitere Informationen zum Arbeiten mit Vorschauen und Schätzungen mithilfe der Segmentierungs-API finden Sie im [Handbuch zu Vorschau- und Schätzendpunkten](../../segmentation/api/previews-and-estimates.md).

