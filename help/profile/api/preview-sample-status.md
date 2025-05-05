---
keywords: Experience Platform;Profil;Echtzeit-Kundenprofil;Fehlerbehebung;API;Vorschau;Beispiel
title: API-Endpunkt für Musterstatus der Vorschau (Profilvorschau)
description: Der Endpunkt für den Vorschaubeispielstatus der Echtzeit-Kundenprofil-API ermöglicht Ihnen die Vorschau des neuesten erfolgreichen Beispiels Ihrer Profildaten, die Auflistung der Profilverteilung nach Datensatz und Identität und die Erstellung von Berichten mit Datensatzüberschneidungen, Identitätsüberschneidungen und nicht zugeordneten Profilen.
role: Developer
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2909'
ht-degree: 5%

---

# Musterstatus-Endpunkt für Vorschau (Profilvorschau)

Mit Adobe Experience Platform können Sie Kundendaten aus verschiedenen Quellen aufnehmen, um ein robustes, einheitliches Profil für jeden einzelnen Ihrer Kunden zu erstellen. Bei der Aufnahme von Daten in Experience Platform wird ein Beispielvorgang ausgeführt, um die Profilanzahl und andere Metriken zu aktualisieren, die sich auf Echtzeit-Kundenprofildaten beziehen.

Die Ergebnisse dieses Beispielauftrags können mit dem `/previewsamplestatus`-Endpunkt, der Teil der Echtzeit-Kundenprofil-API ist, angezeigt werden. Dieser Endpunkt kann auch verwendet werden, um Profilverteilungen sowohl nach Datensatz als auch nach Identity-Namespace aufzulisten und mehrere Berichte zu generieren, um einen Einblick in die Zusammensetzung des Profilspeichers Ihres Unternehmens zu erhalten. Dieses Handbuch führt Sie durch die Schritte, die zum Anzeigen dieser Metriken mithilfe des `/previewsamplestatus`-API-Endpunkts erforderlich sind.

>[!NOTE]
>
>Als Teil der Segmentierungs-Service-API von Adobe Experience Platform stehen Schätzungs- und Vorschau-Endpunkte zur Verfügung, mit denen Sie Informationen auf Zusammenfassungsebene zu Segmentdefinitionen anzeigen können, um sicherzustellen, dass Sie die erwartete Zielgruppe isolieren. Ausführliche Schritte zum Arbeiten mit Vorschau- und Schätzendpunkten finden Sie im [Handbuch zu Vorschauen und ](../../segmentation/api/previews-and-estimates.md)-Endpunkten, das Teil des [!DNL Segmentation]-API-Entwicklerhandbuchs ist.

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil der [[!DNL Real-Time Customer Profile] API](https://www.adobe.com/go/profile-apis-en). Bevor Sie fortfahren, lesen Sie im Handbuch [Erste Schritte](getting-started.md) die Links zu entsprechenden Dokumentationen, den Leitfaden zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtige Informationen zu Kopfzeilen, die für das erfolgreiche Aufrufen einer [!DNL Experience Platform]-API erforderlich sind.

## Profilfragmente im Vergleich zu zusammengeführten Profilen

Dieses Handbuch verweist sowohl auf „Profilfragmente“ als auch auf „zusammengeführte Profile“. Es ist wichtig, den Unterschied zwischen diesen Begriffen zu verstehen, bevor Sie fortfahren.

Jedes einzelne Kundenprofil besteht aus mehreren Profilfragmenten, die zu einer einzigen Ansicht dieses Kunden zusammengefügt wurden. Wenn ein Kunde beispielsweise über mehrere Kanäle mit Ihrer Marke interagiert, verfügt Ihr Unternehmen wahrscheinlich über mehrere Profilfragmente, die sich auf diesen einzelnen Kunden beziehen und in mehreren Datensätzen enthalten sind.

Wenn Profilfragmente in Experience Platform aufgenommen werden, werden sie zusammengeführt (auf der Grundlage einer Zusammenführungsrichtlinie), um ein einziges Profil für diesen Kunden zu erstellen. Daher ist die Gesamtzahl der Profilfragmente wahrscheinlich immer höher als die Gesamtzahl der zusammengeführten Profile, da jedes Profil aus mehreren Fragmenten besteht.

Um mehr über Profile und ihre Rolle in Experience Platform zu erfahren, lesen Sie zunächst die [Übersicht über das Echtzeit-Kundenprofil](../home.md).

## Wie der Beispielvorgang ausgelöst wird

Wenn Daten, die für das Echtzeit-Kundenprofil aktiviert sind, in [!DNL Experience Platform] aufgenommen werden, werden sie im Profildatenspeicher gespeichert. Wenn die Aufnahme von Datensätzen in den Profilspeicher die Gesamtprofilanzahl um mehr als 5 % erhöht oder verringert, wird ein Sampling-Auftrag ausgelöst, um die Anzahl zu aktualisieren. Die Art und Weise, wie die Stichprobe ausgelöst wird, hängt von der Art der Aufnahme ab, die verwendet wird:

* Bei **Streaming-Daten** Workflows wird stündlich überprüft, ob der Schwellenwert von 5 % für die Erhöhung oder Verringerung erreicht wurde. Ist dies der Fall, wird automatisch ein Beispielvorgang ausgelöst, um die Anzahl zu aktualisieren.
* Bei **Batch-Aufnahme** wird innerhalb von 15 Minuten nach der erfolgreichen Aufnahme eines Batches in den Profilspeicher ein Auftrag ausgeführt, um die Anzahl zu aktualisieren, wenn der Schwellenwert von 5 % für die Erhöhung oder Verringerung erreicht wird. Mit der Profil-API können Sie den neuesten erfolgreichen Beispielvorgang in der Vorschau anzeigen sowie die Profilverteilung nach Datensatz und Identity-Namespace auflisten.

Die Metriken Profilanzahl und Profile nach Namespace sind auch im Abschnitt [!UICONTROL Profile] der Experience Platform-Benutzeroberfläche verfügbar. Informationen zum Zugriff auf Profildaten über die Benutzeroberfläche finden Sie im [[!DNL Profile] UI-Handbuch](../ui/user-guide.md).

## Status der letzten Stichprobe anzeigen {#view-last-sample-status}

Sie können eine GET-Anfrage an den `/previewsamplestatus`-Endpunkt ausführen, um die Details für den letzten erfolgreichen Beispielvorgang anzuzeigen, der für Ihr Unternehmen ausgeführt wurde. Dazu gehören die Gesamtzahl der Profile in der Stichprobe sowie die Metrik zur Profilanzahl oder die Gesamtzahl der Profile, die Ihr Unternehmen in Experience Platform hat.

Die Profilanzahl wird nach dem Zusammenführen von Profilfragmenten generiert, um für jeden einzelnen Kunden ein einziges Profil zu bilden. Mit anderen Worten: Wenn Profilfragmente zusammengeführt werden, geben sie die Anzahl „1“ des Profils zurück, da sie alle mit derselben Person verbunden sind.

Die Profilanzahl umfasst auch Profile mit Attributen (Datensatzdaten) sowie Profile, die nur Zeitreihen-(Ereignis-)Daten enthalten, z. B. Adobe Analytics-Profile. Der Beispielvorgang wird regelmäßig aktualisiert, während Profildaten aufgenommen werden, um eine aktuelle Gesamtzahl von Profilen in Experience Platform bereitzustellen.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Die Antwort enthält die Details für den letzten erfolgreichen Beispielvorgang, der für die Organisation ausgeführt wurde.

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
|---|---|
| `numRowsToRead` | Die Gesamtzahl der zusammengeführten Profile in der Stichprobe. |
| `sampleJobRunning` | Ein boolescher Wert, der `true` zurückgibt, wenn ein Beispielvorgang ausgeführt wird. Bietet Transparenz bezüglich der Latenz, die beim Hochladen einer Batch-Datei auftritt, bis zum Zeitpunkt des tatsächlichen Hinzufügens zur Profilspeicherung. |
| `docCount` | Gesamtanzahl der Dokumente in der Datenbank. |
| `totalFragmentCount` | Gesamtzahl der Profilfragmente im Profilspeicher. |
| `lastSuccessfulBatchTimestamp` | Zeitstempel der letzten erfolgreichen Batch-Aufnahme. |
| `streamingDriven` | *Dieses Feld wird nicht mehr unterstützt und hat keine Bedeutung für die Antwort.* |
| `totalRows` | Gesamtzahl der zusammengeführten Profile in Experience Platform, auch bekannt als „Profilanzahl“. |
| `lastBatchId` | ID der letzten Batch-Aufnahme. |
| `status` | Status der letzten Stichprobe. |
| `samplingRatio` | Verhältnis der abgefragten zusammengeführten Profile (`numRowsToRead`) zu den gesamten zusammengeführten Profilen (`totalRows`), ausgedrückt als Prozentsatz im Dezimalformat. |
| `mergeStrategy` | Im Beispiel verwendete Zusammenführungsstrategie. |
| `lastSampledTimestamp` | Letzter erfolgreicher Beispiel-Zeitstempel. |

## Auflisten der Profilverteilung nach Datensatz

Um die Profilverteilung nach Datensatz anzuzeigen, können Sie eine GET-Anfrage an den `/previewsamplestatus/report/dataset`-Endpunkt ausführen.

**API-Format**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| Parameter | Beschreibung |
|---|---|
| `date` | Geben Sie das Datum des zurückzugebenden Berichts an. Wenn am Datum mehrere Berichte ausgeführt wurden, wird der aktuelle Bericht für dieses Datum zurückgegeben. Wenn für das angegebene Datum kein Bericht vorhanden ist, wird der Fehler 404 (Nicht gefunden) zurückgegeben. Wenn kein Datum angegeben wird, wird der letzte Bericht zurückgegeben. Format: JJJJ-MM-TT. Beispiel: `date=2024-12-31` |

**Anfrage**

Die folgende Anfrage verwendet den `date`-Parameter, um den letzten Bericht für das angegebene Datum zurückzugeben.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Die Antwort enthält ein `data`-Array, das eine Liste der Datensatzobjekte enthält. Die angezeigte Antwort wurde gekürzt, um drei Datensätze anzuzeigen.

>[!NOTE]
>
>Wenn für das Datum mehrere Berichte vorhanden sind, wird nur der neueste Bericht zurückgegeben. Wenn für das angegebene Datum kein Datensatzbericht vorhanden ist, wird der HTTP-Status 404 (Nicht gefunden) zurückgegeben.

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
| `sampleCount` | Die Gesamtzahl der stichprobenweise erfassten zusammengeführten Profile mit dieser Datensatz-ID. |
| `samplePercentage` | Der `sampleCount` als Prozentsatz der Gesamtzahl der abgefragten zusammengeführten Profile (der `numRowsToRead` Wert, wie er im [letzten Beispielstatus) zurückgegeben wurde](#view-last-sample-status) ausgedrückt im Dezimalformat. |
| `fullIDsCount` | Die Gesamtzahl der zusammengeführten Profile mit dieser Datensatz-ID. |
| `fullIDsPercentage` | Der `fullIDsCount` als Prozentsatz der Gesamtzahl der zusammengeführten Profile (der `totalRows`, wie im [letzten Beispielstatus) ](#view-last-sample-status) Dezimalformat zurückgegeben. |
| `name` | Der Name des Datensatzes, wie er bei der Erstellung des Datensatzes angegeben wurde. |
| `description` | Die Beschreibung des Datensatzes, die bei der Erstellung des Datensatzes angegeben wurde. |
| `value` | Die ID des Datensatzes. |
| `streamingIngestionEnabled` | Ob der Datensatz für die Streaming-Aufnahme aktiviert ist. |
| `createdUser` | Die Benutzer-ID des Benutzers, der den Datensatz erstellt hat. |
| `reportTimestamp` | Der Zeitstempel des Berichts. Wenn während der Anfrage ein `date` angegeben wurde, wird der Bericht für das angegebene Datum zurückgegeben. Wenn kein `date` angegeben wird, wird der neueste Bericht zurückgegeben. |

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

| Parameter | Beschreibung |
|---|---|
| `date` | Geben Sie das Datum des zurückzugebenden Berichts an. Wenn am Datum mehrere Berichte ausgeführt wurden, wird der aktuelle Bericht für dieses Datum zurückgegeben. Wenn für das angegebene Datum kein Bericht vorhanden ist, wird der Fehler 404 (Nicht gefunden) zurückgegeben. Wenn kein Datum angegeben wird, wird der neueste Bericht zurückgegeben. Format: JJJJ-MM-TT. Beispiel: `date=2024-12-31` |

**Anfrage**

Die folgende Anfrage gibt keinen `date` an und gibt daher den neuesten Bericht zurück.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Die Antwort enthält ein `data`-Array mit einzelnen Objekten, die die Details für jeden Namespace enthalten. Die angezeigte Antwort wurde abgeschnitten, sodass vier Namespaces angezeigt werden.

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
| `sampleCount` | Die Gesamtzahl der abgefragten zusammengeführten Profile im Namespace. |
| `samplePercentage` | Der `sampleCount` als Prozentsatz der abgefragten zusammengeführten Profile (der im [letzten Beispielstatus) zurückgegebene `numRowsToRead`-Wert ](#view-last-sample-status) Dezimalformat. |
| `reportTimestamp` | Der Zeitstempel des Berichts. Wenn während der Anfrage ein `date` angegeben wurde, wird der Bericht für das angegebene Datum zurückgegeben. Wenn kein `date` angegeben wird, wird der neueste Bericht zurückgegeben. |
| `fullIDsFragmentCount` | Die Gesamtzahl der Profilfragmente im Namespace. |
| `fullIDsCount` | Die Gesamtzahl der zusammengeführten Profile im Namespace. |
| `fullIDsPercentage` | Der `fullIDsCount` als Prozentsatz der gesamten zusammengeführten Profile (der `totalRows` wie im [letzten Beispielstatus) ](#view-last-sample-status) Dezimalformat angegeben. |
| `code` | Die `code` für den Namespace. Dies ist beim Arbeiten mit Namespaces mithilfe der [Adobe Experience Platform Identity Service-](../../identity-service/api/list-namespaces.md) zu finden und wird in der Experience Platform-Benutzeroberfläche auch [!UICONTROL Identitätssymbol] genannt. Weitere Informationen finden Sie unter [Übersicht über Identity-Namespaces](../../identity-service/features/namespaces.md). |
| `value` | Der `id` für den Namespace. Dies können Sie beim Arbeiten mit Namespaces mithilfe der [Identity Service-API](../../identity-service/api/list-namespaces.md) feststellen. |

## Erstellen eines Berichts zur Datensatzüberschneidung

Der Bericht zur Datensatzüberschneidung bietet Einblick in die Zusammensetzung des Profilspeichers Ihres Unternehmens, indem er die Datensätze verfügbar macht, die am meisten zu Ihrer adressierbaren Zielgruppe beitragen (zusammengeführte Profile). Dieser Bericht bietet nicht nur Einblicke in Ihre Daten, sondern kann Ihnen auch bei Maßnahmen zur Optimierung der Lizenznutzung helfen, z. B. beim Festlegen von Ablaufzeiten für bestimmte Datensätze.

Sie können den Bericht zur Datensatzüberschneidung generieren, indem Sie eine GET-Anfrage an den `/previewsamplestatus/report/dataset/overlap`-Endpunkt senden.

Eine schrittweise Anleitung zum Generieren des Berichts zur Datensatzüberschneidung mithilfe der Befehlszeile oder der Postman-Benutzeroberfläche finden Sie im Tutorial [Generieren des Berichts zur Datensatzüberschneidung](../tutorials/dataset-overlap-report.md).

**API-Format**

```http
GET /previewsamplestatus/report/dataset/overlap
GET /previewsamplestatus/report/dataset/overlap?{QUERY_PARAMETERS}
```

| Parameter | Beschreibung |
|---|---|
| `date` | Geben Sie das Datum des zurückzugebenden Berichts an. Wenn mehrere Berichte am selben Datum ausgeführt wurden, wird der neueste Bericht für dieses Datum zurückgegeben. Wenn für das angegebene Datum kein Bericht vorhanden ist, wird der Fehler 404 (Nicht gefunden) zurückgegeben. Wenn kein Datum angegeben wird, wird der letzte Bericht zurückgegeben. Format: JJJJ-MM-TT. Beispiel: `date=2024-12-31` |

**Anfrage**

Die folgende Anfrage verwendet den `date`-Parameter, um den letzten Bericht für das angegebene Datum zurückzugeben.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Antwort**

Bei einer erfolgreichen Anfrage wird der HTTP-Status 200 (OK) und der Bericht zur Datensatzüberschneidung zurückgegeben.

```json
{
    "data": {
        "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
        "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
        "5eeda0032af7bb19162172a7": 107
    },
    "reportTimestamp": "2021-12-29T19:55:31.147"
}
```

| Eigenschaft | Beschreibung |
|---|---|
| `data` | Das `data`-Objekt enthält kommagetrennte Listen von Datensätzen und der jeweiligen Profilanzahl. |
| `reportTimestamp` | Der Zeitstempel des Berichts. Wenn während der Anfrage ein `date` angegeben wurde, wird der Bericht für das angegebene Datum zurückgegeben. Wenn kein `date` angegeben wird, wird der neueste Bericht zurückgegeben. |

### Interpretieren des Berichts zur Datensatzüberschneidung

Die Ergebnisse des Berichts können aus den Datensätzen und der Anzahl der Profile in der Antwort interpretiert werden. Betrachten Sie das folgende Beispiel für ein Report `data`-Objekt:

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

Dieser Bericht enthält die folgenden Informationen:

* Es gibt 123 Profile, die aus Daten aus den folgenden Datensätzen bestehen: `5d92921872831c163452edc8`, `5da7292579975918a851db57`, `5eb2cdc6fa3f9a18a7592a98`.
* Es gibt 454.412 Profile, die aus Daten aus diesen beiden Datensätzen bestehen: `5d92921872831c163452edc8` und `5eb2cdc6fa3f9a18a7592a98`.
* Es gibt 107 Profile, die nur aus Daten aus Datensatz `5eeda0032af7bb19162172a7` bestehen.
* Es gibt insgesamt 454.642 Profile in der Organisation.

## Bericht zur Überschneidung von Identity-Namespaces generieren {#identity-overlap-report}

Der Bericht zur Überschneidung von Identity-Namespaces bietet Einblick in die Zusammensetzung des Profilspeichers Ihres Unternehmens, indem er die Identity-Namespaces verfügbar macht, die am meisten zu Ihrer adressierbaren Zielgruppe beitragen (zusammengeführte Profile). Dazu gehören sowohl die von Adobe bereitgestellten Standard-Identity-Namespaces als auch die von Ihrem Unternehmen definierten benutzerdefinierten Identity-Namespaces.

Sie können den Bericht zur Überschneidung von Identity-Namespaces generieren, indem Sie eine GET-Anfrage an den `/previewsamplestatus/report/namespace/overlap`-Endpunkt senden.

**API-Format**

```http
GET /previewsamplestatus/report/namespace/overlap
GET /previewsamplestatus/report/namespace/overlap?{QUERY_PARAMETERS}
```

| Parameter | Beschreibung |
|---|---|
| `date` | Geben Sie das Datum des zurückzugebenden Berichts an. Wenn mehrere Berichte am selben Datum ausgeführt wurden, wird der neueste Bericht für dieses Datum zurückgegeben. Wenn für das angegebene Datum kein Bericht vorhanden ist, wird der Fehler 404 (Nicht gefunden) zurückgegeben. Wenn kein Datum angegeben wird, wird der letzte Bericht zurückgegeben. Format: JJJJ-MM-TT. Beispiel: `date=2024-12-31` |

**Anfrage**

Die folgende Anfrage verwendet den `date`-Parameter, um den letzten Bericht für das angegebene Datum zurückzugeben.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Antwort**

Bei einer erfolgreichen Anfrage wird der HTTP-Status 200 (OK) und der Bericht zur Überschneidung des Identity-Namespace zurückgegeben.

```json
{
    "data": {
        "Email,crmid,loyal": 2,
        "ECID,Email,crmid": 7,
        "ECID,Email,mobilenr": 12,
        "AAID,ECID,loyal": 1,
        "mobilenr": 25,
        "AAID,ECID": 1508,
        "ECID,crmid": 1,
        "AAID,ECID,crmid": 2,
        "Email,crmid": 328,
        "CORE": 49,
        "AAID": 446,
        "crmid,loyal": 20988,
        "Email": 10904,
        "crmid": 249,
        "ECID,Email": 74,
        "Phone": 40,
        "Email,Phone,loyal": 48,
        "AAID,AVID,ECID": 85,
        "Email,loyal": 1002,
        "AAID,ECID,Email,Phone,crmid": 5,
        "AAID,ECID,Email,crmid,loyal": 23,
        "AAID,AVID,ECID,Email,crmid": 2,
        "AVID": 3,
        "AAID,ECID,Phone": 1,
        "loyal": 43,
        "ECID,Email,crmid,loyal": 6,
        "AAID,ECID,Email,Phone,crmid,loyal": 1,
        "AAID,ECID,Email": 2,
        "AAID,ECID,Email,crmid": 142,
        "AVID,ECID": 24,
        "ECID": 6565
    },
    "reportTimestamp": "2021-12-29T16:55:03.624"
}
```

| Eigenschaft | Beschreibung |
|---|---|
| `data` | Das `data`-Objekt enthält kommagetrennte Listen mit eindeutigen Kombinationen von Identitäts-Namespace-Codes und der jeweiligen Profilanzahl. |
| Namespace-Codes | Die `code` ist eine Kurzform für jeden Identity-Namespace-Namen. Eine Zuordnung jeder `code` zu ihrer `name` finden Sie mithilfe der [Adobe Experience Platform Identity Service-API](../../identity-service/api/list-namespaces.md). Experience Platform Die `code` wird in der Benutzeroberfläche von [!UICONTROL &#x200B; auch als &#x200B;]Identitätssymbol“ bezeichnet. Weitere Informationen finden Sie unter [Übersicht über Identity-Namespaces](../../identity-service/features/namespaces.md). |
| `reportTimestamp` | Der Zeitstempel des Berichts. Wenn während der Anfrage ein `date` angegeben wurde, wird der Bericht für das angegebene Datum zurückgegeben. Wenn kein `date` angegeben wird, wird der neueste Bericht zurückgegeben. |

### Interpretieren des Identity-Namespace-Überschneidungsberichts

Die Ergebnisse des Berichts können anhand der Identitäten und der Profilanzahl in der Antwort interpretiert werden. Der numerische Wert jeder Zeile gibt an, wie viele Profile aus dieser exakten Kombination von standardmäßigen und benutzerdefinierten Identity-Namespaces bestehen.

Siehe folgenden Auszug aus dem `data`:

```json
  "AAID,ECID,Email,crmid": 142,
  "AVID,ECID": 24,
  "ECID": 6565
```

Dieser Bericht enthält die folgenden Informationen:

* Es gibt 142 Profile, die aus `AAID`, `ECID` und `Email` Standardidentitäten sowie aus einem benutzerdefinierten `crmid`-Identity-Namespace bestehen.
* Es gibt 24 Profile, die aus `AAID` und `ECID` Identity-Namespaces bestehen.
* Es gibt 6.565 Profile, die nur eine `ECID` Identität enthalten.

## Bericht zu nicht zugeordneten Profilen erstellen

Weitere Einblicke in die Komposition des Profilspeichers Ihrer Organisation erhalten Sie durch den Bericht Nicht zugeordnete Profile . Ein „nicht zusammengefügtes“ Profil ist ein Profil, das nur ein Profilfragment enthält. Ein „unbekanntes“ Profil ist ein Profil, das mit pseudonymen Identity-Namespaces wie `ECID` und `AAID` verknüpft ist. Unbekannte Profile sind inaktiv, d. h. sie haben für den angegebenen Zeitraum keine neuen Ereignisse hinzugefügt. Der Bericht Nicht zugeordnete Profile enthält eine Aufschlüsselung der Profile für einen Zeitraum von 7, 30, 60, 90 und 120 Tagen.

Sie können den Bericht „Nicht zugeordnete Profile“ generieren, indem Sie eine GET-Anfrage an den `/previewsamplestatus/report/unstitchedProfiles`-Endpunkt senden.

**API-Format**

```http
GET /previewsamplestatus/report/unstitchedProfiles
```

**Anfrage**

Die folgende Anfrage gibt den Bericht „Nicht zugeordnete Profile“ zurück.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/unstitchedProfiles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Antwort**

Bei einer erfolgreichen Anfrage wird der HTTP-Status 200 (OK) sowie der Bericht Unstitched Profiles zurückgegeben.

>[!NOTE]
>
>Für die Zwecke dieses Handbuchs wurde der Bericht gekürzt, sodass er nur `"120days"` und &quot;`7days`&quot; Zeiträume enthält. Der Bericht Vollständige nicht zugeordnete Profile enthält eine Aufschlüsselung der Profile für einen Zeitraum von 7, 30, 60, 90 und 120 Tagen.

```json
{
  "data": {
      "totalNumberOfProfiles": 63606,
      "totalNumberOfEvents": 130977,
      "unstitchedProfiles": {
          "120days": {
              "countOfProfiles": 1644,
              "eventsAssociated": 26824,
              "nsDistribution": {
                  "Email": {
                      "countOfProfiles": 18,
                      "eventsAssociated": 95
                  },
                  "loyal": {
                      "countOfProfiles": 26,
                      "eventsAssociated": 71
                  },
                  "ECID": {
                      "countOfProfiles": 1600,
                      "eventsAssociated": 26658
                  }
              }
          },
          "7days": {
              "countOfProfiles": 1782,
              "eventsAssociated": 29151,
              "nsDistribution": {
                  "Email": {
                      "countOfProfiles": 19,
                      "eventsAssociated": 97
                  },
                  "ECID": {
                      "countOfProfiles": 1734,
                      "eventsAssociated": 28591
                  },
                  "loyal": {
                      "countOfProfiles": 29,
                      "eventsAssociated": 463
                  }
              }
          }
      }
  },
  "reportTimestamp": "2025-08-25T22:14:55.186"
}
```

| Eigenschaft | Beschreibung |
|---|---|
| `data` | Das `data`-Objekt enthält die Informationen, die für den Bericht „Nicht zugeordnete Profile“ zurückgegeben wurden. |
| `totalNumberOfProfiles` | Die Gesamtzahl der eindeutigen Profile im Profilspeicher. Dies entspricht der Anzahl der adressierbaren Zielgruppen. Sie enthält sowohl bekannte als auch nicht zugeordnete Profile. |
| `totalNumberOfEvents` | Die Gesamtzahl der ExperienceEvents im Profilspeicher. |
| `unstitchedProfiles` | Ein Objekt, das eine Aufschlüsselung der nicht zugeordneten Profile nach Zeitraum enthält. Der Bericht Nicht zugeordnete Profile enthält eine Aufschlüsselung der Profile nach Zeiträumen von 7, 30, 60, 90 und 120 Tagen. |
| `countOfProfiles` | Die Anzahl der nicht zugeordneten Profile für den Zeitraum oder die Anzahl der nicht zugeordneten Profile für den Namespace. |
| `eventsAssociated` | Die Anzahl der ExperienceEvents für den Zeitraum oder die Anzahl der Ereignisse für den Namespace. |
| `nsDistribution` | Ein Objekt, das einzelne Identity-Namespaces mit der Verteilung von nicht zugeordneten Profilen und Ereignissen für jeden Namespace enthält. Hinweis: Die Summe der `countOfProfiles` für jeden Identity-Namespace im `nsDistribution` entspricht der `countOfProfiles` für den Zeitraum. Dasselbe gilt für die `eventsAssociated` pro Namespace und die `eventsAssociated` pro Zeitraum. |
| `reportTimestamp` | Der Zeitstempel des Berichts. |

### Interpretieren des Berichts Nicht zugeordnete Profile

Die Ergebnisse des Berichts können insight Aufschluss darüber geben, wie viele nicht zugeordnete und inaktive Profile Ihr Unternehmen in seinem Profilspeicher hat.

Siehe folgenden Auszug aus dem `data`:

```json
  "7days": {
    "countOfProfiles": 1782,
    "eventsAssociated": 29151,
    "nsDistribution": {
      "Email": {
        "countOfProfiles": 19,
        "eventsAssociated": 97
      },
      "ECID": {
        "countOfProfiles": 1734,
        "eventsAssociated": 28591
      },
      "loyal": {
        "countOfProfiles": 29,
        "eventsAssociated": 463
      }
    }
  }
```

Dieser Bericht enthält die folgenden Informationen:

* Es gibt 1.782 Profile, die nur ein Profilfragment enthalten und in den letzten sieben Tagen keine neuen Ereignisse aufweisen.
* Den 1.782 nicht zugeordneten Profilen sind 29.151 ExperienceEvents zugeordnet.
* Es gibt 1.734 nicht zugeordnete Profile, die ein einzelnes Profilfragment aus dem Identity-Namespace der ECID enthalten.
* Den 1.734 nicht zugeordneten Profilen, die ein einzelnes Profilfragment aus dem Identity-Namespace von ECID enthalten, sind 28.591 Ereignisse zugeordnet.

## Nächste Schritte

Nachdem Sie nun wissen, wie Sie eine Vorschau von Beispieldaten im Profilspeicher anzeigen und mehrere Berichte zu den Daten ausführen, können Sie auch die Endpunkte „Schätzung“ und „Vorschau“ der Segmentierungs-Service-API verwenden, um Informationen auf Zusammenfassungsebene zu Ihren Segmentdefinitionen anzuzeigen. Diese Informationen helfen sicherzustellen, dass Sie Ihre erwartete Zielgruppe isolieren. Weitere Informationen zum Arbeiten mit Vorschauen und Schätzungen mithilfe der Segmentierungs-API finden Sie im [Handbuch zu Vorschau- und Schätzendpunkten](../../segmentation/api/previews-and-estimates.md).

