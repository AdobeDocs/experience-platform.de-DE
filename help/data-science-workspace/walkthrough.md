---
keywords: Experience Platform; exemplarische Vorgehensweise; Data Science Workspace; beliebte Themen
solution: Experience Platform
title: Anleitung zum Data Science Workspace
topic-legacy: Walkthrough
description: Dieses Dokument bietet eine schrittweise Anleitung für Adobe Experience Platform Data Science Workspace. Insbesondere der allgemeine Workflow, den ein Datenwissenschaftler durchführt, um ein Problem mithilfe des maschinellen Lernens zu lösen.
exl-id: d814846e-52a9-46c6-831a-3399241959f2
source-git-commit: 7d98340e7949aadc744513415c4fc7469efd2403
workflow-type: tm+mt
source-wordcount: '1695'
ht-degree: 33%

---

# [!DNL Data Science Workspace] exemplarische Vorgehensweise

Dieses Dokument bietet eine exemplarische Vorgehensweise für Adobe Experience Platform [!DNL Data Science Workspace]. In diesem Tutorial wird ein allgemeiner Arbeitsablauf für Datenwissenschaftler vorgestellt, in dem erläutert wird, wie diese ein Problem mithilfe von maschinellem Lernen angehen und lösen können.

## Voraussetzungen

- Ein registriertes Adobe ID-Konto
   - Das Adobe ID-Konto muss einer Organisation mit Zugriff auf Adobe Experience Platform und [!DNL Data Science Workspace] hinzugefügt worden sein.

## Anwendungsfall: Einzelhandel

Einem Einzelhändler hat Probleme damit, auf dem aktuellen Markt wettbewerbsfähig zu bleiben. Eines der Hauptanliegen des Einzelhändlers besteht darin, über die optimale Preisgestaltung eines Produkts zu entscheiden und Verkaufstrends vorherzusagen. Mit einem präzisen Prognosemodell wäre ein Einzelhändler in der Lage, das Verhältnis zwischen Nachfrage und Preispolitik zu ermitteln und optimierte Preisentscheidungen zu treffen, um Verkäufe und Umsatz zu maximieren.

## Lösung des Datenwissenschaftlers

Die Lösung eines Datenwissenschaftlers besteht darin, den Reichtum historischer Informationen eines Einzelhändlers zu nutzen, zukünftige Trends vorherzusagen und Preisentscheidungen zu optimieren. Diese exemplarische Vorgehensweise verwendet vergangene Verkaufsdaten, um ein Modell für maschinelles Lernen zu trainieren und mithilfe des Modells zukünftige Verkaufstrends vorherzusagen. Damit können Sie Einblicke generieren, um optimale Preisänderungen vorzunehmen.

Diese Übersicht spiegelt die Schritte wider, die ein Datenwissenschaftler ausführen würde, um einen Datensatz zu erstellen und ein Modell zur Vorhersage der wöchentlichen Umsätze zu erstellen. Dieses Tutorial behandelt die folgenden Abschnitte im Beispiel-Notebook für Einzelhandelsumsätze in Adobe Experience Platform [!DNL Data Science Workspace]:

- [Einrichten](#setup)
- [Erkunden von Daten](#exploring-data)
- [Funktionsentwicklung](#feature-engineering)
- [Training und Validierung](#training-and-verification)

### Notebooks in [!DNL Data Science Workspace]

Wählen Sie in der Adobe Experience Platform-Benutzeroberfläche **[!UICONTROL Notebooks]** auf der Registerkarte **[!UICONTROL Datenwissenschaft]** aus, um zur Übersichtsseite [!UICONTROL Notebooks] zu gelangen. Wählen Sie auf dieser Seite die Registerkarte [!DNL JupyterLab] aus, um Ihre [!DNL JupyterLab]-Umgebung zu starten. Die Standard-Landingpage für [!DNL JupyterLab] ist **[!UICONTROL Launcher]**.

![](./images/walkthrough/notebooks.png)

![](./images/walkthrough/jupyterlab_launcher.png)

In diesem Tutorial wird [!DNL Python] 3 in [!DNL JupyterLab Notebooks] verwendet, um zu zeigen, wie Sie auf die Daten zugreifen und sie analysieren können. Auf der Starter-Seite stehen Ihnen Beispiel-Notebooks zur Verfügung. Das Beispiel-Notebook **[!UICONTROL Einzelhandelsumsätze]** wird in den unten aufgeführten Beispielen verwendet.

### Einrichten {#setup}

Wenn das Notebook &quot;Einzelhandelsumsätze&quot;geöffnet ist, sollten Sie zunächst die für Ihren Workflow erforderlichen Bibliotheken laden. Die folgende Liste enthält eine kurze Beschreibung für jede der Bibliotheken, die in den Beispielen in späteren Schritten verwendet werden.

- **numpy**: Bibliothek für wissenschaftliche Berechnungen, die Unterstützung für große, multidimensionale Arrays und Matrizen bietet
- **pandas**: Bibliothek, die Datenstrukturen und -vorgänge für die Datenbearbeitung und -analyse anbietet
- **matplotlib.pyplot**: Plotting-Bibliothek, die beim Zeichnen ein MATLAB-ähnliches Erlebnis bietet
- **seaborn** : Visualisierungsbibliothek für Daten auf hoher Ebene basierend auf matplotlib
- **sklearn**: Bibliothek für maschinelles Lernen mit Classification-, Regressions-, Support-Vektor- und Cluster-Algorithmen
- **Warnungen**: Bibliothek, die Warnmeldungen steuert

### Daten erkunden {#exploring-data}

#### Laden von Daten

Nachdem die Bibliotheken geladen wurden, können Sie mit der Suche nach den Daten beginnen. Der folgende [!DNL Python]-Code verwendet die `DataFrame`-Datenstruktur von pandas und die [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv)-Funktion, um die auf [!DNL Github] gehostete CSV-Datei in den pandas-DataFrame zu lesen:

![](./images/walkthrough/read_csv.png)

Die DataFrame-Datenstruktur von pandas ist eine zweidimensionale beschriftete Datenstruktur. Um die Dimensionen Ihrer Daten schnell anzuzeigen, können Sie `df.shape` verwenden. Dadurch wird ein Tupel zurückgegeben, das die Dimensionalität des DataFrame darstellt:

![](./images/walkthrough/df_shape.png)

Schließlich können Sie eine Vorschau Ihrer Daten anzeigen. Sie können `df.head(n)` verwenden, um die ersten `n` Zeilen des DataFrame anzuzeigen:

![](./images/walkthrough/df_head.png)

#### Statistische Zusammenfassung

Wir können die pandas-Bibliothek [!DNL Python's] nutzen, um den Datentyp jedes Attributs zu erhalten. Die Ausgabe des folgenden Aufrufs liefert uns Informationen über die Anzahl der Einträge und den Datentyp für die einzelnen Spalten:

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

Damit können Sie sehen, dass für jedes Merkmal 6435 Instanzen vorhanden sind. Darüber hinaus werden statistische Daten wie Mittelwert, Standardabweichung (std), Minimum, Maximum und Interquartile angegeben. So erfahren wir mehr über die Abweichung der Daten. Im nächsten Abschnitt werden Sie die Visualisierung betrachten, die mit diesen Informationen zusammenarbeitet, um uns ein vollständiges Verständnis Ihrer Daten zu ermöglichen.

Wenn Sie sich die Mindest- und Höchstwerte für `store` ansehen, können Sie feststellen, dass die Daten 45 verschiedene Stores repräsentieren. Es gibt auch `storeTypes`, die unterscheiden, was ein Geschäft ist. Sie können die Verteilung von `storeTypes` sehen, indem Sie Folgendes tun:

![](./images/walkthrough/df_groupby.png)

Das bedeutet, dass 22 Geschäfte `storeType A`, 17 `storeType B` und 6 `storeType C` sind.

#### Daten visualisieren

Da Sie Ihre Datenrahmenwerte jetzt kennen, möchten Sie diese durch Visualisierungen ergänzen, um Muster leichter erkennen zu können. Darüber hinaus sind diese Diagramme nützlich, wenn Ergebnisse an eine Zielgruppe übermittelt werden sollen.

#### Eindimensionale Diagramme

Eindimensionale Diagramme sind Diagramme mit einer einzelnen Variablen. Ein gängiges eindimensionales Diagramm, das zur Visualisierung Ihrer Daten dienen kann, sind Box- und Whisker-Diagramme.

Mithilfe Ihres Retail-Datensatzes von zuvor können Sie das Box- und Whisker-Diagramm für jeden der 45 Stores und deren wöchentlichen Umsatz generieren. Das Diagramm wird mithilfe der `seaborn.boxplot`-Funktion erstellt.

![](./images/walkthrough/box_whisker.png)

Ein Box- und Whisker-Diagramm dient dazu, die Verteilung von Daten anzuzeigen. Die äußeren Linien des Diagramms zeigen die oberen und unteren Quartile an, während der Kasten den Interquartilbereich umfasst. Die Linie im Kasten markiert den Median. Alle Datenpunkte, die mehr als das 1,5-Fache des oberen oder unteren Quartils betragen, werden als Kreis markiert. Diese Punkte werden als Ausreißer betrachtet.

Als Nächstes können Sie die wöchentlichen Umsätze mit der Zeit zeichnen. Sie zeigen nur die Ausgabe des ersten Stores an. Der Code im Notebook erzeugt 6 Diagramme, die 6 der 45 Geschäfte in unserem Datensatz entsprechen.

![](./images/walkthrough/weekly_sales.png)

Mit diesem Diagramm können Sie die wöchentlichen Umsätze über einen Zeitraum von 2 Jahren vergleichen. Im Zeitverlauf lassen sich Umsatzspitzen und Talmuster leicht erkennen.

#### Mehrdimensionale Diagramme

Mehrdimensionale Diagramme dienen dazu, die Interaktion zwischen Variablen anzuzeigen. Dank der Visualisierung können Datenwissenschaftler erkennen, ob Korrelationen oder Muster zwischen den Variablen bestehen. Ein häufig verwendetes mehrdimensionales Diagramm ist eine Korrelationsmatrix. Bei einer Korrelationsmatrix werden Abhängigkeiten zwischen verschiedenen Variablen mit dem Korrelationskoeffizienten quantifiziert.

Mit demselben Einzelhandelsdatensatz können Sie die Korrelationsmatrix generieren.

![](./images/walkthrough/correlation_1.png)

Beachten Sie die Diagonale der Einsen in der Mitte. Das bedeutet, dass eine Variable beim Vergleich mit sich selbst eine vollständige positive Korrelation aufweist. Eine starke positive Korrelation wird näher bei 1 liegen, während eine schwache Korrelation näher bei 0 liegt. Negative Korrelation wird durch einen negativen Koeffizienten angezeigt, der auf einen gegenläufigen Trend hinweist.

### Funktionsentwicklung {#feature-engineering}

In diesem Abschnitt wird die Funktions-Engineering verwendet, um Änderungen an Ihrem Einzelhandelsdatensatz vorzunehmen, indem Sie die folgenden Vorgänge durchführen:

- Wochen- und Jahresspalten hinzufügen
- storeType in eine Indikatorvariable konvertieren
- isHoliday in eine numerische Variable konvertieren
- weeklySales der nächsten Woche vorhersagen

#### Wochen- und Jahresspalten hinzufügen

Das aktuelle Datumsformat (`2010-02-05`) kann es schwierig machen, zu erkennen, dass die Daten für jede Woche gelten. Aus diesem Grund sollten Sie das Datum in Woche und Jahr konvertieren.

![](./images/walkthrough/date_to_week_year.png)

Nun sehen die Woche und das Datum wie folgt aus:

![](./images/walkthrough/date_week_year.png)

#### storeType in Indikatorvariable konvertieren

Als Nächstes konvertieren Sie die Spalte storeType in Spalten, die jeweils `storeType` darstellen. Es gibt 3 Storetypen (`A`, `B`, `C`), aus denen Sie 3 neue Spalten erstellen. Der jeweils festgelegte Wert ist ein boolescher Wert, bei dem je nach dem, was `storeType` war, eine &quot;1&quot;und eine `0` für die anderen beiden Spalten festgelegt wird.

![](./images/walkthrough/storeType.png)

Die aktuelle Spalte `storeType` wird entfernt.

#### isHoliday in numerischen Typ konvertieren

Die nächste Änderung besteht darin, den booleschen `isHoliday`-Wert in eine numerische Darstellung zu ändern.

![](./images/walkthrough/isHoliday.png)

#### weeklySales der nächsten Woche vorhersagen

Jetzt möchten Sie jedem Ihrer Datensätze vorherige und zukünftige Wochenumsätze hinzufügen. Sie können dies tun, indem Sie Ihre `weeklySales` versetzen. Außerdem wird die Differenz `weeklySales` berechnet. Dazu wird `weeklySales` von `weeklySales` der Vorwoche abgezogen.

![](./images/walkthrough/weekly_past_future.png)

Da Sie die `weeklySales` -Daten 45 Datensätze vorwärts und 45 Datensätze rückwärts versetzen, um neue Spalten zu erstellen, haben die ersten und letzten 45 Datenpunkte NaN -Werte. Sie können diese Punkte aus Ihrem Datensatz entfernen, indem Sie die Funktion `df.dropna()` verwenden, die alle Zeilen mit NaN-Werten entfernt.

![](./images/walkthrough/dropna.png)

Eine Zusammenfassung des Datensatzes nach Ihren Änderungen finden Sie unten:

![](./images/walkthrough/df_info_new.png)

### Training und Validierung {#training-and-verification}

Nun ist es an der Zeit, verschiedene Datenmodelle zu erstellen und zu entscheiden, welches Modell sich zur Vorhersage künftiger Umsätze am besten eignet. Sie werden die fünf folgenden Algorithmen auswerten:

- Lineare Regression
- Entscheidungsbaum
- Random Forest
- Gradient Boosting
- Nächste Nachbarn

#### Datensatz in Untergruppen für Training und Tests aufteilen

Sie müssen wissen, wie genau Ihr Modell Werte vorhersagen kann. Diese Bewertung kann durchgeführt werden, indem ein Teil des Datensatzes als Validierungs- und der Rest als Trainings-Daten zugewiesen wird. Da `weeklySalesAhead` die tatsächlichen zukünftigen Werte von `weeklySales` ist, können Sie damit bewerten, wie genau das Modell bei der Vorhersage des Werts ist. Die Aufteilung sehen Sie im Folgenden:

![](./images/walkthrough/split_data.png)

Sie verfügen nun über `X_train` und `y_train` zum Vorbereiten der Modelle und `X_test` und `y_test` zum späteren Evaluieren.

#### Stichprobenalgorithmen

In diesem Abschnitt deklarieren Sie alle Algorithmen in einem Array namens `model`. Als Nächstes durchlaufen Sie dieses Array und geben Ihre Trainings-Daten für jeden Algorithmus mit `model.fit()` ein, wodurch ein Modell `mdl` erstellt wird. Mithilfe dieses Modells können Sie `weeklySalesAhead` mit Ihren `X_test` -Daten vorhersagen.

![](./images/walkthrough/training_scoring.png)

Für die Auswertung verwenden Sie die mittlere prozentuale Differenz zwischen den prognostizierten `weeklySalesAhead` und den tatsächlichen Werten in den `y_test` -Daten. Da Sie den Unterschied zwischen Ihrer Prognose und dem tatsächlichen Ergebnis minimieren möchten, ist Gradient Boosting Regressor das Modell mit der besten Performance.

#### Prognosen visualisieren

Schließlich visualisieren Sie Ihr Prognosemodell mit den tatsächlichen wöchentlichen Umsatzwerten. Die blaue Linie stellt die tatsächlichen Zahlen dar, während die grüne die Prognose mit Gradient Boosting darstellt. Der folgende Code generiert 6 Diagramme, die 6 der 45 Stores in Ihrem Datensatz darstellen. Nur `Store 1` wird hier gezeigt:

![](./images/walkthrough/visualize_prediction.png)

## Nächste Schritte

In diesem Dokument wurde ein allgemeiner Arbeitsablauf für Datenwissenschaftler zur Lösung eines Einzelhandelsproblems behandelt. Zusammenfassung:

- Laden Sie die für Ihren Workflow erforderlichen Bibliotheken.
- Nachdem die Bibliotheken geladen wurden, können Sie die Daten mithilfe statistischer Zusammenfassungen, Visualisierungen und Diagramme betrachten.
- Anschließend wird die Funktions-Engineering verwendet, um Änderungen an Ihrem Einzelhandelsdatensatz vorzunehmen.
- Erstellen Sie abschließend Modelle der Daten und wählen Sie das Modell aus, das für die Vorhersage künftiger Umsätze am besten geeignet ist.

Wenn Sie fertig sind, lesen Sie zunächst das [JupyterLab-Benutzerhandbuch](./jupyterlab/overview.md), um einen schnellen Überblick über Notebooks in Adobe Experience Platform Data Science Workspace zu erhalten. Wenn Sie außerdem mehr über Modelle und Rezepte erfahren möchten, lesen Sie zunächst das Tutorial [Einzelhandelsschema und -datensatz](./models-recipes/create-retails-sales-dataset.md) .
