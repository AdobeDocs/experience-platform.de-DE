---
title: Clustering-Algorithmen
description: Erfahren Sie, wie Sie verschiedene Clustering-Algorithmen mit Schlüsselparametern, Beschreibungen und Beispiel-Code konfigurieren und optimieren können, um erweiterte statistische Modelle zu implementieren.
role: Developer
exl-id: 273853c6-85d2-43e5-b51a-aa9d20b313ae
source-git-commit: 69c08f688d355e689e78426dd4b0ed1f4934965c
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 4%

---

# Clustering-Algorithmen {#clustering-algorithms}

Clustering-Algorithmen gruppieren Datenpunkte basierend auf ihren Ähnlichkeiten in verschiedene Cluster, sodass unbeaufsichtigtes Lernen Muster innerhalb der Daten erkennen kann. Verwenden Sie zum Erstellen eines Clustering-Algorithmus den Parameter `type` in der `OPTIONS`-Klausel, um den Algorithmus anzugeben, den Sie für das Modell-Training verwenden möchten. Definieren Sie anschließend die relevanten Parameter als Schlüssel-Wert-Paare, um das Modell fein abzustimmen.

>[!NOTE]
>
>Stellen Sie sicher, dass Sie die Parameteranforderungen für den ausgewählten Algorithmus verstehen. Wenn Sie bestimmte Parameter nicht anpassen möchten, wendet das System die Standardeinstellungen an. In der entsprechenden Dokumentation finden Sie Informationen zur Funktion und zu den Standardwerten der einzelnen Parameter.

## [!DNL K-Means] {#kmeans}

`K-Means` ist ein Clustering-Algorithmus, der Datenpunkte in eine vordefinierte Anzahl von Clustern (K) unterteilt. Aufgrund seiner Einfachheit und Effizienz ist er einer der am häufigsten verwendeten Algorithmen für das Clustering.

**Parameter**

Bei Verwendung von `K-Means` können die folgenden Parameter in der `OPTIONS`-Klausel festgelegt werden:

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|---------------------|---------------------------------------------------------------------------------------------------------------|-----------------|----------------------------------|
| `MAX_ITER` | Die Anzahl der Iterationen, die der Algorithmus ausführen soll. | `20` | (>= 0) |
| `TOL` | Die Konvergenztoleranzstufe. | `0.0001` | (>= 0) |
| `NUM_CLUSTERS` | Die Anzahl der zu erstellenden Cluster (`k`). | `2` | (>1) |
| `DISTANCE_TYPE` | Der Algorithmus zur Berechnung des Abstands zwischen zwei Punkten. Bei dem Wert ist die Groß-/Kleinschreibung zu beachten. | `euclidean` | `euclidean`, `cosine` |
| `KMEANS_INIT_METHOD` | Der Initialisierungsalgorithmus für die Cluster-Center. | `k-means\|\|` | `random`, `k-means\|\|` (Eine Parallelversion von k-Means++) |
| `INIT_STEPS` | Die Anzahl der Schritte für den `k-means\|\|`-Initialisierungsmodus (gilt nur, wenn `KMEANS_INIT_METHOD` `k-means\|\|` ist). | `2` | (>0) |
| `PREDICTION_COL` | Der Name der Spalte, in der die Prognosen gespeichert werden. | `prediction` | Beliebige Zeichenfolge |
| `SEED` | Ein zufälliger Startwert für die Reproduzierbarkeit. | `-1689246527` | Beliebige 64-Bit-Zahl |
| `WEIGHT_COL` | Der Name der Spalte, die für die Gewichtung der Instanzen verwendet wird. Ist dies nicht festgelegt, werden alle Instanzen gleich gewichtet. | `not set` | K. A. |

{style="table-layout:auto"}

**Beispiel**

```sql
CREATE MODEL modelname 
OPTIONS(
  type = 'kmeans',
  MAX_ITERATIONS = 30,
  NUM_CLUSTERS = 4
) 
AS SELECT col1, col2, col3 FROM training-dataset;
```

## [!DNL Bisecting K-means] {#bisecting-kmeans}

[!DNL Bisecting K-means] ist ein hierarchischer Clustering-Algorithmus, der einen teilenden Ansatz (oder einen „Top-Down“-Ansatz) verwendet. Alle Beobachtungen beginnen in einem einzigen Cluster, und Aufspaltungen werden rekursiv durchgeführt, während die Hierarchie erstellt wird. [!DNL Bisecting K-means] kann häufig schneller sein als normale K-Means, liefert aber normalerweise andere Cluster-Ergebnisse.

**Parameter**

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------------|
| `MAX_ITER` | Die maximale Anzahl von Iterationen, die der Algorithmus ausführt. | 20 | (>= 0) |
| `WEIGHT_COL` | Der Spaltenname für die Gewichtung der Instanz. Wenn sie nicht festgelegt oder leer ist, werden alle Instanzgewichte als `1.0` behandelt. | NICHT FESTGELEGT | Beliebige Zeichenfolge |
| `NUM_CLUSTERS` | Die gewünschte Anzahl von Blattclustern. Die tatsächliche Zahl könnte kleiner sein, wenn keine teilbaren Cluster verbleiben. | 4 | (> 1) |
| `SEED` | Der zufällige Seed, der zum Steuern zufälliger Prozesse im Algorithmus verwendet wird. | NICHT FESTGELEGT | Beliebige 64-Bit-Zahl |
| `DISTANCE_MEASURE` | Das Entfernungsmaß, mit dem die Ähnlichkeit zwischen Punkten berechnet wird. | „euklidisch“ | `euclidean`, `cosine` |
| `MIN_DIVISIBLE_CLUSTER_SIZE` | Die Mindestanzahl von Punkten (wenn >= 1,0) oder der Mindestprozentsatz von Punkten (wenn &lt; 1,0), die erforderlich sind, damit ein Cluster teilbar ist. | 1,0 | (>= 0) |
| `PREDICTION_COL` | Der Spaltenname für die Prognoseausgabe. | „Prognose“ | Beliebige Zeichenfolge |

{style="table-layout:auto"}

**Beispiel**

```sql
Create MODEL modelname OPTIONS(
  type = 'bisecting_kmeans',
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Gaussian Mixture Model] {#gaussian-mixture-model}

[!DNL Gaussian Mixture Model] stellt eine zusammengesetzte Verteilung dar, bei der Datenpunkte aus einer von k Gaußschen Unterverteilungen mit jeweils eigener Wahrscheinlichkeit gezogen werden. Er wird zur Modellierung von Datensätzen verwendet, bei denen angenommen wird, dass sie aus einer Mischung mehrerer Gaußscher Verteilungen erzeugt werden.

**Parameter**

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------|
| `MAX_ITER` | Die maximale Anzahl von Iterationen, die der Algorithmus ausführen soll. | 100 | (>= 0) |
| `WEIGHT_COL` | Der Spaltenname, z. B., Gewichtungen. Wenn sie nicht festgelegt oder leer ist, werden alle Instanzgewichte als `1.0` behandelt. | NICHT FESTGELEGT | Beliebiger gültiger Spaltenname oder leer |
| `NUM_CLUSTERS` | Die Anzahl der unabhängigen Gaußschen Verteilungen im Mischungsmodell. | 2 | (> 1) |
| `SEED` | Der zufällige Startwert, der zur Steuerung zufälliger Prozesse im Algorithmus verwendet wird. | NICHT FESTGELEGT | Beliebige 64-Bit-Zahl |
| `AGGREGATION_DEPTH` | Dieser Parameter steuert die Tiefe der Aggregationsbäume, die während der Berechnung verwendet werden. | 2 | (>= 1) |
| `PROBABILITY_COL` | Der Spaltenname für prognostizierte bedingte Klassenwahrscheinlichkeiten. Diese sollten als Konfidenzwerte und nicht als exakte Wahrscheinlichkeiten behandelt werden. | „Wahrscheinlichkeit“ | Beliebige Zeichenfolge |
| `TOL` | Die Konvergenztoleranz für iterative Algorithmen. | 0,01 | (>= 0) |
| `PREDICTION_COL` | Der Spaltenname für die Prognoseausgabe. | „Prognose“ | Beliebige Zeichenfolge |

{style="table-layout:auto"}

**Beispiel**

```sql
Create MODEL modelname OPTIONS(
  type = 'gaussian_mixture',
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Latent Dirichlet Allocation] (LDA) {#latent-dirichlet-allocation}

[!DNL Latent Dirichlet Allocation] (LDA) ist ein probabilistisches Modell, das die zugrunde liegende Themenstruktur aus einer Sammlung von Dokumenten erfasst. Es handelt sich um ein hierarchisches Bayes&#39;sches Modell mit drei Ebenen mit Wort-, Thema- und Dokumentebenen. LDA verwendet diese Ebenen zusammen mit den beobachteten Dokumenten, um eine latente Themenstruktur zu erstellen.

**Parameter**

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------|
| `MAX_ITER` | Die maximale Anzahl von Iterationen, die der Algorithmus ausführt. | 20 | (>= 0) |
| `OPTIMIZER` | Der Optimierer oder Inferenzalgorithmus, der zur Schätzung des LDA-Modells verwendet wird. Unterstützte Optionen sind `"online"` (Online-Variantenreihen) und `"em"` (Erwartungsmaximierung). | „Online“ | `online`, `em` (ignoriert Groß- und Kleinschreibung) |
| `NUM_CLUSTERS` | Die Anzahl der zu erstellenden Cluster (k). | 10 | (> 1) |
| `CHECKPOINT_INTERVAL` | Gibt an, wie oft die zwischengespeicherten Knoten-IDs überprüft werden sollen. | 10 | (>= 1) |
| `DOC_CONCENTRATION` | Der Konzentrationsparameter („Alpha„) bestimmt die vorherigen Annahmen bezüglich der Themenverteilung in Dokumenten. Das Standardverhalten wird vom Optimizer bestimmt. Für den `EM` Optimizer sollten Alpha-Werte größer als 1,0 sein (Standard: gleichmäßig verteilt als (50/k) + 1), um symmetrische Themenverteilungen sicherzustellen. Für den `online` Optimizer können Alpha-Werte 0 oder höher sein (Standard: gleichmäßig verteilt als 1,0/k), was eine flexiblere Themeninitialisierung ermöglicht. | Automatisch | Ein einzelner Wert oder Vektor der Länge k, wobei Werte > 1 für EM sind |
| `KEEP_LAST_CHECKPOINT` | Gibt an, ob der letzte Checkpoint bei Verwendung des `em` beibehalten werden soll. Das Löschen des Checkpoints kann zu Fehlern führen, wenn eine Datenpartition verloren geht. Checkpoints werden automatisch aus dem Speicher entfernt, wenn sie nicht mehr benötigt werden, wie durch Referenzzählung ermittelt. | `true` | `true`, `false` |
| `LEARNING_DECAY` | Lernrate für den `online` Optimizer, festgelegt als exponentielle Abklingrate zwischen `(0.5, 1.0]`. | 0,51 | `(0.5, 1.0]` |
| `LEARNING_OFFSET` | Ein Lernparameter für den `online` Optimizer, der frühe Iterationen heruntergewichtet, damit frühe Iterationen weniger zählen. | 1024 | (> 0) |
| `SEED` | Zufälliger Seed zur Steuerung zufälliger Prozesse im Algorithmus. | NICHT FESTGELEGT | Beliebige 64-Bit-Zahl |
| `OPTIMIZE_DOC_CONCENTRATION` | Für den `online`-Optimizer: ob der `docConcentration` (Dirichlet-Parameter für die Verteilung von Dokumenten - Themenverteilung) während des Trainings optimiert werden soll. | `false` | `true`, `false` |
| `SUBSAMPLING_RATE` | Für den `online`-Optimizer: der Anteil des Korpus, der bei jeder Iteration des Abstiegs des Mini-Batch-Gradienten abgetastet und verwendet wird, im Bereich `(0, 1]`. | 0,05 | `(0, 1]` |
| `TOPIC_CONCENTRATION` | Der Konzentrationsparameter („Beta“ oder „Beta„) definiert die früheren Annahmen hinsichtlich der Verteilung der Themen über Begriffe. Der Standardwert wird vom Optimizer bestimmt: Für `EM` Werte > 1,0 (Standard = 0,1 + 1). Zum `online` Werte ≥ 0 (Standard = 1,0/k). | Automatisch | Ein einzelner Wert oder Vektor der Länge k, wobei Werte > 1 für EM sind |
| `TOPIC_DISTRIBUTION_COL` | Dieser Parameter gibt die geschätzte Verteilung der Themenmischung für jedes Dokument aus, in der Literatur oft als „Theta“ bezeichnet. Bei leeren Dokumenten wird ein Vektor von Nullen zurückgegeben. Die Schätzungen werden mittels variativer Approximation („Gamma„) abgeleitet. | NICHT FESTGELEGT | Beliebige Zeichenfolge |

{style="table-layout:auto"}

**Beispiel**

```sql
Create MODEL modelname OPTIONS(
  type = 'lda',
) AS
  select col1, col2, col3 from training-dataset
```

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie verschiedene Clustering-Algorithmen konfigurieren und verwenden können. Weitere Informationen zu anderen Typen erweiterter statistischer Modelle finden [ in den Dokumenten ](./classification.md)Klassifizierung und [Regression](./regression.md).
