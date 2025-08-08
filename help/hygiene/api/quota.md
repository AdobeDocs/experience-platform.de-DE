---
title: Quoten-API-Endpunkt
description: Mit dem /quota-Endpunkt in der Data Hygiene API können Sie die Nutzung des erweiterten Daten-Lifecycle-Managements in Bezug auf die in Ihrem Unternehmen gültigen monatlichen Quotenbegrenzungen für jeden Vorgangstyp überwachen.
role: Developer
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: 2c2907c5ed38ce4c87b1b73f96e1a0e64586cb97
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 23%

---

# Quoten-Endpunkt

Verwenden Sie den `/quota`-Endpunkt in der Datenhygiene-API, um die aktuelle Nutzung und die aktuellen Einschränkungen Ihres Unternehmens zu überprüfen. Die Quoten variieren je nach Berechtigungen, z. B. Privacy and Security Shield oder Healthcare Shield.

Überwachen Sie die aktuelle Kontingentnutzung, um die Einhaltung der organisatorischen Limits für jeden Vorgangstyp sicherzustellen.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der Data Hygiene API. Bevor Sie fortfahren, lesen Sie eine [Übersicht](./overview.md) zu folgenden Themen:

* Links zur zugehörigen Dokumentation
* Lesen von Beispiel-API-Aufrufen
* Erforderliche Kopfzeilen für Experience Platform-API-Aufrufe

## Kontingente und Verarbeitungszeitpläne {#quotas}

Löschanfragen für Datensätze unterliegen Kontingenten und Service-Level-Erwartungen, die auf Ihrer Lizenzberechtigung basieren. Diese Einschränkungen gelten sowohl für benutzeroberflächen- als auch für API-basierte Löschanfragen.

>[!TIP]
>
>In diesem Dokument erfahren Sie, wie Sie Ihre Nutzung anhand von berechtigungsbasierten Beschränkungen abfragen können. Eine vollständige Beschreibung der Kontingentebenen, der Berechtigungen zum Löschen von Datensätzen und des SLA-Verhaltens finden Sie unter [UI-basiertes Löschen von Datensätzen](../ui/record-delete.md#quotas) oder [API-basiertes Löschen von Datensätzen](./workorder.md#quotas).

## Aufrufen von Kontingenten {#list}

Sie können die Kontingentinformationen Ihres Unternehmens anzeigen, indem Sie eine GET-Anfrage an den `/quota`-Endpunkt senden.

**API-Format**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

>[!NOTE]
>
>Der Kontingentverbrauch wird täglich und monatlich am 1. eines jeden Monats um 0:00 :00 GMT zurückgesetzt.
>
>Nur akzeptierte Anfragen zählen für Ihr Kontingent. Abgelehnte Arbeitsaufträge reduzieren Ihr Kontingent nicht.

| Parameter | Beschreibung |
| --- | --- |
| `{QUOTA_TYPE}` | Ein optionaler Abfrageparameter, der den Typ des abzurufenden Kontingents angibt. Wenn kein `quotaType`-Parameter angegeben ist, werden alle Kontingentwerte in der API-Antwort zurückgegeben. Zu den akzeptierten Werten gehören:<ul><li>`datasetExpirationQuota`: Die Anzahl der aktiven Datensatzgültigkeiten und Ihr Gesamtlimit.</li><li>`dailyConsumerDeleteIdentitiesQuota`: Die Anzahl der heute gelöschten Datensätze und Ihr tägliches Kontingent.</li><li>`monthlyConsumerDeleteIdentitiesQuota`: Die Anzahl der in diesem Monat gelöschten Datensätze und Ihr monatliches Kontingent.</li></ul> |

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
      "description": "The number of concurrently active dataset-expiration delete operations in all work order requests for the organization.",
      "consumed": 11,
      "quota": 75
    },
    {
      "name": "dailyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all work order requests for the organization for today.",
      "consumed": 314,
      "quota": 700000
    },
    {
      "name": "monthlyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all work order requests for the organization this month.",
      "consumed": 2764,
      "quota": 12000000
    }
  ]
}
```

| Eigenschaft | Beschreibung |
| -------- | ------- |
| `quotas` | Listet die Kontingentinformationen für jeden Datenlebenszyklus-Vorgangstyp auf. Jedes Kontingentobjekt enthält die folgenden Eigenschaften:<ul><li>`name`</li><li>`description`</li><li>`consumed`</li><li>`quota`</li></ul> |
| `name` | Die Kennung des Kontingenttyps. |
| `description` | Eine Beschreibung dessen, was dieses Kontingent begrenzt. |
| `consumed` | Die aktuell verbrauchte Kontingentmenge. Die verbrauchte Menge wird am 1. des Monats auf 00 % GMT :00 00 % GMT für :00 tägliche Kontingent zurückgesetzt. |
| `quota` | Die maximale Zuteilung dieses Kontingenttyps für Ihre Organisation. |
