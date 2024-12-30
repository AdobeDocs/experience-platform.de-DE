---
title: Regressionsalgorithmen
description: Erfahren Sie, wie Sie verschiedene Regressionsalgorithmen mit Schlüsselparametern, Beschreibungen und Beispiel-Code konfigurieren und optimieren können, um erweiterte statistische Modelle zu implementieren.
role: Developer
exl-id: d38733bb-0420-40bf-a70b-19e0e0e58730
source-git-commit: 8b9cfb48a11701f0e4b358416c6b627bedf1db8b
workflow-type: tm+mt
source-wordcount: '2384'
ht-degree: 4%

---

# Regressionsalgorithmen {#regression-algorithms}

Dieses Dokument bietet einen Überblick über verschiedene Regressionsalgorithmen, wobei der Schwerpunkt auf ihrer Konfiguration, den wichtigsten Parametern und der praktischen Verwendung in erweiterten statistischen Modellen liegt. Regressionsalgorithmen werden verwendet, um die Beziehung zwischen abhängigen und unabhängigen Variablen zu modellieren und kontinuierliche Ergebnisse auf der Grundlage der beobachteten Daten vorherzusagen. Jeder Abschnitt enthält Parameterbeschreibungen und Beispiel-Code, der Ihnen bei der Implementierung und Optimierung dieser Algorithmen für Aufgaben wie lineare, zufällige Gesamtstruktur- und Überlebensregression hilft.

## [!DNL Decision Tree] Regression {#decision-tree-regression}

[!DNL Decision Tree] Lernen ist eine überwachte Lernmethode, die in der Statistik, im Data Mining und im maschinellen Lernen verwendet wird. Bei diesem Ansatz wird ein Klassifizierungs- oder Regressionsentscheidungsbaum als prädiktives Modell verwendet, um Rückschlüsse auf eine Reihe von Beobachtungen zu ziehen.

**Parameter**

In der folgenden Tabelle sind die wichtigsten Parameter zur Konfiguration und Optimierung der Leistung von Entscheidungsbaum-Modellen aufgeführt.

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|--------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Dieser Parameter gibt die maximale Anzahl von Klassen an, die verwendet werden, um kontinuierliche KEs zu diskretisieren und Aufspaltungen bei jedem Knoten zu bestimmen. Mehr Klassen führen zu einer feineren Granularität und Detailgenauigkeit. | 32 | Muss mindestens 2 und mindestens die Anzahl der Kategorien in einem kategorialen Merkmal sein. |
| `CACHE_NODE_IDS` | Dieser Parameter bestimmt, ob Knoten-IDs für jede Instanz zwischengespeichert werden. Wenn `false`, übergibt der Algorithmus Bäume an ausführende Benutzer, damit Instanzen mit Knoten abgeglichen werden. Wenn `true`, speichert der Algorithmus Knoten-IDs für jede Instanz zwischen, was das Training tiefer stehender Baumstrukturen beschleunigen kann. Benutzer können konfigurieren, wie oft der Cache überprüft werden soll, oder ihn deaktivieren, indem sie `CHECKPOINT_INTERVAL` festlegen. | false | `true` oder `false` |
| `CHECKPOINT_INTERVAL` | Dieser Parameter gibt an, wie oft die Knoten-IDs im Cache überprüft werden sollen. Wenn Sie beispielsweise auf `10` setzen, wird der Cache alle 10 Iterationen überprüft. Dies gilt nur, wenn `CACHE_NODE_IDS` auf `true` gesetzt ist und das Checkpoint-Verzeichnis in `org.apache.spark.SparkContext` konfiguriert ist. | 10 | (>=1) |
| `IMPURITY` | Dieser Parameter gibt das Kriterium für die Berechnung des Informationsgewinns an. Unterstützte Werte sind `entropy` und `gini`. | `gini` | `entropy`, `gini` |
| `MAX_DEPTH` | Dieser Parameter gibt die maximale Tiefe der Baumstruktur an. Beispielsweise bedeutet eine Tiefe von `0` 1 Blattknoten, während eine Tiefe von `1` 1 interner Knoten und 2 Blattknoten bedeutet. Die Tiefe muss innerhalb des Bereichs `[0, 30]` liegen. | 5 | [,0 ] |
| `MIN_INFO_GAIN` | Dieser Parameter legt den minimalen Informationsgewinn fest, der erforderlich ist, damit eine Aufspaltung in einem Strukturknoten als gültig betrachtet wird. | 0,0 | (>=0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | Dieser Parameter gibt den Mindestbruchteil der gewichteten Stichprobenanzahl an, den jeder untergeordnete Knoten nach einer Aufspaltung aufweisen muss. Wenn einer der untergeordneten Knoten einen Bruchteil kleiner als diesen Wert hat, wird die Aufspaltung verworfen. | 0,0 | [0,0, 0,5 ] |
| `MIN_INSTANCES_PER_NODE` | Dieser Parameter legt die Mindestanzahl von Instanzen fest, die jeder untergeordnete Knoten nach einer Aufspaltung aufweisen muss. Wenn eine Aufspaltung zu weniger Instanzen als diesem Wert führt, wird die Aufspaltung als ungültig verworfen. | 1 | (>=1) |
| `MAX_MEMORY_IN_MB` | Dieser Parameter gibt den maximalen Speicher in Megabyte (MB) an, der für die Histogrammaggregation zugewiesen wird. Wenn der Speicher zu klein ist, wird pro Iteration nur ein Knoten aufgeteilt, und seine Aggregate können diese Größe überschreiten. | 256 | Beliebiger positiver ganzzahliger Wert |
| `PREDICTION_COL` | Dieser Parameter gibt den Namen der Spalte an, die zum Speichern von Prognosen verwendet wird. | „Prognose“ | Beliebige Zeichenfolge |
| `SEED` | Dieser Parameter legt die im Modell verwendeten zufälligen Testadressen fest. | Keine | Beliebige 64-Bit-Zahl |
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

[!DNL Factorization Machines] ist ein Regressionslernalgorithmus, der den normalen Gradientenabstieg und den AdamW-Solver unterstützt. Der Algorithmus basiert auf dem Aufsatz von S. Rendle (2010), &quot;[!DNL Factorization Machines].“

**Parameter**

In der folgenden Tabelle sind die wichtigsten Parameter für die Konfiguration und Optimierung der Leistung [!DNL Factorization Machines] Regression aufgeführt.

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|------------------------|-------------------------------------------------------------------------------------------------|---------------|-----------------------|
| `TOL` | Dieser Parameter legt die Konvergenztoleranz für den Algorithmus fest. Höhere Werte können zu einer schnelleren Konvergenz, aber weniger Präzision führen. | `1E-6` | (>= 0) |
| `FACTOR_SIZE` | Dieser Parameter definiert die Dimensionalität der Faktoren. Höhere Werte erhöhen die Modellkomplexität. | 8 | (>= 0) |
| `FIT_INTERCEPT` | Dieser Parameter gibt an, ob das Modell einen Abfangbegriff enthalten soll. | `true` | `true`, `false` |
| `FIT_LINEAR` | Dieser Parameter gibt an, ob ein linearer Begriff (auch als 1-Wege-Begriff bezeichnet) in das Modell aufgenommen werden soll. | `true` | `true`, `false` |
| `INIT_STD` | Dieser Parameter definiert die Standardabweichung der anfänglichen Koeffizienten, die im Modell verwendet werden. | 0,01 | (>= 0) |
| `MAX_ITER` | Dieser Parameter gibt die maximale Anzahl von Iterationen für den auszuführenden Algorithmus an. | 100 | (>= 0) |
| `MINI_BATCH_FRACTION` | Dieser Parameter legt den Teil des Mini-Batches fest, der den Teil der Daten bestimmt, der in jedem Batch verwendet wird. Sie muss im Bereich `(0, 1]` liegen. | 1,0 | `(0, 1]` |
| `REG_PARAM` | Dieser Parameter legt den Regularisierungsparameter fest, um eine Überanpassung zu verhindern. | 0,0 | (>= 0) |
| `SEED` | Dieser Parameter gibt den zufälligen Seed an, der für die Modellinitialisierung verwendet wird. | Keine | Beliebige 64-Bit-Zahl |
| `SOLVER` | Dieser Parameter gibt den Solver-Algorithmus für die Optimierung an. | „adamW“ | `gd` (Gefälle), `adamW` |
| `STEP_SIZE` | Dieser Parameter gibt die anfängliche Schrittgröße (oder Lernrate) für den ersten Optimierungsschritt an. | 1,0 | Beliebiger positiver Wert |
| `PREDICTION_COL` | Dieser Parameter gibt den Namen der Spalte an, in der Prognosen gespeichert werden. | „Prognose“ | Beliebige Zeichenfolge |

{style="table-layout:auto"}

**Beispiel**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'factorization_machines_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Generalized Linear] Regression {#generalized-linear-regression}

Im Gegensatz zur linearen Regression, bei der davon ausgegangen wird, dass das Ergebnis einer normalen (Gauß&#39;schen) Verteilung folgt, können [!DNL Generalized Linear] (GLMs) das Ergebnis je nach Art der Daten verschiedenen Verteilungstypen wie [!DNL Poisson] oder Binomialverteilung folgen lassen.

**Parameter**

In der folgenden Tabelle sind die wichtigsten Parameter für die Konfiguration und Optimierung der Leistung [!DNL Generalized Linear] Regression aufgeführt.

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-------------------------------------------------------------------------|
| `MAX_ITER` | Legt die maximale Anzahl von Iterationen fest (anwendbar bei Verwendung des `irls`). | 25 | (>= 0) |
| `REG_PARAM` | Der Regularisierungsparameter. | NICHT FESTGELEGT | (>= 0) |
| `TOL` | Die Konvergenztoleranz. | `1E-6` | (>= 0) |
| `AGGREGATION_DEPTH` | Die empfohlene Tiefe für `treeAggregate`. | 2 | (>= 2) |
| `FAMILY` | Der Parameter family, der die im Modell verwendete Fehlerverteilung beschreibt. Unterstützte Optionen sind `gaussian`, `binomial`, `poisson`, `gamma` und `tweedie`. | „Gaußsch“ | `gaussian`, `binomial`, `poisson`, `gamma`, `tweedie` |
| `FIT_INTERCEPT` | Gibt an, ob ein Abfangbegriff eingefügt werden soll. | `true` | `true`, `false` |
| `LINK` | Die Verknüpfungsfunktion, die die Beziehung zwischen dem linearen Prädiktor und dem Mittelwert der Verteilungsfunktion definiert. Unterstützte Optionen sind `identity`, `log`, `inverse`, `logit`, `probit`, `cloglog` und `sqrt`. | NICHT FESTGELEGT | `identity`, `log`, `inverse`, `logit`, `probit`, `cloglog`, `sqrt` |
| `LINK_POWER` | Dieser Parameter gibt den Index der Powerlink-Funktion an. Der Parameter gilt nur für die [!DNL Tweedie]. Ist dies nicht festgelegt, wird standardmäßig `1 - variancePower` verwendet, das dem R-`statmod`-Paket entspricht. Spezifische Link-Potenzen von 0, 1, -1 und 0,5 entsprechen den Log-, Identity-, Inverse- und SQRT-Links. | 1 | Beliebiger numerischer Wert |
| `SOLVER` | Der für die Optimierung verwendete Solver-Algorithmus. Unterstützte Option: `irls` (iterativ neu gewichtete Kleinste Quadrate). | „Mädchen“ | `irls` |
| `VARIANCE_POWER` | Dieser Parameter gibt die Potenz der Varianzfunktion der [!DNL Tweedie] an und definiert die Beziehung zwischen Varianz und Mittelwert. Unterstützte Werte sind 0 und `[1, inf)`. Varianzwerte von 0, 1 und 2 entsprechen den Gauß-, Poisson- bzw. Gamma-Familien. | 0,0 | 0 `[1, inf)` |
| `LINK_PREDICTION_COL` | Der Spaltenname der Linkprädiktion (linearer Prädiktor). | NICHT FESTGELEGT | Beliebige Zeichenfolge |
| `OFFSET_COL` | Der Name der Versatzspalte. Ist kein Wert festgelegt, werden alle Instanzversätze als 0,0 behandelt. Die Offset-Funktion hat einen konstanten Koeffizienten von 1,0. | NICHT FESTGELEGT | Beliebige Zeichenfolge |
| `WEIGHT_COL` | Der Name der Gewichtungsspalte. Wenn sie nicht festgelegt oder leer ist, werden alle Instanzgewichte als `1.0` behandelt. In der Binomialfamilie entsprechen Gewichtungen der Anzahl der Versuche, und Nicht-Ganzzahlgewichte werden in der AIC-Berechnung gerundet. | NICHT FESTGELEGT | Beliebige Zeichenfolge |

{style="table-layout:auto"}

**Beispiel**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'generalized_linear_reg'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Gradient Boosted Tree] Regression {#gradient-boosted-tree-regression}

Gradient-Boosted Trees (GBTs) sind eine effektive Methode zur Klassifizierung und Regression, die die Vorhersagen mehrerer Entscheidungsbäume kombiniert, um die Vorhersagegenauigkeit und die Modellleistung zu verbessern.

**Parameter**

In der folgenden Tabelle sind die wichtigsten Parameter für die Konfiguration und Optimierung der Leistung [!DNL Gradient Boosted Tree] Regression aufgeführt.

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|-------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Die maximale Anzahl von Klassen, die verwendet werden, um kontinuierliche Funktionen in diskrete Intervalle zu unterteilen, was dabei hilft, zu bestimmen, wie die Funktionen in jedem Entscheidungsbaum-Knoten aufgeteilt werden. Mehr Klassen bieten eine höhere Granularität. | 32 | Muss mindestens 2 sein und gleich oder größer als die Anzahl der Kategorien in einem kategorialen Merkmal sein. |
| `CACHE_NODE_IDS` | Wenn `false`, übergibt der Algorithmus Bäume an ausführende Benutzer, damit Instanzen mit Knoten abgeglichen werden. Wenn `true`, speichert der Algorithmus Knoten-IDs für jede Instanz zwischen. Caching kann das Training von tieferen Bäumen beschleunigen. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Gibt an, wie oft die zwischengespeicherten Knoten-IDs überprüft werden sollen. `10` bedeutet beispielsweise, dass der Cache alle 10 Iterationen überprüft wird. | 10 | (>= 1) |
| `MAX_DEPTH` | Die maximale Tiefe des Baums (nicht negativ). Zum Beispiel bedeutet `0` Tiefe 1 Blattknoten und Tiefe `1` bedeutet 1 interner Knoten mit 2 Blattknoten. | 5 | (>= 0) |
| `MIN_INFO_GAIN` | Der minimale Informationsgewinn, der erforderlich ist, damit eine Aufspaltung an einem Strukturknoten berücksichtigt wird. | 0,0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | Der MindestBRUCHTEIL der gewichteten Stichprobenanzahl, den jedes Kind nach einer Aufspaltung aufweisen muss. Wenn der Bruchteil des Gesamtgewichts bei einem der untergeordneten Elemente diesen Wert unterschreitet, wird er verworfen. | 0,0 | (>= 0.0, &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | Die Mindestanzahl von Instanzen, die jedes untergeordnete Element nach einer Aufspaltung aufweisen muss. Wenn eine Aufspaltung zu weniger Instanzen als diesen Wert führt, wird die Aufspaltung verworfen. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Der maximale Speicher in MB, der der Histogrammaggregation zugeordnet ist. Wenn dieser Wert zu klein ist, wird pro Iteration nur ein Knoten aufgeteilt, und seine Aggregate können diese Größe überschreiten. | 256 | Beliebiger positiver ganzzahliger Wert |
| `PREDICTION_COL` | Der Spaltenname für die Prognoseausgabe. | „Prognose“ | Beliebige Zeichenfolge |
| `VALIDATION_INDICATOR_COL` | Der Spaltenname, der angibt, ob jede Zeile für das Training oder die Validierung verwendet wird. `false` für Schulung und `true` zur Validierung. | NICHT FESTGELEGT | Beliebige Zeichenfolge |
| `LEAF_COL` | Der Spaltenname für Blattindizes. Der prognostizierte Blattindex jeder Instanz in jedem Baum, der durch Durchlaufen der Vorbestellung generiert wird. | &quot;&quot; | Beliebige Zeichenfolge |
| `FEATURE_SUBSET_STRATEGY` | Dieser Parameter gibt die Anzahl der Funktionen an, die bei Aufspaltungen in jedem Strukturknoten berücksichtigt werden sollen. | „auto“ | `auto`, `all`, `onethird`, `sqrt`, `log2` oder ein Bruchteil zwischen 0 und 1,0 |
| `SEED` | Der zufällige Startwert. | NICHT FESTGELEGT | Beliebige 64-Bit-Zahl |
| `WEIGHT_COL` | Der Spaltenname, z. B., Gewichtungen. Wenn sie nicht festgelegt oder leer ist, werden alle Instanzgewichte als `1.0` behandelt. | NICHT FESTGELEGT | Beliebige Zeichenfolge |
| `LOSS_TYPE` | Dieser Parameter gibt die Verlustfunktion an, die das [!DNL Gradient Boosted Tree] minimiert. | „quadriert“ | `squared` (L2) und `absolute` (L1). Hinweis: Bei Werten wird nicht zwischen Groß- und Kleinschreibung unterschieden. |
| `STEP_SIZE` | Die Schrittgröße (auch als Lernrate bezeichnet) im Bereich `(0, 1]`, die zum Verkleinern des Beitrags jeder Schätzung verwendet wird. | 0,1 | `(0, 1]` |
| `MAX_ITER` | Die maximale Anzahl von Iterationen für den Algorithmus. | 20 | (>= 0) |
| `SUBSAMPLING_RATE` | Der Teil der Trainingsdaten, der zum Erlernen der einzelnen Entscheidungsbäume verwendet wird, im Bereich `(0, 1]`. | 1,0 | `(0, 1]` |

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

In der folgenden Tabelle sind die wichtigsten Parameter zur Konfiguration und Optimierung der Leistung von [!DNL Isotonic Regression] aufgeführt.

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------------|
| `ISOTONIC` | Gibt an, ob die Ausgabesequenz beim `true` isotonisch (ansteigend) oder beim `false` antitonisch (absteigend) sein soll. | `true` | `true`, `false` |
| `WEIGHT_COL` | Der Spaltenname, z. B., Gewichtungen. Wenn sie nicht festgelegt oder leer ist, werden alle Instanzgewichte als `1.0` behandelt. | NICHT FESTGELEGT | Beliebige Zeichenfolge |
| `PREDICTION_COL` | Der Spaltenname für die Prognoseausgabe. | „Prognose“ | Beliebige Zeichenfolge |
| `FEATURE_INDEX` | Der Index der Funktion, der angewendet wird, wenn `featuresCol` eine Vektorspalte ist. Wenn nicht festgelegt, lautet der Standardwert `0`. Andernfalls hat es keine Wirkung. | 0 | Beliebige nicht negative Ganzzahl |

{style="table-layout:auto"}

**Beispiel**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'isotonic_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Linear] Regression {#linear-regression}

[!DNL Linear Regression] ist ein überwachter Algorithmus für maschinelles Lernen, der eine lineare Gleichung an Daten anpasst, um die Beziehung zwischen einer abhängigen Variablen und unabhängigen Funktionen zu modellieren.

**Parameter**

In der folgenden Tabelle sind die wichtigsten Parameter zur Konfiguration und Optimierung der Leistung von [!DNL Linear Regression] aufgeführt.

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------------|
| `MAX_ITER` | Die maximale Anzahl von Iterationen. | 100 | (>= 0) |
| `REGPARAM` | Der Regularisierungsparameter, mit dem die Komplexität des Modells gesteuert wird. | 0,0 | (>= 0) |
| `ELASTICNETPARAM` | Der ElasticNet-Mischparameter, der das Gleichgewicht zwischen L1 (Lasso)- und L2 (Ridge)-Strafen steuert. Bei einem Wert von 0 wird eine L2-Strafe angewendet, während bei einem Wert von 1 eine L1-Strafe angewendet wird. | 0,0 | (>= 0, &lt;= 1) |

{style="table-layout:auto"}

**Beispiel**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'linear_reg'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Random Forest Regression] {#random-forest-regression}

[!DNL Random Forest Regression] ist ein Ensemble-Algorithmus, der während des Trainings mehrere Entscheidungsbäume erstellt und die durchschnittliche Prognose dieser Bäume für Regressionsaufgaben zurückgibt, um eine Überanpassung zu vermeiden.

**Parameter**

In der folgenden Tabelle sind die wichtigsten Parameter zur Konfiguration und Optimierung der Leistung von [!DNL Random Forest Regression] aufgeführt.

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Die maximale Anzahl von Klassen, die verwendet werden, um fortlaufende KEs zu diskretisieren und zu bestimmen, wie die KEs an jedem Knoten aufgeteilt werden. Mehr Klassen bieten eine höhere Granularität. | 32 | Muss mindestens 2 und mindestens gleich der Anzahl der Kategorien in einem kategorialen Merkmal sein. |
| `CACHE_NODE_IDS` | Wenn `false`, übergibt der Algorithmus Bäume an ausführende Benutzer, damit Instanzen mit Knoten abgeglichen werden. Wenn `true`, speichert der Algorithmus Knoten-IDs für jede Instanz zwischen, wodurch das Training tiefer stehender Baumstrukturen beschleunigt wird. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Gibt an, wie oft die zwischengespeicherten Knoten-IDs überprüft werden sollen. `10` bedeutet beispielsweise, dass der Cache alle 10 Iterationen überprüft wird. | 10 | (>= 1) |
| `IMPURITY` | Das Kriterium für die Berechnung des Informationsgewinns (ohne Unterscheidung zwischen Groß- und Kleinschreibung). | „Entropie“ | `entropy`, `gini` |
| `MAX_DEPTH` | Die maximale Tiefe des Baums (nicht negativ). Beispielsweise bedeutet `0` Tiefe 1 Blattknoten und Tiefe `1` bedeutet 1 interner Knoten und 2 Blattknoten. | 5 | Beliebige nicht negative Ganzzahl |
| `MIN_INFO_GAIN` | Der minimale Informationsgewinn, der erforderlich ist, damit eine Aufspaltung an einem Strukturknoten berücksichtigt wird. | 0,0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | Der MindestBRUCHTEIL der gewichteten Stichprobenanzahl, den jedes Kind nach einer Aufspaltung aufweisen muss. Wenn der Bruchteil des Gesamtgewichts bei einem der untergeordneten Elemente diesen Wert unterschreitet, wird er verworfen. | 0,0 | (>= 0.0, &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | Die Mindestanzahl von Instanzen, die jedes untergeordnete Element nach einer Aufspaltung aufweisen muss. Wenn eine Aufspaltung zu weniger Instanzen als diesen Wert führt, wird die Aufspaltung verworfen. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Der maximale Speicher in MB, der der Histogrammaggregation zugeordnet ist. Wenn dieser Wert zu klein ist, wird pro Iteration nur ein Knoten aufgeteilt, und seine Aggregate können diese Größe überschreiten. | 256 | (>= 1) |
| `BOOTSTRAP` | Ob beim Erstellen von Bäumen Bootstrap-Beispiele verwendet werden sollen. | WAHR | `true`, `false` |
| `NUM_TREES` | Die Anzahl der zu trainierenden Bäume (mindestens 1). Wenn `1`, wird kein Bootstrapping durchgeführt. Wenn größer als `1`, wird Bootstrapping angewendet. | 20 | (>= 1) |
| `SUBSAMPLING_RATE` | Der Teil der Trainingsdaten, der zum Trainieren der einzelnen Entscheidungsbäume verwendet wird, im Bereich `(0, 1]`. | 1,0 | (>= 0.0, &lt;= 1) |
| `LEAF_COL` | Der Spaltenname für Blattindizes, der der prognostizierte Blattindex jeder Instanz in jedem Baum ist, der durch Durchlaufen der Vorbestellung generiert wird. | &quot;&quot; | Beliebige Zeichenfolge |
| `PREDICTION_COL` | Der Spaltenname für die Prognoseausgabe. | „Prognose“ | Beliebige Zeichenfolge |
| `SEED` | Der zufällige Startwert. | NICHT FESTGELEGT | Beliebige 64-Bit-Zahl |
| `WEIGHT_COL` | Der Spaltenname, z. B., Gewichtungen. Wenn sie nicht festgelegt oder leer ist, werden alle Instanzgewichte als `1.0` behandelt. | NICHT FESTGELEGT | Ein gültiger Spaltenname oder leer lassen. |

{style="table-layout:auto"}

**Beispiel**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'random_forest_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Survival Regression] {#survival-regression}

[!DNL Survival Regression] wird verwendet, um ein parametrisches Überlebens-Regressionsmodell einzupassen, das als [!DNL Accelerated Failure Time] (AFT)-Modell bezeichnet wird und auf der [!DNL Weibull distribution] basiert. Zur Leistungssteigerung können Instanzen in Blöcken gestapelt werden.

**Parameter**

In der folgenden Tabelle sind die wichtigsten Parameter zur Konfiguration und Optimierung der Leistung von [!DNL Survival Regression] aufgeführt.

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------------|
| `MAX_ITER` | Die maximale Anzahl von Iterationen, die der Algorithmus ausführen soll. | 100 | (>= 0) |
| `TOL` | Die Konvergenztoleranz. | `1E-6` | (>= 0) |
| `AGGREGATION_DEPTH` | Die empfohlene Tiefe für `treeAggregate`. Wenn die Elementabmessungen oder die Anzahl der Partitionen groß sind, kann dieser Parameter auf einen größeren Wert gesetzt werden. | 2 | (>= 2) |
| `FIT_INTERCEPT` | Gibt an, ob ein Abfangbegriff eingefügt werden soll. | WAHR | `true`, `false` |
| `PREDICTION_COL` | Der Spaltenname für die Prognoseausgabe. | „Prognose“ | Beliebige Zeichenfolge |
| `CENSOR_COL` | Der Spaltenname für die Zensur. Der Wert `1` bedeutet, dass das Ereignis aufgetreten ist (unzensiert), während `0` bedeutet, dass das Ereignis zensiert wurde. | „Zensor“ | 0, 1 |
| `MAX_BLOCK_SIZE_IN_MB` | Der maximale Speicher in MB für das Stapeln von Eingabedaten in Blöcken. Wenn die verbleibende Datengröße in einer Partition kleiner ist, wird dieser Wert entsprechend angepasst. Der Wert `0` ermöglicht eine automatische Anpassung. | 0,0 | (>= 0) |

{style="table-layout:auto"}

**Beispiel**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'survival_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie verschiedene Regressionsalgorithmen konfigurieren und verwenden können. Weitere Informationen zu anderen Typen erweiterter statistischer Modelle finden [ in den Dokumenten ](./classification.md)Klassifizierung und [Clustering](./clustering.md).
