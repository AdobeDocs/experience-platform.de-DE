---
keywords: Experience Platform;Entwicklerhandbuch;SDK;Datenzugriff SDK;Data Science Workspace;beliebte Themen
solution: Experience Platform
title: Modellerstellung mit der Adobe Experience Platform SDK
description: In diesem Tutorial erhalten Sie Informationen zum Konvertieren von data_access_sdk_python in das neue Python platform_sdk sowohl in Python als auch in R.
exl-id: 20909cae-5cd2-422b-8dbb-35bc63e69b2a
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 58%

---

# Modellerstellung mit Adobe [!DNL Experience Platform] SDK

>[!NOTE]
>
>Data Science Workspace ist nicht mehr erhältlich.
>
>Diese Dokumentation richtet sich an Bestandskunden mit vorherigen Berechtigungen für Data Science Workspace.

Diese Anleitung bietet Ihnen Informationen zum Konvertieren von `data_access_sdk_python` in das neue Python `platform_sdk` in sowohl Python als auch R. Diese Anleitung enthält Informationen zu den folgenden Vorgängen:

- [Authentifizierung erstellen](#build-authentication)
- [Grundlegendes Datenlesen](#basic-reading-of-data)
- [Grundlegendes Datenschreiben](#basic-writing-of-data)

## Authentifizierung erstellen {#build-authentication}

Für Aufrufe an [!DNL Adobe Experience Platform] ist eine Authentifizierung erforderlich, die aus einem API-Schlüssel, einer Organisations-ID, einem Benutzer-Token und einem Service-Token besteht.

### Python

Wenn Sie Jupyter Notebook verwenden, nutzen Sie den folgenden Code, um den `client_context` zu erstellen:

```python
client_context = PLATFORM_SDK_CLIENT_CONTEXT
```

Wenn Sie Jupyter Notebook nicht verwenden oder die Organisation ändern müssen, verwenden Sie das folgende Codebeispiel:

```python
from platform_sdk.client_context import ClientContext
client_context = ClientContext(api_key={API_KEY},
              org_id={ORG_ID},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

### R

Wenn Sie Jupyter Notebook verwenden, nutzen Sie den folgenden Code, um den `client_context` zu erstellen:

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")

py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
```

Wenn Sie Jupyter Notebook nicht verwenden oder die Organisation ändern müssen, verwenden Sie das folgende Codebeispiel:

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
client_context <- psdk$client_context$ClientContext(api_key={API_KEY},
              org_id={ORG_ID},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

## Grundlegendes Datenlesen {#basic-reading-of-data}

Mit dem neuen [!DNL Experience Platform] SDK beträgt die maximale Lesegröße 32 GB bei einer maximalen Lesezeit von 10 Minuten.

Wenn das Lesen zu lange dauert, können Sie eine der folgenden Filteroptionen verwenden:

- [Filtern von Daten nach Offset und Limit](#filter-by-offset-and-limit)
- [Daten nach Datum filtern](#filter-by-date)
- [Daten nach Spalte filtern](#filter-by-selected-columns)
- [Sortierergebnisse werden abgerufen](#get-sorted-results)

>[!NOTE]
>
>Die Organisation wird innerhalb der `client_context` festgelegt.

### Python

Zum Lesen von Daten in Python verwenden Sie bitte das folgende Code-Beispiel:

```python
from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.limit(100).read()
df.head()
```

### R

Zum Lesen von Daten in R verwenden Sie bitte das folgende Code-Beispiel:

```r
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$read() 
df
```

## Nach Offset und Limit filtern {#filter-by-offset-and-limit}

Da das Filtern nach Batch-Kennung nicht mehr unterstützt wird, müssen Sie zum Begrenzen des Datenlesens `offset` und `limit` verwenden.

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

Die Granularität der Datumsfilterung wird jetzt durch den Zeitstempel definiert und nicht mehr durch den Tag.

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

Die neue [!DNL Experience Platform] SDK unterstützt die folgenden Vorgänge:

| Vorgang | Funktion |
| --------- | -------- |
| Gleich (`=`) | `eq()` |
| Größer als (`>`) | `gt()` |
| Größer oder gleich (`>=`) | `ge()` |
| Niedriger als (`<`) | `lt()` |
| Kleiner oder gleich (`<=`) | `le()` |
| Und (`&`) | `And()` |
| Oder (`|`) | `Or()` |

## Nach ausgewählten Spalten filtern {#filter-by-selected-columns}

Zur weiteren Verfeinerung des Datenlesens können Sie auch nach Spaltennamen filtern.

### Python

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### R

```r
df <- dataset_reader$select(c('column-a','column-b'))$read() 
```

## Sortierte Ergebnisse abrufen {#get-sorted-results}

Die erhaltenen Ergebnisse können nach bestimmten Spalten des Zieldatensatzes und in ihrer Reihenfolge (aufsteigend/absteigend) sortiert werden.

Im folgenden Beispiel wird Dataframe zuerst in aufsteigender Reihenfolge nach „column-a“ sortiert. Zeilen mit den gleichen Werten für „column-a“ werden dann in absteigender Reihenfolge nach „column-b“ sortiert.

### Python

```python
df = dataset_reader.sort([('column-a', 'asc'), ('column-b', 'desc')])
```

### R

```r
df <- dataset_reader$sort(c(('column-a', 'asc'), ('column-b', 'desc')))$read()
```

## Grundlegendes Datenschreiben {#basic-writing-of-data}

>[!NOTE]
>
>Die Organisation wird innerhalb der `client_context` festgelegt.

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

Nachdem Sie den `platform_sdk`-Data-Loader konfiguriert haben, werden die Daten vorbereitet und auf die Datensätze `train` und `val` aufgeteilt. Informationen zur Datenvorbereitung und zum Feature Engineering finden Sie im Abschnitt [Datenvorbereitung und Feature Engineering](../jupyterlab/create-a-model.md#data-preparation-and-feature-engineering) im Tutorial zum Erstellen eines Rezepts mithilfe [!DNL JupyterLab] Notebooks.
