---
keywords: Experience Platform;Profil;Echtzeit-Profil des Kunden;Fehlerbehebung;API;Vorschau;Beispiel
title: Vorschau-Beispielstatus (Profil-Vorschau) API-Endpunkt
description: Mithilfe des Statusendpunkts für die Vorschau, der Teil der Echtzeit-Customer Profil-API ist, können Sie die neueste erfolgreiche Stichprobe Ihrer Profil-Daten, die Verteilung der Liste-Profile nach Datensatz und Identität, und einen Bericht zur Datenüberschneidung erstellen.
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
source-git-commit: 459eb626101b7382b8fe497835cc19f7d7adc6b2
workflow-type: tm+mt
source-wordcount: '2066'
ht-degree: 1%

---

# Vorschau-Musterstatus-Endpunkt (Profil-Vorschau)

Mit Adobe Experience Platform können Sie Kundendaten aus mehreren Quellen erfassen, um ein robustes, einheitliches Profil für jeden Ihrer Kunden zu erstellen. Da Daten in Plattform erfasst werden, wird ein Musterauftrag ausgeführt, um die Profil- und andere Metriken im Zusammenhang mit Profilen zu aktualisieren.

Die Ergebnisse dieses Musterauftrags können mit dem `/previewsamplestatus`-Endpunkt der Echtzeit-Client-Profil-API angezeigt werden. Dieser Endpunkt kann auch verwendet werden, um Profil-Distributionen sowohl durch DataSet- als auch durch Identitäts-Namensraum Liste, sowie um einen Bericht zur Dataset-Überschneidung zu generieren, um die Zusammensetzung des Profil-Speichers Ihres Unternehmens besser sichtbar zu machen. Dieser Leitfaden führt die Schritte durch, die zur Ansicht dieser Metriken mithilfe des API-Endpunkts `/previewsamplestatus` erforderlich sind.

>[!NOTE]
>
>Im Rahmen der Adobe Experience Platform Segmentierungsservice-API stehen Schätzwerte und Vorschauen-Endpunkte zur Verfügung, mit denen Sie zusammenfassende Informationen zu Segmentdefinitionen auf Ansicht erstellen können, um sicherzustellen, dass Sie die erwartete Audience isolieren. Ausführliche Anweisungen zum Arbeiten mit Segmentendpunkten und Schätzendpunkten finden Sie im Handbuch [Vorschauen- und Schätzendpunkte](../../segmentation/api/previews-and-estimates.md), das Teil des [!DNL Segmentation] API-Entwicklerhandbuchs ist.

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil der [[!DNL Real-time Customer Profile] API](https://www.adobe.com/go/profile-apis-en). Bevor Sie fortfahren, lesen Sie bitte im Handbuch [Erste Schritte](getting-started.md) nach Links zu entsprechenden Dokumentationen, einem Leitfaden zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtigen Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen einer [!DNL Experience Platform]-API erforderlich sind.

## Fragmente im Profil im Vergleich zu zusammengeführten Profilen

In diesem Handbuch werden sowohl &quot;Profil-Fragmente&quot;als auch &quot;zusammengeführte Profile&quot;aufgeführt. Es ist wichtig, den Unterschied zwischen diesen Begriffen zu verstehen, bevor Sie fortfahren.

Jedes einzelne Profil besteht aus mehreren Profil-Fragmenten, die zu einer einzigen Ansicht des Kunden zusammengeführt wurden. Wenn ein Kunde beispielsweise über mehrere Kanal mit Ihrer Marke interagiert, weist Ihr Unternehmen wahrscheinlich mehrere Profil-Fragmente auf, die sich auf diesen einzelnen Kunden beziehen und in mehreren Datensätzen angezeigt werden.

Wenn Profil-Fragmente in eine Plattform integriert werden, werden sie (auf der Grundlage einer Zusammenführungsrichtlinie) zusammengeführt, um ein einziges Profil für diesen Kunden zu erstellen. Daher ist die Gesamtanzahl der Fragmente im Profil wahrscheinlich immer höher als die Gesamtanzahl der zusammengeführten Profile, da jedes Profil aus mehreren Fragmenten besteht.

Um mehr über Profil und deren Rolle innerhalb der Experience Platform zu erfahren, lesen Sie zunächst den [Überblick über das Echtzeit-Profil des Kunden](../home.md).

## Auslösen des Musterauftrags

Da Daten, die für Echtzeit-Kundendaten aktiviert wurden, in [!DNL Platform] eingehen, werden sie im Profil-Datenspeicher gespeichert. Wenn die Erfassung von Datensätzen im Profil Store die Gesamtanzahl der Profil um mehr als 5 % erhöht oder verringert, wird ein Stichprobenauftrag ausgelöst, um die Anzahl zu aktualisieren. Wie das Beispiel ausgelöst wird, hängt von der Art der verwendeten Aufnahme ab:

* Für **Streaming-Daten Workflows** wird stündlich geprüft, ob der Schwellenwert für die Erhöhung oder Verringerung um 5 % erreicht wurde. Ist dies der Fall, wird automatisch ein Musterauftrag ausgelöst, um die Anzahl zu aktualisieren.
* Bei **Stapelverarbeitung** wird innerhalb von 15 Minuten nach dem erfolgreichen Einsetzen eines Stapels in den Profil Store ein Auftrag ausgeführt, um die Zählung zu aktualisieren, wenn der Schwellenwert für die Erhöhung oder Verringerung um 5 % erreicht wurde. Mithilfe der Profil-API können Sie den neuesten erfolgreichen Musterauftrag sowie die Verteilung des Liste-Profils nach Datensatz und Identitäts-Namensraum Vorschau werden.

Die Metriken für die Anzahl der Profil und die Profil nach Namensraum stehen auch im Bereich [!UICONTROL Profil] der Benutzeroberfläche der Experience Platform zur Verfügung. Weitere Informationen zum Zugriff auf Profil-Daten über die Benutzeroberfläche finden Sie im Handbuch [[!DNL Profile] UI](../ui/user-guide.md).

## Letzter Musterstatus der Ansicht {#view-last-sample-status}

Sie können eine GET an den `/previewsamplestatus`-Endpunkt senden, um die Details für den letzten erfolgreichen Musterauftrag, der für Ihre IMS-Organisation ausgeführt wurde, Ansicht. Dies umfasst die Gesamtzahl der Profil im Beispiel sowie die Metrik zur Anzahl der Profil oder die Gesamtzahl der Profil, die Ihr Unternehmen innerhalb der Experience Platform hat.

Die Profil-Anzahl wird nach dem Zusammenführen von Profil-Fragmenten generiert, um für jeden einzelnen Kunden ein Profil zu bilden. Wenn also Profil-Fragmente zusammengeführt werden, wird das Profil &quot;1&quot;zurückgegeben, da sie alle mit derselben Person zusammenhängen.

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

Die Antwort enthält die Details zum letzten erfolgreichen Musterauftrag, der für das Unternehmen ausgeführt wurde.

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
>Wenn mehrere Berichte für das Datum vorhanden sind, wird nur der letzte Bericht zurückgegeben. Wenn für das angegebene Datum kein Datensatzbericht vorhanden ist, wird HTTP-Status 404 (Nicht gefunden) zurückgegeben.

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

Sie können eine GET an den `/previewsamplestatus/report/namespace`-Endpunkt ausführen, um die Aufschlüsselung nach Identitäts-Namensraum für alle zusammengeführten Profil in Ihrem Profil-Store Ansicht.

Identity Namensräume sind eine wichtige Komponente des Adobe Experience Platform Identity Service, die als Indikatoren für den Kontext dient, auf den sich Kundendaten beziehen. Um mehr zu erfahren, lesen Sie zunächst den [Übersicht über den Identitäts-Namensraum](../../identity-service/namespaces.md).

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

## Bericht zur Datenüberschneidung erstellen

Der Bericht zur Datenüberschneidung bietet einen Einblick in die Zusammensetzung des Profil-Stores Ihres Unternehmens, indem er die Datensätze offen legt, die am meisten zu Ihrer adressierbaren Audience (Profilen) beitragen. Dieser Bericht bietet Ihnen nicht nur Einblicke in Ihre Daten, sondern kann Ihnen auch bei der Optimierung der Lizenznutzung helfen, z. B. beim Festlegen einer TTL für bestimmte Datensätze.

Sie können den Bericht zur Datenüberschneidung erstellen, indem Sie eine GET an den Endpunkt `/previewsamplestatus/report/dataset/overlap` anfordern.

Eine schrittweise Anleitung zum Generieren des Berichts zur Datenüberschneidung mithilfe der Befehlszeile oder der Postman-Benutzeroberfläche finden Sie im Lehrgang [Generieren des Berichts zur Datenüberschneidung](../tutorials/dataset-overlap-report.md).

**API-Format**

```http
GET /previewsamplestatus/report/dataset/overlap
GET /previewsamplestatus/report/dataset/overlap?{QUERY_PARAMETERS}
```

| Parameter | Beschreibung |
|---|---|
| `date` | Geben Sie das Datum des zurückzugebenden Berichts an. Wenn mehrere Berichte am selben Datum ausgeführt wurden, wird der letzte Bericht für dieses Datum zurückgegeben. Wenn für das angegebene Datum kein Bericht vorhanden ist, wird der Fehler 404 (Nicht gefunden) zurückgegeben. Wenn kein Datum angegeben ist, wird der letzte Bericht zurückgegeben. Format: JJJJ-MM-TT. Beispiel: `date=2024-12-31` |

**Anfrage**

Die folgende Anforderung verwendet den Parameter `date`, um den letzten Bericht für das angegebene Datum zurückzugeben.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Antwort**

Bei einer erfolgreichen Anforderung werden HTTP-Status 200 (OK) und der Bericht zur Datenüberschneidung zurückgegeben.

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
| `data` | Das `data`-Objekt enthält kommagetrennte Listen von Datensätzen und deren jeweilige Profil-Anzahl. |
| `reportTimestamp` | Der Zeitstempel des Berichts. Wenn während der Anforderung ein Parameter `date` angegeben wurde, gilt der zurückgegebene Bericht für das angegebene Datum. Wenn kein Parameter `date` angegeben ist, wird der letzte Bericht zurückgegeben. |

Die Ergebnisse des Berichts können aus den Datensätzen und Profilen in der Antwort interpretiert werden. Betrachten Sie das folgende Beispielobjekt `data`:

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

Dieser Bericht enthält die folgenden Informationen:
* Es gibt 123 Profile aus Daten aus den folgenden Datensätzen: `5d92921872831c163452edc8`, `5da7292579975918a851db57`, `5eb2cdc6fa3f9a18a7592a98`.
* Es gibt 454.412 Profile, die aus Daten aus diesen beiden Datensätzen bestehen: `5d92921872831c163452edc8` und `5eb2cdc6fa3f9a18a7592a98`.
* Es gibt 107 Profil, die nur aus Daten aus dem Datensatz `5eeda0032af7bb19162172a7` bestehen.
* Die Einrichtung hat insgesamt 454 642 Profile.

## Nächste Schritte

Nachdem Sie nun wissen, wie Sie Musterdaten im Segmentspeicher Vorschau und Ausführung des Datenüberschneidungsberichts ausführen, können Sie auch die Vorschauen- und Schätzwerte der Segmentierungsdienst-API verwenden, um Informationen zu Segmentdefinitionen auf der Ebene der Ansicht zu erhalten. Anhand dieser Informationen können Sie sicherstellen, dass Sie die erwartete Audience in Ihrem Segment isolieren. Weitere Informationen zum Arbeiten mit Segmentdaten und -schätzungen mithilfe der Segmentierungs-API finden Sie im Handbuch [Vorschau und Schätzung von Endpunkten](../../segmentation/api/previews-and-estimates.md).

