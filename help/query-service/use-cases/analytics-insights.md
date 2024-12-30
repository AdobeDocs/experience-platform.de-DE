---
title: Analytics Insights für Web- und mobile Interaktionen
description: In diesem Dokument wird erläutert, wie Sie mit Query Service umsetzbare Einblicke aus aufgenommenen Adobe Analytics-Daten erstellen können.
exl-id: f64e61ef-0157-4f0a-88f8-bbe4f9aa83f0
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 1%

---

# Analytics Insights für Web- und mobile Interaktionen

Mit Adobe Experience Platform können Sie Daten aus Adobe Analytics Report Suites mithilfe von Experience-Datenmodell (XDM)-Feldern aufnehmen, um Datensätze auszufüllen. Diese Analytics-Daten werden entsprechend der [!DNL XDM ExperienceEvent] geändert. Query Service kann diese Daten dann verwenden, indem SQL-Abfragen ausgeführt werden, um wertvolle Einblicke aus dem Verhalten eines Benutzers über die digitalen Plattformen zu generieren.

Dieses Dokument enthält eine Vielzahl von SQL-Beispielabfragen, die gängige Anwendungsfälle beim Erstellen von Einblicken aus Web- und Mobile-Analytics-Daten zeigen.

Weitere Informationen [ Aufnehmen und Zuordnen von Analytics-Daten finden ](../../sources/connectors/adobe-applications/mapping/analytics.md) in der Dokumentation zu Analytics-Feldzuordnungen .

## Erste Schritte

Für jeden der folgenden Anwendungsfälle wird ein parametrisiertes SQL-Abfragebeispiel als Vorlage bereitgestellt, die Sie anpassen können. Geben Sie Parameter an, wo immer Sie `{ }` in den SQL-Beispielen für den Datensatz, die eVar, das Ereignis oder den Zeitrahmen sehen, den Sie auswerten möchten.

## Ziele

Die folgenden Beispiele zeigen SQL-Abfragen für gängige Anwendungsfälle zur Analyse Ihrer Adobe Analytics-Daten.

### Generieren der Besucheranzahl für jede Stunde an einem bestimmten Tag

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day,
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour,
       Count(DISTINCT enduserids._experience.aaid.id) AS Visitor_Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY Day, Hour
ORDER BY Hour;
```

### Ermitteln der 10 am häufigsten angezeigten Seiten an einem bestimmten Tag

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

### Die 10 beliebtesten Städte auf Basis der Benutzeraktivität identifizieren

```sql
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city,
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY state_city
ORDER BY Count DESC
LIMIT  10;
```

### 10 am häufigsten angesehene Produkte identifizieren

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

### Ermitteln Sie die 10 höchsten Umsätze.

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
