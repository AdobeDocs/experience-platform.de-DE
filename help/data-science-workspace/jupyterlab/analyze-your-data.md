---
keywords: Experience Platform;JupyterLab;Notebooks;Datenwissenschafts-Workspace;beliebte Themen;Notebooks zur Datenanalyse
solution: Experience Platform
title: Daten mit Notebooks analysieren
type: Tutorial
description: In diesem Tutorial wird beschrieben, wie Sie mit Jupyter Notebooks, die in Data Science Workspace erstellt wurden, auf Ihre Daten zugreifen, sie erkunden und visualisieren können.
exl-id: 3b0148d1-9c08-458b-9601-979cb6c7a0fb
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1730'
ht-degree: 22%

---

# Daten mit Notebooks analysieren

>[!NOTE]
>
>Data Science Workspace ist nicht mehr erhältlich.
>
>Diese Dokumentation richtet sich an Bestandskunden mit vorherigen Berechtigungen für Data Science Workspace.

In diesem Tutorial wird beschrieben, wie Sie mit Jupyter Notebooks, die in Data Science Workspace erstellt wurden, auf Ihre Daten zugreifen, sie erkunden und visualisieren können. Am Ende dieses Tutorials sollten Sie einige der Funktionen von Jupyter-Notebooks kennen, um Ihre Daten besser zu verstehen.

Die folgenden Konzepte werden eingeführt:

- **[!DNL JupyterLab]:** [[!DNL JupyterLab]](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) ist die webbasierte Schnittstelle der nächsten Generation für Project Jupyter und ist eng in [!DNL Adobe Experience Platform] integriert.
- **Batches:** Datensätze bestehen aus Batches. Ein Batch ist ein Satz von Daten, die über einen bestimmten Zeitraum gesammelt und als Einheit verarbeitet werden. Neue Batches werden erstellt, wenn Daten zu einem Datensatz hinzugefügt werden.
- **Datenzugriffs-SDK (veraltet):** Die Datenzugriffs-SDK wird jetzt nicht mehr unterstützt. Bitte verwenden Sie das [[!DNL Experience Platform SDK]](../authoring/platform-sdk.md).

## Notebooks in Data Science Workspace erkunden

In diesem Abschnitt werden Daten untersucht, die zuvor in das Einzelhandelsverkaufsschema aufgenommen wurden.

Mit Data Science Workspace können Benutzer [!DNL Jupyter Notebooks] über die [!DNL JupyterLab] erstellen, wo sie Workflows für maschinelles Lernen erstellen und bearbeiten können. [!DNL JupyterLab] ist ein Server-Client-Collaboration-Tool, mit dem Benutzer Notebook-Dokumente über einen Webbrowser bearbeiten können. Diese Notebooks können sowohl ausführbaren Code als auch Rich-Text-Elemente enthalten. Zu unseren Zwecken verwenden wir Markdown für Analysebeschreibungen und ausführbaren [!DNL Python]-Code, um Datenexploration und -analyse durchzuführen.

### Arbeitsbereich auswählen

Beim Starten von [!DNL JupyterLab] wird eine Web-basierte Oberfläche für Jupyter-Notebooks angezeigt. Je nachdem, für welchen Notebook-Typ wir uns entscheiden, wird ein entsprechender Kernel gestartet.

Beim Vergleich, welche Umgebung verwendet werden soll, müssen die Einschränkungen jedes Services berücksichtigt werden. Wenn wir beispielsweise die Bibliothek [pandas](https://pandas.pydata.org/) mit [!DNL Python] verwenden, beträgt der RAM-Grenzwert für einen normalen Benutzer 2 GB. Selbst als Power-User wären wir auf 20 GB RAM beschränkt. Bei größeren Berechnungen wäre es sinnvoll, [!DNL Spark] zu verwenden, das 1,5 TB bietet, die für alle Notebook-Instanzen freigegeben sind.

Standardmäßig funktionieren Tensorflow-Rezepte in einem GPU-Cluster und Python wird innerhalb eines CPU-Clusters ausgeführt.

### Erstellen eines neuen Notebooks

Wählen Sie in der [!DNL Adobe Experience Platform]-Benutzeroberfläche [!UICONTROL Datenwissenschaft] im oberen Menü aus, um zur Datenwissenschafts-Workspace zu gelangen. Wählen Sie auf dieser Seite die Option [!DNL JupyterLab] aus, um den [!DNL JupyterLab]-Starter zu öffnen. Sie sollten eine Seite sehen, die der folgenden ähnelt.

![](../images/jupyterlab/analyze-data/jupyterlab-launcher-new.png)

In unserem Tutorial verwenden wir [!DNL Python] 3 im Jupyter-Notebook, um zu zeigen, wie man auf die Daten zugreift und sie erkundet. Auf der Starter-Seite finden Sie Beispiele für -Notebooks. Wir verwenden das Rezept für den Einzelhandel für [!DNL Python] 3.

![](../images/jupyterlab/analyze-data/retail_sales.png)

Das Rezept für Einzelhandelsumsätze ist ein eigenständiges Beispiel, das denselben Datensatz für Einzelhandelsumsätze verwendet, um zu zeigen, wie Daten in Jupyter Notebook untersucht und visualisiert werden können. Darüber hinaus wird das Notebook durch Schulungen und Verifizierung noch weiter vertieft. Weitere Informationen zu diesem bestimmten Notebook finden Sie in diesem [Walkthrough](../walkthrough.md).

### Zugriff auf Daten

>[!NOTE]
>
>Der `data_access_sdk_python` ist veraltet und wird nicht mehr empfohlen. Informationen zum Konvertieren von [ finden Sie im Tutorial zum Konvertieren von Datenzugriff auf SDK ](../authoring/platform-sdk.md) Experience Platform SDK . Die folgenden Schritte gelten auch für dieses Tutorial.

Wir werden den internen Zugriff auf Daten von [!DNL Adobe Experience Platform] und den externen Zugriff auf Daten überprüfen. Wir verwenden die `data_access_sdk_python`-Bibliothek für den Zugriff auf interne Daten wie Datensätze und XDM-Schemata. Für externe Daten verwenden wir die [!DNL Python]-Bibliothek von Pandas.

#### Externe Daten

Suchen Sie bei geöffnetem Notebook für den Einzelhandel nach der Kopfzeile „Daten laden“. Der folgende [!DNL Python]-Code verwendet die `DataFrame` Datenstruktur von Pandas und die Funktion [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv), um die auf [!DNL Github] gehostete CSV in den DataFrame zu lesen:

![](../images/jupyterlab/analyze-data/read_csv.png)

Die DataFrame-Datenstruktur von Pandas ist eine 2-dimensionale beschriftete Datenstruktur. Um die Dimensionen unserer Daten schnell zu sehen, können wir die `df.shape` verwenden. Dadurch wird ein Tupel zurückgegeben, das die Dimensionalität des DataFrame darstellt:

![](../images/jupyterlab/analyze-data/df_shape.png)

Schließlich können wir einen Blick darauf werfen, wie unsere Daten aussehen. Wir können `df.head(n)` nutzen, um die ersten `n` Zeilen des DataFrame anzuzeigen:

![](../images/jupyterlab/analyze-data/df_head.png)

#### [!DNL Experience Platform]

Jetzt werden wir über den Zugriff auf [!DNL Experience Platform] Daten gehen.

##### Nach Datensatz-ID

Für diesen Abschnitt verwenden wir den Einzelhandelsumsatz-Datensatz. Dies ist derselbe Datensatz, der auch im Beispiel-Notebook für Einzelhandelsumsätze verwendet wird.

In Jupyter Notebook können Sie auf Ihre Daten über die Registerkarte **Daten** ![Daten](../images/jupyterlab/analyze-data/dataset-tab.png) auf der linken Seite zugreifen. Nach Auswahl der Registerkarte werden zwei Ordner bereitgestellt. Wählen Sie den **[!UICONTROL Datensätze]** aus.

![](../images/jupyterlab/analyze-data/dataset_tab.png)

Im Verzeichnis Datensätze können Sie nun alle aufgenommenen Datensätze sehen. Beachten Sie, dass es eine Minute dauern kann, bis alle Einträge geladen sind, wenn Ihr Verzeichnis stark mit Datensätzen gefüllt ist.

Da der Datensatz derselbe ist, möchten wir die Ladedaten aus dem vorherigen Abschnitt ersetzen, der externe Daten verwendet. Wählen Sie den Codeblock unter **Daten laden** aus und drücken Sie die **d&#39;** auf Ihrer Tastatur zweimal. Stellen Sie sicher, dass der Fokus auf dem Block und nicht auf dem Text liegt. Sie können **&#39;esc&#39;** drücken, um den Textfokus zu umgehen, bevor Sie **&#39;d&#39;** zweimal drücken.

Jetzt können wir mit der rechten Maustaste auf den `Retail-Training-<your-alias>` Datensatz klicken und die Option „Daten in Notebook erkunden“ in der Dropdown-Liste auswählen. In Ihrem Notebook wird ein ausführbarer Code-Eintrag angezeigt.

>[!TIP]
>
>Informationen zum Konvertieren des Codes finden Sie im [[!DNL Experience Platform SDK]](../authoring/platform-sdk.md).

```PYTHON
from data_access_sdk_python.reader import DataSetReader
from datetime import date
reader = DataSetReader()
df = reader.load(data_set_id="xxxxxxxx", ims_org="xxxxxxxx@AdobeOrg")
df.head()
```

Wenn Sie mit anderen Kernels als [!DNL Python] arbeiten, lesen Sie bitte [diese Seite](https://github.com/adobe/acp-data-services-dsw-reference/wiki/Accessing-Data-on-the-Platform) um auf Daten auf der [!DNL Adobe Experience Platform] zuzugreifen.

Wenn Sie die ausführbare Zelle auswählen und dann auf die Wiedergabeschaltfläche in der Symbolleiste klicken, wird der ausführbare Code ausgeführt. Die Ausgabe für `head()` ist eine Tabelle mit den Schlüsseln Ihres Datensatzes als Spalten und den ersten n Zeilen im Datensatz. `head()` akzeptiert ein ganzzahliges Argument, um anzugeben, wie viele Zeilen ausgegeben werden sollen. Standardmäßig ist dies 5.

![](../images/jupyterlab/analyze-data/datasetreader_head.png)

Wenn Sie Ihren Kernel neu starten und alle Zellen erneut ausführen, sollten Sie die gleichen Ausgaben wie zuvor erhalten.

![](../images/jupyterlab/analyze-data/restart_kernel_run.png)


### Erkunden von Daten

Nachdem wir nun auf Ihre Daten zugreifen können, konzentrieren wir uns auf die Daten selbst, indem wir Statistiken und Visualisierungen verwenden. Der Datensatz, den wir verwenden, ist ein Einzelhandels-Datensatz, der verschiedene Informationen zu 45 verschiedenen Geschäften an einem bestimmten Tag liefert. Zu den Merkmalen einer bestimmten `date` und `store` gehören die folgenden:
- `storeType`
- `weeklySales`
- `storeSize`
- `temperature`
- `regionalFuelPrice`
- `markDown`
- `cpi`
- `unemployment`
- `isHoliday`

#### Statistische Zusammenfassung

Wir können [!DNL Python's] Pandas-Bibliothek nutzen, um den Datentyp der einzelnen Attribute abzurufen. Die Ausgabe des folgenden Aufrufs liefert uns Informationen über die Anzahl der Einträge und den Datentyp für die einzelnen Spalten:

```PYTHON
df.info()
```

![](../images/jupyterlab/analyze-data/df_info.png)

Diese Informationen sind hilfreich, da wir durch Kenntnis des Datentyps der einzelnen Spalten wissen, wie die Daten zu behandeln sind.

Sehen wir uns nun die statistische Zusammenfassung an. Es werden nur die numerischen Datentypen angezeigt, daher werden `date`, `storeType` und `isHoliday` nicht ausgegeben:

```PYTHON
df.describe()
```

![](../images/jupyterlab/analyze-data/df_describe.png)

Damit können wir sehen, dass für jedes Merkmal 6.435 Instanzen vorhanden sind. Außerdem werden statistische Informationen wie Mittelwert, Standardabweichung (std), Min, Max und Interquartile angegeben. So erfahren wir mehr über die Abweichung der Daten. Im nächsten Abschnitt gehen wir auf die Visualisierung ein, die mit diesen Informationen zusammenarbeitet, um uns ein gutes Verständnis unserer Daten zu vermitteln.

Wenn wir uns die Mindest- und Maximalwerte für `store` ansehen, können wir feststellen, dass die Daten 45 verschiedene Geschäfte repräsentieren. Es gibt auch `storeTypes`, die unterscheiden, was ein Geschäft ist. Außerdem können wir die Verteilung von `storeTypes` anzeigen, indem wir Folgendes tun:

![](../images/jupyterlab/analyze-data/df_groupby.png)

Dies bedeutet, dass 22 Speicher `storeType` `A`, 17 `storeType` `B` und 6 `storeType` `C` sind.

#### Datenvisualisierung

Da wir unsere Dataframe-Werte nun kennen, möchten wir sie um Visualisierungen ergänzen, damit sich Muster leichter erkennen lassen. Diagramme sind auch bei der Übermittlung der Ergebnisse an eine Zielgruppe nützlich. Zu den [!DNL Python] Bibliotheken, die für die Visualisierung nützlich sind, gehören:
- [matplotlib](https://matplotlib.org/)
- [Pandas](https://pandas.pydata.org/)
- [seaborn](https://seaborn.pydata.org/)
- [gplot](https://ggplot2.tidyverse.org/)

In diesem Abschnitt werden wir kurz einige Vorteile für die Verwendung der einzelnen Bibliotheken vorstellen.

[Matplotlib](https://matplotlib.org/) ist das älteste [!DNL Python] Visualisierungspaket. Ihr Ziel ist es, „einfache Dinge und schwierige Dinge möglich zu machen“. Dies trifft in der Regel zu, da das Paket extrem leistungsstark ist, aber auch mit Komplexität einhergeht. Es ist nicht immer einfach, ein vernünftig aussehendes Diagramm zu erhalten, ohne viel Zeit und Mühe in Anspruch zu nehmen.

[Pandas](https://pandas.pydata.org/) wird hauptsächlich für sein DataFrame-Objekt verwendet, das Datenmanipulationen mit integrierter Indizierung ermöglicht. Pandas verfügen jedoch auch über eine integrierte Plotfunktion, die auf der Grundlage der Plotlib basiert.

[seaborn](https://seaborn.pydata.org/) ist ein Paket, das auf matplotlib aufbaut. Ihr Hauptziel ist es, Standarddiagramme visuell ansprechender zu gestalten und die Erstellung komplizierter Diagramme zu vereinfachen.

[gplot](https://ggplot2.tidyverse.org/) ist ein Paket, das ebenfalls auf Matplotlib aufbaut. Der Hauptunterschied besteht jedoch darin, dass das Tool ein Port von gplot2 für R ist. Ähnlich wie seaborn ist das Ziel, die Matplotlib zu verbessern. Benutzer, die mit gplot2 für R vertraut sind, sollten diese Bibliothek berücksichtigen.


##### Eindimensionale Diagramme

Eindimensionale Diagramme sind Diagramme mit einer einzelnen Variablen. Ein gängiges univariates Diagramm wird verwendet, um Ihre Daten zu visualisieren, ist das Box- und Whisker-Diagramm.

Mit unserem Datensatz für Einzelhandelsumsätze von oben können wir ein Box- und Whisker-Diagramm für jedes der 45 Geschäfte und ihre wöchentlichen Umsätze generieren. Das Diagramm wird mithilfe der `seaborn.boxplot`-Funktion erstellt.

![](../images/jupyterlab/analyze-data/box_whisker.png)

Ein Box- und Whisker-Diagramm dient dazu, die Verteilung von Daten anzuzeigen. Die äußeren Linien der Zeichnung zeigen das obere und untere Quartil, während der Kasten den Interquartilbereich umfasst. Die Linie im Kasten markiert den Median. Alle Datenpunkte, die mehr als das 1,5-Fache des oberen oder unteren Quartils betragen, werden als Kreis markiert. Diese Punkte werden als Ausreißer betrachtet.

##### Mehrdimensionale Diagramme

Mehrdimensionale Diagramme dienen dazu, die Interaktion zwischen Variablen anzuzeigen. Dank der Visualisierung können Datenwissenschaftler erkennen, ob Korrelationen oder Muster zwischen den Variablen bestehen. Ein häufig verwendetes mehrdimensionales Diagramm ist eine Korrelationsmatrix. Bei einer Korrelationsmatrix werden Abhängigkeiten zwischen verschiedenen Variablen mit dem Korrelationskoeffizienten quantifiziert.

Mit demselben Einzelhandelsdatensatz können wir die Korrelationsmatrix generieren.

![](../images/jupyterlab/analyze-data/correlation_1.png)

Achten Sie auf die Diagonale von 1 in der Mitte. Das bedeutet, dass eine Variable beim Vergleich mit sich selbst eine vollständige positive Korrelation aufweist. Eine starke positive Korrelation wird näher bei 1 liegen, während eine schwache Korrelation näher bei 0 liegt. Negative Korrelation wird durch einen negativen Koeffizienten angezeigt, der auf einen gegenläufigen Trend hinweist.


## Nächste Schritte

In diesem Tutorial wurde beschrieben, wie Sie ein neues Jupyter-Notebook in der Data Science Workspace erstellen und wie Sie extern sowie aus [!DNL Adobe Experience Platform] auf Daten zugreifen können. Im Einzelnen haben wir die folgenden Schritte ausgeführt:
- Erstellen eines neuen Jupyter-Notebooks
- Zugreifen auf Datensätze und Schemata
- Erkunden von Datensätzen

Jetzt können Sie mit dem [ Abschnitt fortfahren, ](../models-recipes/package-source-files-recipe.md) ein Rezept zu verpacken und es in Data Science Workspace zu importieren.
