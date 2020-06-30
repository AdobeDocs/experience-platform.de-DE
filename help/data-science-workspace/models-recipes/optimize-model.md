---
keywords: Experience Platform;optimize;model;Data Science Workspace;popular topics
solution: Experience Platform
title: Optimieren eines Modells
topic: Tutorial
translation-type: tm+mt
source-git-commit: 4b0f0dda97f044590f55eaf75a220f631f3313ee
workflow-type: tm+mt
source-wordcount: '1219'
ht-degree: 0%

---


# Optimieren eines Modells mithilfe des Model Insights-Frameworks

Das Model Insights Framework bietet dem Datenwissenschaftler Werkzeuge, um schnelle und fundierte Entscheidungen für optimale Modelle des maschinellen Lernens auf der Grundlage von Experimenten [!DNL Data Science Workspace] zu treffen. Der Rahmen wird die Geschwindigkeit und Effektivität des Arbeitsablaufs für maschinelles Lernen verbessern und die Benutzerfreundlichkeit von Datenwissenschaftlern verbessern. Dies geschieht durch Bereitstellung einer Standardvorlage für jeden maschinellen Lernalgorithmustyp, um die Modellverfeinerung zu unterstützen. Das Endergebnis ermöglicht es Datenwissenschaftlern und Bürgerdatenwissenschaftlern, bessere Modelloptimierungsentscheidungen für ihre Endkunden zu treffen.

## Was sind Metriken?

Nach der Implementierung und Schulung eines Modells würde ein Datenwissenschaftler als nächsten Schritt herausfinden, wie gut das Modell funktionieren wird. Es werden verschiedene Metriken verwendet, um zu ermitteln, wie effektiv ein Modell im Vergleich zu anderen ist. Einige Beispiele für verwendete Metriken:
- Classification-Genauigkeit
- Fläche unter Kurve
- Verwechslungsmatrix
- Klassifizierungsbericht

## Konfigurieren des Rezeptcodes

Derzeit unterstützt das Model Insight Framework die folgenden Laufzeitumgebungen:
- [Scala](#scala)
- [!DNL Python/Tensorflow](#pythontensorflow)
- [R](#r)

Beispielcode für Rezepte finden Sie im [Erlebnis-Plattform-dsw-reference](https://github.com/adobe/experience-platform-dsw-reference) -Repository unter `recipes`. Bestimmte Dateien aus diesem Repository werden in diesem Lernprogramm referenziert.

### Scala {#scala}

Es gibt zwei Möglichkeiten, um den Rezepten Metriken hinzuzufügen. Eine besteht darin, die vom SDK bereitgestellten Standardbewertungsmetriken zu verwenden, die andere besteht darin, benutzerdefinierte Evaluierungsmetriken zu schreiben.

#### Standardauswertungsmetriken für Scala

Standardbewertungen werden als Teil der Classification-Algorithmen berechnet. Hier sind einige Standardwerte für aktuell implementierte Auswerter:

| Bewertungsklasse | `evaluation.class` |
--- | ---
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEvaluator | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

Der Auswerter kann im Rezept in der Datei [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) im `recipe` Ordner definiert werden. Beispiel-Code zur Aktivierung der `DefaultBinaryClassificationEvaluator` ist unten dargestellt:

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

Nachdem eine Bewertungsklasse aktiviert wurde, wird während der Schulung standardmäßig eine Reihe von Metriken berechnet. Standardmetriken können explizit deklariert werden, indem Sie die folgende Zeile zu Ihrer `application.properties`hinzufügen.

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE] Wenn die Metrik nicht definiert ist, sind die Standardmetriken aktiv.

Eine bestimmte Metrik kann aktiviert werden, indem Sie den Wert für ändern `evaluation.metrics.com`. Im folgenden Beispiel ist die F-Score-Metrik aktiviert.

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

In der folgenden Tabelle sind die Standardmetriken für jede Klasse aufgeführt. Ein Benutzer kann auch die Werte in der `evaluation.metric` Spalte verwenden, um eine bestimmte Metrik zu aktivieren.

| `evaluator.class` | Standardmetriken | `evaluation.metric` |
--- | --- | ---
| `DefaultBinaryClassificationEvaluator` | -Precision- <br>Recall- <br>Confusion Matrix <br>-F-Score- <br>-Accuracy- <br>Receiver-Bedienfeldmerkmale <br>- Bereich unter den Betriebsmerkmalen des Empfängers | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` | -Precision- <br>Recall- <br>Confusion Matrix <br>-F-Score- <br>-Accuracy- <br>Receiver-Bedienfeldmerkmale <br>- Bereich unter den Betriebsmerkmalen des Empfängers | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` | -Mittlere mittlere Genauigkeit (MAP) <br>-normalisierte diskontierte kumulierte Verstärkung <br>- mittlere reziproke <br>-Metrik K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Benutzerspezifische Bewertungsmetriken für Scala

Der benutzerdefinierte Auswerter kann bereitgestellt werden, indem Sie die Oberfläche `MLEvaluator.scala` in Ihrer `Evaluator.scala` Datei erweitern. In der Beispieldatei [Evaluator.scala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala) definieren wir benutzerdefinierte `split()` und `evaluate()` Funktionen. Unsere `split()` Funktion teilt unsere Daten zufällig mit einem Verhältnis von 8:2 auf und unsere `evaluate()` Funktion definiert und gibt 3 Metriken zurück: MAPE, MAE und RMSE.

>[!IMPORTANT] Verwenden Sie für die `MLMetric` Klasse nicht `"measures"` für `valueType` `MLMetric` die Erstellung einer neuen Metrik, da die Metrik sonst nicht in der Tabelle mit den benutzerspezifischen Bewertungsmetriken gefüllt wird.
>  
> Führen Sie folgende Schritte aus: `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> Nicht: `metrics.add(new MLMetric("MAPE", mape, "measures"))`


Nach der Definition im Rezept besteht der nächste Schritt darin, es in den Rezepten zu aktivieren. Dies erfolgt in der Datei [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) im `resources` Projektordner. Hier `evaluation.class` wird die `Evaluator` Klasse eingestellt, die in `Evaluator.scala`

```properties
evaluation.class=com.adobe.platform.ml.Evaluator
```

In der [!DNL Data Science Workspace]Tabelle können Benutzer die Einblicke auf der Registerkarte &quot;Bewertungsmetriken&quot;auf der Seite &quot;Experiment&quot;sehen.

### [!DNL Python/Tensorflow] {#pythontensorflow}

Derzeit gibt es keine standardmäßigen Evaluierungsmetriken für [!DNL Python] oder [!DNL Tensorflow]. Um die Bewertungsmetriken abzurufen, müssen Sie daher eine benutzerspezifische Bewertungsmetrik erstellen [!DNL Python] oder [!DNL Tensorflow]diese erstellen. Dies kann durch Implementierung der `Evaluator` Klasse erfolgen.

#### Benutzerspezifische Bewertungsmetriken für [!DNL Python]

Für benutzerdefinierte Bewertungsmetriken müssen zwei Hauptmethoden für den Auswerter implementiert werden: `split()` und `evaluate()`.

Beispielsweise [!DNL Python]würden diese Methoden in [evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) für die `Evaluator` Klasse definiert. Folgen Sie dem Link [evaluation.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) für ein Beispiel der `Evaluator`.

Zum Erstellen von Bewertungsmetriken in [!DNL Python] müssen der Benutzer die `evaluate()` und- `split()` Methoden implementieren.

Die `evaluate()` Methode gibt das metrische Objekt zurück, das ein Array von Metrikobjekten mit den Eigenschaften `name`, `value`und `valueType`enthält.

Der Zweck der `split()` Methode besteht darin, Daten einzugeben und eine Schulung und einen Testdatensatz auszugeben. In unserem Beispiel gibt die `split()` Methode Daten mit dem `DataSetReader` SDK ein und löscht dann die Daten, indem sie nicht verwandte Spalten entfernt. Von dort werden zusätzliche Funktionen aus den vorhandenen Rohdaten-Funktionen erstellt.

Die `split()` Methode sollte eine Schulung und einen Prüfdataframe zurückgeben, die dann von den Methoden zur Schulung und Prüfung des ML-Modells verwendet wird `pipeline()` .

#### Benutzerspezifische Bewertungsmetriken für Tensorflow

Beispielsweise [!DNL Tensorflow]müssen ähnlich wie [!DNL Python]die Methoden `evaluate()` und `split()` in der `Evaluator` Klasse implementiert werden. Die Metriken `evaluate()`sollten beispielsweise zurückgegeben werden, während der Zug- und der Testdatensatz zurückgegeben `split()` wird.

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

Derzeit gibt es keine standardmäßigen Evaluierungsmetriken für R. Um die Bewertungsmetriken für R abzurufen, müssen Sie die `applicationEvaluator` Klasse daher als Teil des Rezepts definieren.

#### Benutzerspezifische Bewertungsmetriken für R

Hauptzweck des `applicationEvaluator` Formulars ist es, ein JSON-Objekt zurückzugeben, das Schlüssel-Wert-Paare von Metriken enthält.

Dieses [applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) kann als Beispiel verwendet werden. In diesem Beispiel `applicationEvaluator` wird der in drei vertraute Abschnitte unterteilt:
- Daten laden
- Datenvorbereitung/Funktionstechnik
- Abrufen des gespeicherten Modells und Auswerten

Daten werden zunächst aus einer in [retail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json)definierten Quelle in einen Datensatz geladen. Von dort werden die Daten gereinigt und so entwickelt, dass sie dem maschinellen Lernmodell entsprechen. Schließlich wird das Modell verwendet, um mithilfe unseres Datensatzes eine Prognose zu erstellen, und aus den prognostizierten Werten und tatsächlichen Werten werden Metriken berechnet. In diesem Fall werden MAPE, MAE und RMSE definiert und im `metrics` Objekt zurückgegeben.

## Verwenden von vordefinierten Metriken und Visualisierungsdiagrammen

Die [!DNL Sensei Model Insights Framework] unterstützt eine Standardvorlage für jeden Typ des maschinellen Lernalgorithmus. Die folgende Tabelle zeigt allgemeine Klassen für maschinelle Lernalgorithmen auf hoher Ebene und zugehörige Bewertungsmetriken und Visualisierungen.

| ML Algorithmustyp | Bewertungsmetriken | Visualisierungen |
--- | --- | ---
| Regression | - RMSE<br>- MAPE<br>- MASE<br>- MAIL | Überlagerungskurve für prognostizierte und tatsächliche Werte |
| Binäre Klassifizierung | - Verwirrungsmatrix<br>- Präzisionsrückruf<br>- Genauigkeit<br>- F-Wert (spezifisch F1,F2)<br>- AUC<br>- ROC | ROC-Kurve und Verwechslungsmatrix |
| Mehrklassige Klassifizierung | -Verwechslungsmatrix <br>- Für jede Klasse: <br>- Genauigkeit beim Rückruf <br>- F-Wert (spezifisch F1, F2) | ROC-Kurve und Verwechslungsmatrix |
| Clustering (w/irdische Wahrheit) | - NMI (normalisiertes Ergebnis der gegenseitigen Information), AMI (angepasstes Ergebnis der gegenseitigen Information)<br>- RI (Rand Index), ARI (angepasster Rand-Index)<br>- Homogenitätsbewertung, Vollständigkeitsbewertung und V-Maß<br>- FMI (Fowlkes-Mallow-Index)<br>- Reinheit<br>- Jakard-Index | Cluster-Diagramm mit Clustern und Zentroiden mit relativen Cluster-Größen, die die Datenpunkte im Cluster widerspiegeln |
| Clustering (ohne Grundwahrheit) | - Trägheit<br>- Silhouettenkoeffizient<br>- CHI (Calinski-Harabaz-Index)<br>- DBI (Davies-Bouldin-Index)<br>- Dunn-Index | Cluster-Diagramm mit Clustern und Zentroiden mit relativen Cluster-Größen, die die Datenpunkte im Cluster widerspiegeln |
| Empfehlung | -Mittlere mittlere Genauigkeit (MAP) <br>-normalisierte diskontierte kumulierte Verstärkung <br>- mittlere reziproke <br>-Metrik K | TBD |
| Anwendungsfälle von TensorFlow | TensorFlow Model Analyse (TFMA) | Vergleich des neuronalen Netzwerkmodells/Visualisierung |
| Sonstige/Fehler-Erfassungsmechanismus | Benutzerdefinierte Metriklogik (und entsprechende Evaluierungstabellen), die vom Modellautor definiert wird. Sorgfältige Fehlerbearbeitung im Falle einer nicht übereinstimmenden Vorlage | Tabelle mit Schlüssel-Wert-Paaren für Bewertungsmetriken |
