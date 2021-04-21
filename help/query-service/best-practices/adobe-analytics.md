---
keywords: Experience Platform;Startseite;beliebte Themen;Abfrage-Dienst;Abfrage-Dienst;Abfragen-Beispiel;Abfrage;Adobe-Analyse;
solution: Experience Platform
title: Beispieldaten für Abfragen für Adobe Analytics-Daten
topic-legacy: queries
description: Die Daten aus ausgewählten Adobe Analytics-Report Suites werden in XDM ExperienceEvents umgewandelt und für Sie als Datensätze in Adobe Experience Platform aufgenommen. In diesem Dokument wird eine Reihe von Anwendungsfällen beschrieben, in denen diese Daten von Query Service von Adobe Experience Platform verwendet werden. Die enthaltenen Beispielabfragen sollten mit Ihren Adobe Analytics-Datensätzen funktionieren.
exl-id: 96da3713-c7ab-41b3-9a9d-397756d9dd07
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1021'
ht-degree: 58%

---

# Beispielabfragen für Adobe Analytics-Daten

Daten aus ausgewählten Adobe Analytics Report Suites werden in Daten umgewandelt, die der [!DNL XDM ExperienceEvent]-Klasse entsprechen, und als Datensätze in Adobe Experience Platform aufgenommen.

In diesem Dokument werden eine Reihe von Anwendungsfällen erläutert, in denen Adobe Experience Platform [!DNL Query Service] diese Daten verwendet, einschließlich Beispieldaten, die mit Ihren Adobe Analytics-Datensätzen verwendet werden sollten. Weitere Informationen zur Zuordnung zu [!DNL Experience Events] finden Sie in der Dokumentation zu [Analytics-Feldzuordnung](../../sources/connectors/adobe-applications/mapping/analytics.md).

## Erste Schritte

Für die SQL-Beispiele in diesem Dokument müssen Sie SQL bearbeiten und die erwarteten Parameter für Ihre Abfragen entsprechend dem Datensatz, der eVar, dem Ereignis oder dem Zeitrahmen ausfüllen, den Sie bewerten möchten. Geben Sie Parameter an, wo immer Sie `{ }` in den folgenden SQL-Beispielen sehen.

## Häufig verwendete SQL-Beispiele

Die folgenden Beispiele zeigen häufig verwendete SQL-Abfragen zur Analyse Ihrer Adobe Analytics-Daten.

### Stündliche Besucherzahl für einen bestimmten Tag

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day,
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Count(DISTINCT enduserids._experience.aaid.id) AS Visitor_Count 
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY Day, Hour
ORDER BY Hour;
```

### Top 10 der angezeigten Seiten für einen bestimmten Tag

```sql
SELECT web.webpagedetails.name AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY web.webpagedetails.name 
ORDER BY page_views DESC 
LIMIT  10;
```

### Top 10 der aktivsten Benutzer

```sql
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY enduserids._experience.aaid.id
ORDER BY Count DESC
LIMIT  10;
```

### Top 10 der Städte nach Benutzeraktivität

```sql
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
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
       FROM   {TARGET_TABLE}
            WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
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
        FROM   {TARGET_TABLE} 
        WHERE  commerce.`order`.purchaseid IS NOT NULL 
                AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')

GROUP BY Purchase_ID 
ORDER BY total_order_revenue DESC 
LIMIT  10;
```

### Anzahl der Ereignisse nach Tag

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day, 
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Sum(_experience.analytics.event1to100.{TARGET_EVENT}.value) AS Event_Count
FROM   {TARGET_TABLE}
WHERE  _experience.analytics.event1to100.{TARGET_EVENT}.value IS NOT NULL 
        AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY Day, Hour
ORDER BY Hour;
```

## Merchandising-Variablen (Produktsyntax)


### Produktsyntax

In Adobe Analytics können benutzerspezifische Daten auf Produktebene über speziell konfigurierte Variablen, so genannte Merchandising-Variablen, erfasst werden. Diese basieren entweder auf einem eVar oder auf benutzerdefinierten Ereignissen. Der Unterschied zwischen diesen Variablen und ihrer Standardverwendung besteht darin, dass sie einen separaten Wert für jedes über den Treffer gefundene Produkt und nicht nur einen einzelnen Wert für den Treffer darstellen.

Diese Variablen werden als Produktsyntax-Merchandising-Variablen bezeichnet. Auf diese Weise können Informationen gesammelt werden, z. B. ein &quot;Rabatt&quot; pro Produkt oder Informationen über den &quot;Ort auf der Seite&quot; des Produkts in den Suchergebnissen des Kunden.

Weitere Informationen zur Verwendung der Produktsyntax finden Sie in der Adobe Analytics-Dokumentation zu [Implementierung von eVars mit der Produktsyntax](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-product-syntax).

Die folgenden Abschnitte beschreiben die XDM-Felder, die für den Zugriff auf die Merchandising-Variablen in Ihrem [!DNL Analytics]-Datensatz erforderlich sind:

#### eVars

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

- `#`: Der Index des Arrays, auf das Sie zugreifen.
- `evar#`: Die spezifische eVar, auf die Sie zugreifen.

#### Benutzerspezifische Ereignisse

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

- `#`: Der Index des Arrays, auf das Sie zugreifen.
- `event#`: Die spezifische Variable für benutzerspezifische Ereignis, auf die Sie zugreifen.

#### Beispielabfragen

Die Beispielabfrage hier gibt eine Merchandising-eVar und ein Ereignis für das erste Produkt zurück, das in `productListItems` gefunden wurde.

```sql
SELECT
  productListItems[0]._experience.analytics.customDimensions.evars.eVar1,
  productListItems[0]._experience.analytics.event1to100.event1.value
FROM adobe_analytics_midvalues
WHERE timestamp = to_timestamp('2019-07-23')
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
LIMIT 10
```

Diese nächste Abfrage explodiert das `productListItems`-Array und gibt jedes Merchandising-eVar und -Ereignis pro Produkt zurück. Das `_id`-Feld ist enthalten, um die Beziehung zum ursprünglichen Treffer anzuzeigen. Der Wert `_id` ist ein eindeutiger Primärschlüssel für den Datensatz.

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
  WHERE TIMESTAMP = to_timestamp('2019-07-23')
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
)
LIMIT 20
```

>[!NOTE]
>
> Wenn Sie versuchen, ein Feld abzurufen, das in Ihrem aktuellen Datensatz nicht vorhanden ist, tritt der Fehler &quot;Kein solches strukturiertes Feld&quot;auf. Bewerten Sie den in der Fehlermeldung zurückgegebenen Grund, um ein verfügbares Feld zu identifizieren, aktualisieren Sie dann Ihre Abfrage und führen Sie sie erneut aus.
>
>
```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### Konvertierungssyntax

Eine weitere Merchandising-Variable in Adobe Analytics ist die Konvertierungssyntax. Bei der Produktsyntax wird der Wert gleichzeitig mit dem Produkt erfasst, dies erfordert jedoch, dass die Daten auf derselben Seite vorhanden sind. Es gibt Szenarien, in denen die Daten auf einer Seite erscheinen, bevor es zu der/dem mit dem Produkt zusammenhängenden Konversion/Ereignis kommt. Betrachten Sie zum Beispiel den Verwendungsfall für die Produktsuchmethode.

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
| ------------------------------ | ------- | ------ | ------------- | ----- |
| Interne Suche:Sommerhemd | 19,99 | 1 | 1 | 1 |
| Interne Suche:Wintermütze | 12,99 | 3 | 1 | 1 |

Weitere Informationen zur Verwendung der Konversionssyntax finden Sie in der Adobe Analytics-Dokumentation zu [Implementieren von eVars mit Konvertierungssyntax](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-conversion-variable-syntax).

Im Folgenden finden Sie die XDM-Felder, um die Konvertierungssyntax in Ihrem [!DNL Analytics]-Datensatz zu erzeugen:

#### eVars

```console
_experience.analytics.customDimensions.evars.evar#
```

- `evar#`: Die spezifische eVar, auf die Sie zugreifen.

#### Produkt

```console
productListItems[#].sku
```

- `#`: Der Index des Arrays, auf das Sie zugreifen.

#### Beispielabfragen

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
