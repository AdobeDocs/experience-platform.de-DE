---
title: Quoten-API-Endpunkt
description: Mit dem /quota-Endpunkt in der Data Hygiene API können Sie die Nutzung des erweiterten Daten-Lifecycle-Managements in Bezug auf die in Ihrem Unternehmen gültigen monatlichen Quotenbegrenzungen für jeden Vorgangstyp überwachen.
role: Developer
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: 48a83e2b615fc9116a93611a5e6a8e7f78cb4dee
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 29%

---

# Quoten-Endpunkt

Der `/quota`-Endpunkt in der Data Hygiene API ermöglicht es Ihnen, die Nutzung Ihres erweiterten Data Lifecycle Management in Bezug auf die Quotenbegrenzungen Ihres Unternehmens für jeden Vorgangstyp zu überwachen.

Die Kontingente werden für jeden Data Lifecycle-Vorgangstyp wie folgt durchgesetzt:

* Löschvorgänge und Aktualisierungen von Datensätzen sind auf eine bestimmte Anzahl von Anfragen pro Monat beschränkt.
* Datensatzabläufe haben ein pauschales Limit für die Anzahl der gleichzeitig aktiven Vorgänge, und zwar unabhängig davon, wann die Abläufe ausgeführt werden.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der Data Hygiene API. Bevor Sie fortfahren, lesen Sie eine [Übersicht](./overview.md) zu folgenden Themen:

* Links zur entsprechenden Dokumentation
* Eine Anleitung zum Lesen der Beispiel-API-Aufrufe in diesem Dokument
* Wichtige Informationen zu den erforderlichen Kopfzeilen, die für Aufrufe an eine Experience Platform-API erforderlich sind

## Aufrufen von Kontingenten {#list}

Sie können die Kontingentinformationen Ihres Unternehmens anzeigen, indem Sie eine GET-Anfrage an den `/quota`-Endpunkt senden.

**API-Format**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

| Parameter | Beschreibung |
| --- | --- |
| `{QUOTA_TYPE}` | Ein optionaler Abfrageparameter, der den Typ des abzurufenden Kontingents angibt. Wenn kein `quotaType`-Parameter angegeben ist, werden alle Kontingentwerte in der API-Antwort zurückgegeben. Zu den akzeptierten Typwerten gehören:<ul><li>`datasetExpirationQuota`: Dieses Objekt zeigt die Anzahl der gleichzeitig aktiven Datensatzgültigkeiten für Ihre Organisation sowie Ihr Gesamtlimit an Gültigkeiten an. </li><li>`dailyConsumerDeleteIdentitiesQuota`: Dieses Objekt zeigt die Gesamtzahl der Löschanfragen für Datensätze an, die von Ihrer Organisation heute gestellt wurden, und das Tagegeld insgesamt.<br>Hinweis: Es werden nur akzeptierte Anfragen gezählt. Wenn ein Arbeitsauftrag abgelehnt wird, weil die Validierung fehlschlägt, werden diese Identitätslöschungen nicht auf Ihr Kontingent angerechnet.</li><li>`monthlyConsumerDeleteIdentitiesQuota`: Dieses Objekt zeigt die Gesamtzahl der Löschanfragen für Datensätze an, die von Ihrer Organisation in diesem Monat gestellt wurden, und das gesamte monatliche Taschengeld.</li><li>`monthlyUpdatedFieldIdentitiesQuota`: Dieses Objekt zeigt die Gesamtzahl der Anfragen zur Aktualisierung von Datensätzen an, die von Ihrer Organisation in diesem Monat gestellt wurden, und Ihre gesamte monatliche Vergütung.</li></ul> |

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/quota \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details Ihrer Datenlebenszykluskontingente zurück.

```json
{
  "quotas": [
    {
      "name": "datasetExpirationQuota",
      "description": "The number of concurrently active Expiration Dataset Delete in all workorder requests for the organization.",
      "consumed": 12,
      "quota": 50
    },
    {
      "name": "dailyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all workorder requests for the organization for today.",
      "consumed": 0,
      "quota": 600000
    },
    {
      "name": "monthlyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all workorder requests for the organization for this month.",
      "consumed": 841,
      "quota": 600000
    },
    {
      "name": "monthlyUpdatedFieldIdentitiesQuota",
      "description": "The consumed number of updated identities in all workorder requests for the organization for this month.",
      "consumed": 0,
      "quota": 0
    }
  ]
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `quotas` | Listet die Kontingentinformationen für jeden Datenlebenszyklus-Vorgangstyp auf. Jedes Kontingentobjekt enthält die folgenden Eigenschaften:<ul><li>`name`: Der Datenlebenszyklus-Vorgangstyp:<ul><li>`expirationDatasetQuota`: Datensatzgültigkeiten</li><li>`deleteIdentityWorkOrderDatasetQuota`: Löschen von Datensätzen</li></ul></li><li>`description`: Eine Beschreibung des Datenlebenszyklus-Vorgangstyps.</li><li>`consumed`: Die Anzahl der Vorgänge dieses Typs, die im aktuellen Zeitraum ausgeführt wird. Der Objektname gibt den Kontingentzeitraum an.</li><li>`quota`: Die Zuteilung für diesen Vorgangstyp für Ihre Organisation. Beim Löschen und Aktualisieren von Datensätzen stellt das Kontingent die Anzahl der Aufträge dar, die für jeden Monatszeitraum ausgeführt werden können. Bei Datensatzgültigkeiten stellt das Kontingent die Anzahl der Aufträge dar, die gleichzeitig aktiv sein können.</li></ul> |

{style="table-layout:auto"}
