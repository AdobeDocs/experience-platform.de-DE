---
title: API-Endpunkt für Datensatzgültigkeiten
description: Mit dem Endpunkt /ttl in der Datenhygiene-API können Sie programmgesteuert einen Zeitplan für Datensatzgültigkeiten in Adobe Experience Platform festlegen.
role: Developer
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1966'
ht-degree: 50%

---

# Endpunkt der Datensatzgültigkeit

Der `/ttl`-Endpunkt in der Datenhygiene-API ermöglicht Ihnen, in Adobe Experience Platform Ablaufdaten für Datensätze zu planen.

Eine Datensatzgültigkeit ist nur ein zeitverzögerter Löschvorgang. Der Datensatz ist in der Zwischenzeit nicht geschützt und kann daher auf andere Weise gelöscht werden, bevor sein Ablaufdatum erreicht wurde.

>[!NOTE]
>
>Obwohl die Löschung als spezifischer Zeitpunkt angegeben ist, kann es bis zu 24 Stunden nach Ablauf der Frist dauern, bevor die eigentliche Löschung eingeleitet wird. Nachdem der Löschvorgang gestartet wurde, kann es bis zu sieben Tage dauern, bis alle Spuren des Datensatzes aus Experience Platform-Systemen entfernt wurden.

Sie können die Gültigkeit jederzeit abbrechen oder den Löschzeitpunkt ändern, solange der Datensatz-Löschvorgang noch nicht gestartet wurde. Nachdem Sie eine Datensatzgültigkeit abgebrochen haben, können Sie sie erneut starten, indem Sie ein neues Ablaufdatum festlegen.

Sobald das Löschen des Datensatzes gestartet wurde, wird seine Gültigkeit als `executing` gekennzeichnet und darf nicht weiter geändert werden. Der Datensatz selbst kann bis zu sieben Tage lang wiederhergestellt werden, jedoch nur durch einen manuellen Prozess über eine Adobe-Service-Anfrage. Während die Anfrage ausgeführt wird, beginnen der Data Lake, der Identity Service und das Echtzeit-Kundenprofil separate Prozesse, um den Inhalt des Datensatzes aus den entsprechenden Services zu entfernen. Sobald die Daten aus allen drei Services gelöscht wurden, wird der Ablauf als `completed` gekennzeichnet.

>[!WARNING]
>
>Wenn ein Datensatz ausläuft, müssen alle Datenflüsse, die Daten in diesen Datensatz einspeisen, manuell geändert werden, damit Ihre nachgeschalteten Workflows nicht beeinträchtigt werden.

Advanced Data Lifecycle Management unterstützt das Löschen von Datensätzen über den Datensatzgültigkeits-Endpunkt und ID-Löschungen (Daten auf Zeilenebene) mithilfe primärer Identitäten über den [Arbeitsauftrags-Endpunkt](./workorder.md). Sie können das Löschen von [Datensatzgültigkeiten](../ui/dataset-expiration.md) und [Datensätzen](../ui/record-delete.md) auch über die Experience Platform-Benutzeroberfläche verwalten. Weitere Informationen finden Sie in der verknüpften Dokumentation .

>[!NOTE]
>
>Der Datenlebenszyklus unterstützt keine Batch-Löschung.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der Data Hygiene API. Bevor Sie fortfahren, lesen Sie [API-Handbuch](./overview.md) um Informationen zu den erforderlichen Kopfzeilen für CRUD-Vorgänge, Fehlermeldungen, Postman-Sammlungen und zum Lesen von Beispiel-API-Aufrufen zu erhalten.

>[!IMPORTANT]
>
>Beim Aufrufen der Datenhygiene-API müssen Sie den -H-`x-sandbox-name: {SANDBOX_NAME}`-Header verwenden.

## Auflisten der Datensatzgültigkeiten {#list}

Sie können alle Datensatzgültigkeiten für Ihr Unternehmen auflisten, indem Sie eine GET-Anfrage stellen. Abfrageparameter können verwendet werden, um die Antwort nach geeigneten Ergebnissen zu filtern.

**API-Format**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| Parameter | Beschreibung |
| --- | --- |
| `{QUERY_PARAMETERS}` | Eine Liste optionaler Abfrageparameter mit mehreren durch `&`-Zeichen getrennten Parametern. Zu den gebräuchlichen Parametern gehören `limit` und `page` für Paginierungszwecke. Eine vollständige Liste der unterstützten Abfrageparameter finden Sie im [Anhang](#query-params). |

{style="table-layout:auto"}

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl?updatedToDate=2021-08-01&author=LIKE%20%25Jane%20Doe%25 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort listet die resultierenden Datensatzgültigkeiten auf. Das folgende Beispiel wurde aus Platzgründen gekürzt.

>[!IMPORTANT]
>
>Die `ttlId` in der Antwort wird auch als `{DATASET_EXPIRATION_ID}` bezeichnet. Beide beziehen sich auf die eindeutige Kennung für die Datensatzgültigkeit.

```json
{
  "results": [
    {
      "ttlId": "SD-b16c8b48-a15a-45c8-9215-587ea89369bf",
      "datasetId": "629bd9125b31471b2da7645c",
      "datasetName": "Sample Acme dataset",
      "sandboxName": "hygiene-beta",
      "imsOrg": "A2A5*EF06164773A8A49418C@AdobeOrg",
      "status": "pending",
      "expiry": "2050-01-01T00:00:00Z",
      "updatedAt": "2023-06-09T16:52:44.136028Z",
      "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e"
    }
  ],
  "current_page": 0,
  "total_pages": 1,
  "total_count": 1
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `total_count` | Anzahl der Datensatzgültigkeiten, die den Parametern des Auflistungsaufrufs entsprechen. |
| `results` | Enthält die Details der zurückgegebenen Datensatzgültigkeiten. Weitere Informationen zu den Eigenschaften einer Datensatzgültigkeit finden Sie im Antwort-Abschnitt zum Erstellen eines [Suchaufrufs](#lookup). |

{style="table-layout:auto"}

## Nachschlagen einer Datensatzgültigkeit {#lookup}

Um nach einer Datensatzgültigkeit zu suchen, stellen Sie eine GET-Anfrage mit dem `{DATASET_ID}` oder dem `{DATASET_EXPIRATION_ID}`.

>[!IMPORTANT]
>
>Die `{DATASET_EXPIRATION_ID}` wird in der Antwort als `ttlId` bezeichnet. Beide beziehen sich auf die eindeutige Kennung für die Datensatzgültigkeit.

**API-Format**

```http
GET /ttl/{DATASET_ID}?include=history
GET /ttl/{DATASET_EXPIRATION_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_ID}` | ID des Datensatzes, dessen Gültigkeit Sie nachschlagen möchten. |
| `{DATASET_EXPIRATION_ID}` | Die ID der Datensatzgültigkeit. |

{style="table-layout:auto"}

**Anfrage**

Die folgende Anfrage sucht für den Datensatz `62759f2ede9e601b63a2ee14` nach den Details der Gültigkeit:

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/62759f2ede9e601b63a2ee14 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Datensatzgültigkeit zurück.

```json
{
    "ttlId": "SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "datasetName": "XtVRwq9-38734",
    "sandboxName": "prod",
    "imsOrg": "A2A5*EF06164773A8A49418C@AdobeOrg",
    "status": "pending",
    "expiry": "2024-12-31T23:59:59Z",
    "updatedAt": "2024-05-11T15:12:40.393115Z",
    "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
    "displayName": "Delete Acme Data before 2025",
    "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `ttlId` | Die ID der Datensatzgültigkeit. |
| `datasetId` | Die ID des Datensatzes, für den diese Gültigkeit zutrifft. |
| `datasetName` | Anzeigename für den Datensatz, für den diese Gültigkeit zutrifft. |
| `sandboxName` | Name der Sandbox, unter dem der Zieldatensatz zu finden ist. |
| `imsOrg` | Die Kennung Ihrer Organisation. |
| `status` | Der aktuelle Status der Datensatzgültigkeit. |
| `expiry` | Das geplante Datum und die Uhrzeit, zu der der Datensatz gelöscht wird. |
| `updatedAt` | Ein Zeitstempel, der angibt, wann die Gültigkeit zuletzt aktualisiert wurde. |
| `updatedBy` | Die Person, der die Gültigkeit zuletzt aktualisiert hat. |
| `displayName` | Der Anzeigename für die Anfrage zur Gültigkeit. |
| `description` | Eine Beschreibung für die Anfrage zur Gültigkeit. |

{style="table-layout:auto"}

### Gültigkeits-Tags des Katalogs

Wenn Sie die [Katalog-API](../../catalog/api/getting-started.md) verwenden, um Details zu einem Datensatz nachzuschlagen, wird dieser unter `tags.adobe/hygiene/ttl` aufgeführt, wenn er ein aktives Gültigkeitsdatum hat.

Die folgende JSON-Datei enthält die gekürzte Antwort für die Details eines Datensatzes aus dem Katalog mit einem Gültigkeitswert von `32503680000000`. Der Wert des Tags kodiert die Gültigkeit als ganzzahlige Anzahl von Millisekunden seit Beginn der Unix-Epoche.

```json
{
  "63212313c308d51b997858ba": {
    "name": "Test Dataset",
    "description": "A piecrust promise, made to be broken",
    "imsOrg": "0FCC747E56F59C747F000101@AdobeOrg",
    "sandboxId": "8dc51b90-d0f9-11e9-b164-ed6a398c8b35",
    "tags": {
      "adobe/hygiene/ttl": [ "32503680000000" ],
      ...
    },
    ...
  }
}
```

## Erstellen einer Datensatzgültigkeit {#create}

Um sicherzustellen, dass Daten nach einem bestimmten Zeitraum aus dem System entfernt werden, planen Sie eine Gültigkeit für einen bestimmten Datensatz, indem Sie die Datensatz-ID sowie das Ablaufdatum und die Ablaufzeit im ISO 8601-Format angeben.

Um eine Datensatzgültigkeit zu erstellen, führen Sie eine POST-Anfrage durch (wie unten gezeigt) und geben Sie die unten genannten Werte in der Payload an.

>[!NOTE]
>
>Wenn Sie einen 404-Fehler erhalten, stellen Sie sicher, dass die Anfrage keine zusätzlichen Schrägstriche aufweist. Ein Schrägstrich am Ende kann dazu führen, dass eine POST-Anfrage fehlschlägt.

**API-Format**

```http
POST /ttl
```

**Anfrage**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/ttl \
  -H `Authorization: Bearer {ACCESS_TOKEN}`
  -H `x-gw-ims-org-id: {ORG_ID}`
  -H `x-api-key: {API_KEY}`
  -H `Accept: application/json`
  -d {
      "datasetId": "5b020a27e7040801dedbf46e",
      "expiry": "2030-12-31T23:59:59Z"
      "displayName": "Delete Acme Data before 2025",
      "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
      }
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `datasetId` | **Erforderlich** Die ID des Zieldatensatzes, für den Sie eine Gültigkeit planen möchten. |
| `expiry` | **Erforderlich** Datum und Uhrzeit im ISO 8601-Format. Wenn die Zeichenfolge keinen expliziten Zeitzonenversatz hat, wird als Zeitzone UTC angenommen. Die Lebensdauer der Daten innerhalb des Systems wird anhand des angegebenen Ablaufwerts festgelegt.<br>Hinweis:<ul><li>Die Anfrage schlägt fehl, wenn bereits eine Datensatzgültigkeit für den Datensatz vorhanden ist.</li><li>Datum und Uhrzeit müssen mindestens **24 Stunden in der Zukunft liegen**.</li></ul> |
| `displayName` | Ein optionaler Anzeigename für die Datensatz-Gültigkeitsanfrage. |
| `description` | Eine optionale Beschreibung für die Anfrage zur Gültigkeit. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 (Erstellt) und den neuen Status der Datensatzgültigkeit zurück.

```json
{
  "ttlId":       "SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f",
  "datasetId":   "5b020a27e7040801dedbf46e",
  "datasetName": "Acme licensed data",
  "sandboxName": "prod",
  "imsOrg":      "{ORG_ID}",
  "status":      "pending",
  "expiry":      "2030-12-31T23:59:59Z",
  "updatedAt":   "2021-08-19T11:14:16Z",
  "updatedBy":   "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
  "displayName": "Delete Acme Data before 2031",
  "description": "The Acme information in this dataset is licensed for our use through the end of 2030."
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `ttlId` | Die ID der Datensatzgültigkeit. |
| `datasetId` | Die ID des Datensatzes, für den diese Gültigkeit zutrifft. |
| `datasetName` | Anzeigename für den Datensatz, für den diese Gültigkeit zutrifft. |
| `sandboxName` | Name der Sandbox, unter dem der Zieldatensatz zu finden ist. |
| `imsOrg` | Die Kennung Ihrer Organisation. |
| `status` | Der aktuelle Status der Datensatzgültigkeit. |
| `expiry` | Das geplante Datum und die Uhrzeit, zu der der Datensatz gelöscht wird. |
| `updatedAt` | Ein Zeitstempel, der angibt, wann die Gültigkeit zuletzt aktualisiert wurde. |
| `updatedBy` | Die Person, der die Gültigkeit zuletzt aktualisiert hat. |
| `displayName` | Ein Anzeigename für die Anfrage zur Gültigkeit. |
| `description` | Eine Beschreibung für die Anfrage zur Gültigkeit. |

Ein 400-HTTP-Status (Bad Request) tritt auf, wenn für den Datensatz bereits eine Datensatzgültigkeit vorhanden ist. Eine nicht erfolgreiche Antwort gibt den HTTP-Status 404 (Nicht gefunden) zurück, wenn keine solche Datensatzgültigkeit vorhanden ist (oder Sie keinen Zugriff auf den Datensatz haben).

## Aktualisieren der Datensatzgültigkeit {#update}

Um ein Ablaufdatum für einen Datensatz zu aktualisieren, verwenden Sie eine PUT-Anfrage und die `ttlId` . Sie können die `displayName`-, `description`- und/oder `expiry` aktualisieren.

>[!NOTE]
>
>Wenn Sie Ablaufdatum und -uhrzeit ändern, muss dieser Wert mindestens 24 Stunden in der Zukunft liegen. Diese erzwungene Verzögerung bietet Ihnen die Möglichkeit, den Ablauf abzubrechen oder neu zu planen und einen versehentlichen Datenverlust zu vermeiden.

**API-Format**

```http
PUT /ttl/{DATASET_EXPIRATION_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_EXPIRATION_ID}` | Die ID der Datensatzgültigkeit, die Sie ändern möchten. Hinweis: Dies wird in der Antwort als `ttlId` bezeichnet. |

**Anfrage**

Mit der folgenden Anfrage wird ein neuer Zeitplan für eine Datensatzgültigkeit `SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f` Ende 2024 festgelegt (Greenwich Mean Time). Wenn die vorhandene Datensatzgültigkeit gefunden wird, wird diese mit dem neuen `expiry` aktualisiert.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "expiry": "2024-12-31T23:59:59Z",
        "displayName": "Delete Acme Data before 2025",
        "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `expiry` | **Erforderlich** Datum und Uhrzeit im ISO 8601-Format. Wenn die Zeichenfolge keinen expliziten Zeitzonenversatz hat, wird als Zeitzone UTC angenommen. Die Lebensdauer der Daten innerhalb des Systems wird anhand des angegebenen Ablaufwerts festgelegt. Jeder frühere Gültigkeitszeitstempel für denselben Datensatz muss durch den von Ihnen angegebenen neuen Gültigkeitswert ersetzt werden. Datum und Uhrzeit müssen mindestens **24 Stunden in der Zukunft liegen**. |
| `displayName` | Ein Anzeigename für die Anfrage zur Gültigkeit. |
| `description` | Eine optionale Beschreibung für die Anfrage zur Gültigkeit. |

{style="table-layout:auto"}

**Antwort**

Eine erfolgreiche Antwort gibt den neuen Status der Datensatzgültigkeit sowie den HTTP-Status 200 (OK) zurück, wenn eine bereits vorhandene Gültigkeit aktualisiert wurde.

```json
{
    "ttlId": "SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f",
    "datasetId": "5b020a27e7040801dedbf46e",
    "imsOrg": "A2A5*EF06164773A8A49418C@AdobeOrg",
    "status": "pending",
    "expiry": "2024-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T22:38:40.393115Z",
    "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
    "displayName": "Delete Acme Data before 2025",
    "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `ttlId` | Die ID der Datensatzgültigkeit. |
| `datasetId` | Die ID des Datensatzes, für den diese Gültigkeit zutrifft. |
| `imsOrg` | Die Kennung Ihrer Organisation. |
| `status` | Der aktuelle Status der Datensatzgültigkeit. |
| `expiry` | Das geplante Datum und die Uhrzeit, zu der der Datensatz gelöscht wird. |
| `updatedAt` | Ein Zeitstempel, der angibt, wann die Gültigkeit zuletzt aktualisiert wurde. |
| `updatedBy` | Die Person, der die Gültigkeit zuletzt aktualisiert hat. |

{style="table-layout:auto"}

Eine nicht erfolgreiche Antwort gibt den HTTP-Status 404 (Nicht gefunden) zurück, wenn keine solche Datensatzgültigkeit vorhanden ist.

## Abbrechen der Datensatzgültigkeit {#delete}

Sie können eine Datensatzgültigkeit abbrechen, indem Sie eine DELETE-Anfrage stellen.

>[!NOTE]
>
>Nur Datensatzgültigkeiten mit dem Status `pending` können abgebrochen werden. Beim Versuch, eine Gültigkeit abzubrechen, die ausgeführt oder bereits abgebrochen wurde, wird ein HTTP 404-Fehler zurückgegeben.

**API-Format**

```http
DELETE /ttl/{EXPIRATION_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{EXPIRATION_ID}` | Die `ttlId` der Datensatzgültigkeit, die Sie abbrechen möchten. |

{style="table-layout:auto"}

**Anfrage**

Mit der folgenden Anfrage wird die Gültigkeit eines Datensatzes mit der ID `SD-b16c8b48-a15a-45c8-9215-587ea89369bf` abgebrochen:

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-b16c8b48-a15a-45c8-9215-587ea89369bf \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) zurück und das Attribut `status` der Gültigkeit wird auf `cancelled` gesetzt.

## Anhang

### Akzeptierte Abfrageparameter {#query-params}

In der folgenden Tabelle sind die verfügbaren Abfrageparameter beim [Auflisten von Datensatzgültigkeiten](#list) aufgeführt:

>[!NOTE]
>
>Die Parameter `description`, `displayName` und `datasetName` enthalten alle die Möglichkeit, nach LIKE-Werten zu suchen. Das bedeutet, dass Sie geplante Datensatzgültigkeiten mit den Namen „Name123“, „Name183“, „DisplayName1234“ finden können, indem Sie nach der Zeichenfolge „Name1“ suchen.

| Parameter | Beschreibung | Beispiel |
| --- | --- | --- |
| `author` | Verwenden Sie den `author` Abfrageparameter , um die Person zu finden, die die Datensatzgültigkeit zuletzt aktualisiert hat. Wenn seit seiner Erstellung keine Aktualisierungen vorgenommen wurden, entspricht dies dem ursprünglichen Ersteller der Gültigkeit. Dieser Parameter sucht nach Gültigkeiten, bei denen das `created_by` Feld der Suchzeichenfolge entspricht.<br>Wenn die Suchzeichenfolge mit `LIKE` oder `NOT LIKE` beginnt, wird der Rest als SQL-Suchmuster behandelt. Andernfalls wird die gesamte Suchzeichenfolge als exakte Zeichenfolge gehandhabt, die genau mit dem gesamten Inhalt des `created_by`-Felds übereinstimmen muss. | `author=LIKE %john%`, `author=John Q. Public` |
| `datasetId` | Gibt die Gültigkeiten wieder, die für einen bestimmten Datensatz gelten. | `datasetId=62b3925ff20f8e1b990a7434` |
| `datasetName` | Gibt die Gültigkeiten zurück, deren Datensatzname die angegebene Suchzeichenfolge enthält. Bei der Übereinstimmung wird nicht zwischen Groß- und Kleinschreibung unterschieden. | `datasetName=Acme` |
| `description` |   | `description=Handle expiration of Acme information through the end of 2024.` |
| `displayName` | Gibt die Gültigkeiten zurück, deren Anzeigename die angegebene Suchzeichenfolge enthält. Bei der Übereinstimmung wird nicht zwischen Groß- und Kleinschreibung unterschieden. | `displayName=License Expiry` |
| `executedDate` / `executedFromDate` / `executedToDate` | Filtert Ergebnisse nach einem genauen Ausführungsdatum, einem Enddatum für die Ausführung oder einem Startdatum für die Ausführung. Sie werden verwendet, um Daten oder Datensätze abzurufen, die mit der Ausführung eines Vorgangs an einem bestimmten Datum, vor einem bestimmten Datum oder nach einem bestimmten Datum verbunden sind. | `executedDate=2023-02-05T19:34:40.383615Z` |
| `expiryDate` | Gibt die Gültigkeiten wieder, die im 24-Stunden-Fenster des angegebenen Datums aufgetreten sind. | `2024-01-01` |
| `expiryToDate` / `expiryFromDate` | Gibt die Gültigkeiten wieder, die im angegebenen Intervall ausgeführt werden sollen oder bereits ausgeführt wurden. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |
| `limit` | Eine Ganzzahl zwischen 1 und 100, die die maximale Anzahl der zurückzugebenden Gültigkeiten angibt. Die Standardeinstellung ist 25. | `limit=50` |
| `orderBy` | Der `orderBy` Abfrageparameter gibt die Sortierreihenfolge der von der API zurückgegebenen Ergebnisse an. Verwenden Sie diese Option, um die Daten basierend auf einem oder mehreren Feldern entweder in aufsteigender (ASC) oder absteigender (DESC) Reihenfolge anzuordnen. Verwenden Sie das Präfix + oder -, um ASC bzw. DESC anzugeben. Folgende Werte werden akzeptiert: `displayName`, `description`, `datasetName`, `id`, `updatedBy`, `updatedAt`, `expiry`, `status`. | `-datasetName` |
| `orgId` | Gibt die Gültigkeiten von Datensätzen zurück, deren Organisations-ID mit der des Parameters übereinstimmt. Dieser Wert ist standardmäßig auf den Wert der `x-gw-ims-org-id`-Kopfzeilen festgelegt und wird ignoriert, es sei denn, die Anfrage liefert ein Service-Token. | `orgId=885737B25DC460C50A49411B@AdobeOrg` |
| `page` | Eine Ganzzahl, die angibt, welche Seite der Gültigkeitenliste zurückgegeben werden soll. | `page=3` |
| `sandboxName` | Gibt die Datensatzgültigkeiten wieder, deren Sandbox-Name genau mit dem Argument übereinstimmt. Die Standardeinstellung ist der Sandbox-Name in der `x-sandbox-name`-Kopfzeile der Anfrage. Verwenden Sie `sandboxName=*`, um Datensatzgültigkeiten aus allen Sandboxes einzuschließen. | `sandboxName=dev1` |
| `search` | Gibt die Gültigkeiten zurück, bei denen die angegebene Zeichenfolge der Gültigkeits-ID exakt entspricht oder **einem der folgenden Felder** enthalten) ist:<br><ul><li>Autor</li><li>Anzeigename</li><li>Beschreibung</li><li>Anzeigename</li><li>Datensatzname</li></ul> | `search=TESTING` |
| `status` | Eine durch Kommas getrennte Liste von Status. Wenn diese Liste enthalten ist, entspricht die Antwort den Datensatzgültigkeiten, deren aktueller Status in der Liste enthalten ist. | `status=pending,cancelled` |
| `ttlId` | Passt die Gültigkeitsanfrage an die angegebene ID an. | `ttlID=SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f` |
| `updatedDate` | Gibt die Gültigkeiten wieder, die im 24-Stunden-Fenster des angegebenen Datums aktualisiert wurden. | `2024-01-01` |
| `updatedToDate` / `updatedFromDate` | Gibt die Gültigkeiten wieder, die im 24-Stunden-Fenster aktualisiert wurden, beginnend mit dem angegebenen Zeitpunkt.<br><br>Eine Gültigkeit wird bei jeder Bearbeitung als aktualisiert erachtet, auch wenn sie erstellt, abgebrochen oder ausgeführt wird. | `updatedDate=2022-01-01` |

{style="table-layout:auto"}

