---
keywords: Experience Platform;developer guide;SDK;Data Access SDK;Data Science Workspace;popular topics
solution: Experience Platform
title: Handbuch zum Plattform-SDK
topic: SDK authoring
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 5%

---


# Handbuch zum Plattform-SDK

Dieses Tutorial bietet Informationen zum Konvertieren `data_access_sdk_python` in den neuen Python `platform_sdk` in Python und R. Dieses Lernprogramm enthält Informationen zu den folgenden Vorgängen:

- [Authentifizierung erstellen](#build-authentication)
- [Grundlegende Datenauswertung](#basic-reading-of-data)
- [Grundlegende Datenverarbeitung](#basic-writing-of-data)

## Authentifizierung erstellen {#build-authentication}

Die Authentifizierung ist erforderlich, um Aufrufe an Adobe Experience Platform durchzuführen. Sie besteht aus API-Schlüssel, IMS-Organisations-ID, einem Benutzertoken und einem Service-Token.

### Python

Wenn Sie Jupyter-Notebook verwenden, verwenden Sie den folgenden Code, um die `client_context`:

```python
client_context = PLATFORM_SDK_CLIENT_CONTEXT
```

Wenn Sie kein Jupyter-Notebook verwenden oder das IMS-Org ändern müssen, verwenden Sie bitte das folgende Codebeispiel:

```python
from platform_sdk.client_context import ClientContext
client_context = ClientContext(api_key={API_KEY},
              org_id={IMS_ORG},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

### R

Wenn Sie Jupyter-Notebook verwenden, verwenden Sie den folgenden Code, um die `client_context`:

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")

py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
```

Wenn Sie kein Jupyter-Notebook verwenden oder das IMS-Org ändern müssen, verwenden Sie bitte das folgende Codebeispiel:

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
client_context <- psdk$client_context$ClientContext(api_key={API_KEY},
              org_id={IMS_ORG},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

## Grundlegende Datenauswertung {#basic-reading-of-data}

Mit dem neuen Plattform-SDK beträgt die maximale Lesegröße 32 GB mit einer maximalen Lesedauer von 10 Minuten.

Wenn Ihre Lesezeit zu lang dauert, können Sie eine der folgenden Filteroptionen verwenden:

- [Filtern von Daten nach Offset und Limit](#filter-by-offset-and-limit)
- [Filtern von Daten nach Datum](#filter-by-date)
- [Filtern von Daten nach Spalten](#filter-by-selected-columns)
- [Sortierte Ergebnisse abrufen](#get-sorted-results)

>[!NOTE] Das IMS-Org wird innerhalb der `client_context`Variablen festgelegt.

### Python

Zum Lesen von Daten in Python verwenden Sie bitte das folgende Codebeispiel:

```python
from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.limit(100).read()
df.head()
```

### R

Zum Lesen von Daten in R verwenden Sie bitte das folgende Codebeispiel:

```r
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$read() 
df
```

## Filtern nach Offset und Limit {#filter-by-offset-and-limit}

Da das Filtern nach Batch-ID nicht mehr unterstützt wird, müssen Sie Daten verwenden `offset` `limit`und lesen, um den Umfang zu verändern.

### Python

```python
df = dataset_reader.limit(100).offset(1).read()
df.head
```

### R

```r
df <- dataset_reader$limit(100L)$offset(1L)$read() 
df
```

## Nach Datum filtern {#filter-by-date}

Die Granularität der Datumsfilterung wird jetzt durch den Zeitstempel definiert und nicht durch den Tag festgelegt.

### Python

```python
df = dataset_reader.where(\
    dataset_reader['timestamp'].gt('2019-04-10 15:00:00').\
    And(dataset_reader['timestamp'].lt('2019-04-10 17:00:00'))\
).read()
df.head()
```

### R

```r
df2 <- dataset_reader$where(
    dataset_reader['timestamp']$gt('2018-12-10 15:00:00')$
    And(dataset_reader['timestamp']$lt('2019-04-10 17:00:00'))
)$read()
df2
```

Das neue Plattform-SDK unterstützt die folgenden Vorgänge:

| Vorgang | Funktion |
| --------- | -------- |
| Gleich (`=`) | `eq()` |
| Größer als (`>`) | `gt()` |
| Größer oder gleich (`>=`) | `ge()` |
| Niedriger als (`<`) | `lt()` |
| Kleiner oder gleich (`<=`) | `le()` |
| And (`&`) | `And()` |
| Oder (`|`) | `Or()` |

## Nach ausgewählten Spalten filtern {#filter-by-selected-columns}

Zur weiteren Verfeinerung des Lesens von Daten können Sie auch nach Spaltennamen filtern.

### Python

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### R

```r
df <- dataset_reader$select(c('column-a','column-b'))$read() 
```

## Sortierte Ergebnisse abrufen {#get-sorted-results}

Die erhaltenen Ergebnisse können nach bestimmten Spalten des Datensatzes der Zielgruppe und in ihrer Reihenfolge (asc/desc) sortiert werden.

Im folgenden Beispiel wird Dataframe zuerst in aufsteigender Reihenfolge nach &quot;column-a&quot;sortiert. Zeilen mit den gleichen Werten für &quot;column-a&quot;werden dann in absteigender Reihenfolge nach &quot;column-b&quot;sortiert.

### Python

```python
df = dataset_reader.sort([('column-a', 'asc'), ('column-b', 'desc')])
```

### R

```r
df <- dataset_reader$sort(c(('column-a', 'asc'), ('column-b', 'desc')))$read()
```

## Grundlegende Datenverarbeitung {#basic-writing-of-data}

>[!NOTE] Das IMS-Org wird innerhalb der `client_context`Variablen festgelegt.

Um Daten in Python und R zu schreiben, verwenden Sie eines der folgenden Beispiele:

### Python

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(client_context).get_by_id("{DATASET_ID}")
dataset_writer = DatasetWriter(client_context, dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### R

```r
dataset <- psdk$models$Dataset(client_context)$get_by_id("{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(client_context, dataset)
write_tracker <- dataset_writer$write({PANDA_DATAFRAME}, file_format='json')
```

## Nächste Schritte

Nachdem Sie den `platform_sdk` Datenladevorgang konfiguriert haben, werden die Daten vorbereitet und in die Datasets `train` und `val` Datensätze aufgeteilt. Informationen zur Datenvorbereitung und zur Funktionstechnik finden Sie im Abschnitt zur [Datenvorbereitung und Funktionstechnik](../jupyterlab/create-a-recipe.md#data-preparation-and-feature-engineering) im Tutorial zum Erstellen eines Skripts mit JupyterLab-Notebooks.