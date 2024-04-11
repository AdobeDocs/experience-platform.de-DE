---
title: Quoten-API-Endpunkt
description: Mit dem Endpunkt /quota in der Data Hygiene API können Sie die Nutzung des erweiterten Data Lifecycle Managements anhand der monatlichen Quotenbegrenzungen Ihres Unternehmens für jeden Auftragstyp überwachen.
role: Developer
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: 48a83e2b615fc9116a93611a5e6a8e7f78cb4dee
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 29%

---

# Quoten-Endpunkt

Die `/quota` -Endpunkt in der Data Hygiene API können Sie die Nutzung des erweiterten Data Lifecycle Managements anhand der Quotenbegrenzungen überwachen, die Ihr Unternehmen für jeden Auftragstyp vorgibt.

Für jeden Auftragstyp des Lebenszyklus werden Quoten wie folgt erzwungen:

* Löschungen und Aktualisierungen von Datensätzen sind auf eine bestimmte Anzahl von Anforderungen pro Monat beschränkt.
* Datensatzabläufe haben ein pauschales Limit für die Anzahl der gleichzeitig aktiven Vorgänge, und zwar unabhängig davon, wann die Abläufe ausgeführt werden.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der Data Hygiene API. Bevor Sie fortfahren, lesen Sie eine [Übersicht](./overview.md) zu folgenden Themen:

* Links zur entsprechenden Dokumentation
* Eine Anleitung zum Lesen der Beispiel-API-Aufrufe in diesem Dokument
* Wichtige Informationen zu den erforderlichen Kopfzeilen, die zum Aufrufen von Experience Platform-APIs benötigt werden

## Aufrufen von Kontingenten {#list}

Sie können die Kontingentinformationen Ihres Unternehmens anzeigen, indem Sie eine GET-Anfrage an den `/quota`-Endpunkt senden.

**API-Format**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

| Parameter | Beschreibung |
| --- | --- |
| `{QUOTA_TYPE}` | Ein optionaler Abfrageparameter, der den Typ des abzurufenden Kontingents angibt. Wenn kein `quotaType`-Parameter angegeben ist, werden alle Kontingentwerte in der API-Antwort zurückgegeben. Zu den akzeptierten Typwerten gehören:<ul><li>`datasetExpirationQuota`: Dieses Objekt zeigt die Anzahl der gleichzeitig aktiven Datensatzabläufe für Ihre Organisation und Ihre Gesamtablaufzeit an. </li><li>`dailyConsumerDeleteIdentitiesQuota`: Dieses Objekt zeigt die Gesamtzahl der Löschanfragen von Datensätzen, die Ihre Organisation heute gestellt hat, und Ihr Tagegeld insgesamt an.<br>Hinweis: Es werden nur akzeptierte Anforderungen gezählt. Wenn ein Arbeitsauftrag abgelehnt wird, weil die Validierung fehlschlägt, werden diese Identitätslöschungen nicht mit Ihrem Kontingent angerechnet.</li><li>`monthlyConsumerDeleteIdentitiesQuota`: Dieses Objekt zeigt die Gesamtzahl der Löschanfragen von Datensätzen, die in diesem Monat von Ihrer Organisation gestellt wurden, und Ihre monatliche Gesamtanzahl an.</li><li>`monthlyUpdatedFieldIdentitiesQuota`: Dieses Objekt zeigt die Gesamtzahl der in diesem Monat von Ihrer Organisation gestellten Anfragen zur Datensatzaktualisierung und Ihre monatliche Gesamtanzahl an.</li></ul> |

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

Eine erfolgreiche Antwort gibt die Details Ihrer Datenlebenszyklusquoten zurück.

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
| `quotas` | Listet die Quoteninformationen für jeden Auftragstyp des Datenlebenszyklus auf. Jedes Kontingentobjekt enthält die folgenden Eigenschaften:<ul><li>`name`: Der Auftragstyp des Datenlebenszyklus:<ul><li>`expirationDatasetQuota`: Datensatzgültigkeiten</li><li>`deleteIdentityWorkOrderDatasetQuota`: Löschen von Datensätzen</li></ul></li><li>`description`: Eine Beschreibung des Auftragstyps für den Datenlebenszyklus.</li><li>`consumed`: Die Anzahl der Aufträge dieses Typs wird im aktuellen Zeitraum ausgeführt. Der Objektname gibt den Quotenzeitraum an.</li><li>`quota`: Die Zuweisung für diesen Auftragstyp für Ihre Organisation. Bei Löschungen und Aktualisierungen von Datensätzen stellt das Kontingent die Anzahl der Aufträge dar, die für jeden monatlichen Zeitraum ausgeführt werden können. Bei Datensatzabläufen stellt das Kontingent die Anzahl der Aufträge dar, die gleichzeitig aktiv sein können.</li></ul> |

{style="table-layout:auto"}
