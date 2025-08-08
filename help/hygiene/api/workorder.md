---
title: Löschen von Arbeitsaufträgen
description: Erfahren Sie, wie Sie den Endpunkt /workorder in der Datenhygiene-API verwenden, um in Adobe Experience Platform Arbeitsaufträge zum Löschen von Datensätzen zu verwalten. In diesem Handbuch werden Kontingente, Verarbeitungszeitpläne und die API-Nutzung behandelt.
role: Developer
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: 4f4b668c2b29228499dc28b2c6c54656e98aaeab
workflow-type: tm+mt
source-wordcount: '2104'
ht-degree: 3%

---

# Löschen von Arbeitsaufträgen aufzeichnen {#work-order-endpoint}

Verwenden Sie den `/workorder`-Endpunkt in der Datenhygiene-API, um Arbeitsaufträge zum Löschen von Datensätzen in Adobe Experience Platform zu erstellen, anzuzeigen und zu verwalten. Mit Arbeitsaufträgen können Sie die Entfernung von Daten über Datensätze hinweg kontrollieren, überwachen und verfolgen, um die Datenqualität zu gewährleisten und die Data Governance-Standards Ihres Unternehmens zu unterstützen.

>[!IMPORTANT]
>
>Arbeitsaufträge zum Löschen von Datensätzen dienen der Datenbereinigung, dem Entfernen anonymer Daten oder der Datenminimierung. **Verwenden Sie keine Arbeitsaufträge zum Löschen von Datensätzen für Anfragen zu den Rechten betroffener Personen gemäß Datenschutzbestimmungen wie der DSGVO.** Verwenden Sie für Compliance-Anwendungsfälle [Adobe Experience Platform Privacy Service ](../../privacy-service/home.md).

## Erste Schritte

Bevor Sie beginnen, lesen Sie die [Übersicht](./overview.md), um mehr über erforderliche Kopfzeilen zu erfahren, wie Sie Beispiel-API-Aufrufe lesen und wo Sie zugehörige Dokumentation finden.

## Kontingente und Verarbeitungszeitpläne {#quotas}

Arbeitsaufträge zum Löschen von Datensätzen unterliegen täglichen und monatlichen Obergrenzen für die Übermittlung von Identifikatoren, die durch die Lizenzberechtigung Ihres Unternehmens bestimmt werden. Diese Einschränkungen gelten sowohl für benutzeroberflächen- als auch für API-basierte Anfragen zum Löschen von Datensätzen.

>[!NOTE]
>
>Sie können bis zu **1.000.000 Kennungen pro Tag**, jedoch nur, wenn Ihr restliches monatliches Kontingent dies zulässt. Wenn Ihre monatliche Obergrenze weniger als 1 Million beträgt, können Ihre täglichen Einreichungen diese Obergrenze nicht überschreiten.

### Berechtigung zur monatlichen Übermittlung nach Produkt {#quota-limits}

Die folgende Tabelle zeigt die Beschränkungen für die Übermittlung von Kennungen nach Produkt und Berechtigungsebene. Für jedes Produkt ist die monatliche Obergrenze der niedrigere von zwei Werten: eine feste Kennungsobergrenze oder ein prozentualer Schwellenwert, der an Ihr lizenziertes Datenvolumen gebunden ist.

| Produkt | Beschreibung der Berechtigung | Monatliche Obergrenze (je nachdem, welcher Wert niedriger ist) |
|----------|-------------------------|---------------------------------|
| Real-Time CDP oder Adobe Journey Optimizer | Ohne Privacy and Security Shield oder Healthcare Shield-Add-on | 2.000.000 Kennungen oder 5 % der adressierbaren Zielgruppe |
| Real-Time CDP oder Adobe Journey Optimizer | Mit dem Add-on Privacy and Security Shield oder Healthcare Shield | 15.000.000 Kennungen oder 10 % der adressierbaren Zielgruppe |
| Customer Journey Analytics | Ohne Privacy and Security Shield oder Healthcare Shield-Add-on | 2.000.000 Kennungen oder 100 Kennungen pro Million CJA-Berechtigungszeilen |
| Customer Journey Analytics | Mit dem Add-on Privacy and Security Shield oder Healthcare Shield | 15.000.000 Kennungen oder 200 Kennungen pro Million CJA-Berechtigungszeilen |

>[!NOTE]
>
>Die meisten Unternehmen verfügen über niedrigere monatliche Limits, die auf ihren tatsächlichen adressierbaren Zielgruppen- oder CJA-Zeilenberechtigungen basieren.

>[!NOTE]
>
>Die Kontingente werden am ersten Tag jedes Kalendermonats zurückgesetzt. Nicht verwendetes Kontingent wird **nicht** übertragen.

>[!NOTE]
>
>Die Kontingentnutzung basiert auf der lizenzierten monatlichen Berechtigung Ihres Unternehmens für **übermittelte Kennungen**. Die Kontingente werden von den Systemleitplanken nicht durchgesetzt, können jedoch überwacht und überprüft werden.\
>Die Kapazität des Arbeitsauftrags zum Löschen von Datensätzen ist ein **freigegebener Dienst**. Die monatliche Obergrenze spiegelt die höchsten Berechtigungen für Real-Time CDP, Adobe Journey Optimizer, Customer Journey Analytics und alle anwendbaren Shield-Add-ons wider.

### Zeitleisten für die Übermittlung von Identifikatoren {#sla-processing-timelines}

Nach der Übermittlung werden die Löschaufträge für Datensätze basierend auf Ihrer Berechtigungsstufe in die Warteschlange gestellt und verarbeitet.

| Produkt- und Berechtigungsbeschreibung | Warteschlangendauer | Maximale Verarbeitungszeit (SLA) |
|------------------------------------|---------------------|-------------------------------|
| Ohne Privacy and Security Shield oder Healthcare Shield-Add-on | Bis zu 15 Tage | 30 Tage |
| Mit dem Add-on Privacy and Security Shield oder Healthcare Shield | In der Regel 24 Stunden | 15 Tage |

Wenn für Ihr Unternehmen höhere Limits erforderlich sind, wenden Sie sich zur Überprüfung der Berechtigungen an den Adobe-Support.

>[!TIP]
>
>Informationen zur aktuellen Kontingentnutzung oder Berechtigungsstufe finden Sie im [Kontingentreferenzhandbuch](../api/quota.md).

## Löschen von Arbeitsaufträgen auflisten {#list}

Rufen Sie eine paginierte Liste von Datensatz-Löscharbeitsaufträgen für Datenhygienevorgänge in Ihrer Organisation ab. Filtern Sie Ergebnisse mithilfe von Abfrageparametern. Jeder Arbeitsauftragsdatensatz enthält den Aktionstyp (z. B. `identity-delete`), den Status, den zugehörigen Datensatz und Benutzerdetails sowie Auditmetadaten.

**API-Format**

```http
GET /workorder
```

In der folgenden Tabelle werden die Abfrageparameter beschrieben, die für die Auflistung von Löschaufträgen für Datensätze verfügbar sind.

| Abfrageparameter | Beschreibung |
| --------------- | ------------|
| `search` | Teilübereinstimmung (Platzhaltersuche) ohne Unterscheidung der Groß-/Kleinschreibung in Feldern: Autor, displayName, Beschreibung oder datasetName. Entspricht auch der exakten Gültigkeits-ID. |
| `type` | Ergebnisse nach Arbeitsauftragstyp filtern (z. B. `identity-delete`). |
| `status` | Liste der Arbeitsauftragsstatus (durch Kommata getrennt) Bei Statuswerten wird zwischen Groß- und Kleinschreibung unterschieden.<br>Aufzählung: `received`, `validated`, `submitted`, `ingested`, `completed`, `failed` |
| `author` | Suchen Sie die Person, die den Arbeitsauftrag zuletzt aktualisiert hat (oder die ursprüngliche Erstellerin bzw. den ursprünglichen Ersteller). Akzeptiert ein Literal- oder SQL-Muster. |
| `displayName` | Übereinstimmung mit dem Anzeigenamen des Arbeitsauftrags, bei der nicht zwischen Groß- und Kleinschreibung unterschieden wird. |
| `description` | Übereinstimmung bei Arbeitsauftragsbeschreibung ohne Unterscheidung von Groß- und Kleinschreibung. |
| `workorderId` | Exakte Übereinstimmung für Arbeitsauftrags-ID. |
| `sandboxName` | Exakte Übereinstimmung für den in der Anfrage verwendeten Sandbox-Namen oder Verwendung von `*` zum Einschließen aller Sandboxes. |
| `fromDate` | Filtern Sie nach Arbeitsaufträgen, die am oder nach diesem Datum erstellt wurden. Erfordert die Einstellung von `toDate`. |
| `toDate` | Filtern Sie nach Arbeitsaufträgen, die am oder vor diesem Datum erstellt wurden. Erfordert die Einstellung von `fromDate`. |
| `filterDate` | Gibt nur Arbeitsaufträge zurück, die zu diesem Datum erstellt, aktualisiert oder geändert wurden. |
| `page` | Zurückzugebender Seitenindex (beginnt bei 0). |
| `limit` | Maximale Ergebnisse pro Seite (1-100, Standard: 25). |
| `orderBy` | Sortierreihenfolge der Ergebnisse. Verwenden Sie `+` oder `-` Präfix für aufsteigende/absteigende Darstellung. Beispiel: `orderBy=-datasetName`. |
| `properties` | Durch Kommas getrennte Liste zusätzlicher Felder, die pro Ergebnis enthalten sein sollen. Optional. |


**Anfrage**

Mit der folgenden Anfrage werden alle abgeschlossenen Datensatz-Löscharbeitsaufträge abgerufen, die auf zwei pro Seite beschränkt sind:

```shell
curl -X GET \
  "https://platform.adobe.io/data/core/hygiene/workorder?status=completed&limit=2" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine paginierte Liste von Löscharbeitsaufträgen für Datensätze zurück.

```json
{
  "results": [
    {
      "workorderId": "DI-1729d091-b08b-47f4-923f-6a4af52c93ac",
      "orgId": "9C1F2AC143214567890ABCDE@AcmeOrg",
      "bundleId": "BN-4cfabf02-c22a-45ef-b21f-bd8c3d631f41",
      "action": "identity-delete",
      "createdAt": "2034-03-15T11:02:10.935Z",
      "updatedAt": "2034-03-15T11:10:10.938Z",
      "operationCount": 3,
      "targetServices": [
        "profile",
        "datalake",
        "identity"
      ],
      "status": "received",
      "createdBy": "a.stark@acme.com <a.stark@acme.com> BD8C3D631F41@acme.com",
      "datasetId": "a7b7c8f3a1b8457eaa5321ab",
      "datasetName": "Acme_Customer_Exports",
      "displayName": "Customer Identity Delete Request",
      "description": "Scheduled identity deletion for compliance"
    }
  ],
  "total": 1,
  "count": 1,
  "_links": {
    "next": {
      "href": "https://platform.adobe.io/workorder?page=1&limit=2",
      "templated": false
    },
    "page": {
      "href": "https://platform.adobe.io/workorder?limit={limit}&page={page}",
      "templated": true
    }
  }
}
```

In der folgenden Tabelle werden die Eigenschaften in der Antwort beschrieben.

| Eigenschaft | Beschreibung |
| --- | --- |
| `results` | Array von Datensatzlöschobjekten für Arbeitsaufträge. Jedes -Objekt enthält die folgenden Felder. |
| `workorderId` | Die eindeutige Kennung für den Löscharbeitsauftrag des Datensatzes. |
| `orgId` | Ihre eindeutige Organisationskennung. |
| `bundleId` | Die eindeutige Kennung des Bundles, das diesen Löscharbeitsauftrag für den Datensatz enthält. Durch die Bündelung können mehrere Löschaufträge gruppiert und von nachgelagerten Services gemeinsam verarbeitet werden. |
| `action` | Der im Arbeitsauftrag angeforderte Aktionstyp. |
| `createdAt` | Der Zeitstempel, wann der Arbeitsauftrag erstellt wurde. |
| `updatedAt` | Der Zeitstempel, wann der Arbeitsauftrag zuletzt aktualisiert wurde. |
| `operationCount` | Die Anzahl der Vorgänge, die im Arbeitsauftrag enthalten sind. |
| `targetServices` | Liste der Ziel-Services für den Arbeitsauftrag. |
| `status` | Aktueller Status des Arbeitsauftrags. Mögliche Werte sind: `received`, `validated`, `submitted`, `ingested`, `completed` und `failed`. |
| `createdBy` | Die E-Mail-Adresse und die Kennung des Benutzers, der den Arbeitsauftrag erstellt hat. |
| `datasetId` | Die eindeutige Kennung für den Datensatz, der mit dem Arbeitsauftrag verknüpft ist. Wenn die Anfrage für alle Datensätze gilt, wird dieses Feld auf ALLE gesetzt. |
| `datasetName` | Der Name des Datensatzes, der mit dem Arbeitsauftrag verknüpft ist. |
| `displayName` | Eine für Menschen lesbare Beschriftung für den Arbeitsauftrag. |
| `description` | Eine Beschreibung des Zwecks des Arbeitsauftrags. |
| `total` | Gesamtzahl der Löschaufträge für Datensätze, die mit der Abfrage übereinstimmen. |
| `count` | Anzahl der Löschaufträge für Datensätze auf der aktuellen Seite. |
| `_links` | Paginierung und Navigations-Links. |
| `next` | Objekt mit `href` (Zeichenfolge) und `templated` (boolesch) für die nächste Seite. |
| `page` | Objekt mit `href` (Zeichenfolge) und `templated` (Boolesch) für die Seitennavigation. |

{style="table-layout:auto"}

## Erstellen eines Arbeitsauftrags zum Löschen eines Datensatzes {#create}

Um Datensätze, die mit einer oder mehreren Identitäten verknüpft sind, aus einem einzelnen Datensatz oder allen Datensätzen zu löschen, stellen Sie eine POST-Anfrage an den `/workorder`-Endpunkt.

Arbeitsaufträge werden asynchron verarbeitet und nach der Übermittlung in der Arbeitsauftragsliste angezeigt.

>[!TIP]
>
>Jeder über die API gesendete Arbeitsauftrag zum Löschen von Datensätzen kann bis zu **100.000 Identitäten**. Senden Sie so viele Identitäten pro Anfrage wie möglich, um die Effizienz zu maximieren. Vermeiden Sie kleinvolumige Übermittlungen wie Arbeitsaufträge mit einer einzigen ID.

**API-Format**

```http
POST /workorder
```

>[!NOTE]
>
>Sie können nur Datensätze aus Datensätzen löschen, deren verknüpftes XDM-Schema eine primäre Identität oder Identitätszuordnung definiert.

>[!NOTE]
>
>Wenn Sie versuchen, einen Arbeitsauftrag zum Löschen eines Datensatzes für einen Datensatz zu erstellen, der bereits eine aktive Gültigkeit hat, gibt die Anfrage HTTP 400 (Fehlerhafte Anfrage) zurück. Eine aktive Gültigkeit ist jede geplante Löschung, die noch nicht abgeschlossen ist.

**Anfrage**

Die folgende Anfrage löscht alle Datensätze, die mit angegebenen E-Mail-Adressen aus einem bestimmten Datensatz verknüpft sind.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "displayName": "Acme Loyalty - Customer Data Deletion",
        "description": "Delete all records associated with the specified email addresses from the Acme_Loyalty_2023 dataset.",
        "action": "delete_identity",
        "datasetId": "7eab61f3e5c34810a49a1ab3",
        "namespacesIdentities": [
          {
            "namespace": {
              "code": "email"
            },
            "IDs": [
              "alice.smith@acmecorp.com",
              "bob.jones@acmecorp.com",
              "charlie.brown@acmecorp.com"
            ]
          }
        ]
      }'
```

In der folgenden Tabelle werden die Eigenschaften zum Erstellen eines Arbeitsauftrags zum Löschen eines Datensatzes beschrieben.

| Eigenschaft | Beschreibung |
| --- | --- |
| `displayName` | Eine menschenlesbare Beschriftung für diesen Datensatz, um einen Arbeitsauftrag zu löschen. |
| `description` | Eine Beschreibung des Arbeitsauftrags zum Löschen des Datensatzes. |
| `action` | Die Aktion, die für den Löscharbeitsauftrag für den Datensatz angefordert wurde. Um Datensätze zu löschen, die mit einer bestimmten Identität verknüpft sind, verwenden Sie `delete_identity`. |
| `datasetId` | Die eindeutige Kennung für den Datensatz. Verwenden Sie die Datensatz-ID für einen bestimmten Datensatz oder `ALL` , um alle Datensätze auszuwählen. Datensätze müssen eine primäre Identität oder Identitätszuordnung aufweisen. Wenn eine Identitätszuordnung vorhanden ist, ist sie als Feld der obersten Ebene mit dem Namen `identityMap` vorhanden.<br>Beachten Sie, dass eine Datensatzzeile viele Identitäten in ihrer Identitätszuordnung haben kann, aber nur eine als primär markiert werden kann. `"primary": true` müssen eingeschlossen werden, damit der `id` mit einer primären Identität übereinstimmt. |
| `namespacesIdentities` | Ein Array von Objekten, die jeweils Folgendes enthalten:<br><ul><li> `namespace`: Ein Objekt mit einer `code` Eigenschaft, die den Identity-Namespace angibt (z. B. „E-Mail„).</li><li> `IDs`: Ein Array von Identitätswerten, die für diesen Namespace gelöscht werden sollen.</li></ul>Identity-Namespaces bieten Kontext zu Identitätsdaten. Sie können die von Experience Platform bereitgestellten Standard-Namespaces verwenden oder eigene erstellen. Weitere Informationen finden Sie in der [Dokumentation zu Identity-Namespaces](../../identity-service/features/namespaces.md) und der [Identity Service API-Spezifikation](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

**Antwort**

Eine erfolgreiche Antwort gibt die Details des neuen Datensatzlöscharbeitsauftrags zurück.

```json
{
  "workorderId": "DI-95c40d52-6229-44e8-881b-fc7f072de63d",
  "orgId": "8B1F2AC143214567890ABCDE@AcmeOrg",
  "bundleId": "BN-c61bec61-5ce8-498f-a538-fb84b094adc6",
  "action": "identity-delete",
  "createdAt": "2035-06-02T09:21:00.000Z",
  "updatedAt": "2035-06-02T09:21:05.000Z",
  "operationCount": 1,
  "targetServices": [
    "profile",
    "datalake",
    "identity"
  ],
  "status": "received",
  "createdBy": "c.lannister@acme.com <c.lannister@acme.com> 7EAB61F3E5C34810A49A1AB3@acme.com",
  "datasetId": "7eab61f3e5c34810a49a1ab3",
  "datasetName": "Acme_Loyalty_2023",
  "displayName": "Loyalty Identity Delete Request",
  "description": "Schedule deletion for Acme loyalty program dataset"
}
```

In der folgenden Tabelle werden die Eigenschaften in der Antwort beschrieben.

| Eigenschaft | Beschreibung |
| --- | --- |
| `workorderId` | Die eindeutige Kennung für den Löscharbeitsauftrag des Datensatzes. Verwenden Sie diesen Wert, um den Status oder die Details der Löschung nachzuschlagen. |
| `orgId` | Ihre eindeutige Organisationskennung. |
| `bundleId` | Die eindeutige Kennung des Bundles, das diesen Löscharbeitsauftrag für den Datensatz enthält. Durch die Bündelung können mehrere Löschaufträge gruppiert und von nachgelagerten Services gemeinsam verarbeitet werden. |
| `action` | Der Aktionstyp, der im Löscharbeitsauftrag für den Datensatz angefordert wurde. |
| `createdAt` | Der Zeitstempel, wann der Arbeitsauftrag erstellt wurde. |
| `updatedAt` | Der Zeitstempel, wann der Arbeitsauftrag zuletzt aktualisiert wurde. |
| `operationCount` | Die Anzahl der Vorgänge, die im Arbeitsauftrag enthalten sind. |
| `targetServices` | Eine Liste der Ziel-Services für den Datensatz-Löscharbeitsauftrag. |
| `status` | Aktueller Status des Datensatzlöscharbeitsauftrags. |
| `createdBy` | Die E-Mail-Adresse und die Kennung des Benutzers, der den Löscharbeitsauftrag für den Datensatz erstellt hat. |
| `datasetId` | Die eindeutige Kennung für den Datensatz. Wenn die Anfrage alle Datensätze betrifft, wird der Wert auf `ALL` gesetzt |
| `datasetName` | Der Name des Datensatzes für diesen Datensatz: Arbeitsauftrag löschen. |
| `displayName` | Eine menschenlesbare Beschriftung für den Arbeitsauftrag zum Löschen von Datensätzen. |
| `description` | Eine Beschreibung des Arbeitsauftrags zum Löschen des Datensatzes. |

{style="table-layout:auto"}

>[!NOTE]
>
>Die Aktionseigenschaft für Löscharbeitsaufträge für Datensätze wird derzeit in API-Antworten `identity-delete`. Wenn die API einen anderen Wert verwendet (z. B. `delete_identity`), wird diese Dokumentation entsprechend aktualisiert.

## Abrufen von Details für einen bestimmten Datensatz zum Löschen von Arbeitsaufträgen {#lookup}

Rufen Sie Informationen zu einem bestimmten Datensatz-Löscharbeitsauftrag ab, indem Sie eine GET-Anfrage an `/workorder/{WORKORDER_ID}` stellen. Die Antwort enthält Aktionstyp, Status, verknüpfte Datensatz- und Benutzerinformationen sowie Audit-Metadaten.

**API-Format**

```http
GET /workorder/{WORKORDER_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{WORK_ORDER_ID}` | Die eindeutige Kennung für den Datensatz-Löscharbeitsauftrag, den Sie suchen. |

{style="table-layout:auto"}

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/DI-6fa98d52-7bd2-42a5-bf61-fb5c22ec9427 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des angegebenen Datensatzlöscharbeitsauftrags zurück.

```json
{
  "workorderId": "DI-6fa98d52-7bd2-42a5-bf61-fb5c22ec9427",
  "orgId": "3C7F2AC143214567890ABCDE@AcmeOrg",
  "bundleId": "BN-dbe3ffad-cb0b-401f-91ae-01c189f8e7b2",
  "action": "identity-delete",
  "createdAt": "2037-01-21T08:25:45.119Z",
  "updatedAt": "2037-01-21T08:30:45.233Z",
  "operationCount": 3,
  "targetServices": [
    "ajo",
    "profile",
    "datalake",
    "identity"
  ],
  "status": "received",
  "createdBy": "g.baratheon@acme.com <g.baratheon@acme.com> C189F8E7B2@acme.com",
  "datasetId": "d2f1c8a4b8f747d0ba3521e2",
  "datasetName": "Acme_Marketing_Events",
  "displayName": "Marketing Identity Delete Request",
  "description": "Scheduled identity deletion for marketing compliance"
}
```

In der folgenden Tabelle werden die Eigenschaften in der Antwort beschrieben.

| Eigenschaft | Beschreibung |
| --- | --- |
| `workorderId` | Die eindeutige Kennung für den Löscharbeitsauftrag des Datensatzes. |
| `orgId` | Die eindeutige Kennung Ihres Unternehmens. |
| `bundleId` | Die eindeutige Kennung des Bundles, das diesen Löscharbeitsauftrag für den Datensatz enthält. Durch die Bündelung können mehrere Löschaufträge gruppiert und von nachgelagerten Services gemeinsam verarbeitet werden. |
| `action` | Der Aktionstyp, der im Löscharbeitsauftrag für den Datensatz angefordert wurde. |
| `createdAt` | Der Zeitstempel, wann der Arbeitsauftrag erstellt wurde. |
| `updatedAt` | Der Zeitstempel, wann der Arbeitsauftrag zuletzt aktualisiert wurde. |
| `operationCount` | Die Anzahl der Vorgänge, die im Arbeitsauftrag enthalten sind. |
| `targetServices` | Eine Liste der Ziel-Services, die von diesem Datensatz betroffen sind, löscht den Arbeitsauftrag. |
| `status` | Der aktuelle Status des Datensatzlöscharbeitsauftrags. |
| `createdBy` | Die E-Mail-Adresse und die Kennung des Benutzers, der den Löscharbeitsauftrag für den Datensatz erstellt hat. |
| `datasetId` | Die eindeutige Kennung für den Datensatz, der mit dem Arbeitsauftrag verknüpft ist. |
| `datasetName` | Der Name des Datensatzes, der mit dem Arbeitsauftrag verknüpft ist. |
| `displayName` | Eine menschenlesbare Beschriftung für den Arbeitsauftrag zum Löschen von Datensätzen. |
| `description` | Eine Beschreibung des Arbeitsauftrags zum Löschen des Datensatzes. |

## Aktualisieren eines Datensatzlöscharbeitsauftrags

Aktualisieren Sie die `name` und `description` für einen Datensatz-Löscharbeitsauftrag, indem Sie eine PUT-Anfrage an den `/workorder/{WORKORDER_ID}`-Endpunkt stellen.

**API-Format**

```http
PUT /workorder/{WORKORDER_ID}
```

Die folgende Tabelle beschreibt den Parameter für diese Anfrage.

| Parameter | Beschreibung |
| --- | --- |
| `{WORK_ORDER_ID}` | Die eindeutige Kennung für den Datensatz-Löscharbeitsauftrag, den Sie aktualisieren möchten. |

{style="table-layout:auto"}

**Anfrage**

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/workorder/DI-893a6b1d-47c2-41e1-b3f1-2d7c2956aabb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Updated Marketing Identity Delete Request",
        "description": "Updated deletion request for marketing data"
      }'
```

In der folgenden Tabelle werden die Eigenschaften beschrieben, die Sie aktualisieren können.

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Die aktualisierte, für Menschen lesbare Bezeichnung für den Löscharbeitsauftrag des Datensatzes. |
| `description` | Die aktualisierte Beschreibung für den Arbeitsauftrag zum Löschen des Datensatzes. |

{style="table-layout:auto"}

**Antwort**

Eine erfolgreiche Antwort gibt die aktualisierte Arbeitsauftragsanfrage zurück.

```json
{
  "workorderId": "DI-893a6b1d-47c2-41e1-b3f1-2d7c2956aabb",
  "orgId": "7D4E2AC143214567890ABCDE@AcmeOrg",
  "bundleId": "BN-12abcf45-32ea-45bc-9d1c-8e7b321cabc8",
  "action": "identity-delete",
  "createdAt": "2038-04-15T12:14:29.210Z",
  "updatedAt": "2038-04-15T12:30:29.442Z",
  "operationCount": 2,
  "targetServices": [
    "profile",
    "datalake"
  ],
  "status": "received",
  "createdBy": "b.tarth@acme.com <b.tarth@acme.com> 8E7B321CABC8@acme.com",
  "datasetId": "1a2b3c4d5e6f7890abcdef12",
  "datasetName": "Acme_Marketing_2024",
  "displayName": "Updated Marketing Identity Delete Request",
  "description": "Updated deletion request for marketing data",
  "productStatusDetails": [
        {
            "productName": "Data Management",
            "productStatus": "waiting",
            "createdAt": "2024-06-12T20:11:18.447747Z"
        },
        {
            "productName": "Identity Service",
            "productStatus": "success",
            "createdAt": "2024-06-12T20:36:09.020832Z"
        },
        {
            "productName": "Profile Service",
            "productStatus": "waiting",
            "createdAt": "2024-06-12T20:11:18.447747Z"
        },
        {
            "productName": "Journey Orchestrator",
            "productStatus": "success",
            "createdAt": "2024-06-12T20:12:19.843199Z"
        }
    ]
}
```

| Eigenschaft | Beschreibung |
| ---------------- | ----------------------------------------------------------------------------------------- |
| `workorderId` | Die eindeutige Kennung für den Löscharbeitsauftrag des Datensatzes. |
| `orgId` | Die eindeutige Kennung Ihres Unternehmens. |
| `bundleId` | Die eindeutige Kennung des Bundles, das diesen Löscharbeitsauftrag für den Datensatz enthält. Durch die Bündelung können mehrere Löschaufträge gruppiert und von nachgelagerten Services gemeinsam verarbeitet werden. |
| `action` | Der Aktionstyp, der im Löscharbeitsauftrag für den Datensatz angefordert wurde. |
| `createdAt` | Der Zeitstempel, wann der Arbeitsauftrag erstellt wurde. |
| `updatedAt` | Der Zeitstempel, wann der Arbeitsauftrag zuletzt aktualisiert wurde. |
| `operationCount` | Die Anzahl der Vorgänge, die im Arbeitsauftrag enthalten sind. |
| `targetServices` | Eine Liste der Ziel-Services, die von diesem Datensatz betroffen sind, löscht den Arbeitsauftrag. |
| `status` | Der aktuelle Status des Datensatzlöscharbeitsauftrags. Mögliche Werte sind: `received`, `validated`, `submitted`, `ingested`, `completed` und `failed`. |
| `createdBy` | Die E-Mail-Adresse und die Kennung des Benutzers, der den Löscharbeitsauftrag für den Datensatz erstellt hat. |
| `datasetId` | Die eindeutige Kennung für den Datensatz, der mit dem Arbeitsauftrag zum Löschen des Datensatzes verknüpft ist. |
| `datasetName` | Der Name des Datensatzes, der mit dem Arbeitsauftrag zum Löschen des Datensatzes verknüpft ist. |
| `displayName` | Eine menschenlesbare Beschriftung für den Arbeitsauftrag zum Löschen von Datensätzen. |
| `description` | Eine Beschreibung des Arbeitsauftrags zum Löschen des Datensatzes. |
| `productStatusDetails` | Ein Array, das den aktuellen Status der nachgelagerten Prozesse für die Anfrage auflistet. Jedes Objekt enthält:<ul><li>`productName`: Name des nachgelagerten Services.</li><li>`productStatus`: Der aktuelle Verarbeitungsstatus vom nachgelagerten Service.</li><li>`createdAt`: Der Zeitstempel, zu dem der letzte Status von dem Service veröffentlicht wurde.</li></ul>Diese Eigenschaft ist verfügbar, nachdem der Arbeitsauftrag an nachgelagerte Services übermittelt wurde, um mit der Verarbeitung zu beginnen. |

{style="table-layout:auto"}
