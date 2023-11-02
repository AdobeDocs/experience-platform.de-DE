---
title: Rückgabe und Verwendung von Merchandising-Variablen aus Analysedaten
description: Erfahren Sie, wie Sie XDM-Felder und Beispielabfragen bereitstellen, um auf die Merchandising-Variablen in Ihren Analytics-Datensätzen zuzugreifen.
exl-id: 1e2ae095-4152-446f-8b66-dae5512d690e
source-git-commit: 7cde32f841497edca7de0c995cc4c14501206b1a
workflow-type: tm+mt
source-wordcount: '1103'
ht-degree: 14%

---

# Zurückgeben und Verwenden von Merchandising-Variablen aus Analysedaten 

Verwenden Sie Query Service , um die Daten zu verwalten, die von Adobe Analytics als Datensätze in Adobe Experience Platform erfasst werden. Die folgenden Abschnitte enthalten Beispielabfragen, mit denen Sie auf die Merchandising-Variablen in Ihren Analytics-Datensätzen zugreifen können. Weitere Informationen finden Sie in der Dokumentation zu [Erfassen und Zuordnen von Adobe Analytics-Daten](../../sources/connectors/adobe-applications/mapping/analytics.md) über die Analytics-Quelle

## Merchandising-Variablen {#merchandising-variables}

Merchandisingvariablen können einer oder zwei Syntaxen folgen:

* **Produktsyntax**: Verbindet den eVar mit einem Produkt. 
* **Syntax der Konversionsvariablen**: Verbindet den eVar nur dann mit einem Produkt, wenn ein Binding-Ereignis auftritt. Sie können die Ereignisse auswählen, die als Binding-Ereignisse dienen.

## Produktsyntax {#product-syntax}

In Adobe Analytics können benutzerdefinierte Daten auf Produktebene über speziell konfigurierte Variablen, so genannte Merchandising-Variablen, erfasst werden. Diese basieren entweder auf einem eVar oder auf benutzerdefinierten Ereignissen. Der Unterschied zwischen diesen Variablen und ihrer typischen Verwendung besteht darin, dass sie für jedes beim Treffer gefundene Produkt einen separaten Wert darstellen und nicht nur einen einzelnen Wert für den Treffer.

Diese Variablen werden als Merchandising-Variablen mit Produktsyntax bezeichnet. Dies ermöglicht die Erfassung von Informationen, z. B. einen pro Produkt ausgegebenen &quot;Rabattbetrag&quot;oder Informationen über die &quot;Position des Produkts auf der Seite&quot;in den Suchergebnissen des Kunden.

Weitere Informationen zur Verwendung der Produktsyntax finden Sie in der Adobe Analytics-Dokumentation unter [Implementieren von eVars mit Produktsyntax](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html#implement-using-product-syntax).

In den folgenden Abschnitten werden die XDM-Felder beschrieben, die für den Zugriff auf die Merchandising-Variablen in Ihren [!DNL Analytics] Datensatz:

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
* `event#`: Die spezifische benutzerspezifische Ereignisvariable, auf die Sie zugreifen.

## Anwendungsfälle für die Produktsyntax {#product-use-cases}

Die folgenden Anwendungsbeispiele konzentrieren sich auf die Rückgabe eines Merchandising-eVar aus dem `productListItems` -Array mit SQL.

### Merchandising-eVar und -Ereignis zurückgeben

Die nachstehende Abfrage gibt ein Merchandising-eVar und -Ereignis für das erste Produkt zurück, das im `productListItems` Array.

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

### Explodieren Sie das productListItems-Array und geben Sie das Merchandising-eVar und -Ereignis für jedes Produkt zurück.

Diese nächste Abfrage explodiert die `productListItems` und gibt jedes Merchandising-eVar und -Ereignis pro Produkt zurück. Das `_id`-Feld ist enthalten, um die Beziehung zum ursprünglichen Treffer anzuzeigen. Die `_id` -Wert ist ein eindeutiger Primärschlüssel für den Datensatz.

>[!NOTE]
>
>Die Explode-Funktion trennt die Elemente eines Arrays in mehrere Zeilen. Null-Werte werden ausgeschlossen.

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
> Wenn Sie versuchen, ein Feld abzurufen, das im aktuellen Datensatz nicht vorhanden ist, tritt der Fehler &quot;No such struct field&quot;auf. Werten Sie den in der Fehlermeldung zurückgegebenen Grund aus, um ein verfügbares Feld zu identifizieren, aktualisieren Sie dann Ihre Abfrage und führen Sie sie erneut aus.
>
>```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### Syntax der Konversionsvariablen {#conversion-variable-syntax}

Ein weiterer in Adobe Analytics zu findender Merchandising-Variablentyp ist die Syntax der Konversionsvariablen. Die Syntax der Konversionsvariablen wird verwendet, wenn der eVar nicht für die Variable &quot;products&quot;verfügbar ist. Dieses Szenario bedeutet in der Regel, dass Ihre Seite keinen Kontext für den Merchandising-Kanal oder die Suchmethode hat. In diesen Fällen sollten Sie die Merchandising-Variable festlegen, bevor der Benutzer zur Produktseite gelangt, und der Wert bleibt bestehen, bis das Binding-Ereignis eintritt.

Das folgende Produktergebnis zeigt beispielsweise, wie die erforderlichen Daten auf einer Seite vorhanden sein können, bevor die mit dem Produkt in Verbindung stehende Konversion oder das Ereignis eintritt.

1. Ein Benutzer führt eine interne Suche nach &quot;Wintermütze&quot;durch, wodurch die für die Konversionssyntax aktivierte Merchandising-eVar6 auf &quot;Interne Suche:Wintermütze&quot;gesetzt wird.
2. Der Benutzer klickt auf „Waffelmütze“ und wird zur Produktdetailseite weitergeleitet.\
   a. Mit dem Öffnen der Seite wird ein `Product View`-Ereignis für die „Waffelmütze“ für $12,99 ausgelöst.\
   b. Seit `Product View` als Binding-Ereignis konfiguriert ist, ist das Produkt &quot;Waffelmütze&quot;jetzt an den eVar6-Wert von &quot;Interne Suche:Wintermütze&quot;gebunden. Jedes Mal, wenn das Produkt &quot;Waffelmütze&quot;erfasst wird, wird es mit &quot;Interne Suche:Wintermütze&quot;verknüpft. Dies geschieht, bis entweder die Ablaufeinstellung der eVar erreicht ist oder ein neuer eVar6-Wert festgelegt und das Binding-Ereignis mit diesem Produkt erneut auftritt.
3. Der Benutzer fügt das Produkt zum Warenkorb hinzu und löst das `Cart Add`-Ereignis aus.
4. Der Benutzer führt eine weitere interne Suche nach &quot;Sommerhemd&quot;durch, wodurch die Konversionssyntax für Merchandising eVar6 auf &quot;Interne Suche:Sommerhemd&quot;gesetzt wird.
5. Der Benutzer wählt &quot;Sportliches T-Shirt&quot;aus und landet auf der Produktdetailseite.\
   a. Mit dem Öffnen der Seite wird ein `Product View`-Ereignis für das „Sportliche T-Shirt“ für $19,99 ausgelöst.\
   b. Als `Product View` -Ereignis das Binding-Ereignis ist, ist das Produkt &quot;Sportliches T-Shirt&quot;jetzt an den eVar 6-Wert von &quot;Interne Suche:Sommerhemd&quot;gebunden. Das frühere Produkt &quot;Waffelmütze&quot;ist weiterhin an den Wert von eVar 6 &quot;Interne Suche:Waffelmütze&quot;gebunden.
6. Der Benutzer fügt das Produkt zum Warenkorb hinzu und löst das `Cart Add`-Ereignis aus.
7. Der Benutzer checkt mit beiden Produkten aus.

In Berichten sind die Bestellungen, der Umsatz, die Produktansichten und die Hinzufügungen zum Warenkorb gegenüber eVar6 gemeldet und richten sich an die Aktivität des gebundenen Produkts.

| eVar6 (Methode zur Produktsuche) | Umsatz | Bestellungen | Produktansichten | Hinzufügen zum Warenkorb |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| Interne Suche:Sommerhemd | 19,99 | 1 | 1 | 1 |
| Interne Suche:Wintermütze | 12,99 | 1 | 1 | 1 |

Weitere Informationen zur Verwendung der Konversionsvariablensyntax finden Sie in der Adobe Analytics-Dokumentation unter [Implementieren von eVars mit der Syntax von Konversionsvariablen](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html#implement-using-conversion-variable-syntax).

Im Folgenden werden die XDM-Felder angezeigt, um die Konversionsvariablensyntax in Ihrer [!DNL Analytics] Datensatz:

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

Die folgenden Anwendungsfälle spiegeln Szenarien wider, die die Syntax der Konversionsvariablen erfordern.

### Binden Sie den Wert an das spezifische Produkt- und Ereignispaar

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

### Beibehalten des gebundenen Werts für nachfolgende Vorkommen des jeweiligen Produkts

Die folgende Beispielabfrage behält den gebundenen Wert für nachfolgende Vorkommen des jeweiligen Produkts bei. Die niedrigste Unterabfrage ermittelt die Beziehung des Werts zum Produkt zum deklarierten Binding-Ereignis. Die nächste Unterabfrage führt die Attribution dieses gebundenen Werts über nachfolgende Interaktionen mit dem jeweiligen Produkt durch. Die Auswahl der obersten Ebene aggregiert die Ergebnisse zur Erstellung der Berichterstellung.

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

Wenn Sie dies noch nicht getan haben, sollten Sie die [Dokumentation zu Analytics-Einblicken für Web- und mobile Interaktionen](./analytics-insights.md) als Nächstes. Sie bietet gängige Anwendungsfälle und zeigt, wie Sie mit Query Service praktische Einblicke aus Web- und mobilen Adobe Analytics-Daten erstellen können.
