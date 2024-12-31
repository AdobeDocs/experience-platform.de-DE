---
keywords: Experience Platform;Startseite;beliebte Themen;Datenzugriff;Python-SDK;Datenzugriffs-API;Python lesen;Python schreiben
solution: Experience Platform
title: Zugreifen auf Daten mithilfe von Python in Data Science Workspace
type: Tutorial
description: Das folgende Dokument enthält Beispiele für den Zugriff auf Daten in Python zur Verwendung in Data Science Workspace.
exl-id: 75aafd58-634a-4df3-a2f0-9311f93deae4
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# Zugreifen auf Daten mithilfe von Python in Data Science Workspace

>[!NOTE]
>
>Data Science Workspace ist nicht mehr erhältlich.
>
>Diese Dokumentation richtet sich an Bestandskunden mit vorherigen Berechtigungen für Data Science Workspace.

Das folgende Dokument enthält Beispiele für den Zugriff auf Daten mithilfe von Python zur Verwendung in Data Science Workspace. Informationen zum Datenzugriff mithilfe von JupyterLab-Notebooks finden Sie in der Dokumentation [Datenzugriff über JupyterLab-Notebooks](../jupyterlab/access-notebook-data.md).

## Lesen eines Datensatzes

Nachdem Sie die Umgebungsvariablen festgelegt und die Installation abgeschlossen haben, kann Ihr Datensatz jetzt in den Pandas-Datenrahmen gelesen werden.

```python
import pandas as pd
from .utils import get_client_context
from platform_sdk.dataset_reader import DatasetReader

def load(config_properties):

client_context = get_client_context(config_properties)

dataset_reader = DatasetReader(client_context, config_properties['DATASET_ID'])

df = dataset_reader.read()
```

### Spalten aus dem Datensatz auswählen

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

Nachfolgend finden Sie ein Beispiel für die Verwendung dieser Filterfunktionen:

```python
df = dataset_reader.where(experience_ds['timestamp'].gt(87879779797).And(experience_ds['timestamp'].lt(87879779797)).Or(experience_ds['a'].eq(123)))
```

### ORDER BY-Klausel

Die ORDER BY-Klausel ermöglicht es, die empfangenen Ergebnisse nach einer angegebenen Spalte in einer bestimmten Reihenfolge (aufsteigend oder absteigend) zu sortieren. Dies geschieht mithilfe der `sort()`-Funktion.

Nachfolgend finden Sie ein Beispiel für die Verwendung der Funktion `sort()` :

```python
df = dataset_reader.sort([('column_1', 'asc'), ('column_2', 'desc')])
```

### LIMIT-Klausel

Mit der LIMIT-Klausel können Sie die Anzahl der vom Datensatz empfangenen Datensätze begrenzen.

Nachfolgend finden Sie ein Beispiel für die Verwendung der Funktion `limit()` :

```python
df = dataset_reader.limit(100).read()
```

### OFFSET-Klausel

Mit der OFFSET-Klausel können Sie Zeilen von Anfang an überspringen, um ab einem späteren Punkt Zeilen zurückzugeben. In Kombination mit LIMIT kann dies verwendet werden, um Zeilen in Blöcken zu iterieren.

Nachfolgend finden Sie ein Beispiel für die Verwendung der Funktion `offset()` :

```python
df = dataset_reader.offset(100).read()
```

## Schreiben eines Datensatzes

Um in einen Datensatz zu schreiben, müssen Sie den Pandas-Datenrahmen für Ihren Datensatz bereitstellen.

### Schreiben des Pandas-Datenrahmens

```python
client_context = get_client_context(config_properties)

# To fetch existing dataset
dataset = Dataset(client_context).get_by_id({DATASET_ID})

dataset_writer = DatasetWriter(client_context, dataset)

write_tracker = dataset_writer.write(<your_dataFrame>, file_format='json')
```

## Verzeichnis „Arbeitsbereich“ (Checkpoint)

Bei Aufträgen mit längerer Laufzeit müssen Sie möglicherweise Zwischenschritte speichern. In Instanzen wie diesen können Sie in einen Benutzerbereich lesen und schreiben.

>[!NOTE]
>
>Pfade zu den Daten werden **nicht** gespeichert. Sie müssen den entsprechenden Pfad zu den jeweiligen Daten speichern.

### In Benutzerbereich schreiben

```python
client_context = get_client_context(config_properties)
                               
user_helper = UserSpaceHelper(client_context)
user_helper.write(data_frame=<data_frame>, path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

### Aus Benutzerbereich lesen

```python
client_context = get_client_context(config_properties)
                               
user_helper = UserSpaceHelper(client_context)
my_df = user_helper.read(path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

## Nächste Schritte

Adobe Experience Platform Data Science Workspace bietet ein Rezeptbeispiel, das die obigen Codebeispiele zum Lesen und Schreiben von Daten verwendet. Weitere Informationen zur Verwendung von Python für den Zugriff auf Ihre Daten finden Sie im [Data Science Workspace Python GitHub-Repository](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail).
