---
keywords: Experience Platform;Profil;Echtzeit-Profil des Kunden;Fehlerbehebung;API;Vorschau;Beispiel
title: Vorschau-Beispielstatus (Profil-Vorschau) API-Endpunkt
description: Mithilfe des Vorschau-Musterstatus-Endpunkts, der Teil der Echtzeit-Customer Profil-API ist, können Sie die neueste erfolgreiche Vorschau Ihrer Profil-Daten sowie die Verteilung der Listen-Profil nach Datensatz und Identitäts-Namensraum innerhalb von Adobe Experience Platform verwenden.
topic: guide
translation-type: tm+mt
source-git-commit: 5266c393b034d1744134522cf1769304f39733da
workflow-type: tm+mt
source-wordcount: '1655'
ht-degree: 4%

---


# Vorschau-Musterstatus-Endpunkt (Profil-Vorschau)

Mit Adobe Experience Platform können Sie Kundendaten aus verschiedenen Quellen erfassen, um stabile einheitliche Profil für einzelne Kunden zu erstellen. Da für Echtzeit-Kundendaten aktivierte Daten in [!DNL Platform] eingehen, werden sie im Profil-Datenspeicher gespeichert.

Wenn die Erfassung von Datensätzen im Profil Store die Gesamtanzahl der Profil um mehr als 5 % erhöht oder verringert, wird ein Stichprobenauftrag ausgelöst, um die Anzahl zu aktualisieren. Wie das Beispiel ausgelöst wird, hängt von der Art der verwendeten Aufnahme ab:

* Für **Streaming-Daten Workflows** wird stündlich geprüft, ob der Schwellenwert für die Erhöhung oder Verringerung um 5 % erreicht wurde. Ist dies der Fall, wird automatisch ein Musterauftrag ausgelöst, um die Anzahl zu aktualisieren.
* Bei **Stapelverarbeitung** wird innerhalb von 15 Minuten nach dem erfolgreichen Einsetzen eines Stapels in den Profil Store ein Auftrag ausgeführt, um die Zählung zu aktualisieren, wenn der Schwellenwert für die Erhöhung oder Verringerung um 5 % erreicht wurde. Mithilfe der Profil-API können Sie den neuesten erfolgreichen Musterauftrag sowie die Verteilung des Liste-Profils nach Datensatz und Identitäts-Namensraum Vorschau werden.

Diese Metriken stehen auch im Bereich [!UICONTROL Profil] der Benutzeroberfläche der Experience Platform zur Verfügung. Informationen zum Zugriff auf Profil-Daten über die Benutzeroberfläche finden Sie im [[!DNL Profile] Benutzerhandbuch](../ui/user-guide.md).

>[!NOTE]
>
>Im Rahmen der Adobe Experience Platform Segmentierungsservice-API stehen Schätzwerte und Vorschauen-Endpunkte zur Verfügung, mit denen Sie zusammenfassende Informationen zu Segmentdefinitionen auf Ansicht erstellen können, um sicherzustellen, dass Sie die erwartete Audience isolieren. Ausführliche Anweisungen zum Arbeiten mit Segmentendpunkten und Schätzendpunkten finden Sie im Handbuch [Vorschauen- und Schätzendpunkte](../../segmentation/api/previews-and-estimates.md), das Teil des [!DNL Segmentation] API-Entwicklerhandbuchs ist.

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil der [[!DNL Real-time Customer Profile] API](https://www.adobe.com/go/profile-apis-en). Bevor Sie fortfahren, lesen Sie bitte im Handbuch [Erste Schritte](getting-started.md) nach Links zu entsprechenden Dokumentationen, einem Leitfaden zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtigen Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen einer [!DNL Experience Platform]-API erforderlich sind.

## Fragmente im Profil im Vergleich zu zusammengeführten Profilen

In diesem Handbuch werden sowohl &quot;Profil-Fragmente&quot;als auch &quot;zusammengeführte Profile&quot;aufgeführt. Es ist wichtig, den Unterschied zwischen diesen Begriffen zu verstehen, bevor Sie fortfahren.

Jedes einzelne Profil besteht aus mehreren Profil-Fragmenten, die zu einer einzigen Ansicht des Kunden zusammengeführt wurden. Wenn ein Kunde beispielsweise über mehrere Kanal mit Ihrer Marke interagiert, enthält Ihr Unternehmen mehrere Profil-Fragmente, die sich auf diesen einzelnen Kunden beziehen und in mehreren Datensätzen angezeigt werden. Wenn diese Fragmente in eine Plattform integriert werden, werden sie (auf der Grundlage der Zusammenführungsrichtlinie) zusammengeführt, um ein einzelnes Profil für diesen Kunden zu erstellen. Daher ist die Gesamtanzahl der Fragmente im Profil wahrscheinlich immer höher als die Gesamtanzahl der zusammengeführten Profile, da jedes Profil aus mehreren Fragmenten besteht.

## Letzter Musterstatus der Ansicht {#view-last-sample-status}

Sie können eine GET an den `/previewsamplestatus`-Endpunkt senden, um die Details für den letzten erfolgreichen Musterauftrag, der für Ihre IMS-Organisation ausgeführt wurde, Ansicht. Dies umfasst die Gesamtzahl der Profil im Beispiel sowie die Metrik zur Anzahl der Profil oder die Gesamtzahl der Profil, die Ihr Unternehmen innerhalb der Experience Platform hat. Die Profil-Anzahl wird nach dem Zusammenführen von Profil-Fragmenten generiert, um für jeden einzelnen Kunden ein Profil zu bilden. Mit anderen Worten: Ihre Organisation hat möglicherweise verschiedene Profilfragmente, die sich auf einen einzelnen Kunden beziehen, der mit Ihrer Marke über unterschiedliche Kanäle interagiert. Diese Fragmente würden jedoch zusammengeführt (gemäß der standardmäßigen Zusammenführungsrichtlinie) und eine Anzahl von „1“ zurückgeben, da sie alle mit derselben Person verbunden sind.

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
>In dieser Beispielantwort sind `numRowsToRead` und `totalRows` gleich. Je nachdem, wie viele Profile Ihr Unternehmen in der Experience Platform hat, kann dies der Fall sein. Im Allgemeinen unterscheiden sich diese beiden Zahlen jedoch, wobei `numRowsToRead` kleiner ist, da es das Beispiel als Untergruppe der Gesamtanzahl der Profil (`totalRows`) darstellt.

```json
{
  "numRowsToRead": "41003",
  "sampleJobRunning": {
    "status": true,
    "submissionTimestamp": "2020-08-01 17:57:57.0"
  },
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
| `sampleJobRunning` | Ein boolescher Wert, der `true` zurückgibt, wenn ein Musterauftrag ausgeführt wird. Bietet Transparenz in Bezug auf die Latenz, die entsteht, wenn eine Stapelverarbeitungsdatei in den Profil-Store hochgeladen wird. |
| `cosmosDocCount` | Gesamtanzahl der Dokumente in Kosmos. |
| `totalFragmentCount` | Gesamtanzahl der Profil-Fragmente im Profil Store. |
| `lastSuccessfulBatchTimestamp` | Letzter erfolgreicher Zeitstempel für die Stapelverarbeitung. |
| `streamingDriven` | *Dieses Feld ist veraltet und enthält keine Bedeutung für die Antwort.* |
| `totalRows` | Gesamtzahl der zusammengeführten Profile in Experience Platform, auch als &quot;Profil-Zähler&quot;bezeichnet. |
| `lastBatchId` | Letzte Batch-Erfassungskennung. |
| `status` | Status des letzten Beispiels. |
| `samplingRatio` | Verhältnis der gesampelten zusammengeführten Profil (`numRowsToRead`) zu den zusammengeführten Profilen insgesamt (`totalRows`), ausgedrückt als Prozentwert im Dezimalformat. |
| `mergeStrategy` | In der Stichprobe verwendete Merge-Strategie. |
| `lastSampledTimestamp` | Letzter erfolgreicher Beispiel-Zeitstempel. |

## Verteilung von Liste-Profil nach Datensatz

Um die Verteilung der Profil nach Datensatz anzuzeigen, können Sie eine GET an den `/previewsamplestatus/report/dataset`-Endpunkt anfordern.

**API-Format**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| Parameter | Beschreibung |
|---|---|
| `date` | Geben Sie das Datum des zurückzugebenden Berichts an. Wenn am Datum mehrere Berichte ausgeführt wurden, wird der letzte Bericht für dieses Datum zurückgegeben. Wenn für das angegebene Datum kein Bericht vorhanden ist, wird der Fehler &quot;404&quot;zurückgegeben. Wenn kein Datum angegeben ist, wird der letzte Bericht zurückgegeben. Format: JJJJ-MM-TT. Beispiel: `date=2024-12-31` |

**Anfrage**

Die folgende Anforderung verwendet den Parameter `date`, um den letzten Bericht für das angegebene Datum zurückzugeben.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Die Antwort enthält ein `data`-Array, das eine Liste von DataSet-Objekten enthält. Die angezeigte Antwort wurde abgeschnitten und zeigt drei Datensätze an.

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
| `samplePercentage` | Der Wert `sampleCount` als Prozentsatz der Gesamtzahl der zusammengeführten Profil mit Stichprobe (der Wert `numRowsToRead`, wie im [letzten Musterstatus](#view-last-sample-status) zurückgegeben), ausgedrückt als Dezimalformat. |
| `fullIDsCount` | Die Gesamtanzahl der zusammengeführten Profil mit dieser DataSet-ID. |
| `fullIDsPercentage` | Der Wert `fullIDsCount` als Prozentsatz der Gesamtanzahl der zusammengeführten Profil (der Wert `totalRows`, der im [letzten Musterstatus](#view-last-sample-status) zurückgegeben wird), ausgedrückt als Dezimalformat. |
| `name` | Der Name des Datensatzes, wie er bei der Erstellung des Datensatzes angegeben wird. |
| `description` | Die Beschreibung des Datensatzes, wie bei der Erstellung des Datensatzes angegeben. |
| `value` | Die ID des Datensatzes. |
| `streamingIngestionEnabled` | Ob der Datensatz für die Streaming-Erfassung aktiviert ist. |
| `createdUser` | Die Benutzer-ID des Benutzers, der den Datensatz erstellt hat. |
| `reportTimestamp` | Der Zeitstempel des Berichts. Wenn während der Anforderung ein Parameter `date` angegeben wurde, gilt der zurückgegebene Bericht für das angegebene Datum. Wenn kein Parameter `date` angegeben ist, wird der letzte Bericht zurückgegeben. |

## Verteilung von Liste-Profil nach Namensraum

Sie können eine GET an den `/previewsamplestatus/report/namespace`-Endpunkt ausführen, um die Aufschlüsselung nach Identitäts-Namensraum für alle zusammengeführten Profil in Ihrem Profil-Store Ansicht. Identity Namensräume sind eine wichtige Komponente des Adobe Experience Platform Identity Service, die als Indikatoren für den Kontext dient, auf den sich Kundendaten beziehen. Weitere Informationen finden Sie unter [Übersicht über den Identitäts-Namensraum](../../identity-service/namespaces.md).

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
| `date` | Geben Sie das Datum des zurückzugebenden Berichts an. Wenn am Datum mehrere Berichte ausgeführt wurden, wird der letzte Bericht für dieses Datum zurückgegeben. Wenn für das angegebene Datum kein Bericht vorhanden ist, wird der Fehler &quot;404&quot;zurückgegeben. Wenn kein Datum angegeben ist, wird der letzte Bericht zurückgegeben. Format: JJJJ-MM-TT. Beispiel: `date=2024-12-31` |

**Anfrage**

Die folgende Anforderung gibt keinen Parameter `date` an und gibt daher den letzten Bericht zurück.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Die Antwort enthält ein Array mit den einzelnen Objekten, die die Details für jeden Namensraum enthalten. `data` Die angezeigte Antwort wurde abgeschnitten und zeigt nun vier Namensräume an.

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
| `sampleCount` | Die Gesamtzahl der zusammengeführten Profil mit Stichproben im Namensraum. |
| `samplePercentage` | Der Wert `sampleCount` als Prozentwert der zusammengeführten Profil mit Stichprobe (der `numRowsToRead`-Wert, wie im [Letzter Musterstatus](#view-last-sample-status) zurückgegeben), ausgedrückt als Dezimalformat. |
| `reportTimestamp` | Der Zeitstempel des Berichts. Wenn während der Anforderung ein Parameter `date` angegeben wurde, gilt der zurückgegebene Bericht für das angegebene Datum. Wenn kein Parameter `date` angegeben ist, wird der letzte Bericht zurückgegeben. |
| `fullIDsFragmentCount` | Die Gesamtanzahl der Profil-Fragmente im Namensraum. |
| `fullIDsCount` | Die Gesamtzahl der zusammengeführten Profil im Namensraum. |
| `fullIDsPercentage` | Der Wert `fullIDsCount` als Prozentsatz des gesamten zusammengeführten Profils (der `totalRows`-Wert, wie im [Letzter Musterstatus](#view-last-sample-status) zurückgegeben), ausgedrückt als Dezimalformat. |
| `code` | Das `code` für den Namensraum. Dies kann bei der Arbeit mit Namensräumen mit der [Adobe Experience Platform Identity Service API](../../identity-service/api/list-namespaces.md) gefunden werden und wird auch als [!UICONTROL Identitätssymbol] in der Benutzeroberfläche der Experience Platform bezeichnet. Weitere Informationen finden Sie unter [Übersicht über den Identitäts-Namensraum](../../identity-service/namespaces.md). |
| `value` | Der `id`-Wert für den Namensraum. Dies kann bei der Arbeit mit Namensräumen mit der [Identitätsdienst-API](../../identity-service/api/list-namespaces.md) gefunden werden. |

## Nächste Schritte

Nachdem Sie nun wissen, wie Sie Musterdaten im Profil Store Vorschau können, können Sie auch die Vorschauen- und Schätzwerte der Segmentierungsdienst-API verwenden, um Informationen auf Zusammenfassungsebene zu Ihren Segmentdefinitionen Ansicht. Anhand dieser Informationen können Sie sicherstellen, dass Sie die erwartete Audience in Ihrem Segment isolieren. Weitere Informationen zum Arbeiten mit Segmentdaten und -schätzungen mithilfe der Segmentierungs-API finden Sie im Handbuch [Vorschau und Schätzung von Endpunkten](../../segmentation/api/previews-and-estimates.md).