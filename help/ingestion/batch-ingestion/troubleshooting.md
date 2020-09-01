---
keywords: Experience Platform;home;popular topics;ingested data;troubleshooting;faq;Ingestion;Batch ingestion;batch ingestion;
solution: Experience Platform
title: Handbuch zur Fehlerbehebung bei der Batch-Erfassung in Adobe Experience Platform
topic: troubleshooting
translation-type: tm+mt
source-git-commit: c04fb056d4564e53f192e0734a700a13820f5ba7
workflow-type: tm+mt
source-wordcount: '1389'
ht-degree: 88%

---


# Handbuch zur Fehlerbehebung bei der Batch-Erfassung

This documentation will help answer frequently asked questions regarding Adobe Experience Platform [!DNL Batch Data Ingestion] APIs.

## Batch-API-Aufrufe

### Sind Batches sofort aktiv, nachdem die HTTP-Antwort „200 OK“ von der CompleteBatch-API erhalten wurde?

Die `200 OK`-Antwort der API bedeutet, dass der Batch zur Verarbeitung akzeptiert wurde; er wird aber erst dann aktiv, wenn er seinen endgültigen Status erreicht, z. B. „Aktiv“ oder „Fehler“.

### Ist es sicher, den CompleteBatch-API-Aufruf erneut auszuführen, nachdem er fehlgeschlagen ist?

Ja; es ist sicher, den API-Aufruf erneut auszuführen. Trotz des Fehlers ist es möglich, dass der Vorgang in Wirklichkeit erfolgreich war und der Batch erfolgreich akzeptiert wurde. Es wird jedoch erwartet, dass Clients im Fall eines API-Fehlers über Wiederholungsmechanismen verfügen und tatsächlich dazu ermutigt werden, es erneut zu versuchen. Wenn der Vorgang in Wirklichkeit erfolgreich war, gibt die API eine Erfolgsmeldung zurück, auch nach einem erneuten Versuch.

### Wann sollte die API zum Hochladen großer Dateien (Large File Upload-API) verwendet werden?

Die empfohlene Dateigröße zur Verwendung der Large File Upload-API ist 256 MB oder mehr. Weiterführende Informationen zur Nutzung der Large File Upload-API finden Sie [hier](./api-overview.md#ingest-large-parquet-files).

### Warum schlägt der Aufruf der Large File Upload-API fehl?

Wenn sich Teile einer großen Datei überschneiden oder fehlen, antwortet der Server mit einer HTTP-Antwort „400 Ungültige Anfrage“. Das kann geschehen, da sich überschneidende Abschnitte hochladen lassen, weil Bereichsprüfungen zum Zeitpunkt der Dateifertigstellung beim Zusammenfügen der Dateiblöcke durchgeführt werden.

## Hilfe bei der Erfassung

### Welche Erfassungsformate werden unterstützt?

Derzeit werden sowohl Parquet als auch JSON unterstützt. CSV wird auf einer älteren Basis unterstützt; zwar werden Daten zum Master höher gestuft und Vorabprüfungen durchgeführt, doch werden keine modernen Funktionen wie Konvertierung, Partitionierung oder Zeilenvalidierung unterstützt.

### Wo sollte das Batch-Eingabeformat angegeben werden?

Das Eingabeformat sollte bei der Batch-Erstellung in der Payload angegeben werden. Nachfolgend finden Sie ein Beispiel zur Angabe des Batch-Eingabeformats:

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
    }'
```

### Warum werden die hochgeladenen Daten nicht im Datensatz angezeigt?

Damit Daten im Datensatz angezeigt werden, muss der Stapel als abgeschlossen markiert werden. Alle Dateien, die Sie erfassen möchten, müssen hochgeladen werden, bevor der Stapel als abgeschlossen markiert werden kann. Ein Beispiel für die Kennzeichnung eines Stapels als abgeschlossen ist unten aufgeführt:

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### Wie wird mehrzeilige JSON erfasst?

Um mehrzeilige JSON zu erfassen, muss bei der Batch-Erstellung das `isMultiLineJson`-Flag gesetzt werden. Ein Beispiel dafür ist unten dargestellt:

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json",
                "isMultiLineJson": true
           }
      }'
```

### Was ist der Unterschied zwischen JSON-Zeilen (einzeilige JSON) und mehrzeiliger JSON?

Bei JSON-Zeilen gibt es ein JSON-Objekt pro Zeile. Beispiel:

```json
{"string":"string1","int":1,"array":[1,2,3],"dict": {"key": "value1"}}
{"string":"string2","int":2,"array":[2,4,6],"dict": {"key": "value2"}}
{"string":"string3","int":3,"array":[3,6,9],"dict": {"key": "value3", "extra_key": "extra_value3"}}
```

Bei mehrzeiliger JSON kann ein Objekt mehrere Zeilen belegen, während alle Objekte in ein JSON-Array eingeschlossen sind. Beispiel:

```json
[
    {"string":"string1","int":1,"array":[1,2,3],"dict": {"key": "value1"}},
    {"string":"string2","int":2,"array":[2,4,6],"dict": {"key": "value2"}},
    {
        "string": "string3",
        "int": 3,
        "array": [
            3,
            6,
            9
        ],
        "dict": {
            "key": "value3",
            "extra_key": "extra_value3"
        }
    }
]
```

By default, [!DNL Batch Data Ingestion] uses single-line JSON.

### Wird CSV-Erfassung unterstützt?

CSV-Erfassung wird nur bei flachen Schemas unterstützt. Derzeit wird das Einfügen hierarchischer Daten in CSV nicht unterstützt.

Um alle Datenerfassungsfunktionen zu erhalten, müssen JSON- oder Parquet-Formate verwendet werden.

### Welche Arten der Validierung werden für die Daten ausgeführt?

Für die Daten werden drei Validierungsstufen ausgeführt:

- Schema – Batch-Erfassung stellt sicher, dass das Schema der erfassten Daten mit dem Schema des Datensatzes übereinstimmt.
- Datentyp – Batch-Erfassung stellt sicher, dass der Typ für jedes erfasste Feld mit dem im Schema des Datensatzes definierten Typ übereinstimmt.
- Begrenzungen – Batch-Erfassung stellt sicher, dass Begrenzungen wie „Erforderlich“, „Aufzählung“ und „Format“ in der Schemadefinition richtig definiert sind.

### Wie kann ein bereits erfasster Batch ersetzt werden?

Ein bereits erfasster Batch kann mithilfe der Funktion „Batch-Wiedergabe“ ersetzt werden. Weiterführende Informationen zur „Batch-Wiedergabe“ finden Sie [hier](./api-overview.md#replay-a-batch).

### Wie lässt sich die Batch-Erfassung überwachen?

Nachdem ein Batch für die Batch-Promotion signalisiert wurde, kann der Fortschritt der Batch-Erfassung mit der folgenden Anfrage überwacht werden:

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

Bei dieser Anfrage erhalten Sie eine Antwort, die in etwa der folgenden ähnelt:

```http
200 OK
```

```json
{
    "{BATCH_ID}":{
        "imsOrg":"{IMS_ORG}",
        "created":1494349962314,
        "createdClient":"{API_KEY}",
        "createdUser":"{USER_ID}",
        "updatedUser":"{USER_ID}",
        "completed":1494349963467,
        "externalId":"{EXTERNAL_ID}",
        "status":"staging",
        "errors":[],
    }
}
```

## Batch-Status

### Welche Batch-Status sind möglich?

Ein Batch kann in seinem Lebenszyklus die folgenden Status durchlaufen:

| Status | In Master geschriebene Daten | Beschreibung |
| ------ | ---------------------- | ----------- |
| Vorzeitig beendet |  | Der Client hat den Batch im erwarteten Zeitrahmen nicht abgeschlossen. |
| Abgebrochen |  | The client has explicitly called, via the [!DNL Batch Data Ingestion] APIs, an abort operation for the specified batch. Sobald sich ein Batch im Status „Geladen“ befindet, kann der Batch nicht mehr abgebrochen werden. |
| Aktiv/Erfolg | x | Der Batch wurde erfolgreich von „Staging“ zu „Master“ höher gestuft und steht nun für den nachgelagerten Gebrauch zur Verfügung. **Hinweis:** „Aktiv“ und „Erfolg“ werden synonym verwendet. |
| Archiviert |  | Der Batch wurde in Cold Storage archiviert. |
| Fehlgeschlagen/Fehler |  | Ein Terminal-Status, der entweder auf eine fehlerhafte Konfiguration und/oder auf fehlerhafte Daten zurückzuführen ist. Zusammen mit dem Batch wird ein eine Aktion erfordernder Fehler aufgezeichnet, um es Clients zu erlauben, die Daten zu korrigieren und erneut zu übermitteln. **Hinweis:** „Fehlgeschlagen“ und „Fehler“ werden synonym verwendet. |
| Inaktiv | x | Der Batch wurde erfolgreich höher gestuft, wurde dann jedoch entweder zurückgesetzt oder ist abgelaufen. Der Batch ist nicht mehr für den nachgelagerten Gebrauch verfügbar, die zugrunde liegenden Daten aber bleiben im Master erhalten, bis sie aufbewahrt, archiviert oder anderweitig gelöscht werden. |
| Wird geladen |  | Der Client schreibt derzeit Daten für den Batch. Der Batch ist zu diesem Zeitpunkt **nicht** bereit zur Promotion. |
| Geladen |  | Der Client hat das Schreiben von Daten für den Batch abgeschlossen. Der Batch kann jetzt höher gestuft werden. |
| Beibehalten |  | Die Daten wurden dem Master entnommen und in einem dafür vorgesehenen Archiv im Adobe Data Lake platziert. |
| Staging |  | Der Client hat den Batch erfolgreich für die Promotion signalisiert, und die Daten werden für den nachgelagerten Gebrauch bereitgestellt. |
| Wird wiederholt |  | Der Client hat den Batch zur Promotion signalisiert. Aufgrund eines Fehlers versucht es ein Batch-Überwachungsdienst für den Batch jedoch erneut. Dieser Status kann dazu dienen, Clients darauf hinzuweisen, dass sich die Datenerfassung verzögern kann. |
| Angehalten |  | Der Client hat den Stapel für die Promotion signalisiert. Nach `n` weiteren Versuchen durch einen Batch-Überwachungsdienst wurde die Batch-Promotion jedoch angehalten. |

### Was bedeutet „Staging“ für Batches?

Befindet sich ein Batch im „Staging“ befindet, bedeutet dies, dass der Batch erfolgreich für die Promotion signalisiert wurde und die Daten für den nachgelagerten Gebrauch bereitgestellt werden.

### Was bedeutet es, wenn es bei einem Batch heißt: „Wird wiederholt“?

Wenn ein Batch den Status „Wird wiederholt“ aufweist, bedeutet dies, dass die Datenerfassung des Batch aufgrund zeitweiliger Probleme vorübergehend angehalten wurde. In diesem Fall ist keine Kundenintervention erforderlich.

### Was bedeutet das, wenn ein Stapel „angehalten“ wurde?

When a batch is in &quot;Stalled&quot;, it means that [!DNL Data Ingestion Services] is experiencing difficulty ingesting the batch and all retries have been exhausted.

### Was bedeutet es, wenn der Status eines Batch immer noch „Wird geladen“ lautet?

Befindet sich ein Batch im Status „Wird geladen“, bedeutet dies, dass die CompleteBatch-API noch nicht aufgerufen wurde, um den Batch höher zu stufen.

### Gibt es eine Möglichkeit herauszufinden, ob ein Batch erfolgreich erfasst wurde?

Sobald der Batch-Status „Aktiv“ ist, wurde ein Batch erfolgreich erfasst. Um den Status des Batch zu ermitteln, führen Sie die [zuvor](#how-is-batch-ingestion-monitored) beschriebenen Schritte aus.

### Was passiert, wenn ein Batch fehlschlägt?

Wenn ein Batch fehlschlägt, kann der Grund für den Fehler im Abschnitt `errors` der Payload ermittelt werden. Beispiele für Fehler sind nachfolgend aufgeführt:

```json
    "errors":[
        {
            "code":"106",
            "description":"Dataset file is empty. Please upload file with data.",
            "rows":[]
        },
        {
            "code":"118",
            "description":"CSV file contains empty header row.",
            "rows":[]
        }
    ]
```

Nach der Korrektur der Fehler kann der Batch erneut hochgeladen werden.

## Batch-Unterstützung

### Wie sollten Batches gelöscht werden?

Instead of deleting directly from [!DNL Catalog], batches should be removed using either method provided below:

1. Wenn der Batch in Bearbeitung ist, sollte der Batch abgebrochen werden.
2. Wenn der Batch erfolgreich zum „Master“ höher gestuft wurde, sollte der Batch zurückgesetzt werden.

### Welche Metriken auf Batch-Ebene stehen zur Verfügung?

Für Batches mit dem Status „Aktiv“/„Erfolg“ stehen auf Batch­Ebene die folgenden Metriken zur Verfügung:

| Metrik | Beschreibung |
| ------ | ----------- |
| inputByteSize | The total number of bytes staged for [!DNL Data Ingestion Services] to process. |
| inputRecordSize | The total number of rows staged for [!DNL Data Ingestion Services] to process. |
| outputByteSize | Die Gesamtanzahl der Bytes, die von [!DNL Data Ingestion Services] bis ausgegeben werden [!DNL Data Lake]. |
| outputRecordSize | Die Gesamtanzahl der Zeilen, die von [!DNL Data Ingestion Services] bis ausgegeben werden [!DNL Data Lake]. |
| partitionCount | The total number of partitions written into [!DNL Data Lake]. |

### Warum sind Metriken nicht bei allen Batches verfügbar?

Es gibt zwei Gründe, warum möglicherweise keine Metriken für Ihren Batch verfügbar sind:

1. Der Batch hat es nie erfolgreich bis zum Status „Aktiv“/„Erfolg“ geschafft.
2. Der Batch wurde mithilfe eines veralteten Promotionspfads (wie CSV-Erfassung) höher gestuft.

### Was bedeuten die verschiedenen Status-Codes?

| Status-Code | Beschreibung |
| ----------- | ----------- |
| 106 | Die Datensatzdatei ist leer. |
| 118 | Die CSV-Datei enthält eine leere Kopfzeile. |
| 200 | Der Batch wurde zur Verarbeitung angenommen und wird einen endgültigen Status wie „Aktiv“ oder „Fehler“ erhalten. Nach der Übermittlung kann der Batch mithilfe des `GetBatch`-Endpunkts überwacht werden. |
| 400 | Ungültige Anfrage. Wird zurückgegeben, wenn ein Batch fehlende oder überlappende Abschnitte enthält. |

[large-file-upload]: batch_data_ingestion_developer_guide.md#how-to-ingest-large-parquet-files
