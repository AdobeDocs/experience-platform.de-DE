---
title: API-Endpunkt für Datensatzablauf
description: Mit dem Endpunkt /ttl in der Data Hygiene API können Sie die Ablaufzeit von Datensätzen in Adobe Experience Platform programmgesteuert planen.
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: 49ba5263c6dc8eccac2ffe339476cf316c68e486
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 34%

---

# Endpunkt für Datensatzablauf

>[!IMPORTANT]
>
>Die Datenhygiene-Funktionen in Adobe Experience Platform sind derzeit nur für Organisationen verfügbar, die Healthcare Shield erworben haben.

Die `/ttl` -Endpunkt in der Data Hygiene API ermöglicht es Ihnen, Ablaufdaten für Datensätze in Adobe Experience Platform zu planen.

Ein Datensatzablauf ist nur ein zeitverzögerter Löschvorgang. Der Datensatz ist in der Zwischenzeit nicht geschützt und kann daher auf andere Weise gelöscht werden, bevor sein Ablaufdatum erreicht wurde.

>[!NOTE]
>
>Obwohl die Löschung als spezifischer Zeitpunkt angegeben ist, kann es bis zu 24 Stunden nach Ablauf der Frist dauern, bevor die eigentliche Löschung eingeleitet wird. Nachdem der Löschvorgang gestartet wurde, kann es bis zu sieben Tage dauern, bis alle Spuren des Datensatzes aus Platform-Systemen entfernt wurden.

Sie können jederzeit vor dem eigentlichen Start des Datensatzlöschens den Ablauf abbrechen oder die Trigger-Zeit ändern. Nachdem Sie den Ablauf eines Datensatzes abgebrochen haben, können Sie ihn erneut öffnen, indem Sie einen neuen Ablauf festlegen.

Sobald das Löschen des Datensatzes eingeleitet wurde, wird sein Ablaufauftrag als `executing`und darf nicht weiter geändert werden. Der Datensatz selbst kann bis zu sieben Tage lang wiederhergestellt werden, jedoch nur durch einen manuellen Prozess über eine Adobe-Service-Anfrage. Während die Anfrage ausgeführt wird, beginnen der Data Lake, der Identity Service und das Echtzeit-Kundenprofil separate Prozesse, um den Inhalt des Datensatzes aus den entsprechenden Diensten zu entfernen. Sobald die Daten aus allen drei Diensten gelöscht wurden, wird der Ablauf als `executed`.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der Data Hygiene API. Bevor Sie fortfahren, lesen Sie die [Übersicht](./overview.md) mit Links zur zugehörigen Dokumentation, einer Anleitung zum Lesen der API-Beispielaufrufe in diesem Dokument und wichtigen Informationen zu den Kopfzeilen, die für die erfolgreiche Ausführung von Aufrufen an eine Experience Platform-API erforderlich sind.

## Auflisten der Datensatzabläufe {#list}

Sie können alle Datensatzabläufe für Ihr Unternehmen auflisten, indem Sie eine GET-Anfrage stellen.

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

Eine erfolgreiche Antwort listet die resultierenden Datensatzabläufe auf. Das folgende Beispiel wurde aus Platzgründen gekürzt.

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
| `results` | Enthält die Details der zurückgegebenen Datensatzabläufe. Weitere Informationen zu den Eigenschaften eines Datensatzablaufs finden Sie im Abschnitt Antwort zum Erstellen einer [Suchaufruf](#lookup). |
| `current_page` | Die aktuelle Seite der aufgelisteten Ergebnisse. |
| `total_pages` | Die Gesamtzahl der Seiten in der Antwort. |
| `total_count` | Die Gesamtzahl der Datensatzabläufe in der Antwort. |

{style=&quot;table-layout:auto&quot;}

## Nachschlagen des Datensatzablaufs {#lookup}

Sie können über eine GET-Anfrage nach einem Datensatzablauf suchen.

**API-Format**

```http
GET /ttl/{TTL_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{TTL_ID}` | Die ID des Datensatzablaufs, den Sie nachschlagen möchten. |

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

Eine erfolgreiche Antwort gibt die Details des Datensatzablaufs zurück.

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
| `ttlId` | Die ID des Datensatzablaufs. |
| `datasetId` | Die Kennung des Datensatzes, für den dieser Ablauf gilt. |
| `imsOrg` | Die Kennung Ihres Unternehmens. |
| `status` | Der aktuelle Status des Datensatzablaufs. |
| `expiry` | Das geplante Datum und die Uhrzeit, zu der der Datensatz gelöscht wird. |
| `updatedAt` | Ein Zeitstempel, der angibt, wann der Ablauf zuletzt aktualisiert wurde. |
| `updatedBy` | Der Benutzer, der das Ablaufdatum zuletzt aktualisiert hat. |

{style=&quot;table-layout:auto&quot;}

## Erstellen eines Datensatzablaufs {#create}

Sie können über eine POST-Anfrage ein Ablaufdatum für einen Datensatz erstellen.

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
| `datasetId` | Die ID des Datensatzes, für den Sie ein Ablaufdatum planen möchten. |
| `expiry` | Ein ISO 8601-Zeitstempel für den Zeitpunkt, zu dem der Datensatz gelöscht wird. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die Details des Datensatzablaufs mit dem HTTP-Status 200 (OK) zurück, wenn ein bereits vorhandener Ablauf aktualisiert wurde, oder 201 (Erstellt), wenn kein bereits vorhandener Ablauf vorhanden war.

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
| `ttlId` | Die ID des Datensatzablaufs. |
| `datasetId` | Die Kennung des Datensatzes, für den dieser Ablauf gilt. |
| `imsOrg` | Die Kennung Ihres Unternehmens. |
| `status` | Der aktuelle Status des Datensatzablaufs. |
| `expiry` | Das geplante Datum und die Uhrzeit, zu der der Datensatz gelöscht wird. |
| `updatedAt` | Ein Zeitstempel, der angibt, wann der Ablauf zuletzt aktualisiert wurde. |
| `updatedBy` | Der Benutzer, der das Ablaufdatum zuletzt aktualisiert hat. |

{style=&quot;table-layout:auto&quot;}

## Aktualisieren des Datensatzablaufs {#update}

Sie können den Ablauf eines Datensatzes über eine PUT-Anfrage aktualisieren.

**API-Format**

```http
PUT /ttl/{TTL_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{TTL_ID}` | Die ID des Datensatzablaufs, den Sie ändern möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Die folgende Anfrage aktualisiert den Ablauf für den Datensatz `5b020a27e7040801dedbf46e` so läuft sie Ende 2023 aus (Greenwich Mean Time).

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

Eine erfolgreiche Antwort gibt die Details des aktualisierten Ablaufs zurück.

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
| `ttlId` | Die ID des Datensatzablaufs. |
| `datasetId` | Die Kennung des Datensatzes, für den dieser Ablauf gilt. |
| `imsOrg` | Die Kennung Ihres Unternehmens. |
| `status` | Der aktuelle Status des Datensatzablaufs. |
| `expiry` | Das geplante Datum und die Uhrzeit, zu der der Datensatz gelöscht wird. |
| `updatedAt` | Ein Zeitstempel, der angibt, wann der Ablauf zuletzt aktualisiert wurde. |
| `updatedBy` | Der Benutzer, der das Ablaufdatum zuletzt aktualisiert hat. |

{style=&quot;table-layout:auto&quot;}

## Abbrechen des Datensatzablaufs {#delete}

Sie können den Ablauf eines Datensatzes abbrechen, indem Sie eine DELETE-Anfrage stellen.

**API-Format**

```http
DELETE /ttl/{TTL_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{TTL_ID}` | Die ID des Datensatzablaufs, den Sie abbrechen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Die folgende Anfrage aktualisiert den Ablauf für den Datensatz `5b020a27e7040801dedbf46e` so läuft sie Ende 2023 aus (Greenwich Mean Time).

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des Datensatzablaufs mit `status` -Attribut jetzt auf `cancelled`.

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
| `ttlId` | Die ID des Datensatzablaufs. |
| `datasetId` | Die Kennung des Datensatzes, für den dieser Ablauf gilt. |
| `imsOrg` | Die Kennung Ihres Unternehmens. |
| `status` | Der aktuelle Status des Datensatzablaufs. |
| `expiry` | Das geplante Datum und die Uhrzeit, zu der der Datensatz gelöscht wird. |
| `updatedAt` | Ein Zeitstempel, der angibt, wann der Ablauf zuletzt aktualisiert wurde. |
| `updatedBy` | Der Benutzer, der das Ablaufdatum zuletzt aktualisiert hat. |

{style=&quot;table-layout:auto&quot;}

## Abrufen des Verlaufs eines Datensatzablaufs

Sie können den Verlauf eines bestimmten Datensatzablaufs mithilfe des Abfrageparameters nachschlagen `include=history` in einer Suchanfrage. Das Ergebnis enthält Informationen über die Erstellung des Datensatzablaufs, alle angewendeten Aktualisierungen sowie über den Abbruch oder die Ausführung (falls zutreffend).

**API-Format**

```http
GET /ttl/{TTL_ID}?include=history
```

| Parameter | Beschreibung |
| --- | --- |
| `{TTL_ID}` | Die ID des Datensatzablaufs, dessen Verlauf Sie nachschlagen möchten. |

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

Eine erfolgreiche Antwort gibt die Details des Datensatzablaufs mit einer `history` Array, das die Details angibt `status`, `expiry`, `updatedAt`und `updatedBy` -Attribute für jede der aufgezeichneten Aktualisierungen.

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
| `ttlId` | Die ID des Datensatzablaufs. |
| `datasetId` | Die Kennung des Datensatzes, für den dieser Ablauf gilt. |
| `imsOrg` | Die Kennung Ihres Unternehmens. |
| `history` | Listet den Verlauf der Aktualisierungen für den Ablauf als ein Array von Objekten auf, wobei jedes Objekt die `status`, `expiry`, `updatedAt`und `updatedBy` -Attribute für den Ablauf zum Zeitpunkt der Aktualisierung. |

{style=&quot;table-layout:auto&quot;}

## Anhang

### Akzeptierte Abfrageparameter {#query-params}

In der folgenden Tabelle sind die verfügbaren Abfrageparameter aufgeführt, wenn [Auflisten der Datensatzabläufe](#list):

| Parameter | Beschreibung | Beispiel |
| --- | --- | --- |
| `size` | Eine Ganzzahl zwischen 1 und 100, die die maximale Anzahl der auszugebenden Abläufe angibt. Die Standardeinstellung ist 25. | `size=50` |
| `page` | Eine Ganzzahl, die angibt, welche Ablaufseite zurückgegeben werden soll. | `page=3` |
| `status` | Eine durch Kommas getrennte Liste von Status. Wenn enthalten, stimmt die Antwort mit den Datensatzabläufen überein, deren aktueller Status zu den aufgelisteten gehört. | `status=pending,cancelled` |
| `author` | Sucht nach Ablauf, dessen `created_by` entspricht der Suchzeichenfolge. Wenn die Suchzeichenfolge mit `LIKE` oder `NOT LIKE` beginnt, wird der Rest als SQL-Suchmuster behandelt. Andernfalls wird die gesamte Suchzeichenfolge als exakte Zeichenfolge gehandhabt, die genau mit dem gesamten Inhalt des `created_by`-Felds übereinstimmen muss. | `author=LIKE %john%` |
| `createdDate` | Sucht nach Ablauffristen, die im 24-Stunden-Fenster erstellt wurden, beginnend mit dem angegebenen Zeitpunkt.<br><br>Beachten Sie, dass ein Datum ohne Uhrzeit (wie `2021-12-07`) den Datum/Uhrzeit-Wert am Anfang des Tages darstellt. Daher `createdDate=2021-12-07` bezieht sich auf alle am 7. Dezember 2021 erstellten Abläufe von `00:00:00` bis `23:59:59.999999999` (UTC). | `createdDate=2021-12-07` |
| `createdFromDate` | Sucht nach Ablauffristen, die zum angegebenen Zeitpunkt oder danach erstellt wurden. | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | Sucht nach Ablauffristen, die zum angegebenen Zeitpunkt oder zuvor erstellt wurden. | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | liken `createdDate` / `createdFromDate` / `createdToDate`, stimmt jedoch mit der Aktualisierungszeit eines Datensatzes anstelle der Erstellungszeit überein.<br><br>Ein Ablauf gilt bei jeder Bearbeitung als aktualisiert, auch bei der Erstellung, dem Abbruch oder der Ausführung. | `updatedDate=2022-01-01` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | Sucht nach Ablauf, die zu einem beliebigen Zeitpunkt im angegebenen Intervall abgebrochen wurden. Dies gilt auch dann, wenn die Gültigkeit später erneut geöffnet wurde (durch Festlegen eines neuen Ablaufs für denselben Datensatz). | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | Sucht nach Ablauffristen, die im angegebenen Intervall abgeschlossen wurden. | `completedToDate=2021-11-11-06:00` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | Sucht nach Ablauffristen, die im angegebenen Intervall ausgeführt werden sollen oder bereits ausgeführt wurden. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |

{style=&quot;table-layout:auto&quot;}
