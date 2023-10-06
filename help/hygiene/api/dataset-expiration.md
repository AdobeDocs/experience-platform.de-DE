---
title: API-Endpunkt für Datensatzgültigkeiten
description: Mit dem Endpunkt /ttl in der Datenhygiene-API können Sie programmgesteuert einen Zeitplan für Datensatzgültigkeiten in Adobe Experience Platform festlegen.
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: 566f1b6478cd0de0691cfb2301d5b86fbbfece52
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 98%

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

Der in diesem Handbuch verwendete Endpunkt ist Teil der Data Hygiene API. Bevor Sie fortfahren, lesen Sie die [Übersicht](./overview.md) mit Links zur zugehörigen Dokumentation, einer Anleitung zum Lesen der API-Beispielaufrufe in diesem Dokument und wichtigen Informationen zu den Kopfzeilen, die für die erfolgreiche Ausführung von Aufrufen an eine Experience Platform-API erforderlich sind.

## Auflisten der Datensatzgültigkeiten {#list}

Sie können alle Datensatzgültigkeiten für Ihre Organisation auflisten, indem Sie eine GET-Anfrage stellen.

**API-Format**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| Parameter | Beschreibung |
| --- | --- |
| `{QUERY_PARAMETERS}` | Eine Liste optionaler Abfrageparameter mit mehreren durch `&`-Zeichen getrennten Parametern. Zu den gebräuchlichen Parametern gehören `size` und `page` für Paginierungszwecke. Eine vollständige Liste der unterstützten Abfrageparameter finden Sie im [Anhang](#query-params). |

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
  "totalRecords": 3,
  "ttlDetails": [
    {
      "status": "completed",
      "workorderId": "SDc17a9501345c4997878c1383c475a77b",
      "imsOrgId": "885737B25DC460C50A49411B@AdobeOrg",
      "datasetId": "f440ac301c414bf1b6ba419162866346",
      "expiry": "2021-07-07T13:14:15Z",
      "updatedAt": "2021-07-07T13:14:15Z",
      "updatedBy": "Jane Doe <jane.doe@example.com> d741b5b877bf47cf@AdobeId"
    },
    {
      "status": "pending",
      "workorderId": "SD8ef60b33dbed444fb81861cced5da10b",
      "imsOrgId": "885737B25DC460C50A49411B@AdobeOrg",
      "datasetId": "80f0d38820a74879a2c5be82e38b1a94",
      "expiry": "2099-02-02T00:00:00Z",
      "updatedAt": "2021-02-02T13:00:00Z",
      "updatedBy": "John Q. Public <jqp@example.com> 93220281bad34ed0@AdobeId"
    },
    {
      "status": "pending",
      "workorderId": "SD2140ad4eaf1f47a1b24c05cce53e303e",
      "imsOrgId": "885737B25DC460C50A49411B@AdobeOrg",
      "datasetId": "9e63f9b25896416ba811657678b4fcb7",
      "expiry": "2099-01-01T00:00:00Z",
      "updatedAt": "2021-01-01T13:00:00Z",
      "updatedBy": "Jane Doe <jane.doe@example.com> d741b5b877bf47cf@AdobeId"
    }
  ]
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `totalRecords` | Anzahl der Datensatzgültigkeiten, die den Parametern des Auflistungsaufrufs entsprechen. |
| `ttlDetails` | Enthält die Details der zurückgegebenen Datensatzgültigkeiten. Weitere Informationen zu den Eigenschaften einer Datensatzgültigkeit finden Sie im Antwort-Abschnitt zum Erstellen eines [Suchaufrufs](#lookup). |

{style="table-layout:auto"}

## Nachschlagen einer Datensatzgültigkeit {#lookup}

Sie können eine Datensatzgültigkeit über eine GET-Anfrage nachschlagen.

**API-Format**

```http
GET /ttl/{DATASET_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_ID}` | ID des Datensatzes, dessen Gültigkeit Sie nachschlagen möchten. |

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
    "workorderId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2023-12-31T23:59:59Z",
    "updatedAt": "2022-05-11T15:12:40.393115Z",
    "updatedBy": "{USER_ID}",
    "displayName": "Example Dataset Expiration Request",
    "description": "A dataset expiration request that will execute at the end of 2023"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `workorderId` | Die ID der Datensatzgültigkeit. |
| `datasetId` | Die ID des Datensatzes, für den diese Gültigkeit zutrifft. |
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

Sie können über eine PUT-Anfrage ein Ablaufdatum für einen Datensatz erstellen oder aktualisieren.

**API-Format**

```http
PUT /ttl/{DATASET_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_ID}` | Die ID des Datensatzes, für den Sie die Gültigkeit planen möchten. |

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
        "expiry": "2022-12-31T23:59:59Z",
        "displayName": "Example Expiration Request",
        "description": "Cleanup identities required by JIRA request 12345 across all datasets in the prod sandbox."
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `expiry` | Ein ISO 8601-Zeitstempel für den Zeitpunkt, zu dem der Datensatz gelöscht wird. |
| `displayName` | Ein Anzeigename für die Anfrage zur Gültigkeit. |
| `description` | Eine optionale Beschreibung für die Anfrage zur Gültigkeit. |

{style="table-layout:auto"}

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Datensatzgültigkeit mit dem HTTP-Status 200 (OK) zurück, wenn eine bereits vorhandene Gültigkeit aktualisiert wurde, oder 201 (Erstellt), wenn keine Gültigkeit vorhanden war.

```json
{
    "workorderId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "5b020a27e7040801dedbf46e",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2032-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T22:38:40.393115Z",
    "updatedBy": "{USER_ID}",
    "displayName": "Example Expiration Request",
    "description": "Cleanup identities required by JIRA request 12345 across all datasets in the prod sandbox."
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `workorderId` | Die ID der Datensatzgültigkeit. |
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
| `{EXPIRATION_ID}` | Die `workorderId` der Datensatzgültigkeit, die Sie abbrechen möchten. |

{style="table-layout:auto"}

**Anfrage**

Mit der folgenden Anfrage wird die Gültigkeit eines Datensatzes mit der ID `SD5cfd7a11b25543a9bcd9ef647db3d8df` abgebrochen:

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/SD5cfd7a11b25543a9bcd9ef647db3d8df \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) zurück und das Attribut `status` der Gültigkeit wird auf `cancelled` gesetzt.

## Gültigkeitsstatus-Verlauf eines Datensatzes abrufen

Sie können das Gültigkeitsstatus-Protokoll eines spezifischen Datensatzes mithilfe des Abfrageparameters `include=history` in einer Suchanfrage aufrufen. Das Ergebnis enthält Informationen über die Erstellung der Datensatzgültigkeit, alle Aktualisierungen sowie über ihren Abbruch oder ihre Ausführung (falls zutreffend).

**API-Format**

```http
GET /ttl/{DATASET_ID}?include=history
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_ID}` | ID des Datensatzes, dessen Gültigkeitsprotokoll Sie aufrufen möchten. |

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
  "workorderId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
  "datasetId": "62759f2ede9e601b63a2ee14",
  "datasetName": "Example Dataset",
  "sandboxName": "prod",
  "displayName": "Expiration Request 123",
  "description": "Expiration Request 123 Description",
  "imsOrg": "{ORG_ID}",
  "status": "cancelled",
  "expiry": "2022-05-09T23:47:30.071186Z",
  "updatedAt": "2022-05-09T23:47:30.071186Z",
  "updatedBy": "{USER_ID}",
  "history": [
    {
      "status": "created",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:38:40.393115Z",
      "updatedBy": "{USER_ID}"
    },
    {
      "status": "updated",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:41:46.731002Z",
      "updatedBy": "{USER_ID}"
    },
    {
      "status": "cancelled",
      "expiry": "2022-05-09T23:47:30.071186Z",
      "updatedAt": "2022-05-09T23:47:30.071186Z",
      "updatedBy": "{USER_ID}"
    }
  ]
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `workorderId` | Die ID der Datensatzgültigkeit. |
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

| Parameter | Beschreibung | Beispiel |
| --- | --- | --- |
| `size` | Eine Ganzzahl zwischen 1 und 100, die die maximale Anzahl der zurückzugebenden Gültigkeiten angibt. Die Standardeinstellung ist 25. | `size=50` |
| `page` | Eine Ganzzahl, die angibt, welche Seite der Gültigkeitenliste zurückgegeben werden soll. | `page=3` |
| `orgId` | Gibt die Gültigkeiten von Datensätzen zurück, deren Organisations-ID mit der des Parameters übereinstimmt. Dieser Wert ist standardmäßig auf den Wert der `x-gw-ims-org-id`-Kopfzeilen festgelegt und wird ignoriert, es sei denn, die Anfrage liefert ein Service-Token. | `orgId=885737B25DC460C50A49411B@AdobeOrg` |
| `status` | Eine durch Kommas getrennte Liste von Status. Wenn diese Liste enthalten ist, entspricht die Antwort den Datensatzgültigkeiten, deren aktueller Status in der Liste enthalten ist. | `status=pending,cancelled` |
| `author` | Gibt die Gültigkeiten zurück, für die `created_by` der Suchzeichenfolge entspricht. Wenn die Suchzeichenfolge mit `LIKE` oder `NOT LIKE` beginnt, wird der Rest als SQL-Suchmuster behandelt. Andernfalls wird die gesamte Suchzeichenfolge als exakte Zeichenfolge gehandhabt, die genau mit dem gesamten Inhalt des `created_by`-Felds übereinstimmen muss. | `author=LIKE %john%` |
| `sandboxName` | Gibt die Datensatzgültigkeiten wieder, deren Sandbox-Name genau mit dem Argument übereinstimmt. Die Standardeinstellung ist der Sandbox-Name in der `x-sandbox-name`-Kopfzeile der Anfrage. Verwenden Sie `sandboxName=*`, um Datensatzgültigkeiten aus allen Sandboxes einzuschließen. | `sandboxName=dev1` |
| `datasetId` | Gibt die Gültigkeiten wieder, die für einen bestimmten Datensatz gelten. | `datasetId=62b3925ff20f8e1b990a7434` |
| `createdDate` | Gibt die Gültigkeiten zurück, die im 24-Stunden-Fenster erstellt wurden, das mit dem angegebenen Zeitpunkt beginnt.<br><br>Beachten Sie, dass ein Datum ohne Uhrzeit (wie `2021-12-07`) den Datum/Uhrzeit-Wert am Anfang des Tages darstellt. Daher bezieht sich `createdDate=2021-12-07` auf alle am 7. Dezember 2021 erstellten Gültigkeiten, von `00:00:00` bis `23:59:59.999999999` (UTC). | `createdDate=2021-12-07` |
| `createdFromDate` | Gibt die Gültigkeiten wieder, die zum angegebenen Zeitpunkt oder danach erstellt wurden. | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | Gibt die Gültigkeiten wieder, die zum angegebenen Zeitpunkt oder davor erstellt wurden. | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | Wie `createdDate` / `createdFromDate` / `createdToDate`, jedoch wird die Aktualisierungszeit einer Datensatzgültigkeit anstelle der Erstellungszeit herangezogen.<br><br>Eine Gültigkeit wird bei jeder Bearbeitung als aktualisiert erachtet, auch wenn sie erstellt, abgebrochen oder ausgeführt wird. | `updatedDate=2022-01-01` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | Gibt die Gültigkeiten wieder, die zu einem beliebigen Zeitpunkt im angegebenen Intervall abgebrochen wurden. Dies gilt auch dann, wenn die Gültigkeit später erneut erstellt wurde (durch Festlegen eines neuen Ablaufdatums für denselben Datensatz). | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | Gibt die Gültigkeiten wieder, die im angegebenen Intervall ausgeführt wurden. | `completedToDate=2021-11-11-06:00` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | Gibt die Gültigkeiten wieder, die im angegebenen Intervall ausgeführt werden sollen oder bereits ausgeführt wurden. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |

{style="table-layout:auto"}
