---
keywords: Experience Platform;Entwicklerhandbuch;Data Science Workspace;beliebte Themen;Echtzeit-maschinelles Lernen;Node-Referenz;
solution: Experience Platform
title: Verwalten von Notebook-Computern mit maschinellem Lernen in Echtzeit
topic: Training and scoring a ML model
description: In der folgenden Anleitung werden die Schritte erläutert, die zum Erstellen einer Echtzeitanwendung für maschinelles Lernen in Adobe Experience Platform JupyterLab erforderlich sind.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '1669'
ht-degree: 0%

---


# Verwalten von Notebook-PCs für maschinelles Lernen in Echtzeit (Alpha)

>[!IMPORTANT]
>
>Das maschinelle Lernen in Echtzeit steht noch nicht allen Benutzern zur Verfügung. Diese Funktion ist alphanumerisch und wird noch getestet. Dieses Dokument kann sich ändern.

In der folgenden Anleitung werden die Schritte beschrieben, die zum Erstellen einer Echtzeit-Anwendung für maschinelles Lernen erforderlich sind. Anhand der bereitgestellten Adobe **[!UICONTROL Echtzeit-ML]**-Python-Notebook-Vorlage wird beschrieben, wie Sie ein Modell trainieren, eine DSL erstellen, DSL an Edge veröffentlichen und die Anforderung bewerten. Wenn Sie mit der Implementierung Ihres Echtzeit-Modell für maschinelles Lernen fortfahren, müssen Sie die Vorlage entsprechend den Anforderungen Ihres Datensatzes ändern.

## Erstellen eines Notebook-PCs für maschinelles Lernen in Echtzeit

Wählen Sie in der Adobe Experience Platform-Benutzeroberfläche unter **Datenwissenschaft** die Option **[!UICONTROL Notebooks]**. Wählen Sie dann **[!UICONTROL JupyterLab]** und lassen Sie die Umgebung etwas zu laden.

![open JupyterLab](../images/rtml/open-jupyterlab.png)

Der Starter [!DNL JupyterLab] wird angezeigt. Blättern Sie nach unten zu *Echtzeit-maschinelles Lernen* und wählen Sie das Notebook **[!UICONTROL Echtzeit-ML]**. Es wird eine Vorlage mit Beispieldatasets für Notebooks mit Beispieldataset geöffnet.

![leere Python](../images/rtml/authoring-notebook.png)

## Importieren und Auffinden von Knoten

Beginn durch Importieren aller erforderlichen Pakete für Ihr Modell. Stellen Sie sicher, dass alle Pakete, die Sie für das Node Authoring verwenden möchten, importiert werden.

>[!NOTE]
>
>Die Liste der Importe kann je nach dem gewünschten Modell unterschiedlich sein. Diese Liste wird sich ändern, wenn im Laufe der Zeit neue Knoten hinzugefügt werden. Eine vollständige Liste der verfügbaren Knoten finden Sie im Handbuch [Node Reference Guide](./node-reference.md).

```python
from pprint import pprint
import pandas as pd
import numpy as np
import json
import uuid
from shutil import copyfile
from pathlib import Path
from datetime import date, datetime, timedelta
from platform_sdk.dataset_reader import DatasetReader

from rtml_nodelibs.nodes.standard.preprocessing.json_to_df import JsonToDataframe
from rtml_sdk.edge.utils import EdgeUtils
from rtml_sdk.graph.utils import GraphBuilder
from rtml_nodelibs.nodes.standard.ml.onnx import ONNXNode
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
from rtml_nodelibs.nodes.standard.preprocessing.pandasnode import Pandas
from rtml_nodelibs.nodes.standard.preprocessing.one_hot_encoder import OneHotEncoder
from rtml_nodelibs.nodes.standard.ml.artifact_utils import ModelUpload
from rtml_nodelibs.core.nodefactory import NodeFactory as nf
from rtml_nodelibs.core.datamsg import DataMsg
```

Die folgende Codezelle druckt eine Liste der verfügbaren Knoten.

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

![Liste der Notizen](../images/rtml/node-list.png)

## Ausbildung eines Echtzeit-maschinellen Lernmodells

Mithilfe einer der folgenden Optionen schreiben Sie [!DNL Python]-Code, um Daten zu lesen, vorbereiten und zu analysieren. Als Nächstes müssen Sie Ihr eigenes ML-Modell trainieren, es in das ONNX-Format serialisieren und es dann in den Echtzeit-Shop des Machine Learning-Modells hochladen.

- [Training Ihres eigenen Modells in JupyterLab-Notebooks](#training-your-own-model)
- [Hochladen Ihres eigenen vorab geschulten ONNX-Modells auf JupyterLab-Notebooks](#pre-trained-model-upload)

### Schulung Ihres eigenen Modells {#training-your-own-model}

Beginn durch Laden der Schulungsdaten.

>[!NOTE]
>
>In der Vorlage **Echtzeit-ML** wird der [CSV-Datensatz für Kfz-Versicherungen](https://github.com/adobe/experience-platform-dsw-reference/tree/master/datasets/insurance) von [!DNL Github] abgerufen.

![Schulungsdaten laden](../images/rtml/load_training.png)

Wenn Sie einen Datensatz aus Adobe Experience Platform verwenden möchten, heben Sie die Auskommentierung der Zelle unten auf. Als Nächstes müssen Sie `DATASET_ID` durch den entsprechenden Wert ersetzen.

![rtml-Datensatz](../images/rtml/rtml-dataset.png)

Um auf ein Dataset in Ihrem [!DNL JupyterLab] Notebook zuzugreifen, wählen Sie die Registerkarte **Daten** in der linken Navigation von [!DNL JupyterLab]. Die Ordner **[!UICONTROL Datensätze]** und **[!UICONTROL Schema]** werden angezeigt. Wählen Sie **[!UICONTROL Datensätze]** und klicken Sie mit der rechten Maustaste und wählen Sie dann die Option **[!UICONTROL Daten im Notebook untersuchen]** aus dem Dropdown-Menü des zu verwendenden Datensatzes. Am unteren Rand des Notebooks wird ein ausführbarer Code-Eintrag angezeigt. Diese Zelle hat Ihr `dataset_id`.

![Datenzugriff](../images/rtml/access-dataset.png)

Klicken Sie nach Abschluss des Vorgangs mit der rechten Maustaste auf die Zelle, die Sie am unteren Rand des Notebooks generiert haben, und löschen Sie sie.

### Schulungseigenschaften

Ändern Sie mithilfe der bereitgestellten Vorlage die Schulungseigenschaften in `config_properties`.

```python
config_properties = {
    "train_records_limit":1000000,
    "n_estimators": "80",
    "max_depth": "5",
    "ten_id": "_experienceplatform"  
}
```

### Vorbereiten des Modells

Mit der Vorlage **[!UICONTROL Echtzeit-ML]** müssen Sie Ihr ML-Modell analysieren, vorbereiten, trainieren und auswerten. Dies geschieht durch die Anwendung von Datentransformationen und den Aufbau einer Schulungspipeline.

**Datentransformationen**

Die Zelle **[!UICONTROL Echtzeit-ML]** **Datenkonvertierungen** muss geändert werden, um mit Ihrem eigenen Datensatz zu funktionieren. Dies umfasst in der Regel das Umbenennen von Spalten, die Datenaggregation und die Datenvorbereitung/Funktionstechnik.

>[!NOTE]
>
>Das folgende Beispiel wurde zur Lesbarkeit mit `[ ... ]` komprimiert. Bitte Ansicht und Erweitern Sie den Abschnitt *Echtzeit-ML* Vorlagendaten-Transformationen für die gesamte Codezelle.

```python
df1.rename(columns = {config_properties['ten_id']+'.identification.ecid' : 'ecid',
                     [ ... ]}, inplace=True)
df1 = df1[['ecid', 'km', 'cartype', 'age', 'gender', 'carbrand', 'leasing', 'city', 
       'country', 'nationality', 'primaryuser', 'purchase', 'pricequote', 'timestamp']]
print("df1 shape 1", df1.shape)
#########################################
# Data Rollup
######################################### 
df1['timestamp'] = pd.to_datetime(df1.timestamp)
df1['hour'] = df1['timestamp'].dt.hour.astype(int)
df1['dayofweek'] = df1['timestamp'].dt.dayofweek

df1.loc[(df1['purchase'] == 'yes'), 'purchase'] = 1
df1.purchase.fillna(0, inplace=True)
df1['purchase'] = df1['purchase'].astype(int)

[ ... ]

print("df1 shape 2", df1.shape)

#########################################
# Data Preparation/Feature Engineering
#########################################      

df1['carbrand'] = df1['carbrand'].str.lower()
df1['country'] = df1['country'].str.lower()
df1.loc[(df1['carbrand'] == 'vw'), 'carbrand'] = 'volkswagen'

[ ... ]

df1['age'].fillna(df1['age'].median(), inplace=True)
df1['gender'].fillna('notgiven', inplace=True)

[ ... ]

df1['city'] = df1.groupby('country')['city'].transform(lambda x : x.fillna(x.mode()))
df1.dropna(subset = ['pricequote'], inplace=True)
print("df1 shape 3", df1.shape)
print(df1)

#grouping
grouping_cols = ['carbrand', 'cartype', 'city', 'country']

for col in grouping_cols:
    df_idx = pd.DataFrame(df1[col].value_counts().head(6))

    def grouping(x):
        if x in df_idx.index:
            return x
        else:
            return "Others"
    df1[col] = df1[col].apply(lambda x: grouping(x))

def age(x):
    if x < 20:
        return "u20"
    elif x > 19 and x < 29:
    [ ... ]
    else: 
        return "Others"

df1['age'] = df1['age'].astype(int)
df1['age_bucket'] = df1['age'].apply(lambda x: age(x))

df_final = df1[['hour', 'dayofweek','age_bucket', 'gender', 'city',  
   'country', 'carbrand', 'cartype', 'leasing', 'pricequote', 'purchase']]
print("df final", df_final.shape)

cat_cols = ['age_bucket', 'gender', 'city', 'dayofweek', 'country', 'carbrand', 'cartype', 'leasing']
df_final = pd.get_dummies(df_final, columns = cat_cols)
```

Führen Sie die angegebene Zelle aus, um ein Beispielergebnis anzuzeigen. Die vom Dataset `carinsurancedataset.csv` zurückgegebene Ausgabentabelle gibt die von Ihnen definierten Änderungen zurück.

![Beispiel für Datentransformationen](../images/rtml/table-return.png)

**Schulungspipeline**

Als Nächstes müssen Sie die Schulungspipeline erstellen. Dies wird ähnlich wie jede andere Schulungspipeline-Datei aussehen, außer Sie müssen eine ONNX-Datei konvertieren und generieren.

Ändern Sie die Vorlage mithilfe der in der vorherigen Zelle definierten Datentransformationen. Der folgende Code, der unten hervorgehoben ist, wird zum Generieren einer ONNX-Datei in Ihrer Feature Pipeline verwendet. Bitte Ansicht der *Echtzeit-ML*-Vorlage für die gesamte Pipelinecodezelle.

```python
#for generating onnx
def generate_onnx_resources(self):        
    install_dir = os.path.expanduser('~/my-workspace')
    print("Generating Onnx")
        
    from skl2onnx import convert_sklearn
    from skl2onnx.common.data_types import FloatTensorType
        
    # ONNX-ification
    initial_type = [('float_input', FloatTensorType([None, self.feature_len]))]

    print("Converting Model to Onnx")
    onx = convert_sklearn(self.model, initial_types=initial_type)
             
    with open("model.onnx", "wb") as f:
        f.write(onx.SerializeToString())
            
    print("Model onnx created")
```

Nachdem Sie die Schulungspipeline abgeschlossen und Ihre Daten durch Datentransformationen geändert haben, führen Sie die Schulung in der folgenden Zelle aus.

```python
model = train(config_properties, df_final)
```

### Erstellen und Hochladen eines ONNX-Modells

Nachdem Sie eine erfolgreiche Schulung abgeschlossen haben, müssen Sie ein ONNX-Modell erstellen und das geschulte Modell in den Store für maschinelles Lernen in Echtzeit hochladen. Nachdem Sie die folgenden Zellen ausgeführt haben, erscheint Ihr ONNX-Modell in der linken Leiste neben allen anderen Notebooks.

```python
import os
import skl2onnx, subprocess

model.generate_onnx_resources()
```

>[!NOTE]
>
>Ändern Sie den Zeichenfolgenwert `model_path` (`model.onnx`), um den Namen Ihres Modells zu ändern.

```python
model_path = "model.onnx"
```

>[!NOTE]
>
>Die folgende Zelle ist weder bearbeitbar noch lesbar und wird benötigt, damit Ihre Echtzeitanwendung für maschinelles Lernen funktioniert.

```python
model = ModelUpload(params={'model_path': model_path})
msg_model = model.process(None, 1)
model_id = msg_model.model['model_id']
 
print("Model ID : ", model_id)
```

![ONNX-Modell](../images/rtml/onnx-model-rail.png)

### Hochladen Ihres eigenen vorab geschulten ONNX-Modells {#pre-trained-model-upload}

Laden Sie mit der Upload-Schaltfläche unter [!DNL JupyterLab] Notebooks Ihr vorab ausgebildetes ONNX-Modell in die [!DNL Data Science Workspace]-Notebook-Umgebung hoch.

![Upload-Symbol](../images/rtml/upload.png)

Ändern Sie anschließend den Zeichenfolgenwert `model_path` im Notebook *Echtzeit-ML* entsprechend Ihrem ONNX-Modellnamen. Führen Sie nach Abschluss des Vorgangs die Zelle *Modellpfad festlegen* aus und führen Sie dann die Zelle *Modell in den RTML-Modellspeicher hochladen* aus. Ihr Modellort und Ihre Modell-ID werden beide bei erfolgreicher Ausführung in der Antwort zurückgegeben.

![Hochladen eines eigenen Modells](../images/rtml/upload-own-model.png)

## DSL-Erstellung (Domänenspezifische Sprache)

In diesem Abschnitt wird die Erstellung einer DSL beschrieben. Sie werden die Knoten erstellen, die jede Vorverarbeitung von Daten zusammen mit dem ONNX-Knoten enthalten. Als Nächstes wird ein DSL-Diagramm mit Knoten und Kanten erstellt. Edges connect nodes using tuple based format (node_1, node_2). Das Diagramm sollte keine Zyklen aufweisen.

>[!IMPORTANT]
>
>Die Verwendung des ONNX-Knotens ist obligatorisch. Ohne den ONNX-Knoten ist die Anwendung nicht erfolgreich.

### Node Authoring

>[!NOTE]
>
> Je nach verwendetem Datentyp verfügen Sie wahrscheinlich über mehrere Knoten. Im folgenden Beispiel wird nur ein einzelner Knoten in der Vorlage *Echtzeit-ML* umrissen. Bitte Ansicht der *Echtzeit-ML*-Vorlagen *Node Authoring* für die gesamte Codemelle.

Der Knoten Pandas unten verwendet `"import": "map"`, um den Methodennamen als Zeichenfolge in die Parameter zu importieren, gefolgt von der Eingabe der Parameter als Zuordnungsfunktion. Im folgenden Beispiel wird dies mit `{'arg': {'dataLayerNull': 'notgiven', 'no': 'no', 'yes': 'yes', 'notgiven': 'notgiven'}}` durchgeführt. Nachdem Sie die Map platziert haben, haben Sie die Möglichkeit, `inplace` auf `True` oder `False` einzustellen. Stellen Sie `inplace` auf `True` oder `False` ein, je nachdem, ob Sie die Transformation anstelle der Transformation anwenden möchten oder nicht. Standardmäßig erstellt `"inplace": False` eine neue Spalte. Die Unterstützung für die Bereitstellung eines neuen Spaltennamens ist so eingestellt, dass er in einer späteren Version hinzugefügt wird. Die letzte Zeile `cols` kann ein einzelner Spaltenname oder eine Liste von Spalten sein. Geben Sie die Spalten an, auf die die Transformation angewendet werden soll. In diesem Beispiel wird `leasing` angegeben. Weitere Informationen zu den verfügbaren Knoten und deren Verwendung finden Sie im Node Reference Guide](./node-reference.md).[

```python
# Renaming leasing column using Pandas Node
leasing_mapper_node = Pandas(params={'import': 'map',
                                'kwargs': {'arg': {
                                    'dataLayerNull': 'notgiven', 
                                    'no': 'no', 
                                    'yes': 'yes', 
                                    'notgiven': 'notgiven'}},
                                'inplace': True,
                                'cols': 'leasing'})
```

### DSL-Diagramm erstellen

Bei der Erstellung Ihrer Knoten besteht der nächste Schritt darin, die Knoten zu verketten, um ein Diagramm zu erstellen.

Beginn durch Auflisten aller Knoten, die Teil des Diagramms sind, durch Erstellen eines Arrays.

```python
nodes = [json_df_node, 
        to_datetime_node,
        hour_node,
        dayofweek_node,
        age_fillna_node,
        carbrand_fillna_node,
        country_fillna_node,
        cartype_primary_nationality_km_fillna_node,
        carbrand_mapper_node,
        cartype_mapper_node,
        country_mapper_node,
        gender_mapper_node,
        leasing_mapper_node,
        age_to_int_node,
        age_bins_node,
        dummies_node, 
        onnx_node]
```

Verbinden Sie dann die Knoten mit Kanten. Jeder Tupel ist eine [!DNL Edge]-Verbindung.

>[!TIP]
>
> Da die Knoten linear voneinander abhängig sind (jeder Knoten hängt von der Ausgabe des vorherigen Knotens ab), können Sie Links mit einem einfachen Python-Liste-Verständnis erstellen. Bitte fügen Sie Ihre eigenen Verbindungen hinzu, wenn ein Knoten von mehreren Eingaben abhängt.

```python
edges = [(nodes[i], nodes[i+1]) for i in range(len(nodes)-1)]
```

Sobald Ihre Knoten verbunden sind, erstellen Sie das Diagramm. Die nachstehende Zelle ist obligatorisch und kann nicht bearbeitet oder gelöscht werden.

```python
dsl = GraphBuilder.generate_dsl(nodes=nodes, edges=edges)
pprint(json.loads(dsl))
```

Nach Abschluss des Vorgangs wird ein `edge`-Objekt zurückgegeben, das alle Knoten und die ihnen zugeordneten Parameter enthält.

![edge return](../images/rtml/edge-return.png)

## Auf Edge veröffentlichen (Hub)

>[!NOTE]
>
>Das maschinelle Lernen in Echtzeit wird vorübergehend am Adobe Experience Platform Hub bereitgestellt und von ihm verwaltet. Weitere Informationen finden Sie im Überblicksabschnitt unter [Architektur für maschinelles Lernen in Echtzeit](./home.md#architecture).

Nachdem Sie ein DSL-Diagramm erstellt haben, können Sie Ihr Diagramm auf dem [!DNL Edge] bereitstellen.

>[!IMPORTANT]
>
>Veröffentlichen Sie nicht häufig auf [!DNL Edge], dies kann die [!DNL Edge]-Knoten überladen. Es wird nicht empfohlen, dasselbe Modell mehrmals zu veröffentlichen.

```python
edge_utils = EdgeUtils()
(edge_location, service_id) = edge_utils.publish_to_edge(dsl=dsl)
print(f'Edge Location: {edge_location}')
print(f'Service ID: {service_id}')
```

### DSL aktualisieren und auf Edge veröffentlichen (optional)

Wenn Sie Ihre DSL nicht aktualisieren müssen, können Sie zu [scoring](#scoring) überspringen.

>[!NOTE]
>
>Die folgenden Zellen sind nur erforderlich, wenn Sie eine vorhandene DSL aktualisieren möchten, die in Edge veröffentlicht wurde.

Ihre Modelle werden sich wahrscheinlich weiter entwickeln. Anstatt einen neuen Dienst zu erstellen, ist es möglich, einen vorhandenen Dienst mit Ihrem neuen Modell zu aktualisieren. Sie können einen Knoten definieren, den Sie aktualisieren möchten, ihm eine neue ID zuweisen und dann den neuen DSL erneut auf das [!DNL Edge] hochladen.

Im Beispiel unten wird Node 0 mit einer neuen ID aktualisiert.

```python
# Update the id of Node 0 with a random uuid.

dsl_dict = json.loads(dsl)
print(f"ID of Node 0 in current DSL: {dsl_dict['edge']['applicationDsl']['nodes'][0]['id']}")

new_node_id = str(uuid.uuid4())
print(f'Updated Node ID: {new_node_id}')

dsl_dict['edge']['applicationDsl']['nodes'][0]['id'] = new_node_id
```

![Aktualisierter Knoten](../images/rtml/updated-node.png)

Nach dem Aktualisieren der Knoten-ID können Sie eine aktualisierte DSL auf der Edge-Seite erneut veröffentlichen.

```python
# Republish the updated DSL to Edge
(edge_location_ret, service_id, updated_dsl) = edge_utils.update_deployment(dsl=json.dumps(dsl_dict), service_id=service_id)
print(f'Updated dsl: {updated_dsl}')
```

Sie erhalten die aktualisierte DSL zurückgegeben.

![Aktualisierte DSL](../images/rtml/updated-dsl.png)

## Scoring {#scoring}

Nach dem Veröffentlichen auf [!DNL Edge] erfolgt die Bewertung durch eine Client-Anfrage zur POST. Normalerweise kann dies über eine Client-Anwendung erfolgen, die ML-Ergebnisse benötigt. Sie können es auch von Postman aus tun. Die Vorlage **[!UICONTROL Echtzeit-ML]** verwendet EdgeUtils, um diesen Vorgang zu demonstrieren.

>[!NOTE]
>
>Vor dem Scoring von Beginn ist eine geringe Verarbeitungszeit erforderlich.

```python
# Wait for the app to come up
import time
time.sleep(20)
```

Anhand desselben Schemas, das bei der Schulung verwendet wurde, werden Scoring-Beispieldaten generiert. Diese Daten werden zum Erstellen eines Datenbilds verwendet, das dann in ein Bewertungswörterbuch konvertiert wird. Bitte Ansicht der *Echtzeit-ML*-Vorlage für die gesamte Codemelle.

![Bewertungsdaten](../images/rtml/generate-score-data.png)

### Ergebnis gegen den Edge-Endpunkt

Verwenden Sie die folgende Zelle in der Vorlage *Echtzeit-ML*, um das Ergebnis mit Ihrem [!DNL Edge]-Dienst zu erzielen.

![Ergebnis gegen Kante](../images/rtml/scoring-edge.png)

Nach Abschluss der Bewertung werden die URL, die Nutzlast und die Ergebnisausgabe von [!DNL Edge] zurückgegeben.[!DNL Edge]

## Liste der bereitgestellten Apps über das [!DNL Edge]

Um eine Liste der derzeit bereitgestellten Apps auf dem [!DNL Edge] zu generieren, führen Sie die folgende Codezelle aus. Diese Zelle kann nicht bearbeitet oder gelöscht werden.

```python
services = edge_utils.list_deployed_services()
print(services)
```

Die zurückgegebene Antwort ist ein Array Ihrer bereitgestellten Dienste.

```json
[
    {
        "created": "2020-05-25T19:18:52.731Z",
        "deprecated": false,
        "id": "40eq76c0-1c6f-427a-8f8f-54y9cdf041b7",
        "type": "edge",
        "updated": "2020-05-25T19:18:52.731Z"
    }
]
```

## Eine bereitgestellte App oder Dienst-ID aus dem [!DNL Edge] löschen (optional)

>[!CAUTION]
>
>Diese Zelle wird zum Löschen der bereitgestellten Edge-Anwendung verwendet. Verwenden Sie die folgende Zelle nur, wenn Sie eine bereitgestellte [!DNL Edge]-Anwendung löschen müssen.

```python
if edge_utils.delete_from_edge(service_id=service_id):
    print(f"Deleted service id {service_id} successfully")
else:
    print(f"Failed to delete service id {service_id}")
```

## Nächste Schritte

Mit dem oben stehenden Tutorial haben Sie erfolgreich ein ONNX-Modell trainiert und in den Real-time Machine Learning Model Store hochgeladen. Zusätzlich haben Sie Ihr Echtzeit-Modell für maschinelles Lernen bewertet und bereitgestellt. Wenn Sie mehr über die Knoten erfahren möchten, die für die Modellerstellung verfügbar sind, besuchen Sie das [Node Reference Guide](./node-reference.md).