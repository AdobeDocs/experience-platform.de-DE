---
title: SQL-Erweiterung für Feature Engineering
description: Erfahren Sie mehr über die SQL-Erweiterung Data Distiller Feature Engineering zur Vorverarbeitung von Daten für die erweiterte statistische Modellierung. Es behandelt die verfügbaren Techniken zur Extraktion, Transformation und Auswahl von Funktionen.
role: Developer
exl-id: 622c8ef3-9651-46b3-ad22-021a93190149
source-git-commit: e7bc30c153f67c59e9c04e8c8df60394f48871d0
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 1%

---

# SQL-Erweiterung für Feature Engineering

>[!AVAILABILITY]
>
>Diese Funktion steht Kunden zur Verfügung, die das Add-on Data Distiller erworben haben. Weitere Informationen erhalten Sie bei Ihrer bzw. Ihrem Adobe-Support-Mitarbeitenden.

Verwenden Sie die SQL Transformer-Erweiterung, um die Vorverarbeitung Ihrer Daten zu vereinfachen und zu automatisieren, um Ihre Funktionsanforderungen zu erfüllen. Verwenden Sie diese Erweiterung, um Funktionen zu erstellen und nahtlose Experimente mit verschiedenen Techniken der Funktionstechnik zu genießen, einschließlich der Verknüpfung mit Modellen. Das für verteilte Datenverarbeitung entwickelte Feature Engineering kann für große Datensätze parallel und skalierbar durchgeführt werden, wodurch die für die Datenvorverarbeitung erforderliche Zeit mit der SQL-Erweiterung Data Distiller Feature Engineering erheblich verkürzt wird.

## Übersicht über die Technik {#technique-overview}

Die Funktionen des Feature Engineering decken drei Hauptbereiche ab: Feature Extraction, Feature Transformation und Feature Selection. Jeder Bereich beinhaltet spezielle Funktionen, die entwickelt wurden, um Ihre Datenvorverarbeitung zu extrahieren, zu konvertieren, zu fokussieren und zu verbessern.

### Funktionsextraktion {#feature-extraction}

Extrahieren Sie relevante Informationen aus Ihren -Daten, insbesondere Textdaten, und konvertieren Sie sie in ein numerisches Format, das die unterstützten Modelle nutzen oder transformieren und Datensätze ableiten können. Verwenden Sie die folgenden Funktionen, um die Funktionsextraktion durchzuführen:

- **[Texttransformator](./feature-transformation.md#textual-transformations)**: Konvertiert Textdaten in numerische Funktionen.
- **[Count Vectorizer](./feature-transformation.md#countvectorizer)**: Wandelt eine Sammlung von Textdokumenten in Vektoren der Token-Anzahl um.
- **[N-Gramm](./feature-transformation.md#ngram)**: Generieren von N-Gramm-Sequenzen aus Textdaten.
- **[Stoppwörter entfernen](./feature-transformation.md#stopwordsremover)**: Filtern Sie häufig verwendete Wörter heraus, die keine signifikante Bedeutung haben.
- **[TF-IDF](./feature-transformation.md#tf-idf)**: Messen der Bedeutung von Wörtern in einem Dokument in Bezug auf ein Korpus.
- **[Tokenizer](./feature-transformation.md#tokenizer)**: Schlüsselt Text in einzelne Begriffe (Wörter) auf.
- **[Word2Vec](./feature-transformation.md#word2vec)**: Ordnen Sie Wörter Vektoren fester Größe zu und erstellen Sie Worteinbettungen.

### Funktionstransformation {#feature-transformation}

Verwenden Sie neben dem Extrahieren von Funktionen die folgenden allgemeinen Transformatoren, um Ihre Funktionen für erweiterte statistische Modelle und abgeleitete Datensätze vorzubereiten. Wenden Sie Skalierung, Normalisierung oder Kodierung an, um sicherzustellen, dass sich Ihre Funktionen auf derselben Skalierung befinden und eine ähnliche Verteilung haben.

#### Allgemeine Transformatoren

Nachfolgend finden Sie eine Liste von Tools zur Verarbeitung einer Vielzahl von Datentypen zur Verbesserung Ihres Workflows für die Datenvorverarbeitung.

- **[Numerischer Computer](./feature-transformation.md#numeric-imputer)**: Füllen Sie fehlende Werte in numerischen Spalten mit einem angegebenen Wert, z. B. dem Mittelwert oder Median.
- **[Zeichenfolgencomputer](./feature-transformation.md#string-imputer)**: Ersetzen Sie fehlende Zeichenfolgenwerte durch einen angegebenen Wert, z. B. die häufigste Zeichenfolge in der Spalte.
- **[Vektor-Assembler](./feature-transformation.md#vector-assembler)**: Kombinieren Sie mehrere Spalten in einer einzelnen Vektorspalte, um Daten für Modelle für maschinelles Lernen vorzubereiten.
- **[Boolescher Computer](./feature-transformation.md#boolean-imputer)**: Füllen Sie fehlende boolesche Werte mit einem angegebenen Wert, z. B. `true` oder `false`.

#### Numerische Transformatoren

Wenden Sie diese Techniken an, um numerische Daten effektiv zu verarbeiten und zu skalieren und so die Modellleistung zu verbessern.

- **[Binarizer](./feature-transformation.md#binarizer)**: Konvertiert fortlaufende Funktionen in Binärwerte basierend auf einem Schwellenwert.
- **[Bucketizer](./feature-transformation.md#bucketizer)**: Ordnen Sie kontinuierliche Funktionen in diskreten Buckets zu.
- **[Min-Max Scaler](./feature-transformation.md#minmaxscaler)**: Skalieren Sie die Funktionen auf einen bestimmten Bereich, normalerweise [0, 1].
- **[Max Abs Scaler](./feature-transformation.md#maxabsscaler)**: Skalieren Sie die Funktionen auf den Bereich [-1, 1] ohne die Sparsity zu verändern.
- **[Normalizer](./feature-transformation.md#normalizer)**: Normalisieren Sie Vektoren, um eine Einheitsnorm zu erhalten.
- **[Quantile Discretizer](./feature-transformation.md#quantilediscretizer)**: Wandelt kontinuierliche Funktionen in kategoriale Funktionen um, indem sie in Quantile klassifiziert werden.
- **[Standardskalierer](./feature-transformation.md#standardscaler)**: Normalisieren Sie Funktionen so, dass sie eine Standardabweichung von der Einheit und/oder einen Nullmittelwert aufweisen.

#### Kategorietransformatoren

Verwenden Sie diese Transformatoren, um kategoriale Daten in Formate zu konvertieren und zu kodieren, die für Modelle für maschinelles Lernen geeignet sind.

- **[String-Indexer](./feature-transformation.md#stringindexer)**: Konvertiert kategoriale Zeichenfolgendaten in numerische Indizes.
- **[One Hot Encoder](./feature-transformation.md#onehotencoder)**: Kategoriale Daten in binäre Vektoren zuordnen.

### Funktionsauswahl {#feature-selection}

Als Nächstes konzentrieren Sie sich auf die Auswahl einer Teilmenge der wichtigsten Funktionen aus dem ursprünglichen Satz. Dieser Prozess trägt dazu bei, die Dimensionalität Ihrer Daten zu reduzieren, wodurch die Verarbeitung Ihrer Modelle erleichtert und die Gesamtleistung des Modells verbessert wird.

<!-- Commented out as it 
## Supported machine learning algorithms {#supported-ml-algorithms}

Once you have preprocessed your data, use the feature engineering SQL extension to prepare your data for the following machine learning algorithms:

### Classification and regression {#classification-regression}

Use logical regression to predict categorical outcomes and linear regression to predict continuous values.

- **Logical Regression**: Use this for binary classification tasks.
- **Linear Regression**: Apply this algorithm for predicting continuous values.

### Clustering {#clustering}

Use a clustering algorithm to group data points into distinct clusters based on their similarities.

- **[`K-Means`](./feature-transformation.md#kmeans)**: Use `K-Means` for unsupervised learning tasks to partition data into a specified number of clusters, with each data point assigned to the cluster with the nearest mean. -->

## Implementierung der OPTIONS-Klausel {#options-clause}

Verwenden Sie beim Definieren des Modells die `OPTIONS`-Klausel, um den Algorithmus und seine Parameter anzugeben. Legen Sie zunächst den `type` fest, um den verwendeten Algorithmus anzugeben, z. B. `K-Means`. Definieren Sie dann die relevanten Parameter in der `OPTIONS`-Klausel als Schlüssel-Wert-Paare, um Ihr Modell fein abzustimmen. Wenn Sie bestimmte Parameter nicht anpassen möchten, wendet das System die Standardeinstellungen an. Informationen zur Funktion und zu den Standardwerten der einzelnen Parameter finden Sie in der entsprechenden Dokumentation .

### Nächste Schritte

Nachdem Sie die in diesem Dokument beschriebenen Techniken zum Erstellen von Funktionen gelernt haben, fahren Sie mit dem Dokument [Modelle](./models.md) fort. Es führt Sie durch den Prozess der Erstellung, Schulung und Verwaltung vertrauenswürdiger Modelle mit den von Ihnen entwickelten Funktionen. Fahren Sie nach der Erstellung der Modelle mit dem Dokument [Implementieren erweiterter statistischer Modelle“ fort.](./implement-models/implement-models.md). Dieses Dokument dient als Übersicht und verweist auf ausführliche Anleitungen für verschiedene Modellierungstechniken, einschließlich Clustering, Klassifizierung und Regression. In diesen Dokumenten erfahren Sie, wie Sie verschiedene vertrauenswürdige Modelle in Ihren SQL-Workflows konfigurieren und implementieren und Ihre Modelle für die erweiterte Datenanalyse optimieren können.
