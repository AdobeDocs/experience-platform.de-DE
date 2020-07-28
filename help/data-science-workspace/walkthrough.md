---
keywords: Experience Platform;walkthrough;Data Science Workspace;popular topics
solution: Experience Platform
title: Anleitung für Data Science Workspace
topic: Walkthrough
translation-type: tm+mt
source-git-commit: 1e5526b54f3c52b669f9f6a792eda0abfc711fdd
workflow-type: tm+mt
source-wordcount: '1638'
ht-degree: 91%

---


# [!DNL Data Science Workspace] exemplarische Vorgehensweise

This document provides a walkthrough for Adobe Experience Platform [!DNL Data Science Workspace]. Insbesondere werden wir uns den allgemeinen Workflow ansehen, den ein Datenwissenschaftler ausführen würde, um ein Problem mit maschinellem Lernen zu lösen.

## Voraussetzungen

- Ein registriertes Adobe ID-Konto
   - Das Adobe ID-Konto muss einer Organisation mit Zugriff auf Adobe Experience Platform und hinzugefügt worden sein.[!DNL Data Science Workspace]

## Motivation des Datenwissenschaftlers

Einem Einzelhändler hat Probleme damit, auf dem aktuellen Markt wettbewerbsfähig zu bleiben. Eines der Hauptanliegen des Einzelhändlers ist es, über die optimale Preisgestaltung seiner Produkte zu entscheiden und Verkaufs-Trends vorherzusagen. Mit einem präzisen Prognosemodell könnte der Einzelhändler das Verhältnis zwischen Nachfrage und Preispolitik ermitteln und optimierte Preisentscheidungen treffen, um Verkäufe und Umsätze zu optimieren.

## Lösung des Datenwissenschaftlers

Die Lösung des Datenwissenschaftlers besteht darin, die Menge historischer Daten zu nutzen, auf die ein Einzelhändler Zugriff hat, um zukünftige Trends vorherzusagen und Preisentscheidungen zu perfektionieren. Wir werden Daten von früheren Verkäufen nutzen, um unser maschinelles Lernmodell zu trainieren und das Modell für die Vorhersage künftiger Verkaufs-Trends zu verwenden. Dadurch kann der Einzelhändler Einblicke erhalten, die ihm beim Vornehmen von Preisänderungen helfen.

In diesem Überblick sehen wir uns die Schritte an, die ein Datenwissenschaftler ergreifen muss, um einen Datensatz zu nutzen und ein Modell zur Vorhersage der wöchentlichen Umsätze zu erstellen. We will go over the following sections in the Sample Retail Sales Notebook on Adobe Experience Platform [!DNL Data Science Workspace]:

- [Einrichten](#setup)
- [Erkunden von Daten](#exploring-data)
- [Funktionsentwicklung](#feature-engineering)
- [Training und Validierung](#training-and-verification)

### Notebooks in [!DNL Data Science Workspace]

Firstly, we want to create a [!DNL JupyterLab] notebook to open the &quot;Retail Sales&quot; sample notebook. Indem wir die Schritte befolgen, die der Datenwissenschaftler im Notebook vornimmt, werden wir verstehen, wie ein typischer Workflow aussieht.

In the Adobe Experience Platform UI, click on the Data Science tab in the top menu to take you to the [!DNL Data Science Workspace]. From this page, click on the [!DNL JupyterLab] tab which will open the [!DNL JupyterLab] launcher. Sie sollten eine Seite sehen, die der folgenden ähnelt.

![](./images/walkthrough/jupyterlab_launcher.png)

In our tutorial, we will be using [!DNL Python] 3 in the [!DNL Jupyter Notebook] to show how to access and explore the data. Auf der Starter-Seite stehen Ihnen Beispiel-Notebooks zur Verfügung. We will be using the &quot;Retail Sales&quot; sample for [!DNL Python] 3.

![](./images/walkthrough/retail_sales.png)

### Einrichten {#setup}

Mit dem geöffneten Notebook „Einzelhandelsumsätze“ laden wir zunächst die für unseren Workflow erforderlichen Bibliotheken. In der folgenden Liste wird kurz beschrieben, wofür die einzelnen Bibliotheken verwendet werden:
- **numpy** – Bibliothek für wissenschaftliche Berechnungen, die Unterstützung für große, multidimensionale Arrays und Matrizen bietet.
- **pandas** – Bibliothek, die Datenstrukturen und -vorgänge für die Bearbeitung und Analyse von Daten bietet.
- **matplotlib.pyplot** – Plotting-Bibliothek, die beim Zeichnen für ein MATLAB-ähnliches Erlebnis sorgt.
- **seaborn** – Bibliothek für die Datenvisualisierung mit übergeordneter Oberfläche auf Grundlage von matplotlib.
- **sklearn** – Bibliothek für maschinelles Lernen mit Klassifizierungs-, Regressions-, Support-Vektor- und Cluster-Algorithmen.
- **warnings** – Bibliothek, die Warnmeldungen steuert.

### Daten erkunden {#exploring-data}

#### Laden von Daten

Nachdem die Bibliotheken geladen wurden, können wir uns die Daten ansehen. The following [!DNL Python] code uses pandas&#39; `DataFrame` data structure and the [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) function to read the CSV hosted on [!DNL Github] into the pandas DataFrame:

![](./images/walkthrough/read_csv.png)

Die DataFrame-Datenstruktur von pandas ist eine zweidimensionale beschriftete Datenstruktur. Um die Dimensionen unserer Daten schnell anzuzeigen, können wir `df.shape` verwenden. Dadurch wird ein Tupel zurückgegeben, das die Dimensionalität des DataFrame darstellt:

![](./images/walkthrough/df_shape.png)

Schließlich können wir einen Blick darauf werfen, wie unsere Daten aussehen. Wir können `df.head(n)` nutzen, um die ersten `n` Zeilen des DataFrame anzuzeigen:

![](./images/walkthrough/df_head.png)

#### Statistische Zusammenfassung

We can leverage [!DNL Python's] pandas library to get the data type of each attribute. Die Ausgabe des folgenden Aufrufs liefert uns Informationen über die Anzahl der Einträge und den Datentyp für die einzelnen Spalten:

```PYTHON
df.info()
```

![](./images/walkthrough/df_info.png)

Diese Informationen sind hilfreich, da wir durch Kenntnis des Datentyps der einzelnen Spalten wissen, wie die Daten zu behandeln sind.

Sehen wir uns nun die statistische Zusammenfassung an. Nur die numerischen Datentypen werden angezeigt, sodass `date`, `storeType` und `isHoliday` nicht ausgegeben werden:

```PYTHON
df.describe()
```

![](./images/walkthrough/df_describe.png)

Damit können wir sehen, dass für jedes Merkmal 6.435 Instanzen vorhanden sind. Darüber hinaus werden statistische Daten wie Mittelwert, Standardabweichung (std), Minimum, Maximum und Interquartile angegeben. So erfahren wir mehr über die Abweichung der Daten. Im nächsten Abschnitt werden wir uns Visualisierung ansehen, die mit diesen Daten arbeitet, um uns eine genaue Übersicht über unsere Daten zu bieten.

Wenn wir uns die Mindest- und Maximalwerte für `store` ansehen, können wir feststellen, dass die Daten 45 verschiedene Geschäfte repräsentieren. Es gibt auch `storeTypes`, die unterscheiden, was ein Geschäft ist. Außerdem können wir die Verteilung von `storeTypes` anzeigen, indem wir Folgendes tun:

![](./images/walkthrough/df_groupby.png)

Das bedeutet, dass 22 Geschäfte `storeType A`, 17 `storeType B` und 6 `storeType C` sind.

#### Daten visualisieren

Da wir unsere Dataframe-Werte nun kennen, möchten wir sie um Visualisierungen ergänzen, damit sich Muster leichter erkennen lassen. Darüber hinaus sind diese Diagramme nützlich, wenn Ergebnisse an eine Zielgruppe übermittelt werden sollen.

#### Eindimensionale Diagramme

Eindimensionale Diagramme sind Diagramme mit einer einzelnen Variablen. Ein gängiges eindimensionales Diagramm, das zur Visualisierung Ihrer Daten dienen kann, sind Box- und Whisker-Diagramme.

Mit unserem Datensatz für Einzelhandelsumsätze von oben können wir ein Box- und Whisker-Diagramm für jedes der 45 Geschäfte und ihre wöchentlichen Umsätze generieren. Das Diagramm wird mithilfe der `seaborn.boxplot`-Funktion erstellt.

![](./images/walkthrough/box_whisker.png)

Ein Box- und Whisker-Diagramm dient dazu, die Verteilung von Daten anzuzeigen. Die äußeren Linien des Diagramms zeigen die oberen und unteren Quartile an, während der Kasten den Interquartilbereich umfasst. Die Linie im Kasten markiert den Median. Alle Datenpunkte, die mehr als das 1,5-Fache des oberen oder unteren Quartils betragen, werden als Kreis markiert. Diese Punkte werden als Ausreißer betrachtet.

Als Nächstes können wir die wöchentlichen Umsätze im Zeitverlauf zeichnen. Wir zeigen nur die Ausgabe des ersten Geschäfts. Der Code im Notebook erzeugt 6 Diagramme, die 6 der 45 Geschäfte in unserem Datensatz entsprechen.

![](./images/walkthrough/weekly_sales.png)

Mit diesem Diagramm können wir die wöchentlichen Umsätze über einen Zeitraum von 2 Jahren vergleichen. Im Zeitverlauf lassen sich Umsatzspitzen und Talmuster leicht erkennen.

#### Mehrdimensionale Diagramme

Mehrdimensionale Diagramme dienen dazu, die Interaktion zwischen Variablen anzuzeigen. Dank der Visualisierung können Datenwissenschaftler erkennen, ob Korrelationen oder Muster zwischen den Variablen bestehen. Ein häufig verwendetes mehrdimensionales Diagramm ist eine Korrelationsmatrix. Bei einer Korrelationsmatrix werden Abhängigkeiten zwischen verschiedenen Variablen mit dem Korrelationskoeffizienten quantifiziert.

Mit demselben Einzelhandelsdatensatz können wir die Korrelationsmatrix generieren.

![](./images/walkthrough/correlation_1.png)

Beachten Sie die Diagonale der Einsen in der Mitte. Das bedeutet, dass eine Variable beim Vergleich mit sich selbst eine vollständige positive Korrelation aufweist. Eine starke positive Korrelation wird näher bei 1 liegen, während eine schwache Korrelation näher bei 0 liegt. Negative Korrelation wird durch einen negativen Koeffizienten angezeigt, der auf einen gegenläufigen Trend hinweist.

### Funktionsentwicklung {#feature-engineering}

In diesem Abschnitt werden wir Änderungen an unserem Einzelhandelsdatensatz vornehmen. Wir führen die folgenden Vorgänge durch:

- Wochen- und Jahresspalten hinzufügen
- storeType in eine Indikatorvariable konvertieren
- isHoliday in eine numerische Variable konvertieren
- weeklySales der nächsten Woche vorhersagen

#### Wochen- und Jahresspalten hinzufügen

Mit dem aktuellen Datumsformat (`2010-02-05`) lässt sich kaum erkennen, dass die Daten für jede Woche gelten. Aus diesem Grund werden wir das Datum in Woche und Jahr umrechnen.

![](./images/walkthrough/date_to_week_year.png)

Nun sehen die Woche und das Datum wie folgt aus:

![](./images/walkthrough/date_week_year.png)

#### storeType in Indikatorvariable konvertieren

Als Nächstes konvertieren wir die Spalte „storeType“ in Spalten, die jeweils einen `storeType` darstellen. Es gibt 3 Geschäftstypen (`A`, `B`, `C`), aus denen wir 3 neue Spalten erstellen. Der jeweils festgelegte Wert ist ein boolescher Wert, bei dem je nach dem, was der Wert von `storeType` war, „1“ und `0` für die anderen beiden Spalten festgelegt wird.

![](./images/walkthrough/storeType.png)

Die aktuelle `storeType`-Spalte wird entfernt.

#### isHoliday in numerischen Typ konvertieren

Die nächste Änderung besteht darin, den booleschen `isHoliday`-Wert in eine numerische Darstellung zu ändern.

![](./images/walkthrough/isHoliday.png)


#### weeklySales der nächsten Woche vorhersagen

Nun möchten wir jedem unserer Datensätze vorherige und zukünftige Wochenumsätze hinzufügen. Das tun wir, indem wir unsere `weeklySales` versetzen. Außerdem berechnen wir die Differenz von `weeklySales`. Dazu wird `weeklySales` von `weeklySales` der Vorwoche abgezogen.

![](./images/walkthrough/weekly_past_future.png)

Da wir die `weeklySales`-Daten 45 Datensätze vorwärts und 45 Datensätze rückwärts versetzen, um neue Spalten zu erstellen, werden die ersten und letzten 45 Datenpunkte NaN-Werte aufweisen. Wir können diese Punkte aus unserem Datensatz entfernen, indem wir die `df.dropna()`-Funktion nutzen, die alle Zeilen mit NaN-Werten entfernt.

![](./images/walkthrough/dropna.png)

Eine Zusammenfassung des Datensatzes nach Vornahme unserer Änderungen finden Sie im Folgenden:

![](./images/walkthrough/df_info_new.png)

### Training und Validierung {#training-and-verification}

Nun ist es an der Zeit, verschiedene Datenmodelle zu erstellen und zu entscheiden, welches Modell sich zur Vorhersage künftiger Umsätze am besten eignet. Wir werden die folgenden fünf Algorithmen auswerten:

- Lineare Regression
- Entscheidungsbaum
- Random Forest
- Gradient Boosting
- Nächste Nachbarn

#### Datensatz in Untergruppen für Training und Tests aufteilen

Wir müssen ermitteln, wie genau unser Modell Werte vorhersagen kann. Diese Bewertung kann durchgeführt werden, indem ein Teil des Datensatzes als Validierungs- und der Rest als Trainings-Daten zugewiesen wird. Da `weeklySalesAhead` die tatsächlichen zukünftigen Werte von `weeklySales` beinhaltet, können wir damit bewerten, wie präzise das Modell bei der Vorhersage des Werts ist. Die Aufteilung sehen Sie im Folgenden:

![](./images/walkthrough/split_data.png)

Jetzt verfügen wir über `X_train` und `y_train` zur Vorbereitung der Modelle sowie über `X_test` und `y_test` zur späteren Auswertung.

#### Stichprobenalgorithmen

In diesem Abschnitt deklarieren wir alle Algorithmen in einem Array namens `model`. Als Nächstes durchlaufen wir dieses Array und geben mit `model.fit()`, das ein Modell `mdl` erstellt, unsere Trainings-Daten ein. Mithilfe dieses Modells werden wir `weeklySalesAhead` unter Verwendung unserer `X_test`-Daten vorhersagen.

![](./images/walkthrough/training_scoring.png)

Für die Bewertung nutzen wir die mittlere prozentuale Differenz zwischen den prognostizierten `weeklySalesAhead` und den tatsächlichen Werten in den `y_test`-Daten. Da wir die Differenz zwischen unserer Prognose und den tatsächlichen Werten minimieren wollen, ist Gradient Boosting Regressor das beste Modell.

#### Prognosen visualisieren

Schließlich visualisieren wir unser Prognosemodell mit den tatsächlichen wöchentlichen Umsatzwerten. Die blaue Linie stellt die tatsächlichen Zahlen dar, während Grün unsere Prognose unter Verwendung von Gradient Boosting darstellt. Der folgende Code generiert 6 Diagramme, die 6 der 45 Geschäfte in unserem Datensatz darstellen. Nur `Store 1` wird hier gezeigt:

![](./images/walkthrough/visualize_prediction.png)

<!--TODO UI Flow> -->

## Zusammenfassung

Mit dieser Übersicht haben wir uns den Workflow angesehen, den ein Datenwissenschaftler durchlaufen würde, um ein Problem mit Einzelhandelsumsätzen zu lösen. Im Einzelnen haben wir folgende Schritte betrachtet, um eine Lösung zu finden, die zukünftige Wochenumsätze vorhersagt.

- [Einrichten](#setup)
- [Erkunden von Daten](#exploring-data)
- [Funktionsentwicklung](#feature-engineering)
- [Training und Validierung](#training-and-verification)