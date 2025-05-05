---
title: Zurückgeben und Verwenden von Merchandising-Variablen aus Analysedaten
description: Erfahren Sie, wie Sie XDM-Felder und Beispielabfragen bereitstellen, um auf die Merchandising-Variablen in Ihren Analytics-Datensätzen zuzugreifen.
exl-id: 1e2ae095-4152-446f-8b66-dae5512d690e
source-git-commit: 7cde32f841497edca7de0c995cc4c14501206b1a
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 12%

---

# Zurückgeben und Verwenden von Merchandising-Variablen aus Analysedaten 

Verwenden Sie den Abfrage-Service, um die Daten zu verwalten, die von Adobe Analytics als Datensätze in Adobe Experience Platform aufgenommen werden. Die folgenden Abschnitte enthalten Beispielabfragen, mit denen Sie auf die Merchandising-Variablen in Ihren Analytics-Datensätzen zugreifen können. Weitere Informationen finden Sie in der Dokumentation [ Aufnehmen und Zuordnen von Adobe Analytics-Daten ](../../sources/connectors/adobe-applications/mapping/analytics.md) der Analytics-Quelle

## Merchandising-Variablen {#merchandising-variables}

Merchandising-Variablen können einer von zwei Syntaxen folgen:

* **Produktsyntax**: Hiermit wird einem Produkt der Wert &quot;eVar&quot; zugewiesen. 
* **Konversionsvariablensyntax**: Hierbei wird einem Produkt nur dann die eVar zugewiesen, wenn ein Binding-Ereignis auftritt. Sie können die Ereignisse auswählen, die als Binding-Ereignisse fungieren.

## Produktsyntax {#product-syntax}

In Adobe Analytics können benutzerdefinierte Daten auf Produktebene über speziell konfigurierte Variablen erfasst werden, die als Merchandising-Variablen bezeichnet werden. Diese basieren entweder auf einer eVar oder auf benutzerspezifischen Ereignissen. Der Unterschied zwischen diesen Variablen und ihrer typischen Verwendung besteht darin, dass sie für jedes Produkt, das im Treffer gefunden wird, einen separaten Wert darstellen, anstatt nur einen einzelnen Wert für den Treffer.

Diese Variablen werden als Merchandising-Variablen mit Produktsyntax bezeichnet. Auf diese Weise können Informationen gesammelt werden, z. B. ein pro Produkt berechneter „Rabattbetrag“ oder Informationen über den „Standort auf der Seite“ des Produkts in den Suchergebnissen des Kunden.

Weitere Informationen zur Verwendung der Produktsyntax finden Sie in der Adobe Analytics-Dokumentation unter [Implementieren von eVars mithilfe der Produktsyntax](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=de#implement-using-product-syntax).

In den folgenden Abschnitten werden die XDM-Felder beschrieben, die für den Zugriff auf die Merchandising-Variablen in Ihrem [!DNL Analytics]-Datensatz erforderlich sind:

### eVars

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

* `#`: Der Index des Arrays, auf das Sie zugreifen.
* `evar#`: Die spezifische eVar-Variable, auf die Sie zugreifen.

### Benutzerspezifische Ereignisse

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

* `#`: Der Index des Arrays, auf das Sie zugreifen.
* `event#`: Die spezifische Variable für benutzerspezifische Ereignisse, auf die Sie zugreifen.

## Anwendungsfälle für die Produktsyntax {#product-use-cases}

Die folgenden Anwendungsfälle konzentrieren sich darauf, eine Merchandising-eVar mithilfe von SQL aus dem `productListItems`-Array zurückzugeben.

### Merchandising-eVar und -Ereignis zurückgeben

Die nachstehende Abfrage gibt eine Merchandising-eVar und ein -Ereignis für das erste Produkt zurück, das im `productListItems`-Array gefunden wurde.

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

### Auflösen des productListItems-Arrays und Zurückgeben der Merchandising-eVar und des -Ereignisses für jedes Produkt.

Diese nächste Abfrage löst das `productListItems`-Array auf und gibt jede Merchandising-eVar und jedes Merchandising-Ereignis pro Produkt zurück. Das `_id`-Feld ist enthalten, um die Beziehung zum ursprünglichen Treffer anzuzeigen. Der `_id` ist ein eindeutiger Primärschlüssel für den Datensatz.

>[!NOTE]
>
>Die Auflösefunktion trennt die Elemente eines Arrays in mehrere Zeilen. Null-Werte werden ausgeschlossen.

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
> Wenn Sie versuchen, ein Feld abzurufen, das nicht in Ihrem aktuellen Datensatz vorhanden ist, tritt der Fehler „Kein solches Strukturfeld“ auf. Prüfen Sie den in der Fehlermeldung zurückgegebenen Grund, um ein verfügbares Feld zu identifizieren, aktualisieren Sie dann Ihre Abfrage und führen Sie sie erneut aus.
>
>```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### Syntax der Konversionsvariablen {#conversion-variable-syntax}

Ein weiterer Typ von Merchandising-Variablen, der in Adobe Analytics zu finden ist, ist die Konversionsvariablensyntax. Die Konversionsvariablensyntax wird verwendet, wenn der eVar-Wert nicht verfügbar ist, um in der Variablen „products“ festgelegt werden zu können. Dieses Szenario bedeutet in der Regel, dass Ihre Seite keinen Kontext des Merchandising-Kanals oder der Suchmethode hat. In diesen Fällen sollten Sie die Merchandising-Variable festlegen, bevor die Benutzerin oder der Benutzer zur Produktseite gelangt, und der Wert bleibt erhalten, bis das Binding-Ereignis eintritt.

Das folgende Szenario zur Produktsuche zeigt beispielsweise, wie die erforderlichen Daten auf einer Seite vorhanden sein können, bevor die Konversion oder das mit dem Produkt verbundene Ereignis eintritt.

1. Ein Benutzer führt eine interne Suche nach „Winterhut“ durch, wobei die Konversionssyntax für Merchandising eVar6 auf „Interne Suche:Winterhut“ festgelegt wird.
2. Der Benutzer klickt auf „Waffelmütze“ und wird zur Produktdetailseite weitergeleitet.\
   a. Mit dem Öffnen der Seite wird ein `Product View`-Ereignis für die „Waffelmütze“ für $12,99 ausgelöst.\
   b. Da `Product View` als Binding-Ereignis konfiguriert ist, ist das Produkt „Waffelmütze“ jetzt an den eVar6-Wert von „internal search:winter hat“ gebunden. Jedes Mal, wenn das „Waffelmütze“ Produkt gesammelt wird, wird es mit „Interne Suche:Wintermütze“ in Verbindung gebracht. Dies geschieht, bis entweder die eVar-Ablaufeinstellung erreicht ist oder ein neuer eVar6-Wert festgelegt ist und das Binding-Ereignis mit diesem Produkt erneut auftritt.
3. Der Benutzer fügt das Produkt zum Warenkorb hinzu und löst das `Cart Add`-Ereignis aus.
4. Der Benutzer führt eine weitere interne Suche nach „Summer Shirt“ durch, bei der die Konversionssyntax, die für Merchandising eVar6 aktiviert ist, auf „internal search:summer shirt“ gesetzt wird.
5. Der Benutzer wählt „sportliches T-Shirt“ und landet auf der Produktdetailseite.\
   a. Mit dem Öffnen der Seite wird ein `Product View`-Ereignis für das „Sportliche T-Shirt“ für $19,99 ausgelöst.\
   b. Da das `Product View` das Binding Event ist, ist das Produkt „Sportliches T-Shirt“ jetzt an den eVar6-Wert „internal search:summer shirt“ gebunden. Das Vorgängerprodukt „Waffelmütze“ ist noch an den eVar6-Wert „internal search:waffle beanie“ gebunden.
6. Der Benutzer fügt das Produkt zum Warenkorb hinzu und löst das `Cart Add`-Ereignis aus.
7. Der Benutzer checkt mit beiden Produkten aus.

In Berichten sind Bestellungen, Umsatz, Produktansichten und Hinzufügungen zum Warenkorb gegenüber eVar6 zu melden und an die Aktivität des gebundenen Produkts anzupassen.

| eVar6 (Produktsuchmethode) | Umsatz | Bestellungen | Produktansichten | Hinzufügen zum Warenkorb |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| Interne Suche:Sommerhemd | 19,99 | 1 | 1 | 1 |
| Interne Suche:Wintermütze | 12,99 | 1 | 1 | 1 |

Weitere Informationen zur Verwendung der Konversionsvariablensyntax finden Sie in der Adobe Analytics-Dokumentation unter [Implementieren von eVars mithilfe der Konversionsvariablensyntax](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=de#implement-using-conversion-variable-syntax).

Im Folgenden werden die XDM-Felder angezeigt, um die Konversionsvariablensyntax in Ihrem [!DNL Analytics] Datensatz zu erstellen:

#### eVars

```console
_experience.analytics.customDimensions.evars.evar#
```

* `evar#`: Die spezifische eVar-Variable, auf die Sie zugreifen.

#### Produkt

```console
productListItems[#].sku
```

* `#`: Der Index des Arrays, auf das Sie zugreifen.

## Anwendungsfälle für Konversionsvariablen {#conversion-variable-use-cases}

Die folgenden Anwendungsfälle spiegeln Szenarien wider, für die eine Konversionsvariablensyntax erforderlich ist.

### Binden des Werts an das spezifische Produkt- und Ereignispaar

Die nachstehende Abfrage bindet den Wert an das spezifische Produkt- und Ereignispaar. In diesem Beispiel ist der Wert an das Produktansichtsereignis gebunden.

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

### Den gebundenen Wert für nachfolgende Vorkommen des entsprechenden Produkts beibehalten

Die folgende Beispielabfrage behält den gebundenen Wert für nachfolgende Vorkommen des jeweiligen Produkts bei. Die niedrigste Unterabfrage stellt die Beziehung des Werts zum Produkt auf dem deklarierten Binding-Ereignis her. Die nächste Unterabfrage führt die Attribution dieses gebundenen Werts über nachfolgende Interaktionen mit dem jeweiligen Produkt durch. Die oberste Ebene SELECT aggregiert die Ergebnisse, um Berichte zu erstellen.

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

## Nächste Schritte

Durch Lesen dieses Dokuments sollten Sie besser verstehen, wie Sie eine Merchandising-eVar mithilfe der Produktsyntax zurückgeben und einen Wert mit der Konversionsvariablensyntax an ein bestimmtes Produkt binden können.

Wenn Sie dies noch nicht getan haben, sollten Sie als Nächstes die Dokumentation [Analytics Insights for Web and Mobile Interactions](./analytics-insights.md) lesen. Es bietet gängige Anwendungsfälle und zeigt, wie Sie mit dem Abfrage-Service umsetzbare Einblicke aus Web- und mobilen Adobe Analytics-Daten erstellen können.
