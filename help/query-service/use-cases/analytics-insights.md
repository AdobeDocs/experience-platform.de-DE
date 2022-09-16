---
title: Analytics Insights für Web- und Mobile-Interaktionen
description: In diesem Dokument wird erläutert, wie Sie mithilfe von Query Service praktische Einblicke aus erfassten Adobe Analytics-Daten erstellen können.
exl-id: f64e61ef-0157-4f0a-88f8-bbe4f9aa83f0
source-git-commit: d573c01a0aa9989f581796a0be4aec6904ffc569
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 1%

---

# Analytics-Einblicke für Web- und mobile Interaktionen

Mit Adobe Experience Platform können Sie Daten aus Adobe Analytics Report Suites mithilfe von XDM-Feldern (Experience-Datenmodell) erfassen, um Datensätze zu füllen. Query Service kann diese Analysedaten dann nutzen, indem Sie SQL-Abfragen ausführen, um wertvolle Einblicke aus dem Benutzerverhalten über die digitalen Plattformen zu generieren.

Dieses Dokument bietet eine Vielzahl von SQL-Beispielabfragen, die gängige Anwendungsfälle beim Erstellen von Einblicken aus Web- und mobilen Analytics-Daten veranschaulichen.

Siehe [Dokumentation zu Analytics-Feldzuordnungen](../../sources/connectors/adobe-applications/mapping/analytics.md) für weitere Informationen zur Erfassung und Zuordnung von Analysedaten.

## Erste Schritte

Für jeden der folgenden Anwendungsfälle wird ein parametrisiertes SQL-Abfragebeispiel als Vorlage bereitgestellt, die Sie anpassen können. Stellen Sie Parameter überall dort bereit, wo Sie sie sehen `{ }` in den SQL-Beispielen für den Datensatz, die eVar, das Ereignis oder den Zeitrahmen, den Sie bewerten möchten.

## Ziele

Die folgenden Beispiele zeigen SQL-Abfragen für gängige Anwendungsfälle zur Analyse Ihrer Adobe Analytics-Daten.

### Generieren der Besucherzahl für jede Stunde an einem bestimmten Tag

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day,
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour,
       Count(DISTINCT enduserids._experience.aaid.id) AS Visitor_Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY Day, Hour
ORDER BY Hour;
```

### Identifizieren der 10 am häufigsten angezeigten Seiten an einem bestimmten Tag

```SQL
SELECT web.webpagedetails.name AS Page_Name,
       Sum(web.webpagedetails.pageviews.value) AS Page_Views
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY web.webpagedetails.name
ORDER BY page_views DESC
LIMIT  10;
```

### Die 10 aktivsten Benutzer identifizieren

```sql
SELECT enduserids._experience.aaid.id AS aaid,
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY enduserids._experience.aaid.id
ORDER BY Count DESC
LIMIT  10;
```

### Die 10 am meisten gewünschten Städte basierend auf der Benutzeraktivität identifizieren

```sql
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city,
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY state_city
ORDER BY Count DESC
LIMIT  10;
```

### Die 10 am häufigsten angezeigten Produkte identifizieren

```sql
SELECT Product_SKU,
       Sum(Product_Views) AS Total_Product_Views
FROM  (SELECT Explode(productlistitems.sku) AS Product_SKU,
              commerce.productviews.value   AS Product_Views
       FROM   {TARGET_TABLE}
            WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
              AND commerce.productviews.value IS NOT NULL)
GROUP BY Product_SKU
ORDER BY Total_Product_Views DESC
LIMIT  10;
```

### Ermitteln Sie die 10 höchsten Bestelleinnahmen.

```sql
SELECT Purchase_ID,
       Round(Sum(Product_Items.priceTotal * Product_Items.quantity), 2) AS Total_Order_Revenue
FROM   (SELECT commerce.`order`.purchaseid AS Purchase_ID,
               Explode(productlistitems)   AS Product_Items
        FROM   {TARGET_TABLE}
        WHERE  commerce.`order`.purchaseid IS NOT NULL
                AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')

GROUP BY Purchase_ID
ORDER BY total_order_revenue DESC
LIMIT  10;
```
