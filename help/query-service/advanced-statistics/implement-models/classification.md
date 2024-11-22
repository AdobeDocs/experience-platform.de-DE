---
title: Klassifizierungsalgorithmen
description: Erfahren Sie, wie Sie verschiedene Klassifizierungsalgorithmen mit Schlüsselparametern, Beschreibungen und Beispielcode konfigurieren und optimieren können, um Ihnen bei der Implementierung erweiterter statistischer Modelle zu helfen.
role: Developer
exl-id: 9105ab04-b480-48a0-b8f7-cf0ed5e5399d
source-git-commit: 489063fcd003e20f233a9c9d85d8cb6c22708d88
workflow-type: tm+mt
source-wordcount: '2449'
ht-degree: 4%

---

# Klassifizierungsalgorithmen {#classification-algorithms}

Dieses Dokument bietet einen Überblick über verschiedene Klassifizierungsalgorithmen, die sich auf ihre Konfiguration, Schlüsselparameter und praktische Verwendung in erweiterten statistischen Modellen konzentrieren. Klassifizierungsalgorithmen werden verwendet, um Datenpunkten basierend auf Eingabefunktionen Kategorien zuzuweisen. Jeder Abschnitt enthält Parameterbeschreibungen und Beispielcode, mit denen Sie diese Algorithmen für Aufgaben wie Entscheidungsbäume, Random Forest und die naive Bayes-Klassifizierung implementieren und optimieren können.

## [!DNL Decision Tree Classifier] {#decision-tree-classifier}

[!DNL Decision Tree Classifier] ist ein beaufsichtigter Lernansatz, der in Statistiken, Data Mining und maschinellem Lernen verwendet wird. Bei diesem Ansatz wird ein Entscheidungsbaum als prädiktives Modell für Klassifizierungsaufgaben verwendet, das Schlussfolgerungen aus einer Reihe von Beobachtungen zieht.

**Parameter**

In der folgenden Tabelle sind die wichtigsten Parameter für die Konfiguration und Optimierung der Leistung eines [!DNL Decision Tree Classifier] aufgeführt.

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------|
| `MAX_BINS` | Die maximale Anzahl von Klassen bestimmt, wie kontinuierliche Merkmale in diskrete Intervalle aufgeteilt werden. Dies wirkt sich darauf aus, wie Funktionen auf jedem Entscheidungsbaum-Knoten aufgeteilt werden. Mehr Klassen bieten eine höhere Granularität. | 32 | Muss mindestens 2 und mindestens der Anzahl der Kategorien in einer kategorischen Funktion entsprechen. |
| `CACHE_NODE_IDS` | Wenn `false`, übergibt der Algorithmus Bäume an Executors, um Instanzen mit Knoten abzugleichen. Wenn der Wert `true` beträgt, speichert der Algorithmus Knoten-IDs für jede Instanz zwischen, was die Schulung tiefer liegender Bäume beschleunigt. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Gibt an, wie oft die zwischengespeicherten Knoten-IDs überprüft werden. Beispiel: `10` bedeutet, dass der Cache alle 10 Iterationen überprüft wird. | 10 | (>= 1) |
| `IMPURITY` | Das für die Berechnung des Informationsgewinns verwendete Kriterium (Groß-/Kleinschreibung nicht beachten). | &quot;gini&quot; | `entropy`, `gini` |
| `MAX_DEPTH` | Die maximale Tiefe der Baumstruktur (nicht negativ). Beispielsweise bedeutet &quot;depth `0`&quot;einen Blattknoten und &quot;depth `1`&quot;einen internen Knoten und 2 Blattknoten. | 5 | (>= 0) (Bereich: [0,30]) |
| `MIN_INFO_GAIN` | Der Mindestinformationsgewinn, der erforderlich ist, damit eine Aufspaltung in einem Strukturknoten berücksichtigt werden kann. | 0,0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | Der Mindestanteil der gewichteten Stichprobenanzahl, die jedes Kind nach einer Aufspaltung aufweisen muss. Wenn eine Aufspaltung dazu führt, dass der Anteil der Gesamtgewichtung in einem der untergeordneten Elemente unter diesem Wert liegt, wird er verworfen. | 0,0 | (>= 0.0, &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | Die Mindestanzahl von Instanzen, die jedes untergeordnete Element nach einer Aufspaltung aufweisen muss. Wenn eine Aufspaltung zu weniger Instanzen als diesem Wert führt, wird die Aufspaltung verworfen. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Der maximale Speicher in MB, der der Histogrammaggregation zugeordnet ist. Wenn dieser Wert zu klein ist, wird nur 1 Knoten pro Iteration aufgeteilt und die Aggregate können diese Größe überschreiten. | 256 | (>= 0) |
| `PREDICTION_COL` | Der Spaltenname für die Ausgabe der Prognose. | &quot;prediction&quot; | Beliebige Zeichenfolge |
| `SEED` | Der zufällige Samen. | K. A. | Beliebige 64-Bit-Zahl |
| `WEIGHT_COL` | Der Spaltenname, z. B. die Gewichtung. Wenn nicht festgelegt oder leer, werden alle Instanzgewichte als `1.0` behandelt. | NICHT GESETZT | Beliebige Zeichenfolge |
| `ONE_VS_REST` | Aktiviert oder deaktiviert das Umbrechen dieses Algorithmus mit &quot;Eins vs. Rest&quot;, das für Classification-Probleme mit mehreren Klassen verwendet wird. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Beispiel**

```sql
Create MODEL modelname OPTIONS(
  type = 'decision_tree_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Factorization Machine Classifier] {#factorization-machine-classifier}

Der [!DNL Factorization Machine Classifier] ist ein Classification-Algorithmus, der die normale Abstufung von Farbverläufen und den AdamW-Resolver unterstützt. Das Klassifizierungsmodell Factorization Machine verwendet Logistikverluste, die über einen Gradientenabfall optimiert werden können, und enthält häufig Regularisierungsbegriffe wie L2, um eine Überanpassung zu verhindern.

**Parameter**

Die nachstehende Tabelle enthält wichtige Parameter für die Konfiguration und Optimierung der Leistung des [!DNL Factorization Machine Classifier].

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-------------------------------------------------------------------------------------------------------|
| `TOL` | Die Konvergenztoleranz, die die Genauigkeit der Optimierung kontrolliert. | `1E-6` | (>= 0) |
| `FACTOR_SIZE` | Die Dimensionalität der Faktoren. | 8 | (>= 0) |
| `FIT_INTERCEPT` | Gibt an, ob ein Konstantenbegriff angepasst werden soll. | `true` | `true`, `false` |
| `FIT_LINEAR` | Gibt an, ob der lineare Begriff angepasst werden soll (auch als 1-Weg-Begriff bezeichnet). | `true` | `true`, `false` |
| `INIT_STD` | Die Standardabweichung für die Initialisierung von Koeffizienten. | 0,01 | (>= 0) |
| `MAX_ITER` | Die maximale Anzahl der Iterationen, die der Algorithmus ausführen soll. | 100 | (>= 0) |
| `MINI_BATCH_FRACTION` | Der Teil der Daten, die während des Trainings in Mini-Batches verwendet werden sollen. Muss im Bereich `(0, 1]` liegen. | 1,0 | 0 &lt; Wert &lt;= 1 |
| `REG_PARAM` | Der Regularisierungsparameter hilft bei der Steuerung der Modellkomplexität und der Vermeidung einer Überanpassung. | 0,0 | (>= 0) |
| `SEED` | Die Zufallsstichprobe zur Steuerung zufälliger Prozesse im Algorithmus. | K. A. | Beliebige 64-Bit-Zahl |
| `SOLVER` | Der für die Optimierung verwendete Lösungs-Algorithmus. Unterstützte Optionen sind `gd` (Abstufung des Verlaufs) und `adamW`. | &quot;adamW&quot; | `gd`, `adamW` |
| `STEP_SIZE` | Die anfängliche Schrittgröße zur Optimierung, häufig als Lernrate interpretiert. | 1,0 | > 0 |
| `PROBABILITY_COL` | Der Spaltenname für prognostizierte bedingte Klassenwahrscheinlichkeiten. Hinweis: Nicht alle Modelle liefern gut kalibrierte Wahrscheinlichkeiten; diese sollten als Konfidenzwerte und nicht als exakte Wahrscheinlichkeiten behandelt werden. | &quot;wahrscheinlichkeit&quot; | Beliebige Zeichenfolge |
| `PREDICTION_COL` | Der Spaltenname für vorab prognostizierte Klassenbeschriftungen. | &quot;prediction&quot; | Beliebige Zeichenfolge |
| `RAW_PREDICTION_COL` | Der Spaltenname für Rohdatenprognosewerte (auch als Konfidenz bezeichnet). | &quot;rawPreforecast&quot; | Beliebige Zeichenfolge |
| `ONE_VS_REST` | Gibt an, ob Eins-vs-Rest für mehrklassige Classification aktiviert werden soll. | FALSE | `true`, `false` |

{style="table-layout:auto"}

**Beispiel**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'factorization_machines_classifier'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Gradient Boosted Tree Classifier] {#gradient-boosted-tree-classifier}

Der [!DNL Gradient Boosted Tree Classifier] verwendet ein Ensemble von Entscheidungsbäumen, um die Genauigkeit von Klassifizierungsaufgaben zu verbessern, indem mehrere Bäume kombiniert werden, um die Modellleistung zu verbessern.

**Parameter**

Die nachstehende Tabelle enthält wichtige Parameter für die Konfiguration und Optimierung der Leistung des [!DNL Gradient Boosted Tree Classifier].

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|-------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Die maximale Anzahl von Klassen bestimmt, wie kontinuierliche Merkmale in diskrete Intervalle aufgeteilt werden. Dies wirkt sich darauf aus, wie Funktionen auf jedem Entscheidungsbaum-Knoten aufgeteilt werden. Mehr Klassen bieten eine höhere Granularität. | 32 | Muss mindestens 2 und gleich oder größer als die Anzahl der Kategorien in einer beliebigen kategorischen Funktion sein. |
| `CACHE_NODE_IDS` | Wenn `false`, übergibt der Algorithmus Bäume an Executors, um Instanzen mit Knoten abzugleichen. Wenn der Wert `true` beträgt, speichert der Algorithmus Knoten-IDs für jede Instanz zwischen, was die Schulung tiefer liegender Bäume beschleunigt. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Gibt an, wie oft die zwischengespeicherten Knoten-IDs überprüft werden. Beispiel: `10` bedeutet, dass der Cache alle 10 Iterationen überprüft wird. | 10 | (>= 1) |
| `MAX_DEPTH` | Die maximale Tiefe der Baumstruktur (nicht negativ). Beispielsweise bedeutet &quot;depth `0`&quot;einen Blattknoten und &quot;depth `1`&quot;einen internen Knoten und 2 Blattknoten. | 5 | (>= 0) |
| `MIN_INFO_GAIN` | Der Mindestinformationsgewinn, der erforderlich ist, damit eine Aufspaltung in einem Strukturknoten berücksichtigt werden kann. | 0,0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | Der Mindestanteil der gewichteten Stichprobenanzahl, die jedes Kind nach einer Aufspaltung aufweisen muss. Wenn eine Aufspaltung dazu führt, dass der Anteil der Gesamtgewichtung in einem der untergeordneten Elemente unter diesem Wert liegt, wird er verworfen. | 0,0 | (>= 0.0, &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | Die Mindestanzahl von Instanzen, die jedes untergeordnete Element nach einer Aufspaltung aufweisen muss. Wenn eine Aufspaltung zu weniger Instanzen als diesem Wert führt, wird die Aufspaltung verworfen. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Der maximale Speicher in MB, der der Histogrammaggregation zugeordnet ist. Wenn dieser Wert zu klein ist, wird nur 1 Knoten pro Iteration aufgeteilt und die Aggregate können diese Größe überschreiten. | 256 | (>= 0) |
| `PREDICTION_COL` | Der Spaltenname für die Ausgabe der Prognose. | &quot;prediction&quot; | Beliebige Zeichenfolge |
| `VALIDATION_INDICATOR_COL` | Der Spaltenname gibt an, ob die einzelnen Zeilen für Schulungen oder Überprüfungen verwendet werden. Der Wert &quot;`false`&quot;zeigt das Training an und &quot;`true`&quot;zeigt die Validierung an. Wenn kein Wert festgelegt ist, ist der Standardwert `None`. | „Keine“ | Beliebige Zeichenfolge |
| `RAW_PREDICTION_COL` | Der Spaltenname für Rohdatenprognosewerte (auch als Konfidenz bezeichnet). | &quot;rawPreforecast&quot; | Beliebige Zeichenfolge |
| `LEAF_COL` | Der Spaltenname für Blattindizes, d. h. der prognostizierte Blattindex jeder Instanz in jedem Baum, der durch Preorder Traversal generiert wird. | &quot;&quot; | Beliebige Zeichenfolge |
| `FEATURE_SUBSET_STRATEGY` | Die Anzahl der Funktionen, die für die Aufteilung auf jedem Baumknoten berücksichtigt werden. Unterstützte Optionen: `auto` (automatisch basierend auf der Aufgabe bestimmt), `all` (alle Funktionen verwenden), `onethird` (Verwendung eines Drittels der Funktionen), `sqrt` (Verwendung der Quadratwurzel der Anzahl der Funktionen), `log2` (Verwendung des Basis-2-Logarithmus der Anzahl der Funktionen) und `n` (wobei n entweder ein Bruchteil der Funktionen im Bereich `(0, 1]` oder eine bestimmte Anzahl von Funktionen ist wenn im Bereich `[1, total number of features]`). | &quot;auto&quot; | `auto`, `all`, `onethird`, `sqrt`, `log2`, `n` |
| `WEIGHT_COL` | Der Spaltenname, z. B. die Gewichtung. Wenn nicht festgelegt oder leer, werden alle Instanzgewichte als `1.0` behandelt. | NICHT GESETZT | Beliebige Zeichenfolge |
| `LOSS_TYPE` | Die Verlustfunktion, die das Modell [!DNL Gradient Boosted Tree] zu minimieren versucht. | &quot;logistisch&quot; | `logistic` (nicht von Schreibweise abhängig) |
| `STEP_SIZE` | Die Schrittgröße (auch als Lernrate bezeichnet) im Bereich `(0, 1]`, die verwendet wird, um den Beitrag der einzelnen Schätzer zu verkleinern. | 0,1 | (>= 0,0, &lt;= 1) |
| `MAX_ITER` | Die maximale Anzahl von Iterationen für den Algorithmus. | 20 | (>= 0) |
| `SUBSAMPLING_RATE` | Der Bruchteil der Schulungsdaten, die zum Trainieren der einzelnen Entscheidungsstrukturen verwendet werden. Der Wert muss im Bereich 0 &lt; Wert &lt;= 1 liegen. | 1,0 | `(0, 1]` |
| `PROBABILITY_COL` | Der Spaltenname für prognostizierte bedingte Klassenwahrscheinlichkeiten. Hinweis: Nicht alle Modelle liefern gut kalibrierte Wahrscheinlichkeiten; diese sollten als Konfidenzwerte und nicht als exakte Wahrscheinlichkeiten behandelt werden. | &quot;wahrscheinlichkeit&quot; | Beliebige Zeichenfolge |
| `ONE_VS_REST` | Aktiviert oder deaktiviert das Umbrechen dieses Algorithmus mit Eins- vs. Ruhezustand für mehrklassige Classification. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Beispiel**

```sql
Create MODEL modelname OPTIONS(
  type = 'gradient_boosted_tree_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Linear Support Vector Classifier] (LinearSVC) {#linear-support-vector-classifier}

Der [!DNL Linear Support Vector Classifier] (LinearSVC) erstellt eine Hyperebene, um Daten in einem hochdimensionalen Raum zu klassifizieren. Sie können sie verwenden, um den Rand zwischen Klassen zu maximieren, um Classification-Fehler zu minimieren.

**Parameter**

Die nachstehende Tabelle enthält wichtige Parameter für die Konfiguration und Optimierung der Leistung des [!DNL Linear Support Vector Classifier (LinearSVC)].

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_ITER` | Die maximale Anzahl der Iterationen, die der Algorithmus ausführen soll. | 100 | (>= 0) |
| `AGGREGATION_DEPTH` | Die Tiefe für die Baumaggregation. Dieser Parameter wird verwendet, um den Mehraufwand für die Netzwerkkommunikation zu reduzieren. | 2 | Beliebige positive ganze Zahl |
| `FIT_INTERCEPT` | Ob ein Begriffsbegriff passt. | `true` | `true`, `false` |
| `TOL` | Dieser Parameter legt den Schwellenwert zum Anhalten von Iterationen fest. | 1E-6 | (>= 0) |
| `MAX_BLOCK_SIZE_IN_MB` | Der maximale Speicher in MB für die Stapelung von Eingabedaten in Blöcken. Wenn der Parameter auf `0` gesetzt ist, wird automatisch der optimale Wert ausgewählt (normalerweise etwa 1 MB). | 0,0 | (>= 0) |
| `REG_PARAM` | Der Regularisierungsparameter hilft bei der Steuerung der Modellkomplexität und der Vermeidung einer Überanpassung. | 0,0 | (>= 0) |
| `STANDARDIZATION` | Dieser Parameter gibt an, ob die Trainings-Funktionen standardisiert werden sollen, bevor das Modell angepasst wird. | `true` | `true`, `false` |
| `PREDICTION_COL` | Der Spaltenname für die Ausgabe der Prognose. | &quot;prediction&quot; | Beliebige Zeichenfolge |
| `RAW_PREDICTION_COL` | Der Spaltenname für Rohdatenprognosewerte (auch als Konfidenz bezeichnet). | &quot;rawPreforecast&quot; | Beliebige Zeichenfolge |
| `ONE_VS_REST` | Aktiviert oder deaktiviert das Umbrechen dieses Algorithmus mit Eins- vs. Ruhezustand für mehrklassige Classification. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Beispiel**

```sql
Create MODEL modelname OPTIONS(
  type = 'linear_svc_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Logistic Regression] {#logistic-regression}

[!DNL Logistic Regression] ist ein beaufsichtigter Algorithmus, der für binäre Klassifizierungsaufgaben verwendet wird. Sie modelliert die Wahrscheinlichkeit, dass eine Instanz zu einer Klasse gehört, mithilfe der logistischen Funktion und weist die Instanz der Klasse mit der höheren Wahrscheinlichkeit zu. Dies ist für Probleme geeignet, bei denen die Daten in eine von zwei Kategorien unterteilt werden sollen.

**Parameter**

In der folgenden Tabelle sind die wichtigsten Parameter für die Konfiguration und Optimierung der Leistung von [!DNL Logistic Regression] aufgeführt.

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|----------------|
| `MAX_ITER` | Die maximale Anzahl von Iterationen, die der Algorithmus ausführt. | 100 | (>= 0) |
| `REGPARAM` | Der Regularisierungsparameter wird verwendet, um die Komplexität des Modells zu steuern. | 0,0 | (>= 0) |
| `ELASTICNETPARAM` | Der Mixingparameter `ElasticNet` steuert das Gleichgewicht zwischen L1 (Lasso) und L2 (Ridge). Bei einem Wert von 0 wird eine L2-Strafe (Ridge, die die Größe der Koeffizienten verringert) angewendet, während bei einem Wert von 1 eine L1-Strafe (Lasso, der die Sparsamkeit durch die Festlegung einiger Koeffizienten auf Null fördert) angewendet wird. | 0,0 | (>= 0, &lt;= 1) |

{style="table-layout:auto"}

**Beispiel**

```sql
Create MODEL modelname OPTIONS(
  type = 'logistic_reg'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Multilayer Perceptron Classifier] {#multilayer-perceptron-classifier}

Der [!DNL Multilayer Perceptron Classifier] (MLPC) ist ein künstlichen neuronalen Netzwerk-Klassifizierer für den Feedback. Sie besteht aus mehreren vollständig verbundenen Knotenschichten, wobei jeder Knoten eine gewichtete lineare Kombination von Eingaben anwendet, gefolgt von einer Aktivierungsfunktion. MLPC wird für komplexe Klassifizierungsaufgaben verwendet, die nichtlineare Entscheidungsgrenzen erfordern.

**Parameter**

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------|
| `MAX_ITER` | Die maximale Anzahl der Iterationen, die der Algorithmus ausführen soll. | 100 | (>= 0) |
| `BLOCK_SIZE` | Die Blockgröße für die Stapelung von Eingabedaten in Matrizen in Partitionen. Wenn die Blockgröße die verbleibenden Daten einer Partition übersteigt, wird sie entsprechend angepasst. | 128 | (>= 0) |
| `STEP_SIZE` | Die Schrittgröße, die für jede Iteration der Optimierung verwendet wird (gilt nur für Resolver `gd`). | 0,03 | (> 0) |
| `TOL` | Die Konvergenztoleranz für die Optimierung. | `1E-6` | (>= 0) |
| `PREDICTION_COL` | Der Spaltenname für die Ausgabe der Prognose. | &quot;prediction&quot; | Beliebige Zeichenfolge |
| `SEED` | Die Zufallsstichprobe zur Steuerung zufälliger Prozesse im Algorithmus. | NICHT GESETZT | Beliebige 64-Bit-Zahl |
| `PROBABILITY_COL` | Der Spaltenname für prognostizierte bedingte Klassenwahrscheinlichkeiten. Diese sollten als Konfidenzwerte und nicht als exakte Wahrscheinlichkeiten behandelt werden. | &quot;wahrscheinlichkeit&quot; | Beliebige Zeichenfolge |
| `RAW_PREDICTION_COL` | Der Spaltenname für Rohdatenprognosewerte (auch als Konfidenz bezeichnet). | &quot;rawPreforecast&quot; | Beliebige Zeichenfolge |
| `ONE_VS_REST` | Aktiviert oder deaktiviert das Umbrechen dieses Algorithmus mit Eins- vs. Ruhezustand für mehrklassige Classification. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Beispiel**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'multilayer_perceptron_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Naive Bayes Classifier] {#naive-bayes-classifier}

[!DNL Naive Bayes Classifier] ist ein einfacher probabilistischer, mehrklassenbasierter Klassifizierer, der auf dem Bayes-Theorem basiert und starke (naive) Unabhängigkeitsannahmen zwischen Funktionen aufweist. Sie trainiert effizient, indem sie bedingte Wahrscheinlichkeiten in einem einzigen Übergang über die Trainings-Daten berechnet, um die bedingte Wahrscheinlichkeitsverteilung für jede Funktion für jede Bezeichnung zu berechnen. Für Prognosen verwendet er das Bayes-Theorem, um die bedingte Wahrscheinlichkeitsverteilung jedes einzelnen Kennzeichens, das eine Beobachtung erhalten hat, zu berechnen.

**Parameter**

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------------|
| `MODEL_TYPE` | Gibt den Modelltyp an. Unterstützte Optionen sind `"multinomial"`, `"complement"`, `"bernoulli"` und `"gaussian"`. Beim Modelltyp wird zwischen Groß- und Kleinschreibung unterschieden. | &quot;multinomial&quot; | `"multinomial"`, `"complement"`, `"bernoulli"`, `"gaussian"` |
| `SMOOTHING` | Der Ausgleichsparameter wird verwendet, um Probleme mit Nullfrequenzen in kategorischen Daten zu beheben. | 1,0 | (>= 0) |
| `PROBABILITY_COL` | Dieser Parameter gibt den Spaltennamen für die prognostizierten bedingten Klassenwahrscheinlichkeiten an. Hinweis: Nicht alle Modelle liefern gut kalibrierte Wahrscheinlichkeitsschätzungen; behandeln diese Werte als Konfidenzen und nicht als präzise Wahrscheinlichkeiten. | &quot;wahrscheinlichkeit&quot; | Beliebige Zeichenfolge |
| `WEIGHT_COL` | Der Spaltenname für die Instanzgewichtung. Wenn nicht festgelegt oder leer, werden alle Instanzgewichte als `1.0` behandelt. | NICHT GESETZT | Beliebige Zeichenfolge |
| `PREDICTION_COL` | Der Spaltenname für die Ausgabe der Prognose. | &quot;prediction&quot; | Beliebige Zeichenfolge |
| `RAW_PREDICTION_COL` | Der Spaltenname für Rohdatenprognosewerte (auch als Konfidenz bezeichnet). | &quot;rawPreforecast&quot; | Beliebige Zeichenfolge |
| `ONE_VS_REST` | Gibt an, ob Eins-vs-Rest für mehrklassige Classification aktiviert werden soll. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Beispiel**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'naive_bayes_classifier'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Random Forest Classifier] {#random-forest-classifier}

[!DNL Random Forest Classifier] ist ein Ensemble-Lernalgorithmus, der während des Trainings mehrere Entscheidungsbäume erstellt. Es reduziert Überanpassung, indem die Vorhersagen gemittelt und die Klasse ausgewählt wird, die von den meisten Bäumen für Klassifizierungsaufgaben ausgewählt wird.

**Parameter**

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Die maximale Anzahl von Klassen bestimmt, wie kontinuierliche Merkmale in diskrete Intervalle aufgeteilt werden. Dies wirkt sich darauf aus, wie Funktionen auf jedem Entscheidungsbaum-Knoten aufgeteilt werden. Mehr Klassen bieten eine höhere Granularität. | 32 | Muss mindestens 2 und gleich oder größer als die Anzahl der Kategorien in einer beliebigen kategorischen Funktion sein. |
| `CACHE_NODE_IDS` | Wenn `false`, übergibt der Algorithmus Bäume an Executors, um Instanzen mit Knoten abzugleichen. Wenn der Wert `true` beträgt, speichert der Algorithmus Knoten-IDs für jede Instanz zwischen, was die Schulung beschleunigt. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Gibt an, wie oft die zwischengespeicherten Knoten-IDs überprüft werden. Beispiel: `10` bedeutet, dass der Cache alle 10 Iterationen überprüft wird. | 10 | (>= 1) |
| `IMPURITY` | Das für die Berechnung des Informationsgewinns verwendete Kriterium (Groß-/Kleinschreibung nicht beachten). | &quot;gini&quot; | `entropy`, `gini` |
| `MAX_DEPTH` | Die maximale Tiefe der Baumstruktur (nicht negativ). Beispielsweise bedeutet &quot;depth `0`&quot;einen Blattknoten und &quot;depth `1`&quot;einen internen Knoten und 2 Blattknoten. | 5 | (>= 0) |
| `MIN_INFO_GAIN` | Der Mindestinformationsgewinn, der erforderlich ist, damit eine Aufspaltung in einem Strukturknoten berücksichtigt werden kann. | 0,0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | Der Mindestanteil der gewichteten Stichprobenanzahl, die jedes Kind nach einer Aufspaltung aufweisen muss. Wenn eine Aufspaltung dazu führt, dass der Anteil der Gesamtgewichtung in einem der untergeordneten Elemente unter diesem Wert liegt, wird er verworfen. | 0,0 | (>= 0.0, &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | Die Mindestanzahl von Instanzen, die jedes untergeordnete Element nach einer Aufspaltung aufweisen muss. Wenn eine Aufspaltung zu weniger Instanzen als diesem Wert führt, wird die Aufspaltung verworfen. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Der maximale Speicher in MB, der der Histogrammaggregation zugeordnet ist. Wenn dieser Wert zu klein ist, wird nur 1 Knoten pro Iteration aufgeteilt und die Aggregate können diese Größe überschreiten. | 256 | (>= 1) |
| `PREDICTION_COL` | Der Spaltenname für die Ausgabe der Prognose. | &quot;prediction&quot; | Beliebige Zeichenfolge |
| `WEIGHT_COL` | Der Spaltenname, z. B. die Gewichtung. Wenn nicht festgelegt oder leer, werden alle Instanzgewichte als `1.0` behandelt. | NICHT GESETZT | Beliebiger gültiger Spaltenname oder leer |
| `SEED` | Der Zufallsstichtest, der zur Steuerung zufälliger Prozesse im Algorithmus verwendet wird. | -1689246527 | Beliebige 64-Bit-Zahl |
| `BOOTSTRAP` | Ob Bootstrap-Proben beim Erstellen von Bäumen verwendet werden. | `true` | `true`, `false` |
| `NUM_TREES` | Die Anzahl der zu trainierenden Bäume. Wenn `1`, wird kein Bootstrapping verwendet. Wenn größer als `1` ist, wird das Bootstrapping angewendet. | 20 | (>= 1) |
| `SUBSAMPLING_RATE` | Der Anteil der Trainings-Daten, die für das Lernen der einzelnen Entscheidungsstrukturen verwendet werden. | 1,0 | (> 0, &lt;= 1) |
| `LEAF_COL` | Der Spaltenname für die Blattindizes, der den prognostizierten Blattindex jeder Instanz in jeder Baumstruktur nach Vorreihenfolge enthält. | &quot;&quot; | Beliebige Zeichenfolge |
| `PROBABILITY_COL` | Der Spaltenname für prognostizierte bedingte Klassenwahrscheinlichkeiten. Diese sollten als Konfidenzwerte und nicht als exakte Wahrscheinlichkeiten behandelt werden. | NICHT GESETZT | Beliebige Zeichenfolge |
| `RAW_PREDICTION_COL` | Der Spaltenname für Rohdatenprognosewerte (auch als Konfidenz bezeichnet). | &quot;rawPreforecast&quot; | Beliebige Zeichenfolge |
| `ONE_VS_REST` | Gibt an, ob Eins-vs-Rest für mehrklassige Classification aktiviert werden soll. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Beispiel**

```sql
Create MODEL modelname OPTIONS(
  type = 'random_forest_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie verschiedene Classification-Algorithmen konfigurieren und verwenden können. Weitere Informationen zu anderen Typen erweiterter statistischer Modelle finden Sie in den Dokumenten zu [Regression](./regression.md) und [Clustering](./clustering.md) .
