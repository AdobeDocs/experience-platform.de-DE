---
title: API-Endpunkt für Datensatzgültigkeiten
description: Mit dem Endpunkt /ttl in der Datenhygiene-API können Sie programmgesteuert einen Zeitplan für Datensatzgültigkeiten in Adobe Experience Platform festlegen.
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: a954059155857e6dde7884cf413561cd5214d9bb
workflow-type: tm+mt
source-wordcount: '1714'
ht-degree: 78%

---

# Endpunkt der Datensatzgültigkeit

Der `/ttl`-Endpunkt in der Datenhygiene-API ermöglicht Ihnen, in Adobe Experience Platform Ablaufdaten für Datensätze zu planen.

Eine Datensatzgültigkeit ist nur ein zeitverzögerter Löschvorgang. Der Datensatz ist in der Zwischenzeit nicht geschützt und kann daher auf andere Weise gelöscht werden, bevor sein Ablaufdatum erreicht wurde.

>[!NOTE]
>
>Obwohl die Löschung als spezifischer Zeitpunkt angegeben ist, kann es bis zu 24 Stunden nach Ablauf der Frist dauern, bevor die eigentliche Löschung eingeleitet wird. Nachdem der Löschvorgang gestartet wurde, kann es bis zu sieben Tage dauern, bis alle Spuren des Datensatzes aus Platform-Systemen entfernt wurden.

Sie können die Gültigkeit jederzeit abbrechen oder den Löschzeitpunkt ändern, solange der Datensatz-Löschvorgang noch nicht gestartet wurde. Nachdem Sie eine Datensatzgültigkeit abgebrochen haben, können Sie sie erneut starten, indem Sie ein neues Ablaufdatum festlegen.

Sobald das Löschen des Datensatzes gestartet wurde, wird seine Gültigkeit als `executing` gekennzeichnet und darf nicht weiter geändert werden. Der Datensatz selbst kann bis zu sieben Tage lang wiederhergestellt werden, jedoch nur durch einen manuellen Prozess über eine Adobe-Service-Anfrage. Während die Anfrage ausgeführt wird, beginnen der Data Lake, der Identity Service und das Echtzeit-Kundenprofil separate Prozesse, um den Inhalt des Datensatzes aus den entsprechenden Diensten zu entfernen. Sobald die Daten aus allen drei Services gelöscht wurden, wird der Ablauf als `executed` gekennzeichnet.

>[!WARNING]
>
>Wenn ein Datensatz ausläuft, müssen alle Datenflüsse, die Daten in diesen Datensatz einspeisen, manuell geändert werden, damit Ihre nachgeschalteten Workflows nicht beeinträchtigt werden.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der Data Hygiene API. Bevor Sie fortfahren, lesen Sie bitte die [API-Handbuch](./overview.md) Informationen zu erforderlichen Kopfzeilen für CRUD-Vorgänge, Fehlermeldungen, Postman-Sammlungen und zum Lesen von Beispiel-API-Aufrufen.

>[!IMPORTANT]
>
>Bei Aufrufen der Data Hygiene API müssen Sie den -H verwenden `x-sandbox-name: {SANDBOX_NAME}` -Kopfzeile.

## Auflisten der Datensatzgültigkeiten {#list}

Sie können alle Datensatzgültigkeiten für Ihre Organisation auflisten, indem Sie eine GET-Anfrage stellen. Mithilfe von Abfrageparametern kann die Antwort nach geeigneten Ergebnissen gefiltert werden.

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
  https://platform.adobe.io/data/core/hygiene/ttl?updatedToDate=2021-08-01&author=LIKE%Jane Doe%25 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort listet die resultierenden Datensatzgültigkeiten auf. Das folgende Beispiel wurde aus Platzgründen gekürzt.

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
| `totalRecords` | Anzahl der Datensatzgültigkeiten, die den Parametern des Auflistungsaufrufs entsprechen. |
| `ttlDetails` | Enthält die Details der zurückgegebenen Datensatzgültigkeiten. Weitere Informationen zu den Eigenschaften einer Datensatzgültigkeit finden Sie im Antwort-Abschnitt zum Erstellen eines [Suchaufrufs](#lookup). |

{style="table-layout:auto"}

## Nachschlagen einer Datensatzgültigkeit {#lookup}

Um nach dem Ablauf eines Datensatzes zu suchen, stellen Sie eine GET-Anfrage mit der `datasetId` oder `ttlId`.

**API-Format**

```http
GET /ttl/{DATASET_ID}?include=history
GET /ttl/{TTL_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_ID}` | ID des Datensatzes, dessen Gültigkeit Sie nachschlagen möchten. |
| `{TTL_ID}` | Die ID der Datensatzgültigkeit. |

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

<!-- Is there a different response from making a GET request to either '/ttl/{DATASET_ID}?include=history' or '/ttl/{TTL_ID}'? If so please can you provide the response for both (or just the ttl endpoint itf it differs from teh example) -->

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

## Datensatzgültigkeit erstellen bzw. aktualisieren {#create-or-update}

Erstellen oder aktualisieren Sie über eine PUT-Anfrage ein Ablaufdatum für einen Datensatz. Die PUT-Anfrage verwendet entweder die `datasetId` oder `ttlId`.

**API-Format**

```http
PUT /ttl/{DATASET_ID}
PUT /ttl/{TTL_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_ID}` | Die ID des Datensatzes, für den Sie die Gültigkeit planen möchten. |
| `{TTL_ID}` | Die ID der Datensatzgültigkeit. |

**Anfrage**

Mit der folgenden Anfrage wird als Zeitpunkt für die Löschung des Datensatzes `5b020a27e7040801dedbf46e` Ende 2022 festgelegt (Greenwich Mean Time). Wenn für den Datensatz keine vorhandene Gültigkeit gefunden wird, wird eine neue erstellt. Wenn der Datensatz bereits eine ausstehende Gültigkeit aufweist, wird diese mit dem neuen `expiry`-Wert aktualisiert.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
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
| `expiry` | Datum und Uhrzeit im ISO 8601-Format. Wenn die Zeichenfolge keinen expliziten Zeitzonenversatz hat, wird als Zeitzone UTC angenommen. Die Lebensdauer der Daten im System wird entsprechend dem angegebenen Ablaufwert festgelegt. Jeder vorherige Ablaufzeitstempel für denselben Datensatz wird durch den von Ihnen angegebenen neuen Ablaufwert ersetzt. |
| `displayName` | Ein Anzeigename für die Anfrage zur Gültigkeit. |
| `description` | Eine optionale Beschreibung für die Anfrage zur Gültigkeit. |

{style="table-layout:auto"}

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Datensatzgültigkeit mit dem HTTP-Status 200 (OK) zurück, wenn eine bereits vorhandene Gültigkeit aktualisiert wurde, oder 201 (Erstellt), wenn keine Gültigkeit vorhanden war.

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

## Gültigkeitsstatus-Verlauf eines Datensatzes abrufen {#retrieve-expiration-history}

Sie können das Gültigkeitsstatus-Protokoll eines spezifischen Datensatzes mithilfe des Abfrageparameters `include=history` in einer Suchanfrage aufrufen. Das Ergebnis enthält Informationen über die Erstellung der Datensatzgültigkeit, alle Aktualisierungen sowie über ihren Abbruch oder ihre Ausführung (falls zutreffend). Sie können auch die `ttlId` des Datensatzablaufs.

**API-Format**

```http
GET /ttl/{DATASET_ID}?include=history
GET /ttl/{TTL_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_ID}` | ID des Datensatzes, dessen Gültigkeitsprotokoll Sie aufrufen möchten. |
| `{TTL_ID}` | Die ID der Datensatzgültigkeit. |

{style="table-layout:auto"}

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/62759f2ede9e601b63a2ee14?include=history \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort geben die Details der Datensatzgültigkeit mit einem `history`-Array zurück, das die Details der Attribute `status`, `expiry`, `updatedAt` und `updatedBy` für jede der aufgezeichneten Aktualisierungen angibt.

```json
{
  "ttlId": "SD-b16c8b48-a15a-45c8-9215-587ea89369bf",
  "datasetId": "62759f2ede9e601b63a2ee14",
  "datasetName": "Example Dataset",
  "sandboxName": "prod",
  "displayName": "Expiration Request 123",
  "description": "Expiration Request 123 Description",
  "imsOrg": "0FCC747E56F59C747F000101@AdobeOrg",
  "status": "cancelled",
  "expiry": "2022-05-09T23:47:30.071186Z",
  "updatedAt": "2022-05-09T23:47:30.071186Z",
  "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
  "history": [
    {
      "status": "created",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:38:40.393115Z",
      "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e"
    },
    {
      "status": "updated",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:41:46.731002Z",
      "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e"
    },
    {
      "status": "cancelled",
      "expiry": "2022-05-09T23:47:30.071186Z",
      "updatedAt": "2022-05-09T23:47:30.071186Z",
      "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e"
    }
  ]
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `ttlId` | Die ID der Datensatzgültigkeit. |
| `datasetId` | Die ID des Datensatzes, für den diese Gültigkeit zutrifft. |
| `datasetName` | Anzeigename für den Datensatz, für den diese Gültigkeit zutrifft. |
| `sandboxName` | Name der Sandbox, unter dem der Zieldatensatz zu finden ist. |
| `displayName` | Der Anzeigename für die Anfrage zur Gültigkeit. |
| `description` | Eine Beschreibung für die Anfrage zur Gültigkeit. |
| `imsOrg` | Die Kennung Ihrer Organisation. |
| `history` | Listet das Protokoll der Aktualisierungen für die Gültigkeit als Array von Objekten auf, wobei jedes Objekt die Attribute `status`, `expiry`, `updatedAt` und `updatedBy` für die Gültigkeit zum Zeitpunkt der Aktualisierung enthält. |

{style="table-layout:auto"}

## Anhang

### Akzeptierte Abfrageparameter {#query-params}

In der folgenden Tabelle sind die verfügbaren Abfrageparameter beim [Auflisten von Datensatzgültigkeiten](#list) aufgeführt:

>[!NOTE]
>
>Die `description`, `displayName`, und `datasetName` -Parameter enthalten alle die Möglichkeit, nach LIKE-Werten zu suchen. Das bedeutet, dass Sie geplante Datensatzabläufe namens &quot;Name123&quot;, &quot;Name183&quot;, &quot;DisplayName1234&quot;finden können, indem Sie nach der Zeichenfolge &quot;Name1&quot;suchen.

| Parameter | Beschreibung | Beispiel |
| --- | --- | --- |
| `author` | Gibt die Gültigkeiten zurück, für die `created_by` der Suchzeichenfolge entspricht. Wenn die Suchzeichenfolge mit `LIKE` oder `NOT LIKE` beginnt, wird der Rest als SQL-Suchmuster behandelt. Andernfalls wird die gesamte Suchzeichenfolge als exakte Zeichenfolge gehandhabt, die genau mit dem gesamten Inhalt des `created_by`-Felds übereinstimmen muss. | `author=LIKE %john%`, `author=John Q. Public` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | Gibt die Gültigkeiten wieder, die zu einem beliebigen Zeitpunkt im angegebenen Intervall abgebrochen wurden. Dies gilt auch dann, wenn die Gültigkeit später erneut erstellt wurde (durch Festlegen eines neuen Ablaufdatums für denselben Datensatz). | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | Gibt die Gültigkeiten wieder, die im angegebenen Intervall ausgeführt wurden. | `completedToDate=2021-11-11-06:00` |
| `createdDate` | Gibt die Gültigkeiten zurück, die im 24-Stunden-Fenster erstellt wurden, das mit dem angegebenen Zeitpunkt beginnt.<br><br>Beachten Sie, dass ein Datum ohne Uhrzeit (wie `2021-12-07`) den Datum/Uhrzeit-Wert am Anfang des Tages darstellt. Daher bezieht sich `createdDate=2021-12-07` auf alle am 7. Dezember 2021 erstellten Gültigkeiten, von `00:00:00` bis `23:59:59.999999999` (UTC). | `createdDate=2021-12-07` |
| `createdFromDate` | Gibt die Gültigkeiten wieder, die zum angegebenen Zeitpunkt oder danach erstellt wurden. | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | Gibt die Gültigkeiten wieder, die zum angegebenen Zeitpunkt oder davor erstellt wurden. | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `datasetId` | Gibt die Gültigkeiten wieder, die für einen bestimmten Datensatz gelten. | `datasetId=62b3925ff20f8e1b990a7434` |
| `datasetName` | Sucht nach Abläufen, deren Datensatzname die angegebene Suchzeichenfolge enthält. Bei der Übereinstimmung wird nicht zwischen Groß- und Kleinschreibung unterschieden. | `datasetName=Acme` |
| `description` |   | `description=Handle expiration of Acme information through the end of 2024.` |
| `displayName` | Sucht nach Ablauf, dessen Anzeigename die angegebene Suchzeichenfolge enthält. Bei der Übereinstimmung wird nicht zwischen Groß- und Kleinschreibung unterschieden. | `displayName=License Expiry` |
| `executedDate` / `executedFromDate` / `executedToDate` | Filtert Ergebnisse anhand eines exakten Ausführungsdatums, eines Enddatums für die Ausführung oder eines Anfangsdatums für die Ausführung. Sie werden zum Abrufen von Daten oder Datensätzen verwendet, die mit der Ausführung eines Vorgangs an einem bestimmten Datum, vor einem bestimmten Datum oder nach einem bestimmten Datum verknüpft sind. | `executedDate=2023-02-05T19:34:40.383615Z` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | Gibt die Gültigkeiten wieder, die im angegebenen Intervall ausgeführt werden sollen oder bereits ausgeführt wurden. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |
| `limit` | Eine Ganzzahl zwischen 1 und 100, die die maximale Anzahl der zurückzugebenden Gültigkeiten angibt. Die Standardeinstellung ist 25. | `limit=50` |
| `orderBy` | Die `orderBy` -Abfrageparameter gibt die Sortierreihenfolge der von der API zurückgegebenen Ergebnisse an. Verwenden Sie sie, um die Daten basierend auf einem oder mehreren Feldern anzuordnen, entweder in aufsteigender (ASC) oder in absteigender (DESC) Reihenfolge. Verwenden Sie das Präfix + oder - , um ASC bzw. DESC anzugeben. Folgende Werte werden akzeptiert: `displayName`, `description`, `datasetName`, `id`, `updatedBy`, `updatedAt`, `expiry`, `status`. | `-datasetName` |
| `orgId` | Gibt die Gültigkeiten von Datensätzen zurück, deren Organisations-ID mit der des Parameters übereinstimmt. Dieser Wert ist standardmäßig auf den Wert der `x-gw-ims-org-id`-Kopfzeilen festgelegt und wird ignoriert, es sei denn, die Anfrage liefert ein Service-Token. | `orgId=885737B25DC460C50A49411B@AdobeOrg` |
| `page` | Eine Ganzzahl, die angibt, welche Seite der Gültigkeitenliste zurückgegeben werden soll. | `page=3` |
| `sandboxName` | Gibt die Datensatzgültigkeiten wieder, deren Sandbox-Name genau mit dem Argument übereinstimmt. Die Standardeinstellung ist der Sandbox-Name in der `x-sandbox-name`-Kopfzeile der Anfrage. Verwenden Sie `sandboxName=*`, um Datensatzgültigkeiten aus allen Sandboxes einzuschließen. | `sandboxName=dev1` |
| `search` | Sucht nach Abläufen, bei denen die angegebene Zeichenfolge eine exakte Übereinstimmung mit der Ablaufüberkennung ist oder **enthalten** in einem dieser Felder:<br><ul><li>author</li><li>Anzeigename</li><li>Beschreibung</li><li>Anzeigename</li><li>Datensatzname</li></ul> | `search=TESTING` |
| `status` | Eine durch Kommas getrennte Liste von Status. Wenn diese Liste enthalten ist, entspricht die Antwort den Datensatzgültigkeiten, deren aktueller Status in der Liste enthalten ist. | `status=pending,cancelled` |
| `ttlId` | Entspricht der Ablaufanfrage der angegebenen ID. | `ttlID=SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | Wie `createdDate` / `createdFromDate` / `createdToDate`, jedoch wird die Aktualisierungszeit einer Datensatzgültigkeit anstelle der Erstellungszeit herangezogen.<br><br>Eine Gültigkeit wird bei jeder Bearbeitung als aktualisiert erachtet, auch wenn sie erstellt, abgebrochen oder ausgeführt wird. | `updatedDate=2022-01-01` |

{style="table-layout:auto"}
