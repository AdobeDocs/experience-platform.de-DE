---
keywords: Experience Platform;Entwicklerhandbuch;Datenwissenschafts-Arbeitsbereich;beliebte Themen;maschinelles Lernen in Echtzeit;Knotenreferenz;
solution: Experience Platform
title: Knotenreferennz für maschinelles Lernen in Echtzeit
description: Ein Knoten ist die grundlegende Einheit, aus der Diagramme gebildet werden. Jeder Knoten führt eine bestimmte Aufgabe aus und kann mithilfe von Verknüpfungen mit anderen Knoten verkettet werden, um ein Diagramm zu bilden, das für eine ML-Pipeline steht. Die von einem Knoten ausgeführte Aufgabe stellt einen Vorgang an Eingabedaten dar, beispielsweise eine Umwandlung von Daten oder Schemata oder eine Schlussfolgerung durch maschinelles Lernen. Der Knoten gibt den transformierten oder abgeleiteten Wert an den oder die nächsten Knoten aus.
exl-id: 67fe26b5-ce03-4a9a-ad45-783b2acf8d92
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: ht
source-wordcount: '678'
ht-degree: 100%

---

# Knotenreferenz für maschinelles Lernen in Echtzeit (Alpha)

>[!IMPORTANT]
>
>Das maschinelle Lernen in Echtzeit steht noch nicht allen Benutzenden zur Verfügung. Diese Funktion befindet sich in der Alpha-Phase und wird noch getestet. Dieses Dokument kann sich ändern.

Ein Knoten ist die grundlegende Einheit, aus der Diagramme gebildet werden. Jeder Knoten führt eine bestimmte Aufgabe aus und kann mithilfe von Verknüpfungen mit anderen Knoten verkettet werden, um ein Diagramm zu bilden, das für eine ML-Pipeline steht. Die von einem Knoten ausgeführte Aufgabe stellt einen Vorgang an Eingabedaten dar, beispielsweise eine Umwandlung von Daten oder Schemata oder eine Schlussfolgerung durch maschinelles Lernen. Der Knoten gibt den transformierten oder abgeleiteten Wert an den oder die nächsten Knoten aus.

Im folgenden Handbuch werden die unterstützten Knotenbibliotheken für maschinelles Lernen in Echtzeit beschrieben.

## Erkennen von Knoten zur Verwendung in Ihrer ML-Pipeline

Kopieren Sie den folgenden Code in ein [!DNL Python]-Notebook, um alle Knoten anzuzeigen, die zur Verwendung verfügbar sind.

```python
from pprint import pprint
 
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
```

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

**Beispielantwort**

```json
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

Standardknoten basieren auf Open-Source-Datenwissenschaftsbibliotheken wie Pandas und ScikitLearn.

### ModelUpload

Der Knoten „ModelUpload“ ist ein interner Adobe-Knoten, der über einen model_path das Modell aus dem lokalen Modellpfad in den Blob-Speicher für maschinelles Lernen in Echtzeit hochlädt.

```python
model = ModelUpload(params={'model_path': model_path})
  
msg_model = model.process(None, 1)
  
model_id = msg_model.model['model_id']
```

### ONNXNode

ONNXNode ist ein interner Adobe-Knoten, der mithilfe einer Modell-ID das vortrainierte ONNX-Modell abruft und es verwendet, um eingehende Daten zu bewerten.

>[!TIP]
>
>Geben Sie die Spalten in derselben Reihenfolge an, in der die Daten an das ONNX-Modell zur Bewertung gesendet werden sollen.

```python
node_model_score = ONNXNode(params={"features": ['browser', 'device', 'login_page', 'product_page', 'search_page'], "model_id": model_id})
```

### Pandas {#pandas}

Der folgende Pandas-Knoten ermöglicht den Import jeder `pd.DataFrame`-Methode oder einer beliebigen allgemeinen Pandas-Funktion auf oberster Ebene. Weitere Informationen zu Pandas-Methoden finden Sie in der [Dokumentation zu Pandas-Methoden](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html). Weitere Informationen zu Funktionen der obersten Ebene finden Sie im [Pandas-API-Referenzhandbuch für allgemeine Funktionen](https://pandas.pydata.org/pandas-docs/stable/reference/general_functions.html).

Der nachstehende Knoten verwendet `"import": "map"`, um den Methodennamen als Zeichenfolge in die Parameter zu importieren, gefolgt von der Eingabe der Parameter als Zuordnungsfunktion. Im folgenden Beispiel wird dazu `{"arg": {"Desktop": 1, "Mobile": 0}, "na_action": 0}` verwendet. Nachdem Sie die Zuordnung eingerichtet haben, haben Sie die Möglichkeit, `inplace` als `True` oder `False` festzulegen. Legen Sie `inplace` als `True` oder `False` fest, je nachdem, ob Sie die Umwandlung an Ort und Stelle anwenden möchten oder nicht. Standardmäßig erstellt `"inplace": False` eine neue Spalte. Es ist geplant, die Unterstützung für die Bereitstellung eines neuen Spaltennamens in einer nachfolgenden Version hinzuzufügen. Die letzte Zeile `cols` kann ein einzelner Spaltenname oder eine Spaltenliste sein. Geben Sie die Spalten an, auf die Sie die Umwandlung anwenden wollen. In diesem Beispiel ist `device` festgelegt.

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

Mit dem Knoten „ScikitLearn“ können Sie beliebige ScikitLearn-ML-Modelle oder -Scaler importieren. In der folgenden Tabelle finden Sie weitere Informationen zu den im Beispiel verwendeten Werten:

```python
model_train = ScikitLearn(params={
    "features":['browser', 'device', 'login_page', 'product_page', 'search_page'],
    "label": "payment_confirm",
    "mode": "train",
    "model_path": "resources/model.onnx",
    "params": {
        "model": "sklearn.linear_model.LogisticRegression",
        "model_params": {"solver": 'lbfgs'}
    }})
msg6 = model_train.process(msg5)
```

| Wert | Beschreibung |
| --- | --- |
| Funktionen | Eingabefunktionen für das Modell (Liste der Zeichenfolgen). <br> Beispiel: `browser`, `device`, `login_page`, `product_page`, `search_page` |
| label | Name der Zielspalte (Zeichenfolge). |
| mode | Trainieren/Testen (Zeichenfolge). |
| model_path | Pfad zum lokalen Speichermodell im onnx-Format. |
| params.model | Absoluter Importpfad zum Modell (Zeichenfolge), z. B.: `sklearn.linear_model.LogisticRegression`. |
| params.model_params | Modellhyperparameter (weitere Informationen in der [sklearn-API (map/dict)](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html)-Dokumentation). |
| node_instance.process(data_message_from_previous_node) | Die Methode `process()` nimmt DataMsg aus dem vorherigen Knoten und wendet die Umwandlung an. Dies hängt vom aktuellen verwendeten Knoten ab. |

### Aufspalten

Verwenden Sie den folgenden Knoten, um Ihren Datenrahmen in „Trainieren“ und „Testen“ aufzuteilen, indem Sie `train_size` oder `test_size` übergeben. Dadurch wird ein Datenrahmen mit einem Multi-Index zurückgegeben. Sie können mithilfe des folgenden Beispiels auf Datenrahmen zum Trainieren und Testen zugreifen: `msg5.data.xs("train")`.

```python
splitter = Split(params={"train_size": 0.7})
msg5 = splitter.process(msg4)
```

## Nächste Schritte

Der nächste Schritt besteht darin, Knoten zur Verwendung bei der Bewertung eines Modells für maschinelles Lernen in Echtzeit zu erstellen. Weiterführende Informationen finden Sie im [Benutzerhandbuch zum Notebook für maschinelles Lernen in Echtzeit](./rtml-authoring-notebook.md).
