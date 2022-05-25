---
title: Datensatz-Time-to-Live (TTL)-API-Endpunkt
description: Mit dem Endpunkt /ttl in der Data Hygiene API können Sie Datensatz-TTLs in Adobe Experience Platform programmgesteuert planen.
source-git-commit: 931b847761e649696aa8433d53233593efd4d1ee
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 7%

---

# Endpunkt &quot;Datensatzzeit bis Live&quot;(TTL)

>[!IMPORTANT]
>
>Die Funktionen zur Datenhygiene in Adobe Experience Platform sind derzeit nur für Organisationen verfügbar, die Adobe Shield für das Gesundheitswesen erworben haben.

Die `/ttl` -Endpunkt in der Data Hygiene API ermöglicht es Ihnen, Time-to-Live (TTL)-Protokolle für Datensätze in Adobe Experience Platform zu planen.

Eine Datensatz-TTL ist nur ein zeitverzögerter Löschvorgang. Der Datensatz ist in der Zwischenzeit nicht geschützt, daher kann er auf andere Weise gelöscht werden, bevor sein Ablauf erreicht ist.

>[!NOTE]
>
>Obwohl der Ablauf als spezifischer Zeitpunkt angegeben ist, kann es bis zu 24 Stunden nach Ablauf der Frist geben, bevor die eigentliche Löschung eingeleitet wird. Sobald der Löschvorgang eingeleitet wurde, kann es bis zu sieben Tage dauern, bis alle Spuren des Datensatzes aus Platform-Systemen entfernt wurden.

Sie können die TTL jederzeit abbrechen oder die Trigger-Zeit ändern, bevor der Datensatz-Löschvorgang tatsächlich eingeleitet wird. Nachdem Sie eine TTL abgebrochen haben, können Sie sie erneut öffnen, indem Sie einen neuen Ablauf festlegen.

Sobald das Löschen des Datensatzes initiiert wurde, wird seine TTL als `executing`und darf nicht weiter geändert werden. Der Datensatz selbst kann bis zu sieben Tage lang wiederhergestellt werden, jedoch nur durch einen manuellen Prozess, der über eine Adobe-Serviceanfrage initiiert wurde.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der Data Hygiene API. Bevor Sie fortfahren, lesen Sie bitte die [Übersicht](./overview.md) für Links zur zugehörigen Dokumentation, eine Anleitung zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtige Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen von Experience Platform-APIs benötigt werden.

## Datensatz-TTLs auflisten {#list}

Sie können alle TTL-Datensätze für Ihr Unternehmen auflisten, indem Sie eine GET-Anfrage stellen.

**API-Format**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| Parameter | Beschreibung |
| --- | --- |
| `{QUERY_PARAMETERS}` | Eine Liste optionaler Abfrageparameter mit mehreren durch getrennten Parametern `&` Zeichen. Zu den gebräuchlichen Parametern gehören `size` und `page` für Paginierungszwecke. Eine vollständige Liste der unterstützten Abfrageparameter finden Sie im Abschnitt [Anhang](#query-params). |

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

Eine erfolgreiche Antwort listet die resultierenden TTLs auf. Das folgende Beispiel wurde aus Platzgründen abgeschnitten.

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
| `results` | Enthält die Details der zurückgegebenen TTLs. Weitere Informationen zu den Eigenschaften einer TTL-Entität finden Sie im Abschnitt Antwort zum Erstellen einer [Suchaufruf](#lookup). |
| `current_page` | Die aktuelle Seite der aufgelisteten Ergebnisse. |
| `total_pages` | Die Gesamtzahl der Seiten in der Antwort. |
| `total_count` | Die Gesamtzahl der TTL-Entitäten in der Antwort. |

{style=&quot;table-layout:auto&quot;}

## TTL nachschlagen {#lookup}

Sie können eine Datensatz-TTL über eine GET-Anfrage nachschlagen.

**API-Format**

```http
GET /ttl/{TTL_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{TTL_ID}` | Die Kennung der TTL, die Sie nachschlagen möchten. |

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
| `ttlId` | Die Kennung der TTL des Datensatzes. |
| `datasetId` | Die Kennung des Datensatzes, für den diese TTL gilt. |
| `imsOrg` | Die Kennung Ihres Unternehmens. |
| `status` | Der aktuelle Status der TTL. |
| `expiry` | Das geplante Datum und die Uhrzeit, zu der der Datensatz gelöscht wird. |
| `updatedAt` | Ein Zeitstempel, der angibt, wann die TTL zuletzt aktualisiert wurde. |
| `updatedBy` | Der Benutzer, der die TTL zuletzt aktualisiert hat. |

{style=&quot;table-layout:auto&quot;}

## TTL erstellen {#create}

Sie können eine TTL für einen Datensatz über eine POST-Anfrage hinzufügen.

**API-Format**

```http
POST /ttl
```

**Anfrage**

Die folgende Anfrage plant einen Datensatz `5b020a27e7040801dedbf46e` zur Streichung Ende 2022 (Greenwich Mean Time).

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

Eine erfolgreiche Antwort gibt die Details der TTL mit dem HTTP-Status 200 (OK) zurück, wenn eine bereits vorhandene TTL aktualisiert wurde, oder 201 (Erstellt), wenn keine bereits vorhandene TTL vorhanden war.

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
| `ttlId` | Die Kennung der TTL des Datensatzes. |
| `datasetId` | Die Kennung des Datensatzes, für den diese TTL gilt. |
| `imsOrg` | Die Kennung Ihres Unternehmens. |
| `status` | Der aktuelle Status der TTL. |
| `expiry` | Das geplante Datum und die Uhrzeit, zu der der Datensatz gelöscht wird. |
| `updatedAt` | Ein Zeitstempel, der angibt, wann die TTL zuletzt aktualisiert wurde. |
| `updatedBy` | Der Benutzer, der die TTL zuletzt aktualisiert hat. |

{style=&quot;table-layout:auto&quot;}

## TTL aktualisieren {#update}

Sie können eine TTL für einen Datensatz über eine PUT-Anfrage aktualisieren.

**API-Format**

```http
PUT /ttl/{TTL_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{TTL_ID}` | Die Kennung der TTL, die Sie ändern möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Die folgende Anfrage aktualisiert die TTL für den Datensatz `5b020a27e7040801dedbf46e` so läuft sie Ende 2023 aus (Greenwich Mean Time).

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
| `ttlId` | Die Kennung der TTL des Datensatzes. |
| `datasetId` | Die Kennung des Datensatzes, für den diese TTL gilt. |
| `imsOrg` | Die Kennung Ihres Unternehmens. |
| `status` | Der aktuelle Status der TTL. |
| `expiry` | Das geplante Datum und die Uhrzeit, zu der der Datensatz gelöscht wird. |
| `updatedAt` | Ein Zeitstempel, der angibt, wann die TTL zuletzt aktualisiert wurde. |
| `updatedBy` | Der Benutzer, der die TTL zuletzt aktualisiert hat. |

{style=&quot;table-layout:auto&quot;}

## TTL abbrechen {#delete}

Sie können eine TTL abbrechen, indem Sie eine DELETE-Anfrage stellen.

**API-Format**

```http
DELETE /ttl/{TTL_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{TTL_ID}` | Die Kennung der TTL, die Sie abbrechen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Die folgende Anfrage aktualisiert die TTL für den Datensatz `5b020a27e7040801dedbf46e` so läuft sie Ende 2023 aus (Greenwich Mean Time).

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der TTL mit ihrer `status` -Attribut jetzt auf `cancelled`.

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
| `ttlId` | Die Kennung der TTL des Datensatzes. |
| `datasetId` | Die Kennung des Datensatzes, für den diese TTL gilt. |
| `imsOrg` | Die Kennung Ihres Unternehmens. |
| `status` | Der aktuelle Status der TTL. |
| `expiry` | Das geplante Datum und die Uhrzeit, zu der der Datensatz gelöscht wird. |
| `updatedAt` | Ein Zeitstempel, der angibt, wann die TTL zuletzt aktualisiert wurde. |
| `updatedBy` | Der Benutzer, der die TTL zuletzt aktualisiert hat. |

{style=&quot;table-layout:auto&quot;}

## Verlauf einer TTL abrufen

Sie können den Verlauf einer bestimmten TTL mithilfe des Abfrageparameters nachschlagen `include=history` in einer Suchanfrage. Das Ergebnis enthält Informationen über die Erstellung der TTL, alle angewendeten Aktualisierungen sowie über deren Abbruch oder Ausführung (falls zutreffend).

**API-Format**

```http
GET /ttl/{TTL_ID}?include=history
```

| Parameter | Beschreibung |
| --- | --- |
| `{TTL_ID}` | Die Kennung der TTL, deren Verlauf Sie nachschlagen möchten. |

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

Eine erfolgreiche Antwort gibt die Details der TTL mit einer `history` Array, das die Details angibt `status`, `expiry`, `updatedAt`und `updatedBy` -Attribute für jede der aufgezeichneten Aktualisierungen.

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
| `ttlId` | Die Kennung der TTL des Datensatzes. |
| `datasetId` | Die Kennung des Datensatzes, für den diese TTL gilt. |
| `imsOrg` | Die Kennung Ihres Unternehmens. |
| `history` | Listet den Verlauf der Aktualisierungen für die TTL als Array von Objekten auf, wobei jedes Objekt die `status`, `expiry`, `updatedAt`und `updatedBy` -Attribute für die TTL zum Zeitpunkt der Aktualisierung. |

{style=&quot;table-layout:auto&quot;}

## Anhang

### Akzeptierte Abfrageparameter {#query-params}

In der folgenden Tabelle sind die verfügbaren Abfrageparameter aufgeführt, wenn [Datensatz-TTLs auflisten](#list):

| Parameter | Beschreibung | Beispiel |
| --- | --- | --- |
| `size` | Eine Ganzzahl zwischen 1 und 100, die die maximale Anzahl der zurückzugebenden TTLs angibt. Die Standardeinstellung ist 25. | `size=50` |
| `page` | Eine Ganzzahl, die angibt, welche Seite von TTLs zurückgegeben werden soll. | `page=3` |
| `status` | Eine kommagetrennte Liste von Status. Wenn dies eingeschlossen ist, stimmt die Antwort mit TTLs überein, deren aktueller Status zu den aufgelisteten gehört. | `status=pending,cancelled` |
| `author` | Stimmt überein mit TTLs, deren `created_by` entspricht der Suchzeichenfolge. Wenn die Suchzeichenfolge mit `LIKE` oder `NOT LIKE`, wird der Rest als SQL-Suchmuster behandelt. Andernfalls wird die gesamte Suchzeichenfolge als Zeichenfolge in Textform behandelt, die genau mit dem gesamten Inhalt eines `created_by` -Feld. | `author=LIKE %john%` |
| `createdDate` | Sucht nach TTLs, die im 24-Stunden-Fenster erstellt wurden, beginnend mit dem angegebenen Zeitpunkt.<br><br>Beachten Sie, dass Daten ohne Uhrzeit (wie `2021-12-07`) den Datum/Uhrzeit am Anfang des Tages darstellen. Daher `createdDate=2021-12-07` bezieht sich auf alle am 7. Dezember 2021 erstellten TTL aus `00:00:00` bis `23:59:59.999999999` (UTC). | `createdDate=2021-12-07` |
| `createdFromDate` | Entspricht TTLs, die zum angegebenen Zeitpunkt oder danach erstellt wurden. | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | Entspricht TTLs, die zum angegebenen Zeitpunkt oder vor dem angegebenen Zeitpunkt erstellt wurden. | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | liken `createdDate` / `createdFromDate` / `createdToDate`, stimmt jedoch mit der Aktualisierungszeit einer TTL anstelle der Erstellungszeit überein.<br><br>Eine TTL wird bei jeder Bearbeitung als aktualisiert betrachtet, auch wenn sie erstellt, abgebrochen oder ausgeführt wird. | `updatedDate=2022-01-01` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | Sucht nach TTLs, die zu einem beliebigen Zeitpunkt im angegebenen Intervall abgebrochen wurden. Dies gilt auch dann, wenn die TTL später erneut geöffnet wurde (durch Festlegen eines neuen Ablaufs für denselben Datensatz). | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | Sucht nach TTLs, die im angegebenen Intervall abgeschlossen wurden. | `completedToDate=2021-11-11-06:00` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | Sucht nach TTLs, die im angegebenen Intervall ausgeführt werden sollen oder bereits ausgeführt wurden. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |

{style=&quot;table-layout:auto&quot;}
