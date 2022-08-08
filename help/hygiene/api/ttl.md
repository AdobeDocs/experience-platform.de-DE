---
title: Endpunkt der Datensatz-TTL-API (Time-to-Live)
description: Mit dem Endpunkt /ttl in der Data Hygiene API können Sie programmgesteuert einen Zeitplan für Datensatz-TTLs in Adobe Experience Platform festlegen.
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: 7f1e4bdf54314cab1f69619bcbb34216da94b17e
workflow-type: ht
source-wordcount: '1313'
ht-degree: 100%

---

# Datensatz-TTL-Endpunkt (Time-to-Live)

>[!IMPORTANT]
>
>Die Datenhygiene-Funktionen in Adobe Experience Platform sind derzeit nur für Organisationen verfügbar, die Healthcare Shield erworben haben.

Der `/ttl`-Endpunkt in der Data Hygiene API ermöglicht Ihnen, in Adobe Experience Platform einen Zeitplan für TTL-Protokolle für Datensätze festzulegen.

Eine Datensatz-TTL ist ein zeitverzögerter Löschvorgang. Der Datensatz ist in der Zwischenzeit nicht geschützt und kann daher auf andere Weise gelöscht werden, bevor sein Ablaufdatum erreicht wurde.

>[!NOTE]
>
>Obwohl die Löschung als spezifischer Zeitpunkt angegeben ist, kann es bis zu 24 Stunden nach Ablauf der Frist dauern, bevor die eigentliche Löschung eingeleitet wird. Nachdem der Löschvorgang gestartet wurde, kann es bis zu sieben Tage dauern, bis alle Spuren des Datensatzes aus Platform-Systemen entfernt wurden.

Sie können die TTL jederzeit abbrechen oder den Löschzeitpunkt ändern, solange der Datensatz-Löschvorgang noch nicht gestartet wurde. Nachdem Sie einen TTL-Vorgang abgebrochen haben, können Sie ihn erneut starten, indem Sie ein neues Ablaufdatum festlegen.

Sobald das Löschen des Datensatzes gestartet wurde, wird seine TTL als `executing` gekennzeichnet und darf nicht weiter geändert werden. Der Datensatz selbst kann bis zu sieben Tage lang wiederhergestellt werden, jedoch nur durch einen manuellen Prozess über eine Adobe-Service-Anfrage.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der Data Hygiene API. Bevor Sie fortfahren, lesen Sie die [Übersicht](./overview.md) mit Links zur zugehörigen Dokumentation, einer Anleitung zum Lesen der API-Beispielaufrufe in diesem Dokument und wichtigen Informationen zu den Kopfzeilen, die für die erfolgreiche Ausführung von Aufrufen an eine Experience Platform-API erforderlich sind.

## Auflisten der Datensatz-TTLs {#list}

Sie können alle Datensatz-TTLs für Ihre Organisation auflisten, indem Sie eine GET-Anfrage stellen.

**API-Format**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| Parameter | Beschreibung |
| --- | --- |
| `{QUERY_PARAMETERS}` | Eine Liste optionaler Abfrageparameter mit mehreren durch `&`-Zeichen getrennten Parametern. Zu den gebräuchlichen Parametern gehören `size` und `page` für Paginierungszwecke. Eine vollständige Liste der unterstützten Abfrageparameter finden Sie im [Anhang](#query-params). |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl?page=1&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort listet die resultierenden TTLs auf. Das folgende Beispiel wurde aus Platzgründen gekürzt.

```json
{
  "results": [
    {
      "ttlId": "SDfba908e9fb2e427ab4275d20465631d7",
      "datasetId": "62799c3e1151781b63ccaa28",
      "imsOrg": "{ORG_ID}",
      "status": "cancelled",
      "expiry": "2022-05-09T22:57:05.531024Z",
      "updatedAt": "2022-05-09T22:57:05.531025Z",
      "updatedBy": "{USER_ID}"
    },
    {
      "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
      "datasetId": "62759f2ede9e601b63a2ee14",
      "imsOrg": "{ORG_ID}",
      "status": "pending",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:41:46.731002Z",
      "updatedBy": "{USER_ID}"
    }
  ],
  "current_page": 1,
  "total_pages": 36,
  "total_count": 886
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `results` | Enthält die Details der zurückgegebenen TTLs. Weitere Informationen zu den Eigenschaften einer TTL-Entität finden Sie im Antwort-Abschnitt zum Erstellen eines [Suchaufrufs](#lookup). |
| `current_page` | Die aktuelle Seite der aufgelisteten Ergebnisse. |
| `total_pages` | Die Gesamtzahl der Seiten in der Antwort. |
| `total_count` | Die Gesamtzahl der TTL-Entitäten in der Antwort. |

{style=&quot;table-layout:auto&quot;}

## Suchen einer TTL {#lookup}

Sie können eine Datensatz-TTL über eine GET-Anfrage suchen.

**API-Format**

```http
GET /ttl/{TTL_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{TTL_ID}` | Die ID der TTL, die Sie suchen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der TTL zurück.

```json
{
    "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2023-12-31T23:59:59Z",
    "updatedAt": "2022-05-11T15:12:40.393115Z",
    "updatedBy": "{USER_ID}"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `ttlId` | Die ID der Datensatz-TTL. |
| `datasetId` | Die ID des Datensatzes, für den diese TTL gilt. |
| `imsOrg` | Die Kennung Ihres Unternehmens. |
| `status` | Der aktuelle Status der TTL. |
| `expiry` | Das geplante Datum und die Uhrzeit, zu der der Datensatz gelöscht wird. |
| `updatedAt` | Ein Zeitstempel, der angibt, wann die TTL zuletzt aktualisiert wurde. |
| `updatedBy` | Der Benutzer, der die TTL zuletzt aktualisiert hat. |

{style=&quot;table-layout:auto&quot;}

## Erstellen einer TTL {#create}

Sie können eine TTL für einen Datensatz über eine POST-Anfrage hinzufügen.

**API-Format**

```http
POST /ttl
```

**Anfrage**

Mit der folgenden Anfrage wird als Zeitpunkt für die Löschung des Datensatzes `5b020a27e7040801dedbf46e` Ende 2022 festgelegt (Greenwich Mean Time).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/ttl \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "datasetId": "5b020a27e7040801dedbf46e",
        "expiry": "2022-12-31T23:59:59Z"
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `datasetId` | Die ID des Datensatzes, für den Sie eine TTL planen möchten. |
| `expiry` | Ein ISO 8601-Zeitstempel für den Zeitpunkt, zu dem der Datensatz gelöscht wird. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die Details der TTL mit dem HTTP-Status 200 (OK) zurück, wenn eine bereits vorhandene TTL aktualisiert wurde, oder 201 (Erstellt), wenn keine TTL vorhanden war.

```json
{
    "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "5b020a27e7040801dedbf46e",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2032-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T22:38:40.393115Z",
    "updatedBy": "{USER_ID}"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `ttlId` | Die ID der Datensatz-TTL. |
| `datasetId` | Die ID des Datensatzes, für den diese TTL gilt. |
| `imsOrg` | Die Kennung Ihres Unternehmens. |
| `status` | Der aktuelle Status der TTL. |
| `expiry` | Das geplante Datum und die Uhrzeit, zu der der Datensatz gelöscht wird. |
| `updatedAt` | Ein Zeitstempel, der angibt, wann die TTL zuletzt aktualisiert wurde. |
| `updatedBy` | Der Benutzer, der die TTL zuletzt aktualisiert hat. |

{style=&quot;table-layout:auto&quot;}

## Aktualisieren einer TTL {#update}

Sie können eine TTL für einen Datensatz über eine PUT-Anfrage aktualisieren.

**API-Format**

```http
PUT /ttl/{TTL_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{TTL_ID}` | Die ID der TTL, die Sie ändern möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Mit der folgenden Anfrage wird die TTL für den Datensatz `5b020a27e7040801dedbf46e` aktualisiert, sodass sie Ende 2023 gelöscht wird (Greenwich Mean Time).

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "expiry": "2023-12-31T23:59:59Z"
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `expiry` | Ein ISO 8601-Zeitstempel für den Zeitpunkt, zu dem der Datensatz gelöscht wird. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die Details der aktualisierten TTL zurück.

```json
{
    "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2023-12-31T23:59:59Z",
    "updatedAt": "2022-05-11T15:12:40.393115Z",
    "updatedBy": "{USER_ID}"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `ttlId` | Die ID der Datensatz-TTL. |
| `datasetId` | Die ID des Datensatzes, für den diese TTL gilt. |
| `imsOrg` | Die Kennung Ihres Unternehmens. |
| `status` | Der aktuelle Status der TTL. |
| `expiry` | Das geplante Datum und die Uhrzeit, zu der der Datensatz gelöscht wird. |
| `updatedAt` | Ein Zeitstempel, der angibt, wann die TTL zuletzt aktualisiert wurde. |
| `updatedBy` | Der Benutzer, der die TTL zuletzt aktualisiert hat. |

{style=&quot;table-layout:auto&quot;}

## Abbrechen einer TTL {#delete}

Sie können eine TTL abbrechen, indem Sie eine DELETE-Anfrage stellen.

**API-Format**

```http
DELETE /ttl/{TTL_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{TTL_ID}` | Die ID der TTL, die Sie abbrechen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Mit der folgenden Anfrage wird die TTL für den Datensatz `5b020a27e7040801dedbf46e` aktualisiert, sodass sie Ende 2023 gelöscht wird (Greenwich Mean Time).

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der TTL zurück, wobei das `status`-Attribut jetzt `cancelled` lautet.

```json
{
    "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "imsOrg": "{ORG_ID}",
    "status": "cancelled",
    "expiry": "2023-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T23:47:30.071186Z",
    "updatedBy": "{USER_ID}"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `ttlId` | Die ID der Datensatz-TTL. |
| `datasetId` | Die ID des Datensatzes, für den diese TTL gilt. |
| `imsOrg` | Die Kennung Ihres Unternehmens. |
| `status` | Der aktuelle Status der TTL. |
| `expiry` | Das geplante Datum und die Uhrzeit, zu der der Datensatz gelöscht wird. |
| `updatedAt` | Ein Zeitstempel, der angibt, wann die TTL zuletzt aktualisiert wurde. |
| `updatedBy` | Der Benutzer, der die TTL zuletzt aktualisiert hat. |

{style=&quot;table-layout:auto&quot;}

## Abrufen des TTL-Verlaufs

Sie können den Verlauf einer TTL in einer Suchanfrage mithilfe des Abfrageparameters `include=history` aufrufen. Das Ergebnis enthält Informationen über die Erstellung der TTL, alle Aktualisierungen sowie über ihren Abbruch oder ihre Ausführung (falls zutreffend).

**API-Format**

```http
GET /ttl/{TTL_ID}?include=history
```

| Parameter | Beschreibung |
| --- | --- |
| `{TTL_ID}` | Die ID der TTL, deren Verlauf Sie aufrufen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e?include=history \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der TTL mit einem `history`-Array zurück, das die Details der Attribute `status`, `expiry`, `updatedAt` und `updatedBy` für jede der aufgezeichneten Aktualisierungen angibt.

```json
{
  "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
  "datasetId": "62759f2ede9e601b63a2ee14",
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
| `ttlId` | Die ID der Datensatz-TTL. |
| `datasetId` | Die ID des Datensatzes, für den diese TTL gilt. |
| `imsOrg` | Die Kennung Ihres Unternehmens. |
| `history` | Listet den Verlauf der Aktualisierungen für die TTL als Array von Objekten auf, wobei jedes Objekt die Attribute `status`, `expiry`, `updatedAt` und `updatedBy` für die TTL zum Zeitpunkt der Aktualisierung enthält. |

{style=&quot;table-layout:auto&quot;}

## Anhang

### Akzeptierte Abfrageparameter {#query-params}

In der folgenden Tabelle sind die verfügbaren Abfrageparameter beim [Auflisten von Datensatz-TTLs](#list) aufgeführt:

| Parameter | Beschreibung | Beispiel |
| --- | --- | --- |
| `size` | Eine Ganzzahl zwischen 1 und 100, die die maximale Anzahl der zurückzugebenden TTLs angibt. Die Standardeinstellung ist 25. | `size=50` |
| `page` | Eine Ganzzahl, die angibt, welche Seite von TTLs zurückgegeben werden soll. | `page=3` |
| `status` | Eine durch Kommas getrennte Liste von Status. Wenn dieser Parameter enthalten ist, werden in der Antwort die TTLs zurückgegeben, deren aktueller Status aufgelistet ist. | `status=pending,cancelled` |
| `author` | Sucht TTLs, deren `created_by` der Suchzeichenfolge entspricht. Wenn die Suchzeichenfolge mit `LIKE` oder `NOT LIKE` beginnt, wird der Rest als SQL-Suchmuster behandelt. Andernfalls wird die gesamte Suchzeichenfolge als exakte Zeichenfolge gehandhabt, die genau mit dem gesamten Inhalt des `created_by`-Felds übereinstimmen muss. | `author=LIKE %john%` |
| `createdDate` | Sucht nach TTLs, die im 24-Stunden-Fenster erstellt wurden, beginnend mit dem angegebenen Zeitpunkt.<br><br>Beachten Sie, dass ein Datum ohne Uhrzeit (wie `2021-12-07`) den Datum/Uhrzeit-Wert am Anfang des Tages darstellt. Daher bezieht sich `createdDate=2021-12-07` auf alle am 7. Dezember 2021 erstellten TTLs, von `00:00:00` bis `23:59:59.999999999` (UTC). | `createdDate=2021-12-07` |
| `createdFromDate` | Sucht TTLs, die zum angegebenen Zeitpunkt oder danach erstellt wurden. | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | Sucht TTLs, die zum angegebenen Zeitpunkt oder davor erstellt wurden. | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | Wie `createdDate` / `createdFromDate` / `createdToDate`, jedoch wird die Aktualisierungszeit einer TTL anstelle der Erstellungszeit herangezogen.<br><br>Eine TTL wird bei jeder Bearbeitung als aktualisiert erachtet, auch wenn sie erstellt, abgebrochen oder ausgeführt wird. | `updatedDate=2022-01-01` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | Sucht nach TTLs, die zu einem beliebigen Zeitpunkt im angegebenen Intervall abgebrochen wurden. Dies gilt auch dann, wenn die TTL später erneut erstellt wurde (durch Festlegen eines neuen Ablaufdatums für denselben Datensatz). | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | Sucht nach TTLs, die im angegebenen Intervall ausgeführt wurden. | `completedToDate=2021-11-11-06:00` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | Sucht nach TTLs, die im angegebenen Intervall ausgeführt werden sollen oder bereits ausgeführt wurden. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |

{style=&quot;table-layout:auto&quot;}
