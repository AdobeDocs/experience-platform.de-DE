---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Abfragen
topic: queries
translation-type: tm+mt
source-git-commit: 45da024d45b5eebdfc393ee14890e24aed6021ce

---


# Beispieldaten für Abfragen für Adobe Analytics

Daten aus ausgewählten Adobe Analytics-Report Suites werden in XDM ExperienceEvents umgewandelt und als Datensätze in Adobe Experience Platform integriert. In diesem Dokument wird eine Reihe von Anwendungsfällen erläutert, in denen Adobe Experience Platform Abfrage Service diese Daten nutzt. Die darin enthaltenen Beispieldaten sollten mit Ihren Adobe Analytics-Datensätzen zusammenarbeiten. Weitere Informationen zur Zuordnung zu XDM ExperienceEvents finden Sie in der Dokumentation [zur Feldzuordnung für](../../source-connectors/ui/adobe-applications/analytics-mapping.md) Analytics.

## Erste Schritte

Die SQL-Beispiele in diesem Dokument erfordern, dass Sie SQL bearbeiten und die erwarteten Parameter für Ihre Abfragen entsprechend dem Datensatz, der eVar, dem Ereignis oder dem Zeitrahmen ausfüllen, den Sie bewerten möchten. Geben Sie Parameter an, wo immer Sie `{ }` in den folgenden SQL-Beispielen sehen.

## Häufig verwendete SQL-Beispiele

### Stündlicher Besucher für einen bestimmten Tag

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day,
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Count(DISTINCT enduserids._experience.aaid.id) AS Visitor_Count 
FROM   {target_table}
WHERE _acp_year = {target_year} 
      AND _acp_month = {target_month}  
      AND _acp_day = {target_day}
GROUP BY Day, Hour
ORDER BY Hour;
```

### Die 10 am häufigsten angezeigten Seiten für einen bestimmten Tag

```sql
SELECT web.webpagedetails.name AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP BY web.webpagedetails.name 
ORDER BY page_views DESC 
LIMIT  10;
```

### Die 10 aktivsten Benutzer

```sql
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp) AS Count
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP BY enduserids._experience.aaid.id
ORDER BY Count DESC
LIMIT  10;
```

### Die 10 beliebtesten Städte nach Aktivität

```sql
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp) AS Count
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP BY state_city
ORDER BY Count DESC
LIMIT  10;
```

### Die 10 am häufigsten angezeigten Produkte

```sql
SELECT Product_SKU,
       Sum(Product_Views) AS Total_Product_Views
FROM  (SELECT Explode(productlistitems.sku) AS Product_SKU, 
              commerce.productviews.value   AS Product_Views 
       FROM   {target_table}
       WHERE  _acp_year = {target_year}
              AND _acp_month = {target_month}
              AND _acp_day = {target_day}
              AND commerce.productviews.value IS NOT NULL) 
GROUP BY Product_SKU 
ORDER BY Total_Product_Views DESC
LIMIT  10;
```

### Wichtigster 10 Gesamtumsatz

```sql
SELECT Purchase_ID, 
       Round(Sum(Product_Items.priceTotal * Product_Items.quantity), 2) AS Total_Order_Revenue 
FROM   (SELECT commerce.`order`.purchaseid AS Purchase_ID, 
               Explode(productlistitems)   AS Product_Items 
        FROM   {target_table} 
        WHERE  commerce.`order`.purchaseid IS NOT NULL 
               AND _acp_year = {target_year} 
               AND _acp_month = {target_month}  
               AND _acp_day = {target_day}) 
GROUP BY Purchase_ID 
ORDER BY total_order_revenue DESC 
LIMIT  10;
```

### Ereignis nach Tag

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day, 
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Sum(_experience.analytics.event1to100.{target_event}.value) AS Event_Count
FROM   {target_table}
WHERE  _experience.analytics.event1to100.{target_event}.value IS NOT NULL 
        AND _acp_year = {target_year} 
        AND _acp_month = {target_month}  
        AND _acp_day = {target_day}
GROUP BY Day, Hour
ORDER BY Hour;
```

## Merchandising-Variablen (Produktsyntax)

In Adobe Analytics können benutzerspezifische Daten auf Produktebene über speziell konfigurierte Variablen namens &quot;Merchandising-Variablen&quot;erfasst werden. Diese basieren entweder auf einer eVar oder einem benutzerspezifischen Ereignis. Der Unterschied zwischen diesen Variablen und ihrer standardmäßigen Verwendung besteht darin, dass sie für jedes Produkt, das beim Treffer gefunden wird, einen separaten Wert darstellen und nicht nur einen einzelnen Wert für den Treffer. Diese Variablen werden als &quot;Produktsyntax-Merchandising-Variablen&quot;bezeichnet. Dies ermöglicht die Erfassung von Informationen, wie z.B. einen &quot;Rabatt Betrag&quot; pro Produkt oder Informationen über die &quot;Position auf der Seite&quot; des Produkts in den Suchergebnissen des Kunden.

Im Folgenden finden Sie die XDM-Felder, um auf die Merchandising-Variablen in Ihrem Analytics-Datensatz zuzugreifen:

### eVars

```
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

Dabei `[#]` ist ein Array-Index und `evar#` die spezifische eVar-Variable.

### Benutzerspezifische Ereignisse

```
productListItems[#]._experience.analytics.event1to100.event#.value
```

Hierbei `[#]` handelt es sich um einen Array-Index und `event#` die spezifische Variable für benutzerspezifische Ereignis.

### Abfragen

Im Folgenden finden Sie eine Abfrage, die eine Merchandising-eVar und ein Ereignis für das erste in der `productListItems`.

```sql
SELECT
  productListItems[0]._experience.analytics.customDimensions.evars.eVar1,
  productListItems[0]._experience.analytics.event1to100.event1.value
FROM adobe_analytics_midvalues
WHERE _ACP_YEAR=2019 AND _ACP_MONTH=7 AND _ACP_DAY=23
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
LIMIT 10
```

Diese nächste Abfrage &#39;explodiert&#39; die `productListItems` und gibt jede Merchandising eVar und jedes Ereignis pro Produkt zurück. Das `_id` Feld wird einbezogen, um die Beziehung zum ursprünglichen Treffer anzuzeigen. Der `_id` Wert ist ein eindeutiger Primärschlüssel im ExperienceEvent-Datensatz.

```sql
SELECT
  _id,
  productItem._experience.analytics.customDimensions.evars.eVar1,
  productItem._experience.analytics.event1to100.event1.value
FROM (
  SELECT
    _id,
    explode(productListItems) as productItem
  FROM adobe_analytics_midvalues
  WHERE _ACP_YEAR=2019 AND _ACP_MONTH=7 AND _ACP_DAY=23
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
)
LIMIT 20
```

### Allgemeiner Fehler bei der Implementierung der Beispiel-Abfragen

Der Fehler &quot;Kein solches strukturiertes Feld&quot;wird angezeigt, wenn Sie versuchen, ein Feld abzurufen, das in Ihrem aktuellen Datensatz nicht vorhanden ist. Bewerten Sie den in der Fehlermeldung zurückgegebenen Grund, um ein verfügbares Feld zu identifizieren und aktualisieren Sie dann Ihre Abfrage und führen Sie sie erneut aus.

```
ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
```

## Merchandising-Variablen (Konvertierungssyntax)

Ein anderer Typ einer Merchandising-Variablen in Adobe Analytics ist die Konvertierungssyntax. Mit der Produktsyntax wird der Wert gleichzeitig mit dem Produkt erfasst, dies erfordert jedoch, dass die Daten auf derselben Seite vorhanden sind. Es gibt Szenarien, in denen die Daten auf einer Seite vor der Konvertierung oder dem Ereignis von Interesse für das Produkt auftauchen. Betrachten Sie z. B. den Anwendungsfall des Berichte &quot;Produktsuchmethode&quot;.

1. Ein Benutzer führt eine interne Suche nach &quot;Winterhut&quot;durch, wodurch die für die Konversionssyntax aktivierte Merchandising eVar6 auf &quot;Interne Suche:Winterhut&quot;gesetzt wird
2. Der Benutzer klickt auf &quot;Waffelmütze&quot; und landet auf der Produktdetailseite.\
   a. Die Landung hier löst ein `Product View` Ereignis für die &quot;Waffelmütze&quot; für $12.99 aus.\
   b. Da `Product View` das Produkt &quot;Waffelmütze&quot; als Binding-Ereignis konfiguriert ist, ist es nun an den eVar6-Wert von &quot;internal search:winter hat&quot; gebunden. Jedes Mal, wenn das Produkt &quot;Waffelmütze&quot;gesammelt wird, wird es mit &quot;Interne Suche:Winterhut&quot;verknüpft, bis entweder (1) die Ablaufeinstellung erreicht ist oder (2) ein neuer eVar6-Wert festgelegt wird und das Binding-Ereignis mit diesem Produkt erneut auftritt.
3. Der Benutzer fügt das Produkt zum Warenkorb hinzu und löst das `Cart Add` Ereignis aus.
4. Der Benutzer führt eine weitere interne Suche nach &quot;Summer Shirt&quot;durch, wodurch die Konversionssyntax für Merchandising eVar6 auf &quot;internal search:Summer shirt&quot;gesetzt wird.
5. Der Benutzer klickt auf &quot;sporty t-shirt&quot; und landet auf der Produktdetailseite.\
   a. Die Landung hier feuert ein `Product View` Ereignis für &quot;sportliches T-Shirt für $19.99.\
   b. Das `Product View` Ereignis ist immer noch unser Binding-Ereignis. Das Produkt &quot;sporty t-t-shirt&quot; ist nun an den eVar6-Wert von &quot;internal search:Summer shirt&quot; gebunden und das frühere Produkt &quot;Waffle Bean&quot; ist immer noch an den eVar6-Wert von &quot;internal search:Waffle Bee&quot; gebunden.
6. Der Benutzer fügt das Produkt zum Warenkorb hinzu und löst das `Cart Add` Ereignis aus.
7. Der Benutzer checkt mit beiden Produkten aus.

In Berichte werden die Bestellungen, der Umsatz, die Ansichten des Produkts und die Hinzufügungen zum Einkaufswagen mit eVar6 gemeldet und an die Aktivität des gebundenen Produkts angepasst.

| eVar6 (Produktsuchmethode) | Umsatz | Aufträge | Ansichten | Hinzufügen zum Warenkorb |
|---|---|---|---|---|
| Interne Suche: Sommershirt | 19.99 | 1 | 1 | 1 |
| Interne Suche: Winterhut | 12.99 | 1 | 1 | 1 |

Im Folgenden finden Sie die XDM-Felder, um die Konvertierungssyntax in Ihrem Analytics-Datensatz zu erstellen:

### eVars

```
_experience.analytics.customDimensions.evars.evar#
```

Hierbei `evar#` handelt es sich um die spezifische eVar-Variable.

### Produkt

```
productListItems[#].sku
```

Hierbei `[#]` handelt es sich um einen Array-Index.

### Abfragen

Im Folgenden finden Sie eine Abfrage, die den Wert an das jeweilige Produkt- und Ereignis-Paar bindet, in diesem Fall an das Ereignis zur Ansicht des Produkts.

```sql
SELECT
  endUserIds._experience.aaid.id AS AAID,
  timestamp,
  CASE WHEN commerce.productViews.value = 1 THEN ATTRIBUTION_LAST_TOUCH(timestamp, 'bindConversionSyntaxMerchVariable_eVar1', _experience.analytics.customDimensions.eVars.eVar1)
  OVER(PARTITION BY endUserIds._experience.aaid.id
       ORDER BY timestamp
       ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
  END AS eVar1Bind,
  EXPLODE(productListItems) AS Product_List,
  commerce.productViews.value AS prodView,
  commerce.purchases.value AS purchase
FROM adobe_analytics_midvalues
WHERE commerce.productViews.value = 1 OR commerce.purchases.value = 1 OR _experience.analytics.customDimensions.eVars.eVar1 IS NOT NULL
LIMIT 100
```

Im Folgenden finden Sie eine Beispiel-Abfrage, die den gebundenen Wert an nachfolgende Vorkommen des jeweiligen Produkts beibehält. Die niedrigste Untergrenze der Abfrage bestimmt die Wertbeziehung zum Produkt auf dem deklarierten Binding-Ereignis. Die nächste Subversion-Abfrage führt die Zuordnung dieses gebundenen Werts für nachfolgende Interaktionen mit dem jeweiligen Produkt aus. Und auf der obersten Ebene wählen Sie die Aggregat die Ergebnisse, um den Berichte zu erzeugen.

```sql
SELECT
  Product_List.SKU,
  eVar1101ConversionSyntax,
  SUM(prodView) AS Product_Views,
  SUM(purchase) AS Purchases
FROM
(
  SELECT
    Product_List,
    ATTRIBUTION_LAST_TOUCH(timestamp, 'ConversionSyntax_eVar1', eVar1Bind)
      OVER(PARTITION BY AAID, Product_List.SKU
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
    AS eVar1ConversionSyntax,
    prodView,
    purchase
  FROM
  (
    SELECT
      endUserIds._experience.aaid.id AS AAID,
      timestamp,
      CASE WHEN commerce.productViews.value = 1 THEN ATTRIBUTION_LAST_TOUCH(timestamp, 'bindConversionSyntaxMerchVariable_eVar1', _experience.analytics.customDimensions.eVars.eVar1)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
      END AS eVar1Bind,
      EXPLODE(productListItems) AS Product_List,
      commerce.productViews.value AS prodView,
      commerce.purchases.value AS purchase
    FROM adobe_analytics_midvalues
    WHERE commerce.productViews.value = 1 OR commerce.purchases.value = 1 OR _experience.analytics.customDimensions.eVars.eVar1 IS NOT NULL
  )
)
WHERE eVar1ConversionSyntax IS NOT NULL
GROUP BY 1, 2
ORDER BY 3 DESC
LIMIT 100
```
