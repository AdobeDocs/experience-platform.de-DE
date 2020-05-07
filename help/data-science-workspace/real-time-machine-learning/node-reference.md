---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real-time Machine Learning;node reference;
solution: Experience Platform
title: Referenzhandbuch zu Nodes für maschinelles Lernen in Echtzeit
topic: Nodes reference
translation-type: tm+mt
source-git-commit: a37a3dd0c8f784d69da25ac503ad388b57b05ed9
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 1%

---


# Referenzhandbuch zu Nodes für maschinelles Lernen in Echtzeit

>[!IMPORTANT]
>Das maschinelle Lernen in Echtzeit steht noch nicht allen Benutzern zur Verfügung. Diese Funktion ist alphanumerisch und wird noch getestet. Dieses Dokument kann sich ändern.

In der folgenden Anleitung werden die unterstützten Node-Bibliotheken für maschinelles Lernen in Echtzeit beschrieben.

## Entdecken von Nodes zur Verwendung in Ihrer ML-Pipeline

Kopieren Sie den folgenden Code in ein Python-Notebook, um alle verfügbaren Knoten Ansicht.

```python
from pprint import pprint
 
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
```

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

**Beispielantwort**

```python
{'FieldOps': 'rtml_nodelibs.nodes.standard.preprocessing.fieldops.FieldOps',
 'FieldTrans': 'rtml_nodelibs.nodes.standard.preprocessing.fieldtrans.FieldTrans',
 'ModelUpload': 'rtml_nodelibs.nodes.standard.ml.artifact_utils.ModelUpload',
 'ONNXNode': 'rtml_nodelibs.nodes.standard.ml.onnx.ONNXNode',
 'Pandas': 'rtml_nodelibs.nodes.standard.preprocessing.pandasnode.Pandas',
 'Processor': 'rtml_nodelibs.nodes.standard.preprocessing.processor.Processor',
 'Receiver': 'rtml_nodelibs.nodes.standard.preprocessing.receiver.Receiver',
 'ScikitLearn': 'rtml_nodelibs.nodes.standard.ml.scikitlearn.ScikitLearn',
 'Simulator': 'rtml_nodelibs.nodes.standard.preprocessing.simulator.Simulator',
 'Split': 'rtml_nodelibs.nodes.standard.preprocessing.splitter.Split'}
```

## Standardknoten

Standardknoten bauen auf Open-Source-Datenwissenschaftsbibliotheken wie Pandas und ScikitLearn auf.

### ModelUpload

Der ModelUpload-Knoten ist ein interner Adobe-Knoten, der einen model_path akzeptiert und das Modell vom lokalen Modellpfad in den Real-time Machine Learning Blob Store hochlädt.

```python
model = ModelUpload(params={'model_path': model_path})
  
msg_model = model.process(None, 1)
  
model_id = msg_model.model['model_id']
```

### ONNXNode

ONNXNode ist ein interner Adobe-Knoten, der eine Modell-ID benötigt, um das vorab geschulte ONNX-Modell abzurufen, und es verwendet, um bei eingehenden Daten zu bewerten.

>[!TIP]
>Geben Sie die Spalten in derselben Reihenfolge an, in der die Daten an das ONNX-Modell gesendet werden sollen.

```python
node_model_score = ONNXNode(params={"features": ['browser', 'device', 'login_page', 'product_page', 'search_page'], "model_id": model_id})
```

### Pandas {#pandas}

Mit dem folgenden Pandas-Knoten können Sie eine beliebige `pd.DataFrame` Methode oder eine allgemeine Pandas-Funktion auf oberster Ebene importieren. Weitere Informationen zu Pandas-Methoden finden Sie in der Dokumentation zu den [Pandas-Methoden](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html). Weitere Informationen zu Funktionen auf oberster Ebene finden Sie im [Pandas API-Referenzhandbuch für allgemeine Funktionen](https://pandas.pydata.org/pandas-docs/stable/reference/general_functions.html).

Der unten stehende Knoten verwendet `"import": "map"` zum Importieren des Methodennamens als Zeichenfolge in die Parameter, gefolgt von der Eingabe der Parameter als Zuordnungsfunktion. Im folgenden Beispiel wird dies mithilfe von `{"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0}`. Nachdem Sie die Map eingerichtet haben, haben Sie die Möglichkeit, `inplace` als &quot;true&quot;oder &quot;false&quot;festzulegen. Legen Sie `inplace` als `True` oder `False` basierend darauf fest, ob die Transformation angewendet werden soll oder nicht. Standardmäßig `"inplace": False` wird eine neue Spalte erstellt. Die Unterstützung für die Bereitstellung eines neuen Spaltennamens ist so eingestellt, dass er in einer späteren Version hinzugefügt wird. Die letzte Zeile `cols` kann ein einzelner Spaltenname oder eine Liste von Spalten sein. Geben Sie die Spalten an, auf die die Transformation angewendet werden soll. In diesem Beispiel `device` wird angegeben.

```python
#  df["device"] = df["device"].map({"Desktop":1, "Mobile":0}, na_action=0)
 
node_device_apply = Pandas(params={"import": "map",
    "kwargs": {"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0},
    "inplace": True,
    "cols": "device"})
 
 
# df["browser"] = df["browser"].map({"chrome": 1, "firefox": 0}, "na_action": 0})
 
node_browser_apply = Pandas(params={"import": "map",
    "kwargs": {"arg": {"chrome": 1, "firefox": 0}, "na_action": 0},
    "inplace": True,
    "cols": "browser"})
```

### ScikitLearn

Mit dem Knoten ScikitLearn können Sie beliebige ScikitLearn ML-Modelle oder -Skalierer importieren. Verwenden Sie die unten stehende Tabelle, um weitere Informationen zu einem der im Beispiel verwendeten Werte zu erhalten:

```python
model_train = ScikitLearn(params={
    "features":['browser', 'device', 'login_page', 'product_page', 'search_page'],
    "label": "payment_confirm",
    "mode": "train",
    "model_path": "resources/model.onnx",
    "params": {
        "model": "sklearn.linear_model.LogisticRegression",
        "model_params": {"solver" : 'lbfgs'}
    }})
msg6 = model_train.process(msg5)
```

| Wert | Beschreibung |
| --- | --- |
| Funktionen | Eingabefunktionen für das Modell (Liste von Zeichenfolgen). <br> Beispiel: &quot;browser&quot;, &quot;device&quot;, &quot;login_page&quot;, &quot;product_page&quot;, &quot;search_page&quot; |
| label | Spaltenname der Zielgruppe (Zeichenfolge). |
| mode | Zug/Test (Zeichenfolge). |
| model_path | Pfad zum gespeicherten Modell lokal im Format &quot;onnx&quot;. |
| params.model | Absoluter Importpfad zum Modell (Zeichenfolge), z. B.: &quot;sklearn.linear_model.LogisticRegression&quot;. |
| params.model_params | Modell-Hyperparameter finden Sie in der Dokumentation zur [Sklearn-API (map/dict)](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html) . |
| node_instance.process(data_message_from_previous_node) | Die Methode `process()` nimmt DataMsg von der vorherigen Node und wendet eine Transformation an. Dies hängt von der aktuell verwendeten Node ab. |

### Aufspaltung

Verwenden Sie den folgenden Knoten, um Ihren Dataframe in Zug zu teilen und zu testen, indem Sie ihn bestehen `train_size` oder `test_size`. Dadurch wird ein Dataframe mit einem Multi-Index zurückgegeben. Sie können mithilfe des folgenden Beispiels auf Zug- und Testdataframes zugreifen `msg5.data.xs(“train”)`.

```python
splitter = Split(params={"train_size": 0.7})
msg5 = splitter.process(msg4)
```

## Nächste Schritte

Der nächste Schritt besteht darin, einen Knoten zu erstellen, der zur Bewertung eines Echtzeit-maschinellen Lernmodells verwendet werden kann. Weitere Informationen finden Sie im Tutorial [zur Bewertung eines Echtzeit-maschinellen Lernmodells](./node-reference.md) .
