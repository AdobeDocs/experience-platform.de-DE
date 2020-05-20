---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handbuch zur Fehlerbehebung bei der Stapeleinbettung in Adobe Experience Platform
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 79466c78fd78c0f99f198b11a9117c946736f47a
workflow-type: tm+mt
source-wordcount: '1366'
ht-degree: 1%

---


# Handbuch zur Fehlerbehebung bei der Stapelverarbeitung

Diese Dokumentation hilft bei der Beantwortung häufig gestellter Fragen zu Adobe Experience Platform Batch Data Ingestion APIs.

## Stapel-API-Aufrufe

### Sind Stapel sofort aktiv, nachdem sie ein HTTP 200 OK von der CompleteBatch-API erhalten haben?

Die `200 OK` Antwort der API bedeutet, dass der Stapel zur Verarbeitung akzeptiert wurde - er ist erst aktiv, wenn er in den finalen Status Transition wird, z. B. Aktiv oder Fehler.

### Ist es sicher, den CompleteBatch-API-Aufruf erneut auszuführen, nachdem er fehlgeschlagen ist?

Ja. Es ist sicher, den API-Aufruf erneut auszuführen. Trotz des Fehlers ist es möglich, dass der Vorgang tatsächlich erfolgreich war und der Stapel erfolgreich akzeptiert wurde. Es wird jedoch erwartet, dass Clients im Fall eines API-Fehlers über Wiederholungsmechanismen verfügen und tatsächlich dazu ermutigt werden, es erneut zu versuchen. Wenn der Vorgang tatsächlich erfolgreich war, gibt die API den Erfolg zurück, auch nach einem erneuten Versuch.

### Wann sollte die API zum Hochladen großer Dateien verwendet werden?

Die empfohlene Dateigröße für die Verwendung der API zum Hochladen großer Dateien ist 256 MB oder höher. Weitere Informationen zur Verwendung der API zum Hochladen großer Dateien finden Sie [hier](./api-overview.md#ingest-large-parquet-files).

### Warum schlägt der Aufruf der Complete-API für große Dateien fehl?

Wenn sich Teile einer großen Datei überschneiden oder fehlen, antwortet der Server mit einer HTTP 400-Fehlerhaften Anforderung. Dies kann vorkommen, da sich überschneidende Abschnitte hochgeladen werden können, da Bereichsüberprüfungen zum Zeitpunkt des Dateiabschlusses durchgeführt werden, wenn die Dateiblöcke zusammengeführt werden.

## Unterstützung bei der Integration

### Welche Importformate werden unterstützt?

Derzeit werden sowohl Parquet als auch JSON unterstützt. CSV wird auf einer älteren Basis unterstützt - während Daten in Master-Tests umgewandelt werden und Vorabprüfungen durchgeführt werden, werden keine modernen Funktionen wie Konvertierung, Partitionierung oder Zeilenvalidierung unterstützt.

### Wo sollte das Stapeleingabeformat angegeben werden?

Das Eingabeformat sollte zur Zeit der Stapelerstellung innerhalb der Nutzlast angegeben werden. Nachfolgend finden Sie ein Beispiel zur Angabe des Stapeleingabeformats:

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

### Wie wird mehrzeiliges JSON erfasst?

Um mehrzeilige JSON-Dateien zu erfassen, muss das `isMultiLineJson` Flag zum Zeitpunkt der Stapelerstellung festgelegt werden. Ein Beispiel hierfür ist unten dargestellt:

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

### Was ist der Unterschied zwischen JSON-Linien (einzeiliges JSON) und mehrzeiliges JSON?

Bei JSON-Zeilen gibt es ein JSON-Objekt pro Zeile. Beispiel:

```json
{"string":"string1","int":1,"array":[1,2,3],"dict": {"key": "value1"}}
{"string":"string2","int":2,"array":[2,4,6],"dict": {"key": "value2"}}
{"string":"string3","int":3,"array":[3,6,9],"dict": {"key": "value3", "extra_key": "extra_value3"}}
```

Bei mehrzeiligen JSON-Dateien kann ein Objekt mehrere Zeilen aufnehmen, während alle Objekte in ein JSON-Array eingeschlossen sind. Beispiel:

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

Standardmäßig verwendet die Batch Data Ingestion einzeilige JSON-Dateien.

### Wird die CSV-Erfassung unterstützt?

Die CSV-Erfassung wird nur für flache Schema unterstützt. Derzeit wird das Einfügen von hierarchischen Daten in CSV nicht unterstützt.

Um alle Datenverarbeitungsfunktionen zu erhalten, müssen JSON- oder Parquet-Formate verwendet werden.

### Welche Arten der Überprüfung werden an den Daten durchgeführt?

Für die Daten werden drei Stufen der Validierung durchgeführt:

- Schema - Die Stapeleinfügung stellt sicher, dass das Schema des Datums der erfassten Daten mit dem Schema des Datensatzes übereinstimmt.
- Datentyp - Stapeleinfügung stellt sicher, dass der Typ für jedes erfasste Feld mit dem im Schema des Datensatzes definierten Typ übereinstimmt.
- Einschränkungen: Durch die Stapeleinfügung werden Einschränkungen wie &quot;Erforderlich&quot;, &quot;Enum&quot;und &quot;Format&quot;in der Schema-Definition korrekt definiert.

### Wie kann ein bereits erfasster Stapel ersetzt werden?

Ein bereits erfasster Stapel kann mithilfe der Funktion &quot;Stapelwiedergabe&quot;ersetzt werden. Weitere Informationen zum Batch Replay finden Sie [hier](./api-overview.md#replay-a-batch).

### Wie wird die Chargenaufnahme überwacht?

Nachdem ein Stapel für die Batch-Promotion signalisiert wurde, kann der Batch-Erfassungsstatus mit der folgenden Anforderung überwacht werden:

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

Mit dieser Anforderung erhalten Sie eine Antwort wie die folgende:

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

## Stapelzustände

### Welche Stapelzustände sind möglich?

Ein Stapel kann während seines Lebenszyklus die folgenden Status durchlaufen:

| Status | In Master geschriebene Daten | Beschreibung |
| ------ | ---------------------- | ----------- |
| Abgebrochen |  | Der Client hat den Stapel im erwarteten Zeitrahmen nicht abgeschlossen. |
| Abgebrochen |  | Der Client hat explizit über die Batch Data Ingestion APIs einen Abbruchvorgang für den angegebenen Stapel aufgerufen. Sobald sich ein Stapel im Status &quot;geladen&quot;befindet, kann der Stapel nicht abgebrochen werden. |
| Aktiv/Erfolg | x | Der Stapel wurde erfolgreich von Stufe zu Master beworben und steht nun für den nachgelagerten Verbrauch zur Verfügung. **Hinweis:** Aktiv und Erfolg werden synonym verwendet. |
| Archiviert |  | Der Stapel wurde in kalte Datenspeicherung archiviert. |
| Fehlgeschlagen/Fehler |  | Ein Terminal-Status, der entweder auf eine fehlerhafte Konfiguration und/oder auf fehlerhafte Daten zurückzuführen ist. Es wird ein umsetzbarer Fehler zusammen mit dem Stapel aufgezeichnet, um Clients in die Lage zu versetzen, die Daten zu korrigieren und erneut zu übermitteln. **Hinweis:** Fehlgeschlagen und Fehler werden synonym verwendet. |
| Inaktiv | x | Der Stapel wurde erfolgreich beworben, wurde jedoch entweder zurückgesetzt oder ist abgelaufen. Der Stapel ist nicht mehr für den nachgelagerten Verbrauch verfügbar, aber die zugrunde liegenden Daten bleiben in Master erhalten, bis er aufbewahrt, archiviert oder anderweitig gelöscht wurde. |
| Laden |  | Der Client schreibt derzeit Daten für den Stapel. Der Stapel ist zu diesem Zeitpunkt **nicht** für die Promotion bereit. |
| geladen |  | Der Client hat das Schreiben von Daten für den Stapel abgeschlossen. Der Stapel kann beworben werden. |
| Bewahrt |  | Die Daten wurden von Master und in einem dafür vorgesehenen Archiv in Adobe Data Lake entfernt. |
| Staging |  | Der Kunde hat den Stapel erfolgreich für die Promotion signalisiert, und die Daten werden für den nachgelagerten Verbrauch gestaffelt. |
| Wiederholung |  | Der Client hat den Stapel für die Promotion signalisiert. Aufgrund eines Fehlers wird der Stapel jedoch von einem Batch-Überwachungsdienst erneut versucht. Dieser Status kann verwendet werden, um Clients darauf hinzuweisen, dass die Datenaufnahme verzögert sein kann. |
| Angehalten |  | Der Client hat den Stapel für die Promotion signalisiert. Nach `n` weiteren Zustellversuchen durch einen Stapelüberwachungsdienst wurde die Batch-Promotion jedoch angehalten. |

### Was bedeutet &quot;Staging&quot;für Stapel?

Befindet sich ein Stapel in &quot;Staging&quot;, bedeutet dies, dass der Stapel erfolgreich für die Promotion signalisiert wurde und dass die Daten für den nachgelagerten Verbrauch gestaffelt werden.

### Was bedeutet das, wenn ein Stapel &quot;Wiederholen&quot;lautet?

Befindet sich ein Stapel in &quot;Wiederholen&quot;, bedeutet dies, dass die Datenerfassung des Stapels aufgrund zeitweiliger Probleme vorübergehend gestoppt wurde. In diesem Fall ist kein Kundeneinsatz erforderlich.

### Was bedeutet das, wenn ein Stapel &quot;angehalten&quot;ist?

Befindet sich ein Stapel in &quot;Angehalten&quot;, bedeutet dies, dass Data Ingestion Services Schwierigkeiten bei der Stapelverarbeitung hat und alle weitere Zustellversuche erschöpft sind.

### Was bedeutet es, wenn ein Stapel noch &quot;geladen&quot; ist?

Befindet sich ein Stapel in &quot;Laden&quot;, bedeutet dies, dass die CompleteBatch-API nicht aufgerufen wurde, um den Stapel zu bewerben.

### Gibt es eine Möglichkeit zu wissen, ob ein Stapel erfolgreich aufgenommen wurde?

Sobald der Stapelstatus &quot;Aktiv&quot;ist, wurde der Stapel erfolgreich erfasst. Um den Status des Stapels zu ermitteln, führen Sie die [zuvor](#how-is-batch-ingestion-monitored)beschriebenen Schritte aus.

### Was passiert, wenn ein Stapel fehlschlägt?

Wenn ein Stapel fehlschlägt, kann der Grund für seinen Fehler im `errors` Abschnitt der Nutzlast angegeben werden. Beispiele für Fehler sind nachfolgend aufgeführt:

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

Nachdem die Fehler korrigiert wurden, kann der Stapel erneut hochgeladen werden.

## Batch-Unterstützung

### Wie sollten Stapel gelöscht werden?

Stapel sollten nicht direkt aus dem Katalog gelöscht werden, sondern mit einer der folgenden Methoden entfernt werden:

1. Wenn der Stapel verarbeitet wird, sollte der Stapel abgebrochen werden.
2. Wenn der Stapel erfolgreich gemeistert wurde, sollte der Stapel zurückgesetzt werden.

### Welche Metriken auf Stapelebene stehen zur Verfügung?

Für Stapel im Status Aktiv/Erfolg stehen die folgenden Metriken auf Stapelebene zur Verfügung:

| Metrik | Beschreibung |
| ------ | ----------- |
| inputByteSize | Die Gesamtanzahl der Bytes, die für die Verarbeitung durch Data Ingestion Services gestaffelt wurden. |
| inputRecordSize | Die Gesamtzahl der für die Verarbeitung durch Data Ingestion Services gestaffelten Zeilen. |
| outputByteSize | Die Gesamtanzahl der Bytes, die von Data Ingestion Services an Data Lake ausgegeben werden. |
| outputRecordSize | Die Gesamtzahl der Zeilen, die von Data Ingestion Services an Data Lake ausgegeben werden. |
| partitionCount | Die Gesamtzahl der in Data Lake geschriebenen Partitionen. |

### Warum sind Metriken in einigen Stapeln nicht verfügbar?

Es gibt zwei Gründe, warum Metriken möglicherweise nicht für Ihren Stapel verfügbar sind:

1. Der Stapel hat ihn nie erfolgreich in den Status Aktiv/Erfolg gebracht.
2. Der Stapel wurde mithilfe eines veralteten Promotion-Pfads wie der CSV-Erfassung gefördert.

### Was bedeuten die verschiedenen Statuscodes?

| Statuscode | Beschreibung |
| ----------- | ----------- |
| 106 | Die Datensatzdatei ist leer. |
| 118 | Die CSV-Datei enthält eine leere Kopfzeile. |
| 200 | Der Stapel wurde zur Verarbeitung akzeptiert und wird in einen finalen Status wie &quot;Aktiv&quot;oder &quot;Fehler&quot;Transition. Nach der Übermittlung kann der Stapel mithilfe des `GetBatch` Endpunkts überwacht werden. |
| 400 | Ungültige Anfrage. Wird zurückgegeben, wenn ein Stapel fehlende oder überlappende Abschnitte enthält. |

[large-file-upload]: batch_data_ingestion_developer_guide.md#how-to-ingest-large-parquet-files
