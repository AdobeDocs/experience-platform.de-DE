---
keywords: Experience Platform; JupyterLab; Notebooks; Data Science Workspace; beliebte Themen;%Datensatz; interaktiver Modus; Batch-Modus; Spark-SDK; Python-SDK; Datenzugriff; Notebook-Datenzugriff
solution: Experience Platform
title: Datenzugriff in Jupyterlab-Notebooks
description: Dieser Leitfaden konzentriert sich auf die Verwendung von Jupyter Notebooks, die in Data Science Workspace für den Zugriff auf Ihre Daten entwickelt wurden.
exl-id: 2035a627-5afc-4b72-9119-158b95a35d32
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '3320'
ht-degree: 23%

---

# Datenzugriff in [!DNL Jupyterlab] Notebooks

Jeder unterstützte Kernel bietet native Funktionen, mit denen Sie Platform-Daten aus einem Datensatz in einem Notebook lesen können. Derzeit unterstützt JupyterLab in Adobe Experience Platform Data Science Workspace Notebooks für [!DNL Python], R, PySpark und Scala. Die Unterstützung für die Paginierung von Daten ist jedoch auf [!DNL Python]- und R-Notebooks beschränkt. In diesem Handbuch wird beschrieben, wie Sie mit JupyterLab-Notebooks auf Ihre Daten zugreifen können.

## Erste Schritte

Bevor Sie dieses Handbuch lesen, lesen Sie bitte das [[!DNL JupyterLab] Benutzerhandbuch](./overview.md) , um eine allgemeine Einführung in [!DNL JupyterLab] und dessen Rolle in Data Science Workspace zu erhalten.

## Einschränkungen für Notebook-Daten {#notebook-data-limits}

>[!IMPORTANT]
>
>Bei PySpark- und Scala-Notebooks, wenn Sie einen Fehler mit dem Grund &quot;Remote RPC Client getrennt&quot;erhalten. Dies bedeutet normalerweise, dass dem Treiber oder einem Executor der Speicher ausgeht. Versuchen Sie, zum Modus [&quot;batch&quot;](#mode) zu wechseln, um diesen Fehler zu beheben.

Die folgenden Informationen definieren die maximale Datenmenge, die gelesen werden kann, welche Art von Daten verwendet wurde und den geschätzten Zeitrahmen, in dem die Daten gelesen werden.

Für [!DNL Python] und R wurde ein mit 40 GB RAM konfigurierter Notebook-Server für die Benchmarks verwendet. Für PySpark und Scala wurde ein mit 64 GB RAM, 8 Kernen und 2 DBU konfigurierter Datenbank-Cluster mit maximal 4 Workern für die unten beschriebenen Benchmarks verwendet.

Die verwendeten ExperienceEvent-Schemadaten variierten in ihrer Größe von 1.000 Zeilen (1.000) bis zu einer Milliarde (1.000) Zeilen. Beachten Sie, dass für die Metriken PySpark und [!DNL Spark] ein Datumsbereich von 10 Tagen für die XDM-Daten verwendet wurde.

Die Ad-hoc-Schemadaten wurden mit [!DNL Query Service] Tabelle als Auswahl erstellen (CTAS) vorverarbeitet. Diese Daten variierten auch von 100 (1.000) Zeilen bis zu einer Milliarde (1.000) Zeilen.

### Verwendung des Batch-Modus im Vergleich zum interaktiven Modus {#mode}

Beim Lesen von Datensätzen mit PySpark- und Scala-Notebooks haben Sie die Möglichkeit, den interaktiven Modus oder Batch-Modus zu verwenden, um den Datensatz zu lesen. Interaktiv erfolgt für schnelle Ergebnisse, während der Batch-Modus für große Datensätze verwendet wird.

- Bei PySpark- und Scala-Notebooks sollte der Batch-Modus verwendet werden, wenn mindestens 5 Millionen Datenzeilen gelesen werden. Weitere Informationen zur Effizienz der einzelnen Modi finden Sie in den unten stehenden Tabellen mit den Datenbeschränkungen für [PySpark](#pyspark-data-limits) oder [Scala](#scala-data-limits) .

### [!DNL Python] Notebook-Datenbeschränkungen

**XDM ExperienceEvent-Schema:** Sie sollten maximal 2 Millionen Zeilen (~6,1 GB Daten auf der Festplatte) von XDM-Daten in weniger als 22 Minuten lesen können. Das Hinzufügen zusätzlicher Zeilen kann zu Fehlern führen.

| Anzahl Zeilen | 1 K | 10 K | 100.000 | 1 M | 2 M |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| Größe auf Festplatte (MB) | 18,73 | 187,5 | 308 | 3000 | 6050 |
| SDK (in Sekunden) | 20,3 | 86,8 | 63 | 659 | 1315 |

**Ad-hoc-Schema:** Sie sollten maximal 5 Millionen Zeilen (~5,6 GB Daten auf der Festplatte) von Nicht-XDM-Daten (Ad-hoc-Daten) in weniger als 14 Minuten lesen können. Das Hinzufügen zusätzlicher Zeilen kann zu Fehlern führen.

| Zeilenanzahl | 1 K | 10 K | 100.000 | 1 M | 2 M | 3 M | 5 M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| Größe auf Festplatte (in MB) | 1,21 | 11,72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK (in Sekunden) | 7,27 | 9,04 | 27,3 | 180 | 346 | 487 | 819 |

### R Notebook-Datenbeschränkungen

**XDM ExperienceEvent-Schema:** Sie sollten maximal 1 Million Zeilen mit XDM-Daten (3 GB Daten auf der Festplatte) in weniger als 13 Minuten lesen können.

| Zeilenanzahl | 1 K | 10 K | 100.000 | 1 M |
| ----------------------- | ------ | ------ | ----- | ----- |
| Größe auf Festplatte (MB) | 18,73 | 187,5 | 308 | 3000 |
| R-Kernel (in Sekunden) | 14,03 | 69,6 | 86,8 | 775 |

**Ad-hoc-Schema:** Sie sollten maximal 3 Millionen Zeilen Ad-hoc-Daten (293 MB Daten auf der Festplatte) in etwa 10 Minuten lesen können.

| Zeilenanzahl | 1 K | 10 K | 100.000 | 1 M | 2 M | 3 M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| Größe auf Festplatte (in MB) | 0,082 | 0,612 | 9.0 | 91 | 188 | 293 |
| R SDK (in Sekunden) | 7,7 | 4,58 | 35,9 | 233 | 470,5 | 603 |

### Datenbeschränkungen des PySpark-Notebooks ([!DNL Python] Kernel): {#pyspark-data-limits}

**XDM ExperienceEvent-Schema:** Im interaktiven Modus sollten Sie maximal 5 Millionen Zeilen (~13,42 GB Daten auf der Festplatte) von XDM-Daten in etwa 20 Minuten lesen können. Der interaktive Modus unterstützt nur bis zu 5 Millionen Zeilen. Wenn Sie größere Datensätze lesen möchten, wird empfohlen, in den Batch-Modus zu wechseln. Im Batch-Modus sollten Sie in der Lage sein, maximal 500 Millionen Zeilen (~1,31 TB-Daten auf der Festplatte) von XDM-Daten in etwa 14 Stunden zu lesen.

| Zeilenanzahl | 1 K | 10 K | 100.000 | 1 M | 2 M | 3 M | 5 M | 10 M | 50 M | 100 Min. | 500 Min. |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Größe auf der Festplatte | 2,93MB | 4,38MB | 29,02 | 2,69GB | 5,39GB | 8,09GB | 13,42GB | 26,82GB | 134,24GB | 268,39GB | 1,31 TB |
| SDK (interaktiver Modus) | 33 s | 32,4 s | 55.1 s | 253,5 s | 489.2 s | 729.6 s | 1206.8 s | – | – | – | – |
| SDK (Batch-Modus) | 815.8 s | 492.8 s | 379.1 s | 637,4 s | 624,5 s | 869.2 s | 1104.1 s | 1786 s | 5387.2 s | 10624,6 s | 50547 s |

**Ad-hoc-Schema:** Im interaktiven Modus sollten Sie maximal 5 Millionen Zeilen (~5,36 GB Daten auf der Festplatte) von Nicht-XDM-Daten in weniger als 3 Minuten lesen können. Im Batch-Modus sollten Sie in der Lage sein, maximal 1 Milliarde Zeilen (~1,05 TB Daten auf der Festplatte) von Nicht-XDM-Daten in etwa 18 Minuten zu lesen.

| Zeilenanzahl | 1 K | 10 K | 100.000 | 1 M | 2 M | 3 M | 5 M | 10 M | 50 M | 100 Min. | 500 Min. | 1B |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| Größe auf der Festplatte | 1,12MB | 11,24MB | 109,48MB | 2,69GB | 2,14GB | 3,21GB | 5,36GB | 10,71GB | 53,58GB | 107,52GB | 535,88GB | 1,05 TB |
| Interaktiver SDK-Modus (in Sekunden) | 28.2 s | 18,6 s | 20,8 s | 20.9 s | 23,8 s | 21,7 s | 24,7 s | – | – | – | – | – |
| SDK-Batch-Modus (in Sekunden) | 428.8 s | 578.8 s | 641.4 s | 538.5 s | 630.9 s | 467,3 s | 411 s | 675 s | 702 s | 719.2 s | 1022.1 s | 1122,3 s |

### [!DNL Spark] (Scala-Kernel) Notebook-Datenbeschränkungen: {#scala-data-limits}

**XDM ExperienceEvent-Schema:** Im interaktiven Modus sollten Sie maximal 5 Millionen Zeilen (~13,42 GB Daten auf der Festplatte) von XDM-Daten in etwa 18 Minuten lesen können. Der interaktive Modus unterstützt nur bis zu 5 Millionen Zeilen. Wenn Sie größere Datensätze lesen möchten, wird empfohlen, in den Batch-Modus zu wechseln. Im Batch-Modus sollten Sie in der Lage sein, maximal 500 Millionen Zeilen (~1,31 TB-Daten auf der Festplatte) von XDM-Daten in etwa 14 Stunden zu lesen.

| Zeilenanzahl | 1 K | 10 K | 100.000 | 1 M | 2 M | 3 M | 5 M | 10 M | 50 M | 100 Min. | 500 Min. |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Größe auf der Festplatte | 2,93MB | 4,38MB | 29,02 | 2,69GB | 5,39GB | 8,09GB | 13,42GB | 26,82GB | 134,24GB | 268,39GB | 1,31 TB |
| Interaktiver SDK-Modus (in Sekunden) | 37,9 s | 22,7 s | 45,6 s | 231.7 s | 444,7 s | 660.6 s | 1100 s | – | – | – | – |
| SDK-Batch-Modus (in Sekunden) | 374.4 s | 398.5 s | 527 s | 487.9 s | 588.9 s | 829 s | 939.1 s | 1441 s | 5473.2 s | 10118,8 | 49207,6 |

**Ad-hoc-Schema:** Im interaktiven Modus sollten Sie maximal 5 Millionen Zeilen (~5,36 GB Daten auf der Festplatte) von Nicht-XDM-Daten in weniger als 3 Minuten lesen können. Im Batch-Modus sollten Sie in der Lage sein, maximal 1 Milliarde Zeilen (~1,05 TB Daten auf der Festplatte) von Nicht-XDM-Daten in etwa 16 Minuten zu lesen.

| Zeilenanzahl | 1 K | 10 K | 100.000 | 1 M | 2 M | 3 M | 5 M | 10 M | 50 M | 100 Min. | 500 Min. | 1B |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| Größe auf der Festplatte | 1,12MB | 11,24MB | 109,48MB | 2,69GB | 2,14GB | 3,21GB | 5,36GB | 10,71GB | 53,58GB | 107,52GB | 535,88GB | 1,05 TB |
| Interaktiver SDK-Modus (in Sekunden) | 35,7 s | 31 s | 19,5 s | 25,3 s | 23 s | 33,2 s | 25,5 s | – | – | – | – | – |
| SDK-Batch-Modus (in Sekunden) | 448.8 s | 459.7 s | 519 s | 475.8 s | 599.9 s | 347.6 s | 407.8 s | 397 s | 518.8 s | 487.9 s | 760.2 s | 975.4 s |

## Python Notebooks {#python-notebook}

Mit [!DNL Python] Notebooks können Sie Daten beim Zugriff auf Datensätze paginieren. Beispielcode zum Lesen von Daten mit und ohne Paginierung finden Sie unten. Weitere Informationen zu den verfügbaren Start-Python-Notebooks finden Sie im Abschnitt [[!DNL JupyterLab] Launcher](./overview.md#launcher) im JupyterLab-Benutzerhandbuch.

In der folgenden Python-Dokumentation werden die folgenden Konzepte beschrieben:

- [Aus einem Datensatz lesen](#python-read-dataset)
- [Schreiben in einen Datensatz](#write-python)
- [Abfragedaten](#query-data-python)
- [ExperienceEvent-Daten filtern](#python-filter)

### Aus einem Datensatz in Python lesen {#python-read-dataset}

**Ohne Paginierung:**

Wenn Sie den folgenden Code ausführen, wird der gesamte Datensatz gelesen. Bei erfolgreicher Ausführung werden die Daten als Pandas-Dataframe gespeichert, auf den die Variable `df` verweist.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

**Mit Paginierung:**

Wenn Sie folgenden Code ausführen, werden Daten aus dem angegebenen Datensatz gelesen. Paginierung wird erreicht, indem Daten über die Funktion `limit()` bzw. `offset()` begrenzt und versetzt werden. Datenbegrenzung bezieht sich auf die maximale Anzahl der zu lesenden Datenpunkte, während Versatz auf die Anzahl der Datenpunkte verweist, die vor dem Lesen von Daten übersprungen werden. Wenn der Lesevorgang erfolgreich ausgeführt wird, werden die Daten als Pandas-Dataframe gespeichert, auf den die Variable `df` verweist.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

### Schreiben in einen Datensatz in Python {#write-python}

Um in einen Datensatz in Ihrem JupyterLab-Notebook zu schreiben, wählen Sie im linken Navigationsbereich von JupyterLab die Registerkarte Datensymbol (unten hervorgehoben). Die Verzeichnisse **[!UICONTROL Datensätze]** und **[!UICONTROL Schemata]** werden angezeigt. Wählen Sie **[!UICONTROL Datensätze]** und klicken Sie mit der rechten Maustaste und wählen Sie dann die Option **[!UICONTROL Daten in Notebook schreiben]** aus dem Dropdown-Menü des Datensatzes aus, den Sie verwenden möchten. Unten im Notebook wird ein ausführbarer Code-Eintrag angezeigt.

![](../images/jupyterlab/data-access/write-dataset.png)

- Verwenden Sie **[!UICONTROL Daten in Notebook schreiben]** , um eine Schreibzelle mit Ihrem ausgewählten Datensatz zu generieren.
- Verwenden Sie **[!UICONTROL Daten in Notebook durchsuchen]** , um eine Leselelle mit Ihrem ausgewählten Datensatz zu generieren.
- Verwenden Sie **[!UICONTROL Abfragedaten in Notebook]** , um eine einfache Abfragezelle mit Ihrem ausgewählten Datensatz zu generieren.

Alternativ können Sie die folgende Code-Zelle kopieren und einfügen. Ersetzen Sie sowohl die `{DATASET_ID}` als auch die `{PANDA_DATAFRAME}`.

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(get_platform_sdk_client_context()).get_by_id(dataset_id="{DATASET_ID}")
dataset_writer = DatasetWriter(get_platform_sdk_client_context(), dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### Abfragen von Daten mit [!DNL Query Service] in [!DNL Python] {#query-data-python}

Mit [!DNL JupyterLab] auf [!DNL Platform] können Sie SQL in einem [!DNL Python] Notebook verwenden, um über [Adobe Experience Platform Query Service](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=de) auf Daten zuzugreifen. Der Zugriff auf Daten über den [!DNL Query Service] kann aufgrund der kürzeren Ausführungszeiten bei der Bearbeitung großer Datensätze nützlich sein. Beachten Sie, dass Datenabfragen mit dem [!DNL Query Service] ein Limit bei der Verarbeitungszeit von 10 Minuten aufweisen.

Bevor Sie den [!DNL Query Service] in [!DNL JupyterLab] verwenden, sollten Sie Grundlagenkenntnisse zur [[!DNL Query Service] -SQL-Syntax](https://experienceleague.adobe.com/docs/experience-platform/query/sql/syntax.html?lang=de) besitzen.

Für die Abfrage von Daten mit [!DNL Query Service] müssen Sie den Namen des Zieldatensatzes angeben. Sie können die erforderlichen Code-Zellen generieren, indem Sie den gewünschten Datensatz mit dem **[!UICONTROL Data Explorer]** suchen. Klicken Sie mit der rechten Maustaste auf die Datensatzliste und klicken Sie auf **[!UICONTROL Daten in Notebook abfragen]** , um zwei Code-Zellen in Ihrem Notebook zu generieren. Diese beiden Zellen werden nachfolgend detaillierter beschrieben.

![](../images/jupyterlab/data-access/python-query-dataset.png)

Um [!DNL Query Service] in [!DNL JupyterLab] zu verwenden, müssen Sie zunächst eine Verbindung zwischen Ihrem funktionsfähigen [!DNL Python] Notebook und [!DNL Query Service] herstellen. Dies kann durch Ausführen der ersten generierten Zelle erreicht werden.

```python
qs_connect()
```

In der zweiten generierten Zelle muss die erste Zeile vor der SQL-Abfrage definiert werden. Standardmäßig definiert die generierte Zelle eine optionale Variable (`df0`), mit der die Abfrageergebnisse als Pandas-Dataframe gespeichert werden. <br>Das `-c QS_CONNECTION` -Argument ist obligatorisch und weist den Kernel an, die SQL-Abfrage für [!DNL Query Service] auszuführen. Eine Liste weiterer Argumente finden Sie im [Anhang](#optional-sql-flags-for-query-service).

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

### [!DNL ExperienceEvent] Daten filtern {#python-filter}

Um auf einen [!DNL ExperienceEvent] -Datensatz in einem [!DNL Python] -Notebook zuzugreifen und ihn zu filtern, müssen Sie die Kennung des Datensatzes (`{DATASET_ID}`) zusammen mit den Filterregeln angeben, die mithilfe logischer Operatoren einen bestimmten Zeitraum definieren. Wenn ein Zeitraum definiert ist, wird jede angegebene Paginierung ignoriert und der gesamte Datensatz berücksichtigt.

Eine Liste der Filteroperatoren finden Sie nachfolgend:

- `eq()`: Gleich
- `gt()`: Größer als
- `ge()`: Größer oder gleich
- `lt()`: Niedriger als
- `le()`: Kleiner oder gleich
- `And()`: Logischer UND-Operator
- `Or()`: Logischer ODER-Operator

Die folgende Zelle filtert einen [!DNL ExperienceEvent] -Datensatz für Daten, die ausschließlich zwischen dem 1. Januar 2019 und dem 31. Dezember 2019 existierten.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.\
    where(dataset_reader["timestamp"].gt("2019-01-01 00:00:00").\
    And(dataset_reader["timestamp"].lt("2019-12-31 23:59:59"))\
).read()
```

## R Notebooks {#r-notebooks}

Mit R-Notebooks können Sie Daten beim Zugriff auf Datensätze paginieren. Beispielcode zum Lesen von Daten mit und ohne Paginierung finden Sie unten. Weitere Informationen zu den verfügbaren Start-R-Notebooks finden Sie im Abschnitt [[!DNL JupyterLab] Launcher](./overview.md#launcher) im JupyterLab-Benutzerhandbuch.

In der folgenden R-Dokumentation werden die folgenden Konzepte beschrieben:

- [Aus einem Datensatz lesen](#r-read-dataset)
- [Schreiben in einen Datensatz](#write-r)
- [ExperienceEvent-Daten filtern](#r-filter)

### Aus einem Datensatz in R lesen {#r-read-dataset}

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

**Mit Paginierung:**

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

Um in einen Datensatz in Ihrem JupyterLab-Notebook zu schreiben, wählen Sie im linken Navigationsbereich von JupyterLab die Registerkarte Datensymbol (unten hervorgehoben). Die Verzeichnisse **[!UICONTROL Datensätze]** und **[!UICONTROL Schemata]** werden angezeigt. Wählen Sie **[!UICONTROL Datensätze]** und klicken Sie mit der rechten Maustaste und wählen Sie dann die Option **[!UICONTROL Daten in Notebook schreiben]** aus dem Dropdown-Menü des Datensatzes aus, den Sie verwenden möchten. Unten im Notebook wird ein ausführbarer Code-Eintrag angezeigt.

![](../images/jupyterlab/data-access/r-write-dataset.png)

- Verwenden Sie **[!UICONTROL Daten in Notebook schreiben]** , um eine Schreibzelle mit Ihrem ausgewählten Datensatz zu generieren.
- Verwenden Sie **[!UICONTROL Daten in Notebook durchsuchen]** , um eine Leselelle mit Ihrem ausgewählten Datensatz zu generieren.

Alternativ können Sie die folgende Code-Zelle kopieren und einfügen:

```R
psdk <- import("platform_sdk")
dataset <- psdk$models$Dataset(py$get_platform_sdk_client_context())$get_by_id(dataset_id="{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(py$get_platform_sdk_client_context(), dataset)
write_tracker <- dataset_writer$write(df, file_format='json')
```

### [!DNL ExperienceEvent] Daten filtern {#r-filter}

Um auf einen [!DNL ExperienceEvent] -Datensatz in einem R-Notebook zuzugreifen und ihn zu filtern, müssen Sie die Kennung des Datensatzes (`{DATASET_ID}`) zusammen mit den Filterregeln angeben, die mithilfe logischer Operatoren einen bestimmten Zeitraum definieren. Wenn ein Zeitraum definiert ist, wird jede angegebene Paginierung ignoriert und der gesamte Datensatz berücksichtigt.

Eine Liste der Filteroperatoren finden Sie nachfolgend:

- `eq()`: Gleich
- `gt()`: Größer als
- `ge()`: Größer oder gleich
- `lt()`: Niedriger als
- `le()`: Kleiner oder gleich
- `And()`: Logischer UND-Operator
- `Or()`: Logischer ODER-Operator

Die folgende Zelle filtert einen [!DNL ExperienceEvent] -Datensatz für Daten, die ausschließlich zwischen dem 1. Januar 2019 und dem 31. Dezember 2019 existierten.

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

## PySpark 3 Notebooks {#pyspark-notebook}

In der folgenden PySpark-Dokumentation werden die folgenden Konzepte beschrieben:

- [Initialisieren von sparkSession](#spark-initialize)
- [Daten lesen und schreiben](#magic)
- [Lokalen Dataframe erstellen](#pyspark-create-dataframe)
- [ExperienceEvent-Daten filtern](#pyspark-filter-experienceevent)

### Initialisieren von sparkSession {#spark-initialize}

Bei allen [!DNL Spark] 2.4 Notebooks müssen Sie die Sitzung mit dem folgenden Textbausteincode initialisieren.

```scala
from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()
```

### Verwenden von %dataset zum Lesen und Schreiben mit einem PySpark 3-Notebook {#magic}

Mit der Einführung von [!DNL Spark] 2.4 wird `%dataset` benutzerdefinierte Magie für die Verwendung in PySpark 3 ([!DNL Spark] 2.4) Notebooks bereitgestellt. Weitere Informationen zu magischen Befehlen, die im IPython-Kernel verfügbar sind, finden Sie in der [IPython magic-Dokumentation](https://ipython.readthedocs.io/en/stable/interactive/magics.html).


**Verwendung**

```scala
%dataset {action} --datasetId {id} --dataFrame {df} --mode batch
```

**Beschreibung**

Ein benutzerdefinierter [!DNL Data Science Workspace] magischer Befehl zum Lesen oder Schreiben eines Datensatzes aus einem [!DNL PySpark] Notebook ([!DNL Python] 3 Kernel).

| Name | Beschreibung | Erforderlich |
| --- | --- | --- |
| `{action}` | Der Aktionstyp, der für den Datensatz ausgeführt werden soll. Zwei Aktionen sind verfügbar: &quot;Lesen&quot;oder &quot;Schreiben&quot;. | Ja |
| `--datasetId {id}` | Wird verwendet, um die ID des zu lese- oder schreibenden Datensatzes anzugeben. | Ja |
| `--dataFrame {df}` | Der pandas-Dataframe. <ul><li> Wenn die Aktion &quot;read&quot;lautet, ist {df} die Variable, in der Ergebnisse des Datensatzlesevorgangs verfügbar sind (z. B. ein Dataframe). </li><li> Wenn die Aktion &quot;write&quot;lautet, wird dieser Dataframe {df} in den Datensatz geschrieben. </li></ul> | Ja |
| `--mode` | Ein zusätzlicher Parameter, der die Art des Lesens von Daten ändert. Zulässige Parameter sind &quot;batch&quot;und &quot;interaktiv&quot;. Standardmäßig ist der Modus auf &quot;batch&quot;eingestellt.<br> Es wird empfohlen, den &quot;interaktiven&quot;Modus zu verwenden, um die Abfrageleistung bei kleineren Datensätzen zu verbessern. | Ja |

>[!TIP]
>
>Überprüfen Sie die PySpark-Tabellen im Abschnitt [Notebook-Datenbeschränkungen](#notebook-data-limits) , um zu ermitteln, ob `mode` auf `interactive` oder `batch` eingestellt werden soll.

**Beispiele**

- **Beispiel lesen**: `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0 --mode batch`
- **Schreibbeispiel**: `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0 --mode batch`

>[!IMPORTANT]
>
> Das Zwischenspeichern von Daten mit `df.cache()` vor dem Schreiben von Daten kann die Notebook-Leistung erheblich verbessern. Dies kann hilfreich sein, wenn Sie einen der folgenden Fehler erhalten:
> 
> - Auftrag aufgrund von Staging-Fehler abgebrochen ... Kann nur RDDs mit derselben Anzahl von Elementen in jeder Partition komprimieren.
> - Remote RPC-Client getrennt und andere Speicherfehler.
> - Schlechte Performance beim Lesen und Schreiben von Datensätzen.
> 
> Weitere Informationen finden Sie im [Handbuch zur Fehlerbehebung](../troubleshooting-guide.md) .

Sie können die oben genannten Beispiele automatisch im JupyterLab-Buy mit der folgenden Methode generieren:

Wählen Sie im linken Navigationsbereich von JupyterLab die Registerkarte Datensymbol (unten hervorgehoben). Die Verzeichnisse **[!UICONTROL Datensätze]** und **[!UICONTROL Schemata]** werden angezeigt. Wählen Sie **[!UICONTROL Datensätze]** und klicken Sie mit der rechten Maustaste und wählen Sie dann die Option **[!UICONTROL Daten in Notebook schreiben]** aus dem Dropdown-Menü des Datensatzes aus, den Sie verwenden möchten. Unten im Notebook wird ein ausführbarer Code-Eintrag angezeigt.

- Verwenden Sie **[!UICONTROL Daten im Notebook durchsuchen]** , um eine Leselelle zu generieren.
- Verwenden Sie **[!UICONTROL Daten in Notebook schreiben]** , um eine Schreibzelle zu generieren.

![](../images/jupyterlab/data-access/pyspark-write-dataset.png)

### Lokalen Dataframe erstellen {#pyspark-create-dataframe}

Verwenden Sie SQL-Abfragen, um einen lokalen Dataframe mit PySpark 3 zu erstellen. Beispiel:

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
>Sie können auch ein optionales Seed-Beispiel angeben, z. B. einen booleschen withReplacement-, Double-Bruch- oder Long-Samen.

### [!DNL ExperienceEvent] Daten filtern {#pyspark-filter-experienceevent}

Zum Zugreifen auf und Filtern eines [!DNL ExperienceEvent] -Datensatzes in einem PySpark-Notebook müssen Sie die Datensatz-Identität (`{DATASET_ID}`), die IMS-Identität Ihrer Organisation und die Filterregeln angeben, die einen bestimmten Zeitraum definieren. Ein Filterzeitbereich wird mithilfe der Funktion `spark.sql()` definiert, wobei der Funktionsparameter eine SQL-Abfragezeichenfolge ist.

Die folgenden Zellen filtern einen [!DNL ExperienceEvent] -Datensatz nach Daten, die ausschließlich zwischen dem 1. Januar 2019 und dem 31. Dezember 2019 existierten.

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

## Scala Notebooks {#scala-notebook}

Die folgende Dokumentation enthält Beispiele für die folgenden Konzepte:

- [Initialisieren von sparkSession](#scala-initialize)
- [Datensatz lesen](#read-scala-dataset)
- [Schreiben in einen Datensatz](#scala-write-dataset)
- [Lokalen Dataframe erstellen](#scala-create-dataframe)
- [ExperienceEvent-Daten filtern](#scala-experienceevent)

### Initialisieren von SparkSession {#scala-initialize}

Bei allen Scala-Notebooks müssen Sie die Sitzung mit dem folgenden Textbausteincode initialisieren:

```scala
import org.apache.spark.sql.{ SparkSession }
val spark = SparkSession
  .builder()
  .master("local")
  .getOrCreate()
```

### Datensatz lesen {#read-scala-dataset}

In Scala können Sie `clientContext` importieren, um Platform-Werte abzurufen und zurückzugeben. Dadurch müssen keine Variablen wie `var userToken` definiert werden. Im unten stehenden Scala-Beispiel wird `clientContext` verwendet, um alle zum Lesen eines Datensatzes erforderlichen Werte abzurufen und zurückzugeben.

>[!IMPORTANT]
>
> Das Zwischenspeichern von Daten mit `df.cache()` vor dem Schreiben von Daten kann die Notebook-Leistung erheblich verbessern. Dies kann hilfreich sein, wenn Sie einen der folgenden Fehler erhalten:
> 
> - Auftrag aufgrund von Staging-Fehler abgebrochen ... Kann nur RDDs mit derselben Anzahl von Elementen in jeder Partition komprimieren.
> - Remote RPC-Client getrennt und andere Speicherfehler.
> - Schlechte Performance beim Lesen und Schreiben von Datensätzen.
> 
> Weitere Informationen finden Sie im [Handbuch zur Fehlerbehebung](../troubleshooting-guide.md) .

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
| df1 | Eine Variable, die den Pandas-Dataframe darstellt, der zum Lesen und Schreiben von Daten verwendet wird. |
| user-token | Ihr Benutzer-Token, das automatisch mit `clientContext.getUserToken()` abgerufen wird. |
| service-token | Ihr Service-Token, das automatisch mit `clientContext.getServiceToken()` abgerufen wird. |
| ims-org | Ihre Organisations-ID, die automatisch mit `clientContext.getOrgId()` abgerufen wird. |
| api-key | Ihr API-Schlüssel, der automatisch mit `clientContext.getApiKey()` abgerufen wird. |

>[!TIP]
>
>Überprüfen Sie die Scala-Tabellen im Abschnitt [Notebook-Datenbeschränkungen](#notebook-data-limits) , um zu ermitteln, ob `mode` auf `interactive` oder `batch` eingestellt werden soll.

Sie können das obige Beispiel automatisch im JupyterLab-Buy mit der folgenden Methode generieren:

Wählen Sie im linken Navigationsbereich von JupyterLab die Registerkarte Datensymbol (unten hervorgehoben). Die Verzeichnisse **[!UICONTROL Datensätze]** und **[!UICONTROL Schemata]** werden angezeigt. Wählen Sie **[!UICONTROL Datensätze]** aus, klicken Sie mit der rechten Maustaste und wählen Sie dann im Dropdown-Menü des Datensatzes, den Sie verwenden möchten, die Option **[!UICONTROL Daten in Notebook erkunden]** aus. Unten im Notebook wird ein ausführbarer Code-Eintrag angezeigt.
Und
- Verwenden Sie **[!UICONTROL Daten im Notebook durchsuchen]** , um eine Leselelle zu generieren.
- Verwenden Sie **[!UICONTROL Daten in Notebook schreiben]** , um eine Schreibzelle zu generieren.

![](../images/jupyterlab/data-access/scala-write-dataset.png)

### Schreiben in einen Datensatz {#scala-write-dataset}

In Scala können Sie `clientContext` importieren, um Platform-Werte abzurufen und zurückzugeben. Dadurch müssen keine Variablen wie `var userToken` definiert werden. Im unten stehenden Scala-Beispiel wird `clientContext` verwendet, um alle zum Schreiben in einen Datensatz erforderlichen Werte zu definieren und zurückzugeben.

>[!IMPORTANT]
>
> Das Zwischenspeichern von Daten mit `df.cache()` vor dem Schreiben von Daten kann die Notebook-Leistung erheblich verbessern. Dies kann hilfreich sein, wenn Sie einen der folgenden Fehler erhalten:
> 
> - Auftrag aufgrund von Staging-Fehler abgebrochen ... Kann nur RDDs mit derselben Anzahl von Elementen in jeder Partition komprimieren.
> - Remote RPC-Client getrennt und andere Speicherfehler.
> - Schlechte Performance beim Lesen und Schreiben von Datensätzen.
> 
> Weitere Informationen finden Sie im [Handbuch zur Fehlerbehebung](../troubleshooting-guide.md) .

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

| element | Beschreibung |
| ------- | ----------- |
| df1 | Eine Variable, die den Pandas-Dataframe darstellt, der zum Lesen und Schreiben von Daten verwendet wird. |
| user-token | Ihr Benutzer-Token, das automatisch mit `clientContext.getUserToken()` abgerufen wird. |
| service-token | Ihr Service-Token, das automatisch mit `clientContext.getServiceToken()` abgerufen wird. |
| ims-org | Ihre Organisations-ID, die automatisch mit `clientContext.getOrgId()` abgerufen wird. |
| api-key | Ihr API-Schlüssel, der automatisch mit `clientContext.getApiKey()` abgerufen wird. |

>[!TIP]
>
>Überprüfen Sie die Scala-Tabellen im Abschnitt [Notebook-Datenbeschränkungen](#notebook-data-limits) , um zu ermitteln, ob `mode` auf `interactive` oder `batch` eingestellt werden soll.

### Erstellen eines lokalen Dataframes {#scala-create-dataframe}

Um einen lokalen Dataframe mit Scala zu erstellen, sind SQL-Abfragen erforderlich. Beispiel:

```scala
sparkdf.createOrReplaceTempView("sparkdf")

val localdf = spark.sql("SELECT * FROM sparkdf LIMIT 1)
```

### [!DNL ExperienceEvent] Daten filtern {#scala-experienceevent}

Zum Zugreifen auf und Filtern eines [!DNL ExperienceEvent] -Datensatzes in einem Scala-Notebook müssen Sie die Datensatz-Identität (`{DATASET_ID}`), die IMS-Identität Ihrer Organisation und die Filterregeln angeben, die einen bestimmten Zeitraum definieren. Ein Filterzeitbereich wird mithilfe der Funktion `spark.sql()` definiert, wobei der Funktionsparameter eine SQL-Abfragezeichenfolge ist.

Die folgenden Zellen filtern einen [!DNL ExperienceEvent] -Datensatz nach Daten, die ausschließlich zwischen dem 1. Januar 2019 und dem 31. Dezember 2019 existierten.

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

In diesem Dokument wurden die allgemeinen Richtlinien für den Zugriff auf Datensätze mit JupyterLab-Notebooks erläutert. Ausführliche Beispiele zum Abfragen von Datensätzen finden Sie in der Dokumentation [Query Service in JupyterLab Notebooks](./query-service.md) . Weitere Informationen zum Erkunden und Visualisieren Ihrer Datensätze finden Sie im Dokument unter [Analysieren Ihrer Daten mit Notebooks](./analyze-your-data.md).

## Optionale SQL-Flags für [!DNL Query Service] {#optional-sql-flags-for-query-service}

In dieser Tabelle sind die optionalen SQL-Flags aufgeführt, die für [!DNL Query Service] verwendet werden können.

| **Markierung** | **Beschreibung** |
| --- | --- |
| `-h`, `--help` | Hilfemeldung anzeigen und beenden. |
| `-n`, `--notify` | Umschaltoption für das Benachrichtigen bei Abfrageergebnissen. |
| `-a`, `--async` | Bei Verwendung dieser Markierung wird die Abfrage asynchron ausgeführt und kann der Kernel freigeben werden, während die Abfrage ausgeführt wird. Seien Sie vorsichtig, wenn Sie Abfrageergebnisse Variablen zuweisen, da sie möglicherweise undefiniert sind, wenn die Abfrage noch nicht abgeschlossen ist. |
| `-d`, `--display` | Die Verwendung dieser Markierung verhindert, dass Ergebnisse angezeigt werden. |
