---
title: Prognostizieren der Kundenabwanderung mit SQL-basierter logistischer Regression
description: Erfahren Sie, wie Sie mithilfe einer SQL-basierten logistischen Regression Kundenabwanderungen vorhersagen können. Dieses Handbuch behandelt den gesamten Prozess von der Modellerstellung bis zur Bewertung und Prognose. Gewinnen Sie umsetzbare Einblicke aus dem Kaufverhalten des Kunden, um proaktive Aufbewahrungsstrategien zu implementieren und Geschäftsentscheidungen zu optimieren.
exl-id: 3b18870d-104c-4dce-8549-a6818dc40d24
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 1%

---

# Prognostizieren der Kundenabwanderung mit SQL-basierter logistischer Regression

Die Vorhersage von Kundenabwanderungen hilft Unternehmen, Kunden zu binden, Ressourcen zu optimieren und die Rentabilität zu steigern, indem die Zufriedenheit und Loyalität durch umsetzbare Einblicke verbessert werden.

Erfahren Sie, wie Sie mit SQL-basierter logistischer Regression Kundenabwanderungen vorhersagen können. Verwenden Sie dieses umfassende SQL-Handbuch, um E-Commerce-Rohdaten in aussagekräftige Kundeneinblicke umzuwandeln, die auf wichtigen Verhaltensmetriken basieren (z. B. Kaufhäufigkeit, durchschnittlicher Bestellwert und Neuigkeit des letzten Kaufs). Das Dokument umfasst den gesamten Prozess von der Datenvorbereitung und dem Feature Engineering bis hin zur Modellerstellung, -auswertung und -vorhersage.

Verwenden Sie dieses Handbuch, um ein leistungsstarkes Modell für Abwanderungsprognosen zu erstellen, mit dem gefährdete Kunden identifiziert, Aufbewahrungsstrategien verfeinert und bessere Geschäftsentscheidungen gefördert werden. Sie enthält schrittweise Anweisungen, SQL-Abfragen und detaillierte Erläuterungen, die Ihnen helfen, maschinelle Lerntechniken sicher in Ihrer Datenumgebung anzuwenden.

## Erste Schritte

Bevor Sie das Abwanderungsmodell erstellen, müssen Sie sich mit den wichtigsten Kundenfunktionen und Datenanforderungen befassen. In den folgenden Abschnitten werden wesentliche Kundenattribute und erforderliche Datenfelder für ein genaues Modell-Training beschrieben.

### Definieren von Kundenfunktionen {#define-customer-features}

Um Abwanderung genau zu klassifizieren, analysiert das Modell Kaufgewohnheiten und Trends. In der folgenden Tabelle sind die wichtigsten im Modell verwendeten Funktionen für das Kundenverhalten aufgeführt:

| Funktion | Beschreibung |
|---------------------------|-------------------------------------------------------|
| `total_purchases` | Die Gesamtzahl der vom Kunden getätigten Käufe. |
| `total_revenue` | Der Gesamtumsatz aus Käufen durch Kunden. |
| `avg_order_value` | Der durchschnittliche Wert der Käufe eines Kunden. |
| `customer_lifetime` | Die Anzahl der Tage zwischen dem ersten und letzten Kauf des Kunden. |
| `days_since_last_purchase` | Die Anzahl der Tage seit dem letzten Kauf des Kunden. |
| `purchase_frequency` | Die Anzahl der eindeutigen Monate, in denen der Kunde Käufe getätigt hat. |

### Annahmen und erforderliche Felder {#assumptions-required-fields}

Um Prognosen zur Kundenabwanderung zu generieren, hängt das Modell von Schlüsselfeldern in der `webevents` ab, die Details zu Kundentransaktionen erfassen. Ihr Datensatz muss die folgenden Felder enthalten:

| Feld | Beschreibung |
|--------------------------------|----------------------------------------------------|
| `identityMap['ECID'][0].id` | Eine eindeutige Kennung, mit der Kunden sitzungsübergreifend verfolgt werden. |
| `productListItems.priceTotal[0]` | Die Gesamtkosten der gekauften Artikel pro Transaktion. |
| `productListItems.quantity[0]` | Die Gesamtzahl der Artikel in einem Kauf. |
| `timestamp` | Das genaue Datum und die genaue Uhrzeit jedes Kaufereignisses. |
| `commerce.order.purchaseID` | Ein erforderlicher Wert, der einen abgeschlossenen Kauf bestätigt. |

Der Datensatz muss strukturierte historische Kundentransaktionsdatensätze enthalten, wobei jede Zeile ein Kaufereignis darstellt. Jedes Ereignis muss Zeitstempel in einem geeigneten Datums-/Uhrzeitformat enthalten, das mit der SQL-`DATEDIFF` kompatibel ist (z. B. JJJJ-MM-TT HH:MI:SS). Darüber hinaus muss jeder Datensatz eine gültige Experience Cloud-ID (`ECID`) im Feld `identityMap` enthalten, um Kunden eindeutig zu identifizieren.

>[!TIP]
>
>Die Verarbeitung großer Datensätze mit Millionen von Datensätzen kann die Leistung erheblich beeinträchtigen. Um die Ausführung der Abfrage zu optimieren, unterteilen Sie den Erlebnisdatensatz nach Zeitstempel, führen Sie eine inkrementelle Verarbeitung mithilfe von Momentaufnahmen durch und wenden Sie bei Bedarf effiziente Aggregationsfunktionen an. Filtern Sie außerdem die Daten vor der Aggregation, um den Verarbeitungsaufwand zu reduzieren.

## Modell erstellen {#create-a-model}

Um die Kundenabwanderung vorherzusagen, müssen Sie ein SQL-basiertes logistisches Regressionsmodell erstellen, das den Kaufverlauf und die Verhaltensmetriken der Kunden analysiert. Das Modell klassifiziert Kunden als `churned` oder `not churned`, indem es bestimmt, ob sie in den letzten 90 Tagen einen Kauf getätigt haben.

### Verwenden von SQL zur Erstellung des Prognosemodells für Abwanderungen {#sql-create-model}

Das SQL-basierte Modell verarbeitet `webevents` Daten, indem es Schlüsselmetriken aggregiert und Abwanderungskennzeichnungen auf Grundlage einer 90-tägigen Inaktivitätsregel zuweist. Dieser Ansatz unterscheidet aktive Kunden von Risikokunden. Die SQL-Abfrage führt auch Feature Engineering durch, um die Modellgenauigkeit zu verbessern und die Abwanderungsklassifizierung zu verbessern. Diese Einblicke ermöglichen Ihrem Unternehmen die Implementierung zielgerichteter Aufbewahrungsstrategien, reduzieren die Abwanderung und maximieren den Wert der Kundenlebenszeit.

>[!NOTE]
>
>Das Abwanderungs-Prognosemodell verwendet einen Standardschwellenwert von 90 Tagen, um Kunden als Abwanderung zu klassifizieren. Um diesen Schwellenwert an Ihre Geschäftsziele und Aufbewahrungsstrategien anzupassen, ändern Sie die `DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90` in den SQL-Abfragen.

Verwenden Sie die folgende SQL-Anweisung, um das `retention_model_logistic_reg` mit den angegebenen Funktionen und Beschriftungen zu erstellen:

```sql
CREATE MODEL retention_model_logistic_reg
TRANSFORM (
  vector_assembler(array(total_purchases, total_revenue, avg_order_value, customer_lifetime, days_since_last_purchase, purchase_frequency)) features
  -- Combines selected customer metrics into a feature vector for model training
)
OPTIONS (
  MODEL_TYPE = 'logistic_reg',  -- Specifies logistic regression as the model type
  LABEL = 'churned'             -- Defines the target label for churn classification
)
AS
WITH customer_features AS (
    SELECT
       identityMap['ECID'][0].id AS customer_id,  -- Extract the unique customer ID from identityMap
       AVG(COALESCE(productListItems.priceTotal[0], 0)) AS avg_order_value,  -- Calculates the average order value, and handles null values with COALESCE
       SUM(COALESCE(productListItems.priceTotal[0], 0)) AS total_revenue, -- The sum of all purchase values per customer
       COUNT(COALESCE(productListItems.quantity[0], 0)) AS total_purchases,  -- The total number of items purchased by the customer
       DATEDIFF(MAX(timestamp), MIN(timestamp)) AS customer_lifetime,  -- The days between first and last recorded purchase
       DATEDIFF(CURRENT_DATE, MAX(timestamp)) AS days_since_last_purchase,  -- The days since the last purchase event
       COUNT(DISTINCT CONCAT(YEAR(timestamp), MONTH(timestamp))) AS purchase_frequency  -- The count of unique months with purchases
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)  -- Filters transactions with valid total price
      AND commerce.`order`.purchaseID <> ''  -- Ensures the order has a valid purchase ID
    GROUP BY customer_id 
),
customer_labels AS (
    SELECT
      identityMap['ECID'][0].id AS customer_id,  -- Extract the unique customer ID for labeling
      CASE
          WHEN DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90 THEN 1  -- Marks the customer as churned if no purchase occurred in the last 90 days
          ELSE 0
      END AS churned
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0) 
      AND commerce.`order`.purchaseID <> ''  
    GROUP BY customer_id  
)
SELECT
    f.customer_id,
    f.total_purchases,
    f.total_revenue,
    f.avg_order_value,
    f.customer_lifetime,
    f.days_since_last_purchase,
    f.purchase_frequency,
    l.churned
FROM
    customer_features f
JOIN
    customer_labels l
ON f.customer_id = l.customer_id  -- Join features with churn labels
ORDER BY RANDOM()  -- Shuffles rows randomly for training
LIMIT 500000;  -- Limit the dataset to 500,000 rows for model training
```

### Modellausgabe {#model-output}

Der Ausgabedatensatz enthält kundenbezogene Metriken und deren Abwanderungsstatus. Jede Zeile stellt einen Kunden, seine Funktionswerte und seinen Abwanderungsstatus dar. Mithilfe dieser Ausgabe können Sie das Kundenverhalten analysieren, Prognosemodelle trainieren und zielgerichtete Aufbewahrungsstrategien entwickeln, um gefährdete Kunden zu binden. Nachfolgend finden Sie eine Beispiel-Ausgabetabelle:

```console
 customer_id  | total_purchases | total_revenue | avg_order_value  | customer_lifetime | days_since_last_purchase | purchase_frequency | churned |
|--------------+-----------------+---------------+------------------+-------------------+--------------------------+--------------------+----------
  100001      | 25              | 1250.00       | 50.00            | 540               | 20                       | 10                 | 0       
  100002      | 3               | 90.00         | 30.00            | 120               | 95                       | 1                  | 1       
  100003      | 60              | 7200.00       | 120.00           | 800               | 5                        | 24                 | 0       
  100004      | 15              | 750.00        | 50.00            | 365               | 60                       | 8                  | 0       
  100005      | 1               | 25.00         | 25.00            | 60                | 180                      | 1                  | 1       
```

| Spalte | Beschreibung |
|-----------|------------------------------------------------------------------------------------|
| `churned` | Der Wert gibt an, ob der Kunde innerhalb der letzten 90 Tage einen Kauf getätigt hat (0 = nicht abgewandert, 1 = abgewandert). |

## SQL zur Auswertung des Modells verwenden {#model-evaluation}

Bewerten Sie anschließend das Abwanderungsvorhersagungsmodell, um seine Effektivität bei der Identifizierung gefährdeter Kunden zu bestimmen. Bewerten Sie die Modellleistung mit Schlüsselmetriken, die Genauigkeit und Zuverlässigkeit messen.

Verwenden Sie die `retention_model_logistic_reg`-Funktion, um die Genauigkeit des `model_evaluate`-Modells bei der Prognose der Kundenabwanderung zu messen. Im folgenden SQL-Beispiel wird das Modell mithilfe eines Datensatzes ausgewertet, der wie die Trainingsdaten strukturiert ist:

```sql
SELECT * 
FROM model_evaluate(retention_model_logistic_reg, 1,
WITH customer_features AS (
    SELECT
       identityMap['ECID'][0].id AS customer_id,
       AVG(COALESCE(productListItems.priceTotal[0], 0)) AS avg_order_value,
       SUM(COALESCE(productListItems.priceTotal[0], 0)) AS total_revenue,
       COUNT(COALESCE(productListItems.quantity[0], 0)) AS total_purchases, 
       DATEDIFF(MAX(timestamp), MIN(timestamp)) AS customer_lifetime,
       DATEDIFF(CURRENT_DATE, MAX(timestamp)) AS days_since_last_purchase,
       COUNT(DISTINCT CONCAT(YEAR(timestamp), MONTH(timestamp))) AS purchase_frequency 
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)
      AND commerce.`order`.purchaseID <> ''
    GROUP BY customer_id
),
customer_labels AS (
    SELECT
      identityMap['ECID'][0].id AS customer_id,
      CASE
          WHEN DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90 THEN 1 
          ELSE 0
      END AS churned
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0) 
      AND commerce.`order`.purchaseID <> '' 
    GROUP BY customer_id
)
SELECT
    f.customer_id,
    f.total_purchases,
    f.total_revenue,
    f.avg_order_value,
    f.customer_lifetime,
    f.days_since_last_purchase,
    f.purchase_frequency,
    l.churned
FROM
    customer_features f
JOIN
    customer_labels l
ON f.customer_id = l.customer_id); -- Joins customer features with churn labels
```

### Ausgabe der Modellevaluierung

Die Auswertungsausgabe enthält wichtige Leistungsmetriken wie AUC-ROC, Genauigkeit, Präzision und Rückruf. Diese Metriken liefern Einblicke in die Effektivität von Modellen, mit denen Sie Aufbewahrungsstrategien verfeinern und datengestützte Entscheidungen treffen können.

>[!NOTE]
>
>Die Leistungswerte liegen zwischen 0 und 1, wobei 1,0 die perfekte Leistung darstellt.

```console
 auc_roc | accuracy | precision | recall 
|---------+----------+-----------+--------
1        | 0.99998  |  1        |  1      
```

| Metrik | Beschreibung |
|------------|-------------------------------------------------------------------------|
| `auc_roc` | Diese Metrik zeigt die Fähigkeit des Modells an, zwischen abgewanderten und nicht abgewanderten Kunden zu unterscheiden. Ein Wert näher an 1 bedeutet eine bessere Leistung. |
| `accuracy` | Die Genauigkeitsmetrik stellt den Anteil der korrekten Prognosen dar und bietet somit ein Gesamtmaß für die Modellleistung. |
| `precision` | Präzision zeigt den Anteil der korrekt identifizierten abgewanderten Kunden an und zeigt Zuverlässigkeit bei der Abwanderungsvorhersage. Ein hoher Wert bedeutet weniger falsch-positive Ergebnisse. |
| `recall` | Mit Rückruf wird die Fähigkeit des Modells gemessen, alle tatsächlich abgewanderten Kunden zu identifizieren. Ein hoher Rückrufwert zeigt an, dass weniger Kunden abwandern. |

>[!NOTE]
>
>Die nahezu perfekten Werte in diesem Beispiel dienen zu Demonstrationszwecken. In der Praxis können reale Daten aufgrund von Rauschen und Schwankungen niedrigere Werte ergeben.

## Prognose des Modells {#model-prediction}

Nachdem das Modell evaluiert wurde, verwenden Sie `model_predict` , um es auf einen neuen Datensatz anzuwenden und die Kundenabwanderung zu prognostizieren. Sie können diese Prognosen verwenden, um gefährdete Kunden zu identifizieren und zielgerichtete Aufbewahrungsstrategien zu implementieren.

### SQL zur Erzeugung von Abwanderungsprognosen verwenden {#sql-model-predict}

Die folgende SQL-Abfrage verwendet das `retention_model_logistic_reg`, um Kundenabwanderung mit einem Datensatz vorherzusagen, der wie die Schulungsdaten strukturiert ist:

```sql
SELECT * 
FROM model_predict(retention_model_logistic_reg, 1,  -- Applies the trained model for churn prediction
WITH customer_features AS (
    SELECT
       identityMap['ECID'][0].id AS customer_id,
       AVG(COALESCE(productListItems.priceTotal[0], 0)) AS avg_order_value,  
       SUM(COALESCE(productListItems.priceTotal[0], 0)) AS total_revenue, 
       COUNT(COALESCE(productListItems.quantity[0], 0)) AS total_purchases,  
       DATEDIFF(MAX(timestamp), MIN(timestamp)) AS customer_lifetime,  
       DATEDIFF(CURRENT_DATE, MAX(timestamp)) AS days_since_last_purchase,  
       COUNT(DISTINCT CONCAT(YEAR(timestamp), MONTH(timestamp))) AS purchase_frequency  
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)  -- Ensures only valid purchase data is considered
      AND commerce.`order`.purchaseID <> ''  
    GROUP BY customer_id
),
customer_labels AS (
    SELECT
      identityMap['ECID'][0].id AS customer_id,  
      CASE
          WHEN DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90 THEN 1  -- Identify customers who have not purchased in the last 90 days
          ELSE 0
      END AS churned
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)  
      AND commerce.`order`.purchaseID <> ''  
    GROUP BY customer_id
)
SELECT
    f.customer_id,  
    f.total_purchases,  
    f.total_revenue,  
    f.avg_order_value,  
    f.customer_lifetime,  
    f.days_since_last_purchase,  
    f.purchase_frequency,  
    l.churned  
FROM
    customer_features f
JOIN
    customer_labels l
ON f.customer_id = l.customer_id);  -- Matches features with their churn labels for prediction
```

### Modellvorhersageausgabe {#prediction-output}

Der Ausgabedatensatz enthält wichtige Kundenfunktionen und den prognostizierten Abwanderungsstatus, der angibt, ob eine Abwanderung wahrscheinlich ist. Nutzen Sie diese Erkenntnisse, um proaktive Strategien zur Kundenbindung zu implementieren und die Kundenabwanderung zu reduzieren.

```console
 total_purchases | total_revenue | avg_order_value | customer_lifetime | days_since_last_purchase | purchase_frequency | churned | prediction
|-----------------+---------------+-----------------+-------------------+--------------------------+--------------------+---------+------------
 2               | 299           | 149.5           | 0                 | 13                        | 1                  | 0       | 0
 1               | 710           | 710.00          | 0                 | 149                       | 1                  | 1       | 1
 1               | 19.99         | 19.99           | 0                 | 30                        | 1                  | 0       | 0
 1               | 4528          | 4528.00         | 0                 | 26                        | 1                  | 0       | 0
 1               | 21.84         | 21.84           | 0                 | 90                        | 1                  | 0       | 0
 1               | 16.64         | 16.64           | 0                 | 268                       | 1                  | 1       | 1
```

| Spalte | Beschreibung |
|---------------|-------------------------------------------------------------------------------|
| `prediction` | Der prognostizierte Abwanderungsstatus des Kunden basierend auf dem Modell (0 = nicht abgewandert, 1 = abgewandert). |

## Nächste Schritte

Sie haben jetzt gelernt, wie Sie ein SQL-basiertes Modell erstellen, auswerten und verwenden können, um die Kundenabwanderung vorherzusagen. Auf dieser Grundlage können Sie das Kundenverhalten analysieren, gefährdete Kunden identifizieren und proaktive Kundenbindungsstrategien implementieren, um die Kundenbindung zu verbessern. Zur weiteren Verbesserung und Anwendung Ihres Abwanderungs-Prognosemodells sollten Sie die folgenden Schritte in Betracht ziehen:

- Automatisieren Sie den Prozess: Integrieren Sie das Modell in eine Datenpipeline für die kontinuierliche Überwachung und Echtzeit-Einblicke. [Erfahren Sie, wie Sie Datensätze mit SQL überprüfen und verarbeiten](../../../dashboards/query.md).
- Überwachen der Modellleistung: Bewerten Sie das Modell kontinuierlich mit neuen Daten, um Genauigkeit und Relevanz zu gewährleisten.  Verwenden Sie [KI-](../../../ai-assistant/landing.md)) in der Adobe Experience Platform-Benutzeroberfläche, um wichtige Leistungsänderungen zu überwachen und [Zielgruppentrends vorherzusagen](../../../ai-assistant/new-features/audience-forecasting.md).
