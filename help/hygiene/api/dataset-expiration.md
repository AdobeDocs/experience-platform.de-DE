---
title: API-Endpunkt für Datensatzgültigkeiten
description: Mit dem Endpunkt /ttl in der Datenhygiene-API können Sie programmgesteuert einen Zeitplan für Datensatzgültigkeiten in Adobe Experience Platform festlegen.
role: Developer
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: ca6d7d257085da65b3f08376f0bd32e51e293533
workflow-type: tm+mt
source-wordcount: '2331'
ht-degree: 19%

---

# Endpunkt der Datensatzgültigkeit

Verwenden Sie den `/ttl`-Endpunkt in der Data Hygiene API, um zu planen, wann Datensätze in Adobe Experience Platform gelöscht werden sollen.

Eine Datensatzgültigkeit ist ein verzögerter Löschvorgang. Der Datensatz ist in der Zwischenzeit nicht geschützt und kann vor seiner geplanten Gültigkeit auf andere Weise gelöscht werden.

>[!NOTE]
>
>Obwohl die Löschung als spezifischer Zeitpunkt angegeben ist, kann es bis zu 24 Stunden nach Ablauf der Frist dauern, bevor die eigentliche Löschung eingeleitet wird. Nachdem der Löschvorgang gestartet wurde, kann es bis zu sieben Tage dauern, bis alle Spuren des Datensatzes aus Experience Platform-Systemen entfernt wurden.

Bevor der Löschvorgang beginnt, können Sie den Ablauf abbrechen oder den geplanten Zeitpunkt ändern. Um eine abgebrochene Gültigkeit erneut zu öffnen, legen Sie ein neues Ablaufdatum fest.

Sobald der Löschvorgang beginnt, wird der Gültigkeitsvorgang als `executing` markiert und kann nicht mehr geändert werden. Der Datensatz kann bis zu sieben Tage lang wiederhergestellt werden, jedoch nur über eine manuelle Adobe-Service-Anfrage. Während des Löschens entfernen der Data Lake, der Identity Service und das Echtzeit-Kundenprofil jeweils separat die Inhalte des Datensatzes. Nach Abschluss des Löschvorgangs wird der Ablauf als `completed` markiert.

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

Sie können alle für Ihr Unternehmen konfigurierten Datensatzgültigkeiten auflisten, indem Sie eine GET-Anfrage an den `/ttl`-Endpunkt stellen.

Filtern Sie Ergebnisse mithilfe von Abfrageparametern, um nur die Gültigkeiten zurückzugeben, die Ihren Kriterien entsprechen. Jedes Ergebnis enthält Status- und Konfigurationsdetails für jede Datensatzgültigkeit.

**API-Format**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| Parameter | Beschreibung |
| --- | --- |
| `{QUERY_PARAMETERS}` | Eine Liste optionaler Abfrageparameter mit mehreren durch `&`-Zeichen getrennten Parametern. Zu den gebräuchlichen Parametern gehören `limit` und `page` für Paginierungszwecke. Eine vollständige Liste der unterstützten Abfrageparameter finden Sie im [Anhang](#query-params) einer vollständigen Liste der unterstützten Abfrageparameter. Die am häufigsten verwendeten Parameter sind sowohl unten als auch im Anhang aufgeführt. |
| `author` | Filtern Sie nach dem Benutzer, der die Datensatzgültigkeit zuletzt aktualisiert oder erstellt hat. Unterstützt SQL-ähnliche Muster (z. B. `LIKE %john%`). |
| `datasetId` | Filtern von Gültigkeiten nach einer bestimmten Datensatz-ID. |
| `datasetName` | Bei einem Filter für Datensatznamen wird nicht zwischen Groß- und Kleinschreibung unterschieden. |
| `status` | Filtern Sie nach einer durch Kommas getrennten Liste von Status: `pending`, `executing`, `cancelled`, `completed`. |
| `expiryDate` | Filtern Sie nach Gültigkeiten mit einem bestimmten Ablaufdatum. |
| `limit` | Legen Sie die maximale Anzahl der zurückzugebenden Ergebnisse fest (1-100, Standard: 25). |
| `page` | Paginieren Sie die Ergebnisse mit einem nullbasierten Index (Standardseitengröße: 50, max.: 100). |

{style="table-layout:auto"}

**Anfrage**

Die folgende Anfrage ruft alle Datensatzgültigkeiten ab, die vor dem 1. August 2021 aktualisiert wurden und zuletzt von einem Benutzer aktualisiert wurden, dessen Name mit „Jane Doe“ übereinstimmt.

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
      "ttlId": "SD-c9f113f2-d751-44bc-bc20-9d5ca0b6ae15",
      "datasetId": "3e9f815ae1194c65b2a4c5ea",
      "datasetName": "Acme_Profile_Engagements",
      "sandboxName": "acme-beta",
      "displayName": "Engagement Data Retention Policy",
      "description": "Scheduled expiry for Acme marketing data",
      "imsOrg": "C9D8E7F6A5B41234567890AB@AcmeOrg",
      "status": "pending",
      "expiry": "2027-01-12T17:15:31.000Z",
      "updatedAt": "2026-12-15T12:40:20.000Z",
      "updatedBy": "t.lannister@acme.com <t.lannister@acme.com> 3E9F815AE1194C65B2A4C5EA@acme.com"
    }
  ],
  "current_page": 0,
  "total_pages": 1,
  "total_count": 1
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `results` | Ein Array von Konfigurationen für die Datensatzgültigkeit. |
| `ttlId` | Die eindeutige Kennung für die Konfiguration der Datensatzgültigkeit. |
| `datasetId` | Die eindeutige Kennung des Datensatzes, der dieser Konfiguration zugeordnet ist. |
| `datasetName` | Der Name des Datensatzes. |
| `sandboxName` | Die Sandbox, in der diese Datensatzgültigkeit konfiguriert ist. |
| `displayName` | Ein für Menschen lesbarer Name für die Ablaufkonfiguration. |
| `description` | Eine Beschreibung der Ablaufkonfiguration. |
| `imsOrg` | Ihre eindeutige Organisationskennung. |
| `status` | Der aktuelle Status der Gültigkeit. Eines von: `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | Geplantes Ablaufdatum und -uhrzeit (ISO 8601-Format). |
| `updatedAt` | Der Zeitstempel der letzten Aktualisierung dieser Konfiguration. |
| `updatedBy` | Die Kennung und E-Mail-Adresse des Benutzers oder Dienstes, der die Konfiguration zuletzt aktualisiert hat. |
| `current_page` | Der Index der aktuellen Ergebnisseite (nullbasiert). |
| `total_pages` | Die Gesamtzahl der verfügbaren Ergebnisseiten. |
| `total_count` | Die Gesamtzahl der zurückgegebenen Datensätze zur Datensatzgültigkeitskonfiguration. |

{style="table-layout:auto"}

## Nachschlagen einer Datensatzgültigkeit {#lookup}

Rufen Sie die Details für eine bestimmte Datensatzgültigkeitskonfiguration ab, indem Sie eine GET-Anfrage mit entweder der Datensatzgültigkeits-ID oder der Datensatz-ID als Pfadparameter stellen.

>[!IMPORTANT]
>
>Sie können im Pfad entweder eine Datensatz-Gültigkeits-ID (z. B. `SD-xxxxxx-xxxx`) oder eine Datensatz-ID angeben. Der `ttlId` in der Antwort ist die eindeutige Kennung für die Datensatzgültigkeit.

**API-Format**

```http
GET /ttl/{ID}
GET /ttl/{ID}?include=history
```

| Parameter | Beschreibung |
| --- | --- |
| `{ID}` | Die eindeutige Kennung für die Konfiguration der Datensatzgültigkeit. Sie können entweder eine Datensatz-Ablaufkennung oder eine Datensatz-ID angeben. |
| `include` | (Optional) Bei Festlegung auf `history` enthält die Antwort ein `history`-Array mit Änderungsereignissen für die Konfiguration. |

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
    "displayName": "Delete Acme Data before 2025",
    "description": "The Acme information in this dataset is licensed for our use through the end of 2024.",
    "imsOrg": "885737B25DC460C50A49411B@AdobeOrg",
    "status": "pending",
    "expiry": "2035-09-25T00:00:00Z",
    "updatedAt": "2025-05-01T19:00:55.000Z",
    "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `ttlId` | Die eindeutige Kennung für die Konfiguration der Datensatzgültigkeit. |
| `datasetId` | Die eindeutige Kennung für den Datensatz. |
| `datasetName` | Der Name des Datensatzes. |
| `sandboxName` | Die Sandbox, in der die Datensatzgültigkeit konfiguriert ist. |
| `displayName` | Ein für Menschen lesbarer Name für die Konfiguration der Datensatzgültigkeit. |
| `description` | Eine Beschreibung der Konfiguration der Datensatzgültigkeit. |
| `imsOrg` | Die eindeutige Organisationskennung, die dieser Konfiguration zugeordnet ist. |
| `status` | Der aktuelle Status der Konfiguration der Datensatzgültigkeit.<br>Eins von: `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | Der Zeitstempel der geplanten Gültigkeit für den Datensatz (ISO 8601-Format). |
| `updatedAt` | Zeitstempel der letzten Aktualisierung. |
| `updatedBy` | Die Kennung und E-Mail-Adresse des Benutzers oder Service, der die Datensatzgültigkeit zuletzt aktualisiert hat. |

{style="table-layout:auto"}

### Gültigkeits-Tags des Katalogs

Wenn Sie die [Katalog-API](../../catalog/api/getting-started.md) verwenden, um Details zu einem Datensatz nachzuschlagen, wird dieser unter `tags.adobe/hygiene/ttl` aufgeführt, wenn er ein aktives Gültigkeitsdatum hat.

Die folgende JSON-Datei enthält die gekürzte Katalog-API-Antwort für einen Datensatz mit einem Gültigkeitswert von `32503680000000`. Das Tag kodiert den Ablauf als die Anzahl der Millisekunden seit der Unix-Epoche.

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

Erstellen Sie eine neue Konfiguration für die Datensatzgültigkeit, um festzulegen, wann ein Datensatz abläuft und gelöscht werden kann.\
Geben Sie die Datensatz-ID, das Ablaufdatum oder die Datums-/Uhrzeitangabe (im ISO 8601-Format), einen Anzeigenamen und (optional) eine Beschreibung an.

>[!NOTE]
>
>Der Ablaufwert kann ein Datum (JJJJ-MM-TT) oder ein Datum und eine Uhrzeit (JJJJ-MM-TTh:MM:SSZ) sein. Wenn Sie nur ein Datum angeben, verwendet das System an diesem Tag Mitternacht UTC (:00::00Z). Das Verfalldatum muss mindestens 24 Stunden in der Zukunft liegen.

Um eine Datensatzgültigkeit zu erstellen, senden Sie eine POST-Anfrage, wie unten dargestellt.

>[!TIP]
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
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "datasetId": "3e9f815ae1194c65b2a4c5ea",
        "expiry": "2030-12-31",
        "displayName": "Expiry rule for Acme customers",
        "description": "Set expiration for Acme customer dataset"
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `datasetId` | **Erforderlich.** Die eindeutige Kennung für den Datensatz, auf den die Gültigkeit angewendet werden soll. |
| `expiry` | **Erforderlich.** Ablaufdatum und -uhrzeit im ISO 8601-Format. Dies definiert die Lebensdauer von Daten im System. Wenn nur ein Datum angegeben wird, wird standardmäßig Mitternacht UTC (00:00:00Z) verwendet. Das **muss mindestens 24 Stunden in der Zukunft**. <br>**HINWEIS**:<ul><li>Die Anfrage schlägt fehl, wenn bereits eine Datensatzgültigkeit für den Datensatz vorhanden ist.</li></ul> |
| `displayName` | **Erforderlich.** Ein für Menschen lesbarer Name für die Konfiguration der Datensatzgültigkeit. |
| `description` | Eine optionale Beschreibung für die Konfiguration der Datensatzgültigkeit. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 (Erstellt) und die neue Konfiguration der Datensatzgültigkeit zurück.

```json
{
  "ttlId": "SD-2aaf113e-3f17-4321-bf29-a2c51152b042",
  "datasetId": "3e9f815ae1194c65b2a4c5ea",
  "datasetName": "Acme_Customer_Data",
  "sandboxName": "acme-prod",
  "displayName": "Expiry rule for Acme customers",
  "description": "Set expiration for Acme customer dataset",
  "imsOrg": "{ORG_ID}",
  "status": "pending",
  "expiry": "2030-12-31T00:00:00Z",
  "updatedAt": "2025-01-02T10:35:45.000Z",
  "updatedBy": "s.stark@acme.com <s.stark@acme.com> 3E9F815AE1194C65B2A4C5EA@acme.com"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `ttlId` | Die eindeutige Kennung für die erstellte Datensatzgültigkeitskonfiguration. |
| `datasetId` | Die eindeutige Kennung für den Datensatz. |
| `datasetName` | Der Name des Datensatzes. |
| `sandboxName` | Die Sandbox, in der diese Datensatzgültigkeit konfiguriert ist. |
| `displayName` | Der Anzeigename für die Konfiguration der Datensatzgültigkeit. |
| `description` | Eine Beschreibung der Konfiguration der Datensatzgültigkeit. |
| `imsOrg` | Die eindeutige Organisationskennung, die dieser Konfiguration zugeordnet ist. |
| `status` | Der aktuelle Status der Konfiguration der Datensatzgültigkeit.<br>Eins von: `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | Der Zeitstempel der geplanten Gültigkeit für den Datensatz. |
| `updatedAt` | Der Zeitstempel für die letzte Aktualisierung. |
| `updatedBy` | Die Kennung und E-Mail-Adresse des Benutzers oder Service, der die Konfiguration der Datensatzgültigkeit zuletzt aktualisiert hat. |

Ein 400-HTTP-Status (Bad Request) tritt auf, wenn für den Datensatz bereits eine Datensatzgültigkeit vorhanden ist. Ein 404-HTTP-Status (Nicht gefunden) tritt auf, wenn kein solcher Datensatz vorhanden ist oder Sie keinen Zugriff auf den Datensatz haben.

## Aktualisieren einer Datensatzgültigkeitskonfiguration {#update}

Um eine vorhandene Datensatzgültigkeitskonfiguration zu aktualisieren, stellen Sie eine PUT-Anfrage an `/ttl/DATASET_EXPIRATION_ID`. Sie können nur die Felder `displayName`, `description` und `expiry` der Konfiguration aktualisieren. Aktualisierungen sind nur zulässig, wenn der Ablaufstatus `pending` ist.

>[!NOTE]
>
>Das Feld `expiry` akzeptiert ein Datum (JJJJ-MM-TT) oder Datum und Uhrzeit (JJJJ-MM-TT:MM:SSZ). Wenn nur ein Datum angegeben wird, verwendet das System Mitternacht UTC (00:00:00Z) an diesem Tag. Das **muss mindestens 24 Stunden in der Zukunft**.

**API-Format**

```http
PUT /ttl/{DATASET_EXPIRATION_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_EXPIRATION_ID}` | Die eindeutige Kennung für die Konfiguration der Datensatzgültigkeit. **HINWEIS**: Dies wird in der Antwort als `ttlId` bezeichnet. |

**Anfrage**

Die folgende Anfrage aktualisiert die Gültigkeit, den Anzeigenamen und die Beschreibung für `SD-c1f902aa-57cb-412e-bb2b-c70b8e1a5f45`:

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-c1f902aa-57cb-412e-bb2b-c70b8e1a5f45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "displayName": "Customer Dataset Expiry Rule",
        "description": "Updated description for Acme customer dataset",
        "expiry": "2031-06-15"
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `displayName` | (Optional) Ein neuer, für Menschen lesbarer Name für die Konfiguration der Datensatzgültigkeit. |
| `description` | (Optional) Eine neue Beschreibung für die Konfiguration der Datensatzgültigkeit. |
| `expiry` | (Optional) Ein neues Ablaufdatum oder -datum mit Uhrzeit im ISO 8601-Format. Wenn nur ein Datum angegeben wird, wird standardmäßig Mitternacht (UTC) verwendet. Das Verfalldatum muss **mindestens 24 Stunden in der Zukunft** sein. |

>[!NOTE]
>
>In der Anfrage muss mindestens eines dieser Felder angegeben werden.

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 (OK) und die aktualisierte Konfiguration der Datensatzgültigkeit zurück.

```json
{
  "ttlId": "SD-c1f902aa-57cb-412e-bb2b-c70b8e1a5f45",
  "datasetId": "3e9f815ae1194c65b2a4c5ea",
  "datasetName": "Acme_Customer_Data",
  "sandboxName": "acme-prod",
  "displayName": "Customer Dataset Expiry Rule",
  "description": "Updated description for Acme customer dataset",
  "imsOrg": "C9D8E7F6A5B41234567890AB@AcmeOrg",
  "status": "pending",
  "expiry": "2031-06-15T00:00:00Z",
  "updatedAt": "2031-05-01T14:11:12.000Z",
  "updatedBy": "b.tarth@acme.com <b.tarth@acme.com> 3E9F815AE1194C65B2A4C5EA@acme.com"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `ttlId` | Die eindeutige Kennung für die aktualisierte Konfiguration der Datensatzgültigkeit. |
| `datasetId` | Die eindeutige Kennung für den Datensatz. |
| `datasetName` | Der Name des Datensatzes. |
| `sandboxName` | Die Sandbox, in der diese Datensatzgültigkeit konfiguriert ist. |
| `displayName` | Der Anzeigename für die Konfiguration der Datensatzgültigkeit. |
| `description` | Eine Beschreibung der Konfiguration der Datensatzgültigkeit. |
| `imsOrg` | Die mit dieser Konfiguration verknüpfte Organisations-ID. |
| `status` | Der aktuelle Status der Konfiguration der Datensatzgültigkeit.<br>Eins von: `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | Der Zeitstempel der geplanten Gültigkeit für den Datensatz. |
| `updatedAt` | Der Zeitstempel für die letzte Aktualisierung. |
| `updatedBy` | Die Kennung und E-Mail-Adresse des Benutzers oder Service, der die Konfiguration der Datensatzgültigkeit zuletzt aktualisiert hat. |

{style="table-layout:auto"}

Eine nicht erfolgreiche Antwort gibt den HTTP-Status 404 (Nicht gefunden) zurück, wenn keine solche Datensatzgültigkeit vorhanden ist.

## Abbrechen der Datensatzgültigkeit {#delete}

Brechen Sie eine ausstehende Konfiguration für die Datensatzgültigkeit ab, indem Sie eine DELETE-Anfrage an `/ttl/{ID}` stellen.

>[!NOTE]
>
>Nur Datensatzgültigkeiten im `pending` können abgebrochen werden. Der Versuch, eine Gültigkeit abzubrechen, die bereits `executing`, `completed` oder `cancelled` ist, gibt HTTP 400 zurück (Bad Request).

**API-Format**

```http
DELETE /ttl/{ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{ID}` | Die eindeutige Kennung für die Konfiguration der Datensatzgültigkeit. Sie können entweder eine Datensatz-Ablaufkennung oder eine Datensatz-ID angeben. |

{style="table-layout:auto"}

**Anfrage**

Mit der folgenden Anfrage wird die Gültigkeit eines Datensatzes mit der ID `SD-d4a7d918-283b-41fd-bfe1-4e730a613d21` abgebrochen:

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-d4a7d918-283b-41fd-bfe1-4e730a613d21 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 (OK) sowie die Konfiguration der abgebrochenen Datensatzgültigkeit zurückgegeben. Beachten Sie, dass das `status` der Gültigkeit auf `cancelled` festgelegt ist.

```json
{
  "ttlId": "SD-d4a7d918-283b-41fd-bfe1-4e730a613d21",
  "datasetId": "5a9e2c68d3b24f03b55a91ce",
  "datasetName": "Acme_Customer_Data",
  "sandboxName": "acme-prod",
  "displayName": "Customer Dataset Expiry Rule",
  "description": "Cancelled expiry configuration for Acme customer dataset",
  "imsOrg": "C9D8E7F6A5B41234567890AB@AcmeOrg",
  "status": "cancelled",
  "expiry": "2032-02-28T00:00:00Z",
  "updatedAt": "2032-01-15T08:27:31.000Z",
  "updatedBy": "s.clegane@acme.com <s.clegane@acme.com> 5A9E2C68D3B24F03B55A91CE@acme.com"
}
```

| Eigenschaft | Beschreibung |
|---|---|
| `ttlId` | Die eindeutige Kennung für die Konfiguration der gelöschten Datensatzgültigkeit. |
| `datasetId` | Die eindeutige Kennung für den Datensatz. |
| `datasetName` | Der Name des Datensatzes. |
| `sandboxName` | Die Sandbox, in der diese Datensatzgültigkeit konfiguriert ist. |
| `displayName` | Der Anzeigename für die Konfiguration der Datensatzgültigkeit. |
| `description` | Eine Beschreibung der Konfiguration der Datensatzgültigkeit. |
| `imsOrg` | Die eindeutige Organisationskennung, die dieser Konfiguration zugeordnet ist. |
| `status` | Der aktuelle Status der Konfiguration der Datensatzgültigkeit.<br>Eins von: `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | Der Zeitstempel der geplanten Gültigkeit für den Datensatz. |
| `updatedAt` | Der Zeitstempel für die letzte Aktualisierung. |
| `updatedBy` | Die Kennung und E-Mail-Adresse des Benutzers oder Service, der die Konfiguration der Datensatzgültigkeit zuletzt aktualisiert hat. |

**Beispiel-400-Antwort (Bad Request)**

Beim Versuch, einen Datensatz mit einer `executing`-, `completed`- oder `cancelled`-Ablaufkonfiguration abzubrechen, tritt ein 400-Fehler auf.

```json
{
  "type": "http://ns.adobe.com/aep/errors/HYGN-3102-400",
  "title": "The requested dataset already has an existing expiration. Additional detail: A TTL already exists for datasetId=686e9ca25ef7462aefe72c93",
  "status": 400,
  "report": {
    "tenantInfo": {
      "sandboxName": "prod",
      "sandboxId": "not-applicable",
      "imsOrgId": "{IMS_ORG_ID}"
    },
    "additionalContext": {
      "Invoking Client ID": "acp_privacy_hygiene"
    }
  },
  "error-chain": [
    {
      "serviceId": "HYGN",
      "errorCode": "HYGN-3102-400",
      "invokingServiceId": "acp_privacy_hygiene",
      "unixTimeStampMs": 1754408150394
    }
  ]
}
```

>[!NOTE]
>
>Beim Versuch, eine bereits `completed` oder `cancelled` Datensatzgültigkeit abzubrechen, tritt ein 404-Fehler auf.

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

