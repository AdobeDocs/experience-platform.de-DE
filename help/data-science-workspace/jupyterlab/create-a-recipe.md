---
keywords: Experience Platform;JupyterLab;recipe;notebooks;Data Science Workspace;popular topics
solution: Experience Platform
title: Erstellen eines Skripts mit Jupyter-Notebooks
topic: Tutorial
translation-type: tm+mt
source-git-commit: c48079ba997a7b4c082253a0b2867df76927aa6d
workflow-type: tm+mt
source-wordcount: '2292'
ht-degree: 0%

---


# Erstellen eines Skripts mit Jupyter-Notebooks

Dieses Lernprogramm umfasst zwei Hauptabschnitte. Zuerst erstellen Sie ein maschinelles Lernmodell mit einer Vorlage in [!DNL JupyterLab Notebook]. Als Nächstes führen Sie das Notebook durch, um den Arbeitsablauf für Rezepte zu realisieren, in dem Sie ein Rezept [!DNL JupyterLab] erstellen [!DNL Data Science Workspace].

## Vorgestellte Konzepte:

- **Rezepte:** Ein Rezept ist der von Adobe verwendete Begriff für eine Modellspezifikation. Es handelt sich dabei um einen Container auf oberster Ebene, der ein bestimmtes maschinelles Lernen, einen AI-Algorithmus oder ein Ensemble von Algorithmen, eine Verarbeitungslogik und eine Konfiguration darstellt, die erforderlich sind, um ein geschultes Modell zu erstellen und auszuführen und damit zur Lösung spezifischer Geschäftsprobleme beizutragen.
- **Modell:** Ein Modell ist ein Beispiel für ein maschinelles Lernrezept, das mithilfe von historischen Daten und Konfigurationen für die Lösung eines Geschäftsfalls trainiert wird.
- **Schulung:** Schulung ist der Prozess des Lernens von Mustern und Erkenntnissen aus gekennzeichneten Daten.
- **Bewertung:** Die Auswertung ist der Prozess, bei dem mithilfe eines geschulten Modells Erkenntnisse aus Daten generiert werden.

## Erste Schritte mit der [!DNL JupyterLab] Notebook-Umgebung

Das Erstellen eines Rezeptes von Grund auf kann innerhalb von [!DNL Data Science Workspace]vorgenommen werden. Navigieren Sie zum Beginn zur [Adobe Experience Platform](https://platform.adobe.com) und klicken Sie auf der linken Seite auf die Registerkarte **[!UICONTROL Notebooks]** . Erstellen Sie ein neues Notebook, indem Sie die Vorlage Rezept-Builder aus dem [!DNL JupyterLab Launcher].

Mit dem [!UICONTROL Rezept Builder] Notebook können Sie Trainings- und Scoring-Runs im Notebook ausführen. Dadurch erhalten Sie die Flexibilität, Änderungen an ihren `train()` und `score()` Methoden zwischen laufenden Experimenten mit den Schulungs- und Bewertungsdaten vorzunehmen. Sobald Sie mit den Ausgaben der Schulung und Bewertung zufrieden sind, können Sie ein Rezept erstellen, das bei der [!DNL Data Science Workspace] Verwendung des Notebooks verwendet werden kann, um Funktionen zu rezeptieren, die in das Rezept Builder-Notebook integriert sind.

>[!NOTE]
>Das Rezept Builder-Notebook unterstützt alle Dateiformate, aber derzeit unterstützt die Funktion Rezept erstellen nur [!DNL Python].

![](../images/jupyterlab/create-recipe/recipe-builder.png)

Wenn Sie vom Starter auf das Rezept Builder-Notebook klicken, wird das Notebook in der Registerkarte geöffnet. Die im Notebook verwendete Vorlage ist das Python Retail Sales Forecasting Rezept, das auch in [diesem öffentlichen Repository zu finden ist](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail/)

Sie werden feststellen, dass es in der Symbolleiste drei weitere Aktionen gibt, nämlich **[!UICONTROL Zug]**, **[!UICONTROL Punktzahl]** und Rezept **[!UICONTROL erstellen]**. Diese Symbole werden nur im [!UICONTROL Rezept Builder] -Notebook angezeigt. Weitere Informationen zu diesen Aktionen erhalten Sie [im Bereich](#training-and-scoring) Training und Bewertung, nachdem Sie Ihr Rezept im Notebook erstellt haben.

![](../images/jupyterlab/create-recipe/toolbar_actions.png)

## Bearbeiten von Skriptdateien

Um Änderungen an den Skriptdateien vorzunehmen, navigieren Sie zu der Zelle im Jupyter, die dem Dateipfad entspricht. Wenn Sie zum Beispiel Änderungen vornehmen möchten, suchen Sie nach `evaluator.py`dieser Option `%%writefile demo-recipe/evaluator.py`.

Beginn, die die erforderlichen Änderungen an der Zelle vornehmen, führen Sie die Zelle nach Abschluss einfach aus. Der `%%writefile filename.py` Befehl schreibt den Inhalt der Zelle in die `filename.py`. Sie müssen die Zelle für jede Datei mit Änderungen manuell ausführen.

>[!NOTE] Sie sollten die Zellen gegebenenfalls manuell ausführen.

## Erste Schritte mit dem Rezept Builder-Notebook

Jetzt, da Sie die Grundlagen der [!DNL JupyterLab] Notebook-Umgebung kennen, können Sie damit beginnen, die Dateien zu betrachten, die ein Rezept für ein maschinelles Lernmodell ausmachen. Die Dateien, über die wir sprechen werden, sind hier dargestellt:

- [Anforderungsdatei](#requirements-file)
- [Konfigurationsdateien](#configuration-files)
- [Schulungsdatenlader](#training-data-loader)
- [Datenlader für die Auswertung](#scoring-data-loader)
- [Pipeline-Datei](#pipeline-file)
- [Evaluator-Datei](#evaluator-file)
- [Datenspeicherdatei](#data-saver-file)

### Anforderungsdatei {#requirements-file}

Die Datei &quot;requirements&quot;dient zum Deklarieren zusätzlicher Bibliotheken, die Sie im Rezept verwenden möchten. Sie können die Versionsnummer angeben, wenn eine Abhängigkeit vorliegt. Weitere Bibliotheken finden Sie unter https://anaconda.org. Die Liste der bereits verwendeten Hauptbibliotheken umfasst:

```JSON
python=3.5.2
scikit-learn
pandas
numpy
data_access_sdk_python
```

>[!NOTE]
>Bibliotheken oder spezifische Versionen, die Sie hinzufügen, sind möglicherweise nicht mit den oben genannten Bibliotheken kompatibel.

### Konfigurationsdateien {#configuration-files}

Die Konfigurationsdateien `training.conf` und - `scoring.conf`dateien werden verwendet, um die Datensätze anzugeben, die Sie für Schulungen und Bewertungen verwenden möchten, sowie um Hyperparameter hinzuzufügen. Es gibt separate Konfigurationen für Schulung und Bewertung.

Benutzer müssen die folgenden Variablen ausfüllen, bevor sie eine Schulung und Bewertung durchführen:
- `trainingDataSetId`
- `ACP_DSW_TRAINING_XDM_SCHEMA`
- `scoringDataSetId`
- `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA`
- `scoringResultsDataSetId`

Um den Datensatz und die Schema-IDs zu finden, gehen Sie in Notebooks auf der linken Navigationsleiste (unter dem Ordnersymbol) zur Registerkarte &quot;Daten&quot;.

![](../images/jupyterlab/create-recipe/datasets.png)

Die gleichen Informationen finden Sie auf der [Adobe Experience Platform](https://platform.adobe.com/) unter den Registerkarten **[Schema](https://platform.adobe.com/schema)**und**[Datensatz](https://platform.adobe.com/dataset/overview)** .

Standardmäßig werden beim Zugriff auf Daten die folgenden Konfigurationsparameter festgelegt:

- `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
- `ML_FRAMEWORK_IMS_TOKEN`
- `ML_FRAMEWORK_IMS_ML_TOKEN`
- `ML_FRAMEWORK_IMS_TENANT_ID`

## Schulungsdatenlader {#training-data-loader}

Der Zweck des Schulungsdaten-Laders besteht darin, Daten zu instanziieren, die zum Erstellen des maschinellen Lernmodells verwendet werden. In der Regel gibt es zwei Aufgaben, die der Schulungsdatenlader ausführen wird:
- Daten laden von [!DNL Platform]
- Datenvorbereitung und Funktionstechnik

Die folgenden beiden Abschnitte gehen über das Laden von Daten und die Datenvorbereitung.

### Daten laden {#loading-data}

In diesem Schritt wird das [Pandas-Dataframe](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html)verwendet. Daten können aus Dateien geladen werden, die entweder [!DNL Adobe Experience Platform] mit dem [!DNL Platform] SDK (`platform_sdk`) oder aus externen Quellen mithilfe von Pandas `read_csv()` oder `read_json()` Funktionen verwendet werden.

- [!DNL Platform SDK](#platform-sdk)
- [Externe Quellen](#external-sources)

>[!NOTE]
>Im Recipe Builder-Notebook werden Daten über den `platform_sdk` Datenlader geladen.

### [!DNL Platform] SDK {#platform-sdk}

Eine ausführliche Anleitung zur Verwendung des `platform_sdk` Datenladeprogramms finden Sie im Handbuch zum [Platform-SDK](../authoring/platform-sdk.md). Dieses Lernprogramm enthält Informationen zur Buildauthentifizierung, zum grundlegenden Lesen von Daten und zum grundlegenden Schreiben von Daten.

### Externe Quellen {#external-sources}

Dieser Abschnitt zeigt Ihnen, wie Sie eine JSON- oder CSV-Datei in ein Pandas-Objekt importieren. Die offizielle Dokumentation der Pandas-Bibliothek finden Sie hier:
- [read_csv](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)
- [read_json](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_json.html)

Erstens: Hier ist ein Beispiel für den Import einer CSV-Datei. Das `data` Argument ist der Pfad zur CSV-Datei. Diese Variable wurde aus dem `configProperties` im [vorherigen Abschnitt](#configuration-files)importiert.

```PYTHON
df = pd.read_csv(data)
```

Sie können auch aus einer JSON-Datei importieren. Das `data` Argument ist der Pfad zur CSV-Datei. Diese Variable wurde aus dem `configProperties` im [vorherigen Abschnitt](#configuration-files)importiert.

```PYTHON
df = pd.read_json(data)
```

Jetzt befinden sich Ihre Daten im DataFrame-Objekt und können im [nächsten Abschnitt](#data-preparation-and-feature-engineering)analysiert und bearbeitet werden.

### Von Data Access SDK (nicht mehr unterstützt)

>[!CAUTION]
> `data_access_sdk_python` wird nicht mehr empfohlen. Eine Anleitung zur Verwendung des Datenladeprogramms finden Sie unter [Datenzugriffscode in Platform-SDK](../authoring/platform-sdk.md) konvertieren `platform_sdk` .

Benutzer können Daten mit dem Data Access SDK laden. Die Bibliothek kann oben auf der Seite importiert werden, indem die folgende Zeile eingefügt wird:

`from data_access_sdk_python.reader import DataSetReader`

Anschließend verwenden wir die `load()` Methode, um den Schulungsdatensatz aus der `trainingDataSetId` Konfiguration (`recipe.conf`) zu erfassen.

```PYTHON
prodreader = DataSetReader(client_id=configProperties['ML_FRAMEWORK_IMS_USER_CLIENT_ID'],
                           user_token=configProperties['ML_FRAMEWORK_IMS_TOKEN'],
                           service_token=configProperties['ML_FRAMEWORK_IMS_ML_TOKEN'])

df = prodreader.load(data_set_id=configProperties['trainingDataSetId'],
                     ims_org=configProperties['ML_FRAMEWORK_IMS_TENANT_ID'])
```

>[!NOTE]
>Wie im Abschnitt [Konfigurationsdatei](#configuration-files)erwähnt, werden die folgenden Konfigurationsparameter für Sie festgelegt, wenn Sie Daten aus [!DNL Experience Platform]den folgenden Quellen aufrufen:
> - `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
> - `ML_FRAMEWORK_IMS_TOKEN`
> - `ML_FRAMEWORK_IMS_ML_TOKEN`
> - `ML_FRAMEWORK_IMS_TENANT_ID`


Jetzt, da Sie über Ihre Daten verfügen, können Sie mit der Datenvorbereitung und der Funktionstechnik beginnen.

### Datenvorbereitung und Funktionstechnik {#data-preparation-and-feature-engineering}

Nach dem Laden der Daten werden die Daten vorbereitet und in die `train` und die `val` Datensätze aufgeteilt. Beispiel-Code:

```PYTHON
#########################################
# Data Preparation/Feature Engineering
#########################################
dataframe.date = pd.to_datetime(dataframe.date)
dataframe['week'] = dataframe.date.dt.week
dataframe['year'] = dataframe.date.dt.year

dataframe = pd.concat([dataframe, pd.get_dummies(dataframe['storeType'])], axis=1)
dataframe.drop('storeType', axis=1, inplace=True)
dataframe['isHoliday'] = dataframe['isHoliday'].astype(int)

dataframe['weeklySalesAhead'] = dataframe.shift(-45)['weeklySales']
dataframe['weeklySalesLag'] = dataframe.shift(45)['weeklySales']
dataframe['weeklySalesDiff'] = (dataframe['weeklySales'] - dataframe['weeklySalesLag']) / dataframe['weeklySalesLag']
dataframe.dropna(0, inplace=True)

dataframe = dataframe.set_index(dataframe.date)
dataframe.drop('date', axis=1, inplace=True) 
```

In diesem Beispiel werden dem ursprünglichen Datensatz fünf Dinge angefertigt:
- Hinzufügen `week` und `year` Spalten
- in `storeType` eine Indikatorvariable konvertieren
- in `isHoliday` eine numerische Variable konvertieren
- Offset `weeklySales` für den zukünftigen und vorherigen Verkaufswert
- Daten nach Datum, zu `train` und `val` Datensatz aufteilen

Erstens werden `week` und `year` Spalten erstellt und die ursprüngliche `date` Spalte in [!DNL Python] datetime [](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.to_datetime.html)konvertiert. Wochen- und Jahreswerte werden aus dem datetime-Objekt extrahiert.

Als Nächstes `storeType` werden drei Spalten umgewandelt, die die drei verschiedenen Speichertypen (`A`, `B`und `C`) darstellen. Jede enthält einen booleschen Wert für den Status, der &quot;true&quot; `storeType` lautet. Die `storeType` Spalte wird abgelegt.

Gleichermaßen `weeklySales` ändert sich der `isHoliday` boolesche Wert in eine numerische Darstellung, eine oder Null.

Diese Daten werden zwischen `train` und `val` Datensatz aufgeteilt.

Die `load()` Funktion sollte mit dem Datensatz `train` und dem `val` Datensatz als Ausgabe abgeschlossen werden.

### Datenlader für die Auswertung {#scoring-data-loader}

Das Laden von Daten für die Auswertung ist ähnlich wie das Laden von Schulungsdaten in der `split()` Funktion. Wir verwenden das Data Access SDK, um Daten aus der `scoringDataSetId` Datei in unserer `recipe.conf` Datei zu laden.

```PYTHON
def load(configProperties):

    print("Scoring Data Load Start")

    #########################################
    # Load Data
    #########################################
    prodreader = DataSetReader(client_id=configProperties['ML_FRAMEWORK_IMS_USER_CLIENT_ID'],
                               user_token=configProperties['ML_FRAMEWORK_IMS_TOKEN'],
                               service_token=configProperties['ML_FRAMEWORK_IMS_ML_TOKEN'])

    df = prodreader.load(data_set_id=configProperties['scoringDataSetId'],
                         ims_org=configProperties['ML_FRAMEWORK_IMS_TENANT_ID'])
```

Nach dem Laden der Daten erfolgt die Datenvorbereitung und die Funktionstechnik.

```PYTHON
#########################################
# Data Preparation/Feature Engineering
#########################################
df.date = pd.to_datetime(df.date)
df['week'] = df.date.dt.week
df['year'] = df.date.dt.year

df = pd.concat([df, pd.get_dummies(df['storeType'])], axis=1)
df.drop('storeType', axis=1, inplace=True)
df['isHoliday'] = df['isHoliday'].astype(int)

df['weeklySalesAhead'] = df.shift(-45)['weeklySales']
df['weeklySalesLag'] = df.shift(45)['weeklySales']
df['weeklySalesDiff'] = (df['weeklySales'] - df['weeklySalesLag']) / df['weeklySalesLag']
df.dropna(0, inplace=True)

df = df.set_index(df.date)
df.drop('date', axis=1, inplace=True)

print("Scoring Data Load Finish")

return df
```

Da der Zweck unseres Modells darin besteht, zukünftige wöchentliche Verkäufe vorherzusagen, müssen Sie einen Bewertungsdatensatz erstellen, mit dem bewertet wird, wie gut die Vorhersage des Modells funktioniert.

Dieses Recipe Builder-Notebook macht dies, indem wir unseren wöchentlichen Umsatz 7 Tage vorwärts verrechnen. Beachten Sie, dass wöchentlich 45 Speicher gemessen werden, sodass Sie die `weeklySales` Werte 45 Datensätze vorwärts in eine neue Spalte namens `weeklySalesAhead`verschieben können.

```PYTHON
df['weeklySalesAhead'] = df.shift(-45)['weeklySales']
```

Auf ähnliche Weise können Sie eine Spalte `weeklySalesLag` durch Verschiebung 45 nach hinten erstellen. Auf diese Weise können Sie auch den Unterschied im Wochenverkauf berechnen und in der Spalte speichern `weeklySalesDiff`.

```PYTHON
df['weeklySalesLag'] = df.shift(45)['weeklySales']
df['weeklySalesDiff'] = (df['weeklySales'] - df['weeklySalesLag']) / df['weeklySalesLag']
```

Da Sie die `weeklySales` Datenpunkte 45 und 45 Datensätze rückwärts verschieben, um neue Spalten zu erstellen, haben die ersten und letzten 45 Datenpunkte NaN-Werte. Sie können diese Punkte aus unserem Datensatz entfernen, indem Sie die `df.dropna()` Funktion verwenden, die alle Zeilen mit NaN-Werten entfernt.

```PYTHON
df.dropna(0, inplace=True)
```

Die `load()` Funktion in Ihrer Datenladefunktion sollte mit dem Bewertungsdataset als Ausgabe abgeschlossen werden.

### Pipeline-Datei {#pipeline-file}

Die `pipeline.py` Datei enthält eine Logik für Schulung und Bewertung.

### Schulung {#training}

Der Zweck der Schulung besteht darin, ein Modell mithilfe von Funktionen und Beschriftungen in Ihrem Schulungsdatensatz zu erstellen.

>[!NOTE]\
>_Funktionen_ beziehen sich auf die Eingabevariable, die vom maschinellen Lernmodell zur Vorhersage der _Beschriftungen_ verwendet wird.

Die `train()` Funktion sollte das Schulungsmodell enthalten und das geschulte Modell zurückgeben. Einige Beispiele für verschiedene Modelle finden Sie in der Dokumentation [des](https://scikit-learn.org/stable/user_guide.html)Benutzerhandbuchszum Scikit-Lernen.

Nach der Auswahl Ihres Schulungsmodells passen Sie Ihr x- und y-Schulungsdatensatz an das Modell und die Funktion gibt das geschulte Modell zurück. Ein Beispiel, das Folgendes zeigt:

```PYTHON
def train(configProperties, data):

    print("Train Start")

    #########################################
    # Extract fields from configProperties
    #########################################
    learning_rate = float(configProperties['learning_rate'])
    n_estimators = int(configProperties['n_estimators'])
    max_depth = int(configProperties['max_depth'])


    #########################################
    # Fit model
    #########################################
    X_train = data.drop('weeklySalesAhead', axis=1).values
    y_train = data['weeklySalesAhead'].values

    seed = 1234
    model = GradientBoostingRegressor(learning_rate=learning_rate,
                                      n_estimators=n_estimators,
                                      max_depth=max_depth,
                                      random_state=seed)

    model.fit(X_train, y_train)

    print("Train Complete")

    return model
```

Beachten Sie, dass je nach Anwendung Argumente in Ihrer `GradientBoostingRegressor()` Funktion vorhanden sind. `xTrainingDataset` sollte Ihre für Schulungen verwendeten Funktionen enthalten, während die Beschriftungen enthalten sein `yTrainingDataset` sollten.

### Bewertung {#scoring}

Die `score()` Funktion sollte den Bewertungsalgorithmus enthalten und eine Messung zurückgeben, um anzugeben, wie erfolgreich das Modell funktioniert. Die `score()` Funktion verwendet die Beschriftungen des Bewertungsdatasets und das geschulte Modell, um eine Reihe vorhergesagter Funktionen zu generieren. Diese prognostizierten Werte werden dann mit den tatsächlichen Funktionen im Bewertungsdatensatz verglichen. In diesem Beispiel verwendet die `score()` Funktion das geschulte Modell, um Funktionen mithilfe der Beschriftungen des Bewertungsdatasets vorherzusagen. Die prognostizierten Funktionen werden zurückgegeben.

```PYTHON
def score(configProperties, data, model):

    print("Score Start")

    X_test = data.drop('weeklySalesAhead', axis=1).values
    y_test = data['weeklySalesAhead'].values
    y_pred = model.predict(X_test)

    data['prediction'] = y_pred
    data = data[['store', 'prediction']].reset_index()
    data['date'] = data['date'].astype(str)

    print("Score Complete")

    return data
```

### Evaluator-Datei {#evaluator-file}

Die `evaluator.py` Datei enthält eine Logik, wie Sie Ihr geschultes Rezept bewerten und wie Ihre Schulungsdaten aufgeteilt werden sollen. Im Einzelhandelsbeispiel wird die Logik zum Laden und Vorbereiten der Schulungsdaten einbezogen. Wir gehen über die beiden folgenden Abschnitte.

### Datensatz teilen {#split-the-dataset}

Die Vorbereitung der Daten für Schulungen erfordert die Aufteilung des Datensatzes, der für Schulungen und Tests verwendet werden soll. Diese `val` Daten werden implizit verwendet, um das Modell nach dessen Schulung zu bewerten. Dieser Prozess ist von der Bewertung getrennt.

Dieser Abschnitt zeigt die `split()` Funktion, die zuerst Daten in das Notebook lädt und dann die Daten bereinigt, indem sie nicht verwandte Spalten im Datensatz entfernt. Von dort aus können Sie die Funktionstechnik durchführen, die die Erstellung zusätzlicher relevanter Funktionen aus den vorhandenen Rohdaten ermöglicht. Ein Beispiel für diesen Vorgang ist unten zusammen mit einer Erklärung zu sehen.

Die `split()` Funktion ist unten dargestellt. Das im Argument bereitgestellte Datenformat wird in die zurückzugebenden `train` und- `val` Variablen aufgeteilt.

```PYTHON
def split(self, configProperties={}, dataframe=None):
    train_start = '2010-02-12'
    train_end = '2012-01-27'
    val_start = '2012-02-03'
    train = dataframe[train_start:train_end]
    val = dataframe[val_start:]

    return train, val
```

### Bewerten Sie das geschulte Modell. {#evaluate-the-trained-model}

Die `evaluate()` Funktion wird ausgeführt, nachdem das Modell trainiert wurde, und gibt eine Metrik zurück, die angibt, wie erfolgreich das Modell funktioniert. Die `evaluate()` Funktion verwendet die Testdataset-Bezeichnungen und das Trainingsmodell, um eine Reihe von Funktionen vorherzusagen. Diese prognostizierten Werte werden dann mit den tatsächlichen Funktionen im Testdatensatz verglichen. Häufige Bewertungsalgorithmen sind:
- [Mittlerer absoluter prozentualer Fehler (MAPE)](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error)
- [Mittlerer absoluter Fehler](https://en.wikipedia.org/wiki/Mean_absolute_error)
- [Root-medium-square error (RMSE)](https://en.wikipedia.org/wiki/Root-mean-square_deviation)


Die `evaluate()` Funktion in der Stichprobe für Einzelhandelsverkäufe ist unten dargestellt:

```PYTHON
def evaluate(self, data=[], model={}, configProperties={}):
    print ("Evaluation evaluate triggered")
    val = data.drop('weeklySalesAhead', axis=1)
    y_pred = model.predict(val)
    y_actual = data['weeklySalesAhead'].values
    mape = np.mean(np.abs((y_actual - y_pred) / y_actual))
    mae = np.mean(np.abs(y_actual - y_pred))
    rmse = np.sqrt(np.mean((y_actual - y_pred) ** 2))

    metric = [{"name": "MAPE", "value": mape, "valueType": "double"},
                {"name": "MAE", "value": mae, "valueType": "double"},
                {"name": "RMSE", "value": rmse, "valueType": "double"}]

    return metric
```

Beachten Sie, dass die Funktion ein `metric` Objekt zurückgibt, das ein Array von Bewertungsmetriken enthält. Anhand dieser Metriken wird bewertet, wie gut das geschulte Modell funktioniert.

### Datenspeicherdatei {#data-saver-file}

Die `datasaver.py` Datei enthält die `save()` Funktion zum Speichern Ihrer Prognose während des Testens der Bewertung. Die `save()` Funktion nimmt Ihre Vorhersage vor und schreibt mithilfe von [!DNL Experience Platform Catalog] APIs die Daten in die von `scoringResultsDataSetId` Ihnen in der `scoring.conf` Datei angegebene Datei.

Das Beispiel, das im Rezept für Einzelhandelsverkäufe verwendet wird, ist hier dargestellt. Beachten Sie die Verwendung der `DataSetWriter` Bibliothek zum Schreiben von Daten in die Platform:

```PYTHON
from data_access_sdk_python.writer import DataSetWriter

def save(configProperties, prediction):
    print("Datasaver Start")
    print("Setting up Writer")

    catalog_url = "https://platform.adobe.io/data/foundation/catalog"
    ingestion_url = "https://platform.adobe.io/data/foundation/import"

    writer = DataSetWriter(catalog_url=catalog_url,
                           ingestion_url=ingestion_url,
                           client_id=configProperties['ML_FRAMEWORK_IMS_USER_CLIENT_ID'],
                           user_token=configProperties['ML_FRAMEWORK_IMS_TOKEN'],
                           service_token=configProperties['ML_FRAMEWORK_IMS_ML_TOKEN'])

    print("Writer Configured")

    writer.write(data_set_id=configProperties['scoringResultsDataSetId'],
                 dataframe=prediction,
                 ims_org=configProperties['ML_FRAMEWORK_IMS_TENANT_ID'])

    print("Write Done")
    print("Datasaver Finish")
    print(prediction)
```

## Ausbildung und Punktesystem {#training-and-scoring}

Wenn Sie Ihre Änderungen an Ihrem Notebook vorgenommen haben und Ihr Rezept trainieren möchten, können Sie auf die entsprechenden Schaltflächen oben in der Leiste klicken, um einen Schulungslauf in der Zelle zu erstellen. Wenn Sie auf die Schaltfläche klicken, wird ein Protokoll mit Befehlen und Ausgängen aus dem Schulungsskript im Notebook (unter der `evaluator.py` Zelle) angezeigt. Conda installiert zuerst alle Abhängigkeiten, dann wird die Schulung initiiert.

Beachten Sie, dass Sie mindestens einmal eine Schulung ausführen müssen, bevor Sie die Punktbewertung durchführen können. Wenn Sie auf die Schaltfläche &quot;Punktzahl **[!UICONTROL ausführen]** &quot;klicken, wird das trainierte Modell bewertet, das während der Schulung generiert wurde. Das Bewertungsskript wird unter `datasaver.py`angezeigt.

Wenn Sie zum Debugging die ausgeblendete Ausgabe anzeigen möchten, fügen Sie sie `debug` zum Ende der Ausgabenzelle hinzu und führen Sie sie erneut aus.

## Rezept erstellen {#create-recipe}

Wenn Sie die Bearbeitung des Rezepts abgeschlossen haben und mit der Schulungs-/Bewertungsausgabe zufrieden sind, können Sie ein Rezept aus dem Notebook erstellen, indem Sie in der Navigation oben rechts auf Rezept **[!UICONTROL erstellen]** klicken.

![](../images/jupyterlab/create-recipe/create-recipe.png)

Nach dem Klicken auf die Schaltfläche werden Sie aufgefordert, einen Rezeptnamen einzugeben. Dieser Name stellt das eigentliche Rezept dar, das am [!DNL Platform].

![](../images/jupyterlab/create-recipe/enter_recipe_name.png)

Wenn Sie **[!UICONTROL OK]** drücken, können Sie auf der [Adobe Experience Platform](https://platform.adobe.com/)zu dem neuen Rezept navigieren. Sie können auf die Schaltfläche **[!UICONTROL Ansicht Rezepte]** klicken, um zur Registerkarte **[!UICONTROL Rezepte]** unter **[!UICONTROL ML-Modelle zu gelangen]**

![](../images/jupyterlab/create-recipe/recipe_creation_started.png)

Sobald der Prozess abgeschlossen ist, sieht das Rezept wie folgt aus:

![](../images/jupyterlab/create-recipe/recipe_details.png)

>[!CAUTION]
> - Löschen Sie keine der Dateizellen
> - Bearbeiten Sie nicht die `%%writefile` Zeile oben in den Dateizellen
> - Erstellen Sie nicht gleichzeitig Rezepte in verschiedenen Notebooks


## Nächste Schritte {#next-steps}

Mit diesem Lernprogramm haben Sie gelernt, wie Sie ein Modell für maschinelles Lernen im Rezept Builder-Notebook erstellen können. Sie haben auch gelernt, wie Sie das Notebook mit dem Rezept-Workflow im Notebook ausüben können, um ein Rezept in [!DNL Data Science Workspace]Ihrem Notebook zu erstellen.

Um weiter zu lernen, wie man mit Ressourcen innerhalb von zu arbeiten, besuchen Sie [!DNL Data Science Workspace]bitte das Dropdown-Menü [!DNL Data Science Workspace] Rezepte und Modelle.

## Zusätzliche Ressourcen {#additional-resources}

Das folgende Video unterstützt Sie beim Erstellen und Bereitstellen von Modellen.

>[!VIDEO](https://video.tv.adobe.com/v/30575?quality=12&enable10seconds=on&speedcontrol=on)


