---
keywords: Experience Platform;Entwicklerhandbuch;Datenwissenschafts-Arbeitsbereich; beliebte Themen;maschinelles Lernen in Echtzeit;Knotenreferenz
solution: Experience Platform
title: Verwalten von Notebooks für maschinelles Lernen in Echtzeit
description: Im folgenden Handbuch werden die Schritte beschrieben, die zum Erstellen einer Anwendung für maschinelles Lernen in Echtzeit in Adobe Experience Platform JupyterLab erforderlich sind.
exl-id: 604c4739-5a07-4b5a-b3b4-a46fd69e3aeb
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1669'
ht-degree: 100%

---

# Verwalten von Notebooks für maschinelles Lernen in Echtzeit (Alpha)

>[!IMPORTANT]
>
>Das maschinelle Lernen in Echtzeit steht noch nicht allen Benutzenden zur Verfügung. Diese Funktion befindet sich in der Alpha-Phase und wird noch getestet. Dieses Dokument kann sich ändern.

Im folgenden Handbuch werden die Schritte beschrieben, die zum Erstellen einer Anwendung für maschinelles Lernen in Echtzeit erforderlich sind. Unter Verwendung der von Adobe bereitgestellten **[!UICONTROL Echtzeit-ML]**-Python-Notebook-Vorlage behandelt dieses Handbuch das Trainieren eines Modells, das Erstellen einer DSL, das Veröffentlichen der DSL in Edge und die Bewertung der Anfrage. Wenn Sie Ihr Modell zum maschinellen Lernen in Echtzeit implementieren, wird erwartet, dass Sie die Vorlage entsprechend den Anforderungen Ihres Datensatzes ändern.

## Erstellen eines Notebooks für maschinelles Lernen in Echtzeit

Wählen Sie in der Adobe Experience Platform-Benutzeroberfläche unter **Datenwissenschaften** die Option **[!UICONTROL Notebooks]** aus. Wählen Sie als Nächstes **[!UICONTROL JupyterLab]** aus und lassen Sie dem System etwas Zeit, um die Umgebung zu laden.

![Öffnen von JupyterLab](../images/rtml/open-jupyterlab.png)

Der [!DNL JupyterLab]-Starter wird angezeigt. Scrollen Sie nach unten zu *Maschinelles Lernen in Echtzeit* und wählen Sie das **[!UICONTROL Echtzeit-ML]**-Notebook aus. Eine Vorlage wird geöffnet, die beispielhafte Notebook-Zellen mit einem Beispieldatensatz enthält.

![Leeres Python](../images/rtml/authoring-notebook.png)

## Importieren und Erkennen von Knoten

Importieren Sie zunächst alle erforderlichen Pakete für Ihr Modell. Stellen Sie sicher, dass alle Pakete, die Sie für die Knotenerstellung verwenden möchten, importiert werden.

>[!NOTE]
>
>Die Importliste kann je nach gewünschtem Modell unterschiedlich sein. Diese Liste wird sich ändern, wenn neue Knoten im Laufe der Zeit hinzugefügt werden. Eine vollständige Liste der verfügbaren Knoten finden Sie im [Knotenreferenzhandbuch](./node-reference.md).

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

Mit der folgenden Code-Zelle wird eine Liste der verfügbaren Knoten gedruckt.

```python
# Discover Nodes
pprint(nf.discover_nodes())
```

![Liste der Hinweise](../images/rtml/node-list.png)

## Trainieren eines Modells für maschinelles Lernen in Echtzeit

Mit einer der folgenden Optionen schreiben Sie [!DNL Python]-Code zum Lesen, Vorverarbeiten und Analysieren von Daten. Als Nächstes müssen Sie Ihr eigenes ML-Modell trainieren, es in das ONNX-Format serialisieren und dann in den Modellspeicher für maschinelles Lernen in Echtzeit hochladen.

- [Trainieren Ihres eigenen Modells in JupyterLab-Notebooks](#training-your-own-model)
- [Hochladen Ihres eigenen vortrainierten ONNX-Modells auf JupyterLab-Notebooks](#pre-trained-model-upload)

### Trainieren Ihres eigenen Modells {#training-your-own-model}

Laden Sie zunächst Ihre Schulungsdaten.

>[!NOTE]
>
>In der **Echtzeit-ML**-Vorlage wird der [CSV-Datensatz für Kfz-Versicherungen](https://github.com/adobe/experience-platform-dsw-reference/tree/master/datasets/insurance) aus [!DNL Github] abgerufen.

![Laden von Schulungsdaten](../images/rtml/load_training.png)

Wenn Sie einen Datensatz aus Adobe Experience Platform verwenden möchten, heben Sie die Auskommentierung der Zelle unten auf. Als Nächstes müssen Sie `DATASET_ID` durch den entsprechenden Wert ersetzen.

![rtml-Datensatz](../images/rtml/rtml-dataset.png)

Um auf einen Datensatz in Ihrem [!DNL JupyterLab]-Notebook zuzugreifen, wählen Sie die Registerkarte **Daten** im linken Navigationsbereich von [!DNL JupyterLab] aus. Die Verzeichnisse **[!UICONTROL Datensätze]** und **[!UICONTROL Schemata]** werden angezeigt. Wählen Sie **[!UICONTROL Datensätze]** aus, klicken Sie mit der rechten Maustaste und wählen Sie dann im Dropdown-Menü des Datensatzes, den Sie verwenden möchten, die Option **[!UICONTROL Daten in Notebook erkunden]** aus. Unten im Notebook wird ein ausführbarer Code-Eintrag angezeigt. Diese Zelle enthält Ihre `dataset_id`.

![Datensatzzugriff](../images/rtml/access-dataset.png)

Klicken Sie anschließend mit der rechten Maustaste auf die Zelle, die Sie unten im Notebook generiert haben, und löschen Sie sie.

### Trainings-Eigenschaften

Ändern Sie mithilfe der bereitgestellten Vorlage eine der Trainings-Eigenschaften in `config_properties`.

```python
config_properties = {
    "train_records_limit":1000000,
    "n_estimators": "80",
    "max_depth": "5",
    "ten_id": "_experienceplatform"  
}
```

### Vorbereiten des Modells

Mithilfe der **[!UICONTROL Echtzeit-ML]**-Vorlage müssen Sie Ihr ML-Modell analysieren, vorverarbeiten, trainieren und bewerten. Dies geschieht durch die Anwendung von Datenumwandlungen und den Aufbau einer Schulungs-Pipeline.

**Datenumwandlungen**

3Die Zelle **Datenumwandlungen** der **[!UICONTROL Echtzeit-ML]**-Vorlage muss so geändert werden, dass sie mit Ihrem eigenen Datensatz verwenden werden kann. Normalerweise umfasst dies das Umbenennen von Spalten, die Datenaggregation und die Datenvorbereitung/Funktionsentwicklung.

>[!NOTE]
>
>Das folgende Beispiel wurde aus Gründen der Lesbarkeit mithilfe von `[ ... ]` verkürzt. Sehen Sie sich den Abschnitt *Echtzeit-ML*-Vorlagen-Datenumwandlungen für die vollständige Code-Zelle an und erweitern Sie ihn.

```python
df1.rename(columns = {config_properties['ten_id']+'.identification.ecid': 'ecid',
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

df1['city'] = df1.groupby('country')['city'].transform(lambda x: x.fillna(x.mode()))
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

Führen Sie die bereitgestellte Zelle aus, um ein Beispielergebnis anzuzeigen. Die vom `carinsurancedataset.csv`-Datensatz zurückgegebene Ausgabetabelle gibt die von Ihnen definierten Änderungen aus.

![Beispiel für Datenumwandlungen](../images/rtml/table-return.png)

**Trainings-Pipeline**

Als Nächstes müssen Sie die Trainings-Pipeline erstellen. Dies geschieht ähnlich wie bei jeder anderen Trainings-Pipeline-Datei, mit der Ausnahme, dass Sie eine ONNX-Datei konvertieren und generieren müssen.

Ändern Sie die Vorlage mithilfe der in Ihrer vorherigen Zelle definierten Datenumwandlungen. Der folgende unten hervorgehobene Code wird zum Generieren einer ONNX-Datei in Ihrer Funktions-Pipeline verwendet. Zeigen Sie die *Echtzeit-ML*-Vorlage für die vollständige Pipeline-Code-Zelle an.

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

Sobald Sie Ihre Schulungspipeline abgeschlossen und Ihre Daten durch Datenumwandlungen geändert haben, verwenden Sie die folgende Zelle, um die Schulung auszuführen.

```python
model = train(config_properties, df_final)
```

### Generieren und Hochladen eines ONNX-Modells

Nach einem erfolgreichen Trainings-Durchlauf müssen Sie ein ONNX-Modell generieren und das trainierte Modell in den Modellspeicher für maschinelles Lernen in Echtzeit hochladen. Nachdem Sie die folgenden Zellen ausgeführt haben, wird Ihr ONNX-Modell in der linken Leiste neben allen anderen Notebooks angezeigt.

```python
import os
import skl2onnx, subprocess

model.generate_onnx_resources()
```

>[!NOTE]
>
>Ändern Sie den `model_path`-Zeichenfolgenwert (`model.onnx`), um den Namen Ihres Modells zu ändern.

```python
model_path = "model.onnx"
```

>[!NOTE]
>
>Die folgende Zelle kann nicht bearbeitet oder gelöscht werden und ist erforderlich, damit Ihre Anwendung für maschinelles Lernen in Echtzeit funktioniert.

```python
model = ModelUpload(params={'model_path': model_path})
msg_model = model.process(None, 1)
model_id = msg_model.model['model_id']
 
print("Model ID: ", model_id)
```

![ONNX-Modell](../images/rtml/onnx-model-rail.png)

### Hochladen Ihres eigenen vortrainierten ONNX-Modells {#pre-trained-model-upload}

Laden Sie mithilfe der Upload-Schaltfläche in [!DNL JupyterLab]-Notebooks Ihr vortrainiertes ONNX-Modell in die [!DNL Data Science Workspace]-Notebook-Umgebung hoch.

![Upload-Symbol](../images/rtml/upload.png)

Ändern Sie als Nächstes den `model_path`-Zeichenfolgenwert im *Echtzeit-ML*-Notebook entsprechend Ihrem ONNX-Modellnamen. Führen Sie anschließend die Zelle *Modellpfad festlegen* und dann die Zelle *Modell in den RTML-Modellspeicher hochladen* aus. Ihr Modellort und Ihre Modell-ID werden im Erfolgsfall in der Antwort zurückgegeben.

![Hochladen eines eigenen Modells](../images/rtml/upload-own-model.png)

## Erstellen einer Domain-spezifischen Sprache (DSL)

In diesem Abschnitt wird die Erstellung einer DSL beschrieben. Sie werden die Knoten erstellen, die eine Vorverarbeitung von Daten zusammen mit dem ONNX-Knoten beinhalten. Als Nächstes wird ein DSL-Diagramm mit Knoten und Kanten erstellt. Kanten verbinden Knoten im Tupel-basierten Format (node_1, node_2). Das Diagramm sollte keine Zyklen aufweisen.

>[!IMPORTANT]
>
>Die Verwendung des ONNX-Knotens ist obligatorisch. Ohne den ONNX-Knoten ist die Anwendung nicht erfolgreich.

### Knotenerstellung

>[!NOTE]
>
> Je nach verwendetem Datentyp verfügen Sie wahrscheinlich über mehrere Knoten. Im folgenden Beispiel wird nur ein einzelner Knoten in der *Echtzeit-ML*-Vorlage beschrieben. Die vollständige Code-Zelle können Sie dem Abschnitt *Knotenerstellung* der *Echtzeit-ML*-Vorlage entnehmen.

Der nachstehende Pandas-Knoten verwendet `"import": "map"`, um den Methodennamen als Zeichenfolge in die Parameter zu importieren, gefolgt von der Eingabe der Parameter als Zuordnungsfunktion. Im folgenden Beispiel wird dazu `{'arg': {'dataLayerNull': 'notgiven', 'no': 'no', 'yes': 'yes', 'notgiven': 'notgiven'}}` verwendet. Nach erfolgter Zuordnung haben Sie die Möglichkeit, `inplace` als `True` oder `False` festzulegen. Legen Sie `inplace` als `True` oder `False` fest, je nachdem, ob Sie die Umwandlung an Ort und Stelle anwenden wollen oder nicht. Standardmäßig erstellt `"inplace": False` eine neue Spalte. Es ist geplant, die Unterstützung für die Bereitstellung eines neuen Spaltennamens in einer nachfolgenden Version hinzuzufügen. Die letzte Zeile `cols` kann ein einzelner Spaltenname oder eine Spaltenliste sein. Geben Sie die Spalten an, auf die Sie die Umwandlung anwenden wollen. In diesem Beispiel ist `leasing` festgelegt. Weiterführende Informationen zu den verfügbaren Knoten und deren Verwendung finden Sie im [Knotenreferenzhandbuch](./node-reference.md).

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

### Erstellen des DSL-Diagramms

Wenn Ihre Knoten erstellt wurden, besteht der nächste Schritt darin, die Knoten zu verketten, um ein Diagramm zu erstellen.

Listen Sie zunächst alle Knoten auf, die Teil des Diagramms sind, indem Sie ein Array erstellen.

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

Verbinden Sie dann die Knoten mit den Kanten. Jeder Tupel ist eine [!DNL Edge]-Verbindung.

>[!TIP]
>
> Da die Knoten linear voneinander abhängig sind (jeder Knoten hängt von der Ausgabe des vorherigen Knotens ab), können Sie Links mit einem einfachen Verständnis von Python-Listen erstellen. Bitte fügen Sie Ihre eigenen Verbindungen hinzu, wenn ein Knoten von mehreren Eingaben abhängig ist.

```python
edges = [(nodes[i], nodes[i+1]) for i in range(len(nodes)-1)]
```

Sobald Ihre Knoten verbunden sind, erstellen Sie das Diagramm. Die nachstehende Zelle ist obligatorisch und kann weder bearbeitet noch gelöscht werden.

```python
dsl = GraphBuilder.generate_dsl(nodes=nodes, edges=edges)
pprint(json.loads(dsl))
```

Nach Abschluss wird ein `edge`-Objekt zurückgegeben, das alle Knoten und die ihnen zugeordneten Parameter enthält.

![Edge-Rückgabe](../images/rtml/edge-return.png)

## Veröffentlichen in Edge (Hub)

>[!NOTE]
>
>Das maschinelle Lernen in Echtzeit wird vorübergehend vom Adobe Experience Platform-Hub bereitgestellt und von diesem verwaltet. Weitere Informationen finden Sie in der Übersicht zur [Architektur des maschinellen Lernens in Echtzeit](./home.md#architecture).

Nachdem Sie ein DSL-Diagramn erstellt haben, können Sie Ihr Diagramm für [!DNL Edge] bereitstellen.

>[!IMPORTANT]
>
>Veröffentlichen Sie nicht zu häufig in [!DNL Edge]. Dies kann die [!DNL Edge]-Knoten überlasten. Es wird davon abgeraten, dasselbe Modell mehrmals zu veröffentlichen.

```python
edge_utils = EdgeUtils()
(edge_location, service_id) = edge_utils.publish_to_edge(dsl=dsl)
print(f'Edge Location: {edge_location}')
print(f'Service ID: {service_id}')
```

### Aktualisieren der DSL und erneutes Veröffentlichen in Edge (optional)

Wenn Sie Ihre DSL nicht aktualisieren müssen, können Sie mit der [Bewertung](#scoring) weitermachen.

>[!NOTE]
>
>Die folgenden Zellen sind nur erforderlich, wenn Sie eine vorhandene DSL aktualisieren möchten, die in Edge veröffentlicht wurde.

Ihre Modelle werden sich wahrscheinlich weiter entwickeln. Anstatt einen völlig neuen Service zu erstellen, ist es möglich, einen vorhandenen Service mit Ihrem neuen Modell zu aktualisieren. Sie können einen Knoten definieren, den Sie aktualisieren möchten, ihm eine neue ID zuweisen und dann die neue DSL erneut in [!DNL Edge] hochladen.

Im folgenden Beispiel wird Knoten 0 mit einer neuen ID aktualisiert.

```python
# Update the id of Node 0 with a random uuid.

dsl_dict = json.loads(dsl)
print(f"ID of Node 0 in current DSL: {dsl_dict['edge']['applicationDsl']['nodes'][0]['id']}")

new_node_id = str(uuid.uuid4())
print(f'Updated Node ID: {new_node_id}')

dsl_dict['edge']['applicationDsl']['nodes'][0]['id'] = new_node_id
```

![Aktualisierter Knoten](../images/rtml/updated-node.png)

Nach dem Aktualisieren der Knoten-ID können Sie eine aktualisierte DSL erneut in Edge veröffentlichen.

```python
# Republish the updated DSL to Edge
(edge_location_ret, service_id, updated_dsl) = edge_utils.update_deployment(dsl=json.dumps(dsl_dict), service_id=service_id)
print(f'Updated dsl: {updated_dsl}')
```

Sie erhalten die aktualisierte DSL zurück.

![Aktualisierte DSL](../images/rtml/updated-dsl.png)

## Bewertung {#scoring}

Nach der Veröffentlichung in [!DNL Edge] erfolgt die Bewertung durch eine Client-seitige POST-Anfrage. Normalerweise kann dies über eine Client-Anwendung erfolgen, die ML-Bewertungen benötigt. Eine weitere Möglichkeit ist hier Postman. Die **[!UICONTROL Echtzeit-ML]**-Vorlage verwendet EdgeUtils, um diesen Vorgang zu zeigen.

>[!NOTE]
>
>Vor der Bewertung ist ein wenig Verarbeitungszeit erforderlich.

```python
# Wait for the app to come up
import time
time.sleep(20)
```

Mit demselben Schema, das für das Training verwendet wurde, werden beispielhafte Bewertungsdaten generiert. Diese Daten werden zum Erstellen eines Bewertungsdatenrahmens verwendet, der dann in ein Bewertungsverzeichnis konvertiert wird. Die vollständige Code-Zelle können Sie der *Echtzeit-ML*-Vorlage entnehmen.

![Bewertungsdaten](../images/rtml/generate-score-data.png)

### Bewerten gegenüber dem Edge-Endpunkt

Verwenden Sie die folgende Zelle in der *Echtzeit-ML*-Vorlage, um eine Bewertung gegenüber Ihrem [!DNL Edge]-Service durchzuführen.

![Bewerten gegenüber Edge](../images/rtml/scoring-edge.png)

Nach der Bewertung wird die [!DNL Edge]-URL, -Payload und -Ergebnisausgabe aus [!DNL Edge] zurückgegeben.

## Auflisten der in [!DNL Edge] bereitgestellten Apps

Um eine Liste Ihrer derzeit in [!DNL Edge] bereitgestellten Apps zu erstellen, führen Sie die folgende Code-Zelle aus. Diese Zelle kann nicht bearbeitet oder gelöscht werden.

```python
services = edge_utils.list_deployed_services()
print(services)
```

Die zurückgegebene Antwort ist ein Array Ihrer bereitgestellten Services.

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

## Löschen einer bereitgestellten App oder Service-ID aus [!DNL Edge] (optional)

>[!CAUTION]
>
>Diese Zelle wird zum Löschen Ihrer bereitgestellten Edge-Anwendung verwendet. Verwenden Sie die folgende Zelle nur, wenn Sie eine bereitgestellte [!DNL Edge]-Anwendung löschen müssen.

```python
if edge_utils.delete_from_edge(service_id=service_id):
    print(f"Deleted service id {service_id} successfully")
else:
    print(f"Failed to delete service id {service_id}")
```

## Nächste Schritte

Mithilfe des oben stehenden Tutorials haben Sie erfolgreich ein ONNX-Modell trainiert und in den Modellspeicher für maschinelles Lernen in Echtzeit hochgeladen. Darüber hinaus haben Sie Ihr Modell für maschinelles Lernen in Echtzeit bewertet und bereitgestellt. Weitere Informationen zu den Knoten, die für die Modellbearbeitung verfügbar sind, finden Sie im [Knotenreferenzhandbuch](./node-reference.md).
