---
keywords: Experience Platform;walkthrough;Data Science Workspace;popular topics
solution: Experience Platform
title: Anleitung für Data Science Workspace
topic: Walkthrough
description: Dieses Dokument bietet eine schrittweise Anleitung für Adobe Experience Platform Data Science Workspace. Speziell der allgemeine Arbeitsablauf, den ein Datenwissenschaftler durchlaufen würde, um ein Problem mit maschinellem Lernen zu lösen.
translation-type: tm+mt
source-git-commit: 0d76b14599bc6b6089f9c760ef6a6be3a19243d4
workflow-type: tm+mt
source-wordcount: '1708'
ht-degree: 33%

---


# [!DNL Data Science Workspace] exemplarische Vorgehensweise

This document provides a walkthrough for Adobe Experience Platform [!DNL Data Science Workspace]. In diesem Lernprogramm wird ein allgemeiner Arbeitsablauf für Datenwissenschaftler vorgestellt, in dem erläutert wird, wie sie mit maschinellem Lernen auf ein Problem zugehen und es lösen können.

## Voraussetzungen

- Ein registriertes Adobe ID-Konto
   - The Adobe ID account must have been added to an Organization with access to Adobe Experience Platform and [!DNL Data Science Workspace].

## Einzelhandelsanwendungsfall

Einem Einzelhändler hat Probleme damit, auf dem aktuellen Markt wettbewerbsfähig zu bleiben. Eines der Hauptanliegen des Einzelhändlers besteht darin, über die optimale Preisgestaltung eines Produkts zu entscheiden und die Verkaufsentwicklung vorherzusagen. Mit einem präzisen Prognosemodell wäre ein Einzelhändler in der Lage, das Verhältnis zwischen der Nachfrage- und der Preispolitik zu ermitteln und optimierte Preisentscheidungen zu treffen, um Verkäufe und Umsatz zu maximieren.

## Lösung des Datenwissenschaftlers

Die Lösung eines Datenwissenschaftlers besteht darin, die Fülle historischer Informationen eines Einzelhändlers zu nutzen, zukünftige Trends vorherzusagen und Preisentscheidungen zu optimieren. In dieser exemplarischen Vorgehensweise werden bisherige Verkaufsdaten verwendet, um ein Modell für maschinelles Lernen zu schulen und anhand des Modells künftige Verkaufstrends vorherzusagen. Damit können Sie Einblicke generieren, um optimale Preisänderungen vorzunehmen.

Diese Übersicht spiegelt die Schritte wider, die ein Datenwissenschaftler ausführen würde, um einen Datensatz zu erstellen und ein Modell zur Vorhersage der wöchentlichen Verkäufe zu erstellen. Dieses Tutorial behandelt die folgenden Abschnitte im Beispiel für Einzelhandelsverkäufe auf Adobe Experience Platform [!DNL Data Science Workspace]:

- [Einrichten](#setup)
- [Erkunden von Daten](#exploring-data)
- [Funktionsentwicklung](#feature-engineering)
- [Training und Validierung](#training-and-verification)

### Notebooks in [!DNL Data Science Workspace]

Wählen Sie in der Adobe Experience Platform-Benutzeroberfläche auf der Registerkarte &quot; **[!UICONTROL Datenwissenschaften]** &quot;die Option &quot; **[!UICONTROL Notebooks]** &quot;aus, um zur Übersichtsseite &quot; [!UICONTROL Notebooks] &quot;zu gelangen. Wählen Sie auf dieser Seite die [!DNL JupyterLab] Registerkarte aus, um Ihre [!DNL JupyterLab] Umgebung zu starten. Die standardmäßige Landingpage für [!DNL JupyterLab] ist der **[!UICONTROL Starter]**.

![](./images/walkthrough/notebooks.png)

![](./images/walkthrough/jupyterlab_launcher.png)

Dieses Lernprogramm verwendet [!DNL Python] 3 in, [!DNL JupyterLab Notebooks] um zu zeigen, wie Sie auf die Daten zugreifen und diese untersuchen. Auf der Starter-Seite stehen Ihnen Beispiel-Notebooks zur Verfügung. In den unten stehenden Beispielen wird das Beispielheft **[!UICONTROL für den Einzelhandel]** verwendet.

### Einrichten {#setup}

Wenn das Notebook für den Einzelhandel geöffnet ist, sollten Sie als Erstes die für Ihren Workflow erforderlichen Bibliotheken laden. In der folgenden Liste werden die einzelnen Bibliotheken beschrieben, die in den Beispielen in späteren Schritten verwendet werden.

- **numpy**: Wissenschaftsrechenbibliothek, die Unterstützung für große, multidimensionale Arrays und Matrizen bietet
- **Pandas**: Bibliothek, die Datenstrukturen und -vorgänge für die Datenverarbeitung und Analyse Angebot
- **matplotlib.pyplot**: Plotting-Bibliothek, die beim Plotten ein MATLAB-ähnliches Erlebnis bietet
- **seaborn** : Visualisierungsbibliothek für Daten auf hoher Ebene basierend auf matplotlib
- **sklearn**: Bibliothek für maschinelles Lernen mit Classification-, Regression-, Support Vektor- und Cluster-Algorithmen
- **Warnungen**: Bibliothek, die Warnmeldungen steuert

### Daten erkunden {#exploring-data}

#### Laden von Daten

Nachdem die Bibliotheken geladen wurden, können Sie den Beginn mit der Anzeige der Daten aufrufen. The following [!DNL Python] code uses pandas&#39; `DataFrame` data structure and the [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) function to read the CSV hosted on [!DNL Github] into the pandas DataFrame:

![](./images/walkthrough/read_csv.png)

Die DataFrame-Datenstruktur von pandas ist eine zweidimensionale beschriftete Datenstruktur. To quickly see the dimensions of your data, you can use `df.shape`. Dadurch wird ein Tupel zurückgegeben, das die Dimensionalität des DataFrame darstellt:

![](./images/walkthrough/df_shape.png)

Schließlich können Sie Vorschauen darüber vornehmen, wie Ihre Daten aussehen. You can use `df.head(n)` to view the first `n` rows of the DataFrame:

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

Damit können Sie sehen, dass für jedes Merkmal 6435 Instanzen vorhanden sind. Darüber hinaus werden statistische Daten wie Mittelwert, Standardabweichung (std), Minimum, Maximum und Interquartile angegeben. So erfahren wir mehr über die Abweichung der Daten. Im nächsten Abschnitt werden Sie über Visualisierung gehen, die mit diesen Informationen zusammenarbeitet, um uns ein vollständiges Verständnis Ihrer Daten zu geben.

Looking at the minimum and maximum values for `store`, you can see that there are 45 unique stores the data represents. Es gibt auch `storeTypes`, die unterscheiden, was ein Geschäft ist. you can see the distribution of `storeTypes` by doing the following:

![](./images/walkthrough/df_groupby.png)

Das bedeutet, dass 22 Geschäfte `storeType A`, 17 `storeType B` und 6 `storeType C` sind.

#### Daten visualisieren

Da Sie Ihre Datenrahmenwerte kennen, möchten Sie diese durch Visualisierungen ergänzen, um die Dinge klarer zu gestalten und Muster leichter zu identifizieren. Darüber hinaus sind diese Diagramme nützlich, wenn Ergebnisse an eine Zielgruppe übermittelt werden sollen.

#### Eindimensionale Diagramme

Eindimensionale Diagramme sind Diagramme mit einer einzelnen Variablen. Ein gängiges eindimensionales Diagramm, das zur Visualisierung Ihrer Daten dienen kann, sind Box- und Whisker-Diagramme.

Mithilfe Ihres Retail-Datensatzes von zuvor können Sie die Box und das Whisker-Diagramm für jeden der 45 Läden und deren Wochenverkäufe erstellen. Das Diagramm wird mithilfe der `seaborn.boxplot`-Funktion erstellt.

![](./images/walkthrough/box_whisker.png)

Ein Box- und Whisker-Diagramm dient dazu, die Verteilung von Daten anzuzeigen. Die äußeren Linien des Diagramms zeigen die oberen und unteren Quartile an, während der Kasten den Interquartilbereich umfasst. Die Linie im Kasten markiert den Median. Alle Datenpunkte, die mehr als das 1,5-Fache des oberen oder unteren Quartils betragen, werden als Kreis markiert. Diese Punkte werden als Ausreißer betrachtet.

Als Nächstes können Sie die wöchentlichen Verkäufe mit der Zeit grafisch darstellen. Sie zeigen nur die Ausgabe des ersten Stores an. Der Code im Notebook erzeugt 6 Diagramme, die 6 der 45 Geschäfte in unserem Datensatz entsprechen.

![](./images/walkthrough/weekly_sales.png)

Mit diesem Diagramm können Sie die wöchentlichen Verkäufe über einen Zeitraum von 2 Jahren vergleichen. Im Zeitverlauf lassen sich Umsatzspitzen und Talmuster leicht erkennen.

#### Mehrdimensionale Diagramme

Mehrdimensionale Diagramme dienen dazu, die Interaktion zwischen Variablen anzuzeigen. Dank der Visualisierung können Datenwissenschaftler erkennen, ob Korrelationen oder Muster zwischen den Variablen bestehen. Ein häufig verwendetes mehrdimensionales Diagramm ist eine Korrelationsmatrix. Bei einer Korrelationsmatrix werden Abhängigkeiten zwischen verschiedenen Variablen mit dem Korrelationskoeffizienten quantifiziert.

Mit demselben für den Handel bestimmten Datensatz können Sie die Korrelationsmatrix generieren.

![](./images/walkthrough/correlation_1.png)

Beachten Sie die Diagonale der Einsen in der Mitte. Das bedeutet, dass eine Variable beim Vergleich mit sich selbst eine vollständige positive Korrelation aufweist. Eine starke positive Korrelation wird näher bei 1 liegen, während eine schwache Korrelation näher bei 0 liegt. Negative Korrelation wird durch einen negativen Koeffizienten angezeigt, der auf einen gegenläufigen Trend hinweist.

### Funktionsentwicklung {#feature-engineering}

In diesem Abschnitt wird die Funktionstechnik verwendet, um Änderungen an Ihrem Retail-Datensatz vorzunehmen, indem die folgenden Vorgänge durchgeführt werden:

- Wochen- und Jahresspalten hinzufügen
- storeType in eine Indikatorvariable konvertieren
- isHoliday in eine numerische Variable konvertieren
- weeklySales der nächsten Woche vorhersagen

#### Wochen- und Jahresspalten hinzufügen

The current format for date (`2010-02-05`) can make it hard to differentiate that the data is for every week. Aus diesem Grund sollten Sie das Datum in Woche und Jahr konvertieren.

![](./images/walkthrough/date_to_week_year.png)

Nun sehen die Woche und das Datum wie folgt aus:

![](./images/walkthrough/date_week_year.png)

#### storeType in Indikatorvariable konvertieren

Next, you want to convert the storeType column to columns representing each `storeType`. There are 3 store types, (`A`, `B`, `C`), from which you are creating 3 new columns. The value set in each is a boolean value where a &#39;1&#39; is set depending on what the `storeType` was and `0` for the other 2 columns.

![](./images/walkthrough/storeType.png)

Die aktuelle `storeType` Spalte wird abgelegt.

#### isHoliday in numerischen Typ konvertieren

Die nächste Änderung besteht darin, den booleschen `isHoliday`-Wert in eine numerische Darstellung zu ändern.

![](./images/walkthrough/isHoliday.png)

#### weeklySales der nächsten Woche vorhersagen

Jetzt möchten Sie jedem Datensatz vorherigen und zukünftigen wöchentlichen Verkauf hinzufügen. Sie können dies tun, indem Sie Ihre `weeklySales`. Zusätzlich wird die `weeklySales` Differenz berechnet. Dazu wird `weeklySales` von `weeklySales` der Vorwoche abgezogen.

![](./images/walkthrough/weekly_past_future.png)

Since you are offsetting the `weeklySales` data 45 datasets forwards and 45 datasets backwards to create new columns, the first and last 45 data points have NaN values. You can remove these points from your dataset by using the `df.dropna()` function which removes all rows that have NaN values.

![](./images/walkthrough/dropna.png)

Eine Zusammenfassung des Datensatzes nach Ihren Änderungen wird unten angezeigt:

![](./images/walkthrough/df_info_new.png)

### Training und Validierung {#training-and-verification}

Nun ist es an der Zeit, verschiedene Datenmodelle zu erstellen und zu entscheiden, welches Modell sich zur Vorhersage künftiger Umsätze am besten eignet. Sie werden die folgenden 5 Algorithmen auswerten:

- Lineare Regression
- Entscheidungsbaum
- Random Forest
- Gradient Boosting
- Nächste Nachbarn

#### Datensatz in Untergruppen für Training und Tests aufteilen

Sie müssen wissen, wie genau Ihr Modell Werte vorhersagen kann. Diese Bewertung kann durchgeführt werden, indem ein Teil des Datensatzes als Validierungs- und der Rest als Trainings-Daten zugewiesen wird. Since `weeklySalesAhead` is the actual future values of `weeklySales`, you can use this to evaluate how accurate the model is at predicting the value. Die Aufteilung sehen Sie im Folgenden:

![](./images/walkthrough/split_data.png)

You now have `X_train` and `y_train` for preparing the models and `X_test` and `y_test` for evaluation later.

#### Stichprobenalgorithmen

In this section, you declare all the algorithms into an array called `model`. Next, you iterate through this array and for each algorithm, input your training data with `model.fit()` which creates a model `mdl`. Mit diesem Modell können Sie `weeklySalesAhead` mit Ihren `X_test` Daten vorhersagen.

![](./images/walkthrough/training_scoring.png)

For the scoring, you are taking the mean percentage difference between the predicted `weeklySalesAhead` with the actual values in the `y_test` data. Da Sie den Unterschied zwischen Ihrer Prognose und dem tatsächlichen Ergebnis minimieren möchten, ist der Regressor für die Verlaufsverstärkung das leistungsstärkste Modell.

#### Prognosen visualisieren

Schließlich stellen Sie sich Ihr Prognosemodell mit den tatsächlichen wöchentlichen Verkaufswerten vor. Die blaue Linie stellt die tatsächlichen Zahlen dar, während das Grün Ihre Prognose mit der Verlaufsverstärkung darstellt. Der folgende Code generiert 6 Plots, die 6 der 45 Stores in Ihrem Datensatz darstellen. Nur `Store 1` wird hier gezeigt:

![](./images/walkthrough/visualize_prediction.png)

## Nächste Schritte

In diesem Dokument wurde ein allgemeiner Arbeitsablauf für Datenwissenschaftler zur Lösung eines Einzelhandelsproblems behandelt. Zusammenfassung:

- Laden Sie die für Ihren Workflow erforderlichen Bibliotheken.
- Nach dem Laden der Bibliotheken können Sie die Daten mithilfe statistischer Zusammenfassungen, Visualisierungen und Diagramme im Beginn betrachten.
- Als Nächstes wird die Funktionstechnik verwendet, um Änderungen an Ihrem Retail-Datensatz vorzunehmen.
- Erstellen Sie schließlich Modelle der Daten und wählen Sie das Modell aus, das die beste Leistung für die Vorhersage künftiger Verkäufe bietet.

Sobald Sie bereit sind, erhalten Sie im [JupyterLab Benutzerhandbuch](./jupyterlab/overview.md) einen schnellen Überblick über Notebooks in Adobe Experience Platform Data Science Workspace. Außerdem, wenn Sie interessiert sind, über Modelle und Rezepte zu lernen, Beginn durch Lesen der [Einzelhandel Schema und Dataset](./models-recipes/create-retails-sales-dataset.md) Tutorial. Dieses Lernprogramm bereitet Sie auf nachfolgende Data Science Workspace-Tutorials vor, die Sie auf der [Seite](../tutorials/data-science-workspace.md)&quot;Data Science Workspace-Tutorials&quot;ansehen können.