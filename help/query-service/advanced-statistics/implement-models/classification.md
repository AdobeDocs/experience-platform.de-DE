---
title: Klassifizierungsalgorithmen
description: Erfahren Sie, wie Sie verschiedene Klassifizierungsalgorithmen mit Schlüsselparametern, Beschreibungen und Beispiel-Code konfigurieren und optimieren können, um erweiterte statistische Modelle zu implementieren.
role: Developer
exl-id: 9105ab04-b480-48a0-b8f7-cf0ed5e5399d
source-git-commit: 489063fcd003e20f233a9c9d85d8cb6c22708d88
workflow-type: tm+mt
source-wordcount: '2449'
ht-degree: 4%

---

# Klassifizierungsalgorithmen {#classification-algorithms}

Dieses Dokument bietet einen Überblick über verschiedene Klassifizierungsalgorithmen, wobei der Schwerpunkt auf ihrer Konfiguration, den wichtigsten Parametern und der praktischen Verwendung in erweiterten statistischen Modellen liegt. Klassifizierungsalgorithmen werden verwendet, um Datenpunkten auf der Grundlage von Eingabefunktionen Kategorien zuzuweisen. Jeder Abschnitt enthält Parameterbeschreibungen und Beispiel-Code, der Ihnen bei der Implementierung und Optimierung dieser Algorithmen für Aufgaben wie Entscheidungsbäume, zufällige Gesamtstrukturen und native Bayes-Klassifizierung hilft.

## [!DNL Decision Tree Classifier] {#decision-tree-classifier}

[!DNL Decision Tree Classifier] ist ein überwachter Lernansatz, der in der Statistik, im Data Mining und im maschinellen Lernen verwendet wird. Bei diesem Ansatz wird ein Entscheidungsbaum als prädiktives Modell für Klassifizierungsaufgaben verwendet, das Schlussfolgerungen aus einer Reihe von Beobachtungen zieht.

**Parameter**

In der folgenden Tabelle sind die wichtigsten Parameter zur Konfiguration und Optimierung der Leistung eines [!DNL Decision Tree Classifier] aufgeführt.

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------|
| `MAX_BINS` | Die maximale Anzahl von Klassen bestimmt, wie kontinuierliche Funktionen in diskrete Intervalle unterteilt werden. Dies wirkt sich darauf aus, wie die Funktionen bei jedem Entscheidungsbaum-Knoten aufgeteilt werden. Mehr Klassen bieten eine höhere Granularität. | 32 | Muss mindestens 2 und mindestens gleich der Anzahl der Kategorien in einem kategorialen Merkmal sein. |
| `CACHE_NODE_IDS` | Wenn `false`, übergibt der Algorithmus Bäume an ausführende Benutzer, damit Instanzen mit Knoten abgeglichen werden. Wenn `true`, speichert der Algorithmus Knoten-IDs für jede Instanz zwischen, wodurch das Training tiefer stehender Baumstrukturen beschleunigt wird. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Gibt an, wie oft die zwischengespeicherten Knoten-IDs überprüft werden sollen. `10` bedeutet beispielsweise, dass der Cache alle 10 Iterationen überprüft wird. | 10 | (>= 1) |
| `IMPURITY` | Das Kriterium für die Berechnung des Informationsgewinns (ohne Unterscheidung zwischen Groß- und Kleinschreibung). | „Gini“ | `entropy`, `gini` |
| `MAX_DEPTH` | Die maximale Tiefe des Baums (nicht negativ). Beispielsweise bedeutet `0` Tiefe 1 Blattknoten und Tiefe `1` bedeutet 1 interner Knoten und 2 Blattknoten. | 5 | (>= 0) (Bereich: [0,30]) |
| `MIN_INFO_GAIN` | Der minimale Informationsgewinn, der erforderlich ist, damit eine Aufspaltung an einem Strukturknoten berücksichtigt wird. | 0,0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | Der MindestBRUCHTEIL der gewichteten Stichprobenanzahl, den jedes Kind nach einer Aufspaltung aufweisen muss. Wenn der Bruchteil des Gesamtgewichts bei einem der untergeordneten Elemente diesen Wert unterschreitet, wird er verworfen. | 0,0 | (>= 0.0, &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | Die Mindestanzahl von Instanzen, die jedes untergeordnete Element nach einer Aufspaltung aufweisen muss. Wenn eine Aufspaltung zu weniger Instanzen als diesen Wert führt, wird die Aufspaltung verworfen. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Der maximale Speicher in MB, der der Histogrammaggregation zugeordnet ist. Wenn dieser Wert zu klein ist, wird pro Iteration nur ein Knoten aufgeteilt, und seine Aggregate können diese Größe überschreiten. | 256 | (>= 0) |
| `PREDICTION_COL` | Der Spaltenname für die Prognoseausgabe. | „Prognose“ | Beliebige Zeichenfolge |
| `SEED` | Der zufällige Startwert. | K. A. | Beliebige 64-Bit-Zahl |
| `WEIGHT_COL` | Der Spaltenname, z. B., Gewichtungen. Wenn sie nicht festgelegt oder leer ist, werden alle Instanzgewichte als `1.0` behandelt. | NICHT FESTGELEGT | Beliebige Zeichenfolge |
| `ONE_VS_REST` | Aktiviert oder deaktiviert das Umbrechen dieses Algorithmus in One-vs-Rest, der für Probleme mit der Mehrklassen-Klassifizierung verwendet wird. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Beispiel**

```sql
Create MODEL modelname OPTIONS(
  type = 'decision_tree_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Factorization Machine Classifier] {#factorization-machine-classifier}

Der [!DNL Factorization Machine Classifier] ist ein Klassifizierungsalgorithmus, der den normalen Gradientenabstieg und den AdamW-Solver unterstützt. Das Klassifizierungsmodell der Faktorisierungsmaschine nutzt logistische Verluste, die über die Gradientenabsenkung optimiert werden können und oft Regularisierungsbegriffe wie L2 enthalten, um eine Überanpassung zu verhindern.

**Parameter**

In der folgenden Tabelle sind die wichtigsten Parameter zur Konfiguration und Optimierung der [!DNL Factorization Machine Classifier] aufgeführt.

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-------------------------------------------------------------------------------------------------------|
| `TOL` | Die Konvergenztoleranz, die die Genauigkeit der Optimierung steuert. | `1E-6` | (>= 0) |
| `FACTOR_SIZE` | Die Dimensionalität der Faktoren. | 8 | (>= 0) |
| `FIT_INTERCEPT` | Gibt an, ob ein Schnittstellenbegriff eingefügt werden soll. | `true` | `true`, `false` |
| `FIT_LINEAR` | Gibt an, ob der lineare Begriff (auch als 1-Wege-Begriff bezeichnet) angepasst werden soll. | `true` | `true`, `false` |
| `INIT_STD` | Die Standardabweichung für Initialisierungskoeffizienten. | 0,01 | (>= 0) |
| `MAX_ITER` | Die maximale Anzahl von Iterationen, die der Algorithmus ausführen soll. | 100 | (>= 0) |
| `MINI_BATCH_FRACTION` | Der Teil der Daten, der während des Trainings in Mini-Batches verwendet werden soll. Muss im Bereich `(0, 1]` liegen. | 1,0 | 0 &lt; Wert &lt;= 1 |
| `REG_PARAM` | Der Regularisierungsparameter, mit dem die Modellkomplexität kontrolliert und Überanpassung verhindert werden kann. | 0,0 | (>= 0) |
| `SEED` | Der zufällige Startwert für die Steuerung zufälliger Prozesse im Algorithmus. | K. A. | Beliebige 64-Bit-Zahl |
| `SOLVER` | Der für die Optimierung verwendete Solver-Algorithmus. Unterstützte Optionen sind `gd` (Verlaufsabstieg) und `adamW`. | „adamW“ | `gd`, `adamW` |
| `STEP_SIZE` | Die anfängliche Schrittgröße für die Optimierung, häufig interpretiert als Lernrate. | 1,0 | > 0 |
| `PROBABILITY_COL` | Der Spaltenname für prognostizierte bedingte Klassenwahrscheinlichkeiten. Hinweis: Nicht alle Modelle geben gut kalibrierte Wahrscheinlichkeiten aus. Diese sollten als Konfidenzwerte und nicht als exakte Wahrscheinlichkeiten behandelt werden. | „Wahrscheinlichkeit“ | Beliebige Zeichenfolge |
| `PREDICTION_COL` | Der Spaltenname für prognostizierte Klassenbezeichnungen. | „Prognose“ | Beliebige Zeichenfolge |
| `RAW_PREDICTION_COL` | Der Spaltenname für die rohen Prognosewerte (auch als Konfidenz bezeichnet). | „rawPrediction“ | Beliebige Zeichenfolge |
| `ONE_VS_REST` | Gibt an, ob One-vs-Rest für die Mehrklassenklassifizierung aktiviert werden soll. | FALSCH | `true`, `false` |

{style="table-layout:auto"}

**Beispiel**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'factorization_machines_classifier'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Gradient Boosted Tree Classifier] {#gradient-boosted-tree-classifier}

Die [!DNL Gradient Boosted Tree Classifier] verwendet ein Ensemble von Entscheidungsbäumen, um die Genauigkeit von Klassifizierungsaufgaben zu verbessern, indem mehrere Bäume kombiniert werden, um die Modellleistung zu verbessern.

**Parameter**

In der folgenden Tabelle sind die wichtigsten Parameter zur Konfiguration und Optimierung der [!DNL Gradient Boosted Tree Classifier] aufgeführt.

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|-------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Die maximale Anzahl von Klassen bestimmt, wie kontinuierliche Funktionen in diskrete Intervalle unterteilt werden. Dies wirkt sich darauf aus, wie die Funktionen bei jedem Entscheidungsbaum-Knoten aufgeteilt werden. Mehr Klassen bieten eine höhere Granularität. | 32 | Muss mindestens 2 sein und gleich oder größer als die Anzahl der Kategorien in einem kategorialen Merkmal sein. |
| `CACHE_NODE_IDS` | Wenn `false`, übergibt der Algorithmus Bäume an ausführende Benutzer, damit Instanzen mit Knoten abgeglichen werden. Wenn `true`, speichert der Algorithmus Knoten-IDs für jede Instanz zwischen, wodurch das Training tiefer stehender Baumstrukturen beschleunigt wird. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Gibt an, wie oft die zwischengespeicherten Knoten-IDs überprüft werden sollen. `10` bedeutet beispielsweise, dass der Cache alle 10 Iterationen überprüft wird. | 10 | (>= 1) |
| `MAX_DEPTH` | Die maximale Tiefe des Baums (nicht negativ). Beispielsweise bedeutet `0` Tiefe 1 Blattknoten und Tiefe `1` bedeutet 1 interner Knoten und 2 Blattknoten. | 5 | (>= 0) |
| `MIN_INFO_GAIN` | Der minimale Informationsgewinn, der erforderlich ist, damit eine Aufspaltung an einem Strukturknoten berücksichtigt wird. | 0,0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | Der MindestBRUCHTEIL der gewichteten Stichprobenanzahl, den jedes Kind nach einer Aufspaltung aufweisen muss. Wenn der Bruchteil des Gesamtgewichts bei einem der untergeordneten Elemente diesen Wert unterschreitet, wird er verworfen. | 0,0 | (>= 0.0, &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | Die Mindestanzahl von Instanzen, die jedes untergeordnete Element nach einer Aufspaltung aufweisen muss. Wenn eine Aufspaltung zu weniger Instanzen als diesen Wert führt, wird die Aufspaltung verworfen. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Der maximale Speicher in MB, der der Histogrammaggregation zugeordnet ist. Wenn dieser Wert zu klein ist, wird pro Iteration nur ein Knoten aufgeteilt, und seine Aggregate können diese Größe überschreiten. | 256 | (>= 0) |
| `PREDICTION_COL` | Der Spaltenname für die Prognoseausgabe. | „Prognose“ | Beliebige Zeichenfolge |
| `VALIDATION_INDICATOR_COL` | Der Spaltenname gibt an, ob jede Zeile für das Training oder die Validierung verwendet wird. Der Wert `false` steht für Training und `true` für Validierung. Wenn kein Wert festgelegt ist, lautet der Standardwert `None`. | „Keine“ | Beliebige Zeichenfolge |
| `RAW_PREDICTION_COL` | Der Spaltenname für die rohen Prognosewerte (auch als Konfidenz bezeichnet). | „rawPrediction“ | Beliebige Zeichenfolge |
| `LEAF_COL` | Der Spaltenname für Blattindizes, der der prognostizierte Blattindex jeder Instanz in jedem Baum ist, der durch Durchlaufen der Vorbestellung generiert wird. | &quot;&quot; | Beliebige Zeichenfolge |
| `FEATURE_SUBSET_STRATEGY` | Die Anzahl der Funktionen, die für die Aufspaltung bei jedem Strukturknoten berücksichtigt werden. Unterstützte Optionen: `auto` (basierend auf der Aufgabe automatisch bestimmt), `all` (alle Funktionen verwenden), `onethird` (ein Drittel der Funktionen verwenden), `sqrt` (die Quadratwurzel der Anzahl der Funktionen verwenden), `log2` (den Logarithmus zur Basis 2 der Anzahl der Funktionen verwenden) und `n` (wobei n entweder ein Bruchteil der Funktionen ist, wenn im Bereich `(0, 1]`, oder eine bestimmte Anzahl von Funktionen ist, wenn im Bereich `[1, total number of features]`). | „auto“ | `auto`, `all`, `onethird`, `sqrt`, `log2`, `n` |
| `WEIGHT_COL` | Der Spaltenname, z. B., Gewichtungen. Wenn sie nicht festgelegt oder leer ist, werden alle Instanzgewichte als `1.0` behandelt. | NICHT FESTGELEGT | Beliebige Zeichenfolge |
| `LOSS_TYPE` | Die Verlustfunktion, die das [!DNL Gradient Boosted Tree] zu minimieren versucht. | „Logistisch“ | `logistic` (ignoriert Groß- und Kleinschreibung) |
| `STEP_SIZE` | Die Schrittgröße (auch als Lernrate bezeichnet) im Bereich `(0, 1]`, die zum Verkleinern des Beitrags jeder Schätzung verwendet wird. | 0,1 | (>= 0.0, &lt;= 1) |
| `MAX_ITER` | Die maximale Anzahl von Iterationen für den Algorithmus. | 20 | (>= 0) |
| `SUBSAMPLING_RATE` | Der Teil der Trainingsdaten, der zum Trainieren der einzelnen Entscheidungsbäume verwendet wird. Der Wert muss im Bereich 0 &lt; Wert &lt;= 1 liegen. | 1,0 | `(0, 1]` |
| `PROBABILITY_COL` | Der Spaltenname für prognostizierte bedingte Klassenwahrscheinlichkeiten. Hinweis: Nicht alle Modelle geben gut kalibrierte Wahrscheinlichkeiten aus. Diese sollten als Konfidenzwerte und nicht als exakte Wahrscheinlichkeiten behandelt werden. | „Wahrscheinlichkeit“ | Beliebige Zeichenfolge |
| `ONE_VS_REST` | Aktiviert oder deaktiviert das Umschließen dieses Algorithmus mit One-vs-Rest für die Mehrklassen-Klassifizierung. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Beispiel**

```sql
Create MODEL modelname OPTIONS(
  type = 'gradient_boosted_tree_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Linear Support Vector Classifier] (LineSVC) {#linear-support-vector-classifier}

Die [!DNL Linear Support Vector Classifier] (LinearSVC) konstruiert eine Hyperebene zur Klassifizierung von Daten in einem hochdimensionalen Raum. Sie können damit den Abstand zwischen den Klassen maximieren, um Klassifizierungsfehler zu minimieren.

**Parameter**

In der folgenden Tabelle sind die wichtigsten Parameter zur Konfiguration und Optimierung der [!DNL Linear Support Vector Classifier (LinearSVC)] aufgeführt.

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_ITER` | Die maximale Anzahl von Iterationen, die der Algorithmus ausführen soll. | 100 | (>= 0) |
| `AGGREGATION_DEPTH` | Die Tiefe für die Baumaggregation. Dieser Parameter wird verwendet, um den Netzwerk-Kommunikationsaufwand zu reduzieren. | 2 | Beliebige positive Ganzzahl |
| `FIT_INTERCEPT` | Gibt an, ob ein Abfangbegriff eingefügt werden soll. | `true` | `true`, `false` |
| `TOL` | Dieser Parameter bestimmt den Schwellenwert für das Stoppen von Iterationen. | 1e-6 | (>= 0) |
| `MAX_BLOCK_SIZE_IN_MB` | Der maximale Speicher in MB für das Stapeln von Eingabedaten in Blöcken. Wenn der Parameter auf `0` gesetzt ist, wird automatisch der optimale Wert ausgewählt (in der Regel um 1 MB). | 0,0 | (>= 0) |
| `REG_PARAM` | Der Regularisierungsparameter, mit dem die Modellkomplexität kontrolliert und Überanpassung verhindert werden kann. | 0,0 | (>= 0) |
| `STANDARDIZATION` | Dieser Parameter gibt an, ob die Trainingsfunktionen vor dem Anpassen des Modells standardisiert werden sollen. | `true` | `true`, `false` |
| `PREDICTION_COL` | Der Spaltenname für die Prognoseausgabe. | „Prognose“ | Beliebige Zeichenfolge |
| `RAW_PREDICTION_COL` | Der Spaltenname für die rohen Prognosewerte (auch als Konfidenz bezeichnet). | „rawPrediction“ | Beliebige Zeichenfolge |
| `ONE_VS_REST` | Aktiviert oder deaktiviert das Umschließen dieses Algorithmus mit One-vs-Rest für die Mehrklassen-Klassifizierung. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Beispiel**

```sql
Create MODEL modelname OPTIONS(
  type = 'linear_svc_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Logistic Regression] {#logistic-regression}

[!DNL Logistic Regression] ist ein überwachter Algorithmus, der für binäre Klassifizierungsaufgaben verwendet wird. Es modelliert die Wahrscheinlichkeit, dass eine Instanz zu einer Klasse gehört, mithilfe der logistischen Funktion und weist die Instanz der Klasse mit der höheren Wahrscheinlichkeit zu. Dadurch eignet es sich für Probleme, bei denen das Ziel darin besteht, Daten in eine von zwei Kategorien zu unterteilen.

**Parameter**

In der folgenden Tabelle sind die wichtigsten Parameter zur Konfiguration und Optimierung der Leistung von [!DNL Logistic Regression] aufgeführt.

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|----------------|
| `MAX_ITER` | Die maximale Anzahl von Iterationen, die der Algorithmus ausführt. | 100 | (>= 0) |
| `REGPARAM` | Der Regularisierungsparameter wird verwendet, um die Komplexität des Modells zu steuern. | 0,0 | (>= 0) |
| `ELASTICNETPARAM` | Der `ElasticNet` Mischparameter steuert das Gleichgewicht zwischen L1 (Lasso) und L2 (Ridge) Strafen. Bei einem Wert von 0 wird eine L2-Strafe angewendet (Ridge, wodurch die Größe der Koeffizienten verringert wird), während bei einem Wert von 1 eine L1-Strafe angewendet wird (Lasso, das die Sparsity fördert, indem einige Koeffizienten auf null gesetzt werden). | 0,0 | (>= 0, &lt;= 1) |

{style="table-layout:auto"}

**Beispiel**

```sql
Create MODEL modelname OPTIONS(
  type = 'logistic_reg'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Multilayer Perceptron Classifier] {#multilayer-perceptron-classifier}

Der [!DNL Multilayer Perceptron Classifier] (MLPC) ist ein vorwärtsgerichteter Klassifikator für neuronale Netze. Es besteht aus mehreren vollständig verbundenen Knotenschichten, wobei jeder Knoten eine gewichtete lineare Kombination von Eingängen anwendet, gefolgt von einer Aktivierungsfunktion. MLPC wird für komplexe Klassifizierungsaufgaben eingesetzt, die nichtlineare Entscheidungsgrenzen erfordern.

**Parameter**

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------|
| `MAX_ITER` | Die maximale Anzahl von Iterationen, die der Algorithmus ausführen soll. | 100 | (>= 0) |
| `BLOCK_SIZE` | Die Blockgröße zum Stapeln von Eingabedaten in Matrizen innerhalb von Partitionen. Wenn die Blockgröße die verbleibenden Daten in einer Partition überschreitet, wird sie entsprechend angepasst. | 128 | (>= 0) |
| `STEP_SIZE` | Die Schrittgröße, die für jede Iteration der Optimierung verwendet wird (gilt nur für Solver-`gd`). | 0,03 | (> 0) |
| `TOL` | Die Konvergenztoleranz für die Optimierung. | `1E-6` | (>= 0) |
| `PREDICTION_COL` | Der Spaltenname für die Prognoseausgabe. | „Prognose“ | Beliebige Zeichenfolge |
| `SEED` | Der zufällige Startwert für die Steuerung zufälliger Prozesse im Algorithmus. | NICHT FESTGELEGT | Beliebige 64-Bit-Zahl |
| `PROBABILITY_COL` | Der Spaltenname für prognostizierte bedingte Klassenwahrscheinlichkeiten. Diese sollten als Konfidenzwerte und nicht als exakte Wahrscheinlichkeiten behandelt werden. | „Wahrscheinlichkeit“ | Beliebige Zeichenfolge |
| `RAW_PREDICTION_COL` | Der Spaltenname für die rohen Prognosewerte (auch als Konfidenz bezeichnet). | „rawPrediction“ | Beliebige Zeichenfolge |
| `ONE_VS_REST` | Aktiviert oder deaktiviert das Umschließen dieses Algorithmus mit One-vs-Rest für die Mehrklassen-Klassifizierung. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Beispiel**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'multilayer_perceptron_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Naive Bayes Classifier] {#naive-bayes-classifier}

[!DNL Naive Bayes Classifier] ist ein einfacher probabilistischer, mehrklassiger Klassifikator, der auf dem Satz von Bayes basiert und von starken (naiven) Annahmen bezüglich der Unabhängigkeit zwischen den Merkmalen ausgeht. Es trainiert effizient, indem es die bedingten Wahrscheinlichkeiten in einem einzigen Durchgang über die Trainingsdaten berechnet, um die bedingte Wahrscheinlichkeitsverteilung jeder Funktion für jede Kennzeichnung zu berechnen. Für Vorhersagen verwendet es den Satz von Bayes, um die bedingte Wahrscheinlichkeitsverteilung jeder einzelnen Markierung für eine Beobachtung zu berechnen.

**Parameter**

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------------|
| `MODEL_TYPE` | Gibt den Modelltyp an. Unterstützte Optionen sind `"multinomial"`, `"complement"`, `"bernoulli"` und `"gaussian"`. Beim Modelltyp wird zwischen Groß- und Kleinschreibung unterschieden. | „Multinomial“ | `"multinomial"`, `"complement"`, `"bernoulli"`, `"gaussian"` |
| `SMOOTHING` | Der Glättungsparameter wird zur Behandlung von Nullfrequenzproblemen in kategorialen Daten verwendet. | 1,0 | (>= 0) |
| `PROBABILITY_COL` | Dieser Parameter gibt den Spaltennamen für bedingte Wahrscheinlichkeiten der prognostizierten Klasse an. Hinweis: Nicht alle Modelle liefern gut kalibrierte Wahrscheinlichkeitsschätzungen. Behandeln Sie diese Werte als Konfidenzen und nicht als präzise Wahrscheinlichkeiten. | „Wahrscheinlichkeit“ | Beliebige Zeichenfolge |
| `WEIGHT_COL` | Der Spaltenname für die Gewichtung der Instanz. Wenn sie nicht festgelegt oder leer ist, werden alle Instanzgewichte als `1.0` behandelt. | NICHT FESTGELEGT | Beliebige Zeichenfolge |
| `PREDICTION_COL` | Der Spaltenname für die Prognoseausgabe. | „Prognose“ | Beliebige Zeichenfolge |
| `RAW_PREDICTION_COL` | Der Spaltenname für die rohen Prognosewerte (auch als Konfidenz bezeichnet). | „rawPrediction“ | Beliebige Zeichenfolge |
| `ONE_VS_REST` | Gibt an, ob One-vs-Rest für die Mehrklassenklassifizierung aktiviert werden soll. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Beispiel**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'naive_bayes_classifier'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Random Forest Classifier] {#random-forest-classifier}

[!DNL Random Forest Classifier] ist ein Lernalgorithmus für ein Ensemble, der während des Trainings mehrere Entscheidungsbäume erstellt. Es verhindert Überanpassung, indem es Vorhersagen mittelt und die von der Mehrheit der Bäume für Klassifizierungsaufgaben gewählte Klasse auswählt.

**Parameter**

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Die maximale Anzahl von Klassen bestimmt, wie kontinuierliche Funktionen in diskrete Intervalle unterteilt werden. Dies wirkt sich darauf aus, wie die Funktionen bei jedem Entscheidungsbaum-Knoten aufgeteilt werden. Mehr Klassen bieten eine höhere Granularität. | 32 | Muss mindestens 2 sein und gleich oder größer als die Anzahl der Kategorien in einem kategorialen Merkmal sein. |
| `CACHE_NODE_IDS` | Wenn `false`, übergibt der Algorithmus Bäume an ausführende Benutzer, damit Instanzen mit Knoten abgeglichen werden. Wenn `true`, speichert der Algorithmus Knoten-IDs für jede Instanz zwischen, wodurch das Training beschleunigt wird. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Gibt an, wie oft die zwischengespeicherten Knoten-IDs überprüft werden sollen. `10` bedeutet beispielsweise, dass der Cache alle 10 Iterationen überprüft wird. | 10 | (>= 1) |
| `IMPURITY` | Das Kriterium für die Berechnung des Informationsgewinns (ohne Unterscheidung zwischen Groß- und Kleinschreibung). | „Gini“ | `entropy`, `gini` |
| `MAX_DEPTH` | Die maximale Tiefe des Baums (nicht negativ). Beispielsweise bedeutet `0` Tiefe 1 Blattknoten und Tiefe `1` bedeutet 1 interner Knoten und 2 Blattknoten. | 5 | (>= 0) |
| `MIN_INFO_GAIN` | Der minimale Informationsgewinn, der erforderlich ist, damit eine Aufspaltung an einem Strukturknoten berücksichtigt wird. | 0,0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | Der MindestBRUCHTEIL der gewichteten Stichprobenanzahl, den jedes Kind nach einer Aufspaltung aufweisen muss. Wenn der Bruchteil des Gesamtgewichts bei einem der untergeordneten Elemente diesen Wert unterschreitet, wird er verworfen. | 0,0 | (>= 0.0, &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | Die Mindestanzahl von Instanzen, die jedes untergeordnete Element nach einer Aufspaltung aufweisen muss. Wenn eine Aufspaltung zu weniger Instanzen als diesen Wert führt, wird die Aufspaltung verworfen. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Der maximale Speicher in MB, der der Histogrammaggregation zugeordnet ist. Wenn dieser Wert zu klein ist, wird pro Iteration nur ein Knoten aufgeteilt, und seine Aggregate können diese Größe überschreiten. | 256 | (>= 1) |
| `PREDICTION_COL` | Der Spaltenname für die Prognoseausgabe. | „Prognose“ | Beliebige Zeichenfolge |
| `WEIGHT_COL` | Der Spaltenname, z. B., Gewichtungen. Wenn sie nicht festgelegt oder leer ist, werden alle Instanzgewichte als `1.0` behandelt. | NICHT FESTGELEGT | Beliebiger gültiger Spaltenname oder leer |
| `SEED` | Der zufällige Seed, der zum Steuern zufälliger Prozesse im Algorithmus verwendet wird. | -1689246527 | Beliebige 64-Bit-Zahl |
| `BOOTSTRAP` | Ob beim Erstellen von Bäumen Bootstrap-Beispiele verwendet werden. | `true` | `true`, `false` |
| `NUM_TREES` | Die Anzahl der zu trainierenden Bäume. Wenn `1`, wird kein Bootstrapping durchgeführt. Wenn größer als `1`, wird Bootstrapping angewendet. | 20 | (>= 1) |
| `SUBSAMPLING_RATE` | Der Teil der Schulungsdaten, der für das Erlernen jedes Entscheidungsbaums verwendet wird. | 1,0 | (> 0, &lt;= 1) |
| `LEAF_COL` | Der Spaltenname für die Blattindizes, der den prognostizierten Blattindex jeder Instanz in jedem Baum nach Vorreihenfolge enthält. | &quot;&quot; | Beliebige Zeichenfolge |
| `PROBABILITY_COL` | Der Spaltenname für prognostizierte bedingte Klassenwahrscheinlichkeiten. Diese sollten als Konfidenzwerte und nicht als exakte Wahrscheinlichkeiten behandelt werden. | NICHT FESTGELEGT | Beliebige Zeichenfolge |
| `RAW_PREDICTION_COL` | Der Spaltenname für die rohen Prognosewerte (auch als Konfidenz bezeichnet). | „rawPrediction“ | Beliebige Zeichenfolge |
| `ONE_VS_REST` | Gibt an, ob One-vs-Rest für die Mehrklassenklassifizierung aktiviert werden soll. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Beispiel**

```sql
Create MODEL modelname OPTIONS(
  type = 'random_forest_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie verschiedene Klassifizierungsalgorithmen konfigurieren und verwenden können. Weitere Informationen zu anderen Typen erweiterter statistischer Modelle finden [ in den Dokumenten ](./regression.md)Regression und [Clustering](./clustering.md).
