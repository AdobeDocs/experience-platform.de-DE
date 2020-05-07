---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;node reference;
solution: Experience Platform
title: Ausbildung eines Modells für maschinelles Echtzeit-Lernen
topic: Training a ML model
translation-type: tm+mt
source-git-commit: dd2c9714c410d00ef2ba06e9f9728747fc6f989a
workflow-type: tm+mt
source-wordcount: '1537'
ht-degree: 0%

---


# Ausbildung eines Modells für maschinelles Echtzeit-Lernen

>[!IMPORTANT]
>Das maschinelle Lernen in Echtzeit steht noch nicht allen Benutzern zur Verfügung. Diese Funktion ist alphanumerisch und wird noch getestet. Dieses Dokument kann sich ändern.

Dieses Dokument bietet eine Anleitung zum Hochladen eines ONNX-Modells in den Store für maschinelles Lernen in Echtzeit.

Mithilfe einer der folgenden Optionen schreiben Sie Python-Code, um Daten zu lesen, vorbereiten und zu analysieren. Als Nächstes müssen Sie Ihr eigenes ML-Modell trainieren, es in das ONNX-Format serialisieren und es schließlich in den Real-time Machine Learning Model Store hochladen. Außerdem erhalten Sie am Ende des Lernprogramms eine Modell-ID, mit der das geschulte Modell für die Verwendung im [Bewertungslehrgang](./scoring-ml-model.md)identifiziert wird.

* [Training eines Modells mit einem Python-Notebook](#training-model-python-notebook)
* [Training eines Modells mit einem eigenen ONNX-Modell](#train-using-own-onnx-model)
* [Schulung eines Modells mithilfe der Rezept-Builder-Vorlage](#train-using-recipe-builder)
* [Schulung eines Modells mithilfe des Arbeitsablaufs für Datenwissenschaften](#recipe-workflow-train-model)


## Modell mit einem Python-Notebook trainieren {#training-model-python-notebook}

Wählen Sie in der Benutzeroberfläche der Adobe Experience Platform **[!UICONTROL Notebooks]** in der *Datenwissenschaft* aus. Wählen Sie als Nächstes &quot; **[!UICONTROL JupyterLab]** &quot;aus und lassen Sie die Umgebung etwas länger laden.

![open JupyterLab](../images/rtml/open-jupyterlab.png)

Beginn durch Auswahl des **leeren Python 3 Notebooks** im JupyterLab-Starter.

![leere Python](../images/rtml/python-blank.png)

### Zugriffsdaten {#access-data}

Wählen Sie anschließend den Datensatz aus, den Sie verwenden möchten. Um auf ein Dataset in Ihrem JupyterLab-Notebook zuzugreifen, wählen Sie in der linken Navigation von JupyterLab die Registerkarte &quot; **Daten** &quot;aus. Die Ordner *Datasets* und *Schemas* werden angezeigt. Wählen Sie &quot; **[!UICONTROL Datensätze]** &quot;und klicken Sie mit der rechten Maustaste und wählen Sie dann im Dropdown-Menü des zu verwendenden Datensatzes die Option &quot;Daten im Notebook **** untersuchen&quot;. Ein ausführbarer Code-Eintrag wird in Ihrem Notebook angezeigt.

![Datenzugriff](../images/rtml/access-dataset.png)

### Vorbereiten des Modells

Verwenden Sie die folgende Vorlage, um Ihr ML-Modell zu analysieren, vorzubereiten, auszubilden und zu bewerten. Für ein vollständiges Beispiel verwenden Sie die folgenden Screenshots:

```python
from sklearn import svm, metrics
from sklearn.model_selection import train_test_split


data = df[input_columns]
target = df[target_column]
# Create a classifier: a support vector classifier
classifier = svm.SVC(gamma=0.001)

# Split data into train and test subsets
X_train, X_test, y_train, y_test = train_test_split(
    data, target, test_size=0.5, shuffle=False)

# We train the classifier
classifier.fit(X_train, y_train)

# Now do predictions
predicted = classifier.predict(X_test)


print("Classification report for classifier %s:\n%s\n"
      % (classifier, metrics.classification_report(y_test, predicted)))
disp = metrics.plot_confusion_matrix(classifier, X_test, y_test)
disp.figure_.suptitle("Confusion Matrix")
print("Confusion matrix:\n%s" % disp.confusion_matrix)
```

>[!NOTE]
>Im folgenden Beispiel wird die &quot;scikit-learn&quot;-Bibliothek verwendet, anstatt die Daten aus einem erfassten Adobe Experience Platform-Datensatz zu laden.

![install scikit](../images/rtml/install-scikit.png)-![Schulungsbeispiel](../images/rtml/train-example.png)

**Ausgabe**

![Ausgabe für scikit](../images/rtml/train-example-response.png)

### Hochladen des Modells

Nachdem Sie den vorherigen Schritt abgeschlossen haben, müssen Sie Ihr Modell in ein ONNX-Format serialisieren und es in den Echtzeit-Store für maschinelles Lernen hochladen. Dadurch wird der `model_id` , der im [nächsten Lernprogramm](#next-steps)verwendet wird, zurückgegeben.

Verwenden Sie die folgende Vorlage, um in ONNX zu konvertieren und Ihren Datensatz hochzuladen:

```python
from rtml_nodelibs.nodes.standard.ml.artifact_utils
import ModelUpload
from rtml_nodelibs.core.nodefactory
import NodeFactory as nf
from skl2onnx.common.data_types
import FloatTensorType
from skl2onnx
import convert_sklearn

########## Save sklearn model in ONNX format at model_path ##########
inputs = [('features', FloatTensorType([None, X_train.shape[1]]))]
model_onnx = convert_sklearn(classifier, 'ScikitLearnModel', inputs)

model_path = "model.onnx"
os.environ["ONNX_MODEL_PATH"] = model_path

with open(model_path, "wb") as f:
  f.write(model_onnx.SerializeToString())

  ########## Upload the model from model_path to RTML model store ##########
  model = ModelUpload(params = {
    'model_path': model_path
  })

msg_model = model.process(None, 1)

model_id = msg_model.model['model_id']

print("Model ID : ", model_id)
```

**Antwort**

![model id](../images/rtml/model-id.png)

Nachdem Sie Ihren Bericht erhalten haben, kopieren Sie ihn `model_id`und fahren Sie mit den [nächsten Schritten](#next-steps)fort.


## Training eines Modells mit einem eigenen ONNX-Modell {#train-using-own-onnx-model}

Wählen Sie in der Benutzeroberfläche der Adobe Experience Platform **[!UICONTROL Notebooks]** in der *Datenwissenschaft* aus. Wählen Sie als Nächstes &quot; **[!UICONTROL JupyterLab]** &quot;aus und lassen Sie die Umgebung etwas länger laden.

![open JupyterLab](../images/rtml/open-jupyterlab.png)

Laden Sie das ONNX-Modell mit der Upload-Schaltfläche in JupyterLab-Notebooks in die Umgebung Data Science Workspace hoch.

![Upload-Symbol](../images/rtml/upload.png)

Erstellen Sie anschließend ein neues leeres Notebook, indem Sie im JupyterLab-Starter unter Python 3 das leere Notizbuchsymbol auswählen.

![leere Python](../images/rtml/python-blank.png)

Kopieren Sie in das leere Notebook Folgendes und fügen Sie es ein:

>[!NOTE]
> Stellen Sie sicher, dass Sie die `model_path` von Ihnen hochgeladene Version des ONNX-Modells angeben.

```python
from rtml_nodelibs.nodes.standard.ml.artifact_utils import ModelUpload
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
 
model_path = <path/to/onnx_model>
########## Upload the model from model_path to RTML model store ##########
model = ModelUpload(params={'model_path': model_path})
 
msg_model = model.process(None, 1)
 
model_id = msg_model.model['model_id']
 
print("Model ID : ", model_id)
```

Nachdem die Zelle oben ausgeführt wurde, `model_id` wird eine zurückgegeben. Kopieren Sie die Modell-ID, die im [nächsten Lernprogramm](#next-steps)verwendet werden soll.

## Erstellen eines Modells mithilfe einer vordefinierten Rezeptvorlage {#train-using-recipe-builder}

Wählen Sie in der Benutzeroberfläche der Adobe Experience Platform **[!UICONTROL Notebooks]** in der *Datenwissenschaft* aus. Wählen Sie als Nächstes &quot; **[!UICONTROL JupyterLab]** &quot;aus und lassen Sie die Umgebung etwas länger laden.

![open JupyterLab](../images/rtml/open-jupyterlab.png)

Anschließend folgen Sie dem Lernprogramm Jupyter-Notebooks, um ein Rezept zu [erstellen](../jupyterlab/create-a-recipe.md) . Nach Abschluss des Vorgangs müssen Sie die Datei &quot;pipelines.py&quot;ändern, damit die inferencing-Funktion in Echtzeit funktioniert.

>[!NOTE]
>Die von Data Science Workspace bereitgestellte Vorlage muss an Ihren Datensatz angepasst werden.

Achten Sie darauf, Ihr Modell im ONNX-Format zu speichern und die Variable &quot;Umgebung&quot;auf `ONNX_MODEL_PATH`. Das unten stehende Beispiel zeigt, wie die Pipeline-Datei mithilfe der Rezept-Builder-Vorlage geändert wird.

```python
def train(configProperties, data):

  print("Train Start")

########## Extract fields from configProperties ##########
learning_rate = float(configProperties['learning_rate'])
n_estimators = int(configProperties['n_estimators'])
max_depth = int(configProperties['max_depth'])

########## Fit model ##########
X_train = data.drop('weeklySalesAhead', axis = 1).values
y_train = data['weeklySalesAhead'].values

seed = 1234
model = GradientBoostingRegressor(learning_rate = learning_rate,
  n_estimators = n_estimators,
  max_depth = max_depth,
  random_state = seed)

model.fit(X_train, y_train)

########## Save sklearn model in ONNX format at model_path ##########
inputs = [('features', FloatTensorType([None, X_train.shape[1]]))]
model_onnx = convert_sklearn(model, 'ScikitLearnModel', inputs)

model_path = "retail_sales_model.onnx"
os.environ["ONNX_MODEL_PATH"] = model_path

with open(model_path, "wb") as f:
  f.write(model_onnx.SerializeToString())

print("Train Complete")

return model
```

Führen Sie nach dem Ändern der Datei &quot;pipelines.py&quot; **[!UICONTROL Training]** und **[!UICONTROL Scoring]** aus. Klicken Sie nach Abschluss des Vorgangs auf die Schaltfläche &quot;Rezept **[!UICONTROL erstellen]** &quot;.

![Schaltflächen für Schulung und Bewertung](../images/rtml/train-score.png)

Ein Benennungsdialogfeld wird angezeigt. Geben Sie den Namen Ihres Rezepts ein und wählen Sie &quot; **[!UICONTROL OK&quot;]**. Es wird ein neuer Dialog angezeigt, in dem Sie darauf hingewiesen werden, dass die Rezepterstellung begonnen hat. Warten Sie einige Zeit, bis das Rezept erstellt wurde.

![Dialogfeld &quot;Rezept&quot;](../images/rtml/recipe-dialog.png)

![Dialogfeld &quot;Rezept&quot;](../images/rtml/recipe-dialog-confrim.png)

Nachdem ein Rezept erstellt wurde, kann es angezeigt werden, indem **[!UICONTROL Ansicht Rezepte]** im angezeigten Dialogfeld ausgewählt werden oder indem Sie zu **[!UICONTROL Modelle]** navigieren und dann **[!UICONTROL Rezepte]** oben links wählen. Eine nach Erstellungsdatum sortierte Liste von Rezepten wird angezeigt. Vergewissern Sie sich, dass Ihr neues Rezept oben steht.

![Ihr Rezept](../images/rtml/view-recipe.png)

Wählen Sie Ihr Rezept aus. Die Seite &quot;Skriptübersicht&quot;wird angezeigt. Wählen Sie in der oberen rechten Navigation **[!UICONTROL Modell]** erstellen.

![Rezept - Übersicht](../images/rtml/create-model.png)

Wählen Sie anschließend einen entsprechenden Datensatz aus. Klicken Sie dann in der Navigation oben rechts auf **[!UICONTROL Weiter]** .

![Datensatz auswählen](../images/rtml/select-dataset.png)

Die Konfigurationsseite wird geöffnet. Geben Sie einen Namen für das Modell ein und überprüfen Sie die Standardmodellkonfigurationen. Standardkonfigurationen werden während der Rezepterstellung angewendet. Überprüfen und ändern Sie die Konfigurationswerte, indem Sie mit der Dublette auf die Werte klicken. Um einen neuen Konfigurationssatz bereitzustellen, klicken Sie auf Neue Konfiguration **[!UICONTROL hochladen]** und ziehen Sie eine JSON-Datei mit Modellkonfigurationen in das Browserfenster. Wählen Sie **[!UICONTROL Fertig stellen]** , um das Modell zu erstellen.

![Modell konfigurieren](../images/rtml/configure-model.png)

Nachdem das Modell erstellt wurde, müssen Sie warten, bis der Schulungslauf abgeschlossen ist. Nach Abschluss eines erfolgreichen Schulungslaufs können Sie den Schulungslauf zur Ansicht der Details auswählen.

Wählen Sie einen Schulungslauf aus. Nach der Auswahl wird rechts ein Eigenschaftendialogfeld angezeigt. Wählen Sie in diesem Dialogfeld die Option **[!UICONTROL Ansicht Aktivität Logs]**.

![Ansichten](../images/rtml/view-training.png)

Das Popup-Fenster &quot;Protokolle zur Aktivität der *Ansicht* &quot;wird angezeigt. Wählen Sie die URL für die *Stderprotokolle* aus, um die Protokolle herunterzuladen und die Details der Ausführung anzuzeigen.

![Ansichten](../images/rtml/view-logs.png)

Protokolle sind besonders nützlich für fehlgeschlagene Ausführung, um zu sehen, was schiefgelaufen ist. Aber in diesem Fall suchen Sie nach dem `model-id` passenden ONNX-Modell. Kopieren Sie die Modell-ID.

>[!NOTE]
>Sie müssen keinen Bewertungsauftrag ausführen. Im [nächsten Schritt](#next-steps)wird die Edge-Bewertung für maschinelles Lernen in Echtzeit behandelt.

![Modell-ID suchen](../images/rtml/find-model-id-logs.png)

## Schulung eines Modells mithilfe des Arbeitsablaufs für Datenwissenschaften {#recipe-workflow-train-model}

Dies ist die beste Methode, wenn Sie mit Docker, Git und Packen Python-Code vertraut sind. Die Verwendung des Arbeitsablaufs &quot;Data Science Workspace&quot;bietet Ihnen die größtmögliche Flexibilität und Freiheit bei der Erstellung Ihrer Rezepte. Sie können ein Basisdockerbild ziehen und eine eigene Docker-Umgebung erstellen, Ihr Rezept einfacher debuggen, vorgefertigte Rezepte klonen, um sie mit jedem Data Science Workspace-Dienst herum abspielen zu können, die Ausführung des Skripts planen und vieles mehr.

### Schema erstellen

Für den ersten Schritt müssen Sie über ein Schema für Ihre Daten verfügen. Ein Schema kann über die Benutzeroberfläche oder Plattform-APIs von Adobe Experience Platform erstellt werden.

>[!NOTE]
>Wenn Sie bereits über die Daten verfügen, die Sie in Adobe Experience Platform verwenden möchten, überspringen Sie die [Erstellung eines Python-Rezepts](#create-a-python-recipe).

* [Erstellen eines Schemas mithilfe des Schema-Editor-Lernprogramms](../../xdm/tutorials/create-schema-ui.md)
* [Erstellen eines Schemas mithilfe des Schema-Editor-API-Tutorials](../../xdm/tutorials/create-schema-api.md)

### Daten erfassen

Als Nächstes müssen Sie Daten mit dem soeben erstellten Schema erfassen. Dies kann über die API oder die Plattform-Benutzeroberfläche erfolgen.

>[!NOTE]
>Wenn Sie bereits über die Daten verfügen, die Sie in Adobe Experience Platform verwenden möchten, überspringen Sie die [Erstellung eines Python-Rezepts](#create-a-python-recipe).

* [Daten in das Lernprogramm zur Benutzeroberfläche der Adobe Experience Platform integrieren](../../ingestion/tutorials/ingest-batch-data.md)
* [Daten in das Lernprogramm zur Adobe Experience Platform API einbeziehen](../../ingestion/batch-ingestion/api-overview.md)

### Erstellen eines Python-Rezepts {#create-a-python-recipe}

Beginn zur Rezepterstellung mit Quelldateien zum Erstellen einer Archivdatei. Quelldateien definieren die Logik des maschinellen Lernens und Algorithmen, die zur Lösung eines bestimmten Problems verwendet werden. Verwenden Sie das folgende Lernprogramm, um ein Python Docker-Bild zu erstellen.

* [Verpacken von Quelldateien in einem Rezept](../models-recipes/package-source-files-recipe.md)

Um den nächsten Schritt abzuschließen, benötigen Sie ein Docker-Bild in einer Azurblauen Container-Registrierung zusammen mit der entsprechenden Bild-URL. Wählen Sie einen der folgenden Links zum Erstellen eines Python-Skripts aus:

* [Verpacktes Rezept in die Benutzeroberfläche importieren](../models-recipes/import-packaged-recipe-ui.md)
* [Verpacktes Rezept mit der API importieren](../models-recipes/import-packaged-recipe-api.md)

### Erstellen eines Schulungslaufs

In Adobe Experience Platform Data Science Workspace wird ein Modell für maschinelles Lernen erstellt, indem ein vorhandenes Rezept integriert wird, das für die Absicht des Modells geeignet ist. Anschließend wird das Modell trainiert und bewertet, um seine Betriebseffizienz und Wirksamkeit zu optimieren, indem die zugehörigen Hyperparameter präzisiert werden.

* [Erstellen und Auswerten eines Modells in der Benutzeroberfläche](../models-recipes/train-evaluate-model-ui.md)
* [Erstellen und Auswerten eines Modells in der API](../models-recipes/train-evaluate-model-api.md)

>[!IMPORTANT]
>Speichern Sie das Modell in der Datei &quot;ipipipeline.py&quot;für Ihr Rezept im ONNX-Format `model_path` und setzen Sie die Variable &quot;Umgebung&quot;auf `ONNX_MODEL_PATH`. Die Laufzeitumgebung sucht nach dieser spezifischen Umgebung-Variablen.

```python
def train(configProperties, data):
 
    print("Train Start")
 
    ########## Extract fields from configProperties ##########

    learning_rate = float(configProperties['learning_rate'])
    n_estimators = int(configProperties['n_estimators'])
    max_depth = int(configProperties['max_depth'])
 
 
    
    ########## Fit model ##########
    
    X_train = data.drop('weeklySalesAhead', axis=1).values
    y_train = data['weeklySalesAhead'].values
 
    seed = 1234
    model = GradientBoostingRegressor(learning_rate=learning_rate,
                                      n_estimators=n_estimators,
                                      max_depth=max_depth,
                                      random_state=seed)
 
    model.fit(X_train, y_train)
     
    ########## Save sklearn model in ONNX format at model_path ##########
    inputs = [('features', FloatTensorType([None, X_train.shape[1]]))]
    model_onnx = convert_sklearn(model, 'ScikitLearnModel', inputs)
 
    model_path = "retail_sales_model.onnx"
    os.environ["ONNX_MODEL_PATH"] = model_path
 
    with open(model_path, "wb") as f:
        f.write(model_onnx.SerializeToString())
 
    print("Train Complete")
 
    return model
```

Nachdem das Modell erstellt wurde, müssen Sie warten, bis der Schulungslauf abgeschlossen ist. Nach Abschluss eines erfolgreichen Schulungslaufs können Sie den Schulungslauf auswählen, um die Details zur Ansicht anzuzeigen. Wählen Sie einen Schulungslauf aus. Wenn Sie ein Eigenschaftendialogfeld ausgewählt haben, wählen Sie rechts die Option **[!UICONTROL Ansicht Aktivität Logs]**.

![Ansichten](../images/rtml/view-training.png)

Das Popup-Fenster &quot;Protokolle zur Aktivität der *Ansicht* &quot;wird angezeigt. Wählen Sie die URL für die *Stderprotokolle* aus, um die Protokolle herunterzuladen und die Details der Ausführung anzuzeigen.

![Ansichten](../images/rtml/view-logs.png)

Protokolle sind besonders nützlich für fehlgeschlagene Ausführung, um zu sehen, was schiefgelaufen ist. Aber in diesem Fall suchen Sie nach dem `model-id` passenden ONNX-Modell. Kopieren Sie die Modell-ID.

![Modell-ID suchen](../images/rtml/find-model-id-logs.png)

Sie müssen keinen Bewertungsauftrag im Rezept ausführen. Im [nächsten Lernprogramm](#next-steps)wird die Edge-Bewertung für maschinelles Lernen in Echtzeit behandelt.

## Nächste Schritte {#next-steps}

Indem Sie einem der oben genannten Lernprogramme folgen, haben Sie erfolgreich ein ONNX-Modell trainiert und in den Store für Echtzeit-maschinelles Lernen hochgeladen und haben eine `model_id` zur Identifizierung Ihres Modells. Fahren Sie mit dem nächsten Lernprogramm fort, um zu erfahren, wie Sie Ihr Echtzeit-Modell für maschinelles Lernen [bewerten können](./scoring-ml-model.md).