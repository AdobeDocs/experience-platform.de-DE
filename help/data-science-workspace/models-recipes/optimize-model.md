---
keywords: Experience Platform; optimieren; Modell; Data Science Workspace; beliebte Themen; Modelleinblicke
solution: Experience Platform
title: Modell mithilfe des Model Insights Framework optimieren
topic-legacy: tutorial
type: Tutorial
description: Das Model Insights Framework bietet Data Scientists Werkzeuge in Data Science Workspace, um auf der Grundlage von Experimenten schnelle und fundierte Entscheidungen für optimale maschinelle Lernmodelle zu treffen.
exl-id: f989a3f1-6322-47c6-b7d6-6a828766053f
source-git-commit: d3e1bc9bc075117dcc96c85b8b9c81d6ee617d29
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 88%

---

# Modell mithilfe des Model Insights-Frameworks optimieren

Das Model Insights Framework stellt den Datenwissenschaftlern Tools in [!DNL Data Science Workspace] um schnelle und fundierte Entscheidungen für optimale Modelle des maschinellen Lernens auf der Grundlage von Experimenten zu treffen. Das Framework verbessert die Geschwindigkeit und Effektivität des Workflows für maschinelles Lernen und erhöht die Anwenderfreundlichkeit für Data Scientists. Dies geschieht durch Bereitstellung einer Standardvorlage für jeden maschinellen Lernalgorithmustyp, sodass sich Modelle verfeinern lassen. Das Endergebnis ermöglicht es Data Scientists und Citizen Data Scientists, bessere Entscheidungen zur Optimierung von Modellen ihrer Endkunden zu treffen.

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
| `DefaultMultiClassificationEvaluator` | -Precision <br>-Recall <br>-Verwirrungsmatrix <br>-F-Score <br>-Genauigkeit <br>-Bedienungsmerkmale des Receivers <br>-Bereich unter den Betriebseigenschaften des Receivers | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` | -Mean Average Precision (MAP) <br>-Normalized Discounted Cumulative Gain <br>-Mean Reciprocal Rank <br>-Metric K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Benutzerdefinierte Auswertungsmetriken für Scala

Der benutzerdefinierte Auswerter kann angegeben werden, indem Sie die Oberfläche von `MLEvaluator.scala` in Ihrer `Evaluator.scala`-Datei erweitern. In der Beispieldatei [Evaluator.scala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala) definieren wir benutzerdefinierte `split()`- und `evaluate()`-Funktionen. Die `split()`-Funktion teilt unsere Daten im Verhältnis von 8:2 zufällig auf; die `evaluate()`-Funktion definiert und gibt drei Metriken zurück: MAPE, MAE und RMSE.

>[!IMPORTANT]
>
>Verwenden Sie bei der `MLMetric`-Klasse nicht `"measures"` als `valueType`, wenn Sie eine neue `MLMetric` erstellen, da diese Metrik sonst nicht in die Tabelle mit den benutzerdefinierten Auswertungsmetriken aufgenommen wird.
>  
> Führen Sie folgende Schritte aus: `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> Und nicht: `metrics.add(new MLMetric("MAPE", mape, "measures"))`


Nach der Definition im Rezept besteht der nächste Schritt darin, sie in den Rezepten zu aktivieren. Dies erfolgt in der Datei [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) im Ordner `resources` des Projekts. Hier ist `evaluation.class` auf die `Evaluator`-Klasse eingestellt, die in `Evaluator.scala` definiert wurde.

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

Im [!DNL Data Science Workspace]festgelegt ist, kann der Benutzer die Einblicke auf der Registerkarte &quot;Auswertungsmetriken&quot;auf der Experimentseite sehen.

### [!DNL Python/Tensorflow] {#pythontensorflow}

Derzeit gibt es keine standardmäßigen Auswertungsmetriken für [!DNL Python] oder [!DNL Tensorflow]. So erhalten Sie die Auswertungsmetriken für [!DNL Python] oder [!DNL Tensorflow]müssen Sie eine benutzerdefinierte Auswertungsmetrik erstellen. Dies kann durch Implementierung der `Evaluator`-Klasse erfolgen.

#### Benutzerdefinierte Auswertungsmetriken für [!DNL Python]

Für benutzerdefinierte Auswertungsmetriken müssen für den Auswerter zwei Hauptmethoden implementiert werden: `split()` und `evaluate()`.

Für [!DNL Python]festlegen, würden diese Methoden in [evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) für `Evaluator` -Klasse. Folgen Sie dem Link [evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py), um ein Beispiel für `Evaluator` zu sehen.

Erstellen von Auswertungsmetriken in [!DNL Python] erfordert, dass der Benutzer die `evaluate()` und `split()` -Methoden.

Die `evaluate()`-Methode gibt das metrische Objekt zurück, das eine Gruppe von Metrikobjekten mit den Eigenschaften `name`, `value` und `valueType` enthält.

Der Zweck der `split()`-Methode besteht darin, Daten einzugeben und ein Training sowie einen Testdatensatz auszugeben. In unserem Beispiel gibt die `split()`-Methode Daten mit dem `DataSetReader` SDK ein und löscht die Daten dann, indem nicht verwandte Spalten entfernt werden. Anschließend werden aus den vorhandenen Rohfunktionen zusätzliche Funktionen erstellt.

Die `split()`-Methode sollte einen Trainings- und Prüf-Dataframe zurückgeben, der dann von den `pipeline()`-Methoden zum Trainieren und Prüfen des ML-Modells verwendet wird.

#### Benutzerdefinierte Auswertungsmetriken für TensorFlow

Für [!DNL Tensorflow], ähnlich wie [!DNL Python], die Methoden `evaluate()` und `split()` im `Evaluator` -Klasse implementiert werden. Für `evaluate()` sollten die Metriken zurückgegeben werden, während `split()` die Trainings- und Testdatensätze zurückgibt.

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

Die [!DNL Sensei Model Insights Framework] unterstützt eine Standardvorlage für jeden Typ von maschinellem Lernalgorithmus. Die folgende Tabelle beinhaltet allgemeine übergeordnete Klassen für maschinelle Lernalgorithmen und zugehörige Auswertungsmetriken und Visualisierungen.

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
