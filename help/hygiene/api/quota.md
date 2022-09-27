---
title: Quota-API-Endpunkt
description: Mit dem /quota -Endpunkt in der Data Hygiene API können Sie die Nutzung Ihrer Daten in Bezug auf die hygienischen Bedingungen in Ihrem Unternehmen anhand der monatlichen Quotenbegrenzungen für jeden Auftragstyp überwachen.
source-git-commit: 364ada0c354ddba8a855945f4f806f5600f21416
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 13%

---

# Endpunkt &quot;Kontingent&quot;

>[!IMPORTANT]
>
>Die Datenhygiene-Funktionen in Adobe Experience Platform sind derzeit nur für Organisationen verfügbar, die Healthcare Shield erworben haben.

Die `/quota` -Endpunkt in der Data Hygiene API ermöglicht es Ihnen, die Nutzung Ihrer Daten in Bezug auf die Hygiene-Nutzung anhand der Quotenbegrenzungen Ihres Unternehmens für jeden Auftragstyp zu überwachen.

Die Quotenerzwingung erfolgt für jeden Auftragstyp im Bereich Datenhygiene wie folgt:

* Benutzerdefinierte Löschvorgänge und Feldaktualisierungen sind auf eine bestimmte Anzahl von Anforderungen pro Monat beschränkt.
* Die Datensatzabläufe haben eine feste Begrenzung für die Anzahl der gleichzeitig aktiven Aufträge, unabhängig davon, wann die Abläufe ausgeführt werden.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der Data Hygiene API. Bevor Sie fortfahren, lesen Sie bitte die [Übersicht](./overview.md) für die folgenden Informationen:

* Links zur zugehörigen Dokumentation
* Eine Anleitung zum Lesen der Beispiel-API-Aufrufe in diesem Dokument
* Wichtige Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen von Experience Platform-APIs benötigt werden

## Kontingente auflisten {#list}

Sie können die Quoteninformationen Ihres Unternehmens anzeigen, indem Sie eine GET-Anfrage an die `/quota` -Endpunkt.

**API-Format**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

| Parameter | Beschreibung |
| --- | --- |
| `{QUOTA_TYPE}` | Ein optionaler Abfrageparameter, der den Typ des abzurufenden Kontingents angibt. Wenn nicht `quotaType` angegeben ist, werden alle Quotenwerte in der API-Antwort zurückgegeben. Zu den akzeptierten Typwerten gehören:<ul><li>`expirationDatasetQuota`: Datensatzgültigkeiten</li><li>`deleteIdentityWorkOrderDatasetQuota`: Löschen von Verbrauchern</li><li>`fieldUpdateWorkOrderDatasetQuota`: Feldaktualisierungen</li></ul> |

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

Bei einer erfolgreichen Antwort werden die Details Ihrer Datenhygienekosten zurückgegeben.

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
      "description": "The number of Consumer Delete Work Order requests for the organization for this month.",
      "consumed": 390,
      "quota": 10000
    }
  ]
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `quotas` | Listet die Quoteninformationen für jeden Datentyp im Hygienebereich auf. Jedes Quotenobjekt enthält die folgenden Eigenschaften:<ul><li>`name`: Arbeitstyp für den Datenhygiene:<ul><li>`expirationDatasetQuota`: Datensatzgültigkeiten</li><li>`deleteIdentityWorkOrderDatasetQuota`: Löschen von Verbrauchern</li></ul></li><li>`description`: Eine Beschreibung des Auftragstyps für die Datenhygiene.</li><li>`consumed`: Die Anzahl der Aufträge dieses Typs wird im aktuellen Monatszeitraum ausgeführt.</li><li>`quota`: Die Quotenbegrenzung für diesen Auftragstyp. Bei Benutzerlöschungen und Feldaktualisierungen stellt dies die Anzahl der Aufträge dar, die für jeden monatlichen Zeitraum ausgeführt werden können. Bei Datensatzabläufen stellt dies die Anzahl der Aufträge dar, die gleichzeitig aktiv sein können.</li></ul> |

{style=&quot;table-layout:auto&quot;}
