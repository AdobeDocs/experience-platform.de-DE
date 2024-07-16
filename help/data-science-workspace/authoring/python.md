---
keywords: Experience Platform;home;popular topics;data access;python sdk;data access api;read python;write python
solution: Experience Platform
title: Zugriff auf Daten mithilfe von Python in Data Science Workspace
type: Tutorial
description: Das folgende Dokument enthält Beispiele für den Zugriff auf Daten in Python zur Verwendung in Data Science Workspace.
exl-id: 75aafd58-634a-4df3-a2f0-9311f93deae4
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# Zugriff auf Daten mit Python in Data Science Workspace

Das folgende Dokument enthält Beispiele für den Zugriff auf Daten mit Python zur Verwendung in Data Science Workspace. Informationen zum Zugriff auf Daten mit JupyterLab-Notebooks finden Sie in der Dokumentation zum Datenzugriff auf JupyterLab-Notebooks ](../jupyterlab/access-notebook-data.md).[

## Datensatz lesen

Nachdem Sie die Umgebungsvariablen festgelegt und die Installation abgeschlossen haben, kann Ihr Datensatz jetzt in den pandas-Dataframe gelesen werden.

```python
import pandas as pd
from .utils import get_client_context
from platform_sdk.dataset_reader import DatasetReader

def load(config_properties):

client_context = get_client_context(config_properties)

dataset_reader = DatasetReader(client_context, config_properties['DATASET_ID'])

df = dataset_reader.read()
```

### Spalten aus Datensatz auswählen

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

Mit der DISTINCT-Klausel können Sie alle eindeutigen Werte auf Zeilen-/Spaltenebene abrufen und alle doppelten Werte aus der Antwort entfernen.

Nachfolgend finden Sie ein Beispiel für die Verwendung der Funktion `distinct()` :

```python
df = dataset_reader.select(['column-a']).distinct().read()
```

### WHERE-Klausel

Sie können bestimmte Operatoren in Python verwenden, um Ihren Datensatz zu filtern.

>[!NOTE]
>
>Bei den Filterfunktionen wird zwischen Groß- und Kleinschreibung unterschieden.

```python
eq() = '='
gt() = '>'
ge() = '>='
lt() = '<'
le() = '<='
And = and operator
Or = or operator
```

Nachfolgend finden Sie ein Beispiel für die Verwendung dieser Filterfunktionen:

```python
df = dataset_reader.where(experience_ds['timestamp'].gt(87879779797).And(experience_ds['timestamp'].lt(87879779797)).Or(experience_ds['a'].eq(123)))
```

### ORDER BY-Klausel

Die &quot;ORDER BY&quot;-Klausel ermöglicht die Sortierung der empfangenen Ergebnisse nach einer bestimmten Spalte in einer bestimmten Reihenfolge (aufsteigend oder absteigend). Dies geschieht mithilfe der Funktion `sort()` .

Nachfolgend finden Sie ein Beispiel für die Verwendung der Funktion `sort()` :

```python
df = dataset_reader.sort([('column_1', 'asc'), ('column_2', 'desc')])
```

### LIMIT-Klausel

Die LIMIT-Klausel ermöglicht es Ihnen, die Anzahl der vom Datensatz empfangenen Datensätze zu begrenzen.

Nachfolgend finden Sie ein Beispiel für die Verwendung der Funktion `limit()` :

```python
df = dataset_reader.limit(100).read()
```

### OFFSET-Klausel

Mit der OFFSET-Klausel können Sie Zeilen von Anfang an überspringen, um Zeilen von einem späteren Zeitpunkt an zurückzugeben. In Kombination mit LIMIT kann dies zum Iterieren von Zeilen in Blöcken verwendet werden.

Nachfolgend finden Sie ein Beispiel für die Verwendung der Funktion `offset()` :

```python
df = dataset_reader.offset(100).read()
```

## Schreiben eines Datensatzes

Um in einen Datensatz zu schreiben, müssen Sie den pandas-Dataframe in Ihren Datensatz einfügen.

### Schreiben des pandas-Dataframes

```python
client_context = get_client_context(config_properties)

# To fetch existing dataset
dataset = Dataset(client_context).get_by_id({DATASET_ID})

dataset_writer = DatasetWriter(client_context, dataset)

write_tracker = dataset_writer.write(<your_dataFrame>, file_format='json')
```

## Benutzeroberflächenverzeichnis (Checkpoint)

Für Aufträge, die länger ausgeführt werden, müssen Sie möglicherweise Zwischenschritte speichern. In solchen Fällen können Sie in einen Benutzerbereich lesen und schreiben.

>[!NOTE]
>
>Pfade zu den Daten werden **nicht** gespeichert. Sie müssen den entsprechenden Pfad zu den entsprechenden Daten speichern.

### Schreiben in den Benutzerbereich

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

Adobe Experience Platform Data Science Workspace bietet ein Rezept-Beispiel, in dem die oben genannten Codebeispiele zum Lesen und Schreiben von Daten verwendet werden. Wenn Sie mehr darüber erfahren möchten, wie Sie mit Python auf Ihre Daten zugreifen können, lesen Sie bitte das [Data Science Workspace Python GitHub-Repository](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail).
