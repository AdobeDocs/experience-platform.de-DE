---
keywords: Experience Platform;JupyterLab;Notebooks;Datenwissenschafts-Workspace;beliebte Themen;%dataset;interaktiver Modus;Batch-Modus;Spark SDK;Python SDK;Zugriffsdaten;Notebook-Datenzugriff
solution: Experience Platform
title: Datenzugriff in JupyterLab-Notebooks
description: In diesem Handbuch wird beschrieben, wie Sie mit Jupyter Notebooks, die in Data Science Workspace erstellt wurden, auf Ihre Daten zugreifen können.
exl-id: 2035a627-5afc-4b72-9119-158b95a35d32
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '3346'
ht-degree: 23%

---

# Datenzugriff in [!DNL Jupyterlab] Notebooks

>[!NOTE]
>
>Data Science Workspace ist nicht mehr erhältlich.
>
>Diese Dokumentation richtet sich an Bestandskunden mit vorherigen Berechtigungen für Data Science Workspace.

Jeder unterstützte Kernel bietet integrierte Funktionen, mit denen Sie Experience Platform-Daten aus einem Datensatz innerhalb eines Notebooks lesen können. Derzeit unterstützt JupyterLab in Adobe Experience Platform Data Science Workspace Notebooks für [!DNL Python], R, PySpark und Scala. Die Unterstützung für die Paginierung von Daten ist jedoch auf [!DNL Python]- und R-Notebooks beschränkt. In diesem Handbuch wird beschrieben, wie Sie mit JupyterLab-Notebooks auf Ihre Daten zugreifen können.

## Erste Schritte

Bevor Sie dieses Handbuch lesen, lesen Sie [[!DNL JupyterLab] Benutzerhandbuch](./overview.md) um eine allgemeine Einführung in [!DNL JupyterLab] und seine Rolle in Data Science Workspace zu erhalten.

## Notebook-Datenbeschränkungen {#notebook-data-limits}

>[!IMPORTANT]
>
>Für PySpark- und Scala-Notebooks, wenn Sie einen Fehler mit der Ursache „Remote-RPC-Client getrennt“ erhalten. Dies bedeutet in der Regel, dass dem Treiber oder einem Executor nicht mehr genügend Speicher zur Verfügung steht. Versuchen Sie, in [ „Batch“-Modus ](#mode) wechseln, um diesen Fehler zu beheben.

Die folgenden Informationen definieren die maximale Datenmenge, die gelesen werden kann, den verwendeten Datentyp und den geschätzten Zeitrahmen für das Lesen der Daten.

Für [!DNL Python] und R wurde ein Notebook-Server mit 40 GB RAM für die Benchmarks verwendet. Für PySpark und Scala wurde ein Databricks-Cluster mit 64 GB RAM, 8 Kernen, 2 DBU und maximal 4 Workern für die unten beschriebenen Benchmarks verwendet.

Die verwendeten ExperienceEvent-Schemadaten variierten in der Größe, beginnend mit eintausend (1K) Zeilen, die bis zu einer Milliarde (1B) Zeilen reichten. Beachten Sie, dass für die PySpark- und [!DNL Spark]-Metriken ein Datumsbereich von 10 Tagen für die XDM-Daten verwendet wurde.

Die Ad-hoc-Schemadaten wurden mit [!DNL Query Service] CREATE TABLE AS SELECT (CTAS) vorverarbeitet. Diese Daten variierten auch in der Größe, beginnend mit eintausend (1K) Zeilen, die bis zu einer Milliarde (1B) Zeilen reichten.

### Wann der Batch-Modus oder der interaktive Modus verwendet werden sollte {#mode}

Beim Lesen von Datensätzen mit PySpark- und Scala-Notebooks haben Sie die Möglichkeit, den Datensatz im interaktiven Modus oder im Batch-Modus zu lesen. Interaktiv sorgt für schnelle Ergebnisse, während der Batch-Modus für große Datensätze geeignet ist.

- Bei PySpark- und Scala-Notebooks sollte der Batch-Modus verwendet werden, wenn mindestens 5 Millionen Datenzeilen gelesen werden. Weitere Informationen zur Effizienz der einzelnen Modi finden Sie in den [PySpark](#pyspark-data-limits)- oder [Scala](#scala-data-limits)-Datentabellen unten.

### [!DNL Python] Notebook-Datenbeschränkungen

**XDM ExperienceEvent-Schema:** Sie sollten in der Lage sein, maximal 2 Millionen Zeilen (ca. 6,1 GB Daten auf der Festplatte) von XDM-Daten in weniger als 22 Minuten zu lesen. Das Hinzufügen zusätzlicher Zeilen kann zu Fehlern führen.

| Anzahl Zeilen | 1.000 | 10.000 | 100.000 | 1 Mio. | 2 M |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| Größe auf der Festplatte (MB) | 18,73 | 187,5 | 308 | 3000 | 6050 |
| SDK (in Sekunden) | 20,3 | 86,8 | 63 | 659 | 1315 |

**Ad-hoc-Schema:** Sie sollten in der Lage sein, maximal 5 Millionen Zeilen (ca. 5,6 GB Daten auf der Festplatte) von Nicht-XDM (Ad-hoc)-Daten in weniger als 14 Minuten zu lesen. Das Hinzufügen zusätzlicher Zeilen kann zu Fehlern führen.

| Anzahl Zeilen | 1.000 | 10.000 | 100.000 | 1 Mio. | 2 M | 3 M | 5m |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| Größe auf der Festplatte (in MB) | 1,21 | 11,72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK (in Sekunden) | 7,27 | 9,04 | 27,3 | 180 | 346 | 487 | 819 |

### R Notebook-Datenbeschränkungen

**XDM ExperienceEvent-Schema:** Sie sollten maximal 1 Million XDM-Datenzeilen (3 GB-Daten auf der Festplatte) in weniger als 13 Minuten lesen können.

| Anzahl Zeilen | 1.000 | 10.000 | 100.000 | 1 Mio. |
| ----------------------- | ------ | ------ | ----- | ----- |
| Größe auf der Festplatte (MB) | 18,73 | 187,5 | 308 | 3000 |
| R-Kernel (in Sekunden) | 14,03 | 69,6 | 86,8 | 775 |

**Ad-hoc-Schema:** Sie sollten in der Lage sein, maximal 3 Millionen Zeilen mit Ad-hoc-Daten (293 MB Daten auf der Festplatte) in etwa 10 Minuten zu lesen.

| Anzahl Zeilen | 1.000 | 10.000 | 100.000 | 1 Mio. | 2 M | 3 M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| Größe auf der Festplatte (in MB) | 0,082 | 0,612 | 9.0 | 91 | 188 | 293 |
| R SDK (in s) | 7,7 | 4,58 | 35,9 | 233 | 470,5 | 603 |

### Datenbeschränkungen des PySpark-Notebooks ([!DNL Python]-Kernel): {#pyspark-data-limits}

**XDM ExperienceEvent-Schema:** Im interaktiven Modus sollten Sie in der Lage sein, maximal 5 Millionen Zeilen (ca. 13,42 GB Daten auf der Festplatte) von XDM-Daten in etwa 20 Minuten zu lesen. Der interaktive Modus unterstützt nur bis zu 5 Millionen Zeilen. Wenn Sie größere Datensätze lesen möchten, wird empfohlen, in den Batch-Modus zu wechseln. Im Batch-Modus sollten Sie in der Lage sein, maximal 500 Millionen Zeilen (ca. 1,31 TB Daten auf der Festplatte) von XDM-Daten in etwa 14 Stunden zu lesen.

| Anzahl Zeilen | 1.000 | 10.000 | 100.000 | 1 Mio. | 2 M | 3 M | 5m | 10 M | 50 M | 100 M | 500 Mio. |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Größe auf der Festplatte | 2,93MB | 4,38MB | 29,02 | 2,69GB | 5,39GB | 8,09GB | 13,42GB | 26,82GB | 134,24GB | 268,39GB | 1,31 TB |
| SDK (interaktiver Modus) | 33er | 32,4 s | 55,1 s | 253,5 s | 489,2 s | 729,6 s | 1 206,8 s | – | – | – | – |
| SDK (Batchmodus) | 815,8 s | 492,8 s | 379,1 s | 637,4 s | 624,5 s | 869,2 s | 1 104,1s | 1 786 s | 5 387,2 s | 10624,6s | 50547s |

**Ad-hoc-Schema:** Im interaktiven Modus sollten Sie in der Lage sein, maximal 5 Millionen Zeilen (ca. 5,36 GB Daten auf der Festplatte) von Nicht-XDM-Daten in weniger als 3 Minuten zu lesen. Im Batch-Modus sollten Sie in der Lage sein, maximal 1 Milliarde Zeilen (~1,05 TB Daten auf der Festplatte) von Nicht-XDM-Daten in etwa 18 Minuten zu lesen.

| Anzahl Zeilen | 1.000 | 10.000 | 100.000 | 1 Mio. | 2 M | 3 M | 5m | 10 M | 50 M | 100 M | 500 Mio. | 1b |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| Größe auf Festplatte | 1,12MB | 11,24MB | 109,48MB | 2,69GB | 2,14GB | 3,21GB | 5,36GB | 10,71GB | 53,58GB | 107,52GB | 535,88GB | 1,05 TB |
| Interaktiver SDK-Modus (in Sekunden) | 28,2 s | 18,6s | 20,8 s | 20,9 s | 23,8 s | 21,7 s | 24,7 s | – | – | – | – | – |
| SDK-Batch-Modus (in Sekunden) | 428,8 s | 578,8 s | 641,4 s | 538,5 s | 630,9 s | 467,3 s | 411 s | 675 s | 702 s | 719,2 s | 1 022,1 s | 1 122,3 s |

### [!DNL Spark] (Scala-Kernel) Notebook-Datenbeschränkungen: {#scala-data-limits}

**XDM ExperienceEvent-Schema:** Im interaktiven Modus sollten Sie in der Lage sein, maximal 5 Millionen Zeilen (ca. 13,42 GB Daten auf der Festplatte) von XDM-Daten in etwa 18 Minuten zu lesen. Der interaktive Modus unterstützt nur bis zu 5 Millionen Zeilen. Wenn Sie größere Datensätze lesen möchten, wird empfohlen, in den Batch-Modus zu wechseln. Im Batch-Modus sollten Sie in der Lage sein, maximal 500 Millionen Zeilen (ca. 1,31 TB Daten auf der Festplatte) von XDM-Daten in etwa 14 Stunden zu lesen.

| Anzahl Zeilen | 1.000 | 10.000 | 100.000 | 1 Mio. | 2 M | 3 M | 5m | 10 M | 50 M | 100 M | 500 Mio. |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Größe auf Festplatte | 2,93MB | 4,38MB | 29,02 | 2,69GB | 5,39GB | 8,09GB | 13,42GB | 26,82GB | 134,24GB | 268,39GB | 1,31 TB |
| Interaktiver SDK-Modus (in Sekunden) | 37,9 s | 22,7 s | 45,6 s | 231,7 s | 444,7 s | 660,6 s | 1100er | – | – | – | – |
| SDK-Batch-Modus (in Sekunden) | 374,4 s | 398,5 s | 527 s | 487,9 s | 588,9 s | 829 s | 939,1 s | 1 441 s | 5 473,2 s | 10118,8 | 49207,6 |

**Ad-hoc-Schema:** Im interaktiven Modus sollten Sie in der Lage sein, maximal 5 Millionen Zeilen (ca. 5,36 GB Daten auf der Festplatte) von Nicht-XDM-Daten in weniger als 3 Minuten zu lesen. Im Batch-Modus sollten Sie in der Lage sein, maximal 1 Milliarde Zeilen (~1,05 TB Daten auf der Festplatte) von Nicht-XDM-Daten in etwa 16 Minuten zu lesen.

| Anzahl Zeilen | 1.000 | 10.000 | 100.000 | 1 Mio. | 2 M | 3 M | 5m | 10 M | 50 M | 100 M | 500 Mio. | 1b |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| Größe auf Festplatte | 1,12MB | 11,24MB | 109,48MB | 2,69GB | 2,14GB | 3,21GB | 5,36GB | 10,71GB | 53,58GB | 107,52GB | 535,88GB | 1,05 TB |
| Interaktiver SDK-Modus (in Sekunden) | 35,7 s | 31s | 19,5 s | 25,3 s | 23er | 33,2 s | 25,5 s | – | – | – | – | – |
| SDK-Batch-Modus (in Sekunden) | 448,8 s | 459,7 s | 519 s | 475,8 s | 599,9 s | 347,6 s | 407,8 s | 397 s | 518,8 s | 487,9 s | 760,2 s | 975,4 s |

## Python-Notebooks {#python-notebook}

Mit [!DNL Python]-Notebooks können Sie beim Zugriff auf Datensätze Daten paginieren. Beispielcode zum Lesen von Daten mit und ohne Paginierung wird unten gezeigt. Weitere Informationen zu den verfügbaren Python-Starter-Notebooks finden Sie [[!DNL JupyterLab]  Abschnitt „Starter](./overview.md#launcher) im JupyterLab-Benutzerhandbuch.

In der folgenden Python-Dokumentation werden die folgenden Konzepte erläutert:

- [Aus einem Datensatz lesen](#python-read-dataset)
- [Schreiben in einen Datensatz](#write-python)
- [Abfragedaten](#query-data-python)
- [Filtern von ExperienceEvent-Daten](#python-filter)

### Lesen aus einem Datensatz in Python {#python-read-dataset}

**Ohne Paginierung:**

Wenn Sie den folgenden Code ausführen, wird der gesamte Datensatz gelesen. Bei erfolgreicher Ausführung werden die Daten als Pandas-Dataframe gespeichert, auf den die Variable `df` verweist.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

**mit Seitenumbruch:**

Wenn Sie folgenden Code ausführen, werden Daten aus dem angegebenen Datensatz gelesen. Paginierung wird erreicht, indem Daten über die Funktion `limit()` bzw. `offset()` begrenzt und versetzt werden. Datenbegrenzung bezieht sich auf die maximale Anzahl der zu lesenden Datenpunkte, während Versatz auf die Anzahl der Datenpunkte verweist, die vor dem Lesen von Daten übersprungen werden. Wenn der Lesevorgang erfolgreich ausgeführt wird, werden die Daten als Pandas-Dataframe gespeichert, auf den die Variable `df` verweist.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

### Schreiben in einen Datensatz in Python {#write-python}

Um in einen Datensatz in Ihrem JupyterLab-Notebook zu schreiben, wählen Sie die Registerkarte Datensymbol (unten hervorgehoben) im linken Navigationsbereich von JupyterLab aus. Die Verzeichnisse **[!UICONTROL Datensätze]** und **[!UICONTROL Schemata]** werden angezeigt. Wählen Sie **[!UICONTROL Datensätze]** klicken Sie mit der rechten Maustaste und wählen Sie dann im Dropdown-Menü des Datensatzes, den Sie verwenden möchten, die Option **[!UICONTROL Daten in Notebook schreiben]** aus. Unten im Notebook wird ein ausführbarer Code-Eintrag angezeigt.

![](../images/jupyterlab/data-access/write-dataset.png)

- Verwenden Sie **[!UICONTROL Daten in Notebook schreiben]**, um eine Schreibzelle mit Ihrem ausgewählten Datensatz zu generieren.
- Verwenden Sie **[!UICONTROL Erkunden von Daten in Notebook]**, um eine Lesezelle mit Ihrem ausgewählten Datensatz zu generieren.
- Verwenden Sie **[!UICONTROL Abfragedaten in Notebook]**, um eine einfache Abfragezelle mit Ihrem ausgewählten Datensatz zu generieren.

Alternativ können Sie die folgende Code-Zelle kopieren und einfügen. Ersetzen Sie sowohl die `{DATASET_ID}` als auch die `{PANDA_DATAFRAME}`.

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(get_platform_sdk_client_context()).get_by_id(dataset_id="{DATASET_ID}")
dataset_writer = DatasetWriter(get_platform_sdk_client_context(), dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### Abfragen von Daten mit [!DNL Query Service] in [!DNL Python] {#query-data-python}

[!DNL JupyterLab] on [!DNL Experience Platform] ermöglicht Ihnen die Verwendung von SQL in einem [!DNL Python] Notebook für den Datenzugriff über den [Adobe Experience Platform Query Service](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=de). Der Zugriff auf Daten über den [!DNL Query Service] kann aufgrund der kürzeren Ausführungszeiten bei der Bearbeitung großer Datensätze nützlich sein. Beachten Sie, dass Datenabfragen mit dem [!DNL Query Service] ein Limit bei der Verarbeitungszeit von 10 Minuten aufweisen.

Bevor Sie den [!DNL Query Service] in [!DNL JupyterLab] verwenden, sollten Sie Grundlagenkenntnisse zur [[!DNL Query Service] -SQL-Syntax](https://experienceleague.adobe.com/docs/experience-platform/query/sql/syntax.html?lang=de) besitzen.

Für die Abfrage von Daten mit [!DNL Query Service] müssen Sie den Namen des Zieldatensatzes angeben. Sie können die erforderlichen Code-Zellen generieren, indem Sie den gewünschten Datensatz mit dem **[!UICONTROL Data Explorer]** suchen. Klicken Sie mit der rechten Maustaste auf die Datensatzliste und klicken Sie auf **[!UICONTROL Daten in Notebook abfragen]**, um zwei Code-Zellen in Ihrem Notebook zu generieren. Diese beiden Zellen werden im Folgenden genauer beschrieben.

![](../images/jupyterlab/data-access/python-query-dataset.png)

Um [!DNL Query Service] in [!DNL JupyterLab] nutzen zu können, müssen Sie zunächst eine Verbindung zwischen Ihrem [!DNL Python] Notebook und [!DNL Query Service] herstellen. Dies kann durch Ausführen der ersten generierten Zelle erreicht werden.

```python
qs_connect()
```

In der zweiten generierten Zelle muss die erste Zeile vor der SQL-Abfrage definiert werden. Standardmäßig definiert die generierte Zelle eine optionale Variable (`df0`), mit der die Abfrageergebnisse als Pandas-Dataframe gespeichert werden. <br>Das `-c QS_CONNECTION` Argument ist obligatorisch und weist den Kernel an, die SQL-Abfrage für [!DNL Query Service] auszuführen. Eine Liste weiterer Argumente finden Sie im [Anhang](#optional-sql-flags-for-query-service).

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

Python-Variablen können in einer SQL-Abfrage direkt referenziert werden, indem Sie eine im Zeichenfolgenformat formatierte Syntax verwenden und die Variablen in geschweifte Klammern (`{}`) setzen (siehe folgendes Beispiel):

```python
table_name = 'name_of_the_dataset'
table_columns = ','.join(['col_1','col_2','col_3'])
```

```python
%%read_sql demo -c QS_CONNECTION
SELECT {table_columns}
FROM {table_name}
```

### Filtern [!DNL ExperienceEvent] Daten {#python-filter}

Um auf einen [!DNL ExperienceEvent] Datensatz in einem [!DNL Python]-Notebook zuzugreifen und ihn zu filtern, müssen Sie die ID des Datensatzes (`{DATASET_ID}`) zusammen mit den Filterregeln angeben, die einen bestimmten Zeitraum mithilfe von logischen Operatoren definieren. Wenn ein Zeitraum definiert ist, wird jede angegebene Paginierung ignoriert und der gesamte Datensatz berücksichtigt.

Eine Liste der Filteroperatoren finden Sie nachfolgend:

- `eq()`: Gleich
- `gt()`: Größer als
- `ge()`: Größer oder gleich
- `lt()`: Niedriger als
- `le()`: Kleiner oder gleich
- `And()`: Logischer UND-Operator
- `Or()`: Logischer ODER-Operator

Die folgende Zelle filtert einen [!DNL ExperienceEvent] Datensatz nach Daten, die ausschließlich zwischen dem 1. Januar 2019 und dem 31. Dezember 2019 existieren.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.\
    where(dataset_reader["timestamp"].gt("2019-01-01 00:00:00").\
    And(dataset_reader["timestamp"].lt("2019-12-31 23:59:59"))\
).read()
```

## R-Notebooks {#r-notebooks}

Mit R-Notebooks können Sie beim Zugriff auf Datensätze Daten paginieren. Beispielcode zum Lesen von Daten mit und ohne Paginierung wird unten gezeigt. Weitere Informationen zu den verfügbaren Starter-R-Notebooks finden Sie [[!DNL JupyterLab]  Abschnitt „Starter](./overview.md#launcher) im JupyterLab-Benutzerhandbuch.

In der folgenden R-Dokumentation werden die folgenden Konzepte erläutert:

- [Aus einem Datensatz lesen](#r-read-dataset)
- [Schreiben in einen Datensatz](#write-r)
- [Filtern von ExperienceEvent-Daten](#r-filter)

### Lesen aus einem Datensatz in R {#r-read-dataset}

**Ohne Paginierung:**

Wenn Sie den folgenden Code ausführen, wird der gesamte Datensatz gelesen. Bei erfolgreicher Ausführung werden die Daten als Pandas-Dataframe gespeichert, auf den die Variable `df0` verweist.

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
datetime <- import("datetime", convert = FALSE)
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df0 <- dataset_reader$read()
head(df0)
```

**mit Seitenumbruch:**

Wenn Sie folgenden Code ausführen, werden Daten aus dem angegebenen Datensatz gelesen. Paginierung wird erreicht, indem Daten über die Funktion `limit()` bzw. `offset()` begrenzt und versetzt werden. Datenbegrenzung bezieht sich auf die maximale Anzahl der zu lesenden Datenpunkte, während Versatz auf die Anzahl der Datenpunkte verweist, die vor dem Lesen von Daten übersprungen werden. Wenn der Lesevorgang erfolgreich ausgeführt wird, werden die Daten als Pandas-Dataframe gespeichert, auf den die Variable `df0` verweist.

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
datetime <- import("datetime", convert = FALSE)
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}") 
df0 <- dataset_reader$limit(100L)$offset(10L)$read()
```

### Schreiben in einen Datensatz in R {#write-r}

Um in einen Datensatz in Ihrem JupyterLab-Notebook zu schreiben, wählen Sie die Registerkarte Datensymbol (unten hervorgehoben) im linken Navigationsbereich von JupyterLab aus. Die Verzeichnisse **[!UICONTROL Datensätze]** und **[!UICONTROL Schemata]** werden angezeigt. Wählen Sie **[!UICONTROL Datensätze]** klicken Sie mit der rechten Maustaste und wählen Sie dann im Dropdown-Menü des Datensatzes, den Sie verwenden möchten, die Option **[!UICONTROL Daten in Notebook schreiben]** aus. Unten im Notebook wird ein ausführbarer Code-Eintrag angezeigt.

![](../images/jupyterlab/data-access/r-write-dataset.png)

- Verwenden Sie **[!UICONTROL Daten in Notebook schreiben]**, um eine Schreibzelle mit Ihrem ausgewählten Datensatz zu generieren.
- Verwenden Sie **[!UICONTROL Erkunden von Daten in Notebook]**, um eine Lesezelle mit Ihrem ausgewählten Datensatz zu generieren.

Alternativ können Sie die folgende Code-Zelle kopieren und einfügen:

```R
psdk <- import("platform_sdk")
dataset <- psdk$models$Dataset(py$get_platform_sdk_client_context())$get_by_id(dataset_id="{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(py$get_platform_sdk_client_context(), dataset)
write_tracker <- dataset_writer$write(df, file_format='json')
```

### Filtern [!DNL ExperienceEvent] Daten {#r-filter}

Um auf einen [!DNL ExperienceEvent] Datensatz in einem R-Notebook zuzugreifen und ihn zu filtern, müssen Sie die ID des Datensatzes (`{DATASET_ID}`) zusammen mit den Filterregeln angeben, die einen bestimmten Zeitraum mithilfe von logischen Operatoren definieren. Wenn ein Zeitraum definiert ist, wird jede angegebene Paginierung ignoriert und der gesamte Datensatz berücksichtigt.

Eine Liste der Filteroperatoren finden Sie nachfolgend:

- `eq()`: Gleich
- `gt()`: Größer als
- `ge()`: Größer oder gleich
- `lt()`: Niedriger als
- `le()`: Kleiner oder gleich
- `And()`: Logischer UND-Operator
- `Or()`: Logischer ODER-Operator

Die folgende Zelle filtert einen [!DNL ExperienceEvent] Datensatz nach Daten, die ausschließlich zwischen dem 1. Januar 2019 und dem 31. Dezember 2019 existieren.

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
datetime <- import("datetime", convert = FALSE)
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")

client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}") 

df0 <- dataset_reader$
    where(dataset_reader["timestamp"]$gt("2019-01-01 00:00:00")$
    And(dataset_reader["timestamp"]$lt("2019-12-31 23:59:59"))
)$read()
```

## PySpark 3-Notebooks {#pyspark-notebook}

In der folgenden PySpark-Dokumentation werden die folgenden Konzepte erläutert:

- [SparkSession initialisieren](#spark-initialize)
- [Lesen und Schreiben von Daten](#magic)
- [Erstellen eines lokalen Datenrahmens](#pyspark-create-dataframe)
- [Filtern von ExperienceEvent-Daten](#pyspark-filter-experienceevent)

### SparkSession wird initialisiert {#spark-initialize}

Bei allen [!DNL Spark] 2.4-Notebooks müssen Sie die Sitzung mit dem folgenden Textbausteincode initialisieren.

```scala
from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()
```

### Mit %dataset lesen und schreiben mit einem PySpark 3-Notebook {#magic}

Mit der Einführung von [!DNL Spark] 2.4 wird `%dataset` benutzerdefinierte Magie für die Verwendung in PySpark 3 ([!DNL Spark] 2.4)-Notebooks bereitgestellt. Weitere Informationen zu den im IPython-Kernel verfügbaren magischen Befehlen finden Sie in der [IPython magic-Dokumentation](https://ipython.readthedocs.io/en/stable/interactive/magics.html).


**Verwendung**

```scala
%dataset {action} --datasetId {id} --dataFrame {df} --mode batch
```

**Beschreibung**

Ein benutzerdefinierter [!DNL Data Science Workspace] Magic-Befehl zum Lesen oder Schreiben eines Datensatzes aus einem [!DNL PySpark] Notebook ([!DNL Python] 3 Kernel).

| Name | Beschreibung | Erforderlich |
| --- | --- | --- |
| `{action}` | Der Typ der Aktion, die mit dem Datensatz durchgeführt werden soll. Zwei Aktionen sind verfügbar: „Lesen“ oder „Schreiben“. | Ja |
| `--datasetId {id}` | Wird verwendet, um die ID des Datensatzes zum Lesen oder Schreiben anzugeben. | Ja |
| `--dataFrame {df}` | Der Pandas-Datenrahmen. <ul><li> Wenn die Aktion „Lesen“ ist, ist {df} die Variable, in der die Ergebnisse des Datensatzlesevorgangs verfügbar sind (z. B. ein Datenrahmen). </li><li> Wenn die Aktion „write“ ist, wird dieser {df} in den Datensatz geschrieben. </li></ul> | Ja |
| `--mode` | Ein zusätzlicher Parameter, der das Lesen von Daten ändert. Zulässige Parameter sind „batch“ und „interactive“. Standardmäßig ist der Modus auf „batch“ (Batch) festgelegt.<br> Es wird empfohlen, den Modus „Interaktiv“ zu verwenden, um die Abfrageleistung bei kleineren Datensätzen zu verbessern. | Ja |

>[!TIP]
>
>Überprüfen Sie die PySpark-Tabellen im Abschnitt [Notebook-Datenbeschränkungen](#notebook-data-limits), um festzustellen, ob `mode` auf `interactive` oder `batch` eingestellt werden soll.

**Beispiele**

- **Beispiel lesen**: `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0 --mode batch`
- **Beispiel schreiben**: `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0 --mode batch`

>[!IMPORTANT]
>
> Durch das Zwischenspeichern von Daten mithilfe von `df.cache()` vor dem Schreiben von Daten kann die Notebook-Leistung erheblich verbessert werden. Dies kann hilfreich sein, wenn Sie einen der folgenden Fehler erhalten:
> 
> - Auftrag aufgrund von Staging-Fehler abgebrochen ... Kann nur RDDs mit derselben Anzahl von Elementen in jeder Partition komprimieren.
> - Remote RPC-Client getrennt und andere Speicherfehler.
> - Schlechte Performance beim Lesen und Schreiben von Datensätzen.
> 
> Weitere Informationen finden [ im ](../troubleshooting-guide.md) zur Fehlerbehebung .

Sie können die oben genannten Beispiele automatisch in JupyterLab generieren, indem Sie die folgende Methode verwenden:

Wählen Sie im linken Navigationsbereich von JupyterLab die Registerkarte mit dem Datensymbol (siehe unten) aus. Die Verzeichnisse **[!UICONTROL Datensätze]** und **[!UICONTROL Schemata]** werden angezeigt. Wählen Sie **[!UICONTROL Datensätze]** klicken Sie mit der rechten Maustaste und wählen Sie dann im Dropdown-Menü des Datensatzes, den Sie verwenden möchten, die Option **[!UICONTROL Daten in Notebook schreiben]** aus. Unten im Notebook wird ein ausführbarer Code-Eintrag angezeigt.

- Verwenden Sie **[!UICONTROL Erkunden von Daten in Notebook]**, um eine Lesezelle zu generieren.
- Verwenden Sie **[!UICONTROL Write Data in Notebook]**, um eine Schreibzelle zu generieren.

![](../images/jupyterlab/data-access/pyspark-write-dataset.png)

### Erstellen eines lokalen Datenrahmens {#pyspark-create-dataframe}

Verwenden Sie SQL-Abfragen, um einen lokalen Datenrahmen mit PySpark 3 zu erstellen. z. B.:

```scala
date_aggregation.createOrReplaceTempView("temp_df")

df = spark.sql('''
  SELECT *
  FROM sparkdf
''')

local_df
```

```scala
df = spark.sql('''
  SELECT *
  FROM sparkdf
  LIMIT limit
''')
```

```scala
sample_df = df.sample(fraction)
```

>[!TIP]
>
>Sie können auch eine optionale Testadresse angeben, z. B. einen booleschen Wert mit „Ersatz“, eine doppelte Fraktion oder einen langen Testwert.

### Filtern [!DNL ExperienceEvent] Daten {#pyspark-filter-experienceevent}

Um auf einen [!DNL ExperienceEvent] Datensatz in einem PySpark-Notebook zugreifen und ihn filtern zu können, müssen Sie die Datensatzidentität (`{DATASET_ID}`), die IMS-Identität Ihres Unternehmens und die Filterregeln angeben, die einen bestimmten Zeitraum definieren. Ein Filterzeitbereich wird mithilfe der `spark.sql()` definiert, wobei der Funktionsparameter eine SQL-Abfragezeichenfolge ist.

Die folgenden Zellen filtern einen [!DNL ExperienceEvent] Datensatz nach Daten, die ausschließlich zwischen dem 1. Januar 2019 und dem 31. Dezember 2019 existierten.

```python
# PySpark 3 (Spark 2.4)

from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()

%dataset read --datasetId {DATASET_ID} --dataFrame df --mode batch

df.createOrReplaceTempView("event")
timepd = spark.sql("""
    SELECT *
    FROM event
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timepd.show()
```

## Scala-Notebooks {#scala-notebook}

Die folgende Dokumentation enthält Beispiele für die folgenden Konzepte:

- [SparkSession initialisieren](#scala-initialize)
- [Datensatz lesen](#read-scala-dataset)
- [Schreiben in einen Datensatz](#scala-write-dataset)
- [Erstellen eines lokalen Datenrahmens](#scala-create-dataframe)
- [Filtern von ExperienceEvent-Daten](#scala-experienceevent)

### SparkSession wird initialisiert {#scala-initialize}

Bei allen Scala-Notebooks müssen Sie die Sitzung mit dem folgenden Textbausteincode initialisieren:

```scala
import org.apache.spark.sql.{ SparkSession }
val spark = SparkSession
  .builder()
  .master("local")
  .getOrCreate()
```

### Datensatz lesen {#read-scala-dataset}

In Scala können Sie `clientContext` importieren, um Experience Platform-Werte abzurufen und zurückzugeben, sodass Sie keine Variablen wie `var userToken` definieren müssen. Im folgenden Scala-Beispiel wird `clientContext` verwendet, um alle erforderlichen Werte zum Lesen eines Datensatzes abzurufen und zurückzugeben.

>[!IMPORTANT]
>
> Durch das Zwischenspeichern von Daten mithilfe von `df.cache()` vor dem Schreiben von Daten kann die Notebook-Leistung erheblich verbessert werden. Dies kann hilfreich sein, wenn Sie einen der folgenden Fehler erhalten:
> 
> - Auftrag aufgrund von Staging-Fehler abgebrochen ... Kann nur RDDs mit derselben Anzahl von Elementen in jeder Partition komprimieren.
> - Remote RPC-Client getrennt und andere Speicherfehler.
> - Schlechte Performance beim Lesen und Schreiben von Datensätzen.
> 
> Weitere Informationen finden [ im ](../troubleshooting-guide.md) zur Fehlerbehebung .

```scala
import org.apache.spark.sql.{Dataset, SparkSession}
import com.adobe.platform.token.ClientContext
val spark = SparkSession.builder().master("local").config("spark.sql.warehouse.dir", "/").getOrCreate()

val clientContext = ClientContext.getClientContext()
val df1 = spark.read.format("com.adobe.platform.query")
  .option("user-token", clientContext.getUserToken())
  .option("ims-org", clientContext.getOrgId())
  .option("api-key", clientContext.getApiKey())
  .option("service-token", clientContext.getServiceToken())
  .option("sandbox-name", clientContext.getSandboxName())
  .option("mode", "batch")
  .option("dataset-id", "5e68141134492718af974844")
  .load()

df1.printSchema()
df1.show(10)
```

| Element | Beschreibung |
| ------- | ----------- |
| DF1 | Eine Variable, die den Pandas-Datenrahmen darstellt, der zum Lesen und Schreiben von Daten verwendet wird. |
| user-token | Ihr Benutzer-Token, das automatisch mit `clientContext.getUserToken()` abgerufen wird. |
| service-token | Ihr Service-Token, das automatisch mit `clientContext.getServiceToken()` abgerufen wird. |
| ims-org | Ihre Organisations-ID, die automatisch mit `clientContext.getOrgId()` abgerufen wird. |
| api-key | Ihr API-Schlüssel, der automatisch mit `clientContext.getApiKey()` abgerufen wird. |

>[!TIP]
>
>Überprüfen Sie die Scala-Tabellen im Abschnitt [Notebook-Datenbeschränkungen](#notebook-data-limits), um festzustellen, ob `mode` auf `interactive` oder `batch` eingestellt werden soll.

Sie können das obige Beispiel automatisch in JupyterLab generieren, indem Sie die folgende Methode verwenden:

Wählen Sie im linken Navigationsbereich von JupyterLab die Registerkarte mit dem Datensymbol (siehe unten) aus. Die Verzeichnisse **[!UICONTROL Datensätze]** und **[!UICONTROL Schemata]** werden angezeigt. Wählen Sie **[!UICONTROL Datensätze]** aus, klicken Sie mit der rechten Maustaste und wählen Sie dann im Dropdown-Menü des Datensatzes, den Sie verwenden möchten, die Option **[!UICONTROL Daten in Notebook erkunden]** aus. Unten im Notebook wird ein ausführbarer Code-Eintrag angezeigt.
Und
- Verwenden Sie **[!UICONTROL Erkunden von Daten in Notebook]**, um eine Lesezelle zu generieren.
- Verwenden Sie **[!UICONTROL Write Data in Notebook]**, um eine Schreibzelle zu generieren.

![](../images/jupyterlab/data-access/scala-write-dataset.png)

### Schreiben in einen Datensatz {#scala-write-dataset}

In Scala können Sie `clientContext` importieren, um Experience Platform-Werte abzurufen und zurückzugeben, sodass Sie keine Variablen wie `var userToken` definieren müssen. Im folgenden Scala-Beispiel wird `clientContext` verwendet, um alle erforderlichen Werte zum Schreiben in einen Datensatz zu definieren und zurückzugeben.

>[!IMPORTANT]
>
> Durch das Zwischenspeichern von Daten mithilfe von `df.cache()` vor dem Schreiben von Daten kann die Notebook-Leistung erheblich verbessert werden. Dies kann hilfreich sein, wenn Sie einen der folgenden Fehler erhalten:
> 
> - Auftrag aufgrund von Staging-Fehler abgebrochen ... Kann nur RDDs mit derselben Anzahl von Elementen in jeder Partition komprimieren.
> - Remote RPC-Client getrennt und andere Speicherfehler.
> - Schlechte Performance beim Lesen und Schreiben von Datensätzen.
> 
> Weitere Informationen finden [ im ](../troubleshooting-guide.md) zur Fehlerbehebung .

```scala
import org.apache.spark.sql.{Dataset, SparkSession}
import com.adobe.platform.token.ClientContext
val spark = SparkSession.builder().master("local").config("spark.sql.warehouse.dir", "/").getOrCreate()

val clientContext = ClientContext.getClientContext()
df1.write.format("com.adobe.platform.query")
  .option("user-token", clientContext.getUserToken())
  .option("service-token", clientContext.getServiceToken())
  .option("ims-org", clientContext.getOrgId())
  .option("api-key", clientContext.getApiKey())
  .option("sandbox-name", clientContext.getSandboxName())
  .option("mode", "batch")
  .option("dataset-id", "5e68141134492718af974844")
  .save()
```

| Element | Beschreibung |
| ------- | ----------- |
| DF1 | Eine Variable, die den Pandas-Datenrahmen darstellt, der zum Lesen und Schreiben von Daten verwendet wird. |
| user-token | Ihr Benutzer-Token, das automatisch mit `clientContext.getUserToken()` abgerufen wird. |
| service-token | Ihr Service-Token, das automatisch mit `clientContext.getServiceToken()` abgerufen wird. |
| ims-org | Ihre Organisations-ID, die automatisch mit `clientContext.getOrgId()` abgerufen wird. |
| api-key | Ihr API-Schlüssel, der automatisch mit `clientContext.getApiKey()` abgerufen wird. |

>[!TIP]
>
>Überprüfen Sie die Scala-Tabellen im Abschnitt [Notebook-Datenbeschränkungen](#notebook-data-limits), um festzustellen, ob `mode` auf `interactive` oder `batch` eingestellt werden soll.

### Erstellen eines lokalen Datenrahmens {#scala-create-dataframe}

Um einen lokalen Datenrahmen mit Scala zu erstellen, sind SQL-Abfragen erforderlich. z. B.:

```scala
sparkdf.createOrReplaceTempView("sparkdf")

val localdf = spark.sql("SELECT * FROM sparkdf LIMIT 1)
```

### Filtern [!DNL ExperienceEvent] Daten {#scala-experienceevent}

Für den Zugriff auf und die Filterung eines [!DNL ExperienceEvent] Datensatzes in einem Scala-Notebook müssen Sie die Datensatzidentität (`{DATASET_ID}`), die IMS-Identität Ihres Unternehmens und die Filterregeln angeben, die einen bestimmten Zeitraum definieren. Ein Filterzeitbereich wird mithilfe der Funktion `spark.sql()` definiert, wobei der Funktionsparameter eine SQL-Abfragezeichenfolge ist.

Die folgenden Zellen filtern einen [!DNL ExperienceEvent] Datensatz nach Daten, die ausschließlich zwischen dem 1. Januar 2019 und dem 31. Dezember 2019 existierten.

```scala
// Spark (Spark 2.4)

// Turn off extra logging
import org.apache.log4j.{Level, Logger}
Logger.getLogger("org").setLevel(Level.OFF)
Logger.getLogger("com").setLevel(Level.OFF)

import org.apache.spark.sql.{Dataset, SparkSession}
val spark = org.apache.spark.sql.SparkSession.builder().appName("Notebook")
  .master("local")
  .getOrCreate()

// Stage Exploratory
val dataSetId: String = "{DATASET_ID}"
val orgId: String = sys.env("IMS_ORG_ID")
val clientId: String = sys.env("PYDASDK_IMS_CLIENT_ID")
val userToken: String = sys.env("PYDASDK_IMS_USER_TOKEN")
val serviceToken: String = sys.env("PYDASDK_IMS_SERVICE_TOKEN")
val mode: String = "batch"

var df = spark.read.format("com.adobe.platform.query")
  .option("user-token", userToken)
  .option("ims-org", orgId)
  .option("api-key", clientId)
  .option("mode", mode)
  .option("dataset-id", dataSetId)
  .option("service-token", serviceToken)
  .load()
df.createOrReplaceTempView("event")
val timedf = spark.sql("""
    SELECT * 
    FROM event 
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timedf.show()
```

## Nächste Schritte

In diesem Dokument wurden die allgemeinen Richtlinien für den Zugriff auf Datensätze mithilfe von JupyterLab-Notebooks behandelt. Ausführlichere Beispiele zum Abfragen von Datensätzen finden Sie in der Dokumentation [Abfrage-Service in JupyterLab](./query-service.md)-Notebooks. Weitere Informationen dazu, wie Sie Ihre Datensätze untersuchen und visualisieren können, finden Sie im Dokument [Analysieren Ihrer Daten mithilfe von Notebooks](./analyze-your-data.md).

## Optionale SQL-Flags für [!DNL Query Service] {#optional-sql-flags-for-query-service}

In dieser Tabelle sind die optionalen SQL-Flags aufgeführt, die für die [!DNL Query Service] verwendet werden können.

| **Markierung** | **Beschreibung** |
| --- | --- |
| `-h`, `--help` | Hilfemeldung anzeigen und beenden. |
| `-n`, `--notify` | Umschaltoption für das Benachrichtigen bei Abfrageergebnissen. |
| `-a`, `--async` | Bei Verwendung dieser Markierung wird die Abfrage asynchron ausgeführt und kann der Kernel freigeben werden, während die Abfrage ausgeführt wird. Seien Sie vorsichtig, wenn Sie Abfrageergebnisse Variablen zuweisen, da sie möglicherweise undefiniert sind, wenn die Abfrage noch nicht abgeschlossen ist. |
| `-d`, `--display` | Die Verwendung dieser Markierung verhindert, dass Ergebnisse angezeigt werden. |
