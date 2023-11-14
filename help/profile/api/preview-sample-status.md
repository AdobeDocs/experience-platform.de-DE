---
keywords: Experience Platform; Profil; Echtzeit-Kundenprofil; Fehlerbehebung; API; Vorschau; Beispiel
title: API-Endpunkt "Vorschaustatus"(Profilvorschau)
description: Mit dem Beispielstatusendpunkt "Vorschau"der Echtzeit-Kundenprofil-API können Sie eine Vorschau des neuesten erfolgreichen Beispiels Ihrer Profildaten anzeigen, die Profilverteilung nach Datensatz und Identität auflisten und Berichte mit Datensatzüberschneidungen, Identitätsüberschneidungen und nicht zugewiesenen Profilen erstellen.
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
source-git-commit: 8ae18565937adca3596d8663f9c9e6d84b0ce95a
workflow-type: tm+mt
source-wordcount: '2868'
ht-degree: 5%

---

# Anzeigen einer Vorschau des Beispielstatus-Endpunkts (Profilvorschau)

Mit Adobe Experience Platform können Sie Kundendaten aus verschiedenen Quellen erfassen, um ein robustes, einheitliches Profil für jeden Ihrer Kunden zu erstellen. Da Daten in Platform erfasst werden, wird ein Beispielauftrag ausgeführt, um die Profilanzahl und andere datenbezogene Metriken des Echtzeit-Kundenprofils zu aktualisieren.

Die Ergebnisse dieses Beispielauftrags können mit dem `/previewsamplestatus` -Endpunkt, Teil der Echtzeit-Kundenprofil-API. Dieser Endpunkt kann auch verwendet werden, um Profilverteilungen nach Datensatz und Identitäts-Namespace aufzulisten und mehrere Berichte zu generieren, um Einblicke in die Zusammensetzung des Profilspeichers Ihres Unternehmens zu erhalten. In diesem Handbuch werden die Schritte erläutert, die zur Ansicht dieser Metriken mithilfe der Variablen `/previewsamplestatus` API-Endpunkt.

>[!NOTE]
>
>Es gibt Schätzungs- und Vorschau-Endpunkte, die als Teil der Adobe Experience Platform Segmentation Service-API verfügbar sind und mit denen Sie Informationen auf Zusammenfassungsebene zu Segmentdefinitionen anzeigen können, um sicherzustellen, dass Sie die erwartete Zielgruppe isolieren. Detaillierte Schritte zum Arbeiten mit Vorschau- und Schätzendpunkten finden Sie im Abschnitt [Handbuch zu Vorschau- und Schätzendpunkten](../../segmentation/api/previews-and-estimates.md), Teil der [!DNL Segmentation] API-Entwicklerhandbuch.

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil der [[!DNL Real-Time Customer Profile] API](https://www.adobe.com/go/profile-apis-en). Bevor Sie fortfahren, lesen Sie im Handbuch [Erste Schritte](getting-started.md) die Links zu entsprechenden Dokumentationen, den Leitfaden zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtige Informationen zu Kopfzeilen, die für das erfolgreiche Aufrufen einer [!DNL Experience Platform]-API erforderlich sind.

## Profilfragmente im Vergleich zu zusammengeführten Profilen

Dieses Handbuch verweist sowohl auf &quot;Profilfragmente&quot;als auch auf &quot;zusammengeführte Profile&quot;. Bevor Sie fortfahren, müssen Sie die Unterschiede zwischen diesen Begriffen verstehen.

Jedes einzelne Kundenprofil besteht aus mehreren Profilfragmenten, die zu einer einzigen Ansicht dieses Kunden zusammengefügt wurden. Wenn beispielsweise ein Kunde über mehrere Kanäle mit Ihrer Marke interagiert, weist Ihr Unternehmen wahrscheinlich mehrere Profilfragmente auf, die sich auf diesen einzelnen Kunden beziehen und in mehreren Datensätzen angezeigt werden.

Wenn Profilfragmente in Platform erfasst werden, werden sie zusammengeführt (basierend auf einer Zusammenführungsrichtlinie), um ein einzelnes Profil für diesen Kunden zu erstellen. Daher ist die Gesamtanzahl der Profilfragmente wahrscheinlich immer höher als die Gesamtanzahl der zusammengeführten Profile, da jedes Profil aus mehreren Fragmenten besteht.

Um mehr über Profile und ihre Rolle innerhalb von Experience Platform zu erfahren, lesen Sie zunächst das [Übersicht über das Echtzeit-Kundenprofil](../home.md).

## Auslösen des Beispielauftrags

Da Daten, die für das Echtzeit-Kundenprofil aktiviert sind, in erfasst werden [!DNL Platform], wird sie im Profildatenspeicher gespeichert. Wenn die Aufnahme von Datensätzen in den Profilspeicher die Gesamtzahl der Profile um mehr als 5 % erhöht oder verringert, wird ein Sampling-Auftrag ausgelöst, um die Anzahl zu aktualisieren. Die Art und Weise, wie das Beispiel ausgelöst wird, hängt vom verwendeten Erfassungstyp ab:

* Für **Streaming-Daten-Workflows** wird stündlich überprüft, ob der Schwellenwert für eine Zu- oder Abnahme um 5 % erreicht wurde. Ist dies der Fall, wird automatisch ein Beispielauftrag ausgelöst, um die Anzahl zu aktualisieren.
* Für **Batch-Erfassung** innerhalb von 15 Minuten nach erfolgreicher Aufnahme eines Batches in den Profilspeicher wird ein Auftrag ausgeführt, um die Anzahl zu aktualisieren, wenn der Schwellenwert für die Erhöhung oder Verringerung um 5 % erreicht ist. Mithilfe der Profil-API können Sie eine Vorschau des neuesten erfolgreichen Beispielauftrags anzeigen sowie die Profilverteilung nach Datensatz und Identitäts-Namespace auflisten.

Die Profilanzahl und die Profile nach Namespace-Metriken sind auch in der Variablen [!UICONTROL Profile] -Abschnitt der Experience Platform-Benutzeroberfläche. Informationen zum Zugriff auf Profildaten über die Benutzeroberfläche finden Sie unter [[!DNL Profile] UI-Handbuch](../ui/user-guide.md).

## Letzten Beispielstatus anzeigen {#view-last-sample-status}

Sie können eine GET-Anfrage an die `/previewsamplestatus` -Endpunkt, um die Details für den letzten erfolgreichen Beispielauftrag anzuzeigen, der für Ihr Unternehmen ausgeführt wurde. Dazu gehören die Gesamtzahl der Profile im Beispiel sowie die Profilzählung oder die Gesamtanzahl der Profile, die Ihr Unternehmen im Rahmen von Experience Platform hat.

Die Profilanzahl wird nach dem Zusammenführen von Profilfragmenten generiert, um für jeden einzelnen Kunden ein einzelnes Profil zu erstellen. Mit anderen Worten: Wenn Profilfragmente zusammengeführt werden, geben sie die Anzahl der Profile &quot;1&quot;zurück, da sie alle mit derselben Person verbunden sind.

Die Profilanzahl umfasst auch Profile mit Attributen (Datensatzdaten) sowie Profile, die nur Zeitreihendaten (Ereignisdaten) enthalten, z. B. Adobe Analytics-Profile. Der Beispielauftrag wird regelmäßig aktualisiert, wenn Profildaten erfasst werden, um eine aktuelle Gesamtanzahl von Profilen in Platform bereitzustellen.

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

Die Antwort enthält die Details zum letzten erfolgreichen Beispielauftrag, der für das Unternehmen ausgeführt wurde.

>[!NOTE]
>
>In dieser Beispielantwort `numRowsToRead` und `totalRows` sind gleich einander. Abhängig von der Anzahl der Profile, die Ihr Unternehmen im Experience Platform hat, kann dies der Fall sein. Im Allgemeinen unterscheiden sich diese beiden Zahlen jedoch, wobei `numRowsToRead` ist die kleinere Zahl, da sie die Stichprobe als Teilmenge der Gesamtzahl der Profile darstellt (`totalRows`).

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
| `numRowsToRead` | Die Gesamtzahl der zusammengeführten Profile in der Stichprobe. |
| `sampleJobRunning` | Ein boolescher Wert, der `true` wenn ein Beispielauftrag ausgeführt wird. Bietet Transparenz in Bezug auf die Latenz, die auftritt, wenn eine Batch-Datei in hochgeladen wird, wenn sie tatsächlich zum Profilspeicher hinzugefügt wird. |
| `cosmosDocCount` | Gesamtanzahl der Dokumente in Cosmos. |
| `totalFragmentCount` | Gesamtzahl der Profilfragmente im Profilspeicher. |
| `lastSuccessfulBatchTimestamp` | Letzter erfolgreicher Zeitstempel der Batch-Erfassung. |
| `streamingDriven` | *Dieses Feld ist veraltet und enthält keine Bedeutung für die Antwort.* |
| `totalRows` | Gesamtzahl der zusammengeführten Profile in Experience Platform, auch als &quot;Profilanzahl&quot;bezeichnet. |
| `lastBatchId` | Letzte Batch-Aufnahme-ID. |
| `status` | Status des letzten Beispiels. |
| `samplingRatio` | Verhältnis der gesampelten zusammengeführten Profile (`numRowsToRead`) auf die Gesamtzahl der zusammengeführten Profile (`totalRows`), ausgedrückt als Prozentsatz im Dezimalformat. |
| `mergeStrategy` | In der Stichprobe verwendete Zusammenführungsstrategie. |
| `lastSampledTimestamp` | Letzter erfolgreicher Beispiel-Zeitstempel. |

## Profilverteilung nach Datensatz auflisten

Um die Verteilung der Profile nach Datensatz anzuzeigen, können Sie eine GET-Anfrage an die `/previewsamplestatus/report/dataset` -Endpunkt.

**API-Format**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| Parameter | Beschreibung |
|---|---|
| `date` | Geben Sie das Datum des zurückzugebenden Berichts an. Wenn am Datum mehrere Berichte ausgeführt wurden, wird der neueste Bericht für dieses Datum zurückgegeben. Wenn für das angegebene Datum kein Bericht vorhanden ist, wird der Fehler 404 (Nicht gefunden) zurückgegeben. Wenn kein Datum angegeben ist, wird der neueste Bericht zurückgegeben. Format: JJJJ-MM-TT. Beispiel: `date=2024-12-31` |

**Anfrage**

Die folgende Anfrage verwendet die `date` -Parameter, um den neuesten Bericht für das angegebene Datum zurückzugeben.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Die Antwort enthält eine `data` -Array, das eine Liste von Datensatzobjekten enthält. Die angezeigte Antwort wurde gekürzt, um drei Datensätze anzuzeigen.

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
| `sampleCount` | Die Gesamtzahl der gesampelten zusammengeführten Profile mit dieser Datensatz-ID. |
| `samplePercentage` | Die `sampleCount` als Prozentsatz der Gesamtzahl der gesampelten zusammengeführten Profile (die `numRowsToRead` -Wert, der im [Letzter Beispielstatus](#view-last-sample-status)), ausgedrückt in Dezimalformat. |
| `fullIDsCount` | Die Gesamtzahl der zusammengeführten Profile mit dieser Datensatz-ID. |
| `fullIDsPercentage` | Die `fullIDsCount` als Prozentsatz der Gesamtzahl der zusammengeführten Profile (die `totalRows` -Wert, der im [Letzter Beispielstatus](#view-last-sample-status)), ausgedrückt in Dezimalformat. |
| `name` | Der Name des Datensatzes, wie er bei der Erstellung des Datensatzes angegeben wurde. |
| `description` | Die Beschreibung des Datensatzes, wie bei der Erstellung des Datensatzes angegeben. |
| `value` | Die Kennung des Datensatzes. |
| `streamingIngestionEnabled` | Gibt an, ob der Datensatz für die Streaming-Erfassung aktiviert ist. |
| `createdUser` | Die Benutzer-ID des Benutzers, der den Datensatz erstellt hat. |
| `reportTimestamp` | Der Zeitstempel des Berichts. Wenn eine `date` während der Anfrage angegeben wurde, wird der zurückgegebene Bericht für das angegebene Datum angezeigt. Wenn nicht `date` angegeben wird, wird der neueste Bericht zurückgegeben. |

## Profilverteilung nach Identitäts-Namespace auflisten

Sie können eine GET-Anfrage an die `/previewsamplestatus/report/namespace` -Endpunkt verwenden, um die Aufschlüsselung nach Identitäts-Namespace für alle zusammengeführten Profile in Ihrem Profilspeicher anzuzeigen. Dazu gehören sowohl die von Adobe bereitgestellten Standardidentitäten als auch die von Ihrem Unternehmen definierten benutzerdefinierten Identitäten.

Identitäts-Namespaces sind eine wichtige Komponente des Adobe Experience Platform Identity Service, die als Indikatoren für den Kontext dient, auf den sich Kundendaten beziehen. Um mehr zu erfahren, lesen Sie zunächst die [Übersicht über Identitäts-Namespace](../../identity-service/namespaces.md).

>[!NOTE]
>
>Die Gesamtanzahl der Profile nach Namespace (addiert die für jeden Namespace angezeigten Werte) kann höher sein als die Profilzählungsmetrik, da ein Profil mit mehreren Namespaces verknüpft werden könnte. Wenn beispielsweise ein Kunde mit Ihrer Marke auf mehr als einem Kanal interagiert, werden diesem einzelnen Kunden mehrere Namespaces zugeordnet.

**API-Format**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| Parameter | Beschreibung |
|---|---|
| `date` | Geben Sie das Datum des zurückzugebenden Berichts an. Wenn am Datum mehrere Berichte ausgeführt wurden, wird der neueste Bericht für dieses Datum zurückgegeben. Wenn für das angegebene Datum kein Bericht vorhanden ist, wird der Fehler 404 (Nicht gefunden) zurückgegeben. Wenn kein Datum angegeben ist, wird der neueste Bericht zurückgegeben. Format: JJJJ-MM-TT. Beispiel: `date=2024-12-31` |

**Anfrage**

Die folgende Anfrage enthält keine `date` und gibt daher den neuesten Bericht zurück.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Die Antwort enthält eine `data` -Array mit einzelnen Objekten, die die Details für jeden Namespace enthalten. Die angezeigte Antwort wurde abgeschnitten und zeigt vier Namespaces.

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
| `sampleCount` | Die Gesamtzahl der gesampelten zusammengeführten Profile im Namespace. |
| `samplePercentage` | Die `sampleCount` als Prozentsatz der gesampelten zusammengeführten Profile (die `numRowsToRead` -Wert, der im [Letzter Beispielstatus](#view-last-sample-status)), ausgedrückt in Dezimalformat. |
| `reportTimestamp` | Der Zeitstempel des Berichts. Wenn eine `date` während der Anfrage angegeben wurde, wird der zurückgegebene Bericht für das angegebene Datum angezeigt. Wenn nicht `date` angegeben wird, wird der neueste Bericht zurückgegeben. |
| `fullIDsFragmentCount` | Die Gesamtzahl der Profilfragmente im Namespace. |
| `fullIDsCount` | Die Gesamtzahl der zusammengeführten Profile im Namespace. |
| `fullIDsPercentage` | Die `fullIDsCount` als Prozentsatz der Gesamt-zusammengeführten Profile (die `totalRows` -Wert, der im [Letzter Beispielstatus](#view-last-sample-status)), ausgedrückt in Dezimalformat. |
| `code` | Die `code` für den Namespace. Dies ist beim Arbeiten mit Namespaces unter Verwendung der Variablen [Adobe Experience Platform Identity Service-API](../../identity-service/api/list-namespaces.md) und wird auch als [!UICONTROL Identitätssymbol] in der Experience Platform-Benutzeroberfläche. Weitere Informationen finden Sie unter [Übersicht über Identitäts-Namespace](../../identity-service/namespaces.md). |
| `value` | Die `id` -Wert für den Namespace. Dies ist beim Arbeiten mit Namespaces unter Verwendung der Variablen [Identity Service-API](../../identity-service/api/list-namespaces.md). |

## Erstellen eines Berichts zur Datensatzüberschneidung

Der Bericht zur Datensatzüberschneidung bietet einen Einblick in die Zusammensetzung des Profilspeichers Ihres Unternehmens, indem er die Datensätze verfügbar macht, die am meisten zu Ihrer adressierbaren Zielgruppe (zusammengeführten Profilen) beitragen. Dieser Bericht bietet Ihnen nicht nur Einblicke in Ihre Daten, sondern ermöglicht Ihnen auch Maßnahmen zur Optimierung der Lizenznutzung, z. B. die Festlegung von Ablauffristen für bestimmte Datensätze.

Sie können den Bericht zur Datensatzüberschneidung generieren, indem Sie eine GET-Anfrage an die `/previewsamplestatus/report/dataset/overlap` -Endpunkt.

Eine schrittweise Anleitung zum Generieren des Berichts zur Datensatzüberlappung mithilfe der Befehlszeile oder der Postman-Benutzeroberfläche finden Sie im Abschnitt [Tutorial zum Generieren der Berichtüberschneidung von Datensätzen](../tutorials/dataset-overlap-report.md).

**API-Format**

```http
GET /previewsamplestatus/report/dataset/overlap
GET /previewsamplestatus/report/dataset/overlap?{QUERY_PARAMETERS}
```

| Parameter | Beschreibung |
|---|---|
| `date` | Geben Sie das Datum des zurückzugebenden Berichts an. Wenn mehrere Berichte am selben Datum ausgeführt wurden, wird der neueste Bericht für dieses Datum zurückgegeben. Wenn für das angegebene Datum kein Bericht vorhanden ist, wird der Fehler 404 (Nicht gefunden) zurückgegeben. Wenn kein Datum angegeben ist, wird der neueste Bericht zurückgegeben. Format: JJJJ-MM-TT. Beispiel: `date=2024-12-31` |

**Anfrage**

Die folgende Anfrage verwendet die `date` -Parameter, um den neuesten Bericht für das angegebene Datum zurückzugeben.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Antwort**

Eine erfolgreiche Anfrage gibt den HTTP-Status 200 (OK) und den Bericht zur Datensatzüberlappung zurück.

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
| `data` | Die `data` -Objekt enthält kommagetrennte Listen mit Datensätzen und den entsprechenden Profilzahlen. |
| `reportTimestamp` | Der Zeitstempel des Berichts. Wenn eine `date` während der Anfrage angegeben wurde, wird der zurückgegebene Bericht für das angegebene Datum angezeigt. Wenn nicht `date` angegeben wird, wird der neueste Bericht zurückgegeben. |

### Interpretieren des Berichts zur Datensatzüberlappung

Die Ergebnisse des Berichts können aus den Datensätzen und Profilzahlen in der Antwort interpretiert werden. Betrachten Sie den folgenden Beispielbericht `data` -Objekt:

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

Dieser Bericht enthält die folgenden Informationen:

* Es gibt 123 Profile, die aus Daten aus den folgenden Datensätzen bestehen: `5d92921872831c163452edc8`, `5da7292579975918a851db57`, `5eb2cdc6fa3f9a18a7592a98`.
* Es gibt 454.412 Profile, die aus Daten aus diesen beiden Datensätzen bestehen: `5d92921872831c163452edc8` und `5eb2cdc6fa3f9a18a7592a98`.
* Es gibt 107 Profile, die nur aus Daten aus einem Datensatz bestehen `5eeda0032af7bb19162172a7`.
* Insgesamt gibt es 454.642 Profile in der Organisation.

## Bericht zur Identitäts-Namespace-Überschneidung erstellen {#identity-overlap-report}

Der Bericht zur Überschneidung von Identitäts-Namespaces bietet Einblick in die Zusammensetzung des Profilspeichers Ihres Unternehmens, indem er die Identitäts-Namespaces offenlegt, die am meisten zu Ihrer adressierbaren Zielgruppe (zusammengeführten Profilen) beitragen. Dazu gehören sowohl die von Adobe bereitgestellten standardmäßigen Identitäts-Namespaces als auch die von Ihrem Unternehmen definierten benutzerdefinierten Identitäts-Namespaces.

Sie können den Bericht zur Überschneidung von Identitäts-Namespaces generieren, indem Sie eine GET-Anfrage an die `/previewsamplestatus/report/namespace/overlap` -Endpunkt.

**API-Format**

```http
GET /previewsamplestatus/report/namespace/overlap
GET /previewsamplestatus/report/namespace/overlap?{QUERY_PARAMETERS}
```

| Parameter | Beschreibung |
|---|---|
| `date` | Geben Sie das Datum des zurückzugebenden Berichts an. Wenn mehrere Berichte am selben Datum ausgeführt wurden, wird der neueste Bericht für dieses Datum zurückgegeben. Wenn für das angegebene Datum kein Bericht vorhanden ist, wird der Fehler 404 (Nicht gefunden) zurückgegeben. Wenn kein Datum angegeben ist, wird der neueste Bericht zurückgegeben. Format: JJJJ-MM-TT. Beispiel: `date=2024-12-31` |

**Anfrage**

Die folgende Anfrage verwendet die `date` -Parameter, um den neuesten Bericht für das angegebene Datum zurückzugeben.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Antwort**

Eine erfolgreiche Anfrage gibt den HTTP-Status 200 (OK) und den Bericht zur Identitäts-Namespace-Überschneidung zurück.

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
| `data` | Die `data` -Objekt enthält kommagetrennte Listen mit eindeutigen Kombinationen aus Identitäts-Namespace-Codes und deren jeweiligen Profilzahlen. |
| Namespace-Codes | Die `code` ist ein Kurzformular für jeden Identitäts-Namespace-Namen. Eine Zuordnung zu jedem `code` zu `name` kann mit der [Adobe Experience Platform Identity Service-API](../../identity-service/api/list-namespaces.md). Die `code` wird auch als [!UICONTROL Identitätssymbol] in der Experience Platform-Benutzeroberfläche. Weitere Informationen finden Sie unter [Übersicht über Identitäts-Namespace](../../identity-service/namespaces.md). |
| `reportTimestamp` | Der Zeitstempel des Berichts. Wenn eine `date` während der Anfrage angegeben wurde, wird der zurückgegebene Bericht für das angegebene Datum angezeigt. Wenn nicht `date` angegeben wird, wird der neueste Bericht zurückgegeben. |

### Interpretieren des Berichts zur Identitäts-Namespace-Überschneidung

Die Ergebnisse des Berichts können aus den Identitäten und Profilzahlen in der Antwort interpretiert werden. Der numerische Wert jeder Zeile gibt an, wie viele Profile aus dieser exakten Kombination aus standardmäßigen und benutzerdefinierten Identitäts-Namespaces bestehen.

Betrachten Sie den folgenden Auszug aus dem `data` -Objekt:

```json
  "AAID,ECID,Email,crmid": 142,
  "AVID,ECID": 24,
  "ECID": 6565
```

Dieser Bericht enthält die folgenden Informationen:

* Es gibt 142 Profile, die aus `AAID`, `ECID`, und `Email` Standardidentitäten sowie benutzerdefinierte `crmid` Identitäts-Namespace.
* Es gibt 24 Profile, die aus `AAID` und `ECID` Identitäts-Namespaces.
* Es gibt 6.565 Profile, die nur eine `ECID` Identität.

## Bericht zu nicht zugeordneten Profilen erstellen

Über den Bericht zu nicht zugewiesenen Profilen können Sie die Zusammensetzung des Profilspeichers Ihres Unternehmens besser einsehen. Ein Profil, das nur ein Profilfragment enthält, ist ein Profil, das die Zuordnung aufgehoben hat. Ein &quot;unbekanntes&quot;Profil ist ein Profil, das mit pseudonymen Identitäts-Namespaces wie `ECID` und `AAID`. Unbekannte Profile sind inaktiv, d. h. sie haben für den angegebenen Zeitraum keine neuen Ereignisse hinzugefügt. Der Bericht zu nicht zugeordneten Profilen bietet eine Aufschlüsselung der Profile für einen Zeitraum von 7, 30, 60, 90 und 120 Tagen.

Sie können den Bericht zu nicht zugewiesenen Profilen generieren, indem Sie eine GET-Anfrage an die `/previewsamplestatus/report/unstitchedProfiles` -Endpunkt.

**API-Format**

```http
GET /previewsamplestatus/report/unstitchedProfiles
```

**Anfrage**

Die folgende Anfrage gibt den Bericht zu nicht zugeordneten Profilen zurück.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/unstitchedProfiles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Antwort**

Eine erfolgreiche Anfrage gibt den HTTP-Status 200 (OK) und den Bericht zu nicht zugeordneten Profilen zurück.

>[!NOTE]
>
>Für die Zwecke dieses Handbuchs wurde der Bericht abgeschnitten und enthält nur `"120days"` und &quot;`7days`&quot;Zeiträume. Der vollständige Bericht zu nicht zugestellten Profilen bietet eine Aufschlüsselung der Profile für einen Zeitraum von 7, 30, 60, 90 und 120 Tagen.

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
| `data` | Die `data` -Objekt enthält die Informationen, die für den Bericht zu nicht zugeordneten Profilen zurückgegeben werden. |
| `totalNumberOfProfiles` | Die Gesamtzahl der eindeutigen Profile im Profilspeicher. Dies entspricht der Anzahl der adressierbaren Zielgruppen. Es enthält sowohl bekannte als auch nicht zugewiesene Profile. |
| `totalNumberOfEvents` | Die Gesamtzahl der ExperienceEvents im Profilspeicher. |
| `unstitchedProfiles` | Ein Objekt, das eine Aufschlüsselung der nicht zugeordneten Profile nach Zeiträumen enthält. Der Bericht zu nicht zugeordneten Profilen bietet eine Aufschlüsselung der Profile für Zeiträume von 7, 30, 60, 90 und 120 Tagen. |
| `countOfProfiles` | Die Anzahl der nicht zugeordneten Profile für den Zeitraum oder die Anzahl der nicht zugeordneten Profile für den Namespace. |
| `eventsAssociated` | Die Anzahl der ExperienceEvents für den Zeitraum oder die Anzahl der Ereignisse für den Namespace. |
| `nsDistribution` | Ein Objekt, das einzelne Identitäts-Namespaces mit der Verteilung nicht zugewiesener Profile und Ereignisse für jeden Namespace enthält. Hinweis: Addieren Sie die Summe `countOfProfiles` für jeden Identitäts-Namespace im `nsDistribution` -Objekt entspricht dem `countOfProfiles` für den Zeitraum. Dasselbe gilt für `eventsAssociated` pro Namespace und der Gesamtwert `eventsAssociated` nach Zeiträumen. |
| `reportTimestamp` | Der Zeitstempel des Berichts. |

### Interpretieren des Berichts über nicht zuordenbare Profile

Die Ergebnisse des Berichts können Aufschluss darüber geben, wie viele nicht zugewiesene und inaktive Profile Ihr Unternehmen im Profilspeicher hat.

Betrachten Sie den folgenden Auszug aus dem `data` -Objekt:

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

* Es gibt 1.782 Profile, die nur ein Profilfragment enthalten und in den letzten sieben Tagen keine neuen Ereignisse haben.
* Den 1.782 aufgetrennten Profilen sind 29.151 ExperienceEvents zugeordnet.
* Es gibt 1.734 nicht zugeordnete Profile, die ein einzelnes Profilfragment aus dem Identitäts-Namespace von ECID enthalten.
* Den 1.734 aufgetrennten Profilen sind 28.591 Ereignisse zugeordnet, die ein einzelnes Profilfragment aus dem Identitäts-Namespace von ECID enthalten.

## Nächste Schritte

Nachdem Sie nun wissen, wie Sie Beispieldaten im Profilspeicher in der Vorschau anzeigen und mehrere Berichte zu den Daten ausführen, können Sie auch die Schätzungs- und Vorschau-Endpunkte der Segmentation Service-API verwenden, um Informationen auf Zusammenfassungsebene zu Ihren Segmentdefinitionen anzuzeigen. Diese Informationen helfen Ihnen dabei sicherzustellen, dass Sie Ihre erwartete Zielgruppe isolieren. Weitere Informationen zum Arbeiten mit Vorschau und Schätzungen mithilfe der Segmentation-API finden Sie unter [Handbuch zur Vorschau und Schätzung von Endpunkten](../../segmentation/api/previews-and-estimates.md).

