---
keywords: Experience Platform; Startseite; beliebte Themen; Query Service; Query Service; Beispielabfragen; Beispielabfrage; Adobe Analytics
solution: Experience Platform
title: Beispielabfragen für Adobe Analytics-Daten
description: Daten aus ausgewählten Adobe Analytics Report Suites werden in XDM ExperienceEvents umgewandelt und als Datensätze in Adobe Experience Platform aufgenommen. In diesem Dokument wird eine Reihe von Anwendungsfällen beschrieben, in denen Query Service diese Daten nutzt, sowie Beispielabfragen, die für die Verwendung mit Ihren Adobe Analytics-Datensätzen entwickelt wurden.
exl-id: 96da3713-c7ab-41b3-9a9d-397756d9dd07
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 41%

---

# Beispielabfragen für Adobe Analytics-Daten

Daten aus ausgewählten Adobe Analytics Report Suites werden in Daten umgewandelt, die dem [!DNL XDM ExperienceEvent] -Klasse und in Adobe Experience Platform als Datensätze erfasst.

In diesem Dokument wird eine Reihe von Anwendungsfällen beschrieben, in denen Adobe Experience Platform [!DNL Query Service] verwendet diese Daten. Weitere Informationen finden Sie in der Dokumentation unter [Analytics-Feldzuordnung](../../sources/connectors/adobe-applications/mapping/analytics.md) Weitere Informationen zur Zuordnung zu [!DNL Experience Events].

Siehe [Anwendungsfalldokumentation für Analytics](../use-cases/analytics-insights.md) , um zu erfahren, wie Sie mit Query Service praktische Einblicke aus erfassten Adobe Analytics-Daten erstellen können.

## Deduplizierung

[!DNL Query Service] unterstützt die Datendeduplizierung. Siehe [Datendeduplizierung in [!DNL Query Service] Dokumentation](../best-practices/deduplication.md) für Informationen zum Generieren neuer Werte zum Zeitpunkt der Abfrage [!DNL Experience Event] Datensätze.

## Merchandising-Variablen (Produktsyntax)

Die folgenden Abschnitte enthalten XDM-Felder und Beispielabfragen, mit denen Sie auf die Merchandising-Variablen in Ihren [!DNL Analytics] Datensatz.

### Produktsyntax

In Adobe Analytics können benutzerdefinierte Daten auf Produktebene über speziell konfigurierte Variablen, so genannte Merchandising-Variablen, erfasst werden. Diese basieren entweder auf einem eVar oder auf benutzerdefinierten Ereignissen. Der Unterschied zwischen diesen Variablen und ihrer typischen Verwendung besteht darin, dass sie für jedes beim Treffer gefundene Produkt einen separaten Wert darstellen und nicht nur einen einzelnen Wert für den Treffer.

Diese Variablen werden als Merchandising-Variablen mit Produktsyntax bezeichnet. Dies ermöglicht die Erfassung von Informationen, z. B. einen &quot;Rabattbetrag&quot;pro Produkt oder Informationen über die &quot;Position auf der Seite&quot;des Produkts in den Suchergebnissen des Kunden.

Weitere Informationen zur Verwendung der Produktsyntax finden Sie in der Adobe Analytics-Dokumentation unter [Implementierung von eVars mit Produktsyntax](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-product-syntax).

In den folgenden Abschnitten werden die XDM-Felder beschrieben, die für den Zugriff auf die Merchandising-Variablen in Ihren [!DNL Analytics] Datensatz:

#### eVars

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

- `#`: Der Index des Arrays, auf das Sie zugreifen.
- `evar#`: Die spezifische eVar-Variable, auf die Sie zugreifen.

#### Benutzerspezifische Ereignisse

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

- `#`: Der Index des Arrays, auf das Sie zugreifen.
- `event#`: Die spezifische benutzerspezifische Ereignisvariable, auf die Sie zugreifen.

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

Diese nächste Abfrage explodiert die `productListItems` und gibt jedes Merchandising-eVar und -Ereignis pro Produkt zurück. Das `_id`-Feld ist enthalten, um die Beziehung zum ursprünglichen Treffer anzuzeigen. Die `_id` -Wert ist ein eindeutiger Primärschlüssel für den Datensatz.

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
> Wenn Sie versuchen, ein Feld abzurufen, das in Ihrem aktuellen Datensatz nicht vorhanden ist, tritt der Fehler &quot;No such struct field&quot;auf. Werten Sie den in der Fehlermeldung zurückgegebenen Grund aus, um ein verfügbares Feld zu identifizieren, aktualisieren Sie dann Ihre Abfrage und führen Sie sie erneut aus.
>
>
```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### Konversionssyntax

Ein weiterer in Adobe Analytics zu findender Merchandising-Variablentyp ist die Konversionssyntax. Mit der Produktsyntax wird der Wert gleichzeitig mit dem Produkt erfasst. Dazu müssen die Daten jedoch auf derselben Seite vorhanden sein. Es gibt Szenarien, in denen die Daten auf einer Seite erscheinen, bevor es zu der/dem mit dem Produkt zusammenhängenden Konversion/Ereignis kommt. Betrachten Sie beispielsweise den Anwendungsfall für die Produktsuchmethode.

1. Ein Benutzer führt eine interne Suche nach „Wintermütze“ durch, wodurch die für die Konversionssyntax aktivierte Merchandising-eVar6 auf „Interne Suche:Wintermütze“ gesetzt wird.
2. Der Benutzer klickt auf „Waffelmütze“ und wird zur Produktdetailseite weitergeleitet.\
   a. Mit dem Öffnen der Seite wird ein `Product View`-Ereignis für die „Waffelmütze“ für $12,99 ausgelöst.\
   b. Seit `Product View` als Binding-Ereignis konfiguriert ist, ist das Produkt &quot;Waffelmütze&quot;jetzt an den eVar6-Wert von &quot;Interne Suche:Wintermütze&quot;gebunden. Jedes Mal, wenn das Produkt „Waffelmütze“ gesammelt wird, wird es mit „Interne Suche:Wintermütze“ verknüpft, bis entweder (1) die Ablaufeinstellung erreicht ist oder (2) ein neuer eVar6-Wert festgelegt wird und das Binding-Ereignis mit diesem Produkt erneut auftritt.
3. Der Benutzer fügt das Produkt zum Warenkorb hinzu und löst das `Cart Add`-Ereignis aus.
4. Der Benutzer führt eine weitere interne Suche nach „Sommerhemd“ durch, wodurch die Konversionssyntax für Merchandising-eVar6 auf „Interne Suche:Sommerhemd“ gesetzt wird.
5. Der Benutzer klickt auf „Sportliches T-Shirt“ und wird zur Produktdetailseite weitergeleitet.\
   a. Mit dem Öffnen der Seite wird ein `Product View`-Ereignis für das „Sportliche T-Shirt“ für $19,99 ausgelöst.\
   b. Das `Product View`-Ereignis ist immer noch unser Binding-Ereignis. Das Produkt „Sportliches T-Short“ ist nun an den eVar6-Wert von „Interne Suche:Sommerhemd“ gebunden und das frühere Produkt „Waffelmütze“ ist immer noch an den eVar6-Wert von „Interne Suche:Wintermütze“ gebunden.
6. Der Benutzer fügt das Produkt zum Warenkorb hinzu und löst das `Cart Add`-Ereignis aus.
7. Der Benutzer checkt mit beiden Produkten aus.

Beim Reporting werden Bestellungen, Umsatz, Produktansichten und Hinzufügen zum Warenkorb entsprechend der eVar6 gemeldet und sind an der Aktivität des gebundenen Produkts ausgerichtet.

| eVar6 (Methode zur Produktsuche) | Umsatz | Bestellungen | Produktansichten | Hinzufügen zum Warenkorb |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| Interne Suche:Sommerhemd | 19,99 | 1 | 1 | 1 |
| Interne Suche:Wintermütze | 12,99 | 1 | 1 | 1 |

Weitere Informationen zur Verwendung der Konversionssyntax finden Sie in der Adobe Analytics-Dokumentation unter [Implementieren von eVars mit Konversionssyntax](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-conversion-variable-syntax).

Hier finden Sie die XDM-Felder, um die Konversionssyntax in Ihrer [!DNL Analytics] Datensatz:

#### eVars

```console
_experience.analytics.customDimensions.evars.evar#
```

- `evar#`: Die spezifische eVar-Variable, auf die Sie zugreifen.

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
