---
title: Regressionsalgorithmen
description: Erfahren Sie, wie Sie verschiedene Regressionsalgorithmen mit Schlüsselparametern, Beschreibungen und Beispielcode konfigurieren und optimieren können, um Ihnen bei der Implementierung erweiterter statistischer Modelle zu helfen.
role: Developer
exl-id: d38733bb-0420-40bf-a70b-19e0e0e58730
source-git-commit: 8b9cfb48a11701f0e4b358416c6b627bedf1db8b
workflow-type: tm+mt
source-wordcount: '2384'
ht-degree: 4%

---

# Regressionsalgorithmen {#regression-algorithms}

Dieses Dokument bietet einen Überblick über verschiedene Regressionsalgorithmen, die sich auf ihre Konfiguration, Schlüsselparameter und praktische Verwendung in erweiterten statistischen Modellen konzentrieren. Regressionsalgorithmen werden verwendet, um die Beziehung zwischen abhängigen und unabhängigen Variablen zu modellieren und kontinuierliche Ergebnisse basierend auf den beobachteten Daten vorherzusagen. Jeder Abschnitt enthält Parameterbeschreibungen und Beispielcode, mit denen Sie diese Algorithmen für Aufgaben wie lineare, zufällige Wälder und Überlebensregression implementieren und optimieren können.

## [!DNL Decision Tree] Regression {#decision-tree-regression}

[!DNL Decision Tree] learning ist eine beaufsichtigte Lernmethode, die in Statistiken, Data Mining und maschinellem Lernen verwendet wird. Bei diesem Ansatz wird ein Entscheidungsbaum für Klassifizierungs- oder Regressionsentscheidungen als Vorhersagemodell verwendet, um Schlussfolgerungen zu einer Reihe von Beobachtungen zu ziehen.

**Parameter**

In der folgenden Tabelle sind die wichtigsten Parameter für die Konfiguration und Optimierung der Leistung von Entscheidungsbaummodellen aufgeführt.

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|--------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Dieser Parameter gibt die maximale Anzahl von Klassen an, die verwendet werden, um kontinuierliche Funktionen zu diskretisieren und Aufspaltungen an jedem Knoten zu bestimmen. Mehr Klassen führen zu feiner Granularität und Details. | 32 | Muss mindestens 2 und mindestens die Anzahl der Kategorien in einer beliebigen kategorischen Funktion betragen. |
| `CACHE_NODE_IDS` | Dieser Parameter bestimmt, ob Knoten-IDs für jede Instanz zwischengespeichert werden. Wenn `false`, übergibt der Algorithmus Bäume an Executors, um Instanzen mit Knoten abzugleichen. Wenn der Wert `true` ist, speichert der Algorithmus Knoten-IDs für jede Instanz zwischen, was das Training tiefer liegender Bäume beschleunigen kann. Benutzer können konfigurieren, wie oft der Cache überprüft werden soll, oder deaktivieren ihn, indem sie `CHECKPOINT_INTERVAL` festlegen. | false | `true` oder `false` |
| `CHECKPOINT_INTERVAL` | Dieser Parameter gibt an, wie oft die zwischengespeicherten Knoten-IDs überprüft werden sollen. Wenn Sie sie beispielsweise auf &quot;`10`&quot;setzen, wird der Cache alle 10 Iterationen überprüft. Dies gilt nur, wenn `CACHE_NODE_IDS` auf `true` gesetzt ist und das Checkpoint-Verzeichnis in `org.apache.spark.SparkContext` konfiguriert ist. | 10 | (>=1) |
| `IMPURITY` | Dieser Parameter gibt das für die Berechnung des Informationsgewinns verwendete Kriterium an. Unterstützte Werte sind `entropy` und `gini`. | `gini` | `entropy`, `gini` |
| `MAX_DEPTH` | Dieser Parameter gibt die maximale Tiefe der Baumstruktur an. Beispielsweise bedeutet eine Tiefe von &quot;`0`&quot; einen Blattknoten, während eine Tiefe von &quot;`1`&quot; 1 interner Knoten und 2 Blattknoten bedeutet. Die Tiefe muss im Bereich `[0, 30]` liegen. | 5 | [0, 30] |
| `MIN_INFO_GAIN` | Dieser Parameter legt den Mindestinformationsgewinn fest, der erforderlich ist, damit eine Aufspaltung in einem Strukturknoten als gültig betrachtet werden kann. | 0,0 | (>=0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | Dieser Parameter gibt den minimalen Anteil der gewichteten Stichprobenanzahl an, den jeder untergeordnete Knoten nach einer Aufspaltung aufweisen muss. Wenn einer der untergeordneten Knoten einen Bruchteil unter diesem Wert hat, wird die Aufspaltung verworfen. | 0,0 | [0.0, 0.5] |
| `MIN_INSTANCES_PER_NODE` | Dieser Parameter legt die Mindestanzahl von Instanzen fest, die jeder untergeordnete Knoten nach einer Aufspaltung aufweisen muss. Wenn eine Aufspaltung zu weniger Instanzen als diesem Wert führt, wird die Aufspaltung als ungültig verworfen. | 1 | (>=1) |
| `MAX_MEMORY_IN_MB` | Dieser Parameter gibt den maximal zugewiesenen Speicher in Megabyte (MB) für die Histogrammaggregation an. Wenn der Speicher zu klein ist, wird nur ein Knoten pro Iteration aufgeteilt und die Aggregate können diese Größe überschreiten. | 256 | Ein positiver ganzzahliger Wert |
| `PREDICTION_COL` | Dieser Parameter gibt den Namen der Spalte an, die zum Speichern von Prognosen verwendet wird. | &quot;prediction&quot; | Beliebige Zeichenfolge |
| `SEED` | Dieser Parameter legt den im Modell verwendeten zufälligen Test fest. | Keine | Beliebige 64-Bit-Zahl |
| `WEIGHT_COL` | Dieser Parameter gibt den Namen der Gewichtungsspalte an. Wenn dieser Parameter nicht festgelegt oder leer ist, werden alle Instanzgewichte als `1.0` behandelt. | Nicht festgelegt | Beliebige Zeichenfolge |

{style="table-layout:auto"}

**Beispiel**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'decision_tree_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Factorization Machines] Regression {#factorization-machines-regression}

[!DNL Factorization Machines] ist ein Regressions-Lernalgorithmus, der den normalen Abstieg des Farbverlaufs und den AdamW-Löser unterstützt. Der Algorithmus basiert auf dem Papier von S. Rendle (2010), &quot;[!DNL Factorization Machines]&quot;.

**Parameter**

In der folgenden Tabelle sind die wichtigsten Parameter für die Konfiguration und Optimierung der Leistung der [!DNL Factorization Machines] -Regression aufgeführt.

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|------------------------|-------------------------------------------------------------------------------------------------|---------------|-----------------------|
| `TOL` | Dieser Parameter gibt die Konvergenztoleranz für den Algorithmus an. Höhere Werte können zu einer schnelleren Konvergenz führen, aber weniger Genauigkeit. | `1E-6` | (>= 0) |
| `FACTOR_SIZE` | Dieser Parameter definiert die Dimensionalität der Faktoren. Höhere Werte erhöhen die Modellkomplexität. | 8 | (>= 0) |
| `FIT_INTERCEPT` | Dieser Parameter gibt an, ob das Modell einen Konstanten-Begriff enthalten soll. | `true` | `true`, `false` |
| `FIT_LINEAR` | Dieser Parameter gibt an, ob ein linearer Begriff (auch als 1-Weg-Begriff bezeichnet) in das Modell aufgenommen werden soll. | `true` | `true`, `false` |
| `INIT_STD` | Dieser Parameter definiert die Standardabweichung der anfänglichen Koeffizienten, die im Modell verwendet werden. | 0,01 | (>= 0) |
| `MAX_ITER` | Dieser Parameter gibt die maximale Anzahl von Iterationen an, die der Algorithmus ausführen soll. | 100 | (>= 0) |
| `MINI_BATCH_FRACTION` | Dieser Parameter legt die Mini-Batch-Fraktion fest, die den in den einzelnen Batches verwendeten Datenanteil bestimmt. Sie muss im Bereich `(0, 1]` liegen. | 1,0 | `(0, 1]` |
| `REG_PARAM` | Dieser Parameter legt den Regularisierungsparameter fest, um eine Überanpassung zu verhindern. | 0,0 | (>= 0) |
| `SEED` | Dieser Parameter gibt den für die Modellinitialisierung verwendeten Zufallsstichprobe an. | Keine | Beliebige 64-Bit-Zahl |
| `SOLVER` | Dieser Parameter gibt den für die Optimierung verwendeten Solver-Algorithmus an. | &quot;adamW&quot; | `gd` (Verlaufswert), `adamW` |
| `STEP_SIZE` | Dieser Parameter gibt die anfängliche Schrittgröße (oder Lernrate) für den ersten Optimierungsschritt an. | 1,0 | Alle positiven Werte |
| `PREDICTION_COL` | Dieser Parameter gibt den Namen der Spalte an, in der Prognosen gespeichert werden. | &quot;prediction&quot; | Beliebige Zeichenfolge |

{style="table-layout:auto"}

**Beispiel**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'factorization_machines_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Generalized Linear] Regression {#generalized-linear-regression}

Im Gegensatz zu einer linearen Regression, bei der davon ausgegangen wird, dass das Ergebnis einer normalen (gaussischen) Verteilung folgt, ermöglichen [!DNL Generalized Linear] Modelle (GLMs) je nach Art der Daten unterschiedliche Verteilungstypen wie [!DNL Poisson] oder Binomial.

**Parameter**

In der folgenden Tabelle sind die wichtigsten Parameter für die Konfiguration und Optimierung der Leistung der [!DNL Generalized Linear] -Regression aufgeführt.

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-------------------------------------------------------------------------|
| `MAX_ITER` | Legt die maximale Anzahl von Iterationen fest (anwendbar bei Verwendung des Lötmittels `irls`). | 25 | (>= 0) |
| `REG_PARAM` | Der Regularisierungsparameter. | NICHT GESETZT | (>= 0) |
| `TOL` | Die Konvergenztoleranz. | `1E-6` | (>= 0) |
| `AGGREGATION_DEPTH` | Die empfohlene Tiefe für `treeAggregate`. | 2 | (>= 2) |
| `FAMILY` | Der Familienparameter, der die im Modell verwendete Fehlerverteilung beschreibt. Unterstützte Optionen sind `gaussian`, `binomial`, `poisson`, `gamma` und `tweedie`. | &quot;gaussisch&quot; | `gaussian`, `binomial`, `poisson`, `gamma`, `tweedie` |
| `FIT_INTERCEPT` | Ob ein Begriffsbegriff passt. | `true` | `true`, `false` |
| `LINK` | Die Verknüpfungsfunktion, die die Beziehung zwischen dem linearen Prädiktor und dem arithmetischen Mittel der Verteilungsfunktion definiert. Unterstützte Optionen sind `identity`, `log`, `inverse`, `logit`, `probit`, `cloglog` und `sqrt`. | NICHT GESETZT | `identity`, `log`, `inverse`, `logit`, `probit`, `cloglog`, `sqrt` |
| `LINK_POWER` | Dieser Parameter gibt den Index in der Power Link-Funktion an. Der Parameter gilt nur für die [!DNL Tweedie] -Familie. Wenn nicht festgelegt, wird standardmäßig `1 - variancePower` verwendet, was mit dem R `statmod`-Paket übereinstimmt. Spezifische Verknüpfungsmächte von 0, 1, -1 und 0.5 entsprechen den Links Protokoll, Identität, Umgekehrt und SQL. | 1 | Beliebiger numerischer Wert |
| `SOLVER` | Der für die Optimierung verwendete Lösungs-Algorithmus. Unterstützte Option: `irls` (die kleinsten Quadrate werden iterativ neu gewichtet). | &quot;irls&quot; | `irls` |
| `VARIANCE_POWER` | Dieser Parameter gibt die Leistung in der Varianzfunktion der [!DNL Tweedie] -Verteilung an und definiert die Beziehung zwischen Varianz und Mittelwert. Die unterstützten Werte sind 0 und `[1, inf)`. Die Varianz von 0, 1 und 2 entspricht jeweils den Familien Gaussisch, Poisson und Gamma. | 0,0 | 0, `[1, inf)` |
| `LINK_PREDICTION_COL` | Der Spaltenname der Link-Prognose (Lineare Vorhersage). | NICHT GESETZT | Beliebige Zeichenfolge |
| `OFFSET_COL` | Der Name der Offset-Spalte. Wenn nicht festgelegt, werden alle Instanzabweichungen als 0.0 behandelt. Die Offset-Funktion hat einen konstanten Koeffizienten von 1,0. | NICHT GESETZT | Beliebige Zeichenfolge |
| `WEIGHT_COL` | Der Name der Gewichtungsspalte. Wenn nicht festgelegt oder leer, werden alle Instanzgewichte als `1.0` behandelt. In der Binomial-Familie entsprechen die Gewichtungen der Anzahl der Versuche und die nicht ganzzahligen Gewichtungen werden in der AIC-Berechnung gerundet. | NICHT GESETZT | Beliebige Zeichenfolge |

{style="table-layout:auto"}

**Beispiel**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'generalized_linear_reg'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Gradient Boosted Tree] Regression {#gradient-boosted-tree-regression}

Verlaufsgeboostete Bäume (GBTs) sind eine effektive Methode zur Klassifizierung und Regression, die die Vorhersagen mehrerer Entscheidungsbäume kombiniert, um die Vorhersagegenauigkeit und Modellleistung zu verbessern.

**Parameter**

In der folgenden Tabelle sind die wichtigsten Parameter für die Konfiguration und Optimierung der Leistung der [!DNL Gradient Boosted Tree] -Regression aufgeführt.

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|-------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Die maximale Anzahl von Klassen, die verwendet werden, um kontinuierliche Funktionen in diskrete Intervalle zu unterteilen, wodurch bestimmt wird, wie Funktionen auf jedem Entscheidungsbaum-Knoten aufgeteilt werden. Mehr Klassen bieten eine höhere Granularität. | 32 | Muss mindestens 2 und gleich oder größer als die Anzahl der Kategorien in einer beliebigen kategorischen Funktion sein. |
| `CACHE_NODE_IDS` | Wenn `false`, übergibt der Algorithmus Bäume an Executors, um Instanzen mit Knoten abzugleichen. Wenn `true`, speichert der Algorithmus Knoten-IDs für jede Instanz zwischen. Caching kann das Training tiefer liegender Bäume beschleunigen. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Gibt an, wie oft die zwischengespeicherten Knoten-IDs überprüft werden. Beispiel: `10` bedeutet, dass der Cache alle 10 Iterationen überprüft wird. | 10 | (>= 1) |
| `MAX_DEPTH` | Die maximale Tiefe der Baumstruktur (nicht negativ). Beispielsweise bedeutet &quot;depth `0`&quot;einen Blattknoten und &quot;depth `1`&quot;einen internen Knoten mit 2 Blattknoten. | 5 | (>= 0) |
| `MIN_INFO_GAIN` | Der Mindestinformationsgewinn, der erforderlich ist, damit eine Aufspaltung in einem Strukturknoten berücksichtigt werden kann. | 0,0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | Der Mindestanteil der gewichteten Stichprobenanzahl, die jedes Kind nach einer Aufspaltung aufweisen muss. Wenn eine Aufspaltung dazu führt, dass der Anteil des Gesamtgewichts in einem der untergeordneten Elemente kleiner als dieser Wert ist, wird er verworfen. | 0,0 | (>= 0.0, &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | Die Mindestanzahl von Instanzen, die jedes untergeordnete Element nach einer Aufspaltung aufweisen muss. Wenn eine Aufspaltung zu weniger Instanzen als diesem Wert führt, wird die Aufspaltung verworfen. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Der maximale Speicher in MB, der der Histogrammaggregation zugeordnet ist. Wenn dieser Wert zu klein ist, wird nur 1 Knoten pro Iteration aufgeteilt und die Aggregate können diese Größe überschreiten. | 256 | Ein positiver ganzzahliger Wert |
| `PREDICTION_COL` | Der Spaltenname für die Ausgabe der Prognose. | &quot;prediction&quot; | Beliebige Zeichenfolge |
| `VALIDATION_INDICATOR_COL` | Der Spaltenname, der angibt, ob die einzelnen Zeilen für Schulungen oder Überprüfungen verwendet werden. `false` für Schulung und `true` für Validierung. | NICHT GESETZT | Beliebige Zeichenfolge |
| `LEAF_COL` | Der Spaltenname für Blattindizes. Der prognostizierte Blattindex jeder Instanz in jedem Baum, generiert durch Preorder Traversal. | &quot;&quot; | Beliebige Zeichenfolge |
| `FEATURE_SUBSET_STRATEGY` | Dieser Parameter gibt die Anzahl der Funktionen an, die bei Aufspaltungen an jedem Strukturknoten berücksichtigt werden sollen. | &quot;auto&quot; | `auto`, `all`, `onethird`, `sqrt`, `log2` oder eine Bruchzahl zwischen 0 und 1,0 |
| `SEED` | Der zufällige Samen. | NICHT GESETZT | Beliebige 64-Bit-Zahl |
| `WEIGHT_COL` | Der Spaltenname, z. B. die Gewichtung. Wenn nicht festgelegt oder leer, werden alle Instanzgewichte als `1.0` behandelt. | NICHT GESETZT | Beliebige Zeichenfolge |
| `LOSS_TYPE` | Dieser Parameter gibt die Verlustfunktion an, die das [!DNL Gradient Boosted Tree]-Modell minimiert. | &quot;squared&quot; | `squared` (L2) und `absolute` (L1). Hinweis: Bei Werten wird nicht zwischen Groß- und Kleinschreibung unterschieden. |
| `STEP_SIZE` | Die Schrittgröße (auch als Lernrate bezeichnet) im Bereich `(0, 1]`, die verwendet wird, um den Beitrag der einzelnen Schätzer zu verkleinern. | 0,1 | `(0, 1]` |
| `MAX_ITER` | Die maximale Anzahl von Iterationen für den Algorithmus. | 20 | (>= 0) |
| `SUBSAMPLING_RATE` | Der Teil der Trainings-Daten, der zum Erlernen der einzelnen Entscheidungsstrukturen verwendet wird, im Bereich `(0, 1]`. | 1,0 | `(0, 1]` |

{style="table-layout:auto"}

**Beispiel**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'gradient_boosted_tree_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Isotonic] Regression {#isotonic-regression}

[!DNL Isotonic Regression] ist ein Algorithmus, der verwendet wird, um Entfernungen iterativ anzupassen und dabei die relative Reihenfolge der Unterschiede in den Daten beizubehalten.

**Parameter**

In der folgenden Tabelle sind die wichtigsten Parameter für die Konfiguration und Optimierung der Leistung von [!DNL Isotonic Regression] aufgeführt.

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------------|
| `ISOTONIC` | Gibt an, ob die Ausgabesequenz isotonisch (erhöht) sein soll, wenn `true` oder antitonisch (absteigend) bei `false`. | `true` | `true`, `false` |
| `WEIGHT_COL` | Der Spaltenname, z. B. die Gewichtung. Wenn nicht festgelegt oder leer, werden alle Instanzgewichte als `1.0` behandelt. | NICHT GESETZT | Beliebige Zeichenfolge |
| `PREDICTION_COL` | Der Spaltenname für die Ausgabe der Prognose. | &quot;prediction&quot; | Beliebige Zeichenfolge |
| `FEATURE_INDEX` | Der Index der Funktion, anwendbar, wenn `featuresCol` eine Vektorspalte ist. Wenn nicht festgelegt, ist der Standardwert `0`. Andernfalls hat dies keine Auswirkungen. | 0 | Beliebige nicht negative Ganzzahl |

{style="table-layout:auto"}

**Beispiel**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'isotonic_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Linear] Regression {#linear-regression}

[!DNL Linear Regression] ist ein beaufsichtigter maschineller Lernalgorithmus, der eine lineare Gleichung an Daten anpasst, um die Beziehung zwischen einer abhängigen Variablen und unabhängigen Funktionen zu modellieren.

**Parameter**

In der folgenden Tabelle sind die wichtigsten Parameter für die Konfiguration und Optimierung der Leistung von [!DNL Linear Regression] aufgeführt.

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------------|
| `MAX_ITER` | Die maximale Anzahl von Iterationen. | 100 | (>= 0) |
| `REGPARAM` | Der Regularisierungsparameter, der zur Steuerung der Komplexität des Modells verwendet wird. | 0,0 | (>= 0) |
| `ELASTICNETPARAM` | Der ElasticNet-Mischparameter, der das Gleichgewicht zwischen L1 (Lasso) und L2 (Ridge)-Strafen steuert. Bei einem Wert von 0 wird eine L2-Strafe angewendet, während bei einem Wert von 1 eine L1-Strafe angewendet wird. | 0,0 | (>= 0, &lt;= 1) |

{style="table-layout:auto"}

**Beispiel**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'linear_reg'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Random Forest Regression] {#random-forest-regression}

[!DNL Random Forest Regression] ist ein Ensemble-Algorithmus, der während des Trainings mehrere Entscheidungsbäume baut und die durchschnittliche Vorhersage dieser Bäume für Regressionsaufgaben zurückgibt, was dazu beiträgt, eine Überanpassung zu verhindern.

**Parameter**

In der folgenden Tabelle sind die wichtigsten Parameter für die Konfiguration und Optimierung der Leistung von [!DNL Random Forest Regression] aufgeführt.

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Die maximale Anzahl von Klassen, die verwendet werden, um kontinuierliche Funktionen zu diskretisieren und zu bestimmen, wie Funktionen auf jedem Knoten aufgeteilt werden. Mehr Klassen bieten eine höhere Granularität. | 32 | Muss mindestens 2 und mindestens der Anzahl der Kategorien in einer kategorischen Funktion entsprechen. |
| `CACHE_NODE_IDS` | Wenn `false`, übergibt der Algorithmus Bäume an Executors, um Instanzen mit Knoten abzugleichen. Wenn der Wert `true` beträgt, speichert der Algorithmus Knoten-IDs für jede Instanz zwischen, was die Schulung tiefer liegender Bäume beschleunigt. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Gibt an, wie oft die zwischengespeicherten Knoten-IDs überprüft werden. Beispiel: `10` bedeutet, dass der Cache alle 10 Iterationen überprüft wird. | 10 | (>= 1) |
| `IMPURITY` | Das für die Berechnung des Informationsgewinns verwendete Kriterium (Groß-/Kleinschreibung nicht beachten). | &quot;entropy&quot; | `entropy`, `gini` |
| `MAX_DEPTH` | Die maximale Tiefe der Baumstruktur (nicht negativ). Beispielsweise bedeutet &quot;depth `0`&quot;einen Blattknoten und &quot;depth `1`&quot;einen internen Knoten und 2 Blattknoten. | 5 | Beliebige nicht negative Ganzzahl |
| `MIN_INFO_GAIN` | Der Mindestinformationsgewinn, der erforderlich ist, damit eine Aufspaltung in einem Strukturknoten berücksichtigt werden kann. | 0,0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | Der Mindestanteil der gewichteten Stichprobenanzahl, die jedes Kind nach einer Aufspaltung aufweisen muss. Wenn eine Aufspaltung dazu führt, dass der Anteil der Gesamtgewichtung in einem der untergeordneten Elemente unter diesem Wert liegt, wird er verworfen. | 0,0 | (>= 0.0, &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | Die Mindestanzahl von Instanzen, die jedes untergeordnete Element nach einer Aufspaltung aufweisen muss. Wenn eine Aufspaltung zu weniger Instanzen als diesem Wert führt, wird die Aufspaltung verworfen. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Der maximale Speicher in MB, der der Histogrammaggregation zugeordnet ist. Wenn dieser Wert zu klein ist, wird nur 1 Knoten pro Iteration aufgeteilt und die Aggregate können diese Größe überschreiten. | 256 | (>= 1) |
| `BOOTSTRAP` | Ob beim Erstellen von Bäumen Bootstrap-Proben verwendet werden. | TRUE | `true`, `false` |
| `NUM_TREES` | Die Anzahl der zu trainierenden Bäume (mindestens 1). Wenn `1`, wird kein Bootstrapping verwendet. Wenn größer als `1` ist, wird das Bootstrapping angewendet. | 20 | (>= 1) |
| `SUBSAMPLING_RATE` | Der Bruchteil der Trainings-Daten, die zum Trainieren der einzelnen Entscheidungsstrukturen verwendet werden, im Bereich `(0, 1]`. | 1,0 | (>= 0,0, &lt;= 1) |
| `LEAF_COL` | Der Spaltenname für Blattindizes, d. h. der prognostizierte Blattindex jeder Instanz in jedem Baum, der durch Preorder Traversal generiert wird. | &quot;&quot; | Beliebige Zeichenfolge |
| `PREDICTION_COL` | Der Spaltenname für die Ausgabe der Prognose. | &quot;prediction&quot; | Beliebige Zeichenfolge |
| `SEED` | Der zufällige Samen. | NICHT GESETZT | Beliebige 64-Bit-Zahl |
| `WEIGHT_COL` | Der Spaltenname, z. B. die Gewichtung. Wenn nicht festgelegt oder leer, werden alle Instanzgewichte als `1.0` behandelt. | NICHT GESETZT | Jeder gültige Spaltenname oder leer lassen. |

{style="table-layout:auto"}

**Beispiel**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'random_forest_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Survival Regression] {#survival-regression}

[!DNL Survival Regression] wird verwendet, um ein parametrisches Überlebensregressionsmodell, das als [!DNL Accelerated Failure Time] (AFT)-Modell bezeichnet wird, basierend auf dem [!DNL Weibull distribution] anzupassen. Instanzen können zur Leistungsverbesserung in Blöcken gestapelt werden.

**Parameter**

In der folgenden Tabelle sind die wichtigsten Parameter für die Konfiguration und Optimierung der Leistung von [!DNL Survival Regression] aufgeführt.

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------------|
| `MAX_ITER` | Die maximale Anzahl von Iterationen, die der Algorithmus ausführen soll. | 100 | (>= 0) |
| `TOL` | Die Konvergenztoleranz. | `1E-6` | (>= 0) |
| `AGGREGATION_DEPTH` | Die empfohlene Tiefe für `treeAggregate`. Wenn die Funktionsdimensionen oder die Anzahl der Partitionen groß sind, kann dieser Parameter auf einen größeren Wert eingestellt werden. | 2 | (>= 2) |
| `FIT_INTERCEPT` | Ob ein Begriffsbegriff passt. | TRUE | `true`, `false` |
| `PREDICTION_COL` | Der Spaltenname für die Ausgabe der Prognose. | &quot;prediction&quot; | Beliebige Zeichenfolge |
| `CENSOR_COL` | Der Spaltenname für die Zensur. Der Wert `1` zeigt an, dass das Ereignis aufgetreten ist (nicht gespeichert), während `0` bedeutet, dass das Ereignis zensiert wird. | &quot;zensieren&quot; | 0, 1 |
| `MAX_BLOCK_SIZE_IN_MB` | Der maximale Speicher in MB für die Stapelung von Eingabedaten in Blöcken. Wenn die verbleibende Datengröße in einer Partition kleiner ist, wird dieser Wert entsprechend angepasst. Der Wert `0` ermöglicht eine automatische Anpassung. | 0,0 | (>= 0) |

{style="table-layout:auto"}

**Beispiel**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'survival_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie verschiedene Regressionsalgorithmen konfigurieren und verwenden können. Weitere Informationen zu anderen Typen erweiterter statistischer Modelle finden Sie in den Dokumenten zu [Klassifizierung](./classification.md) und [Clustering](./clustering.md) .
