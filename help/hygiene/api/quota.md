---
title: Quoten-API-Endpunkt
description: Mit dem Endpunkt /quota in der Data Hygiene API können Sie die Nutzung des erweiterten Data Lifecycle Managements anhand der monatlichen Quotenbegrenzungen Ihres Unternehmens für jeden Auftragstyp überwachen.
role: Developer
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 57%

---

# Quoten-Endpunkt

Die `/quota` -Endpunkt in der Data Hygiene API ermöglicht es Ihnen, die Nutzung des erweiterten Data Lifecycle Managements anhand der Quotenbegrenzungen Ihres Unternehmens für jeden Auftragstyp zu überwachen.

Für jeden Auftragstyp des Datenlebenszyklus werden Quoten wie folgt erzwungen:

* Löschungen und Aktualisierungen von Datensätzen sind auf eine bestimmte Anzahl von Anforderungen pro Monat beschränkt.
* Datensatzabläufe haben ein pauschales Limit für die Anzahl der gleichzeitig aktiven Vorgänge, und zwar unabhängig davon, wann die Abläufe ausgeführt werden.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der Data Hygiene API. Bevor Sie fortfahren, lesen Sie eine [Übersicht](./overview.md) zu folgenden Themen:

* Links zur entsprechenden Dokumentation
* Eine Anleitung zum Lesen der Beispiel-API-Aufrufe in diesem Dokument
* Wichtige Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen von Experience Platform-APIs benötigt werden

## Aufrufen von Kontingenten {#list}

Sie können die Kontingentinformationen Ihres Unternehmens anzeigen, indem Sie eine GET-Anfrage an den `/quota`-Endpunkt senden.

**API-Format**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

| Parameter | Beschreibung |
| --- | --- |
| `{QUOTA_TYPE}` | Ein optionaler Abfrageparameter, der den Typ des abzurufenden Kontingents angibt. Wenn kein `quotaType`-Parameter angegeben ist, werden alle Kontingentwerte in der API-Antwort zurückgegeben. Zu den akzeptierten Typwerten gehören:<ul><li>`expirationDatasetQuota`: Datensatzgültigkeiten</li><li>`deleteIdentityWorkOrderDatasetQuota`: Löschen von Datensätzen</li><li>`fieldUpdateWorkOrderDatasetQuota`: Aktualisierungen der Datensätze</li></ul> |

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
      "name": "expirationDatasetQuota",
      "description": "The number of concurrently active Expiration Dataset Delete Work Order requests for the organization.",
      "consumed": 3154,
      "quota": 10000
    },
    {
      "name": "deleteIdentityWorkOrderQuota",
      "description": "The number of Record Delete Work Order requests for the organization for this month.",
      "consumed": 390,
      "quota": 10000
    }
  ]
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `quotas` | Listet die Quoteninformationen für jeden Auftragstyp des Datenlebenszyklus auf. Jedes Kontingentobjekt enthält die folgenden Eigenschaften:<ul><li>`name`: Der Auftragstyp des Datenlebenszyklus:<ul><li>`expirationDatasetQuota`: Datensatzgültigkeiten</li><li>`deleteIdentityWorkOrderDatasetQuota`: Löschen von Datensätzen</li></ul></li><li>`description`: Eine Beschreibung des Auftragstyps für den Datenlebenszyklus.</li><li>`consumed`: Die Anzahl der Vorgänge dieses Typs, die im aktuellen Monatszeitraum ausgeführt wird.</li><li>`quota`: Die Kontingentbegrenzung für diesen Vorgangstyp. Bei Datensatzlöschungen und -aktualisierungen stellt dies die Anzahl der Aufträge dar, die für jeden monatlichen Zeitraum ausgeführt werden können. Bei Datensatzabläufen stellt dies die Anzahl der Vorgänge dar, die gleichzeitig aktiv sein können.</li></ul> |

{style="table-layout:auto"}
