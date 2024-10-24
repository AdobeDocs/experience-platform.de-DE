---
keywords: Experience Platform; JupyterLab; Rezept; Notebooks; Data Science Workspace; beliebte Themen; Rezept erstellen
solution: Experience Platform
title: Erstellen eines Modells mit JupyterLab Notebooks
type: Tutorial
description: Dieses Tutorial führt Sie durch die erforderlichen Schritte zum Erstellen eines Rezepts mithilfe der JupyterLab Notebook-Rezept-Builder-Vorlage.
exl-id: d3f300ce-c9e8-4500-81d2-ea338454bfde
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '2106'
ht-degree: 29%

---

# Erstellen eines Modells mit JupyterLab Notebooks

>[!NOTE]
>
>Data Science Workspace ist nicht mehr erhältlich.
>
>Diese Dokumentation richtet sich an Bestandskunden mit vorherigen Berechtigungen für Data Science Workspace.

Dieses Tutorial führt Sie durch die erforderlichen Schritte zum Erstellen eines Modells mithilfe der JupyterLab Notebook-Rezept-Builder-Vorlage.

## Vorgestellte Konzepte:

- **Rezepte:** Ein Rezept ist ein Adobe für eine Modellspezifikation und ein Container auf oberster Ebene, der einen bestimmten maschinellen Lernprozess, einen KI-Algorithmus oder eine Gruppe von Algorithmen, Verarbeitungslogik und Konfiguration darstellt, die zum Erstellen und Ausführen eines trainierten Modells erforderlich sind.
- **Modell:** Ein Modell ist eine Instanz eines maschinellen Lernrezepts, das mithilfe von historischen Daten und Konfigurationen zur Lösung eines geschäftlichen Anwendungsfalls trainiert wird.
- **Training:** Ein Training besteht aus dem Erlernen von Mustern und Insights auf Grundlage gekennzeichneter Daten.
- **Scoring:** Beim Scoring werden mithilfe eines trainierten Modells Insights aus Daten generiert.

## Herunterladen der erforderlichen Assets {#assets}

Bevor Sie mit diesem Tutorial fortfahren, müssen Sie die erforderlichen Schemata und Datensätze erstellen. Besuchen Sie das Tutorial zum Erstellen der Luma-Propensity-Modellschemas und -Datensätze ](../models-recipes/create-luma-data.md) , um die erforderlichen Assets herunterzuladen und die Voraussetzungen einzurichten.[

## Erste Schritte mit der [!DNL JupyterLab] Notebook-Umgebung

Das Erstellen eines neuen Rezepts kann innerhalb von [!DNL Data Science Workspace] erfolgen. Navigieren Sie zunächst zu [Adobe Experience Platform](https://platform.adobe.com) und wählen Sie links die Registerkarte **[!UICONTROL Notebooks]** aus. Um ein neues Notebook zu erstellen, wählen Sie die Vorlage &quot;Recipe Builder&quot;aus dem Feld [!DNL JupyterLab Launcher].

Mit dem Notebook [!UICONTROL Recipe Builder] können Sie Trainings- und Scoring-Läufe im Notebook ausführen. So können Sie zwischen laufenden Experimenten für Trainings- und Scoring-Daten flexibel Änderungen an den `train()`- und `score()`-Methoden vorzunehmen. Sobald Sie mit den Trainings- und Scoring-Ergebnissen zufrieden sind, können Sie ein Rezept erstellen und es außerdem als Modell veröffentlichen, indem Sie das Rezept zur Modellfunktionalität verwenden.

>[!NOTE]
>
>Das Notebook [!UICONTROL Recipe Builder] unterstützt die Arbeit mit allen Dateiformaten, derzeit unterstützt die Funktion zum Erstellen von Rezepten jedoch nur [!DNL Python].

![](../images/jupyterlab/create-recipe/recipe_builder-new.png)

Wenn Sie das Notebook [!UICONTROL Recipe Builder] aus dem Starter auswählen, wird das Notebook in einer neuen Registerkarte geöffnet.

Auf der neuen Notebook-Registerkarte oben lädt eine Symbolleiste mit drei zusätzlichen Aktionen: **[!UICONTROL Trainieren]**, **[!UICONTROL Score]** und **[!UICONTROL Rezept erstellen]**. Diese Symbole werden nur im Notebook [!UICONTROL Recipe Builder] angezeigt. Weitere Informationen zu diesen Aktionen finden Sie [im Abschnitt &quot;Training und Scoring&quot;](#training-and-scoring), nachdem Sie Ihr Rezept im Notebook erstellt haben.

![](../images/jupyterlab/create-recipe/toolbar_actions.png)

## Erste Schritte mit dem Notebook [!UICONTROL Recipe Builder]

Im bereitgestellten Asset-Ordner ist ein Luma-Tendenzmodell `propensity_model.ipynb`. Laden Sie über die Option zum Hochladen von Notebooks in JupyterLab das bereitgestellte Modell hoch und öffnen Sie das Notebook.

![Notebook hochladen](../images/jupyterlab/create-recipe/upload_notebook.png)

Der Rest dieses Tutorials umfasst die folgenden Dateien, die im Propensity Model Notebook vordefiniert sind:

- [Anforderungsdatei](#requirements-file)
- [Konfigurationsdateien](#configuration-files)
- [Ladeprogramm für Trainings-Daten](#training-data-loader)
- [Ladeprogramm für Scoring-Daten](#scoring-data-loader)
- [Pipeline-Datei](#pipeline-file)
- [Evaluator-Datei](#evaluator-file)
- [Data Saver-Datei](#data-saver-file)

Im folgenden Video-Tutorial wird das Modell-Notebook &quot;Luma-Neigung&quot;erläutert:

>[!VIDEO](https://video.tv.adobe.com/v/333570)

### Anforderungsdatei {#requirements-file}

Die Anforderungsdatei wird verwendet, um zusätzliche Bibliotheken zu deklarieren, die Sie im Modell verwenden möchten. Sie können die Versionsnummer angeben, wenn eine Abhängigkeit vorliegt. Um nach weiteren Bibliotheken zu suchen, besuchen Sie [anaconda.org](https://anaconda.org). Informationen zum Formatieren der Anforderungsdatei finden Sie unter [Kontext](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-file-manually). Die Liste der bereits verwendeten Hauptbibliotheken umfasst:

```JSON
python=3.6.7
scikit-learn
pandas
numpy
data_access_sdk_python
```

>[!NOTE]
>
>Bibliotheken oder bestimmte Versionen, die Sie hinzufügen, sind möglicherweise nicht mit den oben genannten Bibliotheken kompatibel. Wenn Sie sich außerdem dafür entscheiden, eine Umgebungsdatei manuell zu erstellen, darf das Feld `name` nicht überschrieben werden.

Für das Luma Propensity Model Notebook müssen die Anforderungen nicht aktualisiert werden.

### Konfigurationsdateien {#configuration-files}

Mit den Konfigurationsdateien `training.conf` und `scoring.conf` werden die Datensätze angegeben, die Sie für das Training und Scoring sowie das Hinzufügen von Hyperparametern nutzen möchten. Es gibt separate Konfigurationen für Training und Scoring.

Damit ein Modell eine Schulung ausführen kann, müssen Sie die `trainingDataSetId`, `ACP_DSW_TRAINING_XDM_SCHEMA` und `tenantId` angeben. Zusätzlich zum Scoring müssen Sie die `scoringDataSetId`, `tenantId` und `scoringResultsDataSetId ` angeben.

Um die Datensatz- und Schema-IDs zu finden, gehen Sie in Notebooks in der linken Navigationsleiste (unter dem Ordnersymbol) zur Registerkarte &quot;Daten&quot;![Registerkarte &quot;Daten&quot;](../images/jupyterlab/create-recipe/dataset-tab.png). Es müssen drei verschiedene Datensatz-IDs angegeben werden. Der `scoringResultsDataSetId` wird verwendet, um die Modellbewertungsergebnisse zu speichern, und sollte ein leerer Datensatz sein. Diese Datensätze wurden zuvor im Schritt [Erforderliche Assets](#assets) vorgenommen.

![](../images/jupyterlab/create-recipe/dataset_tab.png)

Dieselben Daten finden Sie in [Adobe Experience Platform](https://platform.adobe.com/) unter den Registerkarten **[Schema](https://platform.adobe.com/schema)** und **[Datensätze](https://platform.adobe.com/dataset/overview)**.

Nach dem Abschluss sollte Ihre Trainings- und Scoring-Konfiguration dem folgenden Screenshot ähneln:

![configuration](../images/jupyterlab/create-recipe/config.png)

Standardmäßig werden die folgenden Konfigurationsparameter für Sie festgelegt, wenn Sie Daten trainieren und bewerten:

- `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
- `ML_FRAMEWORK_IMS_TOKEN`
- `ML_FRAMEWORK_IMS_ML_TOKEN`
- `ML_FRAMEWORK_IMS_TENANT_ID`

## Grundlegendes zum Ladeprogramm für Schulungsdaten {#training-data-loader}

Der Zweck des Ladeprogramms für Trainings-Daten besteht darin, Daten zu instanziieren, die zum Erstellen des maschinellen Lernmodells verwendet werden. In der Regel gibt es zwei Aufgaben, die der Ladeprogramm für Trainings-Daten durchführt:

- Laden von Daten aus [!DNL Platform]
- Datenvorbereitung und Funktionsentwicklung

Die folgenden beiden Abschnitte liefern Informationen über das Laden und Vorbereiten von Daten.

### Laden von Daten {#loading-data}

In diesem Schritt wird der [pandas-Dataframe](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html) verwendet. Daten können aus Dateien in [!DNL Adobe Experience Platform] entweder mit dem [!DNL Platform] SDK (`platform_sdk`) oder aus externen Quellen mit den Funktionen `read_csv()` oder `read_json()` von pandas geladen werden.

- [[!DNL Platform SDK]](#platform-sdk)
- [Externe Quellen](#external-sources)

>[!NOTE]
>
>Im Recipe Builder-Notebook werden Daten über das Ladeprogramm `platform_sdk` geladen.

### [!DNL Platform] SDK {#platform-sdk}

Eine ausführliche Anleitung zur Verwendung des Datenladeprogramms `platform_sdk` finden Sie im [Handbuch zum Platform-SDK](../authoring/platform-sdk.md). Dieses Tutorial enthält Informationen zur Build-Authentifizierung, zum grundlegenden Lesen von Daten sowie zum grundlegenden Schreiben von Daten.

### Externe Quellen {#external-sources}

Dieser Abschnitt veranschaulicht, wie Sie eine JSON- oder CSV-Datei in ein pandas-Objekt importieren können. Die offizielle Dokumentation der pandas-Bibliothek finden Sie hier:
- [read_csv](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)
- [read_json](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_json.html)

Zunächst finden Sie hier ein Beispiel für den Import einer CSV-Datei. Das `data`-Argument ist der Pfad zur CSV-Datei. Diese Variable wurde aus den `configProperties` im [vorherigen Abschnitt](#configuration-files) importiert.

```PYTHON
df = pd.read_csv(data)
```

Sie können auch aus einer JSON-Datei importieren. Das `data`-Argument ist der Pfad zur CSV-Datei. Diese Variable wurde aus den `configProperties` im [vorherigen Abschnitt](#configuration-files) importiert.

```PYTHON
df = pd.read_json(data)
```

Jetzt befinden sich Ihre Daten im Dataframe-Objekt und können im [nächsten Abschnitt](#data-preparation-and-feature-engineering) analysiert und bearbeitet werden.

## Datei für Trainings-Datenladeprogramm

In diesem Beispiel werden Daten mit dem Platform SDK geladen. Die Bibliothek kann oben auf der Seite importiert werden, indem die folgende Zeile eingefügt wird:

`from platform_sdk.dataset_reader import DatasetReader`

Anschließend können Sie die `load()` -Methode verwenden, um den Trainings-Datensatz aus dem `trainingDataSetId` zu erfassen, wie in der Konfigurationsdatei (`recipe.conf`) festgelegt.

```PYTHON
def load(config_properties):
    print("Training Data Load Start")

    #########################################
    # Load Data
    #########################################    
    client_context = get_client_context(config_properties)
    dataset_reader = DatasetReader(client_context, dataset_id=config_properties['trainingDataSetId'])
```

>[!NOTE]
>
>Wie im Abschnitt [Konfigurationsdatei](#configuration-files) erwähnt, werden die folgenden Konfigurationsparameter für Sie festgelegt, wenn Sie mit `client_context = get_client_context(config_properties)` auf Daten von Experience Platform zugreifen:
> - `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
> - `ML_FRAMEWORK_IMS_TOKEN`
> - `ML_FRAMEWORK_IMS_ML_TOKEN`
> - `ML_FRAMEWORK_IMS_TENANT_ID`

Jetzt, da Sie über Ihre Daten verfügen, können Sie mit der Datenvorbereitung und Funktionsentwicklung beginnen.

### Datenvorbereitung und Funktionsentwicklung {#data-preparation-and-feature-engineering}

Nach dem Laden der Daten müssen die Daten bereinigt und einer Datenvorbereitung unterzogen werden. In diesem Beispiel besteht das Ziel des Modells darin, vorherzusagen, ob ein Kunde ein Produkt bestellen wird oder nicht. Da das Modell bestimmte Produkte nicht betrachtet, benötigen Sie nicht `productListItems` und daher wird die Spalte entfernt. Als Nächstes werden zusätzliche Spalten abgelegt, die nur einen oder zwei Werte in einer Spalte enthalten. Beim Trainieren eines Modells ist es wichtig, nur nützliche Daten beizubehalten, die bei der Vorhersage Ihres Ziels hilfreich sind.

![Beispiel für Datenvorgabe](../images/jupyterlab/create-recipe/data_prep.png)

Sobald Sie unnötige Daten gelöscht haben, können Sie mit der Funktionsentwicklung beginnen. Die für dieses Beispiel verwendeten Demodaten enthalten keine Sitzungsinformationen. Normalerweise möchten Sie Daten zu aktuellen und vorherigen Sitzungen für einen bestimmten Kunden haben. Aufgrund fehlender Sitzungsinformationen imitiert dieses Beispiel stattdessen aktuelle und vergangene Sitzungen über die Journey-Abgrenzung.

![Journey-Abgrenzung](../images/jupyterlab/create-recipe/journey_demarcation.png)

Nach Abschluss der Abgrenzung werden die Daten beschriftet und eine Journey erstellt.

![beschriften Sie die Daten](../images/jupyterlab/create-recipe/label_data.png)

Als Nächstes werden die Funktionen erstellt und in Vergangenheit und Gegenwart unterteilt. Dann werden unnötige Spalten entfernt, sodass Sie sowohl über die bisherigen als auch über die aktuellen Journey verfügen. Diese Journey enthalten Informationen, wie z. B. ob ein Kunde einen Artikel gekauft hat und die Journey, die er bis zum Kauf durchgeführt hat.

![letzte aktuelle Schulung](../images/jupyterlab/create-recipe/final_journey.png)

## Ladeprogramm für Scoring-Daten {#scoring-data-loader}

Das Laden von Daten für das Scoring ähnelt dem Laden von Trainings-Daten. Wenn Sie sich den Code genau ansehen, können Sie sehen, dass alles mit Ausnahme der `scoringDataSetId` in der `dataset_reader` identisch ist. Dies liegt daran, dass dieselbe Luma-Datenquelle sowohl für Schulungen als auch für Auswertungen verwendet wird.

Falls Sie verschiedene Datendateien für Training und Scoring verwenden möchten, ist der Ladeprogramm für Trainings- und Scoring-Daten separat. Auf diese Weise können Sie zusätzliche Vorab-Bearbeitungsvorgänge durchführen, z. B. bei Bedarf Ihre Trainings-Daten Ihren Scoring-Daten zuordnen.

## Pipeline-Datei {#pipeline-file}

Die Datei `pipeline.py` enthält Logik für Training und Scoring.

Der Zweck von Schulungen besteht darin, ein Modell mithilfe von Funktionen und Bezeichnungen in Ihrem Trainings-Datensatz zu erstellen. Nachdem Sie Ihr Trainings-Modell ausgewählt haben, müssen Sie Ihren x- und y-Trainings-Datensatz an das Modell anpassen und die Funktion gibt das trainierte Modell zurück.

>[!NOTE]
> 
>Funktionen beziehen sich auf die Eingabevariable, die vom maschinellen Lernmodell zur Vorhersage der Beschriftungen verwendet wird.

![def train](../images/jupyterlab/create-recipe/def_train.png)

Die `score()`-Funktion sollte den Scoring-Algorithmus enthalten und einen Messwert zurückgeben, der angibt, wie gut das Modell funktioniert. Die `score()`-Funktion nutzt die Bezeichnungen des Scoring-Datensatzes und das trainierte Modell, um eine Reihe von prognostizierten Funktionen zu generieren. Die prognostizierten Werte werden dann mit den tatsächlichen Funktionen im Scoring-Datensatz abgeglichen. In diesem Beispiel verwendet die Funktion `score()` das trainierte Modell, um Funktionen mithilfe der Bezeichnungen aus dem Scoring-Datensatz vorherzusagen. Die prognostizierten Funktionen werden zurückgegeben.

![def score](../images/jupyterlab/create-recipe/def_score.png)

## Evaluator-Datei {#evaluator-file}

Die Datei `evaluator.py` enthält Logik dafür, wie Sie Ihr trainiertes Rezept bewerten und Ihre Trainings-Daten aufteilen möchten.

### Datensatz aufteilen {#split-the-dataset}

Die Vorbereitung der Daten für das Training erfordert eine Aufteilung des Datensatzes, damit er sich für Training und Tests verwenden lässt. Diese `val` -Daten werden implizit verwendet, um das Modell nach dem Trainieren zu bewerten. Dieser Prozess erfolgt getrennt vom Scoring.

In diesem Abschnitt wird die Funktion `split()` angezeigt, die Daten in das Notebook lädt und dann die Daten bereinigt, indem nicht verwandte Spalten im Datensatz entfernt werden. Von dort aus können Sie Funktionsentwicklung durchführen, um zusätzliche relevante Funktionen aus vorhandenen Rohfunktionen in den Daten zu erstellen.

![Aufspaltungsfunktion](../images/jupyterlab/create-recipe/split.png)

### Trainiertes Modell auswerten {#evaluate-the-trained-model}

Die Funktion `evaluate()` wird ausgeführt, nachdem das Modell trainiert wurde, und gibt eine Metrik zurück, die angibt, wie erfolgreich das Modell funktioniert. Die Funktion `evaluate()` verwendet die Testdatensatzbezeichnungen und das trainierte Modell, um eine Reihe von Funktionen vorherzusagen. Die prognostizierten Werte werden dann mit den tatsächlichen Funktionen im Testdatensatz abgeglichen. In diesem Beispiel werden die Metriken `precision`, `recall`, `f1` und `accuracy` verwendet. Beachten Sie, dass die Funktion ein `metric`-Objekt zurückgibt, das eine Gruppe von Auswertungsmetriken enthält. Diese Metriken werden verwendet, um zu bewerten, wie gut das trainierte Modell funktioniert.

![evaluate](../images/jupyterlab/create-recipe/evaluate.png)

Durch Hinzufügen von `print(metric)` können Sie die Metrikergebnisse anzeigen.

![Metrikergebnisse](../images/jupyterlab/create-recipe/evaluate_metric.png)

## Data Saver-Datei {#data-saver-file}

Die Datei `datasaver.py` enthält die Funktion `save()` und wird zum Speichern Ihrer Prognose beim Testen der Auswertung verwendet. Die Funktion `save()` nimmt Ihre Prognose entgegen und schreibt die Daten mithilfe von [!DNL Experience Platform Catalog] -APIs in die `scoringResultsDataSetId`, die Sie in Ihrer `scoring.conf` -Datei angegeben haben. Sie können

![Data Saver](../images/jupyterlab/create-recipe/data_saver.png)

## Training und Scoring {#training-and-scoring}

Wenn Sie die Änderungen an Ihrem Notebook abgeschlossen haben und Ihr Rezept trainieren möchten, können Sie die zugehörigen Schaltflächen oben in der Leiste auswählen, um einen Trainings-Lauf in der Zelle zu erstellen. Nach Auswahl der Schaltfläche wird ein Protokoll mit Befehlen und Ausgaben aus dem Trainings-Skript im Notebook angezeigt (unter der Zelle `evaluator.py` ). Conda installiert zunächst alle Abhängigkeiten, dann wird das Training initiiert.

Beachten Sie, dass Sie ein Training mindestens einmal ausführen müssen, bevor Sie mit dem Scoring fortfahren können. Wenn Sie die Schaltfläche **[!UICONTROL Scoring ausführen]** auswählen, wird das trainierte Modell, das während des Trainings generiert wurde, bewertet. Das Scoring-Skript wird unter `datasaver.py` angezeigt.

Wenn Sie zum Debuggen die ausgeblendete Ausgabe anzeigen möchten, fügen Sie `debug` am Ende der Ausgabenzelle hinzu und führen Sie das Scoring erneut aus.

![Trainieren und Punktstand](../images/jupyterlab/create-recipe/toolbar_actions.png)

## Rezept erstellen {#create-recipe}

Wenn Sie die Bearbeitung des Rezepts abgeschlossen haben und mit der Trainings-/Scoring-Ausgabe zufrieden sind, können Sie ein Rezept aus dem Notebook erstellen, indem Sie oben rechts die Option **[!UICONTROL Rezept erstellen]** auswählen.

![](../images/jupyterlab/create-recipe/create-recipe.png)

Nach Auswahl von **[!UICONTROL Rezept erstellen]** werden Sie aufgefordert, einen Rezeptnamen einzugeben. Dieser Name stellt das eigentliche Rezept dar, das für [!DNL Platform] erstellt wurde.

![](../images/jupyterlab/create-recipe/enter_recipe_name.png)

Wenn Sie **[!UICONTROL OK]** auswählen, beginnt der Prozess zur Rezepterstellung. Dies kann einige Zeit dauern und anstelle der Schaltfläche Rezept erstellen wird eine Fortschrittsleiste angezeigt. Nach Abschluss können Sie die Schaltfläche **[!UICONTROL Rezepte anzeigen]** auswählen, um zur Registerkarte **[!UICONTROL Rezepte]** unter **[!UICONTROL ML-Modelle]** zu gelangen.

![](../images/jupyterlab/create-recipe/recipe_creation_started.png)

>[!CAUTION]
>
> - Löschen Sie keine der Dateizellen.
> - Bearbeiten Sie nicht die `%%writefile`-Zeile oben in den Dateizellen.
> - Erstellen Sie nicht gleichzeitig Rezepte in verschiedenen Notebooks.

## Nächste Schritte {#next-steps}

In diesem Tutorial haben Sie gelernt, wie Sie ein Modell für maschinelles Lernen im Notebook [!UICONTROL Recipe Builder] erstellen. Sie haben auch gelernt, wie Sie den Workflow Notebook an Rezept ausführen können.

Um weiterhin zu lernen, wie Sie mit Ressourcen in [!DNL Data Science Workspace] arbeiten, besuchen Sie bitte das Dropdown-Menü [!DNL Data Science Workspace] Rezepte und Modelle .