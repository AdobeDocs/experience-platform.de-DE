---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Beispielabfragen
topic: queries
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 88%

---


# Beispielabfragen für Adobe Analytics-Daten

Data from selected Adobe Analytics report suites is transformed into XDM [!DNL ExperienceEvents] and ingested into Adobe Experience Platform as datasets for you. This document outlines a number of use cases where Adobe Experience Platform [!DNL Query Service] makes use of this data, and the included sample queries should work with your Adobe Analytics datasets. See the [Analytics field mapping documentation](../../sources/connectors/adobe-applications/mapping/analytics.md) for more information on mapping to XDM [!DNL ExperienceEvents].

## Erste Schritte

Für die SQL-Beispiele in diesem Dokument müssen Sie SQL bearbeiten und die erwarteten Parameter für Ihre Abfragen entsprechend dem Datensatz, der eVar, dem Ereignis oder dem Zeitrahmen ausfüllen, den Sie bewerten möchten. Geben Sie Parameter an, wo immer Sie `{ }` in den folgenden SQL-Beispielen sehen.

## Häufig verwendete SQL-Beispiele

### Stündliche Besucherzahl für einen bestimmten Tag

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

### Top 10 der angezeigten Seiten für einen bestimmten Tag

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

### Top 10 der aktivsten Benutzer

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

### Top 10 der Städte nach Benutzeraktivität

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

### Top 10 der angezeigten Produkte

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

### Top 10 des Gesamtbestellumsatzes

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

### Anzahl der Ereignisse nach Tag

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

In Adobe Analytics können benutzerdefinierte Daten auf Produktebene über speziell konfigurierte Variablen namens „Merchandising-Variablen“ erfasst werden. Diese basieren entweder auf einer eVar oder einem benutzerspezifischen Ereignis. Der Unterschied zwischen diesen Variablen und ihrer Standardverwendung besteht darin, dass sie einen separaten Wert für jedes über den Treffer gefundene Produkt und nicht nur einen einzelnen Wert für den Treffer darstellen. Diese Variablen werden als Produktsyntax-Merchandising-Variablen bezeichnet. Dies ermöglicht die Erfassung von Informationen, wie z. B. einen „Rabattbetrag“ pro Produkt oder Informationen über die „Position auf der Seite“ des Produkts, in den Suchergebnissen des Kunden.

Here are the XDM fields to access the merchandising variables in your [!DNL Analytics] dataset:

### eVars

```
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

Dabei ist `[#]` ein Array-Index und `evar#` die spezifische eVar-Variable.

### Benutzerspezifische Ereignisse

```
productListItems[#]._experience.analytics.event1to100.event#.value
```

Dabei ist `[#]` ein Array-Index und `event#` die spezifische Variable für das benutzerspezifische Ereignis.

### Beispielabfragen

Die Beispielabfrage hier gibt eine Merchandising-eVar und ein Ereignis für das erste Produkt zurück, das in `productListItems` gefunden wurde.

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

Diese nächste Abfrage schlüsselt die `productListItems` auf und gibt eine Merchandising-eVar und ein Ereignis pro Produkt zurück. Das `_id`-Feld ist enthalten, um die Beziehung zum ursprünglichen Treffer anzuzeigen. The `_id` value is a unique primary key in the [!DNL ExperienceEvent] dataset.

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

### Häufige Fehler bei der Implementierung der Beispielabfragen

Der Fehler „No such struct field“ (Kein solches Strukturfeld) tritt auf, wenn Sie versuchen, ein Feld abzurufen, das in Ihrem aktuellen Datensatz nicht vorhanden ist. Werten Sie den in der Fehlermeldung zurückgegebenen Grund aus, um ein verfügbares Feld zu identifizieren. Aktualisieren Sie dann Ihre Abfrage und führen Sie sie erneut aus.

```
ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
```

## Merchandising-Variablen (Konversionssyntax)

Ein anderer Typ einer Merchandising-Variablen in Adobe Analytics ist die Konversionssyntax. Bei der Produktsyntax wird der Wert gleichzeitig mit dem Produkt erfasst. Dazu müssen die Daten jedoch auf derselben Seite vorhanden sein. Es gibt Szenarien, in denen die Daten auf einer Seite erscheinen, bevor es zu der/dem mit dem Produkt zusammenhängenden Konversion/Ereignis kommt. Betrachten Sie beispielsweise den Anwendungsfall für die Berichte zur Produktsuchmethode.

1. Ein Benutzer führt eine interne Suche nach „Wintermütze“ durch, wodurch die für die Konversionssyntax aktivierte Merchandising-eVar6 auf „Interne Suche:Wintermütze“ gesetzt wird.
2. Der Benutzer klickt auf „Waffelmütze“ und wird zur Produktdetailseite weitergeleitet.\
   a. Mit dem Öffnen der Seite wird ein `Product View`-Ereignis für die „Waffelmütze“ für $12,99 ausgelöst.\
   b. Da `Product View` als bindendes Ereignis konfiguriert ist, ist das Produkt „Waffelmütze“ jetzt an den eVar6-Wert von „Interne Suche:Wintermütze“ gebunden. Jedes Mal, wenn das Produkt „Waffelmütze“ gesammelt wird, wird es mit „Interne Suche:Wintermütze“ verknüpft, bis entweder (1) die Ablaufeinstellung erreicht ist oder (2) ein neuer eVar6-Wert festgelegt wird und das Binding-Ereignis mit diesem Produkt erneut auftritt.
3. Der Benutzer fügt das Produkt zum Warenkorb hinzu und löst das `Cart Add`-Ereignis aus.
4. Der Benutzer führt eine weitere interne Suche nach „Sommerhemd“ durch, wodurch die Konversionssyntax für Merchandising-eVar6 auf „Interne Suche:Sommerhemd“ gesetzt wird.
5. Der Benutzer klickt auf „Sportliches T-Shirt“ und wird zur Produktdetailseite weitergeleitet.\
   a. Mit dem Öffnen der Seite wird ein `Product View`-Ereignis für das „Sportliche T-Shirt“ für $19,99 ausgelöst.\
   b. Das `Product View`-Ereignis ist immer noch unser Binding-Ereignis. Das Produkt „Sportliches T-Short“ ist nun an den eVar6-Wert von „Interne Suche:Sommerhemd“ gebunden und das frühere Produkt „Waffelmütze“ ist immer noch an den eVar6-Wert von „Interne Suche:Wintermütze“ gebunden.
6. Der Benutzer fügt das Produkt zum Warenkorb hinzu und löst das `Cart Add`-Ereignis aus.
7. Der Benutzer checkt mit beiden Produkten aus.

Beim Reporting werden Bestellungen, Umsatz, Produktansichten und Hinzufügen zum Warenkorb entsprechend der eVar6 gemeldet und sind an der Aktivität des gebundenen Produkts ausgerichtet.

| eVar6 (Produktsuchmethode) | Umsatz | Bestellungen | Produktansichten | Hinzufügen zum Warenkorb |
|---|---|---|---|---|
| Interne Suche:Sommerhemd | 19,99 | 1 | 1 | 1 |
| Interne Suche:Wintermütze | 12,99 | 1 | 1 | 1 |

Here are the XDM fields to produce the Conversion Syntax in your [!DNL Analytics] dataset:

### eVars

```
_experience.analytics.customDimensions.evars.evar#
```

Wobei `evar#` die spezifische eVar-Variable ist.

### Produkt

```
productListItems[#].sku
```

Wobei `[#]` ein Array-Index ist.

### Beispielabfragen

Im Folgenden finden Sie eine Beispielabfrage, die den Wert an das jeweilige Produkt- und Ereignispaar bindet, in diesem Fall an das Produktansichtsereignis.

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

Im Folgenden finden Sie eine Beispielabfrage, die den gebundenen Wert für nachfolgende Vorkommen des jeweiligen Produkts beibehält. Die niedrigste Unterabfrage stellt die Wertebeziehung zum Produkt für das deklarierte Binding-Ereignis her. Die nächste Unterabfrage führt die Attribution dieses gebundenen Werts über nachfolgende Interaktionen mit dem jeweiligen Produkt durch. Die Auswahl der obersten Ebene aggregiert die Ergebnisse, um die Berichte zu erstellen.

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
