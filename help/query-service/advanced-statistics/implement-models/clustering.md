---
title: Clustering-Algorithmen
description: Erfahren Sie, wie Sie verschiedene Clustering-Algorithmen mit Schlüsselparametern, Beschreibungen und Beispielcode konfigurieren und optimieren können, um Ihnen bei der Implementierung erweiterter statistischer Modelle zu helfen.
role: Developer
source-git-commit: 4ee7ce2468c1ea5f0960349c288d406f43a8bb91
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 4%

---

# Clustering-Algorithmen {#clustering-algorithms}

Durch das Clustering von Algorithmen werden Datenpunkte basierend auf ihren Ähnlichkeiten in separate Cluster gruppiert, sodass unbeaufsichtigtes Lernen Muster in den Daten erkennen kann. Verwenden Sie zum Erstellen eines Clustering-Algorithmus den Parameter `type` in der `OPTIONS`-Klausel, um den Algorithmus anzugeben, den Sie für die Modellschulung verwenden möchten. Definieren Sie anschließend die relevanten Parameter als Schlüssel-Wert-Paare, um das Modell zu optimieren.

>[!NOTE]
>
>Stellen Sie sicher, dass Sie die Parameteranforderungen für den ausgewählten Algorithmus verstehen. Einige Parameter können positionell sein und erfordern die Angabe aller vorangehenden Parameter, wenn benutzerdefinierte Werte angegeben werden. Wenn Sie bestimmte Parameter nicht anpassen möchten, wendet das System die Standardeinstellungen an. Lesen Sie die entsprechende Dokumentation , um die Funktionen und Standardwerte der einzelnen Parameter zu verstehen.

## [!DNL K-Means] {#kmeans}

`K-Means` ist ein Clustering-Algorithmus, der Datenpunkte in eine vordefinierte Anzahl von Clustern (k) partitioniert. Es ist einer der am häufigsten verwendeten Algorithmen für Clustering aufgrund seiner Einfachheit und Effizienz.

**Parameter**

Bei Verwendung von `K-Means` können die folgenden Parameter in der `OPTIONS` -Klausel festgelegt werden:

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|---------------------|---------------------------------------------------------------------------------------------------------------|-----------------|----------------------------------|
| `MAX_ITERATIONS` | Die Anzahl der Iterationen, die der Algorithmus ausführen soll. | `20` | (>= 0) |
| `TOL` | Die Konvergenztoleranz. | `0.0001` | (>= 0) |
| `NUM_CLUSTERS` | Die Anzahl der zu erstellenden Cluster (`k`). | `2` | (>1) |
| `DISTANCE_TYPE` | Der Algorithmus zur Berechnung des Abstands zwischen zwei Punkten. | `euclidean` | `euclidean`, `cosine` |
| `KMEANS_INIT_METHOD` | Der Initialisierungsalgorithmus für den Cluster zentriert. | `k-means` | `random`, `k-means` |
| `INIT_STEPS` | Die Anzahl der Schritte für den Initialisierungsmodus `k-means`. | `2` | (>0) |
| `PREDICTION_COL` | Der Name der Spalte, in der Prognosen gespeichert werden. | `prediction` | Beliebige Zeichenfolge |
| `SEED` | Ein zufälliger Test zur Reproduzierbarkeit. | `-1689246527` | Beliebige 64-Bit-Zahl |
| `WEIGHT_COL` | Der Name der Spalte, die für die Instanzgewichtung verwendet wird. Wenn nicht festgelegt, werden alle Instanzen gleichmäßig gewichtet. | `not set` | K. A. |

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

[!DNL Bisecting K-means] ist ein hierarchischer Clustering-Algorithmus, der einen teilweisen (oder &quot;Top-Down&quot;-) Ansatz verwendet. Alle Beobachtungen beginnen in einem einzigen Cluster und werden während der Erstellung der Hierarchie rekursiv aufgeteilt. [!DNL Bisecting K-means] kann oft schneller sein als normale K-Mittel, liefert aber normalerweise unterschiedliche Clusterergebnisse.

**Parameter**

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------------|
| `MAX_ITER` | Die maximale Anzahl von Iterationen, die der Algorithmus ausführt. | 20 | (>= 0) |
| `WEIGHT_COL` | Der Spaltenname für die Instanzgewichtung. Wenn nicht festgelegt oder leer, werden alle Instanzgewichte als `1.0` behandelt. | NICHT GESETZT | Beliebige Zeichenfolge |
| `NUM_CLUSTERS` | Die gewünschte Anzahl von Blattclustern. Die tatsächliche Zahl könnte kleiner sein, wenn keine teilbaren Cluster verbleiben. | 4 | (> 1) |
| `SEED` | Der Zufallsstichtest, der zur Steuerung zufälliger Prozesse im Algorithmus verwendet wird. | NICHT GESETZT | Beliebige 64-Bit-Zahl |
| `DISTANCE_MEASURE` | Die zur Berechnung der Ähnlichkeit zwischen Punkten verwendete Abstandsgröße. | &quot;euclidean&quot; | `euclidean`, `cosine` |
| `MIN_DIVISIBLE_CLUSTER_SIZE` | Die Mindestanzahl von Punkten (wenn >= 1,0) oder der Mindestprozentsatz der Punkte (wenn &lt; 1,0), die für einen Cluster erforderlich sind, um teilbar zu sein. | 1,0 | (>= 0) |
| `PREDICTION_COL` | Der Spaltenname für die Ausgabe der Prognose. | &quot;prediction&quot; | Beliebige Zeichenfolge |

{style="table-layout:auto"}

**Beispiel**

```sql
Create MODEL modelname OPTIONS(
  type = 'bisecting_kmeans',
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Gaussian Mixture Model] {#gaussian-mixture-model}

[!DNL Gaussian Mixture Model] steht für eine zusammengesetzte Verteilung, bei der Datenpunkte aus einer der k gaussischen Unterverteilungen gezogen werden, von denen jede eine eigene Wahrscheinlichkeit hat. Sie wird verwendet, um Datensätze zu modellieren, von denen angenommen wird, dass sie aus einer Mischung mehrerer gaussischer Distributionen generiert werden.

**Parameter**

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------|
| `MAX_ITER` | Die maximale Anzahl der Iterationen, die der Algorithmus ausführen soll. | 100 | (>= 0) |
| `WEIGHT_COL` | Der Spaltenname, z. B. die Gewichtung. Wenn nicht festgelegt oder leer, werden alle Instanzgewichte als `1.0` behandelt. | NICHT GESETZT | Beliebige Zeichenfolge |
| `NUM_CLUSTERS` | Die Anzahl der unabhängigen gaussischen Distributionen im Mischmodell. | 2 | (> 1) |
| `SEED` | Der zufällige Test, der zur Kontrolle zufälliger Prozesse im Algorithmus verwendet wird. | NICHT GESETZT | Beliebige 64-Bit-Zahl |
| `AGGREGATION_DEPTH` | Die während der Berechnung für die Aggregation verwendete Tiefe. | 2 | (>= 1) |
| `PROBABILITY_COL` | Der Spaltenname für prognostizierte bedingte Klassenwahrscheinlichkeiten. Diese sollten als Konfidenzwerte und nicht als exakte Wahrscheinlichkeiten behandelt werden. | &quot;wahrscheinlichkeit&quot; | Beliebige Zeichenfolge |
| `TOL` | Die Konvergenztoleranz für iterative Algorithmen. | 0,01 | (>= 0) |
| `PREDICTION_COL` | Der Spaltenname für die Ausgabe der Prognose. | &quot;prediction&quot; | Beliebige Zeichenfolge |

{style="table-layout:auto"}

**Beispiel**

```sql
Create MODEL modelname OPTIONS(
  type = 'gaussian_mixture',
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Latent Dirichlet Allocation] (LDA) {#latent-dirichlet-allocation}

[!DNL Latent Dirichlet Allocation] (LDA) ist ein probabilistisches Modell, das die zugrunde liegende Themenstruktur aus einer Sammlung von Dokumenten erfasst. Es handelt sich um ein hierarchisches Bayes-Modell mit Wort-, Thema- und Dokumentebenen auf drei Ebenen. LDA verwendet diese Ebenen zusammen mit den beobachteten Dokumenten, um eine latente Themenstruktur zu erstellen.

**Parameter**

| Parameter | Beschreibung | Standardwert | Mögliche Werte |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------|
| `MAX_ITER` | Die maximale Anzahl von Iterationen, die der Algorithmus ausführt. | 20 | (>= 0) |
| `OPTIMIZER` | Der Optimierer- oder Inferenzalgorithmus, der zur Schätzung des LDA-Modells verwendet wird. Unterstützte Optionen sind `"online"` (Online Variational Bayes) und `"em"` (Erwartungsmaximierung). | &quot;online&quot; | `online`, `em` |
| `NUM_CLUSTERS` | Die Anzahl der zu erstellenden Cluster (k). | 10 | (> 1) |
| `CHECKPOINT_INTERVAL` | Gibt an, wie oft die zwischengespeicherten Knoten-IDs überprüft werden. | 10 | (>= 1) |
| `DOC_CONCENTRATION` | Konzentrationsparameter (&quot;alpha&quot;) für die zuvor auf die Verteilung der Dokumente über Themen platzierten Elemente. Steuert die Regularisierung (Ausgleichung). | Automatisch | Jeder einzelne Wert oder Vektor der Länge k |
| `KEEP_LAST_CHECKPOINT` | Gibt an, ob der letzte Checkpoint bei Verwendung des `em`-Optimierers beibehalten werden soll. | `true` | `true`, `false` |
| `LEARNING_DECAY` | Lernrate für den `online`-Optimierer, festgelegt als exponentielle Abfallrate zwischen `(0.5, 1.0]`. | 0,51 | `(0.5, 1.0]` |
| `LEARNING_OFFSET` | Ein Lernparameter für den `online` -Optimierer, der die Gewichtung früherer Iterationen herabsetzt, um die Anzahl früherer Iterationen zu verringern. | 1024 | (> 0) |
| `SEED` | Zufällige Suche zur Steuerung zufälliger Prozesse im Algorithmus. | NICHT GESETZT | Beliebige 64-Bit-Zahl |
| `OPTIMIZE_DOC_CONCENTRATION` | Für den `online` -Optimierer: ob der `docConcentration` (Dirichlet-Parameter für die Verteilung von Dokumentthemen) während des Trainings optimiert werden soll. | `false` | `true`, `false` |
| `SUBSAMPLING_RATE` | Für den Optimierer `online`: der Anteil des Korpus, der in jeder Iteration des Mini-Batch-Farbverlaufs im Bereich `(0, 1]` entnommen und verwendet wird. | 0,05 | `(0, 1]` |
| `TOPIC_CONCENTRATION` | Konzentrationsparameter (&quot;Beta&quot;oder &quot;Beta&quot;) für die zuvor auf die Verteilung der Themen über Bedingungen platzierten Elemente. | Automatisch | (>= 0) |
| `TOPIC_DISTRIBUTION_COL` | Ausgabespalte mit Schätzungen der Themenmischung Verteilung für jedes Dokument. | NICHT GESETZT | Beliebige Zeichenfolge |

{style="table-layout:auto"}

**Beispiel**

```sql
Create MODEL modelname OPTIONS(
  type = 'lda',
) AS
  select col1, col2, col3 from training-dataset
```

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie verschiedene Clustering-Algorithmen konfigurieren und verwenden können. Weitere Informationen zu anderen Typen erweiterter statistischer Modelle finden Sie in den Dokumenten zu [Klassifizierung](./classification.md) und [Regression](./regression.md) .
