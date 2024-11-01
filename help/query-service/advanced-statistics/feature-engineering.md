---
title: Feature Engineering SQL-Erweiterung
description: Erfahren Sie mehr über die SQL-Erweiterung der Data Distiller-Funktionen zur Vorverarbeitung von Daten für eine erweiterte statistische Modellierung. Sie umfasst die verfügbaren Techniken zur Extraktion, Transformation und Auswahl von Funktionen.
role: Developer
source-git-commit: 1fcfb5c41750e853daaf036ceaae3527b805391c
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 1%

---

# Funktionstechnische SQL-Erweiterung

>[!AVAILABILITY]
>
>Diese Funktion steht Kunden zur Verfügung, die das Data Distiller-Add-on erworben haben. Weitere Informationen erhalten Sie beim Adobe-Support.

Um Ihre Anforderungen an die Funktionsentwicklung zu erfüllen, verwenden Sie die SQL Transformer-Erweiterung, um die Vorverarbeitung Ihrer Daten zu vereinfachen und zu automatisieren. Verwenden Sie diese Erweiterung, um Funktionen zu erstellen und nahtlose Experimente mit verschiedenen Techniken der Funktionsentwicklung zu genießen, einschließlich der Zuordnung dieser Funktionen zu Modellen. Für dezentrales Computing konzipiert, können Sie Funktionen für große Datensätze parallel und skalierbar entwickeln und damit die für die Datenvorverarbeitung erforderliche Zeit mit der Data Distiller-Funktionstechnik-SQL-Erweiterung erheblich verkürzen.

## Technischer Überblick {#technique-overview}

Die Funktionen der Funktionsentwicklung decken drei Hauptbereiche ab: Funktionsextrahierung, Funktionsumwandlung und Funktionsauswahl. Jeder Bereich enthält spezifische Funktionen, die dazu bestimmt sind, Ihre Datenvorverarbeitung zu extrahieren, zu konvertieren, zu fokussieren und zu verbessern.

### Funktionsextraktion {#feature-extraction}

Extrahieren Sie relevante Informationen aus Ihren Daten, insbesondere Textdaten, und konvertieren Sie sie in ein numerisches Format, das von den unterstützten Modellen genutzt, umgewandelt und abgeleitet werden kann. Verwenden Sie die folgenden Funktionen, um die Funktionsextraktion durchzuführen:

- **[Texttransformator](./feature-transformation.md#textual-transformations)**: Konvertieren Sie Textdaten in numerische Funktionen.
- **[Zähler-Vectorizer](./feature-transformation.md#countvectorizer)**: Wandeln Sie eine Sammlung von Textdokumenten in Vektoren von Token-Zählungen um.
- **[N-Gramm](./feature-transformation.md#ngram)**: Generiert Sequenzen von n Gramm aus Textdaten.
- **[Behobene Wörter entfernen](./feature-transformation.md#stopwordsremover)**: Filtern Sie häufige Wörter heraus, die keine bedeutende Bedeutung haben.
- **[TF-IDF](./feature-transformation.md#tf-idf)**: Messen Sie die Bedeutung von Wörtern in einem Dokument in Bezug auf einen Korpus.
- **[Tokenizer](./feature-transformation.md#tokenizer)**: Unterteilen Sie Text in einzelne Begriffe (Wörter).
- **[Word2VEC](./feature-transformation.md#word2vec)**: Ordnen Sie Wörter zu Vektoren fester Größe zu und erstellen Sie Worteinbettungen.

### Merkmalumwandlung {#feature-transformation}

Verwenden Sie nicht nur Funktionen zum Extrahieren, sondern auch die folgenden allgemeinen Transformatoren, um Ihre Funktionen für erweiterte statistische Modelle und abgeleitete Datensätze vorzubereiten. Wenden Sie Skalierung, Normalisierung oder Kodierung an, um sicherzustellen, dass Ihre Funktionen auf derselben Skala und mit einer ähnlichen Verteilung vorliegen.

#### Allgemeine Transformatoren

Nachstehend finden Sie eine Liste von Tools zur Verarbeitung einer Vielzahl von Datentypen, mit denen Sie Ihren Datenvorverarbeitungs-Workflow verbessern können.

- **[Numerischer Rechner](./feature-transformation.md#numeric-imputer)**: Füllen Sie fehlende Werte in numerischen Spalten mit einer
- **[String Imputer](./feature-transformation.md#string-imputer)**: Ersetzen Sie fehlende Zeichenfolgenwerte durch einen angegebenen
- **[Vektor-Assembler](./feature-transformation.md#vector-assembler)**: Kombinieren Sie mehrere Spalten in einer einzelnen Vektorspalte.

#### Numerische Transformatoren

Wenden Sie diese Verfahren an, um numerische Daten effektiv zu verarbeiten und zu skalieren und so die Modellleistung zu verbessern.

- **[Binarizer](./feature-transformation.md#binarizer)**: Konvertieren Sie kontinuierliche Funktionen in binäre Werte basierend auf einem Schwellenwert.
- **[Bucketizer](./feature-transformation.md#bucketizer)**: Ordnen Sie kontinuierliche Funktionen in separaten Behältern zu.
- **[Min-Max-Skalierung](./feature-transformation.md#minmaxscaler)**: Skaliert Funktionen in einen bestimmten Bereich um, normalerweise [0, 1].
- **[Max Abs Scaler](./feature-transformation.md#maxabsscaler)**: Skaliert Funktionen in den Bereich [-1, 1] um, ohne die Sparsamkeit zu ändern.
- **[Normalizer](./feature-transformation.md#normalizer)**: Normalisieren Sie Vektoren so, dass sie die Standardeinheit aufweisen.
- **[Quantile Discretizer](./feature-transformation.md#quantilediscretizer)**: Konvertieren Sie kontinuierliche Funktionen in kategorische Merkmale, indem Sie sie in Quantile unterteilen.
- **[Standardskalierer](./feature-transformation.md#standardscaler)**: Normalisieren Sie Funktionen so, dass sie eine Standardabweichung und/oder einen Nullmittelwert aufweisen.

#### Kategorische Transformatoren

Verwenden Sie diese Transformatoren, um kategorische Daten in Formate zu konvertieren und zu kodieren, die für Modelle für maschinelles Lernen geeignet sind.

- **[String-Indexer](./feature-transformation.md#stringindexer)**: Konvertieren Sie kategorische Zeichenfolgendaten in numerische Indizes.
- **[Ein Hot Encoder](./feature-transformation.md#onehotencoder)**: Ordnen Sie kategorische Daten binären Vektoren zu.

### Funktionsauswahl {#feature-selection}

Anschließend konzentrieren Sie sich auf die Auswahl einer Untergruppe der wichtigsten Funktionen aus dem Originalsatz. Dieser Prozess trägt dazu bei, die Dimensionalität Ihrer Daten zu reduzieren, die Verarbeitung Ihrer Modelle zu vereinfachen und die Gesamtleistung des Modells zu verbessern.

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

## Umsetzung der OPTIONS-Klausel {#options-clause}

Wenn Sie Ihr Modell definieren, verwenden Sie die `OPTIONS`-Klausel, um den Algorithmus und seine Parameter anzugeben. Legen Sie zunächst den Parameter `type` fest, um den verwendeten Algorithmus anzugeben, z. B. `K-Means`. Definieren Sie dann die relevanten Parameter in der `OPTIONS`-Klausel als Schlüssel-Wert-Paare, um Ihr Modell zu optimieren. Beachten Sie, dass einige Parameter möglicherweise positioniert sind und dass alle vorangehenden Parameter angegeben werden müssen, wenn benutzerdefinierte Werte angegeben werden. Wenn Sie bestimmte Parameter nicht anpassen möchten, wendet das System die Standardeinstellungen an. Die Funktionen und Standardwerte der einzelnen Parameter finden Sie in der entsprechenden Dokumentation .

### Nächste Schritte

Nachdem Sie die in diesem Dokument beschriebenen Techniken der Funktionsentwicklung kennengelernt haben, wechseln Sie zum Dokument [Modelle](./models.md) . Sie führt Sie durch den Prozess der Erstellung, Schulung und Verwaltung vertrauenswürdiger Modelle mithilfe der von Ihnen entwickelten Funktionen. Nachdem Ihre Modelle erstellt wurden, fahren Sie mit dem Dokument [Erweiterte statistische Modelle implementieren fort.](./implement-models/implement-models.md). Dieses Dokument dient als Überblick und verlinkt zu ausführlichen Handbüchern für verschiedene Modellierungstechniken, einschließlich Clustering, Klassifizierung und Regression. In diesen Dokumenten erfahren Sie, wie Sie verschiedene vertrauenswürdige Modelle in Ihren SQL-Workflows konfigurieren und implementieren und Ihre Modelle für erweiterte Datenanalysen optimieren können.
