---
keywords: Experience Platform;Optimieren;Modell;Datenwissenschaft Workspace;beliebte Themen;Modelleinblicke
solution: Experience Platform
title: Optimieren eines Modells mithilfe des Model Insights-Frameworks
type: Tutorial
description: Das Model Insights Framework stellt dem Datenwissenschaftler in Data Science Workspace Tools zur Verfügung, um schnelle und fundierte Entscheidungen für optimale Modelle für maschinelles Lernen auf der Grundlage von Experimenten zu treffen.
exl-id: f989a3f1-6322-47c6-b7d6-6a828766053f
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 78%

---

# Optimieren eines Modells mithilfe des Model Insights-Frameworks

>[!NOTE]
>
>Data Science Workspace ist nicht mehr erhältlich.
>
>Diese Dokumentation richtet sich an Bestandskunden mit vorherigen Berechtigungen für Data Science Workspace.

Das Modell-Insights-Framework bietet Datenwissenschaftlern Tools, [!DNL Data Science Workspace] schnelle und fundierte Entscheidungen für optimale Modelle für maschinelles Lernen auf der Grundlage von Experimenten zu treffen. Das Framework verbessert die Geschwindigkeit und Effektivität des Workflows für maschinelles Lernen und erhöht die Anwenderfreundlichkeit für Data Scientists. Dies geschieht durch Bereitstellung einer Standardvorlage für jeden maschinellen Lernalgorithmustyp, sodass sich Modelle verfeinern lassen. Das Endergebnis ermöglicht es Data Scientists und Citizen Data Scientists, bessere Entscheidungen zur Optimierung von Modellen ihrer Endkunden zu treffen.

## Was sind Metriken?

Nach dem Implementieren und Trainieren eines Modells würde ein Data Scientist als Nächstes ermitteln, wie gut das Modell funktionieren wird. Es werden verschiedene Metriken verwendet, um herauszufinden, wie gut ein Modell im Vergleich zu anderen abschneidet. Einige Beispiele für verwendete Metriken:

- Klassifizierungsgenauigkeit
- Fläche unter Kurve
- Konfusionsmatrix
- Klassifizierungsbericht

## Konfigurieren von Rezept-Code

Derzeit unterstützt das Model Insights Framework folgende Laufzeitumgebungen:

- [Scala](#scala)
- [Python/TensorFlow](#pythontensorflow)
- [R](#r)

Beispiel-Code für Rezepte finden Sie im Repository [experience-platform-dsw-reference](https://github.com/adobe/experience-platform-dsw-reference) unter `recipes`. Auf bestimmte Dateien aus diesem Repository wird in dieser Anleitung verwiesen.

### Scala {#scala}

Es gibt zwei Möglichkeiten, um den Rezepten Metriken hinzuzufügen. Eine besteht darin, die vom SDK bereitgestellten Standardbewertungsmetriken zu nutzen; die andere besteht darin, benutzerdefinierte Auswertungsmetriken zu schreiben.

#### Standardauswertungsmetriken für Scala

Standardauswertungen werden im Rahmen der Klassifizierungsalgorithmen berechnet. Hier finden Sie einige Standardwerte für Auswerter, die aktuell implementiert sind:

| Auswerterklasse | `evaluation.class` |
|--- | ---|
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEvaluator | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

Der Auswerter kann im Rezept in der Datei [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) im `recipe`-Ordner definiert werden. Beispiel-Code zur Aktivierung des Auswerters `DefaultBinaryClassificationEvaluator` ist unten dargestellt:

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

Nachdem eine Auswerterklasse aktiviert wurde, wird während des Trainierens standardmäßig eine Reihe von Metriken berechnet. Standardmetriken können explizit deklariert werden, indem Sie Ihren `application.properties` die folgende Zeile hinzufügen.

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE]
>
>Wenn die Metrik nicht definiert ist, sind die Standardmetriken aktiv.

Eine bestimmte Metrik kann aktiviert werden, indem Sie den Wert für `evaluation.metrics.com` ändern. Im folgenden Beispiel ist die F-Score-Metrik aktiviert.

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

In der folgenden Tabelle sind die Standardmetriken für jede Klasse aufgeführt. Ein Benutzer kann auch die Werte in der `evaluation.metric`-Spalte verwenden, um eine bestimmte Metrik zu aktivieren.

| `evaluator.class` | Standardmetriken | `evaluation.metric` |
| --- | --- | --- |
| `DefaultBinaryClassificationEvaluator` | -Precision <br>-Recall <br>-Confusion Matrix <br>-F-Score <br>-Accuracy <br>-Receiver Operating Characteristics <br>-Area Under the Receiver Operating Characteristics | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` | -Precision <br>-Recall <br>-Confusion Matrix <br>-F-Score <br>-Accuracy <br>-Receiver Operating Characteristics <br>-Area Under the Receiver Operating Characteristics | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` | -Mean Average Precision (MAP) <br>-Normalized Discounted Cumulative Gain <br>-Mean Reciprocal Rank <br>-Metric K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Benutzerdefinierte Auswertungsmetriken für Scala

Der benutzerdefinierte Auswerter kann angegeben werden, indem Sie die Oberfläche von `MLEvaluator.scala` in Ihrer `Evaluator.scala`-Datei erweitern. In der Beispieldatei [Evaluator.scala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala) definieren wir benutzerdefinierte `split()`- und `evaluate()`-Funktionen. Unsere `split()` teilt unsere Daten zufällig mit einem Verhältnis von 8 auf :2 und unsere `evaluate()` definiert und gibt 3 Metriken zurück: MAPE, MAE und RMSE.

>[!IMPORTANT]
>
>Verwenden Sie für die `MLMetric`-Klasse beim Erstellen eines neuen `"measures"` keine `valueType` für `MLMetric`, da die Metrik sonst nicht in die Tabelle mit benutzerdefinierten Auswertungsmetriken eingefügt wird.
>  
> Führen Sie folgende Schritte aus: `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> Und nicht: `metrics.add(new MLMetric("MAPE", mape, "measures"))`


Nach der Definition im Rezept besteht der nächste Schritt darin, sie in den Rezepten zu aktivieren. Dies erfolgt in der Datei [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) im Ordner `resources` des Projekts. Hier ist `evaluation.class` auf die `Evaluator`-Klasse eingestellt, die in `Evaluator.scala` definiert wurde.

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

In der [!DNL Data Science Workspace] können die Benutzenden die Einblicke auf der Registerkarte „Auswertungsmetriken“ auf der Experimentseite sehen.

### [!DNL Python/Tensorflow] {#pythontensorflow}

Derzeit gibt es keine standardmäßigen Auswertungsmetriken für [!DNL Python] oder [!DNL Tensorflow]. Um die Auswertungsmetriken für [!DNL Python] oder [!DNL Tensorflow] abzurufen, müssen Sie daher eine benutzerdefinierte Auswertungsmetrik erstellen. Dies kann durch Implementierung der `Evaluator`-Klasse erfolgen.

#### Benutzerdefinierte Auswertungsmetriken für [!DNL Python]

Für benutzerdefinierte Auswertungsmetriken müssen für den Auswerter zwei Hauptmethoden implementiert werden: `split()` und `evaluate()`.

[!DNL Python] würden diese Methoden in „evaluator.py[&#x200B; für &#x200B;](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) Klasse `Evaluator` definiert. Folgen Sie dem Link [evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py), um ein Beispiel für `Evaluator` zu sehen.

Um Auswertungsmetriken in [!DNL Python] zu erstellen, muss der Benutzer die `evaluate()`- und `split()` implementieren.

Die `evaluate()`-Methode gibt das metrische Objekt zurück, das eine Gruppe von Metrikobjekten mit den Eigenschaften `name`, `value` und `valueType` enthält.

Der Zweck der `split()`-Methode besteht darin, Daten einzugeben und ein Training sowie einen Testdatensatz auszugeben. In unserem Beispiel gibt die `split()`-Methode Daten mit dem `DataSetReader` SDK ein und löscht die Daten dann, indem nicht verwandte Spalten entfernt werden. Anschließend werden aus den vorhandenen Rohfunktionen zusätzliche Funktionen erstellt.

Die `split()`-Methode sollte einen Trainings- und Prüf-Dataframe zurückgeben, der dann von den `pipeline()`-Methoden zum Trainieren und Prüfen des ML-Modells verwendet wird.

#### Benutzerdefinierte Auswertungsmetriken für TensorFlow

[!DNL Tensorflow] müssen ähnlich wie [!DNL Python] die Methoden `evaluate()` und `split()` in der `Evaluator` implementiert werden. Für `evaluate()` sollten die Metriken zurückgegeben werden, während `split()` die Trainings- und Testdatensätze zurückgibt.

```PYTHON
from ml.runtime.python.Interfaces.AbstractEvaluator import AbstractEvaluator

class Evaluator(AbstractEvaluator):
    def __init__(self):
       print ("initiate")

    def evaluate(self, data=[], model={}, config={}):

        return metrics

    def split(self, config={}):

       return 'train', 'test'
```

### R {#r}

Derzeit gibt es keine standardmäßigen Auswertungsmetriken für R. Um Auswertungsmetriken für R zu erhalten, müssen Sie daher die `applicationEvaluator`-Klasse als Teil des Rezepts definieren.

#### Benutzerdefinierte Auswertungsmetriken für R

Hauptaufgabe des `applicationEvaluator` ist es, ein JSON-Objekt zurückzugeben, das Schlüssel-Wert-Paare von Metriken enthält.

Dieser [applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) kann als Beispiel verwendet werden. In diesem Beispiel wird der `applicationEvaluator` in drei vertraute Abschnitte unterteilt:

- Laden von Daten
- Datenvorbereitung/Funktionsentwicklung
- Abrufen des gespeicherten Modells und Auswerten

Daten werden zunächst aus einer in [retail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json) definierten Quelle in einen Datensatz geladen. Dort werden die Daten bereinigt und so bearbeitet, dass sie dem maschinellen Lernmodell entsprechen. Schließlich wird das Modell verwendet, um mithilfe unseres Datensatzes eine Prognose zu erstellen; aus den prognostizierten und tatsächlichen Werten werden dann Metriken berechnet. In diesem Fall werden MAPE, MAE und RMSE definiert und im `metrics`-Objekt zurückgegeben.

## Verwenden von vordefinierten Metriken und Visualisierungsdiagrammen

Der [!DNL Sensei Model Insights Framework] unterstützt eine Standardvorlage für jeden Typ von maschinellem Lernalgorithmus. Die folgende Tabelle beinhaltet allgemeine übergeordnete Klassen für maschinelle Lernalgorithmen und zugehörige Auswertungsmetriken und Visualisierungen.

| ML-Algorithmustyp | Auswertungsmetriken | Visualisierungen |
| --- | --- | --- |
| Regression | - RMSE<br>- MAPE<br>- MASE<br>- MAE | Überlagerungskurve für prognostizierte vs. tatsächliche Werte |
| Binäre Klassifizierung | - Confusion Matrix<br>- Precision-Recall<br>- Accuracy<br>- F-Score (spezifisch F1 ,F2)<br>- AUC<br>- ROC | ROC-Kurve und Konfusionsmatrix |
| Mehrklassige Klassifizierung | - Confusion Matrix <br>- Für jede Klasse: <br>- Precision-Recall Accuracy <br>- F-Score (spezifisch F1, F2) | ROC-Kurve und Konfusionsmatrix |
| Clustering (mit Ground Truth) | - NMI (Normalized Mutual Information-Wert), AMI (Adjusted Mutual Information-Wert)<br>- RI (Rand Index), ARI (Adjusted Rand Index)<br>- Homogenitätswert, Vollständigkeitswert und V-Wert<br>- FMI (Fowlkes-Mallows Index)<br>- Purity<br>- Jaccard Index | Cluster-Diagramm für Cluster und Zentroide mit relativen Cluster-Größen, die die Datenpunkte im Cluster widerspiegeln |
| Clustering (ohne Ground Truth) | - Inertia<br>- Silhouette Coefficient<br>- CHI (Calinski-Harabaz Index)<br>- DBI (Davies-Bouldin Index)<br>- Dunn Index | Cluster-Diagramm für Cluster und Zentroide mit relativen Cluster-Größen, die die Datenpunkte im Cluster widerspiegeln |
| Empfehlung | - Mean Average Precision (MAP) <br>- Normalized Discounted Cumulative Gain <br>- Mean Reciprocal Rank <br>- Metric K | TBD |
| Anwendungsbeispiele für TensorFlow | TensorFlow Model Analysis (TFMA) | Vergleich/Visualisierung des neuronalen Netzwerkmodells mit DeepCompare |
| Sonstige/Fehlererfassungsmechanismus | Benutzerdefinierte Metriklogik (und entsprechende Auswertungstabellen), vom Modellautor definiert. Ordnungsgemäße Fehlerbehandlung im Falle einer nicht übereinstimmenden Vorlage | Tabelle mit Schlüssel-Wert-Paaren für Auswertungsmetriken |
