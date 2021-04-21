---
keywords: Experience Platform;Home;beliebte Themen;Datenzugriff;Python-SDK;Datenzugriffs-API;Lesen-Python;Schreiben-Python
solution: Experience Platform
title: Zugriff auf Daten mithilfe von Python in Data Science Workspace
topic-legacy: tutorial
type: Tutorial
description: Das folgende Dokument enthält Beispiele für den Zugriff auf Daten in Python zur Verwendung in Data Science Workspace.
exl-id: 75aafd58-634a-4df3-a2f0-9311f93deae4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 2%

---

# Zugriff auf Daten mithilfe von Python in Data Science Workspace

Das folgende Dokument enthält Beispiele für den Zugriff auf Daten mit Python zur Verwendung in Data Science Workspace. Informationen zum Zugriff auf Daten mit JupyterLab-Notebooks finden Sie in der Dokumentation [JupyterLab-Notebook-Datenzugriff](../jupyterlab/access-notebook-data.md).

## Lesen eines Datensatzes

Nach dem Festlegen der Umgebung-Variablen und dem Abschluss der Installation kann der Datensatz jetzt in den Pandas-Dataframe gelesen werden.

```python
import pandas as pd
from .utils import get_client_context
from platform_sdk.dataset_reader import DatasetReader

def load(config_properties):

client_context = get_client_context(config_properties)

dataset_reader = DatasetReader(client_context, config_properties['DATASET_ID'])

df = dataset_reader.read()
```

### Spalten aus dem Datensatz AUSWÄHLEN

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### Partitionierungsinformationen abrufen:

```python
client_context = get_client_context(config_properties)

dataset = Dataset(client_context).get_by_id({DATASET_ID})
partitions = dataset.get_partitions_info()
```

### DISTINCT-Klausel

Mit der DISTINCT-Klausel können Sie alle eindeutigen Werte auf Zeilen-/Spaltenebene abrufen und alle Duplikat-Werte aus der Antwort entfernen.

Ein Beispiel für die Verwendung der Funktion `distinct()` ist unten aufgeführt:

```python
df = dataset_reader.select(['column-a']).distinct().read()
```

### WO-Klausel

Sie können bestimmte Operatoren in Python verwenden, um Ihren Datensatz zu filtern.

>[!NOTE]
>
>Bei den zum Filtern verwendeten Funktionen wird zwischen Groß- und Kleinschreibung unterschieden.

```python
eq() = '='
gt() = '>'
ge() = '>='
lt() = '<'
le() = '<='
And = and operator
Or = or operator
```

Nachfolgend sehen Sie ein Beispiel für die Verwendung dieser Filterfunktionen:

```python
df = dataset_reader.where(experience_ds['timestamp'].gt(87879779797).And(experience_ds['timestamp'].lt(87879779797)).Or(experience_ds['a'].eq(123)))
```

### ORDER BY-Klausel

Die ORDER BY-Klausel ermöglicht es, die empfangenen Ergebnisse in einer bestimmten Reihenfolge (aufsteigend oder absteigend) nach einer bestimmten Spalte zu sortieren. Dies geschieht mit der Funktion `sort()`.

Ein Beispiel für die Verwendung der Funktion `sort()` ist unten aufgeführt:

```python
df = dataset_reader.sort([('column_1', 'asc'), ('column_2', 'desc')])
```

### LIMIT-Klausel

Die LIMIT-Klausel ermöglicht es Ihnen, die Anzahl der vom Datensatz erhaltenen Datensätze zu begrenzen.

Ein Beispiel für die Verwendung der Funktion `limit()` ist unten aufgeführt:

```python
df = dataset_reader.limit(100).read()
```

### OFFSET-Klausel

Mit der OFFSET-Klausel können Sie Zeilen von Anfang an überspringen, bis der Beginn Zeilen von einem späteren Zeitpunkt zurückgibt. In Verbindung mit LIMIT kann dies zur Iteration von Zeilen in Blöcken verwendet werden.

Ein Beispiel für die Verwendung der Funktion `offset()` ist unten aufgeführt:

```python
df = dataset_reader.offset(100).read()
```

## Schreiben eines Datensatzes

Um in einen Datensatz zu schreiben, müssen Sie den Pandas-Dataframe an Ihren Datensatz liefern.

### Schreiben des Pandas-Dataframs

```python
client_context = get_client_context(config_properties)

# To fetch existing dataset
dataset = Dataset(client_context).get_by_id({DATASET_ID})

dataset_writer = DatasetWriter(client_context, dataset)

write_tracker = dataset_writer.write(<your_dataFrame>, file_format='json')
```

## Verzeichnis &quot;Userspace&quot;(Checkpoint)

Bei längeren Aufträgen müssen Sie eventuell Zwischenschritte speichern. In solchen Fällen können Sie in einem Benutzerbereich lesen und schreiben.

>[!NOTE]
>
>Die Pfade zu den Daten werden nicht **gespeichert.** Sie müssen den entsprechenden Pfad zu den entsprechenden Daten speichern.

### In den Benutzerbereich schreiben

```python
client_context = get_client_context(config_properties)
                               
user_helper = UserSpaceHelper(client_context)
user_helper.write(data_frame=<data_frame>, path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

### Aus dem Benutzerbereich lesen

```python
client_context = get_client_context(config_properties)
                               
user_helper = UserSpaceHelper(client_context)
my_df = user_helper.read(path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

## Nächste Schritte

Adobe Experience Platform Data Science Workspace bietet ein Rezept, in dem die oben genannten Codebeispiele zum Lesen und Schreiben von Daten verwendet werden. Wenn Sie mehr darüber erfahren möchten, wie Sie Python für den Zugriff auf Ihre Daten verwenden, lesen Sie bitte das [Data Science Workspace Python GitHub Repository](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail).
